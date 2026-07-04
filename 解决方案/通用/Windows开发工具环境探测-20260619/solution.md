# Windows 本机开发工具环境探测与梳理

> 适用场景：梳理 / 沉淀本机已安装开发工具的版本、路径、环境变量，用于生成环境清单或排查构建问题
> 环境信息：Windows 11 Pro（10.0.26220）+ Git Bash
> 生成日期：2026-06-19

---

## 问题

要把本机所有开发工具（运行时、移动 SDK、数据库、编辑器等）的版本和路径整理成清单。难点在于：工具多、路径散、版本命令各异、部分工具（如 `sdkmanager`）不在 PATH，且容易踩到配置坑（如 `JAVA_HOME` 未设）。

## 原因

直接凭记忆或文档默认值列版本不可靠，**必须实测**；而实测又需要一套系统方法，避免逐个手敲或某个命令卡死拖垮整批探测。

## 解决方案：两步探测法

### 第一步：批量探测「存在性 + 路径」（快、不卡）

用 `command -v` 逐个判断，只返回路径、不取版本，秒级完成，不会因某个工具卡住：

```bash
for t in node npm npx pnpm yarn bun deno python python3 py pip pip3 conda \
         java javac mvn gradle git git-lfs docker docker-compose podman \
         flutter dart adb sdkmanager emulator go rustc cargo rustup \
         php composer ruby gem dotnet code cursor mysql sqlite3 openssl \
         make gcc clang cmake jq curl wget; do
  p=$(command -v "$t" 2>/dev/null) && echo "$t => $p" || echo "$t => (未安装)"
done
```

### 第二步：逐个取版本（只对存在的工具取）

版本命令各工具不同，注意几个特例，**逐个跑而非批量**，避免某个卡死整批：

```bash
node --version; npm --version; yarn --version
python --version; pip --version
java -version 2>&1          # 输出到 stderr，必须 2>&1
flutter --version 2>&1 | grep -E "^Flutter |^Dart "   # 过滤掉更新横幅
dart --version
dotnet --version; rustc --version; cargo --version
git --version; mysql --version; sqlite3 --version
openssl version; code --version
```

### Android SDK 深入探测（adb 在 PATH 但 sdkmanager 不在）

Android SDK 根目录 `$ANDROID_HOME` 下分多个子目录，需分别列；`sdkmanager` 藏在 `cmdline-tools/`：

```bash
SDK="$ANDROID_HOME"
ls "$SDK/build-tools"     # 如 31.0.0 ~ 37.0.0
ls "$SDK/platforms"       # android-31 ~ android-37.0
ls "$SDK/ndk"             # 如 28.2.13676358
ls "$SDK/cmdline-tools"   # sdkmanager 在 cmdline-tools/latest/bin/
"$SDK/platform-tools/adb" --version
```

### 环境变量检查

```bash
echo "ANDROID_HOME=$ANDROID_HOME"
echo "FLUTTER_ROOT=$FLUTTER_ROOT"
echo "PUB_CACHE=$PUB_CACHE"
echo "JAVA_HOME=$JAVA_HOME"
```

## 避坑点（本机实测发现的配置问题）

1. **`JAVA_HOME` 未设**：`java` 靠 Oracle javapath 能用，但 Flutter / Android Gradle 构建会因找不到 JDK 报错 —— 需手动将 `JAVA_HOME` 指向 JDK 目录
2. **Microsoft Store python3 stub 干扰**：PATH 里有 `C:\Users\<user>\AppData\Local\Microsoft\WindowsApps\python3`（Store 占位程序），实际生效的是真实安装目录的 Python，注意别被 stub 误导
3. **`sdkmanager` 不在 PATH**：需用全路径 `…\Android_SDK\cmdline-tools\latest\bin\sdkmanager.bat`
4. **JDK 版本与项目匹配**：本机 JDK 25（最新 LTS），某些旧 Android / 服务端项目需要 JDK 17 / 21，按项目要求切换
5. **Cursor 版本取法**：`cursor --version` 不一定可靠，可读 `D:\cursor\resources\app\package.json` 的 `version` 字段
6. **版本号不要编造**：必须实测命令输出，不能用文档默认值

## 验证方式

- 路径与版本交叉核对（`command -v` 给的路径 vs 版本命令能跑通）
- 配套版本要对应（如 Dart 3.11.4 ↔ Flutter 3.41.6）
- 环境变量值与实际安装目录一致

## 相关

- 本机工具的**实测清单结果**见 `通用/开发工具环境清单-20260619/prompt.md`（本 solution 是其探测方法论）
- 路径命名澄清：用户口语 "D:\Code.prompt" 实际指 "D:\Code\.prompt"（`.prompt` 是目录不是文件），目标歧义须先核实再动手
