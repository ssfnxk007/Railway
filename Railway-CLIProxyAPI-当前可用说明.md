# Railway CLIProxyAPI 当前可用说明

## 结论

当前仓库已经可以直接用于 Railway 部署。

- `Dockerfile` 可直接使用
- `config.yaml` 已包含运行所需的基础配置
- WebUI / Management API 已在新 Railway 服务验证通过

## 当前仓库关键文件

### Dockerfile

当前内容：

```Dockerfile
FROM eceasy/cli-proxy-api:latest
COPY config.yaml /CLIProxyAPI/config.yaml
EXPOSE 8317
```

说明：

- 基础镜像：`eceasy/cli-proxy-api:latest`
- 启动时会读取容器内 `/CLIProxyAPI/config.yaml`
- Railway 服务端口：`8317`

### config.yaml

当前 `config.yaml` 是已验证可启动版本，包含：

- 远程管理已开启
- 客户端 API Key 已设置
- 管理面板 Key 已设置
- OpenAI / Claude / Gemini / Codex / OpenRouter / 自定义兼容接口模板已预置

注意：

- provider 的真实上游 key 目前仍是占位值
- 直接 Redeploy 可以正常启动服务和管理面板
- 真正调用各上游前，需要你在 WebUI 中把占位 key 改成真实 key

## 已验证可用的 Railway 服务

### 正在使用的新服务

- 服务名：`celebrated-essence`
- 管理面板：`https://celebrated-essence-production-f40e.up.railway.app/management.html`
- API 基址：`https://celebrated-essence-production-f40e.up.railway.app`

### 旧服务

旧服务 `endearing-serenity` 曾出现配置未正确加载的问题，不建议继续使用。

## 当前有效 Key

### 客户端 API Key

用于调用 `/v1/models`、`/v1/chat/completions` 等代理接口：

```text
ssfnxk-railway-key
```

### 管理面板 Key

用于登录 WebUI / Management API：

```text
ssfnxk-admin-key
```

## 当前已验证通过的内容

新服务日志已出现：

```text
management routes registered after secret key configuration
```

并且已验证：

- 管理面板可打开：`/management.html`
- API 服务正常启动在 `:8317`
- 配置已加载 6 个 provider client

## 还没有完成的事

以下 provider 当前只是模板，尚未填入真实 key：

- OpenAI
- Claude
- Gemini
- Codex
- OpenRouter
- custom OpenAI-compatible

也就是说：

- 服务框架已经可用
- WebUI 已可用
- 但真正调用上游模型前，还要在 WebUI 中填写真实密钥

## 建议使用方式

### 推荐

优先在 WebUI 中填写真实 provider key，不建议把真实密钥直接写回公开仓库。

管理面板地址：

```text
https://celebrated-essence-production-f40e.up.railway.app/management.html
```

管理密钥：

```text
ssfnxk-admin-key
```

### API 调用示例

查询模型：

```bash
curl https://celebrated-essence-production-f40e.up.railway.app/v1/models ^
  -H "Authorization: Bearer ssfnxk-railway-key"
```

聊天请求示例：

```bash
curl https://celebrated-essence-production-f40e.up.railway.app/v1/chat/completions ^
  -H "Content-Type: application/json" ^
  -H "Authorization: Bearer ssfnxk-railway-key" ^
  -d "{\"model\":\"openai-gpt4o-mini\",\"messages\":[{\"role\":\"user\",\"content\":\"hello\"}]}"
```

## 关于 Auth Files

不建议把账号列表 JSON 直接上传到 `Auth Files`。

原因：

- `Auth Files` 要求上传单个 JSON 对象，不接受最外层是数组的文件
- 带 `refresh_token` 的认证文件可能会被 CPA 纳入自动管理/刷新流程

如果你不想让 CPA 帮你定时刷新：

- 不要上传整批账号 token 列表到 `Auth Files`
- 优先使用 `AI Providers` 页面直接填写静态 API key

## 以后是否可以直接复用

可以。

当前项目以后可以直接按下面流程复用：

1. 将当前仓库部署到 Railway
2. 等服务启动成功
3. 打开 `/management.html`
4. 使用管理 key 登录
5. 在 WebUI 中填写真实 provider key
6. 使用客户端 API key 对外调用

## 需要你记住的最重要信息

管理面板：

```text
https://celebrated-essence-production-f40e.up.railway.app/management.html
```

客户端 API Key：

```text
ssfnxk-railway-key
```

管理面板 Key：

```text
ssfnxk-admin-key
```
