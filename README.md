# xray-azure

自动化部署 Xray 到 Azure Container Apps 的示例仓库。

## 说明
- 使用 `VLESS + WebSocket`，把 TLS 交给 Cloudflare 终结（Cloudflare 对外使用 443/TLS）。
- Azure Container Apps 监听 HTTP（80），GitHub Actions 会构建镜像并推送到 ACR，然后更新 Container App。

## 使用步骤（简要）
1. 在 Azure 上创建资源组、ACR、Container Apps 环境与初始 Container App（见下文）。
2. 在 GitHub 仓库中设置 Secrets（参考下方）。
3. 将本仓库推到 GitHub，Actions 会自动构建并部署。

## 必备 GitHub Secrets
- `AZURE_CREDENTIALS` — 从 `az ad sp create-for-rbac --sdk-auth` 得到的 JSON，用于 azure/login
- `ACR_LOGIN_SERVER` — 例如 `myregistry.azurecr.io`
- `ACR_USERNAME` — ACR 用户名
- `ACR_PASSWORD` — ACR 密码
- `AZURE_RG` — 资源组名
- `AZURE_APP_NAME` — Container App 名称

## 注意事项
- 把 `config.json` 中的 `YOUR_UUID` 替换成你的 UUID。
- 推荐使用 Cloudflare 做 DNS & TLS，CNAME 指向 Container Apps 的域名并开启 Full TLS。
