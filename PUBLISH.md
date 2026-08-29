# FlyingRemote 公开发布

公开仓：

- https://github.com/flyingtang/flyingremote
- https://gitee.com/flyingtang/flyingremote

开发树在 monorepo `ac-remote/`。完整流程见 **mycap** `deploy/docs/PUBLISH-PUBLIC.md`。

## 单产品

```bash
cd ac-remote
npm run release -- --init   # 首次
# 编辑 publish-open.local.env
npm run release             # 需本机 Android SDK / 已配置签名
```

已有 APK：`npm run release -- --skip-build --apk path/to.apk`（或先 stage 再 `--upload`）。

## Android 签名（必做一次）

未配置签名时，Gradle 只会产出 `app-release-unsigned.apk`，公开发布脚本会拒绝暂存。

```bash
cd ac-remote
npm run keys:android
# 生成 android/flyingremote-release.keystore + android/keystore.properties（均勿提交）
```

之后正常 `npm run release` / `publish-public.sh --only flyingremote` 即可打出已签名 `app-release.apk`。  
丢失 keystore 后无法用同一签名发升级包，请自行备份。
