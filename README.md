# PushFeed: Telegram RSS Bot

> 🎉 本项目基于 [ecouus/Feed-Push](https://github.com/ecouus/Feed-Push) 构建，提供 **支持多架构（amd64/arm64）的Docker镜像**

## 🧐 项目特点

PushFeed 可以将你关注的网站或博客的最新更新自动通过 Bot 进行推送，实现信息的即时传递。

**架构支持**:
- ✅ linux/amd64（x86_64）
- ✅ linux/arm64（包括Apple Silicon、树莓派等ARM设备）


## 🛠️ 安装部署

推荐使用docker-compose：

创建 `docker-compose.yml` 文件：
```yaml
services:
  pushfeed:
    image: vitoegg/pushfeed:latest
    container_name: pushfeed
    restart: always
    volumes:
      - ./data:/app/data
    environment:
      - TELEGRAM_BOT_TOKEN=bot_token  # 替换为你的Bot Token
      - ROOT_ID=admin_id  # 替换为你的Telegram ID
      - WHITELIST_GROUP_ID=-123456
      - ENABLE_GROUP_VERIFY=false
      - UPDATE_INTERVAL=300
```

然后启动服务：
```bash
docker-compose up -d
```

## 📖 使用说明

**输入 `/help` 获取指令帮助！**

### 环境变量说明

- **TELEGRAM_BOT_TOKEN**: 在 Telegram 上通过 @BotFather 创建 Bot 时获得的 Token
- **ROOT_ID**: 你的 Telegram 用户 ID，可以通过 @userinfobot 获取
- **WHITELIST_GROUP_ID**: 群组 ID，用于验证用户是否在指定群组中
- **ENABLE_GROUP_VERIFY**: 是否启用群组验证功能（true/false）
- **UPDATE_INTERVAL**: RSS 源更新的时间间隔，单位为秒，默认300s

**修改配置后重启容器：**
```bash
docker-compose down
docker-compose up -d
```

**更新到最新版本：**
```bash
docker-compose pull
docker-compose up -d
```

## 🔄 更新机制

本项目通过 GitHub Actions 自动监测上游仓库更新：
- ✅ 每天自动检查上游代码是否有更新
- ✅ 发现更新后自动构建多架构Docker镜像
- ✅ 自动推送到Docker Hub: `vitoegg/pushfeed`

## 📝 致谢

感谢 [ecouus/Feed-Push](https://github.com/ecouus/Feed-Push) 提供的基础代码和功能支持！


**如需查看源代码或参与开发：**
请访问上游项目：[ecouus/Feed-Push](https://github.com/ecouus/Feed-Push)

## 📦 Docker镜像

- **镜像地址**: [vitoegg/pushfeed](https://hub.docker.com/r/vitoegg/pushfeed)
- **支持架构**: linux/amd64, linux/arm64
- **更新频率**: 每天检查上游更新

## 📄 License

This project is licensed under the GNU General Public License v3.0.  
See the [LICENSE](LICENSE) file for details.
