# GLaDOS / Railgun 自动签到 + 积分兑换脚本

这是一个兼容 Loon / Surge / Quantumult X 的签到脚本，用于自动签到 GLaDOS / Railgun，并在积分达到阈值时尝试兑换计划。

## 功能

- 自动抓取并保存 Cookie
- 支持多个域名（glados.cloud、railgun.info 等）
- 自动签到
- 处理重复签到 / 设备不匹配
- 自动按平台切换 UA 继续重试
- 自动尝试兑换积分（可配置）
- 兼容 Loon / Surge / QX

## 目录说明

- `GLaDOS_Railgun_Checkin.js`：主脚本

## 使用方式

### 1. 安装脚本

将 `GLaDOS_Railgun_Checkin.js` 保存到对应平台的脚本目录中，并在配置中引用。

### 2. 抓取 Cookie

访问以下页面任一地址：

- `https://glados.cloud/console/account`
- `https://railgun.info/console/account`

在页面中登录并打开账号页面后，脚本会自动抓取并保存 Cookie。

### 3. Loon / Surge / QX 配置示例

```ini
[Script]
http-request ^https:\/\/(?:glados\.(?:cloud|network|rocks|one|space|vip)|railgun\.info|glados-facility\.com)\/console\/account$ script-path=https://你的脚本地址/GLaDOS_Railgun_Checkin.js, requires-body=false, timeout=30, tag=GLaDOS获取Cookie
cron "10 7 * * *" script-path=https://你的脚本地址/GLaDOS_Railgun_Checkin.js, timeout=60, tag=GLaDOS签到, enable=true

[MITM]
hostname = glados.cloud, railgun.info, glados.network, glados.rocks, glados.one, glados.space, glados.vip, glados-facility.com
```

### 4. 说明

- 需要开启 MitM 并信任证书
- 若脚本提示“设备不匹配”，脚本会自动切换 UA 重试
- 可修改 `EXCHANGE_PLAN` 以开启/关闭积分兑换

## 变量说明

```javascript
var EXCHANGE_PLAN = "plan500";
```

- `plan500`：积分达到 500 自动兑换
- `plan100` / `plan200`：可按需要修改
- `""`：关闭自动兑换

## 免责声明

仅供学习和自用，请遵守相关网站的使用条款和当地法律法规。
