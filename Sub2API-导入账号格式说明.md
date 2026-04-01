# Sub2API 导入账号格式说明

## 结论

`Sub2API` 不能直接导入注册器导出的原始账号数组 JSON，需要转换成它自己的账号导入结构。

当前仓库新增了一个可参考的样例文件：

```text
sub2api-openai-oauth-import.example.json
```

## 原始数据为什么不能直接导入

你现在手里的原始数据更像这样：

```json
[
  {
    "email": "...",
    "password": "...",
    "access_token": "...",
    "refresh_token": "...",
    "id_token": "..."
  }
]
```

而 `Sub2API` 更接近需要这种结构：

```json
{
  "data": {
    "proxies": [],
    "accounts": [
      {
        "name": "openai-oauth-1",
        "platform": "openai",
        "type": "oauth",
        "credentials": {
          "email": "...",
          "access_token": "...",
          "refresh_token": "...",
          "id_token": "...",
          "expires_at": "..."
        }
      }
    ]
  }
}
```

## 关键字段说明

### 外层账号字段

- `name`: 账号名称，建议唯一
- `platform`: 平台类型，当前按 OpenAI OAuth 思路写为 `openai`
- `type`: 认证类型，当前写为 `oauth`
- `credentials`: 实际认证内容

### credentials 内建议保留字段

- `email`
- `access_token`
- `refresh_token`
- `id_token`
- `expires_at`

## 不建议直接带入的字段

以下字段不建议作为核心导入字段：

- `password`
- `session_token`
- 纯注册状态字段

原因：

- `Sub2API` 更关注 OAuth/API Key 型上游账号凭据
- `password` 不是这类导入的核心字段
- 多余字段可能无意义，甚至增加泄露风险

## 使用方式

1. 复制 `sub2api-openai-oauth-import.example.json`
2. 替换里面的占位值
3. 根据你部署的 `Sub2API` 后台或接口进行导入

## 安全提醒

不要把真实的：

- `access_token`
- `refresh_token`
- `id_token`
- `password`

直接提交到 GitHub 仓库。

如果这些值已经泄露，建议尽快：

1. 修改密码
2. 让旧 token 失效
3. 重新生成新凭据
