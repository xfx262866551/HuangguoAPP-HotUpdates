# HuangguoAPP-HotUpdates

黄果短剧 Android 客户端的热更新资源仓库。**只存放签名后的资源包，不放源码、不放私钥。**

## 用途

客户端启动后会在后台检查本仓库的最新 Release：

```
https://github.com/xfx262866551/HuangguoAPP-HotUpdates/releases/latest/download/hot-update.json
```

下载到的新资源包会先验签、校验摘要与大小，通过后进入 pending 状态，下次启动时试用；启动失败会自动回退到内置资源。

## 发布内容

每次发布一个 Release，包含两个附件：

| 文件 | 说明 |
|---|---|
| `hot-update.json` | 签名信封：`payload`（Base64 元数据）+ `signature`（SHA256withECDSA） |
| `<bundle>.zip` | 资源包：站点规则、主题，或完整前端文件 |

元数据中的 `revision` 必须递增；`url`、`sha256`、`size` 必须与实际附件一致。

## 签名

- 签名算法：ECDSA P-256 / `SHA256withECDSA`。
- 客户端只内置**公钥**；私钥由发布者保管，绝不提交到任何仓库。
- 验签、摘要或大小任一不通过，客户端会拒绝该资源包。

## 注意

- 本仓库必须是**公开**的，否则客户端无法匿名拉取 Release 附件。
- 不要在这里上传 APK、源码、密钥或任何凭据。
