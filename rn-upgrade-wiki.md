#React Native 升级日志


[官方升级日志地址](https://github.com/facebook/react-native/releases)

我们目前master版本是0.12.0，所以我从0.12.0开始

所有的changelog在官方都有是英文的，为了节省大家时间我翻译一下:) 如果理解错了请指正

    
[已知的问题最好经常去看看](http://facebook.github.io/react-native/docs/known-issues.html)

<br />

##0.13.0改变了哪些？
    首先0.13开始支持在windows上用npm 3 安装react-native，虽然没有在mac上开发的好，但是会越来越好，然而对我并没什么用

####重大改变：
1. setImmediate支持批量更新，React的更新方法如setState，将会被列入setImmediate方法批量执行，性能大大提高的同时也非常依赖该方法的精确的处理时间，不然容易引发bug
2. 支持node 4.0
3. ScrollView的keyboardShouldPersistTaps属性默认为false
4. 当style属性如with,backgroundColor被当做组件的属性值传进来时会有警告提示
5. flow升级到0.17
6. 在iOS上移除了RCTCache
7. 移除header_mappings_dir

####已知的问题：
1. React Dev Tools还不能正常工作
2. 打包不支持symlinks了，也就是说在node_modules下面的Symlinks打包的时候将被忽略
3. 在iOS 9.0下有一个bug导致3D触摸破坏了手势体系
4. Android的WebSockets关闭的时候有问题

####新特性：
#####JavaScript
1. 支持const
2. 支持import
3. Number .EPSILON/MIN_SAFE_INTEGER/MAX_SAFE_INTEGER  are polyfilled
4. Animate可以使用颜色名称代替rgba语法，例如’black’
5. 优化processColor
6. 新的Switch组件，支持iOS和Android
7. 保存原始的全局对象在polyfilling他们之前，如果JS环境支持一个全局属性，例如： fetch，它仍然会被polyfilled，但是原始的fetch会被保存为originFetch，这样如果你在chrome中调试的时候，想使用chrome内置的fetch，就可以指定global.fetch = originFetch了
8. 为不同平台适配了Navigator的navigation的不同的样式，并增加navigationStyles属性可以定制你想要的样式

#####iOS
1. Pause JS runloop，没有JS tasks的时候pause CADisplayLink以节省性能消耗
2. 查找源码路径的时候使用bundleForClass代替mainBundle
3. 屏蔽RCTAsset在生产环境下
4. 增加行内图片，即Image组件可以作为Text子组件使用,要注意的是使用行内图片组件的话，现在除了source属性其他属性都会被忽略
5. 提高JS bundle loading的性能

######Android
1. gif自动播放bug修复
2. 在主UI线程之外可以初始化react context
3. ToolbarAndroid组件支持远程图片加载
4. Image组件支持borderWidth和borderColor属性
5. 新增ViewPagerAndroid组件（iOS的官方版还没有实现）
6. Android下实现WebSocket模块
7. 增加默认Proguard配置

#####其他
1. CLI增加了个新的flag —verbose 可以调试出项目初始化缓慢到底慢在哪，要升级一个全局的react-native-cli
2. Packager server的代码更具模块化，对使用者没有什么影响，但是对于代码贡献者阅读代码友好多了
3. 文档更新

#####BUG修复
1. 结束滑块响应当取消触摸的时候
2. 清除图片仅当它从视图中移除的时候，如果该图片只是被移到当前视图的另外一个地方是不会被清除的
3. 多行的import可以被解析了
4. JS的WebSockets实现了EventTarget
5. 保存Android React 接口当处理异常的时候，之前是丢弃了
6. RCTTextInput的scrollsToTop值为No
7. 取消延时当Touchable组件unmounted的时候
8. rpm支持require(‘package.son')
9. iOS上加载不到正确的image url时提示更加友好的错误信息
10. Android上调用原生方法前会先检查接口是不是销毁了
11. 修复了LIstView onEndReached的bug
12. Android上，当键盘可见时修复触摸目标计算不准确的问题

省略了一些，还有想知道具体细节的到github上面去看[commits](https://github.com/facebook/react-native/compare/0.12-stable...0.13-stable)。

##0.14.0改变了哪些？
1. 最最最重大改变我觉得是[资源统一管理](http://facebook.github.io/react-native/docs/images.html#content)
2. react-native bundle的API改了，具体不说了，升级到0.14.0后到命令行打一下react-native bundle 看看就知道了，注意的是原来的—minify没用了，以—dev false代替
3. removeClippedSubviews默认为true
4. 删除多余的打包入口，就用npm start 或者react-native start吧

##0.15.0改变了哪些？
1. 首先如果iOS开发必须把XCode升级到7以上
2. Android中配置一些参数等方面的改变不会重启app
3. iOS中增加富文本
4. 更加友好的错误提示
5. Android增加systrace的支持
6. Android增加Geolocation接口（可以定位的设备方位）
7. Android增加IntentAndroid组件，拥有可以打开系统浏览器，地图和其他应用的能力
8. Android中Cookies可以跨请求保存

##0.16.0改变了哪些？
####JS
1. 增加Babel helpers支持imports，解决0.13.0增加的默认支持imports不能用问题，反正是真正支持imports了
2. 增加For-of语法的支持
3. 支持[Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
4. 插件默认到处的模块实现和bebal保持一致

####Android
1. 增加下拉列表组件
2. view增加阴影实现
3. 转移views后使用正确的touch handing
4. 支持自定义字体，目前只支持TTF和OTF
5. Android的ViewPager增加setPageWithoutAnimation方法
6. Image可以嵌入到Text中

####iOS
1. iOS的TextInput增加keyboardAppearance属性，可以显示黑色键盘
2. AsyncLocalStorage使用内存做缓存
3. TextInput支持onSelectionChange事件
4. 增加RCTPasteboard接口，该接口可以向纸板写字符串，可以用它实现复制到剪贴板功能

####重大改变
1. react-native现在使用Babel 6
2. android的touch事件现在和ios保持一致
3. YellowBox（警告）默认开启在IOS中
4. JS decorators将无法使用
5. 因为Babel exporting default class 然后再extend一个class的时候将报错
6. RCTSparseArray被NSDictionary代替
7. RCTWebViewExcutor被移除
8. 第三方组件统一增加 `
propTypes: {
...View.propTypes,
},
`



##0.17.0改变了哪些？

####最高级别的改变
1. 增加Android WebView
2. 新的Alert API统一了Android和iOS
3. 在JS层简单的包裹一下UIManager模块使它更易使用
4. 修复react-native bundle 在window 10下的bug
5. 修复根据ref获取不到navigatorBar的bug
6. 修复packager中assetsRoot的参数被忽略的bug
7. 修复检测一个无状态的组件会引起程序崩溃的bug
8. 增加剪切板组件同时支持Android和iOS
9. 修复在windows上使用require("./image")的bug

####Android
1. 允许指定一个自定义的文件路径作为JavaScriptCore的profiler输出路径
2. Image组件增加onLoadX事件的支持，如onLoadStart,onLoadEnd等
3. 增加传递ImagePiplineConfig配置到FrescoModule
4. 试验（不知道是不是试验，字面意思是试验）支持LayoutAnimation，需要手动设置UIManager.setLayoutAnimationEnabledExperimental
5. 增加NetInfo的支持
6. ToolbarAndroid增加页面以从右向左（right-to-left）变化的支持
7. 为Image组件增加loadingIndicatorSrc属性，类似iOS下的defaultSource，当正在加载图片的时候默认显示一个图片
8. ReactPropGroup增加double类型
9. 为Views增加rotateX和rotateY属性的变换

####iOS
1. 修复富文本框滚动bug
2. SliderIOS增加定制拇指图片的功能
3. 允许定制颜色和图片在MapView上的动画
4. MapView增加定制两点之间线条的颜色和宽度
5. Views和Shadow Views增加didSetProps回调函数
6. 修复多行TextInput组件不触发onfouics和onBlur方法的bug
7. 修复MapView在IOS8下会崩溃的bug
8. ActionSheetIOS增加excludedActivityTypes属性
9. AlertIOS增加secure-text和password类型，同时修复取消按钮的高亮bug，还有确认按钮和取消按钮label的本地化bug
10. TextInput增加blurOnSubmit事件
11. 修复TextInput还原问题在iOS8以下的问题
12. 修复ScrollVIews嵌套时会出现中断滚动的bug
13. TabBarIOS允许使用一个字符串作为系统图标
14. 增加LinkingIOS支持Universal Links
15. PickerIOS增加style属性，允许自定义字体大小，颜色，排列方式
16. ActionSheetIOS按钮增加tinitColor属性
