# 商品评价文案生成器

输入**商品标题**和**商品关键词**，生成像真人买家随手写的中文商品评价。

纯静态单文件网页，无框架、无构建、无依赖，可直接部署到 GitHub Pages。

## 怎么用

1. 填商品标题（必填）；
2. 填几个关键词，逗号分隔（选填，不填就围绕做工、质量、包装、物流、性价比写）；
3. 选长度、语气、条数，点生成。

每次固定生成 **4 条**，可单条复制、复制全部、导出 txt。点「换一批」重新生成，不会重复上一批。

## 三种生成通道

| 模式 | 说明 | 需要配置 |
| --- | --- | --- |
| **本地引擎**（默认） | 把关键词拆进评价句式模板重新组合，长短混排、带小瑕疵，离线可用，不消耗 token | 无需任何配置 |
| **DeepSeek** | 直接调用 DeepSeek 官方 Chat API（默认 `deepseek-chat`） | 需要 API Key |
| **硅基流动** | 直接调用 SiliconFlow Chat API（默认 `Qwen/Qwen2.5-7B-Instruct`） | 需要 API Key |

云模式由浏览器直接请求官方接口（两家均支持跨域），不经过任何中间服务器，所以纯静态托管即可用，不需要自建后端。

## 参数

- **字数**：30 字 / 45 字 / 50 字三档，本地引擎按档位控制篇幅，成稿落在对应区间内
- **语气**：真实朴素、热情推荐、走心细致、简洁冷淡
- **数量**：每次 4 条

## 部署到 GitHub Pages

```bash
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

仓库 **Settings → Pages** → Source 选 `Deploy from a branch` → 分支 `main`、目录 `/(root)` → Save。
约 1 分钟后访问 `https://<用户名>.github.io/<仓库名>/`。

> `.nojekyll` 用于关闭 Jekyll 处理，请勿删除。

没有 git 环境也可以在仓库页面 **Add file → Upload files** 直接拖拽上传。

## 本地预览

```bash
node server.js      # → http://localhost:3000
```

`server.js` 只是本地预览用的静态服务器，部署到 GitHub Pages 时用不到。也可以直接双击 `index.html` 打开。

## API Key

- DeepSeek → https://platform.deepseek.com
- 硅基流动 → https://cloud.siliconflow.cn

Key 只写入本机浏览器的 `localStorage`，页面不会把它发往除官方接口以外的任何地址（源码可核查）。公共电脑上用完请清空。

## 项目结构

```
.
├── index.html    # 界面 + 本地评价引擎（单文件，无依赖）
├── server.js     # 本地预览服务器（部署时可忽略）
├── .nojekyll     # 关闭 GitHub Pages 的 Jekyll 处理
├── LICENSE       # MIT
└── README.md
```

## License

MIT
