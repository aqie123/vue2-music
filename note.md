一： 前期准备 8/19
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
    2.route/index.js
       a.引入
       b.编写路由
       c.app.vue 使用view-router
    3.开发导航栏 (tab)
      1.app.vue import
      2.在components使用
      3.在模板使用
    4.jsonp
      1.动态创建个script标签
      2.js/jsonp.js
      3.api/recommend.js
      4.api/config.js
    5.recommend组件
      1.获取数据
      2.开发轮播图组件
        a.base/slider/slider.vue  base作为一个npm安装模块
        b.slot
        c.引入slider组件，然后注册
        d.编写slider样式
        e.better-scroll
          1.ref html里面绑定
        f.common/js/dom.js  dom相关代码
        g.currentPageIndex: 指定当前页面
     6.歌单详情页
        1.dev-server.js  引入axios，编写api 
        2.base/scroll/scroll.vue
        3. :data="discList"
        4.给scroll 一个引用
        5.img class="needsclick"
        6.loading组件
          在recommend引入
     7.歌手列表页
        1.api/singer.js
        2.common/js/singer.js  抽象出歌手类
        3开发通讯录基础组件 listview ;并在singer.vue引入
     8.歌手详情页 (子路由)
        1.index.js引入singer-detail.vue
        2.vuex
          a.初始化store
          b.在入口文件main.js引入
          c.singer.vue使用vuex;singer-detail取数据
        3.歌手详情
        4.歌单处理
           a.common/js/song.js  song类
           b.数据处理
      9.music-list组件
        1.singer-detail.vue 调用music-list组件
        2.在music-list.vue填充数据
      10.song-list组件
        在music.vue引入
        1.实现图片根据歌单列表上移
          music-list.vue 在create函数
        2.<scroll> 监听事件
        3.通过scrollY值设置layer偏移量
        4.watch
      11.player-kernel
        1.state.js 设置播放器参数
          配置getters.js
          mutation.js
        2.common/js/config.js
        3.新建player.vue，定义在app.vue
        4.player.vue控制播放器展示
        5.点击歌曲跳转到播放页面
           a.song-list 派发点击事件selectItem
           b.music-list接收派发select事件
           c.music-list 定义selectItem方法
           d.在store/actions.js定义动作,在music-list组件调用
        6.播放器页面
          a.点击返回  , mapMutations
          b.设置切换动画,ref="cdWrapper"
        7.播放功能
          a.mapMutations 传递状态
            watch playing状态
          b.mapGetters: 'currentIndex','fullScreen','playlist','currentSong', 'playing'
          c.前进后退
          d.播放结束 派发@timeupdate="updateTime"
          e.显示歌曲播放时间
        8.进度条 progress-bar.vue
          a.引入到player.vue
          b.进度条接收百分比  props ,watch percent
            在player.vue计算属性percent,传入到组件，此时跟随歌曲进度前进
          c.给进度条添加touch事件,在methods定义事件回调函数
            拖拽结束，派发事件
            在player.vue监听派发事件  onProgressBarChange 实现拖拽
          d.progressClick  进度条添加点击事件
       9.   mini 下面圆形进度条 process-circle.vue
          a.player.vue引入
             slot  就是在组件内部插入
       10.播放模式 (列表播放，单曲循环播放,随机播放)
          a.player.vue mapGetters 添加mode
             映射一个mutation
          b.changeMode后，修改播放列表
            mapGetters 添加 sequenceList
            新建util.js
            修改当前playList mapMutations
            切换播放模式，会改变歌曲播放状态
                watch 解决
       11. audio播放结束 派发end事件
          music-list.vue 添加 random事件
            在store/actions.js添加randomPlay； 在mapActions引入
       12.播放歌词数据抓取
          1.创建api/song.js
          2.common/js/song.js 扩展 song类 getLyric()
          3.在player.vue watch 调用common/js/song.js  getLyric接口
          4.player.vue 引入 lyric-parser
            methods 新建 getLyric  拿到lyric对象
          5.添加歌词dom结构
          6.歌词滚动
            a.
          7.歌词切换
            a.给middle绑定touch事件
            b.透明度切换 ，middle-l 加引用 ref
            c.歌词根据歌曲变化
            
          
            