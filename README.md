# 商品评价文案生成器

把商品信息**整段贴进来**（标题、卖点、关键词、一句需求都行），自动识别品类与卖点，生成像真人买家随手写的中文商品评价。

纯静态单文件网页，无框架、无构建、无依赖，可直接部署到 GitHub Pages。

## 怎么用

1. 把商品信息贴进输入框，格式不用讲究。下面这些都行：
   - `肉包子 皮薄馅大 冷冻装 早上蒸十分钟就能吃`
   - `纯棉短袖T恤男夏季新款宽松透气圆领打底衫`（整句标题）
   - `给生鲜水果写评价，重点夸新鲜和发货快`（一句需求）
2. 选字数、语气，点生成。

系统会自动判断商品品类（食品 / 服饰 / 数码 / 家电 / 美妆 / 家纺 / 家居 / 母婴 / 宠物粮 / 宠物零食 / 通用），并按品类匹配对应的评价语料——食品只说味道口感，服饰只说面料版型，不会出现"包子走线整齐"这种串味评价。结果区会显示识别到的品类。

每次固定生成 **4 条**，可单条复制、复制全部、导出 txt。点「换一批」重新生成，不会重复上一批。

## 三种生成通道

| 模式 | 说明 | 需要配置 |
| --- | --- | --- |
| **本地引擎**（默认） | 自动识别品类、拆解卖点，按品类语料组合成评价，离线可用，不消耗 token | 无需任何配置 |
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

两种部署方式任选其一：

- **分支模式**：Settings → Pages → Source 选 `Deploy from a branch` → 分支 `main`、目录 `/(root)` → Save
- **Actions 模式**：Settings → Pages → Source 保持 `GitHub Actions`，仓库里已带 `.github/workflows/static.yml`，推送后自动构建

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
├── index.html                  # 界面 + 本地评价引擎（单文件，无依赖）
├── server.js                   # 本地预览服务器（部署时可忽略）
├── .nojekyll                   # 关闭 GitHub Pages 的 Jekyll 处理
├── .github/workflows/static.yml # Pages 用 Actions 部署时的构建流程
├── LICENSE                     # MIT
└── README.md
```

## License

MIT
