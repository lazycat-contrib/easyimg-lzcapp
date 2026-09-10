# EasyImg for LazyCat

适用于个人的一站式图床服务，支持开启公共上传、AI 鉴黄服务集成、权限控制、数据统计和实时推送。

主页：https://github.com/chaos-zhu/easyimg

## 使用

要求懒猫微服 1.5.0 或更新版本，目标架构 amd64。默认用户名和密码均为 `easyimg`，首次登录后请立即修改，再分享应用地址。

应用对访客开放，确保图片外链、API 调用及上游公共上传页面可以使用；管理接口由 EasyImg 自身鉴权。公共上传的开关、访问控制和上传限制在应用设置中管理，包不覆盖这些设置。

数据库 `/app/db` 持久化至 `/lzcapp/var/db`，图片 `/app/uploads` 持久化至 `/lzcapp/var/uploads`。备份与迁移时同时保留两个目录。

HTTP 服务监听 3000，通过懒猫应用入口访问，无需占用宿主 8092 端口。保留 `NODE_ENV=production`、`HOST=0.0.0.0`、`PORT=3000`。

AI 鉴黄需要配置上游支持的检测服务；本包不附带检测容器。保留手动登录，不注入文件选择器。

## 构建与发布

```sh
mkdir -p dist
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

仅发布喵喵商店，官方商店关闭。使用 `ghcr.1ms.run/chaos-zhu/easyimg` 加速镜像，自动更新时验证 amd64 摘要与上游一致。初始版本 1.2.2，每日检查三段式稳定版本。

组织 Secrets：`APPSTORE_URL`、`APPSTORE_TOKEN` 和可选的 `PRIVATE_STORE_GROUP_CODES`。喵喵商店引用 GitHub Release 文件 `community.lazycat.app.easyimg-v<version>.lpk` 及其 SHA256。

图标由用户提供。构建和发布检查不替代微服上的上传、外链、权限控制及持久化实测。
