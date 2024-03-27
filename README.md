Nop 发布包仓库（非官方）
===================================

![仓库构建状态](https://github.com/flytreeleft/nop-artifact-repo/actions/workflows/publish.yaml/badge.svg)

> 有关该发布包仓库的使用说明，请祥见 https://nop.repo.crazydan.io/

本 Git 仓库包含 `master` 和 `dist` 分支，
前者为 Nop 构建的配置分支，后者为 Nop 构建产物分支。

`dist` 分支将通过 Github Action 自动更新构建后的发布包，无需人工干预。

由于 `dist` 分支包含 jar 等二进制包，
故而，在克隆本 Git 仓库时仅需克隆 `master` 分支即可：

```bash
git clone --branch master git@github.com:flytreeleft/nop-artifact-repo.git
```
