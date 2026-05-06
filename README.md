# Interpark 抢票机器人
自动填表工具，帮助快速填写订单信息。

在公用的电脑，建议不要填入自己所有的信用卡资料，以避免个人的资料遭其他共用电脑的使用者被盗用。

目前抢票机器人因为 CloudFlare 已无法使用, 需要找时间把脚本从 selenium 改写为 DrissionPage 或 nodriver 格式。

# 功能
* 自动登录 interpark 或 facebook 账号。
* 会自动按「Buy Tickets」的按钮。
* 自动选取第1个可以购买的场次。
* 自动选取第1个可以购买的时间。
* 自动关闭「Booking Info」信息框。
* 自动关闭「Secure Booking service」说明信息框。
* 自动填入个人/信用卡资料。
* 自动勾选 I agree。

# 使用方法

## 环境准备
1. 安装 Python: https://www.python.org/downloads/

2. 安装依赖包:
```bash
pip install selenium chromedriver-autoinstaller
```

3. 运行配置界面:
```bash
python settings.py
```

4. 运行抢票程序:
```bash
python interpark_bot.py
```

# 配置文件说明

配置文件为 `settings.json`，可通过 `python settings.py` 图形界面配置，也可手动编辑。

## 基本设置

| 字段 | 说明 | 示例 |
|------|------|------|
| `homepage` | 要访问的页面URL（票务页面链接） | `https://www.globalinterpark.com/product/23010160?lang=zh-CN` |
| `browser` | 浏览器类型 | `chrome` (可选: chrome, brave, edge, safari, firefox) |
| `webdriver_type` | WebDriver类型 | `selenium` (可选: selenium, undetected_chromedriver) |
| `locale` | 网站语言 | `中文` (可选: 中文, 한국어, 日本語) |
| `language` | 界面语言 | `zh_TW` (可选: zh_TW, en_US, ko_KR, ja_JP) |

## 高级设置 (advanced)

| 字段 | 说明 | 示例 |
|------|------|------|
| `verbose` | 调试模式，显示详细日志 | `false` |
| `headless` | 无头模式（不显示浏览器） | `false` 建议设为 false 方便查看 |
| `adblock_plus_enable` | 启用广告拦截插件 | `false` |
| `interpark_account` | Interpark账号（用于自动登录） | `your@email.com` |
| `interpark_password` | Interpark密码 | 密码 |
| `facebook_account` | Facebook账号（备用登录） | `your@email.com` |
| `facebook_password` | Facebook密码 | 密码 |

## 日期/时间自动选择

### date_auto_select (日期选择)

| 字段 | 说明 | 示例 |
|------|------|------|
| `enable` | 是否启用自动选日期 | `true` / `false` |
| `mode` | 选日期方式 | `from top to bottom` / `from bottom to top` / `random` |
| `date_keyword` | 日期关键字（留空选第一个） | `2024-12-25` 或 `25` |

### time_auto_select (时间选择)

| 字段 | 说明 | 示例 |
|------|------|------|
| `enable` | 是否启用自动选时间 | `true` / `false` |
| `mode` | 选时间方式 | `from top to bottom` / `from bottom to top` / `random` |
| `time_keyword` | 时间关键字（留空选第一个） | `19:00` 或 `晚上7点` |

## 个人信息（必填）

| 字段 | 说明 |
|------|------|
| `user_name` | 真实姓名（必须与信用卡持卡人一致） |
| `user_date_of_birth_year` | 出生年份（4位数），如 `1990` |
| `user_date_of_birth_month` | 出生月份（2位数），如 `01` |
| `user_date_of_birth_day` | 出生日期（2位数），如 `15` |
| `user_email` | 电子邮箱 |
| `user_phone_number` | 联系电话 |
| `user_cell_phone` | 手机号码 |

## 支付信息（必填）

| 字段 | 说明 |
|------|------|
| `foreign_card` | 是否是外国信用卡 (`true`=外国卡, `false`=韩国本地卡) |
| `credit_card_type` | 信用卡类型（外国卡填写），如 `VISA`, `MASTER`, `JCB` |
| `cc_number` | 信用卡号（16位） |
| `cc_exp_month` | 信用卡过期月份（2位数），如 `12` |
| `cc_exp_year` | 信用卡过期年份（4位数），如 `2025` |

## 验证码识别

| 字段 | 说明 |
|------|------|
| `ocr_captcha.enable` | 是否启用自动识别验证码 (`需要安装 ddddocr`) |
| `ocr_captcha.beta` | 是否使用 beta 版模型（识别率更高） |

> 注意：`ddddocr` 仅支持 Intel CPU，ARM (M1/M2) Mac 无法使用

## 其他设置

| 字段 | 说明 |
|------|------|
| `keyword_exclude` | 排除关键字，带有这些关键字的场次会被排除，多个用逗号分隔，如 `VIP,最贵` |

# 建议

限量的订位系统是残酷的，建议不要用破旧电脑或连线不稳的手机网络来抢，因为只要比别人慢个 0.1 秒，名额可能就没了。为了要抢到限量的名额，真心建议去网咖或找一个网络连线稳定且快的地方并使用硬件不差的电脑来抢位子。
