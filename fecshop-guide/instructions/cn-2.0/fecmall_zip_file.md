Fecmall Zip压缩包文件
==========

> zip文件的上传，下载，解压zip文件等


### Fecmall Zip压缩包文件处理

zip文件的处理类：`Yii::$service->helper->zipFile`


### Zip压缩包文件的解压


使用函数：`Yii::$service->helper->zipFile->unzip()`

### Zip压缩包文件的上传


函数：`Yii::$service->helper->zipFile->saveUploadZip($FILE)`


使用例子：

1.html部分


```
<div class="content" style="min-height:60px;">
                                    
    <button style="margin-top:25px;" onclick="getElementById('inputthumbnail_zip').click()" class="scalable" type="button" title="Duplicate" id=""><span><span><span>上传Zip压缩包</span></span></span></button>

    <input type="file"  id="inputthumbnail_zip" style="height:0;width:0;z-index: -1; position: absolute;left: 10px;top: 5px;"/>
    <span style="width:200px;display:inline-block;">
        <a style="display:<?= $downloadZipUrl ? 'block' :   'none' ?>;margin-left:20px;color:#468fa2;width:200px;" class="download_zip" href="<?= $downloadZipUrl ?  $downloadZipUrl :   '' ?>">下载zip文件</a>
    </span>
</div>



$("#inputthumbnail_zip").change(function(){
    var data = new FormData();
    var increment_id = '100000001';
    $.each($('#inputthumbnail_zip')[0].files, function(i, file) {
        data.append('upload_file', file);
    });
    data.append('increment_id', increment_id);
    data.append("<?= CRequest::getCsrfName() ?>", "<?= CRequest::getCsrfValue() ?>");
    $.ajax({
        url:'<?= Yii::$service->url->getUrl('customer/childaccount/uploadzipfile'); ?>',
        type:'POST',
        data:data,
        async:false,
        dataType: 'json', 
        timeout: 80000,
        cache: false,
        contentType: false,		//不可缺参数
        processData: false,		//不可缺参数
        success:function(data, textStatus){
            if(data.return_status == "success"){
                alert('upload zip success');
                var zipUrl = "<?= Yii::$service->url->getUrl('customer/childaccount/downloadzipfile') ?>?increment_id" + increment_id;
                
                $(".download_zip").attr("href", zipUrl);
                $(".download_zip").show();
            }
        },
        error:function(){
            alert('<?= Yii::$service->page->translate->__('Upload Error') ?>');
        }
    });
});

```

php部分，获取zip文件，并进行保存，保存后台相对文件路径是`$zipSavedRelativePath`

```
$zipSavedRelativePath = Yii::$service->helper->zipFile->saveUploadZip($_FILES['upload_file']);
```




### Zip压缩包文件的下载


使用函数：`Yii::$service->helper->zipFile->getDownloadfile($zipFile)`

$zipFile是相对文件路径（上传zip返回的相对路径`$zipSavedRelativePath`）


















