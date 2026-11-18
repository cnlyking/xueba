# 成为学霸（XueBa）

一个给家里孩子用的安卓学习时间管理工具。手机或平板上装好后，孩子要先答题攒够时长，才能正常使用设备；时间到点，应用会把设备拉回锁定页，除答题外不能再做别的。

**本项目的全部代码、题库与界面均为自建内容，未包含任何第三方项目的代码或素材。**

---

## 功能

- **答题换时间**：每答对一组题，解锁一段可用时长
- **到点锁屏**：设定时间用完后，自动把设备拉到前台锁定页
- **答题才算有效时间**：在本应用内答题的时间不计入使用时长
- **两个独立上限**
  - 每次最多积累：一次答题最多能攒多少分钟
  - 每日最多使用：一天总共能用多久，到点直接锁死
- **错题本**：错题达到阈值后追加惩罚题
- **防卸载**：卸载或停用应用时要求输入家长密码
- **密码只设一次**：首次启动设置家长密码，之后不再重复询问
- **开机自启**，进程被杀后自动拉起

## 六个年级版本

题库按年级分开打包，六个安装包互不冲突，可以同时装（也可以只装对应年级的那一个）。

| 版本 | 安装包 | 题量 |
|---|---|---|
| 一年级 | [xueba-grade1-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade1-v2.1.apk) | 11481 道 |
| 二年级 | [xueba-grade2-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade2-v2.1.apk) | 10484 道 |
| 三年级 | [xueba-grade3-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade3-v2.1.apk) | 10133 道 |
| 四年级 | [xueba-grade4-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade4-v2.1.apk) | 12672 道 |
| 五年级 | [xueba-grade5-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade5-v2.1.apk) | 12999 道 |
| 六年级 | [xueba-grade6-v2.1.apk](https://github.com/cnlyking/xueba/releases/download/v2.1/xueba-grade6-v2.1.apk) | 10021 道 |

题目构成：数学为主（四则运算、单位换算、图形面积体积、分数小数百分数、应用题等，答案全部按公式计算生成），另含语文（反义词、近义词、成语释义、古诗接句、量词、标点、修辞、课文作者）和英语（单词中英互译、复数、be 动词、介词、时态、疑问词、日常对话）。一、二年级按教材进度不含英语。

## 安装

直接安装对应年级的 APK 即可，最低支持 Android 6.0（API 23）。

华为 / 鸿蒙设备需要额外两步，否则锁定时拉不到前台：

1. 打开「设置 → 应用 → 成为学霸 → 权限 → 后台弹出界面」，允许
2. 打开「设置 → 辅助功能 → 成为学霸 → 卸载保护」，开启

装好后首次启动会让你设置家长密码（建议记牢，忘了只能卸载重装）。

## 使用

1. 首页点「开始答题」，答完一组会累积可用时长
2. 时长用完，应用自动跳到锁定页，只有继续答题才能解锁
3. 「设置（家长使用）」里可以改密码、每次积累上限、每日使用上限、每组题数、正确率要求等

## 构建

```bash
# 需要 JDK 17+、Android SDK（platform 34 / build-tools 34.0.0）
gradle assembleRelease
```

产物在 `app/build/outputs/apk/grade{1..6}/release/`。

题库由 `tools/gen_math.py`、`tools/gen_cn.py`、`tools/gen_en.py` 生成，输出 JSON 放在 `app/src/grade{N}/assets/banks/`。

## 已知限制

- 华为设备上「后台弹出界面」权限无法通过 adb 授予，只能在系统设置里手动开
- 卸载保护的密码拦截依赖无障碍服务，被系统清理后需要重新开启
- 部分定制系统（MIUI / EMUI）会限制后台拉起，需要手动加白名单

## 许可

MIT，详见 [LICENSE](LICENSE)。仅供学习和家庭自用，请勿用于商业用途。
