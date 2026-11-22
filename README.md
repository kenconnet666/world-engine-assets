# stride-ts-assets

[stride-ts](https://github.com/kenconnet666/stride-ts) 共用的二进制资源：字体、扫描的材质这类不适合放进主仓库 git 的东西。发成 GitHub Release 的
npm 包 `@stride-ts/assets`，主仓库的样例当依赖装上；开发服务器、编辑器打开工程时把包里的 `content/Shared` 同步到工程内容目录的
`Shared/` 下面（那个文件夹不进主仓库的 git），场景、材质照常按 `Shared/...` 的路径引用。

## 目录

- `sources/`：源文件（ttf、扫描贴图的 jpg）和 `sources/sources.json`（每一项导入到哪、来源和许可）。
- `content/Shared/`：引擎直接能用的内容（字体的字形块、KTX2 贴图、材质），由主仓库的 `node tools/assets.ts build` 按
  `sources.json` 用编辑器的导入器生成；这个仓库本身也是一个编辑器工程（`stride.project.json`），可以用编辑器打开看。
- `CREDITS.md`、`licenses/`：每一项的来源、作者和许可证全文。

## 加资源、发版

1. 源文件放进 `sources/`，在 `sources/sources.json` 里登记（字体：文件、放到哪、名字；材质：一组贴图、放到哪、名字），写上来源和许可；
   `CREDITS.md` 加一行。
2. 在主仓库里 `node tools/assets.ts build`：导入新加的、源文件变了的（已有的跳过）。
3. 提交推送这个仓库，再在主仓库里 `node tools/assets.ts dev`（发 `dev-<提交>` 的预发行版、主仓库的 override 指过去、`pnpm install`），
   或者 `node tools/assets.ts release <版本>`（先改这里 package.json 的版本）发正式版。
