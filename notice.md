### 需要完成的事

> 关于vue-cli中ESlint的验证规则修改和制定

需求：vue-cli中采用了默认的eslint验证规则，在JavaScript中默认采用2个字符的缩进，需要变成4个字符的缩进，在JavaScript最后需要添加一个‘;’结尾的验证。

日期：2018.11.16

过程：

1. ESLint引用是在build/webpack.base.conf.js中，配置是在.eslintrc.js中
2. 阅读[ESLint](http://eslint.cn/docs/user-guide/configuring)规则
3. 解决缩进问题，添加规则

        'indent': [2, 4, { 'SwitchCase': 1 }], // 缩进风格, switch, case中使用缩进

        'vue/html-indent': [

            'error',
            4, // 缩进4个空格
            {
                'attribute': 1,
                'closeBracket': 0,
                'alignAttributesVertically': true,
                'ignores': []
            }
        ], // 在template中强制执行一致的缩进
4. 解决以';'号结尾问题

        'semi': [2, 'always'], // 语句强制分号结尾

总结：eslint规则的制定可以初步让我们代码避免一些错误，同时在协同开发的时候，具有更好的规范。

> require和import的使用

需求：在使用webpack的时，经常用到require和import。因此需要熟练掌握他们常用的功能，以及在vue-cli中默认的引用位置。

日期：2018.11.16

过程：

比较他们的区别：

1. require/exports是CommonJS的一部分，而import/export是ES6新规范

    ‘引申关于CommonJS的定义：CommonJS是一套模版系统的规范，把项目中的api打包成一个模版，通过require方法读取一个文件，并返回这个文件内部的exports对象’

2. import是编译时的，require是运行时的，意思是import必须放在文件的开头，而require可以放在代码任何地方。
3. import是一个解构过程，需要通过解构赋值给变量，require同样也可以，但是它也可以直接像函数一样调用
4. import中有default关键字，导入模板时也有*符号，更加灵活多变

总结：require和import现在仍然在项目中大面积使用，import更符合主流一些，而且在用法上更灵活。这两个都是为了让项目更模块话而产生出来的。

> npm初步讨索：学会发布一个npm包

需求：在使用vue-cli中时常需要引用到一个npm包，以方便在协作开发中提取公共方法或者组件。为了更好的学会npm的管理，包的发布过程，需要其进行系统的学习。

日期：2018.11.25

过程：

（注意：以下操作都是在项目的根目录底下的终端进行的）
1. 需要安装node，然后在[npm](https://www.npmjs.com/signup)网站上进行注册
2. 编写模版，新建文件夹和文件，然后把这个文件上传到github（简述这个过程：使用git init初始化文件，当然首先得在电脑上安装git，然后在github上新建repository或者利用现有的repository，复制其地址，在终端上输入 git remote add origin 地址，这样就进行了和github的repository的绑定，最后就git add,git push就可以了）
3. 使用npm init初始化项目文件，然后会进行一系列的提示，关于这个包的信息，其中需要注意的是keywords这个信息是关键词，怎么让别人在搜索npm包的时候能搜索出这个。其它像test command测试命名直接回车，license开源文件，直接回车。
4. 登入，首次npm adduser,然后会让你输入你的npm用户名，密码，邮箱（注意邮箱一点在注册的时候进行验证，否则会出错），登入完之后最后会显示当前链接的镜像，一定要注意这个，可能是使用了国内镜像，或者公司镜像，这个时候npm publish你不会在npm官网上看到你发布的包，所以如果遇到链接镜像不对需要切换。
npm config set registry http://registry.npmjs.org
5. 注意在在上传之前需要去npm官网搜索你将要上传的模块名称，如果搜索不到，你就可以上传，否则需要改名，不然会造成上传失败。如果上传遇到unscoped packages cannot be private这个是2018.10更新的，需要使用npm publish --access public
6. 注意：再切换到npm官网后，在日常工作中还是需要切换到公司的内部镜像。
7. 上传完成后就可以在需要的项目目录下安装 npm i 包名称
8. 常用命令

    查看当前镜像：npm config get registry

    切换当前镜像：npm config set registry 镜像地址

    发布包：npm publish

    下载包：npm i 包名
    删除包：npm remove 包名
