Nop 构建产物仓库使用说明
====================================

本仓库通过 Github Action 自动定时（每日凌晨 2 点）构建 Nop 官方源码，
当前构建的源码版本为：[%latest_commit%](https://gitee.com/canonical-entropy/nop-entropy/tree/%latest_commit%)。

## 免责声明

本仓库为个人构建的 Nop 专用仓库，而非官方的发布仓库，目的是方便有需要的朋友快速开始尝鲜或进行项目开发。

因此，因使用本仓库所产生的任何风险和损失均需由您自行承担，本人将不承担因您的行为所造成的任何后果，
若您继续使用本仓库，则默认视为您已明确知晓相关风险，并承诺后果自负。

建议您在商业产品中慎重使用本仓库，优先选择自行构建官方[源代码](https://gitee.com/canonical-entropy/nop-entropy)，
或等待官方仓库的发布。

若您有关于 Nop 开发相关的问题，请移步至
[Nop Issues](https://gitee.com/canonical-entropy/nop-entropy/issues) 页面提问。

## Nop IDEA 插件安装

点击下载 [nop-idea-plugin-1.0-SNAPSHOT.zip](./nop-idea-plugin-1.0-SNAPSHOT.zip)，
完成后，进入 IDEA 的插件管理（`File -> Settings -> Plugins`），
点击齿轮图标，并选择 `Install Plugin from Disk ...`，再选中已下载的插件
`nop-idea-plugin-1.0-SNAPSHOT.zip` 以将其安装到 IDEA 中。

安装后需要清空 IDEA 缓存并重启：`File -> Invalidate Caches...`。

在启动调试时，需要选择 `XLangDebug` （注意，其仅对 `#main` 函数有效）：

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

## Maven 配置

在 Maven 的配置文件 `conf/settings.xml` 中添加 Nop 仓库地址：

```xml
    <repositories>
      <repository>
        <id>nop-repo</id>
        <url>https://nop.repo.crazydan.io</url>
        <releases>
          <enabled>true</enabled>
          <updatePolicy>always</updatePolicy>
          <checksumPolicy>ignore</checksumPolicy>
        </releases>
        <snapshots>
          <enabled>true</enabled>
          <updatePolicy>always</updatePolicy>
          <checksumPolicy>ignore</checksumPolicy>
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
        <url>https://nop.repo.crazydan.io</url>
        <releases>
          <enabled>true</enabled>
          <updatePolicy>always</updatePolicy>
          <checksumPolicy>ignore</checksumPolicy>
        </releases>
        <snapshots>
          <enabled>true</enabled>
          <updatePolicy>always</updatePolicy>
          <checksumPolicy>ignore</checksumPolicy>
        </snapshots>
      </pluginRepository>

      <!-- ... -->
    </pluginRepositories>
```
