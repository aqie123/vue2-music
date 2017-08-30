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
              watch
              togglePlaying,loop,
            d.拖拽歌曲歌词跟着变化
              onProgressBarChange
            e.cd下面歌词
              handleLyric(执行)
            f.getLyric()获取不到歌词
            g.播放器底部适配
              多个组件处理相同逻辑：common/js/mixin.js
              1.music-list.vue   引入
              2.singer.vue
                在listview.vue 
          13.歌单详情页
              1.router/index.js  创建二级路由
                recommend.vue 添加组件
                router-view 对应二级路由容器
              2.使用vuex传递歌单数据
                a.state.js定义歌单对象 dis{}
                b.mutation-types 添加 SET_DISC
                c.mutation 添加更改函数 SET_DISC
                d.getters export disc
              3.recommend.vue 
                a.引入 mapMutations
                   在methods扩展  mapMutations 对应mutation-types
                b.在点击函数 将setDisc传进去
                c.在disc.vue接收vuex数据
                    1.引入 mapGetters
                    2.computed 引入 mapGetters 实现在this.disc访问到
              4.歌单详情页数居
                a.api/recommend,js  getSongList()
                b.disc.vue 引入上面方法,在created()调用上面请求
                  1._getSongList   获取歌单详情
                  2.disc.vue 中 music-list 绑定songs,并在data定义
                c.解决jsonp名称问题      
           14.排行榜页面 rank.vue
              1.新建api/rank
              2.添加点击事件 selectItem(item)
           15.榜单详情页布局 Vuex实现数据通讯
              1.router/index.js 
              2.vuex
                a.states.js 定义 topList
                b.mutation-types.js  SET_TOP_LIST
                c.mutations.js  types.SET_TOP_LIST
                d.getters.js   topList
                e.rank.vue  引入 mapMutations
                    methods 定义 ...mapMutations 是一个对象 setTopList
                    就可以在上面跳转函数  this.setTopList(item)
                f.top-list.vue 引入 mapGetters
                    在computed  中 ...mapGetters
                    然后在计算属性中 比如标题 ： this.topList.topTitle
              3.抓取榜单详情歌曲数据
                a.api/rank.js getMusicList(榜单ID)
                b.top-list.vue created  获取 this._getMusicList()
                  定义songs接收数据
                c.获取一首歌曲图片
           16.song-list 组件扩展
              1.props 扩展字段 rank 
              2.getRankCls
              3.music-list props扩展 rank
                并在 music-list.vue 将rank 传到song-list属性
                top-list.vue 将data 传 rank: true
           17.搜索页面
              1. 
                  a.components/suggest/suggest.vue
                  b.api/search.js
                  c.base/search-box/search-box.vue
                  d.base/search-list/search-list
                  e.base/confirm/confirm.vue
                  f.base/no-result/no-result.vue
              2.搜索框组件 （search-box.vue）
                  1.props:placeholder 然后绑定
                  2.v-model 双向绑定
                  3.created watch query
               3.热门搜索
                  1.api/search.js
                  2.search.vue 引入 {getHotKey}
                    search-box  添加 setQuery(query)方法
               4.新建suggest组件
                  1.props 检索词   watch query变化
                  2.api/search/search()
                  3. suggest组件 引入search()
                  4. suggest.vue this._genResult(res.data)
                  5.getDisplayName
                  6.search.vue 引入suggest组件
                  7.search.vue 监听 search-box  onQueryChange
                  8. song : 歌曲数据
                     zhida: 歌手数据
                  9.上拉刷新 (扩展scroll组件)
                    a.props: 传入 pullup
                    b.methods 监听滚动scrollEnd事件
                    c.suggest.vue data设置pullup
                      监听 @scrollToEnd 
                      suggest.vue perpage控制每页条数
                    d.suggest.vue 加引用 ref="suggest"
                      page = 1;
                      this.$refs.suggest.scrollTo(0, 0)
               5.search组件点击跳转到歌手列表
                  1.添加  router-view
                  2.route添加二级路由
                  3.suggest组件监听 selectItem(item)
                  4.methods 添加  ...mapMutations
                  5.在上面点击方法 调用 this.setSinger(singer)
                    就会在mutations.js 拿到state.singer
                  6.singer-detail.vue
                    ...mapGetters  取到singer
               6.search组件点击 插入歌曲到当前列表
                  1.state.js 修改 Playlist,sequenceList,(slice添加副本)currentIndex.
                    通过操作mutation改变state
                  2.action.js 定义动作  insertSong
                  3.suggest.vue 引入 mapMutations mapActions
                   并添加 ...mapActions  insertSong
                   在上面方法直接调用 this.insertSong
               7.suggest组件优化
                  1.没有搜索结果
                      定义基础组件 no-result在suggest.vue引入
                  2.基础组件search-box组件
                    create watch query 延时执行
                    派发query事件->search.vue通过onQueryChange set this.query
                    -> 传到suggest组件  监听输入框变化
                    -> suggest.vue watch query 调用 this.search()
                    目的 ： 防止输入一直请求
                    方法 ： common/js/util.js 新建截流函数 debounce()
                            在search-box.vue 引入 
                  3.滚动搜索列表收起键盘
                    1.扩展scroll组件 (Scroll->suggest->search)
                        添加属性 ： beforeScroll (滚动开始派发beforeScrollStart)
                        在scroll.vue判断,派发 beforeScroll
                        在suggest.vue 
                          data 添加beforeScroll ,传入到scroll组件中
                          监听事件 @beforeScroll = listScroll()
                          派发 listScroll事件
                        search.vue 中suggest监听 @listScroll=blurInput
                          调用子组件 search-box 方法
                        search-box.vue
                          1. ref="query"
                          2. 添加blur方法
               8.点击搜索关键词,保存到搜索历史(vuex)
                  1.state.js : searchHistory
                  2.mutation-type : SET_SEARCH_HISTORY
                  3.mutations : state.searchHistory
                  4.getters.js : searchHistory
                  5.suggest.vue : 点击selectItem 派发select事件
                    search.vue : 监听 @select="saveSearch"
                  6.封装action 
                  7.新建 common/js/cache.js 操作localStorage
                    saveSearch()
                    npm 安装 good-storage
                  8.search.vue 调用action saveSearchHistory （点击搜索列表触发）
                    存储到 ; searchHistory
                    同时 ： localStorage 也可以查看
                  9.cache.js 从本地缓存读取searchHistory  : loadSearch
                    并在state.js引入 
                  10.搜索历史渲染到dom
                    search.vue computed 添加
                  11.base/search-list组件
               9.点击搜索历史填入到搜索框 及删除历史记录
                  1.search-list.vue 派发点击事件;在search.vue实现 @select="addQuery"
                  2.添加action  : deleteSearchHistory
                  3.search.vue 中 search-list 派发 delete事件
                  4.弹窗组件confirm.vue 在search.vue 引用
                    基础组建 ： state props data methods events
                    基础组建通过props传入外部数据
                            通过 this.$refs.confirm.show() 调用基础组件方法
               10.搜索页面滚动
                  1. search.vue 引入Scroll组件        shortcut 变成scroll组件   
                      在两个div外面套一个div,用来计算高度
                      hotkey,searchHistory异步获取,定义shortcut计算属性
                  2.watch query改变
               11.播放歌曲重新计算搜索页面 playlist
                  1.playlistMixin
                  2.实现 handlePlaylist()
                    添加 ; ref="shortcutWrapper" ; ref="searchResult"
                    重新计算scroll高度
                    给suggest.vue添加refresh()方法
          18. 歌曲列表组件  (playlist.vue)
                1.player.vue 引入
                2.components/add-song/add-song'