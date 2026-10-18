---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: 2f4f9d0768d7574794591ee7258ece53_06304f1ec3dd11f1820a525400638852
    ReservedCode1: NEjHW9JCknvIOL+8/wqDTW8Uv3s9lpDZg0389Rth0LX/O4PXSrWwqX+xz0qvSNwFnGOdOQ3FujOQZE1gyNYOEz0M6ALNbSTe6Kg5qPe5uKmABKEic16ImUiJts9YqWVe7EX/CBI2JjGpjz6aW+He3FUEJP8tYypDZ4PVjVQ3cWbFNxIIey/VAMvAhqc=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: 2f4f9d0768d7574794591ee7258ece53_06304f1ec3dd11f1820a525400638852
    ReservedCode2: NEjHW9JCknvIOL+8/wqDTW8Uv3s9lpDZg0389Rth0LX/O4PXSrWwqX+xz0qvSNwFnGOdOQ3FujOQZE1gyNYOEz0M6ALNbSTe6Kg5qPe5uKmABKEic16ImUiJts9YqWVe7EX/CBI2JjGpjz6aW+He3FUEJP8tYypDZ4PVjVQ3cWbFNxIIey/VAMvAhqc=
---

# 丝路拾遗·大美西北 — H5 交付说明

## 一、文件结构
```
silksilk/
├── index.html    # 主页面（13 屏）
├── style.css     # 全局样式（设计令牌）
├── app.js        # 数据与交互逻辑
└── assets/       # 【待你放入素材】图片 / 音频
```

## 二、怎么预览
直接双击 `index.html` 用手机浏览器 / 微信打开即可；电脑浏览器可滚动或拖拽预览（已支持滚轮翻页）。

## 三、当前状态（2026-10-09 素材全量就位）
- 已实现 13 屏全部版式、滑动翻页、各省篇章、分类馆、线路、问答闯关、海报生成
- **图片 35 张已全部替换为真实素材**（封面 1 + 省图 5 + 非遗 14 + 地标 15），见 `assets/`，来源清单见 `assets/CREDITS.md`
- **书法字体已接入**：马善政毛笔楷书（Ma Shan Zheng，SIL OFL 开源可商用），已本地化至 `assets/fonts/` 并用于封面/标题/省名等
- **屏12 团队信息已填写**：团队名汇思小组，成员白惠茹（组长）、王嘉慧、马巧铃、石思瑀、解项瑜，指导教师敖慧，日期 2026年10月
- **屏13 二维码已生成**：`assets/qr.png`（占位内容，部署后重生成即可，见下文）
- 音频为 **WebAudio 合成占位音效**（老腔/花儿/口弦/木卡姆/鼓点），真实可发声；实拍音频无法由 AI 生成，保留占位

## 四、素材现状清单

| 类型 | 数量 | 状态 | 位置 |
|---|---|---|---|
| 封面背景图 | 1 | ✅ 已替换 | `assets/cover.jpg` |
| 各省印象大图 | 5 | ✅ 已替换 | `assets/prov-*.jpg` |
| 非遗项目实物图 | 14 | ✅ 已替换 | `assets/item-*.jpg` |
| 文旅地标图 | 13 | ✅ 已替换 | `assets/land-*.jpg` |
| 音频 | 4–5 段 | ⏳ WebAudio 合成占位（可发声） | `app.js` 中 `SOUNDS`；如需实拍，替换后填 `window.ASSETS.audio` |
| 书法字体 | 1 | ✅ 已接入 | `assets/fonts/ma-shan-zheng.css`（马善政毛笔楷书） |
| 手绘西北示意图 | 1 | ⏳ 可选（未替换，使用内置环形入口） | `assets/map.svg` |
| 二维码 | 1 | ✅ 已生成占位 | `assets/qr.png` |

## 五、二维码正式化方法
当前 `assets/qr.png` 内容为「丝路拾遗·大美西北 数字编辑大赛参赛作品 汇思小组」。部署拿到 H5 正式链接后，一条命令重生成：
```
python -c "import qrcode; q= qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_M, box_size=10, border=4); q.add_data('你的H5正式链接'); q.make(fit=True); q.make_image(fill_color='#1A1B1C', back_color='white').save('assets/qr.png')"
```
（需 `pip install qrcode[pil]`）

## 六、比赛交稿前提醒
1. 屏12 团队信息已填写 ✅（如日期需按交稿时间修改，改 `index.html` 中 `.guard-team`）
2. 屏13 二维码：提供 H5 正式链接后重生成（见上）
3. 数据来源已在页面标注：文化和旅游部（2022），含新疆生产建设兵团
4. 图片来源见 `assets/CREDITS.md`，其中「待复核」项交稿前建议按关键词复核源站授权
5. 地图为手绘/环形示意，未使用标准行政区划图

## 六、技术达标
- 首屏轻量：封面背景占位为 CSS 渐变，无大图阻塞
- 音频按需加载，点击播放/暂停，不自动播放
- 背景音乐：`assets/audio/bgm-desertcity.mp3`（Kevin MacLeod - Desert City，CC-BY 4.0，可商用，需署名 "Kevin MacLeod (incompetech.com), CC-BY 4.0"；页面页脚已展示署名）
- 沙丘粒子 ≤ 200，动效使用 transform / opacity，低端机流畅
- 支持 iOS / Android / 微信内置浏览器
*（内容由AI生成，仅供参考）*
