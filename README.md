Nop 组件包仓库（非官方）
===================================

![仓库构建状态](https://github.com/crazydan-studio/nop-repo/actions/workflows/deploy.yaml/badge.svg)

> 有关该仓库的使用说明，请祥见 [仓库站点](https://nop.repo.crazydan.io/)
> （[备用地址](https://crazydan-studio.github.io/nop-repo)）

本 Git 仓库包含 `master` 和 `dist` 分支，
前者为 Nop 构建源码分支，后者为 Nop 构建产物分支。

`dist` 分支将通过 Github Action 自动更新构建后的发布包，无需人工干预。

由于 `dist` 分支包含 jar 等二进制包，
故而，在克隆本 Git 仓库时仅需克隆 `master` 分支即可：

```bash
# https://www.freecodecamp.org/chinese/news/git-clone-branch-how-to-clone-a-specific-branch/
git clone \
    --single-branch \
    --branch master \
    git@github.com:crazydan-studio/nop-repo.git
```
