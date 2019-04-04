###Babel 转码器  

```javascript 
    // 转码前
    input.map(item => item + 1);

    // 转码后
    input.map(function (item) {
      return item + 1;
    });
```

安装：$ npm install --save-dev @babel/core

###Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。
        
        该文件用来设置转码规则和插件，基本格式如下。
```
        {
          "presets": [],
          "plugins": []
        }
```        
        presets字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。
        
        # 最新转码规则
        $ npm install --save-dev @babel/preset-env

        # react 转码规则
        $ npm install --save-dev @babel/preset-react
        然后，将这些规则加入.babelrc。

          {
            "presets": [
              "@babel/env",
              "@babel/preset-react"
            ],
            "plugins": []
          }
###命令行转码
      Babel 提供命令行工具@babel/cli，用于命令行转码。

      它的安装命令如下。

      $ npm install --save-dev @babel/cli
      基本用法如下。

      # 转码结果输出到标准输出
      $ npx babel example.js

      # 转码结果写入一个文件
      # --out-file 或 -o 参数指定输出文件
      $ npx babel example.js --out-file compiled.js
      # 或者
      $ npx babel example.js -o compiled.js

      # 整个目录转码
      # --out-dir 或 -d 参数指定输出目录
      $ npx babel src --out-dir lib
      # 或者
      $ npx babel src -d lib

      # -s 参数生成source map文件
      $ npx babel src -d lib -s
###babel-node
      @babel/node模块的babel-node命令，提供一个支持 ES6 的 REPL 环境。它支持 Node 的 REPL 环境的所有功能，而且可以直接运行 ES6 代码。

      首先，安装这个模块。

      $ npm install --save-dev @babel/node
      然后，执行babel-node就进入 REPL 环境。

      $ npx babel-node
      > (x => x * 2)(1)
      2
      babel-node命令可以直接运行 ES6 脚本。将上面的代码放入脚本文件es6.js，然后直接运行。

      # es6.js 的代码
      # console.log((x => x * 2)(1));
      $ npx babel-node es6.js
      2
###@babel/register 模块
      @babel/register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用 Babel 进行转码。

      $ npm install --save-dev @babel/register
      使用时，必须首先加载@babel/register。

      // index.js
      require('@babel/register');
      require('./es6.js');
      然后，就不需要手动对index.js转码了。

      $ node index.js
      2
      需要注意的是，@babel/register只会对require命令加载的文件转码，而不会对当前文件转码。另外，由于它是实时转码，所以只适合在开发环境使用。

###babel API
        如果某些代码需要调用 Babel 的 API 进行转码，就要使用@babel/core模块。

        var babel = require('@babel/core');

        // 字符串转码
        babel.transform('code();', options);
        // => { code, map, ast }

        // 文件转码（异步）
        babel.transformFile('filename.js', options, function(err, result) {
          result; // => { code, map, ast }
        });

        // 文件转码（同步）
        babel.transformFileSync('filename.js', options);
        // => { code, map, ast }

        // Babel AST转码
        babel.transformFromAst(ast, code, options);
        // => { code, map, ast }
        配置对象options，可以参看官方文档http://babeljs.io/docs/usage/options/。

        下面是一个例子。

        var es6Code = 'let x = n => n + 1';
        var es5Code = require('@babel/core')
          .transform(es6Code, {
            presets: ['@babel/env']
          })
          .code;

        console.log(es5Code);
        // '"use strict";\n\nvar x = function x(n) {\n  return n + 1;\n};'
        上面代码中，transform方法的第一个参数是一个字符串，表示需要被转换的 ES6 代码，第二个参数是转换的配置对象。

###@babel/polyfill
        Babel 默认只转换新的 JavaScript 句法（syntax），而不转换新的 API，比如Iterator、Generator、Set、Map、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

        举例来说，ES6 在Array对象上新增了Array.from方法。Babel 就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

        安装命令如下。

        $ npm install --save-dev @babel/polyfill
        然后，在脚本头部，加入如下一行代码。

        import '@babel/polyfill';
        // 或者
        require('@babel/polyfill');
        Babel 默认不转码的 API 非常多，详细清单可以查看babel-plugin-transform-runtime模块的definitions.js文件。

        浏览器环境
        Babel 也可以用于浏览器环境，使用@babel/standalone模块提供的浏览器版本，将其插入网页。

        <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
        <script type="text/babel">
        // Your ES6 code
        </script>
        注意，网页实时将 ES6 代码转为 ES5，对性能会有影响。生产环境需要加载已经转码完成的脚本。

        Babel 提供一个REPL 在线编译器，可以在线将 ES6 代码转为 ES5 代码。转换后的代码，可以直接作为 ES5 代码插入网页运行。
