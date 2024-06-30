# Nop 组件包仓库（非官方）使用说明

![仓库构建状态](https://github.com/crazydan-studio/nop-repo/actions/workflows/deploy.yaml/badge.svg)

本仓库当前的构建信息如下：

- 每日构建计划：凌晨 2 点（东八区）
- 当前构建开始时间：`2024-07-01 02:17:00 +08:00`，构建总耗时 `4.68` 分钟
- 当前 Nop 组件包版本号：`2.0.0-SNAPSHOT`
- 当前 Nop 源码变更版本：[f4e727ff191f2e1639448c90be022b54603739a0](https://gitee.com/canonical-entropy/nop-entropy/tree/f4e727ff191f2e1639448c90be022b54603739a0)
- 额外构建的 Nop 项目如下：
  - [canonical-entropy/nop-extensions:1.0.0-SNAPSHOT](https://gitee.com/canonical-entropy/nop-extensions/tree/5eb156f8e98d41c97b252c22c4e3de372cc84e31)

> - 该仓库仅提供最后一次构建的产物，不保留既往构建产物，不能通过时间戳引入以前的构建版本
> - 若在构建计划周期内，Nop 源码没有发生更新，则不会再重复构建源码并发布组件包

注意，以下 Nop 工程模块的构建包未发布至本仓库（这些模块均不会被作为依赖引入到其他项目中）：

```ignore
build-tools
nop-all-for-spring
nop-auth/nop-auth-app
nop-auth/nop-auth-codegen
nop-batch/nop-batch-app
nop-batch/nop-batch-codegen
nop-benchmark
nop-demo
nop-demo/nop-delta-demo
nop-demo/nop-jdk17-demo
nop-demo/nop-orm-demo
nop-demo/nop-quarkus-demo
nop-demo/nop-rpc-client-demo
nop-demo/nop-rpc-server-demo
nop-demo/nop-spring-demo
nop-demo/nop-spring-demo-no-orm
nop-demo/nop-spring-demo2
nop-demo/nop-spring-report-demo
nop-demo/nop-spring-security-demo
nop-demo/nop-spring-simple-demo
nop-dev/nop-dev-app
nop-dev/nop-dev-codegen
nop-dyn/nop-dyn-app
nop-dyn/nop-dyn-codegen
nop-file/nop-file-app
nop-file/nop-file-codegen
nop-job/nop-job-app
nop-job/nop-job-codegen
nop-oauth/nop-oauth-app
nop-oauth/nop-oauth-codegen
nop-report/nop-report-app
nop-report/nop-report-codegen
nop-rule/nop-rule-app
nop-rule/nop-rule-codegen
nop-sys/nop-sys-app
nop-sys/nop-sys-codegen
nop-task/nop-task-app
nop-tcc/nop-tcc-app
nop-tcc/nop-tcc-codegen
nop-wf/nop-wf-app
nop-wf/nop-wf-codegen
tests
```

本仓库通过 Github Action 自动构建最新的
[Nop 源码](https://github.com/entropy-cloud/nop-entropy/)，并托管于
[Netlify](https://app.netlify.com) 之上：

- 本仓库主站点: https://nop.repo.crazydan.io
- 本仓库备用站点: https://crazydan-studio.github.io/nop-repo
- 本仓库源码: https://github.com/crazydan-studio/nop-repo

## 目录导航

- [免责声明](#免责声明)
- [Maven 仓库配置](#maven-仓库配置)
- [Nop 组件依赖引入](#nop-组件依赖引入)
- [Nop IDEA 插件安装](#nop-idea-插件安装)
- [Nop Cli 工具使用](#nop-cli-工具使用)

## 免责声明

本仓库由 [Crazydan Studio](https://studio.crazydan.org/) 团队构建并维护，
除了方便本团队的日常开发之外，也向 [Nop 开源社区](https://nop-platform.github.io)免费开放，
社区内任何有需要的朋友均可自由使用，没有任何限制和前提条件。

该仓库并非 Nop 官方仓库，也不是 Nop 开源社区运营的仓库，
因此，因使用本仓库所产生的任何风险和损失均需由您自行承担，
本团队及其成员将不承担因您的任何行为所造成的任何后果。
若您继续使用本仓库，则默认视为您已明确知晓相关风险，并承诺后果自负。

本团队承诺，不会主动在构建和发布的任何环节做任何危及信息安全的行为，
并且保证所构建的源码完全来自于官方仓库，不会对源码做任何修改。

但仍建议您在商业产品中慎重使用本仓库，优先选择自行构建
[Nop 源码](https://gitee.com/canonical-entropy/nop-entropy)，或等待官方仓库的发布。

若您有关于 Nop 开发相关的问题，请移步至
[Nop Issues](https://gitee.com/canonical-entropy/nop-entropy/issues) 页面提问。

> [Crazydan Studio](https://studio.crazydan.org/) 团队也会在
> https://nop.crazydan.io/ 站点上分享开发经验，您可以在开发过程中以其作为参考。

## Nop IDEA 插件安装

点击下载 [nop-idea-plugin-1.0-SNAPSHOT.zip](./nop-idea-plugin-1.0-SNAPSHOT.zip)，
完成后，进入 IDEA 的插件管理（`File -> Settings -> Plugins`），
点击齿轮图标，并选择 `Install Plugin from Disk ...`，再选中已下载的插件
`nop-idea-plugin-1.0-SNAPSHOT.zip` 以将其安装到 IDEA 中。

安装后需要清空 IDEA 缓存并重启：`File -> Invalidate Caches...`。

在启动 XLang 调试之前，需要为带静态 `#main` 函数的启动类 `XxxApplication`
新建一个 `XLang Runner` 类型的 `Run/Debug` 配置：

![](./assets/image/idea-xlang-debug-create-xlang-runner.png)

然后，选择 `XLangDebug` 以调试模式启动 `XxxApplication`：

![](./assets/image/idea-xlang-debug.png)

## Nop Cli 工具使用

点击下载
[nop-cli-2.0.0-BETA.1.jar](./io/github/entropy-cloud/nop-cli/2.0.0-BETA.1/nop-cli-2.0.0-BETA.1.jar)，
并在控制台执行相关命令：

```bash
# 注意，请根据当前运行环境修改 JDK 17+ 的安装路径
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk

${JAVA_HOME}/bin/java \
  -Dfile.encoding=UTF8 \
  -jar ./nop-cli-2.0.0-BETA.1.jar \
  gen -t=/nop/templates/orm \
  ./model/nop-demo.orm.xlsx
```

> 通过 `${JAVA_HOME}/bin/java -jar ./nop-cli-2.0.0-BETA.1.jar gen -h`
> 可查看 `gen` 子命令的详细参数说明。
> 其中，`-t` 选项所指向的是 Nop 工程中
> `nop-codegen/src/main/resources/_vfs/nop/templates/orm`
> 目录下的模板，`gen` 命令所生成的工程目录结构与该模板是一致的。

## Maven 仓库配置

对于第三方仓库，Maven 可以采用全局配置和项目配置两种引入方式：

- 前者将对环境内的所有项目有效，但需要项目开发和构建环境均做修改，改动范围较大
- 后者则仅对已配置的项目有效，但无需修改项目的开发和构建环境，更易上手

全局配置，是直接在 Maven 的配置文件 `conf/settings.xml`
中添加 Nop 仓库地址：

```xml
<settings>
  <!-- ... -->

  <profiles>
    <profile>
      <!-- ... -->

      <repositories>
        <repository>
          <id>nop-repo</id>
          <url>https://nop.repo.crazydan.io/</url>
          <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
          </snapshots>
        </repository>

        <!-- ... -->
      </repositories>
      <pluginRepositories>
        <!--
        Note: Nop Codegen 会被作为 Maven 插件使用，
              故而，需要在插件仓库中也配置上
        -->
        <pluginRepository>
          <id>nop-repo</id>
          <url>https://nop.repo.crazydan.io/</url>
          <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
          </releases>
          <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
          </snapshots>
        </pluginRepository>

        <!-- ... -->
      </pluginRepositories>
    </profile>
  </profiles>

  <!-- ... -->
</settings>
```

而项目配置，则是在 Maven 工程模块的 `pom.xml` 中添加仓库地址（一般可在父模块中添加）：

```xml
<project>
  <!-- ... -->

  <repositories>
    <repository>
      <id>nop-repo</id>
      <url>https://nop.repo.crazydan.io/</url>
    </repository>
  </repositories>
  <pluginRepositories>
    <pluginRepository>
      <id>nop-repo</id>
      <url>https://nop.repo.crazydan.io/</url>
    </pluginRepository>
  </pluginRepositories>

  <!-- ... -->
</project>
```

## Nop 组件依赖引入

首先，在 Maven 工程的父 `pom.xml` 中以 `parent` 方式引入 Nop 及其默认构建配置：

```xml
<project>
  <!-- ... -->

  <parent>
    <groupId>io.github.entropy-cloud</groupId>
    <artifactId>nop-entropy</artifactId>
    <version>2.0.0-SNAPSHOT</version>
  </parent>

  <!-- ... -->
</project>
```

接下来，在各个 Maven 子模块中仅按需依赖 Nop 的相关组件即可，无需指定组件版本号，如：

```xml
<project>
  <!-- ... -->

  <dependencies>
    <dependency>
      <groupId>io.github.entropy-cloud</groupId>
      <artifactId>nop-core</artifactId>
    </dependency>
    <dependency>
      <groupId>io.github.entropy-cloud</groupId>
      <artifactId>nop-orm</artifactId>
    </dependency>

    <!-- ... -->
  </dependencies>

  <!-- ... -->
</project>
```
