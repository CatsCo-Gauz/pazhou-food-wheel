# 琶洲外卖转盘

广州海珠区琶洲“今天吃什么”移动网页。纯前端运行，不提交订单或付款；门店营业与配送范围以外卖平台实时信息为准。

## 美团 App 唤起实现

站点必须由用户点击按钮后发起跳转：

- iPhone：imeituan://www.meituan.com/search?q=店名
- Android：intent://www.meituan.com/search?q=店名#Intent;scheme=imeituan;package=com.sankuai.meituan;end
- 微信内置浏览器：提示改用 Safari 或系统浏览器，同时复制店名
- 未安装或浏览器阻止：停留当前页并提示，店名已复制

不再使用 https://meituan.com 首页作为 App 跳转，因为普通 HTTPS 首页不是搜索深链，且移动网页本身可能报客户端错误。

## 调研证据

- 955xiaoSu/Eat-what 的 index.html 使用 imeituan://www.meituan.com/search?q=周边美食推荐
- 1426098028/Promote 的“打开美团.html”使用 imeituan:// 直接唤起
- KusStar/krude 的 SearchHelper.kt 使用 imeituan://www.meituan.com/search?q=queryplaceholder，并标注 Android 包名 com.sankuai.meituan
- tanhan8023-ux/shesheji 的 takeout_launch_service_web.dart 同时使用 Android intent、美团外卖 meituanwaimai://search?keyword= 和美团主 App Scheme
- 美团官方 AASA 文件 https://www.meituan.com/.well-known/apple-app-site-association 只关联指定路径；普通首页和 /search 不在其路径列表中，不能依赖任意 HTTPS 地址作为 iOS Universal Link

这些 Scheme 属于客户端深链能力，可能随 App 版本和浏览器策略变化；网页保留复制店名兜底。
