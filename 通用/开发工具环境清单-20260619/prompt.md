# 开发工具环境清单

> 适用场景：查阅本机已安装开发工具的版本与路径，避免会话中重复探测；含常见但未安装工具的参考。
> 探测环境：Windows 11 Pro（10.0.26220.8680），Git Bash（MINGW64）
> 生成日期：2026-06-19
> 说明：版本与路径均为本机实测（非文档默认值）。工具变动后需重新生成。

---

## 一、运行时与语言

| 工具 | 版本 | 路径 |
|------|------|------|
| Node.js | v24.11.0 | D:\nodejs |
| npm | 11.6.1 | D:\nodejs |
| yarn | 1.22.22 | D:\npm_global |
| Python | 3.11.5 | D:\Python3.11.5 |
| pip | 23.2.1 | D:\Python3.11.5\Scripts |
| Java（JDK） | 25.0.1 LTS | D:\Java\jdk-25（PATH 经 Oracle javapath 接入） |
| .NET SDK | 10.0.103 | C:\Program Files\dotnet |
| Rust（rustc / cargo） | 1.91.1 | C:\Users\aaa\.cargo |
| Dart SDK | 3.11.4 | D:\Mobile_Development\Flutter\Flutter_SDK\bin |

## 二、移动开发

| 工具 | 版本 | 路径 |
|------|------|------|
| Flutter | 3.41.6（stable） | D:\Mobile_Development\Flutter\Flutter_SDK |
| Android SDK | 见明细 | D:\Mobile_Development\Android\Android_SDK |
| adb（platform-tools） | 1.0.41 | …\Android_SDK\platform-tools |

### Android SDK 明细
`ANDROID_HOME = D:\Mobile_Development\Android\Android_SDK`
- build-tools：31.0.0 ~ 37.0.0（含 33.0.x、35.0.x、36.1.0）
- platforms：android-31 ~ android-37.0
- ndk：28.2.13676358
- platform-tools：adb 1.0.41、sqlite3 3.50.6
- cmdline-tools：latest（sdkmanager 位于 `cmdline-tools\latest\bin\sdkmanager.bat`）
- 另含：emulator、system-images、cmake、sources

## 三、数据库

| 工具 | 版本 | 路径 |
|------|------|------|
| MySQL | 9.5.0 | C:\Program Files\MySQL\MySQL-Server-9.5 |
| SQLite | 3.50.6 | …\Android_SDK\platform-tools |

## 四、编辑器 / Git / 其他

| 工具 | 版本 | 路径 |
|------|------|------|
| VS Code | 1.120.0 | D:\Microsoft VS Code |
| Cursor | 3.3.16 | D:\cursor |
| Git | 2.54.0.windows.1 | Git for Windows（mingw64） |
| OpenSSL | 3.5.6 | mingw64 |
| curl / ssh | 随 Git for Windows | mingw64 / usr\bin |

## 五、关键环境变量

| 变量 | 值 |
|------|-----|
| ANDROID_HOME / ANDROID_SDK_ROOT | D:\Mobile_Development\Android\Android_SDK |
| FLUTTER_ROOT | D:\Mobile_Development\Flutter\Flutter_SDK |
| PUB_CACHE | D:\Mobile_Development\pub-cache |

## 六、常见但本机未安装（供参考，按需安装）

包管理 / 运行时：pnpm、bun、deno
语言：Go、PHP、Composer、Ruby
容器 / 编排：Docker、Docker Compose、kubectl、Helm
JVM 构建：Maven、Gradle（standalone）
云 / IaC：Terraform、AWS CLI、gcloud、Azure CLI
实用：jq、ffmpeg

## 七、注意事项

- **JAVA_HOME 未设置**：当前 `java` 经 Oracle javapath 接入可用，但环境变量 `JAVA_HOME` 未设置。Flutter / Android Gradle 构建若报 JDK 找不到，需手动设 `JAVA_HOME = D:\Java\jdk-25`。
- **Python PATH 冲突**：PATH 中存在 Microsoft Store 的 `python3` stub（`C:\Users\aaa\AppData\Local\Microsoft\WindowsApps`），实际生效的是 `D:\Python3.11.5`。
- **sdkmanager 不在 PATH**：需用全路径 `…\Android_SDK\cmdline-tools\latest\bin\sdkmanager.bat`。
- **JDK 版本较新**：JDK 25 为最新 LTS，部分旧 Android / 服务端项目可能需要 JDK 17 / 21，按项目要求切换。
