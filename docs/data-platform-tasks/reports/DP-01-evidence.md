# DP-01 验证证据（2026-10-29，Asia/Shanghai）

## 初始 Git 状态

```text
 M README.md
?? docs/Data_Platform_Product_Plan_V1.md
?? docs/Data_Platform_Source_Reuse_Assessment.md
?? docs/QuickBlue_NextGen_Product_Roadmap.md
?? docs/data-platform-tasks/
```

初始分支：main；baseline：ac261b8de9a8e4db4eb915617cf3ea8063d04138。
所有 Web 源码、package.json、package-lock.json 和后端源码/POM 在首次验证前均无修改。

## 前端原始结果摘录

`npm ci --no-audit --no-fund`：退出码 0，673 packages；安装弃用警告保留在本地日志。
`npm run build:prod`：退出码 0，Vite 8.2.1，3827 modules transformed，built in 6.19s。
构建警告：CSS :deep 选择器、超过 500 kB 的 chunk、插件耗时；不修改业务样式或拆包策略。
`npm run test:run`：退出码 1。以下为失败摘要（测试数据，不含业务样本）：

```text
 FAIL  src/_diag.test.js [ src/_diag.test.js ]
Error: No test suite found in file /Users/wanna/tk/code/QuickBlue-MicroAI/QuickBule-MicroAI-web/src/_diag.test.js
 FAIL  src/lib/encrypt.test.js > encrypt > 基本功能测试 > 应该能够加密和解密空字符串
AssertionError: expected null to be '' // Object.is equality
 FAIL  src/lib/encrypt.test.js > encrypt > 基本功能测试 > 应该能够加密和解密特殊字符
AssertionError: expected '!@#$%^&*()_+-={}[]|\\:\";\'<>?,./`~' to be '!@#$%^&*()_+-={}[]|\:";\'<>?,./`~' // Object.is equality
 FAIL  src/lib/encrypt.test.js > encrypt > 边界情况测试 > 应该能够加密和解密零值
AssertionError: expected null to be '0' // Object.is equality
 FAIL  src/lib/encrypt.test.js > encrypt > 错误处理测试 > 应该能够处理解密错误数据而不抛出异常
AssertionError: expected [Function] to not throw an error but 'Error: Malformed UTF-8 data' was thrown
 FAIL  src/lib/encrypt.test.js > encrypt > 错误处理测试 > 解密错误数据应该返回空字符串或无效结果
Error: Malformed UTF-8 data
 FAIL  src/lib/encrypt.test.js > encrypt > Unicode和特殊字符测试 > 应该能够处理换行符和制表符
AssertionError: expected 'line1\nline2\ttab' to be 'line1\nline2\ttab' // Object.is equality
 FAIL  src/lib/encrypt.test.js > encrypt > Unicode和特殊字符测试 > 应该能够处理JSON格式的字符串
AssertionError: expected '{\"key\":\"value\",\"number\":123}' to be '{"key":"value","number":123}' // Object.is equality
 FAIL  src/lib/sentry.test.js > sentry > axios错误过滤测试 > 应该处理部分axios错误属性的情况
AssertionError: expected "vi.fn()" to not be called at all, but actually been called 1 times
 FAIL  src/lib/sentry.test.js > sentry > 边界情况测试 > 应该处理undefined错误
AssertionError: expected [Function] to not throw an error but 'TypeError: Cannot read properties of …' was thrown
 FAIL  src/lib/sentry.test.js > sentry > 边界情况测试 > 应该处理null错误
AssertionError: expected [Function] to not throw an error but 'TypeError: Cannot read properties of …' was thrown
 FAIL  src/lib/table-auto-height.test.js > table-auto-height > store状态影响测试 > 应该考虑pageTagFlag对高度的影响
 FAIL  src/lib/table-auto-height.test.js > table-auto-height > store状态影响测试 > 应该考虑footerFlag对高度的影响
 FAIL  src/lib/table-auto-height.test.js > table-auto-height > store状态影响测试 > 应该同时考虑pageTagFlag和footerFlag
Error: Cannot find module '/@/config/app-config' imported from /Users/wanna/tk/code/QuickBlue-MicroAI/QuickBule-MicroAI-web/src/store/modules/system/app-config.js
 FAIL  src/plugins/enums-plugin.test.js > enums-plugin > 错误处理测试 > 应该正确记录错误信息
AssertionError: expected "vi.fn()" to be called with arguments: [ StringContaining "无法找到变量名称", …(1) ]
 FAIL  src/plugins/enums-plugin.test.js > enums-plugin > 错误处理测试 > getValueDescList应该正确记录错误信息
AssertionError: expected "vi.fn()" to be called with arguments: [ StringContaining "无法找到变量名称", …(1) ]
 FAIL  src/plugins/enums-plugin.test.js > enums-plugin > 错误处理测试 > getValueDesc应该正确记录错误信息
AssertionError: expected "vi.fn()" to be called with arguments: [ StringContaining "无法找到变量名称", …(1) ]
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerHyphen > 应该处理已有中划线的字符串
AssertionError: expected 'y-component' to be 'my-component' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerHyphen > 应该处理小写开头的驼峰
AssertionError: expected 'y-component' to be 'my-component' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerHyphen > 应该处理全大写字符串
AssertionError: expected 'a-b-c' to be '-a-b-c' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertUpperCamel > 应该处理下划线开头
AssertionError: expected 'PrivateVar' to be '_private_var' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerCamel > 应该处理连续下划线
AssertionError: expected 'my_component' to be 'My_component' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerCamel > 应该处理数字
AssertionError: expected 'test123' to be 'Test123' // Object.is equality
 FAIL  src/utils/str-util.test.js > str-util.js > convertLowerCamel > 应该处理下划线开头
AssertionError: expected 'PrivateVar' to be '_private_var' // Object.is equality
 Test Files  6 failed | 4 passed (10)
      Tests  23 failed | 238 passed (261)
```

## 固定版本与许可材料

根 LICENSE 声明 Apache-2.0；Web package.json 声明 MIT。保持原声明，不将开源项目或顶层许可证等同于所有传递依赖均已完成许可审核。JDK 分发包保留自带 legal 目录，仅存放本地，不提交二进制。依赖许可证/NOTICE 全量汇总及再分发审核未执行。

根 POM 属性版本（现有声明，无升级）：

```text
QuickBlue.version=4.0.0
java.version=21
lombok.version=1.18.46
spring-boot.version=4.1.1
spring-cloud.version=2025.1.3
spring-cloud-alibaba.version=2025.1.0.0
nacos.version=2.4.3
mysql-connector.version=8.0.33
druid.version=1.2.28
mybatis-plus.version=3.5.17
mybatis-plus-spring-boot4.version=3.5.17
p6spy.version=3.9.1
redisson.version=4.7.0
caffeine.version=3.1.8
sa-token.version=1.46.0
sa-token-core.version=1.46.0
hutool.version=5.8.39
guava.version=33.4.8-jre
fastjson2.version=2.0.58
commons-io.version=2.18.0
commons-lang3.version=3.18.0
commons-collections4.version=4.4
commons-codec.version=1.17.1
commons-compress.version=1.27.1
commons-text.version=1.13.0
easyexcel.version=4.0.3
poi.version=5.4.1
velocity.version=2.4.1
velocity-tools.version=3.1
freemarker.version=2.3.34
jsoup.version=1.21.1
zxing.version=3.5.3
tinypinyin.version=2.0.3
ip2region.version=2.7.0
bouncycastle.version=1.80
resilience4j.version=2.4.0
aws-java-sdk-s3.version=2.31.78
rocketmq-spring-boot.version=2.3.6
sentinel.version=1.8.8
okhttp.version=4.12.0
feign-okhttp.version=13.1
knife4j.version=5.4.0
springdoc.version=3.1.0
swagger.version=2.2.47
spring-boot-admin.version=4.1.2
```

文件 SHA-256：

```text
03e6c8b0c336f566be22f69dd0b741eac0a11c78031f52b3de098393eacfa2d3  QuickBlue-MicroAI/pom.xml
964a9da28264c8d38cb2286b76fa4d98b6e6b396194cbb57ae1134c442270099  QuickBule-MicroAI-web/package.json
081e444ff6957fa7994cc99e3d56f0d0eae0d78d5b33cc1d99c7f52e8d2df25d  QuickBule-MicroAI-web/package-lock.json
c71d239df91726fc519c6eb72d318ec65820627232b2f796219e87dcf35d0ab4  LICENSE
```

本地完整日志位于 `.local/dp-01/`，不提交生成物或可能含环境信息的完整日志。以上摘要和退出码来自实际执行。

## 后端在线构建

实际命令：`./scripts/java21 mvn -B -ntp -f QuickBlue-MicroAI/pom.xml clean verify`，退出码 0。

```text
[INFO] Reactor Summary for QuickBlue MicroAI 4.0.0:
[INFO]
[INFO] QuickBlue MicroAI .................................. SUCCESS [  0.051 s]
[INFO] QuickBlue Common ................................... SUCCESS [  0.001 s]
[INFO] QuickBlue Common Core .............................. SUCCESS [  8.268 s]
[INFO] QuickBlue Common Web ............................... SUCCESS [ 10.920 s]
[INFO] QuickBlue Common Redis ............................. SUCCESS [  6.824 s]
[INFO] QuickBlue Common Security .......................... SUCCESS [  1.722 s]
[INFO] QuickBlue Common Database .......................... SUCCESS [  5.858 s]
[INFO] QuickBlue Common Swagger ........................... SUCCESS [  3.323 s]
[INFO] QuickBlue API ...................................... SUCCESS [  0.001 s]
[INFO] QuickBlue API System ............................... SUCCESS [  5.928 s]
[INFO] QuickBlue Common Log ............................... SUCCESS [  0.024 s]
[INFO] QuickBlue Common Excel ............................. SUCCESS [  0.169 s]
[INFO] QuickBlue API Business ............................. SUCCESS [  0.154 s]
[INFO] QuickBlue API Support .............................. SUCCESS [  0.214 s]
[INFO] QuickBlue API AI ................................... SUCCESS [  0.157 s]
[INFO] QuickBlue Modules .................................. SUCCESS [  0.000 s]
[INFO] QuickBlue System Service ........................... SUCCESS [ 14.854 s]
[INFO] QuickBlue Business Service ......................... SUCCESS [  0.631 s]
[INFO] QuickBlue Support Service .......................... SUCCESS [ 21.748 s]
[INFO] QuickBlue AI Service ............................... SUCCESS [02:05 min]
[INFO] QuickBlue Gateway .................................. SUCCESS [  8.785 s]
[INFO] QuickBlue Admin .................................... SUCCESS [  3.579 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  03:47 min
[INFO] Finished at: 2026-10-29T21:18:40+08:00
[INFO] ------------------------------------------------------------------------
```

现有测试阶段实际输出 `No tests to run.`；唯一 Java 测试源为空文件，没有有效测试用例。构建警告包括既有 MySQL 驱动坐标迁移提示和 Lombok equals/hashCode 超类调用提示，本任务没有修改对应行为。

## 离线诊断

实际命令：`./scripts/java21 mvn -o -B -ntp -f QuickBlue-MicroAI/pom.xml validate`，退出码 1。该诊断在在线构建过程中执行，仅定位缓存条件，不写编译产物。

```text
[ERROR] Plugin org.springframework.boot:spring-boot-maven-plugin:4.1.1 or one of its dependencies could not be resolved:
[ERROR] 	Cannot access central (https://repo.maven.apache.org/maven2) in offline mode and the artifact org.springframework.boot:spring-boot-maven-plugin:jar:4.1.1 has not been downloaded from it before.
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/PluginResolutionException
```

## Launcher 验证

以下命令从 `/tmp` 执行，ROOT 为仓库绝对路径（仅作摘要替换）：

```text
command=['bash', '-n', '$ROOT/scripts/java21'], overrides={}
exit=0

command=['zsh', '-f', '-c', '$ROOT/scripts/java21 java -version; java -version'], overrides={}
exit=0
openjdk version "21.0.13.0.3" 2026-10-24 LTS
OpenJDK Runtime Environment Zulu21.54+109-CA (build 21.0.13.0.3+1-LTS)
OpenJDK 64-Bit Server VM Zulu21.54+109-CA (build 21.0.13.0.3+1-LTS, mixed mode, sharing)
java version "17.0.15" 2025-04-15 LTS
Java(TM) SE Runtime Environment (build 17.0.15+9-LTS-241)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.15+9-LTS-241, mixed mode, sharing)

command=['$ROOT/scripts/java21', 'mvn', '-version'], overrides={}
exit=0
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /opt/homebrew/Cellar/maven/3.9.9/libexec
Java version: 21.0.13.0.3, vendor: Azul Systems, Inc., runtime: $ROOT/.local/dp-01/zulu21.54.109-ca-jdk21.0.13.0.3-macosx_aarch64/Contents/Home
Default locale: zh_CN_#Hans, platform encoding: UTF-8
OS name: "mac os x", version: "26.6.2", arch: "aarch64", family: "mac"

command=['$ROOT/scripts/java21'], overrides={}
exit=2
Usage: scripts/java21 <command> [args...]

command=['$ROOT/scripts/java21', 'java', '-version'], overrides={'PROJECT_JAVA_HOME': '/nonexistent'}
exit=2
JDK 21 missing: set PROJECT_JAVA_HOME or install at .local/jdk-21 (see docs/build-baseline.md).

command=['$ROOT/scripts/java21', 'java', '-version'], overrides={'PROJECT_JAVA_HOME': '/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home'}
exit=2
Expected JDK 21 at /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home; refusing to use another major version.

command=['$ROOT/scripts/java21', 'sh', '-c', 'exit 7'], overrides={}
exit=7

```

原始本地日志 SHA-256（便于核对当前工作区证据）：

```text
1623fce0e551aa9d0e271ab7d0549cc56a39a35df9bf02c52053990302d7bf95  .local/dp-01/npm-ci.log
51cfd771f98980476717dd14f18382101475e79b34bd97326ee4eda55ec89e84  .local/dp-01/frontend-build.log
8bad2fe3b3223b47b6b19577896cba83b39df2568195f5f2f9d35b85d6320644  .local/dp-01/frontend-test.log
ba32c91a9de84baebf67d597574f244c1a851975aa6288e7ad0cdd982ff4a33d  .local/dp-01/backend-build.log
da2ab6b39006a1cc9e7fc922ca052412a8e2c33be76aa64c7742d55264a9bf29  .local/dp-01/backend-offline-validate.log
50244d700ae186c49b285a85d85deac4ea171658aa23244a11f291e6a34efc88  .local/dp-01/launcher-checks.txt
```
