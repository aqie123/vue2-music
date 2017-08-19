一： 前期准备
	1.npm install -g npm   升级到最新
	2.npm install cnpm -g --registry=https://registry.npm.taobao.org   安装cnpm
	3.cnpm install bower -g
	4.npm install -g n    n stable      node升级到最新版本

	在cmd里直接输入： npm install -g cnpm –registry=https://registry.npm.taobao.org

	cnpm install --global vue-cli

	vue init webpack vue-music cd vue-music npm install npm run dev 
二： 目录 
		1.main.js入口文件
		2.common/stylus  样式文件
		3.common/fonts  字体文件

三： 1.cnpm install stylus-loader stylus --save-dev devDependencies --save dependencies  
    2.修改eslintrc,不检测新文件末尾是否空行； 
	3.webpack.base.conf.js resolve 配置别名 然后就可以绝对路径引入stylus文件 
	4.App.vue测试stylus 
	5.修改index.html 
	6.cnpm install babel-runtime fastclick --save :转译es6语法,点击延迟 cnpm install babel-polyfill --save-dev ： es6 API 比如：promise转译 
	7.新建组件，在route引入 
	8.App.vue 添加route-view 切换路由 
	9.cnpm install vue-lazyload vuex axios jsonp better-scroll create-keyframe-animation js-base64 lyric-parser good-storage --save
四： 
    1.tab导航栏 (m-header组件)
      app.vue引入，并输出
    2.