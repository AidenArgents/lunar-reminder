# 农历初一十五提醒日历（2026—2126）

给 iPhone 自带「日历」使用的免费日历订阅文件。无需购买域名、无需部署服务器、无需安装第三方提醒 App。

## 文件说明

- `calendar.ics`：主订阅文件。2026-01-01 至 2126-12-31 之间，所有推算的农历初一、十五各一条事件，**北京时间上午 09:00**，包含 `VALARM` 显示提醒指令。合计 2,499 条独立日程。
- `date-list.csv`：核对表，可搜索具体日期；不需要上传到 GitHub。
- `generate_calendar.py`：可复现的日历生成脚本（需要 Python + pyswisseph + scipy）。如未来修订日期，可重生成并上传文件。
- `icu_dates.js` / `compare.py`（可选）：研发时的交叉比较脚本。

## 发布到 GitHub Pages（零成本）

1. 用你的 GitHub 账号新建一个**公开**仓库，名称建议 `lunar-reminder`。
2. 将 `calendar.ics` 上传到仓库根目录并提交；`README.md` 可一并上传。
3. 进入仓库 `Settings` → `Pages` → `Build and deployment` → `Deploy from a branch` → 选 `main` 分支、`/(root)` → `Save`。
4. 发布后，订阅地址为：

   `https://你的GitHub用户名.github.io/lunar-reminder/calendar.ics`

   替换为实际用户名。**不需要单独买域名。**

提示：GitHub Pages 适用于 GitHub Free 的公开仓库，Pages 站点须保持可访问。日后在仓库里更新 `calendar.ics`、保持文件路径不变，苹果订阅端会按系统节奏重新拉取数据。

## 在 iPhone 上开启订阅和通知

1. 打开「日历」→ 底部「日历」→「添加日历」→「添加订阅日历」，粘贴上面的 `https://...calendar.ics` 网址并订阅。
2. 订阅后，日历列表找到「农历初一十五提醒」→ 旁边 `ⓘ` → 打开「日程提醒」。
3. 进入「设置」→「通知」→「日历」，打开「允许通知」「声音」「锁定屏幕」。静音或专注模式可能影响声音提醒。
4. 检查 2026 年 10 月 24 日（农历九月十五）上午 09:00 的日程是否显示「今天农历十五」并包含提醒。
5. **务必用一条临近日期的测试事件实际验证通知**。标准文件中有提醒字段，不等于所有 iOS 设置都会保证响铃。可在 `generate_test_alert.py` 所在目录运行脚本生成 15 分钟后的测试日历并临时订阅测试地址。

## 农历数据的准确性和边界

- 按**北京时间（UTC+08:00）**计算朔日，即每个农历月初一；十五是初一之后第 14 天。因为每个朔望月都生成记录，**包含闰月**，无需另外识别闰月名称。
- 使用 Swiss Ephemeris（Moshier 实现）推算新月合朔时刻；2026—2100 年与香港天文台公开的农历对照表进行了**部分关键年份/特殊日期核查**，**并未逐年逐日完成 75 年全量官方核验**。
- 对两个有官方公布、容易出现一天误差的朔日，覆盖采用香港天文台日期：**2057-09-28**、**2097-08-07**。2089-09-04 也与香港天文台一致。
- **2101—2126 年没有香港天文台的公开逐日对照表**，当前生成的是天文推算结果，近午夜的合朔日尤其有误差风险。它是可维护的百年预测日历，**不能承诺未来 100 年每个日期 100% 无误**。如果未来有权威更新，改动 GitHub 仓库中的 `calendar.ics` 即可。
- 未来远期使用建议定期复核；如果用于严肃宗教或民俗安排，请在临近日期再次核对通行历法。

## 来源

- [苹果官方：设置多个日历、订阅日历、订阅日程通知](https://support.apple.com/en-ca/guide/iphone/iph3d1110d4/ios)
- [香港天文台：1901—2100 公历与农历对照表及特殊日期不确定性](https://www.hko.gov.hk/sc/gts/time/conversion.htm)
- [香港天文台 2057 年对照表](https://www.hko.gov.hk/en/gts/time/calendar/text/files/T2057e.txt)
- [香港天文台 2097 年对照表](https://www.hko.gov.hk/en/gts/time/calendar/text/files/T2097e.txt)
- [GitHub Pages 官方设置说明](https://docs.github.com/en/pages/quickstart)
