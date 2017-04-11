Fecshop 多模板机制
==================

> fecshop 的多模板机制：有多个模板路径，根据顺序的不同，优先级不同，
其中本地模板路径优先级最高，第三方模板路径次之（第三方模板路径可以是多个路径，这个是一个数组），
fecshop的模板路径优先级最低，如果一个view文件，譬如 cms/home/index.php 在高优先级
的模板路径中找到，就会退出，不会继续到低优先级的模板路径中查找view文件。

### 多模板机制的作用

fecshop是一个可持续升级的商城系统，涉及到新功能的开发，可能涉及到view前端文件的改变，
因此，view文件必须包含在库包中，但是，用户为了前台页面的美观，就必然要修改
view文件，以及js和css文件，这样就会产生矛盾，用户需要二次开发修改的文件，不允许修改，
为了解决这个矛盾，引入了多模板机制。

### 多模板原理

> fecshop的多模板，尽量在模板中使用，非模块中现在还没有测试，

多模板机制是由 page服务的子服务theme来完成的，
@fecshop\services\page\Theme,打开这个文件可以看到：

```php
public $localThemeDir;  # 二次开发用户本地路径。
public $thirdThemeDir;	# 第三方模板路径。
public $fecshopThemeDir ; # fecshop模板路径。
```
### 1.多模板的三个路径变量
$localThemeDir 和  $thirdThemeDir 是在文件：@app\config\fecshop_local_services\stores.php
中定义的（当然也可能是在其他的文件中定义，不过最终都是给page/theme子服务配置参数），打开这个文件可以看到

```php

<?php
   return [
   'store' => [
		'class' => 'fecshop\services\Store',
		'stores' => [
			# store_code ,define by domain and fold.
			# 语言必须在fecshoplang中定义，否则将无法得到语言属性。
			# 在添加store的时候，必须查看 添加的语言在 fecshoplang中是否定义。
			'fecshop.appfront.fancyecommerce.com' => [
				'language' 		=> 'en_US',
				'languageName' 	=> 'English',
				
				//'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/fr' => [
				'language' 		=> 'fr_FR',
				'languageName' 	=> 'Français',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
			],
			'fecshop.appfront.fancyecommerce.com/es' => [
				'language' 		=> 'es_ES',
				'languageName' 	=> 'Español',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'USD',
			],
			'fecshop.appfront.fancyecommerce.com/cn' => [
				'language' 		=> 'zh_CN',
				'languageName' 	=> '中文',
				'localThemeDir'	=> '@appfront/theme/terry/theme01',
				'thirdThemeDir'	=> [],
				'currency' 		=> 'RMB',
			],
		],
		
	],
			
];

```

也就是在各个store中定义，当前store的[[localThemeDir]]  和 [[thirdThemeDir]]。
然后在store service 的[[bootstrap()]]中可以看到下面的代码：

```php
/**
 * set local theme dir.
 */ 
if(isset($store['localThemeDir']) && $store['localThemeDir']){
	Yii::$service->page->theme->localThemeDir = $store['localThemeDir'];
}
/**
 * set third theme dir.
 */ 
if(isset($store['thirdThemeDir']) && $store['thirdThemeDir']){
	Yii::$service->page->theme->thirdThemeDir = $store['thirdThemeDir'];
}
```

也就是在初始化的时候，通过将store的 [[localThemeDir]] 和 [[thirdThemeDir]]，赋值于
page的子服务theme中，完成对[[page->theme]]服务的初始化。

下面是page的子服务theme的三个参数的详细解说:

- 变量：[[localThemeDir]]:  本地路径,这个在配置文件中定义，
- 变量：[[thirdThemeDir]]:  对于第三方，这个需要安装后，在这里配置上即可。
- 变量：[[fecshopThemeDir]]: 这个变量在这里定义是无效的，会在初始化的时候被覆盖，下面我们找一下这个配置在哪里设置，看下面的代码.

```
class AppfrontController extends FecController
{
	public $blockNamespace;
	/**
	 * init theme component property : $fecshopThemeDir and $layoutFile
	 * $fecshopThemeDir is appfront base theme directory.
	 * layoutFile is current layout relative path.
	 */
	public function init(){
		if(!Yii::$service->page->theme->fecshopThemeDir){
			Yii::$service->page->theme->fecshopThemeDir = Yii::getAlias(CConfig::param('appfrontBaseTheme'));
		}
	...
```

可以看到，[[Yii::$service->page->theme->fecshopThemeDir]] 是由配置 [[appfrontBaseTheme]] 来决定的，下面我们去找配置
在文件 [[@fecshop\app\appfront\config\appfront.php]] 中可以看到如下配置：

```
return [
	'modules'=>$modules,
	/* only config in front web */
	'bootstrap' => ['store'],
	'params'	=> [
		/* appfront base theme dir   */
		'appfrontBaseTheme' 	=> '@fecshop/app/appfront/theme/base/front',
		'appfrontBaseLayoutName'=> 'main.php',
	],
	
```

也就是 'appfrontBaseTheme' 的配置路径为：'@fecshop/app/appfront/theme/base/front'

经过上面，我们可以得到三个变量是如何 赋值的。


###2.代码跟踪

在初始化的时候，上面三个路径都全部赋值，当寻找view文件的时候是如何寻找的呢？下面
我们来跟踪代码。

我们在appfront中所有的controller文件，都是继承于[[fecshop\app\appfront\modules\AppfrontController]]  
,在这个文件中可以看到render函数被重写了。

```php

/**
	 * @property $view|String , (only) view file name ,by this module id, this controller id , generate view relative path.
	 * @property $params|Array,
	 * 1.get exist view file from mutil theme by theme protity.
	 * 2.get content by yii view compontent  function renderFile()  , 
	 */
	public function render($view, $params = []){
		$viewFile = Yii::$service->page->theme->getViewFile($view);
		$content = Yii::$app->view->renderFile($viewFile, $params, $this);
        return $this->renderContent($content);
    }

```
也就是通过[[Yii::$service->page->theme->getViewFile($view)]],找到view文件，下面
，通过renderFile，将内容画出来，那么关键就是查看[[Yii::$service->page->theme->getViewFile($view)]]的实现原理


下面我们查看[[Yii::$service->page->theme->getViewFile($view)]]的实现原理：

fecshop\services\page\Theme:

```

/**
	 * find theme file by mutil theme ,if not find view file  and $throwError=true, it will throw InvalidValueException.
	 */ 
	public function getViewFile($view,$throwError=true){
		$view = trim($view);
		if(substr($view,0,1) == '@'){
			return Yii::getAlias($view);
		}
		$relativeFile = '';
		$module = Yii::$app->controller->module;
		if($module && $module->id){
			$relativeFile = $module->id.'/';
		}
		$relativeFile .= Yii::$app->controller->id.'/'.$view.'.php';
		$absoluteDir = Yii::$service->page->theme->getThemeDirArr();
		foreach($absoluteDir as $dir){
			if($dir){
				$file = $dir.'/'.$relativeFile;
				if(file_exists($file)){
					return $file;	
				}
			}
		}
		/* not find view file */
		if($throwError){
			$notExistFile = [];
			foreach($absoluteDir as $dir){
				if($dir){
					$file = $dir.'/'.$relativeFile;
					$notExistFile[] = $file;
				}
			}
			throw new InvalidValueException('view file is not exist in'.implode(',',$notExistFile));
		}else{
			return false;
		}
	}
	
```
可以看到[[$absoluteDir = Yii::$service->page->theme->getThemeDirArr();]],
找出来所有的模板路径，通过优先级依次和view文件的相对路径拼起来，
然后查看文件是否存在，存在则返回，那么我们查看这个函数

```
public function getThemeDirArr(){
		if(!$this->_themeDirArr){
			$arr = [];
			if($localThemeDir = Yii::getAlias($this->localThemeDir)){
				$arr[] = $localThemeDir;
			}
			
			$thirdThemeDirArr = $this->thirdThemeDir;
			if(!empty($thirdThemeDirArr) && is_array($thirdThemeDirArr)){
				foreach($thirdThemeDirArr as $theme){
					$arr[] = Yii::getAlias($theme);
				}
			}
			$arr[] = Yii::getAlias($this->fecshopThemeDir);
			$this->_themeDirArr = $arr;
		}
		return $this->_themeDirArr;
	}
```

 可以看到就是按照上面的三个变量得到的多模板系统的所有模板路径
- 参数：[[localThemeDir]]:  本地路径,这个在配置文件中定义，
- 参数：[[thirdThemeDir]]:  对于第三方，这个需要安装后，在这里配置上即可。
- 参数：[[fecshopThemeDir]]: 下面我们找一个这个配置在哪里设置，看下面的代码.

 排在数组前面的，优先级最高，在[[getViewFile()]]函数中优先判断是否存在，
 优先级最高的先返回，然后就得到了view文件。
 
 然后返回view文件，这就是多模板机制的原理。
 
### 多模板的layout文件的原理

> 多模板的layout文件和view文件类似。

当前的layout的相对路径由[[Yii::$service->page->theme->layoutFile]]
得到，当前的layout多模板路径和上面view文件类似，
多模板路径和view文件拼起来的路径，查看文件是否存在，存在则返回。

Example：

在 @fecshop\app\appfront\modules\Cms\Module的init方法，可以看到：
[[Yii::$service->page->theme->layoutFile = 'home.php';]]
，layout默认设置为home.php文件，
如果不设置，在
在AppfrontController.php中会执行下面的代码：

```
public function init(){
		if(!Yii::$service->page->theme->fecshopThemeDir){
			Yii::$service->page->theme->fecshopThemeDir = Yii::getAlias(CConfig::param('appfrontBaseTheme'));
		}
		if(!Yii::$service->page->theme->layoutFile){
			Yii::$service->page->theme->layoutFile = CConfig::param('appfrontBaseLayoutName');
		}
```

参数[[Yii::$service->page->theme->layoutFile]],会被设置。

通过上面，我们基本明白了多模板系统view 和 layout 的加载原理


### 多模板系统的js和css的加载原理。

多模板的js 和 css 是由  page服务的子服务asset完成的。

我们先看@fecshop\app\appfront\theme\base\front\layouts\home.php里面的代码：

```
<?php
\Yii::$service->page->asset->register($this);
?>
```

打开文件@fecshop\services\page\Asset

```
public function register($view){
		$assetArr = [];
		$themeDir = Yii::$service->page->theme->getThemeDirArr();
		if( is_array($themeDir) && !empty($themeDir)){
			if( is_array($this->jsOptions) && !empty($this->jsOptions)){
				foreach($this->jsOptions as $jsOption){
					if( isset($jsOption['js']) && is_array($jsOption['js']) && !empty($jsOption['js'])){
			
						foreach($jsOption['js'] as $jsPath){
							foreach($themeDir as $dir){
								$dir = $dir.'/'.$this->defaultDir.'/';
								$jsAbsoluteDir = $dir.$jsPath;
								if(file_exists($jsAbsoluteDir)){
										$assetArr[$dir]['jsOptions'][] = [
										'js' 		=>  $jsPath,
										'options' 	=>  $this->initOptions($jsOption['options']),
									];
									break;
								}
							}
						}
					}
				}	
			}
			
			if( is_array($this->cssOptions) && !empty($this->cssOptions)){
				foreach($this->cssOptions as $cssOption){
					if( isset($cssOption['css']) && is_array($cssOption['css']) && !empty($cssOption['css'])){
						foreach($cssOption['css'] as $cssPath){		
							foreach($themeDir as $dir){
								$dir = $dir.'/'.$this->defaultDir.'/';
								$cssAbsoluteDir = $dir.$cssPath;
								if(file_exists($cssAbsoluteDir)){
									$assetArr[$dir]['cssOptions'][] = [
										'css' 		=>  $cssPath,
										'options' 	=>  $this->initOptions($cssOption['options']),
									];
									break;
								}
							}
						}
					}
				}	
			}
		}
		if(!empty($assetArr)){
			foreach($assetArr as $fileDir=>$as){
				$cssConfig = $as['cssOptions'];
				$jsConfig = $as['jsOptions'];
				$publishDir = $view->assetManager->publish($fileDir);
				if(!empty($jsConfig) && is_array($jsConfig)){
					foreach($jsConfig as $c){
						$view->registerJsFile($publishDir[1].'/'.$c['js'],$c['options']);
					}
				}
				if(!empty($cssConfig) && is_array($cssConfig)){
					foreach($cssConfig as $c){
						$view->registerCssFile($publishDir[1].'/'.$c['css'],$c['options']);
					}
				}
			}
		}
	}
```

大致原理和上面的view文件类似，依次在多模板路径下的assets文件夹中查找js或者css文件
如果找到，就会得到文件路径，使用$view->registerJsFile 和 $view->registerCssFile
将js 和css 注册到view中，这样在view中的[[<?php $this->endPage() ?>]]
,就可以将js和css输出了，另外，通过方法[[$view->assetManager->publish($fileDir)]]将文件复制到web下面的assets，
,这样就完成了js和css在多模板中通过多模板的优先级路径加载了。

您可以通过配置page的子服务asset：

```
'asset' => [
	'jsOptions'	=> [
		# js config 1
		[
			'options' => [
				'position' =>  'POS_END',
			//	'condition'=> 'lt IE 9',
			],
			'js'	=>[
				'js/jquery-3.0.0.min.js',
				'js/js.js',
			],
		],
		# js config 2
		[
			'options' => [
				'condition'=> 'lt IE 9',
			],
			'js'	=>[
				'js/ie9js.js'
			],
		],
	],
	# css config
	'cssOptions'	=> [
		# css config 1.
		[
			'css'	=>[
				'css/style.css',
				'css/ie.css',
			],
		],
		
		# css config 2.
		[
			'options' => [
				'condition'=> 'lt IE 9',
			],
			'css'	=>[
				'css/ltie9.css',
			],
		],
	],
],
```

来进行配置css和js文件，配置完成后，会在多模板路径中通过
优先级加载。

到这里多模板的原理已经完全说明白了。


