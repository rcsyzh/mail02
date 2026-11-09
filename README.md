邮箱

## GitHub Actions / Cloudflare 部署配置

工作流必需配置（可放在 GitHub Secrets 或 Variables，敏感值建议使用 Secrets）：

- CLOUDFLARE_API_TOKEN、CLOUDFLARE_ACCOUNT_ID：Cloudflare 部署凭据。
- JWT_SECRET：不能为空，且不能包含问号、百分号、井号、斜杠或反斜杠。
- DOMAIN：必须是 JSON 数组，例如 ["example.com"]。
- ADMIN：管理员邮箱，不能为空。
- CUSTOM_DOMAIN：自定义域名（只填主机名，不带 https://），用于 Worker 路由和数据库初始化；未配置会导致部署初始化失败。

可选配置：NAME（默认 cloud-mail）、KV_NAMESPACE_ID（工作流可自动创建/配置）、R2_BUCKET_NAME（不填则跳过 R2 绑定）、PROJECT_LINK、AI_MODEL（默认使用工作流内置模型）、EMAIL（启用额外发件绑定）、ANALYSIS_CACHE。D1 数据库不存在时工作流会自动创建。

Worker 配置和部署时生成的配置均设置 workers_dev = false，不会启用 Cloudflare 自动分配的 workers.dev 地址；请先配置有效的自定义域名。
