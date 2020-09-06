# Typora+PicGo-Core+SMMS/github/gitee实现图片自动上传图床详细说明

[TOC]

## **一、安装Typora:**

 1、在官网<https://www.typora.io/>可以下载Typora的安装包程序，附上快速通道，直接点击下载[官方安装包-直接点击下载x64即可](https://www.typora.io/windows/typora-setup-x64.exe?：)

2、双击安装包程序进行安装，日常同意+选择安装路径等等这些，比较简单不附图；

![双击安装包进行安装](https://gitee.com/mali8908/pictures/raw/master/img/20200905132927.png)

![等待安装完成即可](https://gitee.com/mali8908/pictures/raw/master/img/20200905132259.png)

3、安装完成之后，就可以正常使用typora写markdows文档了，打开看看，可以设置进行一系列设置，当在文档里插入图片，最后将文章上传发布到网站、论坛、博客等，图片是直接上传不了的，比如在博客里，还得手工一张一张的去粘贴图片，太麻烦。如何把整篇写好的文档，直接进行发布在网络上，还不影响图片的展示。那就是接下来要完成的，把文档里的图片直接上传到图床，这样文章里的图片到哪里都不会丢失，废话多余，直奔主题！

## **二、Typora+PicGo-Core+SMMS实现图片上传到SMMS图床：**

1、打开typora-偏好设置-图像进行如下设置；

![image-20200905134050961](https://gitee.com/mali8908/pictures/raw/master/img/20200905134054.png)

补充自我理解解释说明：上传服务还有其他选项，这里介绍PicGo-Core(command line)、PicGo(app)的区别，PicGo-Core(command line)使用时直接调用相关进程就可以实现图片的上传，消耗资源较小，也不用下载其他APP，PicGo(app)就得下载这个软件，在该软件里设置好上传图片的配置，我不喜欢使用这么繁琐的东西，所以上传服务直接使用PicGo-Core(command line)，其实它俩是一个东西，一个是通过命令行，一个是通过软件GUI界面；

![image-20200905134428857](https://gitee.com/mali8908/pictures/raw/master/img/20200905134431.png)

2、上传服务选择PicGo-Core(command line)，然后点击下载或更新，等待下载完成；

![image-20200905135249704](https://gitee.com/mali8908/pictures/raw/master/img/20200905135252.png)

点击同意并下载,下载的速度可能会有点慢；

![image-20200905135337420](https://gitee.com/mali8908/pictures/raw/master/img/20200905135341.png)

3、下载完成后，点击打开配置文件，Typora**默认**使用的图床是SMMS；

![打开配置文件](https://gitee.com/mali8908/pictures/raw/master/img/20200905143704.png)

此步可忽略：当你点击打开配置文件时，弹出如下提示时，没关系的，直接确定就可以

![image-20200905150935832](https://gitee.com/mali8908/pictures/raw/master/img/20200905150938.png)

将以下的配置复制粘贴到打开的配置文件中即可；

```
{
  "picBed": {
    "uploader": "smms",  //传图床为 SM.MS,
    "smms": {
      "token": "***************"  //这儿的token换成你自己生成的 sm.ms 的token，看如下获取方法
    }
  },
  "picgoPlugins": {}
}
```

SMMS图床：永久存储，图片链接支持https，可以删除上传的图片，提供多种图片链接格式，

每个图片最大5M，单次最多上传10张 。

**SMMS图床的token获取：**

官网:<https://sm.ms/>进去注册一个自己的账号

然后获取tocken:<https://sm.ms/home/apitoken>，获取后粘贴到以上配置文档的相应位置即可

![获取smms图床的tocken](https://gitee.com/mali8908/pictures/raw/master/img/20200905150215.png)

4、保存以上SMMS图床的配置后，重新打开typora,试着上传一张图片看看；

![上传smsm图床成功](https://gitee.com/mali8908/pictures/raw/master/img/20200905143259.png)

也可以直接点击验证图片上传选项；

![点击验证图片上传选项](https://gitee.com/mali8908/pictures/raw/master/img/20200905161603.png)

![验证](https://gitee.com/mali8908/pictures/raw/master/img/20200905161413.png)

可以上传成功，但是你想把这篇文档发在博客上，对以上文档保存，试试导入到博客上，图片可以显示出来不，通过导smsms入此markdown文档后会发现外链图片转存失败，可能是这个smms图床站点有这种机制导致，所以改用github图床；

![image-20200905143625698](https://gitee.com/mali8908/pictures/raw/master/img/20200905143628.png)

## **三、Typora+PicGo-Core+github实现图片上传到github图床：**

1、为后续顺利安装插件，先安装好node.js环境；到node.js官网:<https://nodejs.org/en/>下载或者点击<https://nodejs.org/dist/>进去可选择各版本进行相应的下载，懒人-快车通道下载:[node-v12.18.3-x64.msi](https://nodejs.org/dist/v12.18.3/node-v12.18.3-x64.msi)

![image-20200905163038568](https://gitee.com/mali8908/pictures/raw/master/img/20200905163046.png)

双击安装，最好一路下一步，安装完成；

![安装node.js环境](https://gitee.com/mali8908/pictures/raw/master/img/20200905163222.png)

![image-20200905163305433](https://gitee.com/mali8908/pictures/raw/master/img/20200905163308.png)

![image-20200905163419111](https://gitee.com/mali8908/pictures/raw/master/img/20200905163426.png)

![image-20200905163653227](https://gitee.com/mali8908/pictures/raw/master/img/20200905163656.png)

![image-20200905163750076](https://gitee.com/mali8908/pictures/raw/master/img/20200905163753.png)

![image-20200905163813316](https://gitee.com/mali8908/pictures/raw/master/img/20200905163816.png)

![image-20200905163924500](https://gitee.com/mali8908/pictures/raw/master/img/20200905163930.png)

![image-20200905164044141](https://gitee.com/mali8908/pictures/raw/master/img/20200905164048.png)

检查PATH环境变量是否配置了Node.js，在cmd窗口输入命令“**path**”查下是否有node.js路径；

![image-20200905164308941](https://gitee.com/mali8908/pictures/raw/master/img/20200905164312.png)

我们可以看到PATH环境变量已经包含node.js,在cmd窗口继续输入命令“**node --version**”会输出版本信息，为以下安装插件的node.js环境就准备完毕了！

![image-20200905164531517](https://gitee.com/mali8908/pictures/raw/master/img/20200905164535.png)

2、安装插件；

分别安装**gitee-uploader**，**github-plus**插件来支持gitee，github图床上传，首先确认picdo-core安装的位置在那儿，如下所示，我的路径是在C:\Users\Administrator\AppData\Roaming\Typora\picgo\win64\picgo.exe；

![image-20200905165059844](https://gitee.com/mali8908/pictures/raw/master/img/20200905165102.png)

然后在cmd窗口进入到picgo安装的路径并执行安装插件（此处就用到了以上node.js环境支持）；

共需要用到以下命令；

```
cd C:\Users\Administrator\AppData\Roaming\Typora\picgo\win64

.\picgo.exe install gitee-uploader   //gitee的插件

.\picgo.exe install github-plus   //github的插件

1.picgo use uploader  //选择使用uploader

2.picgo set uploader  //设置uploader=等于设置config.json
```

Github-plus插件安装成功；

![github插件安装成功](https://gitee.com/mali8908/pictures/raw/master/img/20200905170851.png)

配置config.json，先直接回车，各字段填写什么下面会给出对应解释；

![配置config.json](https://gitee.com/mali8908/pictures/raw/master/img/20200905171415.png)

设置使用那个uploader上传，这里选择Github,回车；

![image-20200905171813456](https://gitee.com/mali8908/pictures/raw/master/img/20200905171817.png)

设置config.json说明,可以直接粘贴复制到配置文件中，对照修改为自己的信息即可；

![image-20200905210156012](https://gitee.com/mali8908/pictures/raw/master/img/20200905210200.png)

设置Github说明：

```
{
   "picBed": {
     "current": "github",
     "github": {
       "repo": "Github用户名/仓库名",     //写自己的Github用户名/仓库名
       "branch": "master",  //默认为主分支
       "token": "------------------------------------------------",  //写自己github的tocken
       "path": "img/",  //可以不用修改，默认在仓库下创建img文件夹
       "customUrl": "https://github.com/自己Github用户名/仓库名"   
     },
     "uploader": "github",  //不用修改
     "transformer": "path"   //不用修改
   },
   "picgoPlugins": {
     "picgo-plugin-gitee-uploader": true,  //不用修改
     "picgo-plugin-smms-user": true     //不用修改
   }
 }
```

补充说明获取github的token,token只能查看一次，所以请一定要保存好，方便后期使用；

访问:<https://github.com/settings/tokens>生成自己Github的token

点击“Generate new token”;

![image-20200905221123058](https://gitee.com/mali8908/pictures/raw/master/img/20200905221127.png)

输入用户密码登录；

![image-20200905221317319](https://gitee.com/mali8908/pictures/raw/master/img/20200905221327.png)

![image-20200905221449879](https://gitee.com/mali8908/pictures/raw/master/img/20200905221456.png)

拉到最底下,点击Generate token就生成了token,粘贴复制到配置文件中；

![image-20200905221554108](https://gitee.com/mali8908/pictures/raw/master/img/20200905221558.png)

当你设置好以上信息后，重新打开ytypora，上传图片可能会出现以下情况；①上传成功了但是在typora看不了                        ②上传不成功报错

![上传本地看不了图片](https://gitee.com/mali8908/pictures/raw/master/img/20200905205609.png)

①以上情况个人只有一次是上传成功，并且可以显示出来，再尝试上传一直就是上图的情况，百度了下原因，很可能是网络问题，github不使用代理去访问也比较慢，如果直接修改pc的host文件，添加域名对应IP，个人不想采取此方法.后来尝试使用免费CDN:<https://www.jsdelivr.com/>来加速访问Github的速度；

只需在配置文件中把 "customUrl": "https://github.com/自己Github用户名/仓库名" 设置为 "customUrl": "https://cdn.jsdelivr.net/gh/用户名/仓库名@版本号" 就行（创建的仓库要发布版本）, 创建仓库并发布如下展示；

![github-新建仓库-1](https://gitee.com/mali8908/pictures/raw/master/img/20200905215041.png)

![image-20200905215244785](https://gitee.com/mali8908/pictures/raw/master/img/20200905215248.png)

新建好的仓库需要在该仓库下再新建一个文件夹，就能正常使用了，然后在新仓库下建版本；

![image-20200905215644306](https://gitee.com/mali8908/pictures/raw/master/img/20200905215648.png)

![image-20200905220042476](https://gitee.com/mali8908/pictures/raw/master/img/20200905220046.png)

然后这样设置后，我就第一次上传成功并在typora能够查看图片，再多次上传就又不行了，具体可能因人而异了，这里只做记录而已。

![image-20200905212256423](https://gitee.com/mali8908/pictures/raw/master/img/20200905212259.png)

②出现如上的上传失败的信息，95%是配置有误，仔细回头排查下！

经过以上折腾，我没有如愿以偿的实现自己的需求，所以又改用Gitee图床试试；没想到，成功的实现了我的需求，以下步骤说明和上面的步骤大同小异；

## **四、Typora+PicGo-Core+Gitee实现图片上传到gitee图床：**

1、首先先安装gitee-uploader插件（前提是需要node.js环境的支持，以上已给出具体安装步骤）

同样在cmd窗口输入以下命令；

```
cd C:\Users\Administrator\AppData\Roaming\Typora\picgo\win64

.\picgo.exe install gitee-uploader   //gitee的插件

.\picgo.exe install super-prefix    //gitee的插件
```

![image-20200905223911767](https://gitee.com/mali8908/pictures/raw/master/img/20200905223917.png)

修改配置文件；

![image-20200905224020562](https://gitee.com/mali8908/pictures/raw/master/img/20200905224024.png)

修改为以下内容，直接粘贴复制，然后信息修改为你自己的；

```
{
  "picBed": {
    "uploader": "gitee", // 代表当前的上传图床
    "gitee": {
      "repo": "用户名/仓库名称 ",    // 仓库名：格式是 用户名/仓库名称 必填
      "token": "——————————",    // gitee 私人令牌 必填，token获取在如下说明；
      "path": "img/", // 自定义存储路径，比如 img/ 
      "customUrl": "", // 没有自己的域名的话，可以默认为空，不填写
      "branch": "master" // 分支名，默认是 master
    }
  },
  "picgoPlugins": {
    "picgo-plugin-gitee-uploader": true,
    "picgo-plugin-super-prefix": true
  }, // 为插件预留
  "picgo-plugin-super-prefix": {
    "fileFormat": "YYYYMMDDHHmmss"
  } //super-prefix插件配置
}
```

**获取Gitee的token说明；**

（1）首先得有一个属于自己的Gitee账号，没有就注册一个，访问官网:<https://gitee.com/>

（2）创建一个公开的仓库，用于存放图片；

（3）生成自己Gitee的token，用于以上配置，使Picgo-core操作你的仓库；

访问:<https://gitee.com/profile/personal_access_tokens>

创建公开的仓库，点击新建仓库；

![image-20200905230833991](https://gitee.com/mali8908/pictures/raw/master/img/20200905230837.png)

![image-20200905231327390](https://gitee.com/mali8908/pictures/raw/master/img/20200905231330.png)

点击头像处的'+'-设置-私人令牌；点击生成新令牌；

![image-20200905231550621](https://gitee.com/mali8908/pictures/raw/master/img/20200905231554.png)

![image-20200905232017603](https://gitee.com/mali8908/pictures/raw/master/img/20200906000948.png)

将获得的token复制粘贴到上面的配置里！

配置完成后验证：

![image-20200905224429580](https://gitee.com/mali8908/pictures/raw/master/img/20200905224433.png)

![image-20200905224407483](https://gitee.com/mali8908/pictures/raw/master/img/20200905224410.png)

实际上传一张图片，看看；

![image-20200905224535914](https://gitee.com/mali8908/pictures/raw/master/img/20200905224539.png)

然后将以上的文档保存后，再导入CSDN博客，试试图片会展示出来不；

![image-20200905224835997](https://gitee.com/mali8908/pictures/raw/master/img/20200905224839.png)

好，完成！最终使用Gitee图床实现了需求！

## **总结：**

1、以上折腾，分别使用了SMMS、Github、Gitee图床是来实现图片自动上传！但分别遇到了不同的问题：

​    SMMS图床：经过配置PicGo-Core,可以成功实现图片的上传，但它有反防盗机制，导致转存到其他地方（CSDN博客）不能正常展示图片-欢迎大佬指点！

​    Github图床：在配置PicGo-Core无误的情况下，也能上传到图床，但是不能在typora查看图片，提示有关本地的错误,也有网络方面的原因，使用国外代理可能会解决--欢迎大佬指点！

   Gitee图床：没遇到阻碍，成功实现了需求！

2、本文章写作顺序：一、安装typora

​                                     二、Typora+PicGo-Core+SMMS

​                                     三、Typora+PicGo-Core+Github

​                                     四、Typora+PicGo-Core+Gitee

3、每块主要内容：主要是配置文件config.json的修改、每个模块Token的获取，插件的安装、免费CDN:<https://cdn.jsdelivr.net/>的尝试使用，这个CDN可以加快查看Github的内容，后期也可以用来加速访问github使用（模仿链接：https://cdn.jsdelivr.net/gh/用户名/仓库名...）如果Gitee图床达到了限制，新建一个仓库继续免费使用，把配置文件做相应修改即可！

4、其实通过命令行picgo use uploader/picgo set uploader设置uploader，就是在修改配置文件config.json里的内容，简单粗暴，直接打开config.json进行复制粘贴配置也可以！