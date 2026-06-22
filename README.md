# 🚀 熊出没之家 - 后端部署包（Render）

> 这是后端代码包，用于部署到 Render

## 📦 包内容

```
bear-app-backend/
├── server.js         # 后端主文件
├── package.json      # 项目配置
├── package-lock.json # 依赖锁定
├── database.json     # 数据库文件（默认admin账号）
└── README.md         # 本说明文件
```

---

## 🚀 部署到 Render（3步搞定）

### 第1步：准备 GitHub

1. 注册/登录 [GitHub](https://github.com)
2. 创建一个新仓库（比如叫 `bear-app-backend`）
3. 把这个文件夹里的所有文件上传到仓库

### 第2步：部署到 Render

1. 登录 [Render](https://render.com)（用 GitHub 登录）
2. 点击右上角 **"New +"** → **"Web Service"**
3. 找到你刚才的仓库，点击 **"Connect"**
4. 填写配置：

   | 配置项 | 填写内容 |
   |--------|----------|
   | Name | `bear-api`（随便起） |
   | Runtime | `Node` |
   | Region | `Singapore`（新加坡，速度快） |
   | Branch | `main` |
   | Root Directory | 留空（因为整个仓库就是后端） |
   | Build Command | `npm install` |
   | Start Command | `node server.js` |
   | Plan | `Free`（免费） |

### 第3步：添加环境变量（推荐）

1. 点击 **"Advanced"** 展开
2. 点击 **"Add Environment Variable"**
3. 添加：

   | Key | Value | 说明 |
   |-----|-------|------|
   | `NODE_ENV` | `production` | 生产环境 |
   | `JWT_SECRET` | （点 Generate） | 自动生成密钥 |

4. 点击 **"Create Web Service"**

---

## ✅ 部署完成

部署成功后，页面上方会显示你的后端地址，类似：
```
https://bear-api.onrender.com
```

🎉 **把这个地址记下来，部署前端的时候要用！**

> 💡 小提示：免费套餐15分钟没请求会休眠，第一次访问可能要等10-20秒唤醒，之后就快了。

---

## 💡 可选优化

### 添加持久化磁盘（推荐）

不加磁盘的话，重新部署后用户数据会重置。想保留数据就加个磁盘：

1. 服务页面左侧点击 **"Disks"**
2. 点击 **"Add Disk"**
3. 填写：
   - Name: `data`
   - Mount Path: `/var/data`
   - Size: `1 GB`（免费最多1GB）
4. 点击 **"Create"**
5. 然后左侧 **"Environment"** → 添加环境变量：
   - Key: `DB_DIR`
   - Value: `/var/data`
6. 保存后会自动重新部署

### 防止休眠

用 [UptimeRobot](https://uptimerobot.com) 每5分钟访问一次，保持服务唤醒：

1. 注册 UptimeRobot
2. Add New Monitor
3. 类型选 HTTP(s)
4. URL 填你的后端地址
5. 间隔选 5 分钟

---

## 🔌 API 接口列表

部署成功后，你就有了这些接口：

| 接口 | 方法 | 说明 |
|------|------|------|
| `/api/register` | POST | 用户注册 |
| `/api/login` | POST | 用户登录 |
| `/api/reset-password` | POST | 重置密码 |
| `/api/user/profile` | GET | 获取用户信息（需Token） |
| `/api/user/change-password` | POST | 修改密码（需Token） |
| `/api/videos` | GET | 视频列表（需Token） |
| `/api/series` | GET | 系列作品（需Token） |
| `/api/characters` | GET | 角色信息（需Token） |
| `/api/quotes` | GET | 经典台词（需Token） |
| `/api/achievements` | GET | 荣誉成就（需Token） |

---

## 👤 默认账号

| 用户名 | 密码 |
|--------|------|
| `admin` | `123456` |

登录后建议及时修改密码。

---

## ❓ 常见问题

**Q: 部署失败怎么办？**
A: 看日志，通常是依赖安装失败。重新触发部署试试。

**Q: 接口返回404？**
A: 检查地址对不对，接口路径前面都要加 `/api`。

**Q: 跨域问题？**
A: 后端已经配置了 CORS，所有域名都可以访问，不用担心。

**Q: 用户数据丢了？**
A: 没加持久化磁盘的话，重新部署就会重置。加个磁盘就好了。

---

## 📱 配合前端使用

后端部署好后，把后端地址配置到前端的环境变量里，前端就能正常使用了。

详细步骤看前端包的 README。

---

有问题随时问我，祝你部署顺利！🐻
