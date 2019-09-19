Api- 得到Page信息
================

> vue page页面，得到page信息的api,譬如页面：http://demo.fancyecommerce.com/#/cms/page/about-us

URL: `/cms/article/index`

格式：`json`

方式：`get`


一：请求部分
---------

#### 1.Request Header


| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 必须        |   String     | 从localStorage取出来的值，识别用户登录状态的标示，用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |
| fecshop-currency  | 必须        |   String     | 从localStorage取出来的值，当前的货币值  |
| fecshop-lang      | 必须        |   String     | 从localStorage取出来的值，当前的语言code  |


#### 2.Request Body Form-Data：


| 参数名称        | 是否必须    |  类型       |  描述     |
| ----------------| -----:      | :----:      |:----:     |
| url_key         | 必须        |   String     | 从URL中取的page_key，这个是服务端从数据库查询page信息的唯一key   |

**请求参数示例如下：**

```
{
    url_key:"about-us"
}
```

二：返回部分
----------

#### 1.Reponse Header

| 参数名称          | 是否必须    |  类型        |  描述     |
| ------------------| -----:      | :----:       |:----:     |
| access-token      | 选填        |   String     | 用户登录成功，服务端返回access-token，VUE保存到localStorage中，在下一次请求从localStorage取出来放到request header中   |

#### 2.Reponse Body Form-Data：

格式：`json`

| 参数名称        | 是否必须    |  类型       |  描述        |
| ----------------| -----:      | :----:      |:----:        | 
| code            | 必须        |   Number    | 返回状态码，200 代表完成，完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) |
| message         | 必须        |   String    | 返回状态字符串描述  |
| data            | 必须        |   Array     | 返回详细数据        |

#### 3.参数code所有返回状态码：（完整的返回状态码详细参看:[Api- 状态码](fecshop-server-return-code.md) ）

| code Value      |        描述                                        |
| ----------------| --------------------------------------------------:| 
| 200             | 成功状态码                                         |  
| 1600001         | Article: 文章不存在                  | 

 
#### 4.返回数据举例：

```
{
    "code": 200,
    "message": "process success",
    "data": {
        // page 内容
        "content": "<span id=\"result_box\" lang=\"fr\"><span title=\"Fecshop 全称为Fancy ECommerce Shop，是基于php Yii2框架之上开发的一款优秀的开源电商系统， 遵循OSL3.0开源协议，Fecshop支持多语言，多货币，架构上支持pc，手机web，手机app\">Fecshop appelé Fancy ECommerce Shop, est un système open source basé sur le cadre Yii2 fournisseur d'électricité de php pour le développement d'un protocole open source excellente OSL3.0 de suivi, Fecshop support multi-langue, multi-devises, support pour PC, téléphone mobile web, app de téléphone sur l'architecture </span><span title=\"，和erp对接等入口，您可以免费快速的定制和部署属于您的电商系统。\">et l'entrée erp d'accueil, vous pouvez rapidement personnaliser et déployer la partie libre de votre système de fournisseur d'électricité. </span><span title=\"预计到2017-05月份，完成appfront（pc前端web），appadmin（后台） 命令控制台这几个入口，目前appfront和appadmin功能已经打通，但是，系统的代码bug需要排查， 代码需要优化，不建议\">Horaires 2017--05 mois, appfront complète (pc frontal Web), appadmin (arrière-plan) console de commande que plusieurs entrées, et est actuellement fonction de appadmin appfront a été ouvert, cependant, le système a besoin pour résoudre le code bug, le code doit être optimisé, pas recommandé </span><span title=\"应用到生产环境，如果您一定要在生产环境中用，可以联系我，我会随时技术支持, Terry从事外贸电商6年来， 用了不少开源电商系统，譬如magento， 发现开源框架都有\">appliquée à l'environnement de production, si vous devez utiliser dans un environnement de production, vous pouvez me contacter, je vais garder le soutien technique, Terry engagé dans le fournisseur d'électricité du commerce extérieur en six ans, avec beaucoup d'open-source système de fournisseur d'électricité, par exemple, magento, framework open source a trouvé </span><span title=\"一定的诟病，在并发方面差，后期扩展，业务发展后期重构难， 尤其是现在的移动端的发展，多入口的电商模式占据主流， 性能方面的要求越来越高，Fecshop基于Yii2的高效\">certaines critiques, en termes de la différence entre simultanée, post-expansion, le développement des affaires, post-reconstruction difficile, surtout maintenant que le développement de terminal mobile, les fournisseurs d'entrée électricité multi-mode occupent le grand public, les exigences de performance de plus en plus élevés, Fecshop sur la base du Yii2 efficace </span><span title=\"框架，在此基础上进一步封装，加入了service层和block层，数据库采用了nosql和mysql结合的方式， 关系型表放到mysql中，譬如优惠券，购物车，订单等， 非关系型数据表\">cadre, sur la base d'une nouvelle encapsulé à se joindre à la couche de service et la couche de bloc, la base de données utilise une combinaison de nosql et mysql, tables mysql relationnelles placés dans, par exemple, des coupons, panier, commander, table de données non relationnelle </span><span title=\"（非关系型代表不会出现多表强事务类型操作） 放到mongodb中， 缓存用redis，搜索目前用的是mongodb的FullTextSearch功能， 支持一些主流语言的分词与搜索，不过目前中文搜索不支持分词\">(représentants non-relationnelles ne sera pas un multi-table fortement opération de type de transaction) dans mongodb, le cache avec Redis, recherche actuellement en utilisant mongodb de FullTextSearch propose le support principal de recherche de mot de la langue, mais le courant Recherche chinois ne prend pas en charge mot </span><span title=\"， 后期会扩展ElasticSearch来进行搜索（ElasticSearch有中文插件，安装后支持中文分词）。\">, celui-ci étendra ElasticSearch à la recherche (ElasticSearch un bouchon chinois après support d'installation mot chinois). </span><span title=\"总之，Fecshop目前的定位是为了让程序员们有一个方便学习，扩展，开发的电商框架系统， 如果您发现有哪些代码结构可以优化，调整，或者您有更加合理的建议，可以发送到邮箱\">En bref, la position actuelle Fecshop est de permettre aux programmeurs d'avoir un facile à apprendre, l'expansion et le développement du système de cadre de fournisseur d'électricité, si vous voyez ce que vous pouvez optimiser la structure du code, le réglage, ou si vous avez une proposition plus raisonnable peut être envoyé à la boîte aux lettres </span><span title=\"： 2358269014@qq.com。\">: 2358269014@qq.com.</span></span>",
        // 创建时间
        "created_at": 1489676914,
        // page title
        "title": "about us"
    }
}
```