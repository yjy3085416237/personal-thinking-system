# personal-thinking-system
to  record my thingking
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>个人思考系统｜长期版</title>
  <style>
    :root {
      --bg: #f5f7fb;
      --panel: #ffffff;
      --panel-2: #f9fbff;
      --line: #dde5f0;
      --text: #172033;
      --muted: #61708a;
      --primary: #425df3;
      --primary-soft: #e8edff;
      --accent: #16a34a;
      --warning: #f59e0b;
      --danger: #ef4444;
      --shadow: 0 10px 30px rgba(28, 42, 73, 0.08);
      --radius: 18px;
      --radius-sm: 12px;
      --sidebar-width: 260px;
      --max: 1540px;
    }

    * { box-sizing: border-box; }
    html, body { margin: 0; padding: 0; background: var(--bg); color: var(--text); font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif; }
    body { min-height: 100vh; }
    button, input, textarea, select { font: inherit; }
    a { color: var(--primary); }

    .app {
      max-width: var(--max);
      margin: 0 auto;
      display: grid;
      grid-template-columns: var(--sidebar-width) 1fr;
      gap: 18px;
      padding: 18px;
    }

    .sidebar {
      background: linear-gradient(180deg, #1f2b5f, #172033 78%);
      color: #f6f8ff;
      border-radius: 26px;
      padding: 22px 18px 18px;
      box-shadow: var(--shadow);
      position: sticky;
      top: 18px;
      align-self: start;
      max-height: calc(100vh - 36px);
      overflow: auto;
    }

    .brand {
      padding-bottom: 18px;
      border-bottom: 1px solid rgba(255,255,255,0.1);
      margin-bottom: 16px;
    }
    .brand h1 {
      margin: 0;
      font-size: 22px;
      line-height: 1.25;
    }
    .brand p {
      margin: 10px 0 0;
      color: rgba(255,255,255,0.78);
      font-size: 13px;
      line-height: 1.6;
    }

    .nav-group { margin-bottom: 18px; }
    .nav-label {
      font-size: 12px;
      color: rgba(255,255,255,0.54);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      margin: 10px 10px 8px;
    }

    .nav-list {
      display: grid;
      gap: 8px;
    }

    .nav-btn {
      width: 100%;
      text-align: left;
      background: transparent;
      border: 1px solid rgba(255,255,255,0.08);
      color: #edf1ff;
      padding: 12px 14px;
      border-radius: 14px;
      cursor: pointer;
      transition: 0.2s ease;
    }
    .nav-btn:hover, .nav-btn.active {
      background: rgba(255,255,255,0.1);
      border-color: rgba(255,255,255,0.16);
      transform: translateX(2px);
    }

    .side-tip {
      margin-top: 14px;
      padding: 14px;
      background: rgba(255,255,255,0.08);
      border-radius: 16px;
      font-size: 13px;
      color: rgba(255,255,255,0.82);
      line-height: 1.7;
    }

    .mobile-topbar,
    .mobile-nav { display: none; }

    .main {
      display: grid;
      gap: 16px;
      min-width: 0;
    }

    .toolbar {
      background: var(--panel);
      border-radius: 24px;
      padding: 16px 18px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 12px;
      justify-content: space-between;
      box-shadow: var(--shadow);
    }

    .toolbar-title h2 {
      margin: 0;
      font-size: 24px;
    }
    .toolbar-title p {
      margin: 6px 0 0;
      color: var(--muted);
      font-size: 14px;
    }

    .toolbar-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      align-items: center;
    }

    .btn {
      border: 1px solid var(--line);
      background: var(--panel);
      padding: 10px 14px;
      border-radius: 12px;
      cursor: pointer;
      color: var(--text);
      transition: 0.2s ease;
      box-shadow: 0 2px 6px rgba(27, 41, 74, 0.04);
    }
    .btn:hover { transform: translateY(-1px); }
    .btn.primary { background: var(--primary); color: #fff; border-color: var(--primary); }
    .btn.soft { background: var(--primary-soft); color: var(--primary); border-color: transparent; }
    .btn.success { background: #e8fff0; color: #0f8e3a; border-color: transparent; }
    .btn.warn { background: #fff6df; color: #9b6200; border-color: transparent; }
    .btn.danger { background: #ffe9e9; color: #bf1f1f; border-color: transparent; }

    .section {
      display: none;
      gap: 16px;
    }
    .section.active {
      display: grid;
    }

    .panel {
      background: var(--panel);
      border-radius: 24px;
      padding: 18px;
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .panel-header {
      display: flex;
      gap: 12px;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 16px;
      flex-wrap: wrap;
    }
    .panel-header h3 {
      margin: 0;
      font-size: 20px;
    }
    .panel-header p {
      margin: 8px 0 0;
      color: var(--muted);
      line-height: 1.65;
      font-size: 14px;
      max-width: 720px;
    }

    .grid-2, .grid-3, .grid-4 {
      display: grid;
      gap: 14px;
    }
    .grid-2 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
    .grid-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    .grid-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }

    .stat-card {
      background: linear-gradient(180deg, #ffffff, #f8fbff);
      border: 1px solid var(--line);
      border-radius: 18px;
      padding: 16px;
      min-height: 120px;
    }
    .stat-card .eyebrow {
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 12px;
    }
    .stat-card .value {
      font-size: 34px;
      font-weight: 700;
      margin-bottom: 8px;
      line-height: 1;
    }
    .stat-card .sub {
      color: var(--muted);
      font-size: 13px;
      line-height: 1.6;
    }

    .mini-card, .field-card, .template-card, .week-card, .dictionary-card, .entry-card, .view-card {
      background: var(--panel-2);
      border: 1px solid var(--line);
      border-radius: 18px;
      padding: 16px;
    }

    .field-card h4,
    .template-card h4,
    .week-card h4,
    .entry-card h4,
    .dictionary-card h4,
    .view-card h4,
    .mini-card h4 {
      margin: 0 0 10px;
      font-size: 16px;
    }

    .field-card p,
    .template-card p,
    .entry-card p,
    .week-card p,
    .dictionary-card p,
    .view-card p,
    .mini-card p {
      color: var(--muted);
      font-size: 13px;
      line-height: 1.7;
      margin-top: 0;
    }

    .field-grid {
      display: grid;
      gap: 12px;
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    label {
      display: block;
      font-size: 13px;
      color: var(--muted);
      margin-bottom: 6px;
    }

    input[type="text"], input[type="date"], input[type="month"], input[type="url"], input[type="number"], select, textarea {
      width: 100%;
      border: 1px solid var(--line);
      background: #fff;
      border-radius: 12px;
      padding: 10px 12px;
      color: var(--text);
      resize: vertical;
      min-height: 44px;
    }
    textarea { min-height: 96px; line-height: 1.7; }

    .textarea-sm { min-height: 72px; }
    .textarea-lg { min-height: 160px; }

    .row {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      align-items: center;
    }

    .helper {
      color: var(--muted);
      font-size: 12px;
      line-height: 1.6;
      margin-top: 6px;
    }

    .chips {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }
    .chip {
      padding: 6px 10px;
      border-radius: 999px;
      background: var(--primary-soft);
      color: var(--primary);
      font-size: 12px;
      border: 1px solid transparent;
    }

    .progress-bar {
      height: 10px;
      background: #e8edf7;
      border-radius: 999px;
      overflow: hidden;
      margin-top: 10px;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--primary), #7c90ff);
      width: 0;
      transition: width 0.2s ease;
    }

    .calendar {
      border: 1px solid var(--line);
      background: #fff;
      border-radius: 20px;
      padding: 14px;
    }
    .calendar-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
      gap: 8px;
    }
    .calendar-grid {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 8px;
    }
    .calendar-weekday {
      text-align: center;
      color: var(--muted);
      font-size: 12px;
      padding: 6px 0;
    }
    .day {
      min-height: 88px;
      background: var(--panel-2);
      border: 1px solid var(--line);
      border-radius: 14px;
      padding: 8px;
      display: flex;
      flex-direction: column;
      gap: 6px;
    }
    .day.empty {
      background: transparent;
      border-style: dashed;
      opacity: 0.45;
    }
    .day.today {
      border-color: var(--primary);
      box-shadow: inset 0 0 0 1px var(--primary);
    }
    .day-number {
      font-size: 13px;
      font-weight: 600;
    }
    .day-markers {
      display: flex;
      gap: 4px;
      flex-wrap: wrap;
    }
    .marker {
      width: 8px;
      height: 8px;
      border-radius: 999px;
    }
    .marker.input { background: var(--primary); }
    .marker.output { background: var(--accent); }
    .marker.week { background: var(--warning); }
    .day-note {
      font-size: 11px;
      color: var(--muted);
      line-height: 1.4;
      overflow: hidden;
    }

    .accordion {
      display: grid;
      gap: 12px;
    }
    .accordion-item {
      border: 1px solid var(--line);
      border-radius: 18px;
      background: #fff;
      overflow: hidden;
    }
    .accordion-btn {
      width: 100%;
      border: 0;
      background: transparent;
      padding: 16px;
      text-align: left;
      display: flex;
      justify-content: space-between;
      gap: 12px;
      align-items: center;
      cursor: pointer;
    }
    .accordion-btn strong { font-size: 16px; }
    .accordion-body {
      display: none;
      padding: 0 16px 16px;
      border-top: 1px solid var(--line);
      background: #fcfdff;
    }
    .accordion-item.open .accordion-body { display: block; }

    .list {
      display: grid;
      gap: 12px;
    }

    .card-actions {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      margin-top: 12px;
    }

    .tag-row {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      margin-bottom: 10px;
    }
    .tag {
      font-size: 12px;
      color: var(--muted);
      padding: 4px 10px;
      border-radius: 999px;
      background: #fff;
      border: 1px solid var(--line);
    }

    .template-preview {
      background: #111827;
      color: #e5efff;
      border-radius: 16px;
      padding: 14px;
      font-size: 13px;
      line-height: 1.8;
      white-space: pre-wrap;
      word-break: break-word;
    }

    .timeline {
      display: grid;
      gap: 12px;
    }
    .timeline-item {
      display: grid;
      grid-template-columns: 120px 1fr;
      gap: 12px;
      align-items: start;
    }
    .timeline-time {
      font-size: 13px;
      color: var(--muted);
      padding-top: 6px;
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: #eef3ff;
      color: var(--primary);
      padding: 6px 10px;
      border-radius: 999px;
      font-size: 12px;
      font-weight: 600;
    }

    .empty-state {
      padding: 20px;
      text-align: center;
      color: var(--muted);
      border: 1px dashed var(--line);
      border-radius: 16px;
      background: #fff;
    }

    .split-layout {
      display: grid;
      grid-template-columns: 1.2fr 0.8fr;
      gap: 16px;
    }

    .sticky-subnav {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .small {
      font-size: 12px;
      color: var(--muted);
    }

    .checklist {
      display: grid;
      gap: 10px;
    }
    .check-item {
      display: flex;
      gap: 10px;
      align-items: flex-start;
      padding: 10px 12px;
      border-radius: 12px;
      border: 1px solid var(--line);
      background: #fff;
    }
    .check-item input { margin-top: 2px; }

    .footer-note {
      text-align: center;
      color: var(--muted);
      font-size: 12px;
      padding: 6px 0 80px;
    }

    @media (max-width: 1180px) {
      .grid-4 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
      .split-layout, .grid-3 { grid-template-columns: 1fr; }
    }

    @media (max-width: 920px) {
      .app {
        grid-template-columns: 1fr;
        padding: 12px 12px 84px;
      }
      .sidebar { display: none; }
      .mobile-topbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 12px;
        background: var(--panel);
        border-radius: 20px;
        padding: 14px 16px;
        box-shadow: var(--shadow);
        position: sticky;
        top: 12px;
        z-index: 20;
      }
      .mobile-topbar h1 {
        margin: 0;
        font-size: 18px;
      }
      .mobile-topbar p {
        margin: 4px 0 0;
        color: var(--muted);
        font-size: 12px;
      }
      .toolbar { border-radius: 20px; }
      .grid-2, .grid-4, .field-grid { grid-template-columns: 1fr; }
      .mobile-nav {
        display: flex;
        position: fixed;
        left: 12px;
        right: 12px;
        bottom: 12px;
        z-index: 30;
        background: rgba(255,255,255,0.96);
        border: 1px solid var(--line);
        border-radius: 18px;
        box-shadow: var(--shadow);
        padding: 8px;
        gap: 8px;
        overflow: auto;
        backdrop-filter: blur(12px);
      }
      .mobile-nav button {
        white-space: nowrap;
        border: 0;
        background: transparent;
        padding: 10px 12px;
        border-radius: 12px;
        color: var(--muted);
      }
      .mobile-nav button.active {
        background: var(--primary-soft);
        color: var(--primary);
        font-weight: 600;
      }
      .timeline-item { grid-template-columns: 1fr; }
      .calendar-grid { gap: 6px; }
      .day { min-height: 74px; }
    }
  </style>
</head>
<body>
  <div class="app">
    <aside class="sidebar">
      <div class="brand">
        <h1>个人思考系统</h1>
        <p>服务未来 3–5 年的可持续认知、表达与生存体系。不是一次性填写，而是长期生长。</p>
      </div>

      <div class="nav-group">
        <div class="nav-label">总览</div>
        <div class="nav-list">
          <button class="nav-btn active" data-target="dashboard">仪表盘</button>
          <button class="nav-btn" data-target="vision">长期总纲</button>
          <button class="nav-btn" data-target="views">9观系统</button>
        </div>
      </div>

      <div class="nav-group">
        <div class="nav-label">生产系统</div>
        <div class="nav-list">
          <button class="nav-btn" data-target="inputs">阅读输入</button>
          <button class="nav-btn" data-target="outputs">输出系统</button>
          <button class="nav-btn" data-target="weeks">周系统</button>
          <button class="nav-btn" data-target="dictionary">概念词典</button>
        </div>
      </div>

      <div class="nav-group">
        <div class="nav-label">校准与资产</div>
        <div class="nav-list">
          <button class="nav-btn" data-target="antiBubble">反茧房</button>
          <button class="nav-btn" data-target="assets">双资产库</button>
          <button class="nav-btn" data-target="templates">模板中心</button>
        </div>
      </div>

      <div class="side-tip">
        使用建议：<br>
        1. 先填“总目标、3条母题、价值观、自我观、学习观”。<br>
        2. 每天只整理 1–3 篇输入，至少写 1 条判断。<br>
        3. 第二周之后继续新增周卡即可，系统会一直保留历史。
      </div>
    </aside>

    <div class="mobile-topbar">
      <div>
        <h1>个人思考系统</h1>
        <p>长期版 · 可持续写作与思考</p>
      </div>
      <button class="btn soft" id="mobileMenuHint">分块导航</button>
    </div>

    <main class="main">
      <div class="toolbar">
        <div class="toolbar-title">
          <h2 id="pageTitle">仪表盘</h2>
          <p id="pageDesc">先看整体状态，再决定今天写什么。</p>
        </div>
        <div class="toolbar-actions">
          <button class="btn soft" id="saveBtn">立即保存</button>
          <button class="btn" id="exportBtn">导出 JSON</button>
          <label class="btn" for="importFile">导入备份</label>
          <input type="file" id="importFile" accept="application/json" hidden />
          <button class="btn" onclick="window.print()">打印 / 导出 PDF</button>
        </div>
      </div>

      <section class="section active" id="dashboard">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>你的系统状态</h3>
              <p>这里不是“好看”的展示页，而是你的工作台。下面的数字会随着你持续填写自动变化。</p>
            </div>
            <div class="status-pill" id="saveStatus">已准备开始</div>
          </div>
          <div class="grid-4">
            <div class="stat-card">
              <div class="eyebrow">输入条目</div>
              <div class="value" id="statInputs">0</div>
              <div class="sub">已整理进入系统的文章 / 书摘 / 访谈 / 观察材料</div>
            </div>
            <div class="stat-card">
              <div class="eyebrow">输出条目</div>
              <div class="value" id="statOutputs">0</div>
              <div class="sub">你的判断、短文、片段、问题推进记录</div>
            </div>
            <div class="stat-card">
              <div class="eyebrow">已开启周数</div>
              <div class="value" id="statWeeks">1</div>
              <div class="sub">第二周、第三周以后都可以持续新增，不会覆盖前面的内容</div>
            </div>
            <div class="stat-card">
              <div class="eyebrow">系统完成度</div>
              <div class="value" id="statCompletion">0%</div>
              <div class="sub">根据核心字段的填写情况自动估算，先追求持续，不追求一次写满</div>
              <div class="progress-bar"><div class="progress-fill" id="completionBar"></div></div>
            </div>
          </div>
        </div>

        <div class="split-layout">
          <div class="panel">
            <div class="panel-header">
              <div>
                <h3>本月思考日历</h3>
                <p>蓝点表示输入，绿点表示输出，橙点表示周节点。你可以直观看到自己有没有持续写。</p>
              </div>
            </div>
            <div class="calendar">
              <div class="calendar-header">
                <div class="row">
                  <button class="btn" id="prevMonth">上个月</button>
                  <button class="btn" id="nextMonth">下个月</button>
                </div>
                <strong id="calendarTitle"></strong>
              </div>
              <div class="calendar-grid" id="calendarWeekdays"></div>
              <div class="calendar-grid" id="calendarDays"></div>
            </div>
          </div>

          <div class="panel">
            <div class="panel-header">
              <div>
                <h3>本周聚焦</h3>
                <p>把今天要做的事情缩到最小，系统才会真的跑起来。</p>
              </div>
            </div>
            <div class="list" id="dashboardFocus"></div>
          </div>
        </div>

        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>执行提醒</h3>
              <p>你不是要做一个“漂亮系统”，而是要做一个能陪你 3–5 年持续写下去的系统。</p>
            </div>
          </div>
          <div class="grid-3">
            <div class="mini-card">
              <h4>今天最小动作</h4>
              <p>1 篇输入卡片 + 1 条 100–300 字判断。只要完成这两个动作，系统就在生长。</p>
            </div>
            <div class="mini-card">
              <h4>每周动作</h4>
              <p>整理 3 个最重要的问题、3 个新的判断、1 个被修正的观点。周系统支持一直新增，不会只停在第一周。</p>
            </div>
            <div class="mini-card">
              <h4>避免假充实</h4>
              <p>不是看得越多越好，而是留下来的内容能否帮助你形成自己的判断、语言和方向。</p>
            </div>
          </div>
        </div>
      </section>

      <section class="section" id="vision">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>未来 3–5 年长期总纲</h3>
              <p>这里是你的总方向。先写粗糙版，不要等“想清楚以后”再写。系统的意义就是帮助你慢慢想清楚。</p>
            </div>
          </div>
          <div class="grid-2">
            <div class="field-card">
              <h4>我想成为什么样的人</h4>
              <p>不是写岗位头衔，而是写人格、能力、生活状态、表达方式。</p>
              <textarea id="goalWho" class="textarea-lg" placeholder="例如：我希望成为一个有主体性、有判断力、能持续表达、能在 AI 时代维持独立与柔韧的人。"></textarea>
            </div>
            <div class="field-card">
              <h4>我最不想活成什么样</h4>
              <p>写清楚“反面画像”，它会帮你避免很多看似正确的路径。</p>
              <textarea id="goalAvoid" class="textarea-lg" placeholder="例如：只会接收、不敢表达；被平台和外界评价牵着走；读很多却没有自己的系统。"></textarea>
            </div>
          </div>
        </div>

        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>3 条长期母题</h3>
              <p>不要什么都想写。先固定 3 条你愿意持续追问 100 天以上的主线。</p>
            </div>
          </div>
          <div class="grid-3" id="themeCards"></div>
        </div>

        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>阶段目标与年度提醒</h3>
              <p>把长期目标拆成今年要推进的事情，避免只停留在宏大愿景。</p>
            </div>
          </div>
          <div class="grid-3">
            <div class="field-card">
              <h4>未来一年要完成什么</h4>
              <textarea id="goalYear" placeholder="例如：形成自己的长期问题库；完成 100 条判断；建立可持续周系统；明确 AI 时代个人主体性的第一版立场。"></textarea>
            </div>
            <div class="field-card">
              <h4>未来三年要稳住什么</h4>
              <textarea id="goalThreeYears" placeholder="例如：稳定输出习惯、个人概念词典、核心表达风格、可迁移的职业资产。"></textarea>
            </div>
            <div class="field-card">
              <h4>未来五年想形成什么骨架</h4>
              <textarea id="goalFiveYears" placeholder="例如：一套成熟的价值观、自我观、学习观；几个长期主题上的稳定判断；有现实支撑的独立生存体系。"></textarea>
            </div>
          </div>
        </div>
      </section>

      <section class="section" id="views">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>9观系统</h3>
              <p>原来的 6 观升级为更适合未来 3–5 年的 9 观：价值观、时间观、工作观是关键补充。每一观都建议你填四类内容：我怎么定义、我在追问什么、我当前的判断、我未来还要观察什么。</p>
            </div>
          </div>
          <div class="template-card" style="margin-bottom:16px;">
            <h4>这一块怎么写</h4>
            <div class="tag-row">
              <span class="tag">定义：这一观在我这里是什么意思</span>
              <span class="tag">问题：我长期在追问什么</span>
              <span class="tag">判断：我暂时相信什么</span>
              <span class="tag">观察：还要继续验证什么</span>
            </div>
            <p>不要追求全面，先写第一版。之后你每个月、每个季度都可以回来修正。</p>
          </div>
          <div class="accordion" id="viewsAccordion"></div>
        </div>
      </section>

      <section class="section" id="inputs">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>阅读输入系统</h3>
              <p>不要按公众号整理，要按“我的问题”和“我的判断”整理。每篇进入系统的内容，都至少经过一次压缩和改写。</p>
            </div>
            <div class="row">
              <button class="btn primary" id="addInputBtn">新增输入卡片</button>
            </div>
          </div>

          <div class="grid-2" style="margin-bottom:16px;">
            <div class="template-card">
              <h4>输入模板格式</h4>
              <p>每篇只提炼这几项，不要整段摘抄。</p>
              <div class="template-preview">1. 这篇内容在回答什么问题？
2. 它最核心的判断是什么？
3. 它凭什么这么说？
4. 我同意 / 不同意什么？
5. 用我的话重写成一句：______</div>
              <div class="card-actions">
                <button class="btn soft copy-template" data-copy="1. 这篇内容在回答什么问题？&#10;2. 它最核心的判断是什么？&#10;3. 它凭什么这么说？&#10;4. 我同意 / 不同意什么？&#10;5. 用我的话重写成一句：______">复制模板</button>
              </div>
            </div>
            <div class="template-card">
              <h4>筛选标准</h4>
              <div class="checklist">
                <div class="check-item"><input type="checkbox" disabled checked><div>它回应了我的长期问题之一</div></div>
                <div class="check-item"><input type="checkbox" disabled checked><div>它明显改变了我的看法，或者激发了强烈认同 / 反驳</div></div>
                <div class="check-item"><input type="checkbox" disabled checked><div>它能被我压成一句自己的判断，而不是只能收藏原文</div></div>
              </div>
            </div>
          </div>

          <div class="list" id="inputsList"></div>
        </div>
      </section>

      <section class="section" id="outputs">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>输出系统</h3>
              <p>先练“小判断”，不要一开始就追求长文。只要你能稳定把模糊感受压成清晰句子，表达系统就会慢慢长出来。</p>
            </div>
            <div class="row">
              <button class="btn primary" id="addOutputBtn">新增输出条目</button>
            </div>
          </div>
          <div class="grid-2" style="margin-bottom:16px;">
            <div class="template-card">
              <h4>每日输出模板</h4>
              <div class="template-preview">今天我在想：______
我现在的判断是：______
我的依据是：______
这个判断还不成熟，但我先把它说出来：______</div>
              <div class="card-actions">
                <button class="btn soft copy-template" data-copy="今天我在想：______&#10;我现在的判断是：______&#10;我的依据是：______&#10;这个判断还不成熟，但我先把它说出来：______">复制模板</button>
              </div>
            </div>
            <div class="template-card">
              <h4>适合你的 4 种句式</h4>
              <div class="template-preview">1. 我现在越来越觉得……
2. 以前我以为……现在我觉得……
3. 一个现象背后，真正的问题是……
4. 我不同意一种常见说法……</div>
            </div>
          </div>
          <div class="list" id="outputsList"></div>
        </div>
      </section>

      <section class="section" id="weeks">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>持续周系统</h3>
              <p>第一周写完后，第二周、第三周以后都可以继续新增。这个模块不是一次性的“第一周计划”，而是可持续滚动的长期周记录。</p>
            </div>
            <div class="row">
              <button class="btn primary" id="addWeekBtn">新增一周</button>
            </div>
          </div>
          <div class="grid-2" style="margin-bottom:16px;">
            <div class="template-card">
              <h4>每周模板格式</h4>
              <div class="template-preview">本周主题：______
本周最重要的 3 个问题：
1. ______
2. ______
3. ______

本周形成的 3 个判断：
1. ______
2. ______
3. ______

本周被修正的 1 个观点：______
下周继续追问什么：______</div>
              <div class="card-actions">
                <button class="btn soft copy-template" data-copy="本周主题：______&#10;本周最重要的 3 个问题：&#10;1. ______&#10;2. ______&#10;3. ______&#10;&#10;本周形成的 3 个判断：&#10;1. ______&#10;2. ______&#10;3. ______&#10;&#10;本周被修正的 1 个观点：______&#10;下周继续追问什么：______">复制模板</button>
              </div>
            </div>
            <div class="template-card">
              <h4>怎么长期使用</h4>
              <p>每周新增一张周卡，系统会把所有周卡一直保存下来。你可以回头看自己的问题是怎么推进的，观点是怎么被修正的。</p>
            </div>
          </div>
          <div class="timeline" id="weeksList"></div>
        </div>
      </section>

      <section class="section" id="dictionary">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>个人概念词典</h3>
              <p>长期拥有自己的语言系统，比看过很多内容更重要。把你反复使用、反复修正的词留下来，它们会构成你的思想骨架。</p>
            </div>
            <div class="row">
              <button class="btn primary" id="addConceptBtn">新增概念</button>
            </div>
          </div>
          <div class="grid-2" style="margin-bottom:16px;">
            <div class="template-card">
              <h4>概念模板格式</h4>
              <div class="template-preview">概念：______
在我这里，它的定义是：______
它不是什么：______
我为什么重视这个词：______
未来我还要怎么修正它：______</div>
            </div>
            <div class="template-card">
              <h4>推荐优先定义的词</h4>
              <div class="chips">
                <span class="chip">主体性</span>
                <span class="chip">独立</span>
                <span class="chip">判断力</span>
                <span class="chip">内在秩序</span>
                <span class="chip">可迁移能力</span>
                <span class="chip">边界</span>
                <span class="chip">长期主义</span>
                <span class="chip">有力量的表达</span>
              </div>
            </div>
          </div>
          <div class="list" id="conceptsList"></div>
        </div>
      </section>

      <section class="section" id="antiBubble">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>反信息茧房机制</h3>
              <p>目标不是绝对中立，而是有意识地对冲。你要防的不只是偏见，还包括“我以为自己已经有观点”的幻觉。</p>
            </div>
          </div>
          <div class="grid-2">
            <div class="field-card">
              <h4>我现在最容易陷入的偏好</h4>
              <textarea id="biasComfort" placeholder="例如：只看和自己气质相近的成长类内容；更容易被表达风格而不是论证本身说服。"></textarea>
            </div>
            <div class="field-card">
              <h4>本月我要主动加入的反方阅读</h4>
              <textarea id="biasCounter" placeholder="例如：每周至少读 2 篇我本能上不太认同但值得理解的文章；至少一个不同立场的 AI 观点源。"></textarea>
            </div>
          </div>
          <div class="grid-3" style="margin-top:16px;">
            <div class="template-card">
              <h4>四分法阅读提醒</h4>
              <div class="template-preview">阅读时区分：
1. 事实
2. 观点
3. 情绪
4. 叙事</div>
            </div>
            <div class="template-card">
              <h4>一个问题看两种立场</h4>
              <p>至少同时看乐观派、悲观派或中性分析派，避免被单一语气吞掉。</p>
            </div>
            <div class="template-card">
              <h4>追源头</h4>
              <p>尽量接触原书、原访谈、原始数据，而不是只看二手公众号加工。</p>
            </div>
          </div>
        </div>
      </section>

      <section class="section" id="assets">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>双资产库</h3>
              <p>观点资产是你怎么看世界，现实资产是你靠什么活、靠什么持续拥有选择权。两条线要一起建。</p>
            </div>
          </div>
          <div class="grid-2">
            <div class="field-card">
              <h4>观点资产库</h4>
              <p>写你已经形成、值得反复回看和迭代的判断句。</p>
              <textarea id="assetIdea" class="textarea-lg" placeholder="例如：AI 会降低执行门槛，但会抬高判断门槛。&#10;真正的独立不是孤立，而是低依赖、高选择权。&#10;读很多却说不出来，本质上是没有形成自己的问题结构。"></textarea>
            </div>
            <div class="field-card">
              <h4>现实资产库</h4>
              <p>写你正在积累或未来要积累的可迁移能力、关系资源、作品、职业资本。</p>
              <textarea id="assetReality" class="textarea-lg" placeholder="例如：稳定输出习惯、研究与总结能力、表达能力、AI 协作能力、可迁移作品集、稳定的合作关系。"></textarea>
            </div>
          </div>
        </div>
      </section>

      <section class="section" id="templates">
        <div class="panel">
          <div class="panel-header">
            <div>
              <h3>模板中心</h3>
              <p>你强调不要一长条，所以这里做成分块模板。每块都能单独看、单独复制、单独执行。</p>
            </div>
          </div>
          <div class="grid-3" id="templateCards"></div>
        </div>
      </section>

      <div class="footer-note">单文件 HTML · 本地自动保存到浏览器 · 适合电脑深度整理，也适合手机碎片记录。</div>
    </main>

    <nav class="mobile-nav" id="mobileNav">
      <button class="active" data-target="dashboard">仪表盘</button>
      <button data-target="vision">总纲</button>
      <button data-target="views">9观</button>
      <button data-target="inputs">输入</button>
      <button data-target="outputs">输出</button>
      <button data-target="weeks">周系统</button>
      <button data-target="templates">模板</button>
    </nav>
  </div>

  <script>
    const STORAGE_KEY = 'personal_thought_system_v1';
    const pageMeta = {
      dashboard: ['仪表盘', '先看整体状态，再决定今天写什么。'],
      vision: ['长期总纲', '未来 3–5 年不是拼命补信息，而是逐步长出自己的结构。'],
      views: ['9观系统', '你的长期框架：价值观、时间观、工作观等都要慢慢变成自己的语言。'],
      inputs: ['阅读输入', '所有输入都要经过压缩、改写、判断，才会真正属于你。'],
      outputs: ['输出系统', '先练短判断，再慢慢过渡到更长的表达。'],
      weeks: ['周系统', '第一周之后还可以持续写下去，每周都新增一张卡。'],
      dictionary: ['概念词典', '长期拥有自己的概念系统，比看过很多内容更重要。'],
      antiBubble: ['反茧房', '不是追求绝对不偏，而是建立有意识的对冲机制。'],
      assets: ['双资产库', '观点资产和现实资产要一起积累。'],
      templates: ['模板中心', '按块使用，不要把自己淹没在一整条大文档里。']
    };

    const defaultViews = [
      { key: 'value', title: '价值观', desc: '什么对我真正重要，什么值得长期投入，什么是假的繁荣。' },
      { key: 'self', title: '自我观', desc: '我怎样理解自己、主体性、成长、焦虑和稳定。' },
      { key: 'time', title: '时间观', desc: '我如何安排节奏、长期主义、阶段重点，以及避免被短期刺激牵着走。' },
      { key: 'learning', title: '学习观', desc: '学习在我这里到底是积累信息，还是塑造判断与人格。' },
      { key: 'expression', title: '表达观', desc: '什么是有力量的表达，我想形成怎样的语言和风格。' },
      { key: 'work', title: '工作观', desc: '工作对我意味着什么，什么是职业资产，什么只是暂时换钱。' },
      { key: 'ai', title: 'AI观', desc: 'AI 到底改变了什么，人还要保留什么，以及我如何与 AI 协作。' },
      { key: 'survival', title: '生存观', desc: '什么是独立生存体系，什么能力是可迁移的，如何保持选择权。' },
      { key: 'relationship', title: '关系观', desc: '亲密、边界、尊重、合作、依赖和自我之间的平衡。' }
    ];

    const defaultTemplates = [
      {
        title: '输入卡片',
        use: '整理公众号文章、书摘、访谈、播客、观察',
        body: '标题 / 来源 / 日期\n它在回答什么问题？\n它最核心的判断是什么？\n它凭什么这么说？\n我同意 / 不同意什么？\n用我的话重写成一句：______'
      },
      {
        title: '每日输出',
        use: '写 100–300 字判断',
        body: '今天我在想：______\n我现在的判断是：______\n我的依据是：______\n这个判断还不成熟，但我先把它说出来：______'
      },
      {
        title: '每周复盘',
        use: '周末收束与推进',
        body: '本周最重要的 3 个问题：\n1. ______\n2. ______\n3. ______\n\n本周形成的 3 个判断：\n1. ______\n2. ______\n3. ______\n\n本周被修正的观点：______\n下周继续追问：______'
      },
      {
        title: '概念定义',
        use: '建立你的个人概念词典',
        body: '概念：______\n在我这里，它的定义是：______\n它不是什么：______\n我为什么重视它：______\n未来怎么修正：______'
      },
      {
        title: '9观填写',
        use: '写每一观的第一版骨架',
        body: '这一观在我这里是什么意思：______\n我长期在追问什么：______\n我现在暂时相信什么：______\n未来还需要观察什么：______'
      },
      {
        title: '月度回看',
        use: '看系统是否在真正生长',
        body: '这个月我最常回到哪个问题？\n我最成熟的一个判断是什么？\n哪个判断被推翻了？\n我是不是在假努力或假输入？\n下个月我只推进哪 1–2 个重点？'
      }
    ];

    const defaultData = {
      currentSection: 'dashboard',
      calendarMonth: new Date().toISOString().slice(0, 7),
      fixed: {
        goalWho: '', goalAvoid: '', goalYear: '', goalThreeYears: '', goalFiveYears: '',
        biasComfort: '', biasCounter: '', assetIdea: '', assetReality: ''
      },
      themes: [
        { title: 'AI时代，个人如何保持主体性', why: '这是我的时代主线。', definition: '' },
        { title: '一个人如何建立自己的判断与表达系统', why: '这是我的成长主线。', definition: '' },
        { title: '什么是独立而不封闭的生存方式', why: '这是我的生命主线。', definition: '' }
      ],
      views: defaultViews.map(v => ({ ...v, definition: '', questions: '', judgment: '', observe: '' })),
      inputs: [],
      outputs: [],
      concepts: [],
      weeks: [createDefaultWeek(1)],
      lastSavedAt: null
    };

    function createDefaultWeek(n) {
      const today = new Date();
      const monday = new Date(today);
      monday.setDate(today.getDate() - ((today.getDay() + 6) % 7) + (n - 1) * 7);
      const sunday = new Date(monday);
      sunday.setDate(monday.getDate() + 6);
      return {
        id: uid(),
        weekNumber: n,
        title: `第 ${n} 周`,
        start: formatDate(monday),
        end: formatDate(sunday),
        focus: '',
        questions: '',
        judgments: '',
        revised: '',
        next: ''
      };
    }

    function uid() {
      return Math.random().toString(36).slice(2, 10) + Date.now().toString(36).slice(-4);
    }

    function formatDate(d) {
      const y = d.getFullYear();
      const m = String(d.getMonth() + 1).padStart(2, '0');
      const day = String(d.getDate()).padStart(2, '0');
      return `${y}-${m}-${day}`;
    }

    function loadData() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (!raw) return structuredClone(defaultData);
        const parsed = JSON.parse(raw);
        return mergeData(structuredClone(defaultData), parsed);
      } catch (e) {
        return structuredClone(defaultData);
      }
    }

    function mergeData(base, incoming) {
      const merged = { ...base, ...incoming };
      merged.fixed = { ...base.fixed, ...(incoming.fixed || {}) };
      merged.themes = Array.isArray(incoming.themes) && incoming.themes.length ? incoming.themes : base.themes;
      merged.views = Array.isArray(incoming.views) && incoming.views.length ? incoming.views : base.views;
      merged.inputs = Array.isArray(incoming.inputs) ? incoming.inputs : [];
      merged.outputs = Array.isArray(incoming.outputs) ? incoming.outputs : [];
      merged.concepts = Array.isArray(incoming.concepts) ? incoming.concepts : [];
      merged.weeks = Array.isArray(incoming.weeks) && incoming.weeks.length ? incoming.weeks : base.weeks;
      return merged;
    }

    let data = loadData();

    const fixedIds = ['goalWho', 'goalAvoid', 'goalYear', 'goalThreeYears', 'goalFiveYears', 'biasComfort', 'biasCounter', 'assetIdea', 'assetReality'];

    function saveData(showSignal = true) {
      data.lastSavedAt = new Date().toISOString();
      localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
      if (showSignal) {
        const status = document.getElementById('saveStatus');
        status.textContent = `已保存 · ${new Date().toLocaleTimeString('zh-CN', { hour: '2-digit', minute: '2-digit' })}`;
      }
      renderDashboard();
    }

    function setupFixedBindings() {
      fixedIds.forEach(id => {
        const el = document.getElementById(id);
        if (!el) return;
        el.value = data.fixed[id] || '';
        el.addEventListener('input', (e) => {
          data.fixed[id] = e.target.value;
          saveData(false);
        });
      });
    }

    function showSection(sectionId) {
      data.currentSection = sectionId;
      document.querySelectorAll('.section').forEach(sec => sec.classList.toggle('active', sec.id === sectionId));
      document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.toggle('active', btn.dataset.target === sectionId));
      document.querySelectorAll('.mobile-nav button').forEach(btn => btn.classList.toggle('active', btn.dataset.target === sectionId));
      const meta = pageMeta[sectionId] || ['个人思考系统', ''];
      document.getElementById('pageTitle').textContent = meta[0];
      document.getElementById('pageDesc').textContent = meta[1];
      saveData(false);
    }

    function bindNavigation() {
      document.querySelectorAll('[data-target]').forEach(btn => {
        btn.addEventListener('click', () => showSection(btn.dataset.target));
      });
    }

    function renderThemes() {
      const wrap = document.getElementById('themeCards');
      wrap.innerHTML = '';
      data.themes.forEach((theme, index) => {
        const card = document.createElement('div');
        card.className = 'field-card';
        card.innerHTML = `
          <h4>母题 ${index + 1}</h4>
          <label>标题</label>
          <input type="text" value="${escapeHtml(theme.title || '')}" data-theme-field="title" data-index="${index}" placeholder="例如：AI时代，个人如何保持主体性" />
          <label style="margin-top:10px;">为什么这条母题重要</label>
          <textarea class="textarea-sm" data-theme-field="why" data-index="${index}" placeholder="它是我的哪条主线？">${escapeHtml(theme.why || '')}</textarea>
          <label style="margin-top:10px;">我当前对它的一句话定义</label>
          <textarea data-theme-field="definition" data-index="${index}" placeholder="先写第一版，不求完整。">${escapeHtml(theme.definition || '')}</textarea>
        `;
        wrap.appendChild(card);
      });
      wrap.querySelectorAll('[data-theme-field]').forEach(el => {
        el.addEventListener('input', e => {
          const idx = Number(e.target.dataset.index);
          const key = e.target.dataset.themeField;
          data.themes[idx][key] = e.target.value;
          saveData(false);
        });
      });
    }

    function renderViews() {
      const wrap = document.getElementById('viewsAccordion');
      wrap.innerHTML = '';
      data.views.forEach((view, idx) => {
        const item = document.createElement('div');
        item.className = 'accordion-item' + (idx === 0 ? ' open' : '');
        item.innerHTML = `
          <button class="accordion-btn" type="button">
            <div>
              <strong>${escapeHtml(view.title)}</strong>
              <div class="small">${escapeHtml(view.desc || '')}</div>
            </div>
            <span class="status-pill">点击展开</span>
          </button>
          <div class="accordion-body">
            <div class="field-grid" style="margin-top:14px;">
              <div>
                <label>这一观在我这里是什么意思</label>
                <textarea data-view-index="${idx}" data-view-field="definition" placeholder="先写自己的定义，而不是照抄外部概念。">${escapeHtml(view.definition || '')}</textarea>
              </div>
              <div>
                <label>我长期在追问什么</label>
                <textarea data-view-index="${idx}" data-view-field="questions" placeholder="例如：AI 让什么更值钱？什么会空心化？">${escapeHtml(view.questions || '')}</textarea>
              </div>
              <div>
                <label>我现在暂时相信什么</label>
                <textarea data-view-index="${idx}" data-view-field="judgment" placeholder="写你当前的判断，不求成熟，但要真实。">${escapeHtml(view.judgment || '')}</textarea>
              </div>
              <div>
                <label>未来还需要观察什么</label>
                <textarea data-view-index="${idx}" data-view-field="observe" placeholder="哪些地方你还没有想透？">${escapeHtml(view.observe || '')}</textarea>
              </div>
            </div>
          </div>
        `;
        wrap.appendChild(item);
      });

      wrap.querySelectorAll('.accordion-btn').forEach(btn => {
        btn.addEventListener('click', () => {
          btn.parentElement.classList.toggle('open');
        });
      });

      wrap.querySelectorAll('[data-view-field]').forEach(el => {
        el.addEventListener('input', e => {
          const idx = Number(e.target.dataset.viewIndex);
          const key = e.target.dataset.viewField;
          data.views[idx][key] = e.target.value;
          saveData(false);
        });
      });
    }

    function escapeHtml(str) {
      return String(str)
        .replaceAll('&', '&amp;')
        .replaceAll('<', '&lt;')
        .replaceAll('>', '&gt;')
        .replaceAll('"', '&quot;');
    }

    function addInput() {
      data.inputs.unshift({
        id: uid(),
        date: formatDate(new Date()),
        title: '',
        source: '',
        link: '',
        theme: '',
        weekId: data.weeks[0]?.id || '',
        question: '',
        core: '',
        evidence: '',
        position: '',
        rewrite: ''
      });
      renderInputs();
      saveData();
      showSection('inputs');
    }

    function renderInputs() {
      const wrap = document.getElementById('inputsList');
      wrap.innerHTML = '';
      if (!data.inputs.length) {
        wrap.innerHTML = '<div class="empty-state">还没有输入卡片。先整理今天最值得留下的 1 篇文章。</div>';
        return;
      }
      data.inputs.forEach((item, idx) => {
        const weekOptions = data.weeks.map(w => `<option value="${w.id}" ${w.id === item.weekId ? 'selected' : ''}>${escapeHtml(w.title)}</option>`).join('');
        const card = document.createElement('div');
        card.className = 'entry-card';
        card.innerHTML = `
          <div class="panel-header" style="margin-bottom:10px;">
            <div>
              <h4>输入卡片 ${data.inputs.length - idx}</h4>
              <div class="small">进入系统的内容，最好都能被你压成一句自己的话。</div>
            </div>
            <div class="row">
              <button class="btn danger" data-remove-input="${item.id}">删除</button>
            </div>
          </div>
          <div class="field-grid">
            <div>
              <label>日期</label>
              <input type="date" value="${escapeHtml(item.date || '')}" data-input-id="${item.id}" data-input-field="date" />
            </div>
            <div>
              <label>周归属</label>
              <select data-input-id="${item.id}" data-input-field="weekId">${weekOptions}</select>
            </div>
            <div>
              <label>标题</label>
              <input type="text" value="${escapeHtml(item.title || '')}" data-input-id="${item.id}" data-input-field="title" placeholder="文章 / 书 / 播客标题" />
            </div>
            <div>
              <label>来源</label>
              <input type="text" value="${escapeHtml(item.source || '')}" data-input-id="${item.id}" data-input-field="source" placeholder="公众号 / 书名 / 作者" />
            </div>
            <div>
              <label>链接（可选）</label>
              <input type="url" value="${escapeHtml(item.link || '')}" data-input-id="${item.id}" data-input-field="link" placeholder="https://" />
            </div>
            <div>
              <label>关联主题</label>
              <input type="text" value="${escapeHtml(item.theme || '')}" data-input-id="${item.id}" data-input-field="theme" placeholder="例如：AI观 / 学习观 / 母题1" />
            </div>
            <div>
              <label>它在回答什么问题？</label>
              <textarea data-input-id="${item.id}" data-input-field="question">${escapeHtml(item.question || '')}</textarea>
            </div>
            <div>
              <label>它最核心的判断是什么？</label>
              <textarea data-input-id="${item.id}" data-input-field="core">${escapeHtml(item.core || '')}</textarea>
            </div>
            <div>
              <label>它凭什么这么说？</label>
              <textarea data-input-id="${item.id}" data-input-field="evidence">${escapeHtml(item.evidence || '')}</textarea>
            </div>
            <div>
              <label>我同意 / 不同意什么？</label>
              <textarea data-input-id="${item.id}" data-input-field="position">${escapeHtml(item.position || '')}</textarea>
            </div>
          </div>
          <div style="margin-top:12px;">
            <label>用我的话重写成一句</label>
            <textarea class="textarea-sm" data-input-id="${item.id}" data-input-field="rewrite" placeholder="这是最关键的一步。">${escapeHtml(item.rewrite || '')}</textarea>
          </div>
        `;
        wrap.appendChild(card);
      });

      wrap.querySelectorAll('[data-input-field]').forEach(el => {
        el.addEventListener('input', e => {
          const item = data.inputs.find(i => i.id === e.target.dataset.inputId);
          item[e.target.dataset.inputField] = e.target.value;
          saveData(false);
        });
      });
      wrap.querySelectorAll('[data-remove-input]').forEach(btn => {
        btn.addEventListener('click', () => {
          data.inputs = data.inputs.filter(i => i.id !== btn.dataset.removeInput);
          renderInputs();
          saveData();
        });
      });
    }

    function addOutput() {
      data.outputs.unshift({
        id: uid(),
        date: formatDate(new Date()),
        theme: '',
        type: '判断',
        weekId: data.weeks[0]?.id || '',
        hook: '',
        judgment: '',
        evidence: '',
        next: ''
      });
      renderOutputs();
      saveData();
      showSection('outputs');
    }

    function renderOutputs() {
      const wrap = document.getElementById('outputsList');
      wrap.innerHTML = '';
      if (!data.outputs.length) {
        wrap.innerHTML = '<div class="empty-state">还没有输出条目。今天先写一条 100–300 字判断就够。</div>';
        return;
      }
      data.outputs.forEach((item, idx) => {
        const weekOptions = data.weeks.map(w => `<option value="${w.id}" ${w.id === item.weekId ? 'selected' : ''}>${escapeHtml(w.title)}</option>`).join('');
        const card = document.createElement('div');
        card.className = 'entry-card';
        card.innerHTML = `
          <div class="panel-header" style="margin-bottom:10px;">
            <div>
              <h4>输出条目 ${data.outputs.length - idx}</h4>
              <div class="small">先追求清楚，再追求漂亮。</div>
            </div>
            <div class="row">
              <button class="btn danger" data-remove-output="${item.id}">删除</button>
            </div>
          </div>
          <div class="field-grid">
            <div>
              <label>日期</label>
              <input type="date" value="${escapeHtml(item.date || '')}" data-output-id="${item.id}" data-output-field="date" />
            </div>
            <div>
              <label>周归属</label>
              <select data-output-id="${item.id}" data-output-field="weekId">${weekOptions}</select>
            </div>
            <div>
              <label>主题</label>
              <input type="text" value="${escapeHtml(item.theme || '')}" data-output-id="${item.id}" data-output-field="theme" placeholder="例如：AI观 / 关系观 / 母题2" />
            </div>
            <div>
              <label>类型</label>
              <select data-output-id="${item.id}" data-output-field="type">
                <option ${item.type === '判断' ? 'selected' : ''}>判断</option>
                <option ${item.type === '短文' ? 'selected' : ''}>短文</option>
                <option ${item.type === '问题推进' ? 'selected' : ''}>问题推进</option>
                <option ${item.type === '复盘片段' ? 'selected' : ''}>复盘片段</option>
              </select>
            </div>
            <div>
              <label>今天我在想</label>
              <textarea data-output-id="${item.id}" data-output-field="hook">${escapeHtml(item.hook || '')}</textarea>
            </div>
            <div>
              <label>我现在的判断是</label>
              <textarea data-output-id="${item.id}" data-output-field="judgment">${escapeHtml(item.judgment || '')}</textarea>
            </div>
            <div>
              <label>我的依据是</label>
              <textarea data-output-id="${item.id}" data-output-field="evidence">${escapeHtml(item.evidence || '')}</textarea>
            </div>
            <div>
              <label>下一步还要继续追问什么</label>
              <textarea data-output-id="${item.id}" data-output-field="next">${escapeHtml(item.next || '')}</textarea>
            </div>
          </div>
        `;
        wrap.appendChild(card);
      });

      wrap.querySelectorAll('[data-output-field]').forEach(el => {
        el.addEventListener('input', e => {
          const item = data.outputs.find(i => i.id === e.target.dataset.outputId);
          item[e.target.dataset.outputField] = e.target.value;
          saveData(false);
        });
      });
      wrap.querySelectorAll('[data-remove-output]').forEach(btn => {
        btn.addEventListener('click', () => {
          data.outputs = data.outputs.filter(i => i.id !== btn.dataset.removeOutput);
          renderOutputs();
          saveData();
        });
      });
    }

    function addWeek() {
      const nextNum = (data.weeks.reduce((max, w) => Math.max(max, Number(w.weekNumber) || 0), 0) || 0) + 1;
      data.weeks.unshift(createDefaultWeek(nextNum));
      renderWeeks();
      renderInputs();
      renderOutputs();
      saveData();
      showSection('weeks');
    }

    function renderWeeks() {
      const wrap = document.getElementById('weeksList');
      wrap.innerHTML = '';
      if (!data.weeks.length) {
        wrap.innerHTML = '<div class="empty-state">还没有周记录。</div>';
        return;
      }
      data.weeks.forEach(week => {
        const timeline = document.createElement('div');
        timeline.className = 'timeline-item';
        timeline.innerHTML = `
          <div class="timeline-time">${escapeHtml(week.title)}<br><span class="small">${escapeHtml(week.start || '')} ～ ${escapeHtml(week.end || '')}</span></div>
          <div class="week-card">
            <div class="panel-header" style="margin-bottom:10px;">
              <div>
                <h4>${escapeHtml(week.title)}</h4>
                <div class="small">持续写下去。下一周只要新增，不用覆盖上一周。</div>
              </div>
              <div class="row">
                <button class="btn danger" data-remove-week="${week.id}" ${data.weeks.length === 1 ? 'disabled' : ''}>删除</button>
              </div>
            </div>
            <div class="field-grid">
              <div>
                <label>周标题</label>
                <input type="text" value="${escapeHtml(week.title || '')}" data-week-id="${week.id}" data-week-field="title" />
              </div>
              <div>
                <label>周序号</label>
                <input type="number" value="${escapeHtml(week.weekNumber || '')}" data-week-id="${week.id}" data-week-field="weekNumber" />
              </div>
              <div>
                <label>开始日期</label>
                <input type="date" value="${escapeHtml(week.start || '')}" data-week-id="${week.id}" data-week-field="start" />
              </div>
              <div>
                <label>结束日期</label>
                <input type="date" value="${escapeHtml(week.end || '')}" data-week-id="${week.id}" data-week-field="end" />
              </div>
              <div>
                <label>本周主题</label>
                <textarea class="textarea-sm" data-week-id="${week.id}" data-week-field="focus">${escapeHtml(week.focus || '')}</textarea>
              </div>
              <div>
                <label>本周最重要的 3 个问题</label>
                <textarea data-week-id="${week.id}" data-week-field="questions">${escapeHtml(week.questions || '')}</textarea>
              </div>
              <div>
                <label>本周形成的 3 个判断</label>
                <textarea data-week-id="${week.id}" data-week-field="judgments">${escapeHtml(week.judgments || '')}</textarea>
              </div>
              <div>
                <label>本周被修正的 1 个观点</label>
                <textarea data-week-id="${week.id}" data-week-field="revised">${escapeHtml(week.revised || '')}</textarea>
              </div>
            </div>
            <div style="margin-top:12px;">
              <label>下周继续追问什么</label>
              <textarea class="textarea-sm" data-week-id="${week.id}" data-week-field="next">${escapeHtml(week.next || '')}</textarea>
            </div>
          </div>
        `;
        wrap.appendChild(timeline);
      });

      wrap.querySelectorAll('[data-week-field]').forEach(el => {
        el.addEventListener('input', e => {
          const item = data.weeks.find(i => i.id === e.target.dataset.weekId);
          item[e.target.dataset.weekField] = e.target.value;
          saveData(false);
          renderDashboardFocus();
        });
      });
      wrap.querySelectorAll('[data-remove-week]').forEach(btn => {
        btn.addEventListener('click', () => {
          if (data.weeks.length === 1) return;
          const id = btn.dataset.removeWeek;
          data.weeks = data.weeks.filter(w => w.id !== id);
          data.inputs = data.inputs.map(i => ({ ...i, weekId: i.weekId === id ? (data.weeks[0]?.id || '') : i.weekId }));
          data.outputs = data.outputs.map(i => ({ ...i, weekId: i.weekId === id ? (data.weeks[0]?.id || '') : i.weekId }));
          renderWeeks();
          renderInputs();
          renderOutputs();
          saveData();
        });
      });
    }

    function addConcept() {
      data.concepts.unshift({
        id: uid(),
        name: '',
        definition: '',
        not: '',
        why: '',
        update: ''
      });
      renderConcepts();
      saveData();
      showSection('dictionary');
    }

    function renderConcepts() {
      const wrap = document.getElementById('conceptsList');
      wrap.innerHTML = '';
      if (!data.concepts.length) {
        wrap.innerHTML = '<div class="empty-state">还没有概念词条。先从“主体性、独立、判断力”里挑一个开始定义。</div>';
        return;
      }
      data.concepts.forEach((item, idx) => {
        const card = document.createElement('div');
        card.className = 'dictionary-card';
        card.innerHTML = `
          <div class="panel-header" style="margin-bottom:10px;">
            <div>
              <h4>概念词条 ${data.concepts.length - idx}</h4>
              <div class="small">不断修正，慢慢变成你自己的语言系统。</div>
            </div>
            <button class="btn danger" data-remove-concept="${item.id}">删除</button>
          </div>
          <div class="field-grid">
            <div>
              <label>概念</label>
              <input type="text" value="${escapeHtml(item.name || '')}" data-concept-id="${item.id}" data-concept-field="name" placeholder="例如：主体性" />
            </div>
            <div>
              <label>在我这里，它的定义是</label>
              <textarea data-concept-id="${item.id}" data-concept-field="definition">${escapeHtml(item.definition || '')}</textarea>
            </div>
            <div>
              <label>它不是什么</label>
              <textarea data-concept-id="${item.id}" data-concept-field="not">${escapeHtml(item.not || '')}</textarea>
            </div>
            <div>
              <label>我为什么重视它</label>
              <textarea data-concept-id="${item.id}" data-concept-field="why">${escapeHtml(item.why || '')}</textarea>
            </div>
          </div>
          <div style="margin-top:12px;">
            <label>未来还要怎么修正它</label>
            <textarea class="textarea-sm" data-concept-id="${item.id}" data-concept-field="update">${escapeHtml(item.update || '')}</textarea>
          </div>
        `;
        wrap.appendChild(card);
      });

      wrap.querySelectorAll('[data-concept-field]').forEach(el => {
        el.addEventListener('input', e => {
          const item = data.concepts.find(i => i.id === e.target.dataset.conceptId);
          item[e.target.dataset.conceptField] = e.target.value;
          saveData(false);
        });
      });
      wrap.querySelectorAll('[data-remove-concept]').forEach(btn => {
        btn.addEventListener('click', () => {
          data.concepts = data.concepts.filter(i => i.id !== btn.dataset.removeConcept);
          renderConcepts();
          saveData();
        });
      });
    }

    function renderTemplates() {
      const wrap = document.getElementById('templateCards');
      wrap.innerHTML = '';
      defaultTemplates.forEach(t => {
        const card = document.createElement('div');
        card.className = 'template-card';
        card.innerHTML = `
          <h4>${escapeHtml(t.title)}</h4>
          <p>用途：${escapeHtml(t.use)}</p>
          <div class="template-preview">${escapeHtml(t.body)}</div>
          <div class="card-actions">
            <button class="btn soft copy-template" data-copy="${escapeHtml(t.body).replace(/&quot;/g, '"')}">复制模板</button>
          </div>
        `;
        wrap.appendChild(card);
      });
    }

    function bindTemplateButtons() {
      document.body.addEventListener('click', e => {
        const btn = e.target.closest('.copy-template');
        if (!btn) return;
        const raw = btn.getAttribute('data-copy')
          .replaceAll('&lt;', '<')
          .replaceAll('&gt;', '>')
          .replaceAll('&amp;', '&')
          .replaceAll('&#10;', '\n');
        navigator.clipboard.writeText(raw).then(() => {
          const old = btn.textContent;
          btn.textContent = '已复制';
          setTimeout(() => btn.textContent = old, 1200);
        });
      });
    }

    function completionPercent() {
      const fields = [
        data.fixed.goalWho, data.fixed.goalAvoid, data.fixed.goalYear,
        data.themes[0]?.definition, data.themes[1]?.definition, data.themes[2]?.definition,
        ...data.views.flatMap(v => [v.definition, v.questions, v.judgment]),
      ];
      const filled = fields.filter(v => String(v || '').trim()).length;
      return Math.round((filled / fields.length) * 100);
    }

    function renderDashboard() {
      document.getElementById('statInputs').textContent = data.inputs.length;
      document.getElementById('statOutputs').textContent = data.outputs.length;
      document.getElementById('statWeeks').textContent = data.weeks.length;
      const completion = completionPercent();
      document.getElementById('statCompletion').textContent = `${completion}%`;
      document.getElementById('completionBar').style.width = `${completion}%`;
      renderCalendar();
      renderDashboardFocus();
    }

    function renderDashboardFocus() {
      const wrap = document.getElementById('dashboardFocus');
      const currentWeek = data.weeks[0];
      const inputsThisWeek = data.inputs.filter(i => i.weekId === currentWeek?.id).length;
      const outputsThisWeek = data.outputs.filter(i => i.weekId === currentWeek?.id).length;
      wrap.innerHTML = `
        <div class="mini-card">
          <h4>当前周</h4>
          <p><strong>${escapeHtml(currentWeek?.title || '第 1 周')}</strong></p>
          <p>${escapeHtml(currentWeek?.start || '')} ～ ${escapeHtml(currentWeek?.end || '')}</p>
          <p>${escapeHtml(currentWeek?.focus || '先给这一周写一个主题，例如：建立最小输入输出节律。')}</p>
        </div>
        <div class="mini-card">
          <h4>本周输入 / 输出</h4>
          <p>输入：${inputsThisWeek} 条</p>
          <p>输出：${outputsThisWeek} 条</p>
          <p>建议节奏：每周至少 3 张输入卡 + 3 条输出。</p>
        </div>
        <div class="mini-card">
          <h4>今日建议动作</h4>
          <p>${todaySuggestion()}</p>
        </div>
      `;
    }

    function todaySuggestion() {
      if (!data.fixed.goalWho) return '先写“未来 3–5 年我想成为什么样的人”。';
      if (!data.themes.some(t => t.definition.trim())) return '先给 3 条长期母题写一句自己的定义。';
      if (!data.views.find(v => v.key === 'value')?.judgment) return '先补“价值观”的第一版判断。';
      if (!data.inputs.length) return '今天先整理 1 篇文章做成输入卡片。';
      if (!data.outputs.length) return '今天先写 1 条 100–300 字判断。';
      return '进入正常节律：整理 1–3 篇输入，写 1 条判断，再做周推进。';
    }

    function renderCalendar() {
      const weekdays = ['一', '二', '三', '四', '五', '六', '日'];
      document.getElementById('calendarWeekdays').innerHTML = weekdays.map(d => `<div class="calendar-weekday">${d}</div>`).join('');

      const [year, month] = data.calendarMonth.split('-').map(Number);
      const first = new Date(year, month - 1, 1);
      const last = new Date(year, month, 0);
      const offset = (first.getDay() + 6) % 7;
      const total = last.getDate();
      const cells = [];
      for (let i = 0; i < offset; i++) cells.push('<div class="day empty"></div>');
      for (let day = 1; day <= total; day++) {
        const dateStr = `${year}-${String(month).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        const inputCount = data.inputs.filter(i => i.date === dateStr).length;
        const outputCount = data.outputs.filter(i => i.date === dateStr).length;
        const weekCount = data.weeks.filter(w => w.start === dateStr || w.end === dateStr).length;
        const isToday = dateStr === formatDate(new Date());
        const note = inputCount || outputCount ? `${inputCount ? `输入 ${inputCount}` : ''}${inputCount && outputCount ? ' · ' : ''}${outputCount ? `输出 ${outputCount}` : ''}` : (weekCount ? '周节点' : '');
        cells.push(`
          <div class="day ${isToday ? 'today' : ''}">
            <div class="day-number">${day}</div>
            <div class="day-markers">
              ${inputCount ? '<span class="marker input"></span>' : ''}
              ${outputCount ? '<span class="marker output"></span>' : ''}
              ${weekCount ? '<span class="marker week"></span>' : ''}
            </div>
            <div class="day-note">${note}</div>
          </div>
        `);
      }
      document.getElementById('calendarTitle').textContent = `${year} 年 ${month} 月`;
      document.getElementById('calendarDays').innerHTML = cells.join('');
    }

    function bindCalendar() {
      document.getElementById('prevMonth').addEventListener('click', () => shiftMonth(-1));
      document.getElementById('nextMonth').addEventListener('click', () => shiftMonth(1));
    }

    function shiftMonth(offset) {
      const [y, m] = data.calendarMonth.split('-').map(Number);
      const d = new Date(y, m - 1 + offset, 1);
      data.calendarMonth = `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}`;
      renderCalendar();
      saveData(false);
    }

    function bindToolbar() {
      document.getElementById('saveBtn').addEventListener('click', () => saveData());
      document.getElementById('addInputBtn').addEventListener('click', addInput);
      document.getElementById('addOutputBtn').addEventListener('click', addOutput);
      document.getElementById('addWeekBtn').addEventListener('click', addWeek);
      document.getElementById('addConceptBtn').addEventListener('click', addConcept);
      document.getElementById('exportBtn').addEventListener('click', exportData);
      document.getElementById('importFile').addEventListener('change', importData);
    }

    function exportData() {
      const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `个人思考系统备份_${formatDate(new Date())}.json`;
      a.click();
      URL.revokeObjectURL(url);
    }

    function importData(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => {
        try {
          const imported = JSON.parse(reader.result);
          data = mergeData(structuredClone(defaultData), imported);
          refreshAll();
          saveData();
        } catch (e) {
          alert('导入失败：文件格式不正确');
        }
      };
      reader.readAsText(file, 'utf-8');
      event.target.value = '';
    }

    function refreshAll() {
      setupFixedBindings();
      renderThemes();
      renderViews();
      renderInputs();
      renderOutputs();
      renderWeeks();
      renderConcepts();
      renderTemplates();
      renderDashboard();
      showSection(data.currentSection || 'dashboard');
    }

    function init() {
      bindNavigation();
      bindToolbar();
      bindCalendar();
      bindTemplateButtons();
      refreshAll();
    }

    init();
  </script>
<script defer src="https://static.cloudflareinsights.com/beacon.min.js/v8c78df7c7c0f484497ecbca7046644da1771523124516" integrity="sha512-8DS7rgIrAmghBFwoOTujcf6D9rXvH8xm8JQ1Ja01h9QX8EzXldiszufYa4IFfKdLUKTTrnSFXLDkUEOTrZQ8Qg==" data-cf-beacon='{"version":"2024.11.0","token":"7939e04a4baf43c8b86a560f74aac60e","server_timing":{"name":{"cfCacheStatus":true,"cfEdge":true,"cfExtPri":true,"cfL4":true,"cfOrigin":true,"cfSpeedBrain":true},"location_startswith":null}}' crossorigin="anonymous"></script>
</body>
</html>
