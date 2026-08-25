北韵晋创 · 文化积木智造 AR Demo
====================================
作者：花花的 7 天冲刺工程 · 2026-08-24
说明：这是一个「扫图出 AR」的最小可用 demo，用来给 iCAN 智慧文创赛道做演示。

┌─────────────────────────────────────────────┐
│  项目结构                                    │
├─────────────────────────────────────────────┤
│  index.html      ← 主页面（AR 场景 + 界面）   │
│  assets/                                     │
│    ├─ card.mind  ← 追踪文件（识别用的"特征码"）│
│    └─ card.png   ← 示例追踪图（官方卡片）      │
└─────────────────────────────────────────────┘

【第一步 · 立即体验（今天就能看效果）】
1. 把这个文件夹部署到任意 HTTPS 静态站点：
   - Netlify Drop：https://app.netlify.com/drop 拖文件夹进去
   - 或 GitHub Pages / Cloudflare Pages
2. 电脑上打开 assets/card.png 全屏显示（或打印出来）
3. 手机打开部署后的链接 → 允许摄像头 → 对准电脑屏幕上的卡片图
4. 会看到一个旋转的"积木小塔"浮在卡片上方 —— 这就是 AR

【第二步 · 换成你的积木图（10 分钟）】
1. 拍一张你积木产品的正面高清照（对比度要强，图案清晰）
2. 打开 MindAR 官方编译器：
   https://hiukim.github.io/mind-ar-js-doc/tools/compile
3. 上传照片 → 下载生成的文件（比如 targets.mind）
4. 替换 assets/ 下的 card.mind
5. 改 index.html 里第 60 行：imageTargetSrc: ./assets/targets.mind

【第三步 · 换成 3D 古建模型（30 分钟）】
1. 去 Sketchfab（sketchfab.com）或 CG模型网搜"古塔 / 古建筑 / pagoda / ancient chinese architecture"
2. 下载 .glb 格式（找不到 glb 就下 gltf）
3. 放进 assets/ 文件夹
4. 打开 index.html，把"示例积木塔"那一段（a-entity mindar-image-target 内）
   替换成：
   <a-assets>
     <a-asset-item id="model" src="./assets/你的模型.glb"></a-asset-item>
   </a-assets>
   ...
   <a-entity gltf-model="#model" scale="1 1 1" position="0 -0.3 0"></a-entity>
   （具体写法 index.html 里已有注释）

【疑难排查】
- 手机打不开 / 摄像头黑屏 → 必须是 HTTPS 或 localhost，本地双击 HTML 不行
- 识别不到图 → 图片特征太少（纯色块不行），换图案更丰富的角度重拍
- 模型不显示 → 看浏览器控制台报错，确认 .glb 路径大小写正确
- 本地调试（电脑上跑）→ 在该文件夹执行：python -m http.server 8000
  然后浏览器打开 http://localhost:8000
