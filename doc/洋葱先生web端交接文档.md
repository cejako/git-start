# 洋葱先生Web端交接文档
### 导语：
> 现有项目基本都是基于前端本地构建的，如采用了grunt，fis3，webpack等等，所以如果要修改构建项目，电脑环境必须安装[nodejs](http://nodejs.cn/download/)以及npm(自行百度)

## 一、PC官网

### 代码地址:
> git clone http://54.222.212.169/allce231/home.git

### 项目构建：
* 在`/home`路径下，执行`npm install`，等待安装完所有的项目依赖包
* 阅读项目根目录下的`README.md`文件，最后一行的`rm -rf output && fis3 release prod -d ./output`即为构建生产环境的命令（可参考[fis3文档-发布](http://fis.baidu.com/fis3/docs/beginning/debug.html#%E5%8F%91%E5%B8%83)）
* 若要更改相应的环境，比如发布预发布环境，将上面命令中的`prod`改为`pre`即可（原因在下面会提到，在`fis-conf.js`配置文件可以发现对应配置）
* 上面构建命令执行完成之后，会在`/home`目录下生成`output`文件夹，该文件夹下所有内容即为发布内容，将所有文件上传至S3对应目录即可，上传方法后面统一讲到

### 文件结构：

![pc project](pc-1.jpeg =x400)

* **`css`**: 所有的样式文件，都是以[`sass`](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)语法书写的，除了`common.scss`和`index.scss`中包含的基本都是各页面的共同样式，其他文件都是根据页面来命名的
* **`images`**: 所有的图片等资源文件，也是以页面为单位拆分文件夹的
* **`js`**: 所有的脚本文件。其中，
	+ `lib`: 基本类库，如jquery等
	+ `module`: 各个共同模块化类，如`tab.js`控制各个Tab标签切换功能
	+ `view`: 每个页面的对应的模块
	
	> 采用的[requirejs](http://www.requirejs.cn/)进行模块化开发

* **`*.html`**: 页面文件，其中`header.html`为共同的头，`footer.html`为共同的底部。另外，每个文件含义分别如下：
	+ `index.html`: 首页
	+ `about.html`: 关于我们页
	+ `detail.html`: 新闻正文页
	+ `detail-product.html`: 产品信息页
	+ `detail-yb.html`: 月报页，其中**月报数据**位于*`/home/js/view/yuebaodata.js`*中，每次更新月报需在该文件中仿照原格式更新。
	+ `help.html`: 帮助页
	+ `huoqi.html`: 活期理财产品信息页
	+ `infomationdc.html`: 信息披露页
	+ **`inforegister.html`: 借款人注册页**
	+ `list.html`: 媒体中心页，**已废弃**，老版本
	+ `list-regular.html`: 媒体中心页
	+ `list-yb.html`: 月报列表页
	+ `onion.html`: 洋葱特色页
	+ `register.html`: 注册页
	+ `safe.html`: 安全保障页
	+ `share.html`: 邀请加息页
	+ `template.html`: 新闻列表页
	+ `tiyan.html`: 体验金注册页
	+ `xy.html`: 借贷合同模板页
	
	> 页面渲染模板是写在`<script type="text/template">...</script>`中，采用[`underscore`](http://underscorejs.org/)语法书写，同时脚本中通过`_.template(template)(data)`调用

* **`fis-conf.js`**: [*fis3*](http://fis.baidu.com/)的配置文件。配置含义需参考官方文档，简单来说，做了下面几个事情：
	+ 配置前面提到的`requirejs`全局配置
	+ `sass`编译成`css`以及压缩等
	+ 对`js`,`css`文件进行合并等
	+ 配置了多套环境分别对应的配置参数，根据不同的环境编译不同的版本，如前面提到的执行预发布环境发布命令`fis3 release `**`pre`**` -d ./output`，
		- `debug`: 开发环境
		- `test`: test1环境
		- `pre`: 预发布环境
		- `prod`: 生产环境
	
	> 针对预发布和生产环境，对构建代码配置了`hash`，即最终文件会被编译成 `[file]_md5.*`的名字，同时，无需担心`html`等文件中对应的文件引用错误，fis3会自动帮我们解决这个问题。
	
	> 同时，对于图片，脚本，样式等资源文件，添加了`domain`配置，是因为我们生产环境使用了**`CDN`**，运维对我们的的特定域名做了`CDN`配置，对应也有两套环境：
	>> * **预发布环境**： `http://preimage.51onion.com`
	>> * **生产环境**：`http://image.51onion.com`
	
* `README.md`: 一些基本命令提示，不是很完整
* `package.json`: 项目依赖配置文件
* `.gitignore`: git提交忽略文件配置