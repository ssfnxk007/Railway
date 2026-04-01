# Railway 代理搭建教程

> 本教程记录在 Railway 上部署代理服务的完整流程，方便重复使用。
https://kjgx668.blogspot.com/2025/10/ipip2ipip.html
---
ssfnxk97@wyhsd.xyz
## 📋 准备工作

| 需要 | 说明 |
|------|------|
| GitHub 账号 | 用于登录 Railway |
| 邮箱 | 接收账单通知 |
| V2RayN 客户端 | 用于连接代理 |

---

## 🚀 第一步：注册 Railway

1. 访问 [https://railway.app](https://railway.app)
2. 点击 **Login**
3. 选择登录方式：
   - **GitHub 登录**（推荐）
   - **邮箱登录**（直接输入邮箱，收验证码）
   - **Google 登录**
4. 完成注册

> 💡 **重新注册技巧**：用不同邮箱注册新账号，可以重新获得 $5 赠送额度。
>
> ⚠️ Railway Hobby 计划需要绑定信用卡，每月 $5。新用户可能有 $5 赠送额度。

---

## 🛠️ 第二步：创建项目

1. 登录后进入 Dashboard
2. 点击 **New Project**
3. 选择 **Deploy from Docker Image**

---

## 📦 第三步：部署 Docker 镜像

### 方式一：使用现成镜像（推荐）

输入 Docker 镜像地址：
```
ghcr.io/ssfnxk007/ssfnxk:2055
```

### 方式二：使用其他公开镜像

常用的代理镜像（可能需要配置环境变量）：
- `teddysun/xray` - 需要手动配置
- 其他 Argo-Xray 镜像

---

## ⚙️ 第四步：配置环境变量（如需要）

点击服务 → **Variables** → 添加变量：

| 变量名 | 说明 | 示例值 |
|--------|------|--------|
| `ARGO_AUTH` | Cloudflare Argo Tunnel Token | `eyJhIjo...` (Base64 JSON) |
| `UUID` | 用户 ID（如果镜像需要） | `7db16585-d830-461d-92a5-7a144b32ac5b` |

> 如果使用的镜像已经内置配置，可以跳过此步骤。

---

## 🌐 第五步：配置域名

1. 部署成功后，点击服务
2. 进入 **Settings** → **Networking**
3. 点击 **Generate Domain** 生成公网域名
4. 得到类似：`xxx-production.up.railway.app`

---

## 📱 第六步：获取订阅地址

订阅地址格式（根据你的镜像配置）：
```
https://你的域名/1026
```

示例：
```
https://ssfnxk-production.up.railway.app/1026
```

> 路径 `/1026` 取决于镜像的配置，可能是 `/sub`、`/订阅路径` 等。

---

## 📲 第七步：V2RayN 配置

### 添加订阅

1. 打开 **V2RayN**
2. 点击 **订阅分组** → **订阅分组设置**
3. 点击 **添加**
4. 填写：
   - **别名**：`Railway-美国`（随意）
   - **可选地址(Url)**：`https://你的域名/1026`
5. 点击 **确定**
6. 右键订阅 → **更新订阅**

### 使用代理

1. 在服务器列表选择节点
2. 右键 → **设为活动服务器**
3. 右下角托盘图标 → **系统代理** → **自动配置系统代理**

---

## 💰 费用说明

| 项目 | 费用 |
|------|------|
| Hobby 计划 | $5/月 |
| 新用户赠送 | $5（抵扣首月） |
| 使用量超出 | 按量计费 |

---

## 🔄 重新部署流程（快速版）

1. 登录 [railway.app](https://railway.app)
2. **New Project** → **Docker Image**
3. 输入镜像：`ghcr.io/ssfnxk007/ssfnxk:2055`
4. 等待部署完成
5. 生成域名
6. 订阅地址：`https://域名/1026`
7. V2RayN 添加订阅 → 更新 → 使用

---

## 📝 当前配置信息


| 项目 | 值 |
|------|-----|
| **镜像** | `ghcr.io/ssfnxk007/ssfnxk:2055` |
| **当前域名** | `ssfnxk-production-f52b.up.railway.app` |
| **订阅地址** | `https://ssfnxk-production-f52b.up.railway.app/1026` |
| **账单邮箱** | `ssfnxk102@wyhsd.xyz` |
| **GitHub** | `ssfnxk007` |

---

## ⚠️ 注意事项

1. **账单周期**：每月23日结算
2. **扣款失败**：服务会被暂停
3. **重新开始**：删除项目，用新账号重建
4. **限额技巧**：绑定限额 $0 的卡，扣款失败但不会产生实际费用

---

## 🔗 相关链接

- Railway 官网：https://railway.app
- Railway 文档：https://docs.railway.com
- V2RayN 下载：https://github.com/2dust/v2rayN/releases

---

*文档生成时间：2025年12月15日*
