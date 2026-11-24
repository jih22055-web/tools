# 万能工具箱

在线地址：**https://toolpocket.cn**

一个纯静态的中文在线工具集合，86 个工具，全部在浏览器本地运行——不上传文件、不需要注册、没有广告、没有埋点统计。

## 为什么做这个

日常处理图片、格式化 JSON、生成二维码、算还款、转简繁，这些小事没必要为每一个都装个软件，也不该为了压缩一张图先注册账号、再看三段广告。所以把常用的小工具收在一个页面里，打开就能用。

## 有哪些工具

按 8 个分类组织，共 86 个：

| 分类 | 数量 | 代表工具 |
|---|---|---|
| 开发工具 | 24 | JSON 格式化、SQL 格式化、正则测试、Cron 表达式、CURL 转代码、银行卡号校验 |
| 查询计算 | 15 | 单位换算、汇率、房贷计算、个税、年龄计算、五国地址生成 |
| 图片工具 | 13 | 图片压缩、尺寸调整、格式转换、取色、二维码生成与识别 |
| 文本处理 | 13 | 字数统计、大小写转换、去重排序、简繁转换、拼音标注、摩斯电码 |
| 生活工具 | 9 | 亲戚称谓、鞋码对照、今天吃什么、色盲测试、随机数 |
| 编码解码 | 7 | Base64、URL 编解码、Unicode、Hex、JWT 解析、哈希计算 |
| 网络工具 | 3 | IP 查询、User-Agent 解析、临时邮箱 |
| 表格转换 | 2 | Excel 转 JSON、表格转 Markdown |

## 技术构成

- **原生 HTML + CSS + JavaScript**，零框架、零构建、零后端，改完直接上传就是线上版本
- 托管在 GitHub Pages，HTTPS 由平台自动签发
- 第三方能力全部本地化，不依赖公共 CDN：`crypto-js`（哈希）、`xlsx`（表格）、`qrcode`（二维码）、`jsQR`（识别）、`pinyin-pro`（拼音）、`opencc`（简繁）、`js-yaml`、`jsbarcode`、`turndown`
- 全站 85 个页面均带 `canonical`、JSON-LD 结构化数据（WebApplication + FAQPage）、独立 description，并生成 `sitemap.xml`

**唯一需要联网的工具是临时邮箱**，它连接 Guerrilla Mail 的公共接口收发邮件。其余 83 个工具的数据不出浏览器。

## 本地运行

```bash
git clone https://github.com/jih22055-web/tools.git
cd tools
python -m http.server 8000
```

然后打开 `http://localhost:8000`。也可以直接双击 `index.html`，绝大多数工具照常工作。

## 目录结构

```
index.html      首页，同时是全站唯一的工具清单（TOOLS 数组）
*.html          每个工具一个独立页面
style.css       全站样式
sitemap.xml     85 条 URL
robots.txt      放行全部爬虫
CNAME          GitHub Pages 自定义域名
*.js            9 个本地化的第三方库
```

## 新增一个工具

1. 复制任一工具页（如 `barcode.html`），改造成新工具
2. 在 `index.html` 的 `TOOLS` 数组里加一行：

```js
{name:'工具名',desc:'一句话说明',icon:'🔧',color:'#ef5b41',file:'tool.html',tag:'',cat:'开发工具'},
```

首页的分类筛选和搜索会自动跟着更新，分类是按 `cat` 字段去重的，不需要另外维护。

## 说明

- 不收集任何用户数据，没有登录、没有 Cookie 追踪
- 工具页里的文件处理全部在浏览器内存中完成，关闭页面即释放
- 临时邮箱的地址是公开的，请勿用于接收敏感信息（页面内有明确提示）

有想法或发现 bug，欢迎提 issue。
