# ShizuSU-Apps

ShizuSU 官方 **Android 应用仓库**（APK 商店源）。与 [ShizuSU-Modules](https://github.com/qianyumeng0228/ShizuSU-Modules)（模块仓库）配套：后者分发 Magisk/KSU 模块 zip，本仓库分发配套的 Android APK 应用。

- 仓库地址：https://github.com/qianyumeng0228/ShizuSU-Apps
- 商店源（GitHub Pages）：https://qianyumeng0228.github.io/ShizuSU-Apps/
- 商店索引文件：[`apps.json`](apps.json)（仓库根目录）

---

## apps.json 结构规范

`apps.json` 为一个顶层对象，`apps` 字段是应用条目数组。字段风格与 ShizuSU-Modules 的 `modules.json` 对齐。

```json
{
  "apps": [
    {
      "id": "app-id",
      "name": "应用名",
      "package": "com.example.app",
      "versionName": "1.0.0",
      "versionCode": 100,
      "summary": "简介",
      "author": "作者",
      "downloadUrl": "https://github.com/qianyumeng0228/ShizuSU-Apps/raw/main/private/<id>.apk",
      "updatedAt": "2026-10-09"
    }
  ]
}
```

| 字段 | 类型 | 说明 |
|---|---|---|
| `id` | string | 应用唯一 ID（小写字母/数字/下划线），与 APK 文件名一致 |
| `name` | string | 商店展示名 |
| `package` | string | Android 包名（manifest applicationId） |
| `versionName` | string | 版本名，如 `1.0.0` |
| `versionCode` | int | 版本号（整数），升级必须递增 |
| `summary` | string | 一句话简介（商店列表用） |
| `author` | string | 作者 |
| `downloadUrl` | string | APK 直链，固定走 `raw/main/private/<id>.apk` |
| `updatedAt` | string | 更新日期 `YYYY-MM-DD`（或 ISO8601 时间戳） |

> APK 本体放在 `private/<id>.apk`，`downloadUrl` 指向 `raw/main/private/<id>.apk`。

---

## 上传指引

1. 准备签名 release APK，命名 `<id>.apk`。
2. 把 APK 推到本仓库 `private/<id>.apk`。
3. 在 `apps.json` 的 `apps` 数组里新增/更新对应条目（同 `id` 去重，升级时递增 `versionCode`、更新 `updatedAt` 与 `downloadUrl`）。
4. 一次提交（`private/<id>.apk` + `apps.json`）推到 `main`。
5. GitHub Pages 从 `main` 根目录自动发布，商店端刷新即可看到。

> 权限：推送需要对本仓库的 Contents 写权限。
