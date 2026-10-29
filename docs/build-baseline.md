# DP-01 本地构建基线

仅构建既有后端与 Web 管理端，不启动服务、不连接数据库；桌面打包不属于本次验证。所有命令从仓库根执行，除非注明子目录。构建不等于运行验收。

## 工具选择

验证主机：macOS 26.6.2 / arm64。Maven 3.9.9，Azul Zulu JDK 21.0.13（包 21.54.109），Node 24.22.1，npm 10.9.2。根 POM 要求 Java 21；Web package.json 要求 Node >=24。原默认 Java 17.0.15、Node 23.11.0 不满足要求。

不修改 shell 初始化文件、系统 JDK 注册、Homebrew 链接或全局 JAVA_HOME。`scripts/java21` 只为子进程设置 JAVA_HOME/PATH，默认读取 `.local/jdk-21`；可通过 `PROJECT_JAVA_HOME` 指向其他完整 JDK 21。`.local/` 已忽略，不提交二进制或原始本地日志。

### 在本机重建 JDK（macOS arm64）

固定下载地址，不跟随 latest；SHA-256 来自 Azul 包元数据 API 的 `sha256_hash`（包 UUID `f2caf8b1-ed9c-4405-9145-06f58c4fc129`）。仅适用于该平台；其他平台选择对应 JDK 21 并设置 PROJECT_JAVA_HOME。

```bash
mkdir -p .local/dp-01
curl -fL --retry 2 --max-time 180 \
  https://cdn.azul.com/zulu/bin/zulu21.54.109-ca-jdk21.0.13.0.3-macosx_aarch64.tar.gz \
  -o .local/dp-01/jdk.tar.gz
echo '3fb0c7b00d48e833ad7a1ab1001c9d44cd130be20c198a4744f318592d83af40  .local/dp-01/jdk.tar.gz' | shasum -a 256 -c -
tar -xzf .local/dp-01/jdk.tar.gz -C .local/dp-01
# 已有 .local/jdk-21 时先检查，不覆盖。
ln -s dp-01/zulu21.54.109-ca-jdk21.0.13.0.3-macosx_aarch64/Contents/Home .local/jdk-21
```

### 后端

```bash
./scripts/java21 java -version
./scripts/java21 mvn -version
./scripts/java21 mvn -B -ntp -f QuickBlue-MicroAI/pom.xml clean verify
```

`clean verify` 构建完整 reactor（含既有 AI/business/admin），包含编译、test 和打包阶段，不传 skipTests。仅有的 Java 测试源 InterceptorTest.java 为零字节，不能将 Maven 成功解释为后端行为测试通过。未为 DP-01 新增业务测试或启动集成环境。

### 前端

本机已有 Codex 附带 Node 24.22.1；使用命令级 PATH 选择它，npm 沿用已有 10.9.2。普通终端也可指定同版本 Node 安装的 bin 目录。以下路径仅为本机路径，不是仓库依赖。

```bash
cd QuickBule-MicroAI-web
NODE24_BIN=/Users/wanna/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin
env PATH="$NODE24_BIN:$PATH" node --version
env PATH="$NODE24_BIN:$PATH" npm --version
env PATH="$NODE24_BIN:$PATH" npm ci --no-audit --no-fund
env PATH="$NODE24_BIN:$PATH" npm run build:prod
env PATH="$NODE24_BIN:$PATH" npm run test:run
```

使用现有 package-lock.json，不使用 npm install 重新解析版本。npm ci 会重建 node_modules，build:prod 会重建 dist；不要把这两个目录用于保存手工修改。该构建只生成本地静态产物，不部署或调用生产服务。

## 可重现性边界

后端没有 Maven Wrapper 或依赖锁文件，现有 POM 固定直接版本但仍依赖外部仓库、传递依赖和本地 Maven 设置/缓存；不能声称离线或字节级可重现。前端保留现有锁文件。本任务不做整仓依赖升级。完整结果、原有失败、未验证项与许可边界见 DP-01 交付报告。
