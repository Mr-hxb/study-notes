### 需要完成的事

> 关于vue-cli中ESlint的验证规则修改和制定

需求：vue-cli中采用了默认的eslint验证规则，在JavaScript中默认采用2个字符的缩进，需要变成4个字符的缩进，在JavaScript最后需要添加一个‘;’结尾的验证。

日期：2018.11.16

过程：

1. ESLint引用是在build/webpack.base.conf.js中，配置是在.eslintrc.js中
2. 阅读 [ESLint](http://eslint.cn/docs/user-guide/configuring) 规则
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
4. 解决以';'号结尾问题

        'semi': [2, 'always'], // 语句强制分号结尾

总结：eslint规则的制定可以初步让我们代码避免一些错误，同时在协同开发的时候，具有更好的规范。

> require和import的使用

需求：在使用webpack的时，经常用到require和import。因此需要熟练掌握他们常用的功能，以及在vue-cli中默认的引用位置。

日期：2018.11.16

过程：

比较他们的区别：

1. require/exports是CommonJS的一部分，而import/export是ES6新规范

    
        引申关于CommonJS的定义：CommonJS是一套模版系统的规范，把项目中的api打包成一个模版，通过require方法读取一个文件，并返回这个文件内部的exports对象
2. import是编译时的，require是运行时的，意思是import必须放在文件的开头，而require可以放在代码任何地方。
3. import是一个解构过程，需要通过解构赋值给变量，require同样也可以，但是它也可以直接像函数一样调用
4. import中有default关键字，导入模板时也有*符号，更加灵活多变

总结：require和import现在仍然在项目中大面积使用，import更符合主流一些，而且在用法上更灵活。这两个都是为了让项目更模块话而产生出来的。
