[index.html](https://github.com/user-attachments/files/26387789/index.html)
<!DOCTYPE html>
<html lang="zh-CN"><head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>365天通识框架 · 文明架构师之路</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@300;400;600;700&family=Noto+Sans+SC:wght@300;400;500&family=Cinzel:wght@400;600&display=swap');

  :root {
    --bg: #0a0c10;
    --surface: #11141a;
    --surface2: #181c24;
    --border: #252a35;
    --accent1: #c8975a;
    --accent2: #5a8fc8;
    --accent3: #7ac87a;
    --accent4: #c85a7a;
    --accent5: #a05ac8;
    --accent6: #5ac8b4;
    --accent7: #c8c85a;
    --accent8: #c87a5a;
    --accent9: #8ac8c8;
    --accent10: #c8a07a;
    --text: #e8e0d0;
    --text2: #9a9080;
    --text3: #6a6070;
  }

  /* ─── LIGHT THEME ─── */
  body.light {
    --bg: #f5f2ec;
    --surface: #ede9e0;
    --surface2: #e4dfd4;
    --border: #d0c9bc;
    --text: #2a2420;
    --text2: #6a5f52;
    --text3: #9a8f82;
  }
  body.light #stars { opacity: 0; }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Noto Sans SC', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ─── STARFIELD ─── */
  #stars {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background: radial-gradient(ellipse at 20% 20%, #0d1428 0%, #0a0c10 60%);
  }
  #stars::before, #stars::after {
    content: '';
    position: absolute; inset: 0;
    background-image:
      radial-gradient(1px 1px at 10% 15%, #fff8 0%, transparent 100%),
      radial-gradient(1px 1px at 30% 45%, #fff5 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 55% 25%, #fff6 0%, transparent 100%),
      radial-gradient(1px 1px at 75% 60%, #fff4 0%, transparent 100%),
      radial-gradient(1px 1px at 90% 10%, #fff7 0%, transparent 100%),
      radial-gradient(1px 1px at 15% 75%, #fff5 0%, transparent 100%),
      radial-gradient(1px 1px at 45% 85%, #fff3 0%, transparent 100%),
      radial-gradient(1px 1px at 65% 90%, #fff6 0%, transparent 100%),
      radial-gradient(1px 1px at 85% 35%, #fff4 0%, transparent 100%),
      radial-gradient(1px 1px at 5% 50%, #fff5 0%, transparent 100%);
  }

  /* ─── HEADER ─── */
  .header {
    position: relative; z-index: 10;
    text-align: center;
    padding: 60px 20px 40px;
    border-bottom: 1px solid var(--border);
  }
  .header-eyebrow {
    font-family: 'Cinzel', serif;
    font-size: 11px;
    letter-spacing: 6px;
    color: var(--accent1);
    text-transform: uppercase;
    margin-bottom: 16px;
    opacity: 0.8;
  }
  .header h1 {
    font-family: 'Noto Serif SC', serif;
    font-size: clamp(28px, 5vw, 52px);
    font-weight: 300;
    line-height: 1.2;
    color: var(--text);
    letter-spacing: 4px;
    margin-bottom: 12px;
  }
  .header h1 span { color: var(--accent1); }
  .header-sub {
    font-size: 13px;
    color: var(--text2);
    letter-spacing: 2px;
    margin-bottom: 32px;
  }
  .header-stats {
    display: flex; justify-content: center; gap: 40px; flex-wrap: wrap;
  }
  .stat {
    text-align: center;
  }
  .stat-num {
    font-family: 'Cinzel', serif;
    font-size: 28px;
    color: var(--accent1);
    line-height: 1;
  }
  .stat-label {
    font-size: 11px;
    color: var(--text3);
    letter-spacing: 2px;
    margin-top: 4px;
  }

  /* ─── LEGEND ─── */
  .legend {
    position: relative; z-index: 10;
    display: flex; flex-wrap: wrap; gap: 8px;
    justify-content: center;
    padding: 20px 40px;
    border-bottom: 1px solid var(--border);
  }
  .legend-item {
    display: flex; align-items: center; gap: 6px;
    font-size: 11px; color: var(--text2);
    cursor: pointer;
    padding: 4px 10px;
    border-radius: 20px;
    border: 1px solid transparent;
    transition: all 0.2s;
  }
  .legend-item:hover { border-color: var(--border); background: var(--surface); }
  .legend-dot {
    width: 8px; height: 8px; border-radius: 50%;
    flex-shrink: 0;
  }

  /* ─── GRID ─── */
  .grid {
    position: relative; z-index: 10;
    display: flex;
    flex-direction: column;
  }

  /* ─── MODULE ROW (full width) ─── */
  .module {
    background: var(--bg);
    border-bottom: 1px solid var(--border);
    transition: background 0.2s;
  }
  .module.active { background: var(--surface); }

  .module-header {
    display: flex; align-items: center; gap: 14px;
    padding: 0;
    cursor: pointer;
    user-select: none;
    transition: background 0.15s;
  }
  .module-header:hover { background: var(--surface2); }

  /* colored left accent bar */
  .module-accent {
    width: 4px;
    align-self: stretch;
    flex-shrink: 0;
    border-radius: 0;
  }

  .module-icon {
    width: 36px; height: 36px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 17px;
    flex-shrink: 0;
    margin: 14px 0 14px 16px;
  }

  .module-meta { flex: 1; min-width: 0; padding: 14px 0; }
  .module-num {
    font-family: 'Cinzel', serif;
    font-size: 9px;
    letter-spacing: 3px;
    color: var(--text3);
    margin-bottom: 3px;
    text-transform: uppercase;
  }
  .module-title {
    font-family: 'Noto Serif SC', serif;
    font-size: 15px;
    font-weight: 600;
    line-height: 1.3;
    margin-bottom: 2px;
  }
  .module-subtitle {
    font-size: 11px;
    color: var(--text2);
  }
  .module-days {
    font-family: 'Cinzel', serif;
    font-size: 10px;
    color: var(--text3);
    letter-spacing: 1px;
    margin-top: 2px;
  }

  /* right side: day range badge + chevron */
  .module-right {
    display: flex; align-items: center; gap: 10px;
    padding-right: 18px; flex-shrink: 0;
  }
  .module-range-badge {
    font-family: 'Cinzel', serif;
    font-size: 9px; letter-spacing: 2px;
    padding: 3px 9px;
    border-radius: 20px;
    border: 1px solid var(--border);
    color: var(--text3);
    white-space: nowrap;
  }
  .module-chevron {
    font-size: 11px; color: var(--text3);
    transition: transform 0.25s;
    flex-shrink: 0;
  }
  .module.active .module-chevron { transform: rotate(90deg); }

  /* ─── WEEKS (revealed inside module) ─── */
  .weeks { display: none; }
  .module.active .weeks { display: block; padding: 0 0 16px; }

  .week { margin: 0; border-left: none; padding-left: 0; }
  .week-header {
    display: flex; align-items: center; gap: 8px;
    padding: 8px 20px 6px 24px;
    cursor: pointer;
    user-select: none;
    border-top: 1px solid var(--border);
    margin-top: 8px;
  }
  .week-header:first-child { border-top: none; }
  .week-arrow {
    font-size: 9px; color: var(--text3);
    transition: transform 0.2s; flex-shrink: 0;
  }
  .week.open .week-arrow { transform: rotate(90deg); }
  .week-title { font-size: 11px; color: var(--text2); font-weight: 500; }
  .week-days-count {
    font-size: 9px; color: var(--text3);
    margin-left: auto; letter-spacing: 1px;
  }

  /* ─── DAYS GRID (4 columns) ─── */
  .days { display: none; }
  .week.open .days {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 6px;
    padding: 8px 20px 4px 20px;
  }

  @media (max-width: 1100px) { .week.open .days { grid-template-columns: repeat(3, 1fr); } }
  @media (max-width: 760px)  { .week.open .days { grid-template-columns: repeat(2, 1fr); } }
  @media (max-width: 480px)  { .week.open .days { grid-template-columns: 1fr; } }

  /* ─── DAY CARD ─── */
  .day {
    display: flex; flex-direction: column; gap: 5px;
    padding: 10px 12px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 6px;
    transition: border-color 0.15s, background 0.15s;
    cursor: default;
  }
  .day:hover { border-color: var(--text3); background: var(--surface); }
  .day-num {
    font-family: 'Cinzel', serif;
    font-size: 9px;
    letter-spacing: 2px;
    color: var(--text3);
    flex-shrink: 0;
  }
  .day-content { flex: 1; min-width: 0; }
  .day-topic {
    font-size: 12px;
    color: var(--text);
    line-height: 1.4;
    font-weight: 500;
    margin-bottom: 2px;
  }
  .day-topic em {
    font-style: normal;
    font-size: 9px;
    font-weight: 400;
    opacity: 0.5;
    display: block;
    margin-bottom: 1px;
  }
  .day-desc {
    font-size: 10px;
    color: var(--text3);
    line-height: 1.5;
    margin-top: 2px;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* ─── SPECIAL TAGS ─── */
  .tag {
    display: inline-block;
    font-size: 9px;
    letter-spacing: 1px;
    padding: 1px 6px;
    border-radius: 3px;
    margin-top: 3px;
    font-family: 'Cinzel', serif;
  }
  .tag-review { background: #c8975a22; color: var(--accent1); border: 1px solid #c8975a44; }
  .tag-cross  { background: #5a8fc822; color: var(--accent2); border: 1px solid #5a8fc844; }

  /* ─── TIMELINE BAR ─── */
  .timeline {
    position: relative; z-index: 10;
    padding: 40px 40px;
    border-top: 1px solid var(--border);
  }
  .timeline-title {
    font-family: 'Noto Serif SC', serif;
    font-size: 13px;
    color: var(--text2);
    letter-spacing: 3px;
    margin-bottom: 20px;
    text-align: center;
  }
  .timeline-track {
    display: flex;
    height: 8px;
    border-radius: 4px;
    overflow: hidden;
    gap: 1px;
  }
  .timeline-seg {
    height: 100%;
    transition: all 0.3s;
    cursor: pointer;
    position: relative;
  }
  .timeline-seg:hover { filter: brightness(1.4); }
  .timeline-labels {
    display: flex;
    margin-top: 10px;
    position: relative;
    height: 20px;
  }
  .timeline-label {
    font-size: 9px;
    color: var(--text3);
    letter-spacing: 1px;
    position: absolute;
    transform: translateX(-50%);
    white-space: nowrap;
  }

  /* ─── FOOTER ─── */
  .footer {
    position: relative; z-index: 10;
    text-align: center;
    padding: 40px 20px;
    border-top: 1px solid var(--border);
    color: var(--text3);
    font-size: 11px;
    letter-spacing: 2px;
  }
  .footer span { color: var(--accent1); }

  /* ─── EXPAND ALL BTN ─── */
  .controls {
    position: relative; z-index: 10;
    display: flex; flex-wrap: wrap; justify-content: center; gap: 6px;
    padding: 10px 12px;
    border-bottom: 1px solid var(--border);
  }
  .btn {
    font-family: 'Noto Sans SC', sans-serif;
    font-size: 12px;
    padding: 6px 12px;
    border: 1px solid var(--border);
    background: transparent;
    color: var(--text2);
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.2s;
    white-space: nowrap;
    display: inline-flex; align-items: center; gap: 4px;
  }
  .btn:hover { background: var(--surface2); color: var(--text); border-color: var(--text3); }
  .btn.primary { border-color: var(--accent1); color: var(--accent1); }
  .btn.primary:hover { background: #c8975a18; }

  /* ─── NOTE SYSTEM ─── */
  .note-area {
    margin-top: 8px;
    border-top: 1px dashed #ffffff0f;
    padding-top: 8px;
  }
  .note-toggle {
    display: inline-flex; align-items: center; gap: 5px;
    font-size: 10px;
    color: var(--text3);
    cursor: pointer;
    padding: 3px 0;
    transition: color 0.2s;
    user-select: none;
    background: none; border: none;
  }
  .note-toggle:hover { color: var(--accent1); }
  .note-toggle .nt-icon { font-size: 11px; }
  .note-toggle.has-note { color: var(--accent1); }
  .note-toggle.has-note .nt-icon::before { content: '✦'; }
  .note-toggle:not(.has-note) .nt-icon::before { content: '✧'; }

  .note-editor { display: none; margin-top: 8px; }
  .note-editor.open { display: block; }

  .note-textarea {
    width: 100%;
    min-height: 72px;
    background: #ffffff06;
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    font-family: 'Noto Sans SC', sans-serif;
    font-size: 12px;
    line-height: 1.7;
    padding: 10px 12px;
    resize: vertical;
    outline: none;
    transition: border-color 0.2s;
  }
  .note-textarea:focus { border-color: var(--accent1); }
  .note-textarea::placeholder { color: var(--text3); }

  .note-actions {
    display: flex; gap: 8px; margin-top: 6px; align-items: center;
  }
  .note-save {
    font-family: 'Cinzel', serif;
    font-size: 9px; letter-spacing: 1.5px;
    padding: 5px 14px;
    border: 1px solid var(--accent1);
    background: transparent;
    color: var(--accent1);
    border-radius: 3px;
    cursor: pointer;
    transition: all 0.2s;
  }
  .note-save:hover { background: #c8975a20; }
  .note-save:active { transform: scale(0.97); }
  .note-clear {
    font-size: 10px; color: var(--text3);
    background: none; border: none; cursor: pointer;
    padding: 5px 8px;
    transition: color 0.2s;
  }
  .note-clear:hover { color: #c85a7a; }
  .note-timestamp {
    font-size: 10px; color: var(--text3);
    margin-left: auto;
  }

  .note-display-wrap {
    margin-top: 6px;
    border-left: 2px solid var(--accent1);
    border-radius: 0 4px 4px 0;
    background: #c8975a08;
    display: none;
    overflow: hidden;
  }
  .note-display-wrap.visible { display: block; }

  .note-display-header {
    display: flex; align-items: center; justify-content: space-between;
    padding: 6px 10px;
    cursor: pointer;
    user-select: none;
  }
  .note-display-header:hover { background: #c8975a10; }
  .note-display-label {
    font-size: 10px; color: var(--accent1);
    letter-spacing: 1px; font-family: 'Cinzel', serif;
    display: flex; align-items: center; gap: 5px;
  }
  .note-display-arrow {
    font-size: 9px; color: var(--accent1);
    transition: transform 0.2s;
    display: inline-block;
  }
  .note-display-wrap.collapsed .note-display-arrow { transform: rotate(-90deg); }

  .note-display {
    font-size: 12px;
    color: var(--text2);
    line-height: 1.7;
    white-space: pre-wrap;
    padding: 0 10px 10px;
    transition: max-height 0.25s ease;
  }
  .note-display-wrap.collapsed .note-display {
    display: none;
  }

  /* progress dot on day num */
  .day-num.noted { color: var(--accent1); }
  .day-num.noted::after {
    content: '·';
    display: block;
    text-align: center;
    margin-top: -4px;
    font-size: 16px;
    line-height: 1;
  }

  /* ─── SYNC STATUS ─── */
  .sync-status {
    font-size: 10px; letter-spacing: 1px;
    padding: 4px 10px;
    border-radius: 20px;
    border: 1px solid var(--border);
    transition: all 0.3s;
    white-space: nowrap;
  }
  .sync-idle    { color: var(--text3); border-color: var(--border); }
  .sync-saving  { color: var(--accent1); border-color: var(--accent1); }
  .sync-saved   { color: var(--accent3); border-color: var(--accent3); }
  .sync-error   { color: var(--accent4); border-color: var(--accent4); }

  /* ─── STATS BAR ─── */
  .progress-bar-wrap {
    position: relative; z-index: 10;
    padding: 12px 40px;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 16px;
  }
  .progress-label { font-size: 11px; color: var(--text3); white-space: nowrap; }
  .progress-track {
    flex: 1; height: 4px; background: var(--border); border-radius: 2px; overflow: hidden;
  }
  .progress-fill {
    height: 100%; background: var(--accent1); border-radius: 2px;
    transition: width 0.4s ease;
  }
  .progress-count { font-family: 'Cinzel', serif; font-size: 11px; color: var(--accent1); white-space: nowrap; }

  /* ─── TODAY HIGHLIGHT ─── */
  .day.today {
    background: linear-gradient(90deg, #c8975a12 0%, transparent 100%);
    border-radius: 4px;
    margin: 0 -4px;
    padding-left: 4px;
    padding-right: 4px;
  }
  .day-num.today-num {
    color: var(--accent1) !important;
  }
  .today-badge {
    display: inline-block;
    font-size: 9px; font-family: 'Cinzel', serif;
    letter-spacing: 1px;
    background: var(--accent1);
    color: #000;
    padding: 1px 5px;
    border-radius: 3px;
    margin-left: 6px;
    vertical-align: middle;
  }

  /* ─── SEARCH ─── */
  .search-bar {
    position: relative; z-index: 10;
    padding: 10px 14px;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 8px;
  }
  .search-input {
    flex: 1;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    color: var(--text);
    font-family: 'Noto Sans SC', sans-serif;
    font-size: 14px;
    padding: 8px 16px 8px 38px;
    outline: none;
    transition: border-color 0.2s;
  }
  .search-input:focus { border-color: var(--accent1); }
  .search-input::placeholder { color: var(--text3); }
  .search-icon {
    position: absolute; left: 28px;
    color: var(--text3); font-size: 15px;
    pointer-events: none;
  }
  .search-count {
    font-size: 12px; color: var(--text3);
    white-space: nowrap;
  }
  .search-clear {
    background: none; border: none; color: var(--text3);
    cursor: pointer; font-size: 20px; padding: 0 2px;
    transition: color 0.2s; line-height: 1;
  }
  .search-clear:hover { color: var(--text); }

  /* 搜索结果面板 */
  .search-results {
    display: none;
    position: relative; z-index: 10;
    border-bottom: 2px solid var(--accent1)44;
    background: var(--surface);
    max-height: 60vh;
    overflow-y: auto;
  }
  .search-results.open { display: block; }
  .search-result-item {
    display: flex; align-items: flex-start; gap: 10px;
    padding: 10px 16px;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
    transition: background 0.15s;
  }
  .search-result-item:hover { background: var(--surface2); }
  .search-result-item:last-child { border-bottom: none; }
  .sr-num {
    font-family: 'Cinzel', serif; font-size: 10px;
    color: var(--accent1); min-width: 32px;
    padding-top: 2px; flex-shrink: 0;
  }
  .sr-body { flex: 1; min-width: 0; }
  .sr-topic {
    font-size: 13px; font-weight: 500;
    color: var(--text); line-height: 1.4;
  }
  .sr-meta {
    font-size: 11px; color: var(--text3);
    margin-top: 2px;
  }
  .sr-note {
    font-size: 11px; color: var(--accent1);
    margin-top: 3px; line-height: 1.5;
    background: #c8975a0c;
    border-left: 2px solid var(--accent1)66;
    padding: 3px 6px;
    border-radius: 0 3px 3px 0;
  }
  .sr-hl { background: #c8975a44; border-radius: 2px; padding: 0 1px; }
  .search-no-result {
    padding: 32px; text-align: center;
    color: var(--text3); font-size: 13px;
  }

  /* ─── JOURNAL VIEW ─── */
  .journal-overlay {
    display: none;
    position: fixed; inset: 0; z-index: 200;
    background: var(--bg);
    overflow-y: auto;
    padding: 40px;
  }
  .journal-overlay.open { display: block; }
  .journal-header {
    display: flex; align-items: center; gap: 16px;
    margin-bottom: 32px;
  }
  .journal-title {
    font-family: 'Noto Serif SC', serif;
    font-size: 22px; font-weight: 300;
    color: var(--text); letter-spacing: 4px;
  }
  .journal-title span { color: var(--accent1); }
  .journal-close {
    margin-left: auto;
    background: none; border: 1px solid var(--border);
    color: var(--text2); font-size: 12px;
    padding: 6px 16px; border-radius: 4px;
    cursor: pointer; font-family: 'Cinzel', serif;
    letter-spacing: 1px; transition: all 0.2s;
  }
  .journal-close:hover { border-color: var(--accent1); color: var(--accent1); }
  .journal-entry {
    margin-bottom: 20px;
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    transition: border-color 0.2s;
  }
  .journal-entry:hover { border-color: var(--accent1); }
  .journal-entry-head {
    display: flex; align-items: baseline; gap: 10px;
    padding: 12px 16px;
    background: var(--surface);
    border-bottom: 1px solid var(--border);
  }
  .journal-day-num {
    font-family: 'Cinzel', serif; font-size: 11px;
    color: var(--accent1); letter-spacing: 2px;
  }
  .journal-topic {
    font-size: 13px; font-weight: 500; color: var(--text);
  }
  .journal-module {
    font-size: 10px; color: var(--text3);
    margin-left: auto; white-space: nowrap;
  }
  .journal-date {
    font-size: 10px; color: var(--text3);
    padding: 0 16px; margin-top: 8px;
  }
  .journal-text {
    font-size: 13px; color: var(--text2);
    line-height: 1.8; white-space: pre-wrap;
    padding: 8px 16px 14px;
  }
  .journal-empty {
    text-align: center; padding: 80px 20px;
    color: var(--text3); font-size: 14px;
    line-height: 2;
  }

  /* ─── LINK PANEL ─── */
  .link-btn {
    font-size: 9px; color: var(--text3);
    background: none; border: none; cursor: pointer;
    padding: 2px 4px; margin-left: 2px;
    transition: color 0.2s;
  }
  .link-btn:hover { color: var(--accent2); }
  .day-links {
    display: flex; flex-wrap: wrap; gap: 4px;
    margin-top: 4px;
  }
  .link-chip {
    font-size: 10px; color: var(--accent2);
    border: 1px solid var(--accent2)44;
    background: var(--accent2)11;
    border-radius: 10px; padding: 1px 8px;
    cursor: pointer; transition: all 0.2s;
  }
  .link-chip:hover { background: var(--accent2)22; }
  .link-chip .remove-link {
    margin-left: 4px; opacity: 0.6;
    cursor: pointer;
  }
  .link-chip .remove-link:hover { opacity: 1; color: var(--accent4); }

  /* ─── EBBINGHAUS REMINDER ─── */
  .ebbinghaus-bar {
    position: relative; z-index: 10;
    border-bottom: 1px solid var(--border);
    background: var(--surface);
    overflow: hidden;
  }
  .ebbinghaus-bar.empty { display: none; }

  .ebb-header {
    display: flex; align-items: center; gap: 8px;
    padding: 10px 16px 0;
    cursor: pointer; user-select: none;
  }
  .ebb-title {
    font-size: 11px; letter-spacing: 2px;
    color: var(--text3);
    font-family: 'Cinzel', serif;
  }
  .ebb-toggle-arrow {
    font-size: 10px; color: var(--text3);
    transition: transform 0.2s; margin-left: auto;
  }
  .ebbinghaus-bar.collapsed .ebb-toggle-arrow { transform: rotate(-90deg); }

  .ebb-cards {
    display: flex; gap: 10px;
    padding: 10px 16px 14px;
    overflow-x: auto;
    scrollbar-width: none;
  }
  .ebb-cards::-webkit-scrollbar { display: none; }
  .ebbinghaus-bar.collapsed .ebb-cards { display: none; }

  .ebb-card {
    flex-shrink: 0;
    width: 200px;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 12px;
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s;
    background: var(--bg);
  }
  .ebb-card:hover { border-color: var(--accent1); background: var(--surface2); }

  .ebb-card-label {
    font-size: 9px; letter-spacing: 2px;
    font-family: 'Cinzel', serif;
    margin-bottom: 5px;
  }
  .ebb-label-1  { color: #c85a7a; }
  .ebb-label-7  { color: #c8975a; }
  .ebb-label-30 { color: #5a8fc8; }

  .ebb-card-day {
    font-size: 11px; color: var(--text3);
    margin-bottom: 3px;
  }
  .ebb-card-topic {
    font-size: 12px; font-weight: 500;
    color: var(--text); line-height: 1.4;
    margin-bottom: 5px;
  }
  .ebb-card-note {
    font-size: 11px; color: var(--text2);
    line-height: 1.5;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  /* ─── THEME TOGGLE ─── */
  .theme-btn {
    font-size: 16px; background: none;
    border: 1px solid var(--border);
    border-radius: 4px; padding: 6px 10px;
    cursor: pointer; color: var(--text2);
    transition: all 0.2s; line-height: 1;
  }
  .theme-btn:hover { border-color: var(--accent1); color: var(--accent1); }

  /* ─── EBBINGHAUS BAR ─── */
  .ebb-bar {
    position: relative; z-index: 10;
    border-bottom: 1px solid var(--border);
    background: var(--surface);
    transition: all 0.3s;
  }
  .ebb-bar.empty { display: none; }
  .ebb-header {
    display: flex; align-items: center; gap: 10px;
    padding: 8px 14px;
    cursor: pointer; user-select: none;
  }
  .ebb-header:hover { background: var(--surface2); }
  .ebb-title {
    font-size: 11px; color: var(--accent1);
    font-family: 'Cinzel', serif; letter-spacing: 2px;
    flex: 1;
  }
  .ebb-toggle-arrow {
    font-size: 10px; color: var(--text3);
    transition: transform 0.2s;
  }
  .ebb-bar.collapsed .ebb-toggle-arrow { transform: rotate(-90deg); }
  .ebb-cards {
    display: flex; gap: 10px;
    padding: 0 14px 12px;
    overflow-x: auto;
    scrollbar-width: none;
  }
  .ebb-bar.collapsed .ebb-cards { display: none; }
  .ebb-cards::-webkit-scrollbar { display: none; }
  .ebb-card {
    min-width: 180px; max-width: 220px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px; padding: 10px 12px;
    cursor: pointer; flex-shrink: 0;
    transition: border-color 0.2s, transform 0.15s;
  }
  .ebb-card:hover { border-color: var(--accent1); transform: translateY(-2px); }
  .ebb-card-label {
    font-size: 9px; font-family: 'Cinzel', serif;
    letter-spacing: 1px; margin-bottom: 5px;
    padding: 2px 6px; border-radius: 3px;
    display: inline-block;
  }
  .ebb-label-1  { background: #c85a7a22; color: #c85a7a; }
  .ebb-label-7  { background: #c8975a22; color: var(--accent1); }
  .ebb-label-30 { background: #5a8fc822; color: var(--accent2); }
  .ebb-card-day   { font-size: 10px; color: var(--text3); margin-bottom: 3px; }
  .ebb-card-topic { font-size: 12px; color: var(--text); font-weight: 500; margin-bottom: 5px; line-height: 1.4; }
  .ebb-card-note  { font-size: 11px; color: var(--text2); line-height: 1.5; }

  /* ─── TAGS ─── */
  .day-tags {
    display: flex; flex-wrap: wrap; gap: 4px;
    margin-top: 5px;
  }
  .tag-chip {
    font-size: 10px;
    padding: 1px 8px; border-radius: 10px;
    border: 1px solid var(--border);
    color: var(--text3);
    cursor: pointer; transition: all 0.15s;
    background: transparent;
  }
  .tag-chip:hover { border-color: var(--accent1); color: var(--accent1); }
  .tag-chip.active { background: var(--accent1); color: #000; border-color: var(--accent1); font-weight: 500; }
  .day.tag-dimmed { opacity: 0.18; }
  .day.tag-matched { outline: 1px solid var(--accent1)66; border-radius: 4px; }

  /* tag filter banner */
  .tag-filter-bar {
    display: none;
    position: sticky; top: 0; z-index: 50;
    background: #c8975a18;
    border-bottom: 1px solid var(--accent1)55;
    padding: 6px 14px;
    align-items: center; gap: 10px;
  }
  .tag-filter-bar.visible { display: flex; }
  .tag-filter-info { font-size: 12px; color: var(--accent1); flex: 1; }
  .tag-filter-clear {
    font-size: 11px; color: var(--text3);
    background: none; border: 1px solid var(--border);
    border-radius: 10px; padding: 3px 10px;
    cursor: pointer; transition: all 0.2s;
  }
  .tag-filter-clear:hover { border-color: var(--accent4); color: var(--accent4); }

  /* ─── MINI TAG NETWORK POPUP ─── */
  .tag-graph-popup {
    display: none;
    position: fixed;
    z-index: 400;
    background: #0e1118ee;
    border: 1px solid var(--accent1)66;
    border-radius: 12px;
    box-shadow: 0 8px 40px #000a, 0 0 0 1px #c8975a22;
    overflow: hidden;
    backdrop-filter: blur(12px);
    min-width: 340px;
    max-width: 420px;
    user-select: none;
  }
  .tag-graph-popup.open { display: block; }

  .tgp-header {
    display: flex; align-items: center; gap: 8px;
    padding: 10px 14px 8px;
    border-bottom: 1px solid #ffffff0f;
    cursor: move;
  }
  .tgp-icon { font-size: 13px; }
  .tgp-title {
    font-family: 'Cinzel', serif;
    font-size: 11px; letter-spacing: 2px;
    color: var(--accent1); flex: 1;
  }
  .tgp-count {
    font-size: 10px; color: var(--text3);
    letter-spacing: 1px;
  }
  .tgp-close {
    background: none; border: none;
    color: var(--text3); font-size: 16px;
    cursor: pointer; padding: 0 2px; line-height: 1;
    transition: color 0.2s;
  }
  .tgp-close:hover { color: var(--accent4); }

  #tag-graph-canvas {
    display: block;
    cursor: grab;
  }
  #tag-graph-canvas:active { cursor: grabbing; }

  .tgp-footer {
    padding: 6px 12px;
    border-top: 1px solid #ffffff08;
    font-size: 10px; color: var(--text3);
    letter-spacing: 1px;
    display: flex; align-items: center; gap: 10px;
  }
  .tgp-footer-dot {
    width: 6px; height: 6px; border-radius: 50%;
    display: inline-block; margin-right: 3px;
    vertical-align: middle;
  }
  .tgp-hint { margin-left: auto; color: var(--text3); font-size: 9px; }

  /* ─── KNOWLEDGE GRAPH ─── */
  .graph-overlay {
    display: none;
    position: fixed; inset: 0; z-index: 300;
    background: #020408;
    flex-direction: column;
  }
  .graph-overlay.open { display: flex; }

  /* body = canvas fills entirely; panel floats over as overlay */
  .graph-body {
    flex: 1; position: relative; overflow: hidden;
  }

  #graph-canvas {
    position: absolute; inset: 0;
    display: block;
    cursor: crosshair;
    touch-action: none;
    width: 100%; height: 100%;
  }
  .graph-toolbar {
    display: flex; align-items: center; gap: 8px;
    padding: 8px 14px;
    background: rgba(2,4,8,0.92);
    border-bottom: 1px solid #ffffff0a;
    flex-shrink: 0; flex-wrap: wrap;
    backdrop-filter: blur(8px);
    z-index: 10;
  }
  .graph-title {
    font-family: 'Cinzel', serif;
    font-size: 12px; font-weight: 400;
    color: #c8975a88; letter-spacing: 4px; flex: 1;
    text-transform: uppercase;
  }
  .graph-btn {
    font-size: 10px; padding: 4px 11px;
    border: 1px solid #ffffff14; background: transparent;
    color: #6a6a7a; border-radius: 20px; cursor: pointer;
    transition: all 0.2s; white-space: nowrap;
    font-family: 'Cinzel', serif; letter-spacing: 1px;
  }
  .graph-btn:hover  { border-color: #c8975a66; color: #c8975a; }
  .graph-btn.active { background: #c8975a18; border-color: #c8975a88; color: #c8975a; }
  .graph-close {
    font-size: 16px; background: none; border: none;
    color: #3a3a4a; cursor: pointer; padding: 4px 8px;
    transition: color 0.2s; line-height: 1;
  }
  .graph-close:hover { color: #e8e0d0; }

  /* ─── NODE INFO PANEL (absolute overlay, right side) ─── */
  .graph-panel {
    position: absolute;
    right: 0; top: 0; bottom: 0;
    width: 0; overflow: hidden;
    background: rgba(4,6,14,0.97);
    border-left: 0px solid transparent;
    display: flex; flex-direction: column;
    transition: width 0.32s cubic-bezier(.4,0,.2,1),
                border-color 0.32s;
    z-index: 6;
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
  }
  .graph-panel.open {
    width: min(320px, 80vw);
    border-left: 1px solid #ffffff10;
  }

  .gp-header {
    padding: 18px 18px 12px;
    border-bottom: 1px solid #ffffff08;
    flex-shrink: 0;
  }
  .gp-day-badge {
    font-family: 'Cinzel', serif;
    font-size: 9px; letter-spacing: 3px;
    color: #6a6070; margin-bottom: 6px;
  }
  .gp-topic {
    font-family: 'Noto Serif SC', serif;
    font-size: 15px; font-weight: 600;
    color: #e8e0d0; line-height: 1.4;
    margin-bottom: 4px;
  }
  .gp-field {
    font-size: 11px; color: #9a9080;
    letter-spacing: 1px;
    margin-bottom: 8px;
  }
  .gp-desc {
    font-size: 11px; color: #6a6a7a;
    line-height: 1.7;
  }
  .gp-jump-btn {
    display: inline-flex; align-items: center; gap: 5px;
    margin-top: 10px;
    font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 2px;
    color: #c8975a; border: 1px solid #c8975a55;
    background: #c8975a0c;
    padding: 5px 12px; border-radius: 3px;
    cursor: pointer; transition: all 0.2s;
    text-transform: uppercase;
  }
  .gp-jump-btn:hover { background: #c8975a22; border-color: #c8975a; }

  .gp-section-title {
    font-family: 'Cinzel', serif;
    font-size: 9px; letter-spacing: 3px; text-transform: uppercase;
    color: #3a3a5a; padding: 10px 18px 6px;
    border-bottom: 1px solid #ffffff06;
    flex-shrink: 0;
  }

  .gp-connections {
    flex: 1; overflow-y: auto;
    scrollbar-width: thin; scrollbar-color: #2a2a3a transparent;
  }
  .gp-connections::-webkit-scrollbar { width: 4px; }
  .gp-connections::-webkit-scrollbar-thumb { background: #2a2a3a; border-radius: 2px; }

  .gp-conn-item {
    display: flex; gap: 10px; align-items: flex-start;
    padding: 10px 18px;
    border-bottom: 1px solid #ffffff05;
    cursor: pointer;
    transition: background 0.15s;
  }
  .gp-conn-item:hover { background: #ffffff06; }
  .gp-conn-dot {
    width: 8px; height: 8px; border-radius: 50%;
    flex-shrink: 0; margin-top: 4px;
    box-shadow: 0 0 5px currentColor;
  }
  .gp-conn-body { flex: 1; min-width: 0; }
  .gp-conn-day {
    font-family: 'Cinzel', serif; font-size: 9px;
    letter-spacing: 2px; color: #5a5a6a;
    margin-bottom: 2px;
  }
  .gp-conn-topic {
    font-size: 12px; color: #c8c0b0;
    font-weight: 500; line-height: 1.4;
    margin-bottom: 2px;
  }
  .gp-conn-field { font-size: 10px; color: #5a5a6a; }
  .gp-conn-type {
    font-size: 9px; letter-spacing: 1px;
    padding: 1px 5px; border-radius: 8px;
    font-family: 'Cinzel', serif;
    flex-shrink: 0; margin-top: 3px;
  }
  .gp-conn-type.link { color: #5a8fc8; background: #5a8fc811; border: 1px solid #5a8fc833; }
  .gp-conn-type.tag  { color: #c8975a; background: #c8975a0e; border: 1px solid #c8975a33; }

  .gp-empty {
    padding: 32px 18px; text-align: center;
    font-size: 12px; color: #2a2a3a;
    line-height: 2;
    letter-spacing: 1px;
  }

  .graph-hint {
    position: absolute; bottom: 12px; left: 50%;
    transform: translateX(-50%);
    font-size: 10px; color: #ffffff18;
    letter-spacing: 2px; font-family: 'Cinzel', serif;
    pointer-events: none; white-space: nowrap;
    text-transform: uppercase;
  }

  .graph-legend {
    display: flex; flex-wrap: wrap; gap: 10px;
    padding: 6px 14px;
    border-top: 1px solid #ffffff07;
    flex-shrink: 0;
    background: rgba(2,4,8,0.88);
  }
  .graph-legend-item {
    display: flex; align-items: center; gap: 5px;
    font-size: 9px; color: #4a4a5a;
    font-family: 'Cinzel', serif; letter-spacing: 1px;
    cursor: pointer; transition: color 0.2s;
  }
  .graph-legend-item:hover { color: #9a9080; }
  .graph-legend-dot {
    width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0;
    box-shadow: 0 0 4px currentColor;
  }
</style>
</head>
<body>

<div id="stars"></div>

<header class="header">
  <div class="header-eyebrow">Mind Map · 文明架构师之路</div>
  <h1>365天<span>通识框架</span></h1>
  <div class="header-sub">从宇宙起源到个体重构 · 十大认知模块 · 完整知识体系</div>
  <div class="header-stats">
    <div class="stat"><div class="stat-num">365</div><div class="stat-label">DAYS</div></div>
    <div class="stat"><div class="stat-num">10</div><div class="stat-label">MODULES</div></div>
    <div class="stat"><div class="stat-num">52</div><div class="stat-label">WEEKS</div></div>
    <div class="stat"><div class="stat-num">12</div><div class="stat-label">MONTHS</div></div>
  </div>
</header>

<!-- 艾宾浩斯复习提醒 -->
<div class="ebbinghaus-bar" id="ebbinghaus-bar">
  <div class="ebb-header" onclick="toggleEbb()">
    <span style="font-size:14px">🔔</span>
    <span class="ebb-title">旧闻提醒 · 温故知新</span>
    <span class="ebb-toggle-arrow">▾</span>
  </div>
  <div class="ebb-cards" id="ebb-cards">
      <div class="ebb-card" onclick="jumpToDay(2)">
        <div class="ebb-card-label ebb-label-1">
          ↩ 复习提醒 · 1天前
        </div>
        <div class="ebb-card-day">Day 2 · 物理学</div>
        <div class="ebb-card-topic">牛顿力学与决定论</div>
        <div class="ebb-card-note">经典力学与决定论    Q1-物理学/哲学    2026-03-31
1. 核心逻辑 (The "Why")：
如果世…</div>
      </div></div>
</div>

<!-- 艾宾浩斯旧闻提醒条 -->
<div class="ebb-bar empty" id="ebbinghaus-bar">
  <div class="ebb-header" onclick="toggleEbb()">
    <span class="ebb-title">↩ 旧闻提醒 · 温故知新</span>
    <span class="ebb-toggle-arrow">▾</span>
  </div>
  <div class="ebb-cards" id="ebb-cards"></div>
</div>

<!-- 标签筛选提示条 -->
<div class="tag-filter-bar" id="tag-filter-bar">
  <span class="tag-filter-info" id="tag-filter-info"></span>
  <button class="tag-filter-clear" onclick="clearTagFilter()">× 清除筛选</button>
</div>

<div class="controls">
  <button class="btn primary" onclick="expandAll()">＋ 全展开</button>
  <button class="btn" onclick="collapseAll()">－ 全收起</button>
  <button class="btn" onclick="expandAllWeeks()">≡ 展开周</button>
  <button class="btn" onclick="randomWander()">🎲 随机</button>
  <button class="btn" onclick="openGraph()">🕸 知识图谱</button>
  <button class="btn" onclick="openJournal()">📖 日志</button>
  <button class="btn" onclick="exportNotes()">⬇ 导出MD</button>
  <button class="btn" onclick="exportJSON()">{ } 导出JSON</button>
  <button class="theme-btn" onclick="toggleTheme()" title="切换明暗主题">☀</button>
</div>

<!-- 知识图谱浮层 -->
<div class="graph-overlay" id="graph-overlay">
  <div class="graph-toolbar">
    <span class="graph-title">✦ Knowledge Cosmos</span>
    <button class="graph-btn active" id="graph-btn-all" onclick="graphFilter('all')">全宇宙</button>
    <button class="graph-btn" id="graph-btn-linked" onclick="graphFilter('linked')">仅有连线</button>
    <button class="graph-btn" id="graph-btn-noted" onclick="graphFilter('noted')">仅有感悟</button>
    <button class="graph-btn" onclick="graphReset()">重置视野</button>
    <button class="graph-close" onclick="closeGraph()">✕</button>
  </div>
  <div class="graph-body">
    <canvas id="graph-canvas"></canvas>
    <div class="graph-hint" id="graph-hint">点击星点 · 探索关联</div>
    <!-- 节点详情面板 -->
    <div class="graph-panel" id="graph-panel">
      <div class="gp-header" id="gp-header">
        <div class="gp-day-badge" id="gp-day-badge">DAY —</div>
        <div class="gp-topic" id="gp-topic">选择一颗星</div>
        <div class="gp-field" id="gp-field"></div>
        <div class="gp-desc" id="gp-desc"></div>
        <button class="gp-jump-btn" id="gp-jump-btn" onclick="graphJumpSelected()" style="display:none">
          ↗ 跳转到主视图
        </button>
      </div>
      <div class="gp-section-title" id="gp-section-title" style="display:none">
        CONNECTED NODES
      </div>
      <div class="gp-connections" id="gp-connections">
        <div class="gp-empty">点击图中任意星点<br>查看知识关联</div>
      </div>
    </div>
  </div>
  <div class="graph-legend" id="graph-legend"></div>
</div>

<div class="search-bar">
  <span class="search-icon">🔍</span>
  <input class="search-input" id="search-input" placeholder="搜索主题、学科、感悟内容…" oninput="doSearch(this.value)">
  <button class="search-clear" onclick="clearSearch()" title="清除">×</button>
  <span class="search-count" id="search-count"></span>
</div>
<div class="search-results" id="search-results"></div>

<!-- 学习日志浮层 -->
<div class="journal-overlay" id="journal-overlay">
  <div class="journal-header">
    <div class="journal-title">📖 <span>学习日志</span></div>
    <button class="journal-close" onclick="closeJournal()">× 关闭</button>
  </div>
  <div id="journal-content"></div>
</div>

<div class="progress-bar-wrap">
  <span class="progress-label">学习进度</span>
  <div class="progress-track"><div class="progress-fill" id="progress-fill" style="width: 1%;"></div></div>
  <span class="progress-count" id="progress-count">2 / 365 天</span>
  <span class="sync-status sync-saving" id="sync-status">⬇ 生成中…</span>
</div>

<div class="legend" id="legend"><div class="legend-item"><div class="legend-dot" style="background:#7ac87a"></div><span>自然科学与演化</span></div><div class="legend-item"><div class="legend-dot" style="background:#5a8fc8"></div><span>认知与人文精神</span></div><div class="legend-item"><div class="legend-dot" style="background:#c85a7a"></div><span>社会秩序与博弈</span></div><div class="legend-item"><div class="legend-dot" style="background:#c8975a"></div><span>技术与文明重启</span></div><div class="legend-item"><div class="legend-dot" style="background:#a05ac8"></div><span>艺术、媒介与视觉美学</span></div><div class="legend-item"><div class="legend-dot" style="background:#5ac8b4"></div><span>数学、密码学与复杂系统</span></div><div class="legend-item"><div class="legend-dot" style="background:#c8c85a"></div><span>地缘、资源与大国博弈</span></div><div class="legend-item"><div class="legend-dot" style="background:#c87a5a"></div><span>商业帝国、资本流转与组织演化</span></div><div class="legend-item"><div class="legend-dot" style="background:#8ac8c8"></div><span>语言、符号与思想架构</span></div><div class="legend-item"><div class="legend-dot" style="background:#c8a07a"></div><span>心智算法·未来视野·大一统闭环</span></div></div>

<div class="grid" id="grid"><div class="module active" id="module-1">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#7ac87a"></div>
        <div class="module-icon" style="background:#7ac87a18; color:#7ac87a">⚛️</div>
        <div class="module-meta">
          <div class="module-num">MODULE 01</div>
          <div class="module-title" style="color:#7ac87a">自然科学与演化
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">宇宙的「硬件驱动」</span>
          </div>
          <div class="module-days" style="color:#7ac87a77">物理·化学·生物·演化论·脑科学·生态学</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#7ac87a44;color:#7ac87a99">Day 1–30</span>
          <span class="module-chevron" style="color:#7ac87a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week open">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W1 · 物理学基础</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day today" data-day="1" data-tags="物理学,熵,热力学,宇宙起源">
            <div class="day-num today-num noted" id="daynum-1">D1</div>
            <div class="day-content">
              <div class="day-topic"><em>物理学</em>熵增定律<span class="today-badge">TODAY</span></div>
              <div class="day-desc">理解为什么有序必然走向无序。无论组织管理还是整理房间，本质上都是在「抗熵」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('物理学',this);">物理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('热力学',this);">热力学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙起源',this);">宇宙起源</span></div>
              <div class="note-area">
                <button class="note-toggle has-note" id="note-toggle-1" onclick="toggleNote(1)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">编辑感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(1)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-1"></div>
                <div class="note-display-wrap visible" id="note-display-wrap-1">
                  <div class="note-display-header" onclick="toggleNoteDisplay(1)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-1">熵增定律    Q1-物理学/热力学    2026-03-29
1. 核心逻辑 (The "Why")
用一句话描述这个概念揭示了世界的什么本质规律？
EG：在一个封闭系统中，无序度只会自发增加，除非有外部能量输入。
2. 降维解释 (ELI5)
如果要把这个概念讲给一个不具备专业背景的人，你会用什么类比？
EG：不收拾的房间会自动变乱；洗牌只会越洗越乱。
3. 跨界迁移 (Cross-Domain Bridge)
这个逻辑如何解释另一个领域的现象？
EG：公司不进行流程优化就会滑向人浮于事；模型训练是在噪声中强行制造秩序。
4. 衍生思考/行动建议 (Actionable Insight)
这个知识点改变了你对某件事的看法吗？你打算如何应用它？
EG：承认混乱是常态，所以不再为“琐碎的杂事”焦虑，而是要有意识地投入“高质量能量”去对抗它。

熵增定律：宇宙的终极宿命
第一幕：从一个房间开始
想象你的房间。
早上你刚整理完，一切井井有条：书在书架上，衣服叠好，桌面干净。然后你开始生活——住了一周之后，房间自然变乱了。
现在问你一个问题：你有没有见过一个房间，在没有人打扫的情况下，自己从乱变整齐的？
没有。从来没有。
这不是巧合，这是宇宙的一条铁律。
为什么乱是"自然"的？
假设你把一副扑克牌按顺序排好：A、2、3……K，四种花色全部有序。然后你开始随机洗牌。
洗一次——乱了。
再洗——更乱。
你能洗回原来的顺序吗？理论上可以，但概率极低，低到你洗一辈子也几乎不可能发生。
原因很简单：有序的排列方式只有极少数，无序的排列方式有天文数字那么多。 随机发生的事，几乎必然落在"无序"这一侧。
这就是熵的本质——
熵，是一个系统"混乱程度"的度量。混乱越高，熵越高。
热力学第二定律（熵增定律）用一句话说就是：
在一个封闭的系统里，熵只会增加，永远不会自发减少。
宇宙不会自己从乱变整齐。能量不会自己从分散变集中。时间只朝一个方向走。

第二幕：熵是时间的方向
这里有一件很奇怪的事，值得你停下来想一想。
物理学里几乎所有的方程，时间倒过来也成立。一颗球从空中落下，你把这个过程倒放，从地面弹回手里——这在物理上是完全合法的。引力方程不管时间正反。
但有一件事，倒放就会显得荒谬——
一杯热咖啡放在桌上，慢慢变凉。你把这个过程倒放：一杯冷咖啡，自己越来越热，热量从空气中聚集回杯子里。这绝对不会发生。
为什么？
因为热量自发地从高温流向低温，是熵在增加。反过来，热量自发从低温流向高温，熵会减少——而熵不会自发减少。
所以熵增定律，实际上定义了时间的方向。
我们感知到"过去"和"未来"的区别，根本原因就在这里。物理学家卡洛·罗韦利说：时间之所以流动，是因为宇宙的熵在增加。如果熵不增加，时间就没有方向，"昨天"和"明天"将没有区别。
你现在正在经历"时间流逝"这件事，本质上是你在感知宇宙的熵增。

第三幕：宇宙的终局——热寂
现在把视野放到最大。
宇宙是一个（近似的）封闭系统。熵增定律对它也适用。
宇宙诞生于138亿年前的大爆炸。那一刻，宇宙处于一种极度有序、极度低熵的状态——所有的能量高度集中。从那以后，宇宙一直在膨胀，能量一直在扩散，熵一直在增加。
星星燃烧，是在把核能转化为热和光向外散射——熵在增加。
生命新陈代谢，是在消耗有序的能量——熵在增加。
你今天读这篇文章，你的大脑消耗葡萄糖——熵在增加。
一切活动，无一例外，都在推动宇宙走向同一个终点。
这个终点叫做"热寂"（Heat Death）。
在热寂状态下：
宇宙中所有的能量完全均匀分布，没有任何温差
没有温差就没有能量流动，没有能量流动就没有任何事情发生
没有星星，没有生命，没有运动，没有时间意义上的"变化"
宇宙进入永恒的、均匀的、死寂的平衡
这不是爆炸式的终结，而是一种极度安静的消亡——宇宙慢慢"散"掉了。
时间尺度是10的100次方年以后的事。但方向，从大爆炸那一刻起就已注定。

第四幕：那生命算什么？
学到这里，你可能会有一个很自然的困惑：
如果熵只能增加，那生命是怎么回事？
一颗受精卵变成婴儿，婴儿长大成人——这明明是从简单变复杂，从无序变有序，熵在减少。这不是违反了定律吗？
没有违反。这是整个主题最精彩的地方。
1944年，物理学家薛定谔在《生命是什么》里给出了答案——
生命是靠"吃"负熵为生的。
什么意思？
熵增定律说的是封闭系统。但生命不是封闭系统，生命一直在和外界交换物质和能量。
植物吸收阳光（高质量、低熵的能量），释放热量（低质量、高熵的能量）。在这个过程里，植物内部的秩序增加了——但代价是，它把更多的熵排放到了外界环境中。
你吃饭，消化食物，用其中有序的化学能维持你身体的复杂结构。同时你呼出CO₂、散发热量，把熵排放到外面。
生命从来没有消灭熵，只是把熵转移出去了。 局部的有序，是以周围环境更大的无序为代价换来的。算总账，整个宇宙的熵依然在增加。
这给了我们一个非常深刻的视角来理解生命的本质：
生命是宇宙中一种暂时的、局部的、对抗熵增的结构。 它不违反热力学第二定律，它只是在规则允许的范围内，尽可能地延缓自身的瓦解。
所有的生命活动——进食、繁殖、进化、文明的建立——从物理角度看，都是同一件事：从环境中汲取低熵，维持自身的有序，同时向外输出更多的熵。
这件事会一直持续，直到太阳熄灭，直到所有的星星熄灭，直到宇宙热寂。

检验时间
问题一（概念）
冰箱能把食物从热变冷，这是不是违反了熵增定律？为什么？
问题二（应用）
一座城市从小村庄发展成现代都市，变得越来越有序复杂——这是熵在减少吗？
问题三（思辨）
如果宇宙最终走向热寂，你觉得这对"意义"这个概念意味着什么？

Q1：不是，因为冰箱先是吸收了食物的热气，熵增了，同时又通过发动机把热气排放出去，是一个正向的但是内部会循环的熵增过程 
评：你抓住了关键——冰箱不是封闭系统，它在向外排热。这个方向完全对。
但有一个地方需要纠正："吸收食物热气，熵增了"——这里的主语搞混了。食物变冷，是食物自身的熵在减少。冰箱把这部分热量排到了房间里，房间的熵增加，而且增加得更多。所以总账上，熵是净增加的。
一句话总结你应该说的：冰箱让食物局部降熵，代价是让外部环境熵增更多，符合定律。
迁：一个公司如果不从外部获取人才和订单（能量），内部流程只会越来越僵化、混乱。

Q2：不是，这只是形式上的排列聚集，而非能量上的
评：城市的“有序”代价极其高昂。为了维持一座城市的运转，我们燃烧了海量的煤炭、石油（低熵），排放了巨量的二氧化碳和废热（高熵）。城市是宇宙中一个巨大的熵增放大器。所以城市是和生命一样的东西：局部有序，全局加速熵增。

Q3：这个时候还有概念这个词吗
评：热寂之后没有观察者，没有语言，没有思维，"意义"这个词连同说出它的人一起消失了。意义不是宇宙的属性，它只存在于低熵结构（也就是生命）短暂存在的窗口期里。
这个答案的哲学名字叫反实在论——意义不是被发现的，是被制造的，而制造它的机器（生命）是暂时的。

答疑
问：植物吸收阳光（高质量、低熵的能量），释放热量（低质量、高熵的能量）
答：先从"能量质量"这个说法开始
能量有高低质量之分，不是指能量多少，而是指它能不能被用来做事。
阳光是高质量能量。光子集中、定向、有秩序地从太阳射来，你可以用它驱动化学反应、发电、让植物生长。它是"可用的"。
热量是低质量能量。分子随机乱撞产生的热，分散、无序、方向混乱。你很难再从它身上提取有用的功了。
一个比喻：同样是100块钱，一张整钞和一堆硬币散在地上——面值一样，但你能用整钞做的事，散币做不到。阳光是整钞，热量是散币。
回到植物这个例子
植物吸收一份高质量的阳光能量，用它把CO₂和水组装成葡萄糖——这是在建造有序的化学结构，植物自身的熵降低了。
但这个过程不是免费的。植物同时向外释放热量，而且释放出去的热量，比它吸收的阳光能量更"散"、更无序。
所以：
植物内部：熵减少 ✓
外部环境：熵增加，而且增加更多 ✓
总账：熵净增加 ✓
一句话的本质
阳光的低熵被植物"消费"掉，换成了植物体内的有序结构。但消费过程本身产生了更多的无序热量排出去。
就像你花100块整钞买了一件有用的东西，但找零回来的全是散币，而且散币加起来只有90块。有序的钱变成了东西，但同时损耗掉一部分变成了更无序的形式。
这个道理对所有生命都成立，对所有机器也成立——没有任何转换过程是不产生"散币"的。</div>
                </div>
                <div class="note-editor open" id="note-editor-1">
                  <textarea class="note-textarea" id="note-ta-1" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(1)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(1)">删除</button>
                    <span class="note-timestamp" id="note-ts-1">2026/3/31 22:28 已保存</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="2" data-tags="物理学,宇宙起源,量子力学">
            <div class="day-num noted" id="daynum-2">D2 ✦</div>
            <div class="day-content">
              <div class="day-topic"><em>物理学</em>牛顿力学与决定论</div>
              <div class="day-desc">只要知道初始状态，就能预测未来吗？理解宏观世界的「确定性」与系统控制的错觉。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('物理学',this);">物理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙起源',this);">宇宙起源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('量子力学',this);">量子力学</span></div>
              <div class="note-area">
                <button class="note-toggle has-note" id="note-toggle-2" onclick="toggleNote(2)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">编辑感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(2)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-2"></div>
                <div class="note-display-wrap visible" id="note-display-wrap-2">
                  <div class="note-display-header" onclick="toggleNoteDisplay(2)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)">2026/3/31 22:22</span>
                  </div>
                  <div class="note-display" id="note-display-2">经典力学与决定论    Q1-物理学/哲学    2026-03-31
1. 核心逻辑 (The "Why")：
如果世界遵循固定的因果方程（如 F = ma），那么只要掌握所有初始数据，未来就是可以被精确计算的。
2. 降维解释 (ELI5)：
宇宙是一台巨大的、在大爆炸时就上好了发条的精密钟表，每一个齿轮的转动都是注定的。
3. 跨界迁移 (Cross-Domain Bridge)：
管理学：试图通过模型和数据预测一切，是典型的决定论思维；
历史学：大趋势（生产力发展）可能是决定的，但英雄人物的偶然选择是混沌的种子。
4. 衍生思考 (Actionable Insight)：
接受宏观上的“不可抗力”，但在微观瞬间保持“选择感”。即便自由意志可能是幻觉，这种“主观能动性的体验”也是对抗熵增、维持生命有序的唯一动力。

牛顿力学与决定论：宇宙是一台钟表吗？
第一幕：一个苹果引发的革命
1687年之前，人类对"为什么东西会动"这个问题的回答是混乱的。
亚里士多德说：物体有"天然位置"，石头落地是因为它想回到自己的位置。行星转动是因为有神在推动。不同的现象有不同的解释，天上一套规则，地上另一套规则。
然后牛顿出现了，用三条定律和一个公式，把天上和地下统一了。
牛顿三定律，用最直白的话说：
第一定律（惯性）：
东西不会无缘无故改变运动状态。静止的东西会一直静止，运动的东西会一直匀速直线运动——除非有外力。
你坐车急刹，身体往前冲，就是惯性。你的身体"想"保持原来的速度，是刹车的力打断了它。
第二定律（F=ma）：
力等于质量乘以加速度。你推一个物体，质量越大越难推动，力越大加速越快。
这条定律的革命性在于：它是一个方程。 你只要知道一个物体受到多大的力，就能精确计算出它下一秒在哪里，后一秒在哪里，一年后在哪里。
第三定律（作用力与反作用力）：
你推墙，墙也在推你。力永远成对出现，方向相反，大小相等。
万有引力：把天和地缝合在一起
牛顿还发现，任何两个有质量的物体之间都存在引力，大小和质量成正比，和距离的平方成反比。
这一条的意义是毁天灭地的——
苹果落地和月球绕地球转，是同一种力在起作用。地球拉着苹果往下，也拉着月球往下。月球之所以没有掉下来，是因为它同时在横向运动，一直在"落"但一直在"跑"，就这样绕着圈。
天上和地下，第一次被同一套方程描述了。

第二幕：宇宙是一台钟表
牛顿定律一旦成立，一个极其深刻的推论就出现了。
F=ma 是一个因果方程。给定初始位置和速度，给定所有的力，你就能计算出任何时刻这个物体在哪里、速度是多少。
这对一个物体成立。对两个物体成立。对太阳系里所有行星成立——事实上，天文学家用牛顿方程预测哈雷彗星的轨道，精确到几十年后它会在哪一天回来，误差极小。
那么问题来了：如果对所有物体都成立呢？
1814年，法国数学家拉普拉斯把这个推论说得非常直白——
假设有一个智能存在，它在某一时刻知道宇宙中每一个粒子的位置和速度，并且掌握所有的力。那么对它来说，宇宙的过去和未来将没有任何不确定性，一切都像眼前一样清晰。
这个假想的存在后来被称为**"拉普拉斯妖"**。
它描述的世界观叫做决定论：
宇宙的每一个时刻，都由上一个时刻完全决定。过去决定现在，现在决定未来。整个宇宙的历史，从大爆炸到热寂，在第一秒就已经写好了。
宇宙是一台钟表。发条在大爆炸时上好，然后一格一格地走，每一格都精确无误，没有任何意外，没有任何"本来可以不这样"。
这套世界观的震撼之处
牛顿力学成立之后的100年里，这台"钟表宇宙"的图景深深影响了西方思想。
科学家和哲学家们开始认为：原则上，一切都是可以预测的。战争为什么爆发、瘟疫为什么蔓延、一个人为什么做了某个决定——如果你知道足够多的初始条件，全都可以用方程算出来。
这带来了巨大的知识乐观主义——人类只要足够努力，就能理解一切、预测一切。
但同时，它也带来了一个让人极度不安的推论。

第三幕：你有自由意志吗？
如果宇宙是决定论的，那你的大脑也是宇宙的一部分。
你的大脑由神经元组成，神经元由原子组成，原子遵循牛顿定律。如果拉普拉斯妖存在，它能算出你大脑里每一个粒子在下一秒的状态——也就是说，它能算出你下一秒会想什么、说什么、做什么。
你今天早上选择吃什么早饭，你此刻决定继续读下去，你未来会爱上谁、选择什么职业、在哪一天死去——
在决定论的宇宙里，这些全部在大爆炸的那一刻就已经注定了。
你以为你在"选择"，但那个选择本身，也只是粒子按照方程运动的结果。
自由意志，可能只是一个幻觉。
这是牛顿力学最深的哲学刺。它不只是一套计算工具，它是一种关于现实本质的主张——宇宙没有真正的偶然，没有真正的自由，只有因果链条的无尽延伸。

第四幕：钟表被打破了
故事到这里还没结束。因为20世纪发生了两件事，把这台钟表砸碎了。
第一件：量子力学
20世纪初，物理学家发现，在极小的尺度上，粒子的行为是根本不可预测的。
电子在被观测之前，没有确定的位置，只有一团概率云。你无法同时精确知道一个粒子的位置和速度——不是测量工具不够精确，而是自然界本来就不存在这个确定的值。这叫海森堡不确定性原理。
这直接杀死了拉普拉斯妖。它要求知道每个粒子的精确位置和速度——但这在物理上是不可能的，不是技术上不可能，是逻辑上不可能。
宇宙的底层，不是决定论的，而是概率性的。
第二件：混沌理论
即使不考虑量子力学，决定论也有另一个致命问题。
1960年代，气象学家洛伦兹发现：某些系统对初始条件极度敏感。一只蝴蝶在巴西扇动翅膀，可能引发德克萨斯州的一场龙卷风。
这就是蝴蝶效应。
在混沌系统里，初始条件哪怕有极其微小的误差，预测结果就会在短时间内完全失效。而现实世界中，初始条件的测量永远有误差。
所以即使宇宙在方程层面是决定论的，在实践层面也是根本不可预测的。
所以最终的图景是这样的：
牛顿建造了一台完美的钟表，运行了200年。
量子力学告诉我们，钟表的齿轮其实是随机跳动的。
混沌理论告诉我们，就算齿轮是确定的，我们也永远算不准。
决定论作为一种绝对真理倒下了。但它留下的问题——自由意志是否存在——至今没有答案，因为这已经不是物理学问题，而是哲学问题了。

检验时间
问题一（概念）
用你自己的比喻，解释一下什么是惯性。不要用课本的说法。
问题二（应用）
天气预报为什么永远不能做到100%准确？用今天学的内容解释。
问题三（思辨）
量子力学证明了宇宙底层是随机的，所以自由意志存在——你同意这个说法吗？

Q1：惯性是受到外力影响的条件下，立时反应出的不符合外力作用但符合本来该物体前进方向的一种现象
评：你说的"立时反应"暗示惯性是一种主动的、瞬间的响应——但惯性其实更像是一种被动的、持续的抵抗。更准确的图景是：物体根本不"想"做任何事，它只是懒得改变。外力来之前它怎样，它就想继续怎样。外力是打断这种"懒"的东西。惯性的本质是物体对改变的抵抗，是一种“质量带来的固执”，而不是一种反应。
迁：这在组织管理（HR）中非常常见：一个成熟的部门（质量大）即便面临市场改革（外力），也会由于惯性保持原有的运作习惯（前进方向）。这就是变革阻力的由来。

Q2：因为天气是由空气中的水分含量决定的，而依据混沌理论，只要其中某个水分子的位置发生了某些微小的变动，原本的天气轨迹就有可能被打乱，从而出现预报不准确的情况
评：你所说的正是混沌理论的精髓——对初始条件的极度敏感。但天气不准还有第二层原因，就是我们的测量本身有误差。混沌系统里，测量误差再小，经过足够多的迭代计算，最终结果也会完全偏离。所以是双重不可预测：系统本身敏感，测量本身也有限。

Q3：这只是证明了宇宙底层具有一定的随机性，但牛顿力学证明的庞大的逻辑框架我觉得是具有合理性的，所以我并不觉得自由意志是完全存在的，换个说法，我觉得历史轨道上不存在自由意志，而某些个体存在。我认为集体的走向是被决定的，个体在某些瞬间存在选择空间，普通人在日常微小瞬间里的选择——历史不在乎，但本人真实感受到了自由
评：宏观决定论：你认为历史轨迹有其必然性。这就像是物理学中的 F = ma，大环境的力决定了群体的加速度。微观选择感：你强调了“本人真实感受到自由”的重要性。这非常有力量——即便宇宙是一台钟表，我们在齿轮缝隙里产生的那一点点“想要往左还是往右”的念头，就是生命对抗冷冰冰方程的唯一证据。
你实际上在说：自由意志不需要改变历史才算数，它只需要被感受到。
这在哲学里有一个名字，叫相容论——决定论和自由意志不是非此即彼的，它们可以同时为真。宇宙的因果链条是真实的，但人在那个链条里感受到的选择感，也是真实的，而且那个感受本身就是自由意志的全部含义。
但我要给你一个真正的追问：
你说"本人真实感受到了自由"——
如果这个"感受"本身，也是大脑神经元按照物理规律放电的结果呢？
也就是说：你感受到自由，但这个感受是被决定的。一个被决定的"自由感"，还算自由吗？</div>
                </div>
                <div class="note-editor" id="note-editor-2">
                  <textarea class="note-textarea" id="note-ta-2" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……">经典力学与决定论    Q1-物理学/哲学    2026-03-31
1. 核心逻辑 (The "Why")：
如果世界遵循固定的因果方程（如 F = ma），那么只要掌握所有初始数据，未来就是可以被精确计算的。
2. 降维解释 (ELI5)：
宇宙是一台巨大的、在大爆炸时就上好了发条的精密钟表，每一个齿轮的转动都是注定的。
3. 跨界迁移 (Cross-Domain Bridge)：
管理学：试图通过模型和数据预测一切，是典型的决定论思维；
历史学：大趋势（生产力发展）可能是决定的，但英雄人物的偶然选择是混沌的种子。
4. 衍生思考 (Actionable Insight)：
接受宏观上的“不可抗力”，但在微观瞬间保持“选择感”。即便自由意志可能是幻觉，这种“主观能动性的体验”也是对抗熵增、维持生命有序的唯一动力。

牛顿力学与决定论：宇宙是一台钟表吗？
第一幕：一个苹果引发的革命
1687年之前，人类对"为什么东西会动"这个问题的回答是混乱的。
亚里士多德说：物体有"天然位置"，石头落地是因为它想回到自己的位置。行星转动是因为有神在推动。不同的现象有不同的解释，天上一套规则，地上另一套规则。
然后牛顿出现了，用三条定律和一个公式，把天上和地下统一了。
牛顿三定律，用最直白的话说：
第一定律（惯性）：
东西不会无缘无故改变运动状态。静止的东西会一直静止，运动的东西会一直匀速直线运动——除非有外力。
你坐车急刹，身体往前冲，就是惯性。你的身体"想"保持原来的速度，是刹车的力打断了它。
第二定律（F=ma）：
力等于质量乘以加速度。你推一个物体，质量越大越难推动，力越大加速越快。
这条定律的革命性在于：它是一个方程。 你只要知道一个物体受到多大的力，就能精确计算出它下一秒在哪里，后一秒在哪里，一年后在哪里。
第三定律（作用力与反作用力）：
你推墙，墙也在推你。力永远成对出现，方向相反，大小相等。
万有引力：把天和地缝合在一起
牛顿还发现，任何两个有质量的物体之间都存在引力，大小和质量成正比，和距离的平方成反比。
这一条的意义是毁天灭地的——
苹果落地和月球绕地球转，是同一种力在起作用。地球拉着苹果往下，也拉着月球往下。月球之所以没有掉下来，是因为它同时在横向运动，一直在"落"但一直在"跑"，就这样绕着圈。
天上和地下，第一次被同一套方程描述了。

第二幕：宇宙是一台钟表
牛顿定律一旦成立，一个极其深刻的推论就出现了。
F=ma 是一个因果方程。给定初始位置和速度，给定所有的力，你就能计算出任何时刻这个物体在哪里、速度是多少。
这对一个物体成立。对两个物体成立。对太阳系里所有行星成立——事实上，天文学家用牛顿方程预测哈雷彗星的轨道，精确到几十年后它会在哪一天回来，误差极小。
那么问题来了：如果对所有物体都成立呢？
1814年，法国数学家拉普拉斯把这个推论说得非常直白——
假设有一个智能存在，它在某一时刻知道宇宙中每一个粒子的位置和速度，并且掌握所有的力。那么对它来说，宇宙的过去和未来将没有任何不确定性，一切都像眼前一样清晰。
这个假想的存在后来被称为**"拉普拉斯妖"**。
它描述的世界观叫做决定论：
宇宙的每一个时刻，都由上一个时刻完全决定。过去决定现在，现在决定未来。整个宇宙的历史，从大爆炸到热寂，在第一秒就已经写好了。
宇宙是一台钟表。发条在大爆炸时上好，然后一格一格地走，每一格都精确无误，没有任何意外，没有任何"本来可以不这样"。
这套世界观的震撼之处
牛顿力学成立之后的100年里，这台"钟表宇宙"的图景深深影响了西方思想。
科学家和哲学家们开始认为：原则上，一切都是可以预测的。战争为什么爆发、瘟疫为什么蔓延、一个人为什么做了某个决定——如果你知道足够多的初始条件，全都可以用方程算出来。
这带来了巨大的知识乐观主义——人类只要足够努力，就能理解一切、预测一切。
但同时，它也带来了一个让人极度不安的推论。

第三幕：你有自由意志吗？
如果宇宙是决定论的，那你的大脑也是宇宙的一部分。
你的大脑由神经元组成，神经元由原子组成，原子遵循牛顿定律。如果拉普拉斯妖存在，它能算出你大脑里每一个粒子在下一秒的状态——也就是说，它能算出你下一秒会想什么、说什么、做什么。
你今天早上选择吃什么早饭，你此刻决定继续读下去，你未来会爱上谁、选择什么职业、在哪一天死去——
在决定论的宇宙里，这些全部在大爆炸的那一刻就已经注定了。
你以为你在"选择"，但那个选择本身，也只是粒子按照方程运动的结果。
自由意志，可能只是一个幻觉。
这是牛顿力学最深的哲学刺。它不只是一套计算工具，它是一种关于现实本质的主张——宇宙没有真正的偶然，没有真正的自由，只有因果链条的无尽延伸。

第四幕：钟表被打破了
故事到这里还没结束。因为20世纪发生了两件事，把这台钟表砸碎了。
第一件：量子力学
20世纪初，物理学家发现，在极小的尺度上，粒子的行为是根本不可预测的。
电子在被观测之前，没有确定的位置，只有一团概率云。你无法同时精确知道一个粒子的位置和速度——不是测量工具不够精确，而是自然界本来就不存在这个确定的值。这叫海森堡不确定性原理。
这直接杀死了拉普拉斯妖。它要求知道每个粒子的精确位置和速度——但这在物理上是不可能的，不是技术上不可能，是逻辑上不可能。
宇宙的底层，不是决定论的，而是概率性的。
第二件：混沌理论
即使不考虑量子力学，决定论也有另一个致命问题。
1960年代，气象学家洛伦兹发现：某些系统对初始条件极度敏感。一只蝴蝶在巴西扇动翅膀，可能引发德克萨斯州的一场龙卷风。
这就是蝴蝶效应。
在混沌系统里，初始条件哪怕有极其微小的误差，预测结果就会在短时间内完全失效。而现实世界中，初始条件的测量永远有误差。
所以即使宇宙在方程层面是决定论的，在实践层面也是根本不可预测的。
所以最终的图景是这样的：
牛顿建造了一台完美的钟表，运行了200年。
量子力学告诉我们，钟表的齿轮其实是随机跳动的。
混沌理论告诉我们，就算齿轮是确定的，我们也永远算不准。
决定论作为一种绝对真理倒下了。但它留下的问题——自由意志是否存在——至今没有答案，因为这已经不是物理学问题，而是哲学问题了。

检验时间
问题一（概念）
用你自己的比喻，解释一下什么是惯性。不要用课本的说法。
问题二（应用）
天气预报为什么永远不能做到100%准确？用今天学的内容解释。
问题三（思辨）
量子力学证明了宇宙底层是随机的，所以自由意志存在——你同意这个说法吗？

Q1：惯性是受到外力影响的条件下，立时反应出的不符合外力作用但符合本来该物体前进方向的一种现象
评：你说的"立时反应"暗示惯性是一种主动的、瞬间的响应——但惯性其实更像是一种被动的、持续的抵抗。更准确的图景是：物体根本不"想"做任何事，它只是懒得改变。外力来之前它怎样，它就想继续怎样。外力是打断这种"懒"的东西。惯性的本质是物体对改变的抵抗，是一种“质量带来的固执”，而不是一种反应。
迁：这在组织管理（HR）中非常常见：一个成熟的部门（质量大）即便面临市场改革（外力），也会由于惯性保持原有的运作习惯（前进方向）。这就是变革阻力的由来。

Q2：因为天气是由空气中的水分含量决定的，而依据混沌理论，只要其中某个水分子的位置发生了某些微小的变动，原本的天气轨迹就有可能被打乱，从而出现预报不准确的情况
评：你所说的正是混沌理论的精髓——对初始条件的极度敏感。但天气不准还有第二层原因，就是我们的测量本身有误差。混沌系统里，测量误差再小，经过足够多的迭代计算，最终结果也会完全偏离。所以是双重不可预测：系统本身敏感，测量本身也有限。

Q3：这只是证明了宇宙底层具有一定的随机性，但牛顿力学证明的庞大的逻辑框架我觉得是具有合理性的，所以我并不觉得自由意志是完全存在的，换个说法，我觉得历史轨道上不存在自由意志，而某些个体存在。我认为集体的走向是被决定的，个体在某些瞬间存在选择空间，普通人在日常微小瞬间里的选择——历史不在乎，但本人真实感受到了自由
评：宏观决定论：你认为历史轨迹有其必然性。这就像是物理学中的 F = ma，大环境的力决定了群体的加速度。微观选择感：你强调了“本人真实感受到自由”的重要性。这非常有力量——即便宇宙是一台钟表，我们在齿轮缝隙里产生的那一点点“想要往左还是往右”的念头，就是生命对抗冷冰冰方程的唯一证据。
你实际上在说：自由意志不需要改变历史才算数，它只需要被感受到。
这在哲学里有一个名字，叫相容论——决定论和自由意志不是非此即彼的，它们可以同时为真。宇宙的因果链条是真实的，但人在那个链条里感受到的选择感，也是真实的，而且那个感受本身就是自由意志的全部含义。
但我要给你一个真正的追问：
你说"本人真实感受到了自由"——
如果这个"感受"本身，也是大脑神经元按照物理规律放电的结果呢？
也就是说：你感受到自由，但这个感受是被决定的。一个被决定的"自由感"，还算自由吗？</textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(2)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(2)">删除</button>
                    <span class="note-timestamp" id="note-ts-2">2026/3/31 22:22 已保存</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="3" data-tags="物理学,量子力学,宇宙起源">
            <div class="day-num " id="daynum-3">D3</div>
            <div class="day-content">
              <div class="day-topic"><em>物理学</em>量子力学的概率世界</div>
              <div class="day-desc">观察者如何改变结果？理解微观层面的「不确定性」和叠加态，打破绝对的客观真实。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('物理学',this);">物理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('量子力学',this);">量子力学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙起源',this);">宇宙起源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-3" onclick="toggleNote(3)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(3)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-3"></div>
                <div class="note-display-wrap " id="note-display-wrap-3">
                  <div class="note-display-header" onclick="toggleNoteDisplay(3)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-3"></div>
                </div>
                <div class="note-editor" id="note-editor-3">
                  <textarea class="note-textarea" id="note-ta-3" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(3)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(3)">删除</button>
                    <span class="note-timestamp" id="note-ts-3"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="4" data-tags="物理学,量子力学">
            <div class="day-num " id="daynum-4">D4</div>
            <div class="day-content">
              <div class="day-topic"><em>物理学</em>相对论：时空的弹性</div>
              <div class="day-desc">时间和空间不是绝对的容器，而是受质量扭曲的网。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('物理学',this);">物理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('量子力学',this);">量子力学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-4" onclick="toggleNote(4)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(4)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-4"></div>
                <div class="note-display-wrap " id="note-display-wrap-4">
                  <div class="note-display-header" onclick="toggleNoteDisplay(4)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-4"></div>
                </div>
                <div class="note-editor" id="note-editor-4">
                  <textarea class="note-textarea" id="note-ta-4" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(4)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(4)">删除</button>
                    <span class="note-timestamp" id="note-ts-4"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="5" data-tags="热力学,相对论,时空">
            <div class="day-num " id="daynum-5">D5</div>
            <div class="day-content">
              <div class="day-topic"><em>热力学</em>能量守恒与转化</div>
              <div class="day-desc">能量不会凭空产生，只能转移。识别现实中的「永动机陷阱」和不可避免的系统损耗。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('热力学',this);">热力学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('相对论',this);">相对论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('时空',this);">时空</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-5" onclick="toggleNote(5)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(5)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-5"></div>
                <div class="note-display-wrap " id="note-display-wrap-5">
                  <div class="note-display-header" onclick="toggleNoteDisplay(5)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-5"></div>
                </div>
                <div class="note-editor" id="note-editor-5">
                  <textarea class="note-textarea" id="note-ta-5" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(5)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(5)">删除</button>
                    <span class="note-timestamp" id="note-ts-5"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="6" data-tags="物理学,宇宙起源">
            <div class="day-num " id="daynum-6">D6</div>
            <div class="day-content">
              <div class="day-topic"><em>物理学</em>物质的微观结构</div>
              <div class="day-desc">从原子到夸克，世界如何从几种最简单的基本粒子「堆叠」出无限复杂的可能性。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('物理学',this);">物理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙起源',this);">宇宙起源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-6" onclick="toggleNote(6)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(6)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-6"></div>
                <div class="note-display-wrap " id="note-display-wrap-6">
                  <div class="note-display-header" onclick="toggleNoteDisplay(6)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-6"></div>
                </div>
                <div class="note-editor" id="note-editor-6">
                  <textarea class="note-textarea" id="note-ta-6" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(6)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(6)">删除</button>
                    <span class="note-timestamp" id="note-ts-6"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="7" data-tags="交叉学科,复盘,演化论">
            <div class="day-num " id="daynum-7">D7</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：物理定律迁移</div>
              <div class="day-desc">用这一周的物理词汇，描述你研究的系统中哪些部分在模拟这些物理法则。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-7" onclick="toggleNote(7)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(7)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-7"></div>
                <div class="note-display-wrap " id="note-display-wrap-7">
                  <div class="note-display-header" onclick="toggleNoteDisplay(7)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-7"></div>
                </div>
                <div class="note-editor" id="note-editor-7">
                  <textarea class="note-textarea" id="note-ta-7" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(7)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(7)">删除</button>
                    <span class="note-timestamp" id="note-ts-7"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W2 · 宇宙学与化学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="8" data-tags="宇宙学,演化论,基因">
            <div class="day-num " id="daynum-8">D8</div>
            <div class="day-content">
              <div class="day-topic"><em>宇宙学</em>大爆炸与宇宙膨胀</div>
              <div class="day-desc">理解时间与空间的起点，万物皆始于一个极度低熵的奇点。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙学',this);">宇宙学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('基因',this);">基因</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-8" onclick="toggleNote(8)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(8)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-8"></div>
                <div class="note-display-wrap " id="note-display-wrap-8">
                  <div class="note-display-header" onclick="toggleNoteDisplay(8)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-8"></div>
                </div>
                <div class="note-editor" id="note-editor-8">
                  <textarea class="note-textarea" id="note-ta-8" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(8)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(8)">删除</button>
                    <span class="note-timestamp" id="note-ts-8"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="9" data-tags="宇宙学,演化论,基因">
            <div class="day-num " id="daynum-9">D9</div>
            <div class="day-content">
              <div class="day-topic"><em>宇宙学</em>恒星演化：宇宙的熔炉</div>
              <div class="day-desc">我们都是星尘。理解恒星如何通过核聚变产生构建生命的重元素。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙学',this);">宇宙学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('基因',this);">基因</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-9" onclick="toggleNote(9)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(9)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-9"></div>
                <div class="note-display-wrap " id="note-display-wrap-9">
                  <div class="note-display-header" onclick="toggleNoteDisplay(9)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-9"></div>
                </div>
                <div class="note-editor" id="note-editor-9">
                  <textarea class="note-textarea" id="note-ta-9" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(9)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(9)">删除</button>
                    <span class="note-timestamp" id="note-ts-9"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="10" data-tags="化学,演化论,复杂系统">
            <div class="day-num " id="daynum-10">D10</div>
            <div class="day-content">
              <div class="day-topic"><em>化学</em>元素周期表：原子的秩序</div>
              <div class="day-desc">看透物质的内在逻辑：原子最外层电子的排布如何决定物质的「性格」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('化学',this);">化学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-10" onclick="toggleNote(10)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(10)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-10"></div>
                <div class="note-display-wrap " id="note-display-wrap-10">
                  <div class="note-display-header" onclick="toggleNoteDisplay(10)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-10"></div>
                </div>
                <div class="note-editor" id="note-editor-10">
                  <textarea class="note-textarea" id="note-ta-10" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(10)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(10)">删除</button>
                    <span class="note-timestamp" id="note-ts-10"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="11" data-tags="化学,博弈论,博弈">
            <div class="day-num " id="daynum-11">D11</div>
            <div class="day-content">
              <div class="day-topic"><em>化学</em>化学键：结合的底层动力</div>
              <div class="day-desc">物质为什么会结合？寻找更低、更稳定的能量状态是万物连接的终极驱动力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('化学',this);">化学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-11" onclick="toggleNote(11)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(11)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-11"></div>
                <div class="note-display-wrap " id="note-display-wrap-11">
                  <div class="note-display-header" onclick="toggleNoteDisplay(11)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-11"></div>
                </div>
                <div class="note-editor" id="note-editor-11">
                  <textarea class="note-textarea" id="note-ta-11" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(11)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(11)">删除</button>
                    <span class="note-timestamp" id="note-ts-11"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="12" data-tags="化学,博弈论,博弈">
            <div class="day-num " id="daynum-12">D12</div>
            <div class="day-content">
              <div class="day-topic"><em>化学</em>碳基密码：生命的乐高</div>
              <div class="day-desc">为什么生命选择了碳？理解碳原子的四价键结构是构建复杂系统的「数学最优解」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('化学',this);">化学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-12" onclick="toggleNote(12)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(12)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-12"></div>
                <div class="note-display-wrap " id="note-display-wrap-12">
                  <div class="note-display-header" onclick="toggleNoteDisplay(12)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-12"></div>
                </div>
                <div class="note-editor" id="note-editor-12">
                  <textarea class="note-textarea" id="note-ta-12" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(12)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(12)">删除</button>
                    <span class="note-timestamp" id="note-ts-12"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="13" data-tags="生物学,博弈论,博弈">
            <div class="day-num " id="daynum-13">D13</div>
            <div class="day-content">
              <div class="day-topic"><em>生物学</em>DNA：生命的代码本</div>
              <div class="day-desc">破译四进制的基因编码系统。生命的本质是一套极度精密的信息存储与复制程序。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生物学',this);">生物学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-13" onclick="toggleNote(13)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(13)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-13"></div>
                <div class="note-display-wrap " id="note-display-wrap-13">
                  <div class="note-display-header" onclick="toggleNoteDisplay(13)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-13"></div>
                </div>
                <div class="note-editor" id="note-editor-13">
                  <textarea class="note-textarea" id="note-ta-13" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(13)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(13)">删除</button>
                    <span class="note-timestamp" id="note-ts-13"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="14" data-tags="交叉学科,复杂系统">
            <div class="day-num " id="daynum-14">D14</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：从星尘到代码</div>
              <div class="day-desc">回顾物质如何从无机的元素，一步步跨越到具有自我复制能力的「有机程序」。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-14" onclick="toggleNote(14)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(14)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-14"></div>
                <div class="note-display-wrap " id="note-display-wrap-14">
                  <div class="note-display-header" onclick="toggleNoteDisplay(14)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-14"></div>
                </div>
                <div class="note-editor" id="note-editor-14">
                  <textarea class="note-textarea" id="note-ta-14" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(14)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(14)">删除</button>
                    <span class="note-timestamp" id="note-ts-14"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W3 · 生物学与演化论</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="15" data-tags="细胞学,复杂系统">
            <div class="day-num " id="daynum-15">D15</div>
            <div class="day-content">
              <div class="day-topic"><em>细胞学</em>细胞：精密的微观工厂</div>
              <div class="day-desc">将细胞视作高度分工的组织，理解内部SOP是如何高效运转的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('细胞学',this);">细胞学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-15" onclick="toggleNote(15)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(15)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-15"></div>
                <div class="note-display-wrap " id="note-display-wrap-15">
                  <div class="note-display-header" onclick="toggleNoteDisplay(15)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-15"></div>
                </div>
                <div class="note-editor" id="note-editor-15">
                  <textarea class="note-textarea" id="note-ta-15" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(15)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(15)">删除</button>
                    <span class="note-timestamp" id="note-ts-15"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="16" data-tags="生物学,认知偏差,心理学">
            <div class="day-num " id="daynum-16">D16</div>
            <div class="day-content">
              <div class="day-topic"><em>生物学</em>ATP：生命的通用货币</div>
              <div class="day-desc">理解所有生命体内的「能量结算」系统。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生物学',this);">生物学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-16" onclick="toggleNote(16)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(16)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-16"></div>
                <div class="note-display-wrap " id="note-display-wrap-16">
                  <div class="note-display-header" onclick="toggleNoteDisplay(16)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-16"></div>
                </div>
                <div class="note-editor" id="note-editor-16">
                  <textarea class="note-textarea" id="note-ta-16" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(16)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(16)">删除</button>
                    <span class="note-timestamp" id="note-ts-16"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="17" data-tags="演化论,认知偏差,心理学">
            <div class="day-num " id="daynum-17">D17</div>
            <div class="day-content">
              <div class="day-topic"><em>演化论</em>物竞天择：无目的的演化</div>
              <div class="day-desc">打破「进化是为了变得更完美」的迷思。环境是唯一的考官，适者生存非强者生存。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-17" onclick="toggleNote(17)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(17)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-17"></div>
                <div class="note-display-wrap " id="note-display-wrap-17">
                  <div class="note-display-header" onclick="toggleNoteDisplay(17)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-17"></div>
                </div>
                <div class="note-editor" id="note-editor-17">
                  <textarea class="note-textarea" id="note-ta-17" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(17)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(17)">删除</button>
                    <span class="note-timestamp" id="note-ts-17"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="18" data-tags="演化论,认知偏差,心理学">
            <div class="day-num " id="daynum-18">D18</div>
            <div class="day-content">
              <div class="day-topic"><em>演化论</em>基因突变：创新的Bug</div>
              <div class="day-desc">复制过程中的错误，是系统产生多样性的唯一来源。「不完美」才是系统不被淘汰的关键。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-18" onclick="toggleNote(18)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(18)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-18"></div>
                <div class="note-display-wrap " id="note-display-wrap-18">
                  <div class="note-display-header" onclick="toggleNoteDisplay(18)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-18"></div>
                </div>
                <div class="note-editor" id="note-editor-18">
                  <textarea class="note-textarea" id="note-ta-18" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(18)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(18)">删除</button>
                    <span class="note-timestamp" id="note-ts-18"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="19" data-tags="演化论,意识,心理学">
            <div class="day-num " id="daynum-19">D19</div>
            <div class="day-content">
              <div class="day-topic"><em>演化论</em>自私的基因</div>
              <div class="day-desc">个体只是基因生存和传递的「运载机器」，生物的所有利他与博弈皆受此底层逻辑驱动。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-19" onclick="toggleNote(19)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(19)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-19"></div>
                <div class="note-display-wrap " id="note-display-wrap-19">
                  <div class="note-display-header" onclick="toggleNoteDisplay(19)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-19"></div>
                </div>
                <div class="note-editor" id="note-editor-19">
                  <textarea class="note-textarea" id="note-ta-19" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(19)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(19)">删除</button>
                    <span class="note-timestamp" id="note-ts-19"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="20" data-tags="生理学,意识,心理学">
            <div class="day-num " id="daynum-20">D20</div>
            <div class="day-content">
              <div class="day-topic"><em>生理学</em>免疫系统：边界的防御</div>
              <div class="day-desc">系统如何精确区分「自我」与「非我」，并在遭受外部攻击时启动记忆与反击机制。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生理学',this);">生理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-20" onclick="toggleNote(20)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(20)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-20"></div>
                <div class="note-display-wrap " id="note-display-wrap-20">
                  <div class="note-display-header" onclick="toggleNoteDisplay(20)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-20"></div>
                </div>
                <div class="note-editor" id="note-editor-20">
                  <textarea class="note-textarea" id="note-ta-20" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(20)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(20)">删除</button>
                    <span class="note-timestamp" id="note-ts-20"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="21" data-tags="交叉学科,意识,神经科学">
            <div class="day-num " id="daynum-21">D21</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：演化算法的应用</div>
              <div class="day-desc">将「基因、突变、选择」的演化思维套用在AI工具的迭代与淘汰竞争中。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-21" onclick="toggleNote(21)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(21)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-21"></div>
                <div class="note-display-wrap " id="note-display-wrap-21">
                  <div class="note-display-header" onclick="toggleNoteDisplay(21)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-21"></div>
                </div>
                <div class="note-editor" id="note-editor-21">
                  <textarea class="note-textarea" id="note-ta-21" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(21)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(21)">删除</button>
                    <span class="note-timestamp" id="note-ts-21"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W4 · 脑科学与生态学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="22" data-tags="脑科学,神经科学,认知">
            <div class="day-num " id="daynum-22">D22</div>
            <div class="day-content">
              <div class="day-topic"><em>脑科学</em>神经元：意识的物理学</div>
              <div class="day-desc">所有的思想、意志和情感，本质上都只是神经突触间微弱的物理电信号放电。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('脑科学',this);">脑科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-22" onclick="toggleNote(22)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(22)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-22"></div>
                <div class="note-display-wrap " id="note-display-wrap-22">
                  <div class="note-display-header" onclick="toggleNoteDisplay(22)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-22"></div>
                </div>
                <div class="note-editor" id="note-editor-22">
                  <textarea class="note-textarea" id="note-ta-22" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(22)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(22)">删除</button>
                    <span class="note-timestamp" id="note-ts-22"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="23" data-tags="脑科学,认知,神经科学">
            <div class="day-num " id="daynum-23">D23</div>
            <div class="day-content">
              <div class="day-topic"><em>脑科学</em>视觉重构：大脑的渲染</div>
              <div class="day-desc">大脑不是照相机，而是「渲染引擎」。你看到的世界是大脑在暗箱中推测出来的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('脑科学',this);">脑科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-23" onclick="toggleNote(23)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(23)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-23"></div>
                <div class="note-display-wrap " id="note-display-wrap-23">
                  <div class="note-display-header" onclick="toggleNoteDisplay(23)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-23"></div>
                </div>
                <div class="note-editor" id="note-editor-23">
                  <textarea class="note-textarea" id="note-ta-23" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(23)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(23)">删除</button>
                    <span class="note-timestamp" id="note-ts-23"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="24" data-tags="心理学,心流">
            <div class="day-num " id="daynum-24">D24</div>
            <div class="day-content">
              <div class="day-topic"><em>心理学</em>多巴胺回路：动机代码</div>
              <div class="day-desc">揭开行为的底层驱动力：大脑在预测奖赏时分泌的化学物质如何控制我们的习惯。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心流',this);">心流</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-24" onclick="toggleNote(24)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(24)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-24"></div>
                <div class="note-display-wrap " id="note-display-wrap-24">
                  <div class="note-display-header" onclick="toggleNoteDisplay(24)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-24"></div>
                </div>
                <div class="note-editor" id="note-editor-24">
                  <textarea class="note-textarea" id="note-ta-24" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(24)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(24)">删除</button>
                    <span class="note-timestamp" id="note-ts-24"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="25" data-tags="心理学,认知">
            <div class="day-num " id="daynum-25">D25</div>
            <div class="day-content">
              <div class="day-topic"><em>心理学</em>情绪的价值：避险算法</div>
              <div class="day-desc">负面情绪不是缺陷，而是漫长演化写进基因里的高效避险快捷键。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-25" onclick="toggleNote(25)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(25)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-25"></div>
                <div class="note-display-wrap " id="note-display-wrap-25">
                  <div class="note-display-header" onclick="toggleNoteDisplay(25)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-25"></div>
                </div>
                <div class="note-editor" id="note-editor-25">
                  <textarea class="note-textarea" id="note-ta-25" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(25)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(25)">删除</button>
                    <span class="note-timestamp" id="note-ts-25"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="26" data-tags="生态学,认知偏差,决策">
            <div class="day-num " id="daynum-26">D26</div>
            <div class="day-content">
              <div class="day-topic"><em>生态学</em>生态位与资源网络</div>
              <div class="day-desc">任何系统都是复杂的资源分配网络，「不要在同一个生态位上死磕」的生存智慧。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生态学',this);">生态学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-26" onclick="toggleNote(26)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(26)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-26"></div>
                <div class="note-display-wrap " id="note-display-wrap-26">
                  <div class="note-display-header" onclick="toggleNoteDisplay(26)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-26"></div>
                </div>
                <div class="note-editor" id="note-editor-26">
                  <textarea class="note-textarea" id="note-ta-26" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(26)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(26)">删除</button>
                    <span class="note-timestamp" id="note-ts-26"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="27" data-tags="生态学,复盘">
            <div class="day-num " id="daynum-27">D27</div>
            <div class="day-content">
              <div class="day-topic"><em>生态学</em>能量递减定律</div>
              <div class="day-desc">能量每向上级传递就损耗极大，解释了为什么顶级掠食者注定稀少，层级过多的组织为何低效。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生态学',this);">生态学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-27" onclick="toggleNote(27)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(27)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-27"></div>
                <div class="note-display-wrap " id="note-display-wrap-27">
                  <div class="note-display-header" onclick="toggleNoteDisplay(27)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-27"></div>
                </div>
                <div class="note-editor" id="note-editor-27">
                  <textarea class="note-textarea" id="note-ta-27" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(27)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(27)">删除</button>
                    <span class="note-timestamp" id="note-ts-27"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="28" data-tags="交叉学科,系统论,复杂系统">
            <div class="day-num " id="daynum-28">D28</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：感知与复杂网络</div>
              <div class="day-desc">总结人类如何通过极其有限的感官，在复杂的能量网络中寻找生存策略。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-28" onclick="toggleNote(28)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(28)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-28"></div>
                <div class="note-display-wrap " id="note-display-wrap-28">
                  <div class="note-display-header" onclick="toggleNoteDisplay(28)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-28"></div>
                </div>
                <div class="note-editor" id="note-editor-28">
                  <textarea class="note-textarea" id="note-ta-28" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(28)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(28)">删除</button>
                    <span class="note-timestamp" id="note-ts-28"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W5 · 涌现与大复盘</span>
            <span class="week-days-count">2 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="29" data-tags="系统论,复杂系统,熵">
            <div class="day-num " id="daynum-29">D29</div>
            <div class="day-content">
              <div class="day-topic"><em>系统论</em>涌现：量变到质变的魔法</div>
              <div class="day-desc">当大量简单的个体遵循简单规则互动时，如何自发产生出单个个体完全不具备的复杂高级特征。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-29" onclick="toggleNote(29)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(29)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-29"></div>
                <div class="note-display-wrap " id="note-display-wrap-29">
                  <div class="note-display-header" onclick="toggleNoteDisplay(29)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-29"></div>
                </div>
                <div class="note-editor" id="note-editor-29">
                  <textarea class="note-textarea" id="note-ta-29" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(29)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(29)">删除</button>
                    <span class="note-timestamp" id="note-ts-29"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="30" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-30">D30</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第一月复盘：搭建自然科学底座</div>
              <div class="day-desc">串联前29天的逻辑卡片：如果宇宙是一台机器，生命是如何在这台机器里钻漏洞生存的？</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-30" onclick="toggleNote(30)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(30)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-30"></div>
                <div class="note-display-wrap " id="note-display-wrap-30">
                  <div class="note-display-header" onclick="toggleNoteDisplay(30)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-30"></div>
                </div>
                <div class="note-editor" id="note-editor-30">
                  <textarea class="note-textarea" id="note-ta-30" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(30)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(30)">删除</button>
                    <span class="note-timestamp" id="note-ts-30"></span>
                  </div>
                </div>
              <div class="monthly-summary" style="margin-top: 8px; padding: 8px 10px; border: 1px dashed var(--accent1)44; border-radius: 6px; font-size: 11px; color: var(--text2); line-height: 1.7;"><div style="font-size:10px;color:var(--accent1);font-family:'Cinzel',serif;margin-bottom:4px;letter-spacing:1px">
      ◈ 本月感悟速览（2 条）</div><div style="margin-bottom:3px">· Day 1·熵增定律：熵增定律    Q1-物理学/热力学    2026-03-29
1. 核心逻辑 (The "Wh…</div><div style="margin-bottom:3px">· Day 2·牛顿力学与决定论：经典力学与决定论    Q1-物理学/哲学    2026-03-31
1. 核心逻辑 (…</div></div></div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-2">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#5a8fc8"></div>
        <div class="module-icon" style="background:#5a8fc818; color:#5a8fc8">🧠</div>
        <div class="module-meta">
          <div class="module-num">MODULE 02</div>
          <div class="module-title" style="color:#5a8fc8">认知与人文精神
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">系统的「操作系统」</span>
          </div>
          <div class="module-days" style="color:#5a8fc877">逻辑学·哲学·东方哲学·心理学·宏观历史</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#5a8fc844;color:#5a8fc899">Day 31–60</span>
          <span class="module-chevron" style="color:#5a8fc888">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W6 · 逻辑学与认知科学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="31" data-tags="逻辑学,经济学,市场">
            <div class="day-num " id="daynum-31">D31</div>
            <div class="day-content">
              <div class="day-topic"><em>逻辑学</em>概念与定义界定</div>
              <div class="day-desc">清晰的边界是思考的前提。大多数争论并非观点不合，而是对同一个词的定义不同。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑学',this);">逻辑学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-31" onclick="toggleNote(31)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(31)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-31"></div>
                <div class="note-display-wrap " id="note-display-wrap-31">
                  <div class="note-display-header" onclick="toggleNoteDisplay(31)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-31"></div>
                </div>
                <div class="note-editor" id="note-editor-31">
                  <textarea class="note-textarea" id="note-ta-31" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(31)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(31)">删除</button>
                    <span class="note-timestamp" id="note-ts-31"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="32" data-tags="逻辑学,经济学,市场">
            <div class="day-num " id="daynum-32">D32</div>
            <div class="day-content">
              <div class="day-topic"><em>逻辑学</em>演绎推理与三段论</div>
              <div class="day-desc">从普遍规律推导具体结论的必然性。建立不可被驳倒的硬逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑学',this);">逻辑学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-32" onclick="toggleNote(32)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(32)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-32"></div>
                <div class="note-display-wrap " id="note-display-wrap-32">
                  <div class="note-display-header" onclick="toggleNoteDisplay(32)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-32"></div>
                </div>
                <div class="note-editor" id="note-editor-32">
                  <textarea class="note-textarea" id="note-ta-32" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(32)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(32)">删除</button>
                    <span class="note-timestamp" id="note-ts-32"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="33" data-tags="逻辑学,经济学,博弈">
            <div class="day-num " id="daynum-33">D33</div>
            <div class="day-content">
              <div class="day-topic"><em>逻辑学</em>归纳推理与黑天鹅</div>
              <div class="day-desc">从经验中总结规律的危险性。「过去一直这样」无法推导出「未来一定这样」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑学',this);">逻辑学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-33" onclick="toggleNote(33)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(33)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-33"></div>
                <div class="note-display-wrap " id="note-display-wrap-33">
                  <div class="note-display-header" onclick="toggleNoteDisplay(33)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-33"></div>
                </div>
                <div class="note-editor" id="note-editor-33">
                  <textarea class="note-textarea" id="note-ta-33" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(33)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(33)">删除</button>
                    <span class="note-timestamp" id="note-ts-33"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="34" data-tags="逻辑学,经济学,市场">
            <div class="day-num " id="daynum-34">D34</div>
            <div class="day-content">
              <div class="day-topic"><em>逻辑学</em>常见逻辑谬误</div>
              <div class="day-desc">识别滑坡谬误、稻草人谬误、诉诸人身等逻辑漏洞。给大脑「杀毒」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑学',this);">逻辑学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-34" onclick="toggleNote(34)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(34)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-34"></div>
                <div class="note-display-wrap " id="note-display-wrap-34">
                  <div class="note-display-header" onclick="toggleNoteDisplay(34)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-34"></div>
                </div>
                <div class="note-editor" id="note-editor-34">
                  <textarea class="note-textarea" id="note-ta-34" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(34)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(34)">删除</button>
                    <span class="note-timestamp" id="note-ts-34"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="35" data-tags="认知科学,经济学,复杂系统">
            <div class="day-num " id="daynum-35">D35</div>
            <div class="day-content">
              <div class="day-topic"><em>认知科学</em>第一性原理思维</div>
              <div class="day-desc">将事物拆解到最基础、不可证伪的物理或数学要素，然后从头重构。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知科学',this);">认知科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-35" onclick="toggleNote(35)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(35)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-35"></div>
                <div class="note-display-wrap " id="note-display-wrap-35">
                  <div class="note-display-header" onclick="toggleNoteDisplay(35)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-35"></div>
                </div>
                <div class="note-editor" id="note-editor-35">
                  <textarea class="note-textarea" id="note-ta-35" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(35)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(35)">删除</button>
                    <span class="note-timestamp" id="note-ts-35"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="36" data-tags="认知科学,经济学">
            <div class="day-num " id="daynum-36">D36</div>
            <div class="day-content">
              <div class="day-topic"><em>认知科学</em>奥卡姆剃刀原则</div>
              <div class="day-desc">「如无必要，勿增实体。」在解释复杂现象时，最简单的那个往往最接近正确。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知科学',this);">认知科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-36" onclick="toggleNote(36)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(36)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-36"></div>
                <div class="note-display-wrap " id="note-display-wrap-36">
                  <div class="note-display-header" onclick="toggleNoteDisplay(36)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-36"></div>
                </div>
                <div class="note-editor" id="note-editor-36">
                  <textarea class="note-textarea" id="note-ta-36" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(36)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(36)">删除</button>
                    <span class="note-timestamp" id="note-ts-36"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="37" data-tags="交叉学科,复盘">
            <div class="day-num " id="daynum-37">D37</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：思维的除草</div>
              <div class="day-desc">审视过去的直觉判断，用第一性原理将其完全拆解并重组一次。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-37" onclick="toggleNote(37)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(37)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-37"></div>
                <div class="note-display-wrap " id="note-display-wrap-37">
                  <div class="note-display-header" onclick="toggleNoteDisplay(37)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-37"></div>
                </div>
                <div class="note-editor" id="note-editor-37">
                  <textarea class="note-textarea" id="note-ta-37" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(37)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(37)">删除</button>
                    <span class="note-timestamp" id="note-ts-37"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W7 · 西方哲学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="38" data-tags="哲学,进化论,演化论">
            <div class="day-num " id="daynum-38">D38</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>苏格拉底的牛虻精神</div>
              <div class="day-desc">哲学的起点是「承认无知」。提问比给答案更重要，通过不断追问打破理所当然的日常幻觉。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('进化论',this);">进化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-38" onclick="toggleNote(38)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(38)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-38"></div>
                <div class="note-display-wrap " id="note-display-wrap-38">
                  <div class="note-display-header" onclick="toggleNoteDisplay(38)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-38"></div>
                </div>
                <div class="note-editor" id="note-editor-38">
                  <textarea class="note-textarea" id="note-ta-38" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(38)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(38)">删除</button>
                    <span class="note-timestamp" id="note-ts-38"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="39" data-tags="哲学,演化论">
            <div class="day-num " id="daynum-39">D39</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>柏拉图的洞穴之喻</div>
              <div class="day-desc">现实可能只是更高维「理念世界」的投影。重新思考眼前看到的「真实」到底有几分可信。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-39" onclick="toggleNote(39)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(39)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-39"></div>
                <div class="note-display-wrap " id="note-display-wrap-39">
                  <div class="note-display-header" onclick="toggleNoteDisplay(39)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-39"></div>
                </div>
                <div class="note-editor" id="note-editor-39">
                  <textarea class="note-textarea" id="note-ta-39" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(39)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(39)">删除</button>
                    <span class="note-timestamp" id="note-ts-39"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="40" data-tags="哲学,基因,演化论">
            <div class="day-num " id="daynum-40">D40</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>笛卡尔：我思故我在</div>
              <div class="day-desc">当你把世界上一切东西都怀疑掉之后，唯一不能怀疑的，就是「你正在怀疑」这个意识本身。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('基因',this);">基因</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-40" onclick="toggleNote(40)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(40)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-40"></div>
                <div class="note-display-wrap " id="note-display-wrap-40">
                  <div class="note-display-header" onclick="toggleNoteDisplay(40)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-40"></div>
                </div>
                <div class="note-editor" id="note-editor-40">
                  <textarea class="note-textarea" id="note-ta-40" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(40)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(40)">删除</button>
                    <span class="note-timestamp" id="note-ts-40"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="41" data-tags="哲学,演化论,基因">
            <div class="day-num " id="daynum-41">D41</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>康德与「物自体」</div>
              <div class="day-desc">人类永远戴着「时空和因果律」的有色眼镜看世界，永远无法触及事物本身的绝对面貌。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('基因',this);">基因</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-41" onclick="toggleNote(41)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(41)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-41"></div>
                <div class="note-display-wrap " id="note-display-wrap-41">
                  <div class="note-display-header" onclick="toggleNoteDisplay(41)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-41"></div>
                </div>
                <div class="note-editor" id="note-editor-41">
                  <textarea class="note-textarea" id="note-ta-41" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(41)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(41)">删除</button>
                    <span class="note-timestamp" id="note-ts-41"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="42" data-tags="哲学,神经科学,意识">
            <div class="day-num " id="daynum-42">D42</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>尼采与「超人」哲学</div>
              <div class="day-desc">在没有绝对价值锚点的虚无世界里，人必须拥有强大的生命意志，为自己创造全新的法则。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-42" onclick="toggleNote(42)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(42)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-42"></div>
                <div class="note-display-wrap " id="note-display-wrap-42">
                  <div class="note-display-header" onclick="toggleNoteDisplay(42)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-42"></div>
                </div>
                <div class="note-editor" id="note-editor-42">
                  <textarea class="note-textarea" id="note-ta-42" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(42)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(42)">删除</button>
                    <span class="note-timestamp" id="note-ts-42"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="43" data-tags="哲学,神经科学">
            <div class="day-num " id="daynum-43">D43</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>萨特与存在主义</div>
              <div class="day-desc">「存在先于本质」。人没有被预先设定好的出厂目的，面对不确定性，自由是一种沉重的责任。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-43" onclick="toggleNote(43)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(43)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-43"></div>
                <div class="note-display-wrap " id="note-display-wrap-43">
                  <div class="note-display-header" onclick="toggleNoteDisplay(43)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-43"></div>
                </div>
                <div class="note-editor" id="note-editor-43">
                  <textarea class="note-textarea" id="note-ta-43" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(43)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(43)">删除</button>
                    <span class="note-timestamp" id="note-ts-43"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="44" data-tags="交叉学科,心理学">
            <div class="day-num " id="daynum-44">D44</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：自我意义的赋予</div>
              <div class="day-desc">结合存在主义，不去寻找「标准人生路径」，纯粹依靠当下的行动去定义自身价值。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-44" onclick="toggleNote(44)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(44)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-44"></div>
                <div class="note-display-wrap " id="note-display-wrap-44">
                  <div class="note-display-header" onclick="toggleNoteDisplay(44)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-44"></div>
                </div>
                <div class="note-editor" id="note-editor-44">
                  <textarea class="note-textarea" id="note-ta-44" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(44)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(44)">删除</button>
                    <span class="note-timestamp" id="note-ts-44"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W8 · 东方哲学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="45" data-tags="东方哲学,心理学">
            <div class="day-num " id="daynum-45">D45</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>孔子的世俗秩序系统</div>
              <div class="day-desc">「克己复礼」的本质：通过建立明确的伦理名分和仪式，极大降低人与人之间的协作与沟通成本。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-45" onclick="toggleNote(45)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(45)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-45"></div>
                <div class="note-display-wrap " id="note-display-wrap-45">
                  <div class="note-display-header" onclick="toggleNoteDisplay(45)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-45"></div>
                </div>
                <div class="note-editor" id="note-editor-45">
                  <textarea class="note-textarea" id="note-ta-45" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(45)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(45)">删除</button>
                    <span class="note-timestamp" id="note-ts-45"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="46" data-tags="东方哲学,心理学,认知">
            <div class="day-num " id="daynum-46">D46</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>老子的系统反向控制</div>
              <div class="day-desc">「无为而无不为」。承认系统的混沌性，不强行干预，顺应自然规律反而能达到最优的控制效果。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-46" onclick="toggleNote(46)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(46)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-46"></div>
                <div class="note-display-wrap " id="note-display-wrap-46">
                  <div class="note-display-header" onclick="toggleNoteDisplay(46)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-46"></div>
                </div>
                <div class="note-editor" id="note-editor-46">
                  <textarea class="note-textarea" id="note-ta-46" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(46)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(46)">删除</button>
                    <span class="note-timestamp" id="note-ts-46"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="47" data-tags="东方哲学,复盘">
            <div class="day-num " id="daynum-47">D47</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>庄子的相对主义自由</div>
              <div class="day-desc">「齐物论」：打破功利、大小、对错的二元对立视角，跳出世俗评价体系，获得高维度的心理自由。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-47" onclick="toggleNote(47)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(47)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-47"></div>
                <div class="note-display-wrap " id="note-display-wrap-47">
                  <div class="note-display-header" onclick="toggleNoteDisplay(47)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-47"></div>
                </div>
                <div class="note-editor" id="note-editor-47">
                  <textarea class="note-textarea" id="note-ta-47" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(47)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(47)">删除</button>
                    <span class="note-timestamp" id="note-ts-47"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="48" data-tags="东方哲学,信息论,复杂系统">
            <div class="day-num " id="daynum-48">D48</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>释迦牟尼的苦集灭道</div>
              <div class="day-desc">揭示多巴胺的骗局：人类的痛苦源于对无常事物的执着。切断贪欲的算法，是内心平静的终极路径。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息论',this);">信息论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-48" onclick="toggleNote(48)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(48)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-48"></div>
                <div class="note-display-wrap " id="note-display-wrap-48">
                  <div class="note-display-header" onclick="toggleNoteDisplay(48)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-48"></div>
                </div>
                <div class="note-editor" id="note-editor-48">
                  <textarea class="note-textarea" id="note-ta-48" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(48)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(48)">删除</button>
                    <span class="note-timestamp" id="note-ts-48"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="49" data-tags="东方哲学,复杂系统,熵">
            <div class="day-num " id="daynum-49">D49</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>法家的管理控制论</div>
              <div class="day-desc">纯粹基于人性趋利避害的特点，通过冷酷的「赏罚分明」来驱动庞大组织的运转。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-49" onclick="toggleNote(49)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(49)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-49"></div>
                <div class="note-display-wrap " id="note-display-wrap-49">
                  <div class="note-display-header" onclick="toggleNoteDisplay(49)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-49"></div>
                </div>
                <div class="note-editor" id="note-editor-49">
                  <textarea class="note-textarea" id="note-ta-49" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(49)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(49)">删除</button>
                    <span class="note-timestamp" id="note-ts-49"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="50" data-tags="东方哲学,复杂系统">
            <div class="day-num " id="daynum-50">D50</div>
            <div class="day-content">
              <div class="day-topic"><em>东方哲学</em>禅宗的「指月之指」</div>
              <div class="day-desc">语言、概念和工具都只是指向月亮的那根「手指」。警惕沉迷于工具本身，而忘记了真正要达成的目的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('东方哲学',this);">东方哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-50" onclick="toggleNote(50)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(50)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-50"></div>
                <div class="note-display-wrap " id="note-display-wrap-50">
                  <div class="note-display-header" onclick="toggleNoteDisplay(50)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-50"></div>
                </div>
                <div class="note-editor" id="note-editor-50">
                  <textarea class="note-textarea" id="note-ta-50" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(50)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(50)">删除</button>
                    <span class="note-timestamp" id="note-ts-50"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="51" data-tags="交叉学科,复杂系统">
            <div class="day-num " id="daynum-51">D51</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：组织架构的文化张力</div>
              <div class="day-desc">对比东西方：个人意志与集体和谐的碰撞，透视现代企业规章制度与文化建设底层的矛盾与融合。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-51" onclick="toggleNote(51)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(51)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-51"></div>
                <div class="note-display-wrap " id="note-display-wrap-51">
                  <div class="note-display-header" onclick="toggleNoteDisplay(51)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-51"></div>
                </div>
                <div class="note-editor" id="note-editor-51">
                  <textarea class="note-textarea" id="note-ta-51" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(51)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(51)">删除</button>
                    <span class="note-timestamp" id="note-ts-51"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W9 · 心理学与宏观历史</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="52" data-tags="心理学,复杂系统,博弈">
            <div class="day-num " id="daynum-52">D52</div>
            <div class="day-content">
              <div class="day-topic"><em>心理学</em>丹尼尔·卡尼曼的双系统</div>
              <div class="day-desc">思考的快与慢。大脑为了节能，95%的时间在使用直觉（系统1），这种偷懒导致大量偏见和失误。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-52" onclick="toggleNote(52)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(52)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-52"></div>
                <div class="note-display-wrap " id="note-display-wrap-52">
                  <div class="note-display-header" onclick="toggleNoteDisplay(52)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-52"></div>
                </div>
                <div class="note-editor" id="note-editor-52">
                  <textarea class="note-textarea" id="note-ta-52" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(52)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(52)">删除</button>
                    <span class="note-timestamp" id="note-ts-52"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="53" data-tags="心理学,博弈论,博弈">
            <div class="day-num " id="daynum-53">D53</div>
            <div class="day-content">
              <div class="day-topic"><em>心理学</em>认知失调的自欺机制</div>
              <div class="day-desc">当现实行为与内在信念发生冲突时，人类最擅长的不是改变行为，而是扭曲事实让内心重新感到自洽。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-53" onclick="toggleNote(53)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(53)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-53"></div>
                <div class="note-display-wrap " id="note-display-wrap-53">
                  <div class="note-display-header" onclick="toggleNoteDisplay(53)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-53"></div>
                </div>
                <div class="note-editor" id="note-editor-53">
                  <textarea class="note-textarea" id="note-ta-53" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(53)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(53)">删除</button>
                    <span class="note-timestamp" id="note-ts-53"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="54" data-tags="宏观历史,博弈论,博弈">
            <div class="day-num " id="daynum-54">D54</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观历史</em>认知革命与虚构故事</div>
              <div class="day-desc">智人之所以能统治地球，是因为拥有谈论「不存在之物」并因此达成大规模协作的能力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观历史',this);">宏观历史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-54" onclick="toggleNote(54)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(54)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-54"></div>
                <div class="note-display-wrap " id="note-display-wrap-54">
                  <div class="note-display-header" onclick="toggleNoteDisplay(54)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-54"></div>
                </div>
                <div class="note-editor" id="note-editor-54">
                  <textarea class="note-textarea" id="note-ta-54" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(54)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(54)">删除</button>
                    <span class="note-timestamp" id="note-ts-54"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="55" data-tags="宏观历史,博弈论">
            <div class="day-num " id="daynum-55">D55</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观历史</em>农业革命的内卷陷阱</div>
              <div class="day-desc">技术的反噬：小麦驯化了人类，将人锁死在土地上。效率工具的引入未必带来轻松，反而可能拉高生存门槛。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观历史',this);">宏观历史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-55" onclick="toggleNote(55)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(55)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-55"></div>
                <div class="note-display-wrap " id="note-display-wrap-55">
                  <div class="note-display-header" onclick="toggleNoteDisplay(55)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-55"></div>
                </div>
                <div class="note-editor" id="note-editor-55">
                  <textarea class="note-textarea" id="note-ta-55" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(55)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(55)">删除</button>
                    <span class="note-timestamp" id="note-ts-55"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="56" data-tags="宏观历史,复盘">
            <div class="day-num " id="daynum-56">D56</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观历史</em>想象的共同体与货币</div>
              <div class="day-desc">钞票本身没有价值，它是一套基于集体信任的协议。一切社会秩序底层都建立在「相信同一个故事」上。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观历史',this);">宏观历史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-56" onclick="toggleNote(56)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(56)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-56"></div>
                <div class="note-display-wrap " id="note-display-wrap-56">
                  <div class="note-display-header" onclick="toggleNoteDisplay(56)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-56"></div>
                </div>
                <div class="note-editor" id="note-editor-56">
                  <textarea class="note-textarea" id="note-ta-56" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(56)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(56)">删除</button>
                    <span class="note-timestamp" id="note-ts-56"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="57" data-tags="科技史,哲学,认识论">
            <div class="day-num " id="daynum-57">D57</div>
            <div class="day-content">
              <div class="day-topic"><em>科技史</em>科学革命的范式转移</div>
              <div class="day-desc">从「古人已经知道一切」转变为「承认我们的无知」。观察、实验和数学工具打破了教条主义的封印。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('科技史',this);">科技史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认识论',this);">认识论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-57" onclick="toggleNote(57)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(57)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-57"></div>
                <div class="note-display-wrap " id="note-display-wrap-57">
                  <div class="note-display-header" onclick="toggleNoteDisplay(57)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-57"></div>
                </div>
                <div class="note-editor" id="note-editor-57">
                  <textarea class="note-textarea" id="note-ta-57" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(57)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(57)">删除</button>
                    <span class="note-timestamp" id="note-ts-57"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="58" data-tags="科技史,哲学">
            <div class="day-num " id="daynum-58">D58</div>
            <div class="day-content">
              <div class="day-topic"><em>科技史</em>工业革命与能源解放</div>
              <div class="day-desc">化石燃料的引入不仅改变了生产力，更从根本上重塑了全球的阶级与权力结构。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('科技史',this);">科技史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-58" onclick="toggleNote(58)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(58)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-58"></div>
                <div class="note-display-wrap " id="note-display-wrap-58">
                  <div class="note-display-header" onclick="toggleNoteDisplay(58)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-58"></div>
                </div>
                <div class="note-editor" id="note-editor-58">
                  <textarea class="note-textarea" id="note-ta-58" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(58)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(58)">删除</button>
                    <span class="note-timestamp" id="note-ts-58"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W10 · 历史演化与第二月复盘</span>
            <span class="week-days-count">2 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="59" data-tags="宏观历史,哲学,认识论">
            <div class="day-num " id="daynum-59">D59</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观历史</em>历史演化的必然与偶然</div>
              <div class="day-desc">如果没有爱迪生，灯泡依然会被发明。技术演化有其客观的涌现规律，但关键时刻的走向由偶然性决定。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观历史',this);">宏观历史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认识论',this);">认识论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-59" onclick="toggleNote(59)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(59)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-59"></div>
                <div class="note-display-wrap " id="note-display-wrap-59">
                  <div class="note-display-header" onclick="toggleNoteDisplay(59)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-59"></div>
                </div>
                <div class="note-editor" id="note-editor-59">
                  <textarea class="note-textarea" id="note-ta-59" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(59)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(59)">删除</button>
                    <span class="note-timestamp" id="note-ts-59"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="60" data-tags="大复盘,哲学">
            <div class="day-num " id="daynum-60">D60</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第二月复盘：拆解人类的「源代码」</div>
              <div class="day-desc">从逻辑、哲学到宏观历史，总结人类是如何用脆弱的肉身，通过一套虚构的「协议」建立庞大文明机器的。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-60" onclick="toggleNote(60)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(60)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-60"></div>
                <div class="note-display-wrap " id="note-display-wrap-60">
                  <div class="note-display-header" onclick="toggleNoteDisplay(60)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-60"></div>
                </div>
                <div class="note-editor" id="note-editor-60">
                  <textarea class="note-textarea" id="note-ta-60" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(60)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(60)">删除</button>
                    <span class="note-timestamp" id="note-ts-60"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-3">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#c85a7a"></div>
        <div class="module-icon" style="background:#c85a7a18; color:#c85a7a">⚖️</div>
        <div class="module-meta">
          <div class="module-num">MODULE 03</div>
          <div class="module-title" style="color:#c85a7a">社会秩序与博弈
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">系统的「网络协议」</span>
          </div>
          <div class="module-days" style="color:#c85a7a77">经济学·博弈论·金融学·政治学·社会学·管理学</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#c85a7a44;color:#c85a7a99">Day 61–90</span>
          <span class="module-chevron" style="color:#c85a7a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W11 · 经济学与博弈论</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="61" data-tags="经济学,哲学,伦理">
            <div class="day-num " id="daynum-61">D61</div>
            <div class="day-content">
              <div class="day-topic"><em>经济学</em>稀缺性与机会成本</div>
              <div class="day-desc">世界上没有免费的午餐。你做出任何选择，真正的代价是你为了它而放弃的最高价值的选项。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('伦理',this);">伦理</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-61" onclick="toggleNote(61)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(61)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-61"></div>
                <div class="note-display-wrap " id="note-display-wrap-61">
                  <div class="note-display-header" onclick="toggleNoteDisplay(61)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-61"></div>
                </div>
                <div class="note-editor" id="note-editor-61">
                  <textarea class="note-textarea" id="note-ta-61" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(61)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(61)">删除</button>
                    <span class="note-timestamp" id="note-ts-61"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="62" data-tags="经济学,伦理,哲学">
            <div class="day-num " id="daynum-62">D62</div>
            <div class="day-content">
              <div class="day-topic"><em>经济学</em>边际效用递减</div>
              <div class="day-desc">为什么拥有越多，快乐越少？理解「新增的一单位」带来的价值是如何随着总量增加而暴跌的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('伦理',this);">伦理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-62" onclick="toggleNote(62)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(62)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-62"></div>
                <div class="note-display-wrap " id="note-display-wrap-62">
                  <div class="note-display-header" onclick="toggleNoteDisplay(62)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-62"></div>
                </div>
                <div class="note-editor" id="note-editor-62">
                  <textarea class="note-textarea" id="note-ta-62" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(62)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(62)">删除</button>
                    <span class="note-timestamp" id="note-ts-62"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="63" data-tags="经济学,哲学">
            <div class="day-num " id="daynum-63">D63</div>
            <div class="day-content">
              <div class="day-topic"><em>经济学</em>价格机制的本质</div>
              <div class="day-desc">价格不是由成本决定的，而是由供需决定的。价格本质上是整个社会网络在传递「资源往哪走」的信息。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-63" onclick="toggleNote(63)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(63)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-63"></div>
                <div class="note-display-wrap " id="note-display-wrap-63">
                  <div class="note-display-header" onclick="toggleNoteDisplay(63)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-63"></div>
                </div>
                <div class="note-editor" id="note-editor-63">
                  <textarea class="note-textarea" id="note-ta-63" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(63)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(63)">删除</button>
                    <span class="note-timestamp" id="note-ts-63"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="64" data-tags="博弈论,复盘">
            <div class="day-num " id="daynum-64">D64</div>
            <div class="day-content">
              <div class="day-topic"><em>博弈论</em>囚徒困境与零和博弈</div>
              <div class="day-desc">为什么极其聪明的个人，在特定规则下会做出对集体极其愚蠢的决定？（透视职场内卷的底层机制）</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-64" onclick="toggleNote(64)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(64)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-64"></div>
                <div class="note-display-wrap " id="note-display-wrap-64">
                  <div class="note-display-header" onclick="toggleNoteDisplay(64)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-64"></div>
                </div>
                <div class="note-editor" id="note-editor-64">
                  <textarea class="note-textarea" id="note-ta-64" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(64)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(64)">删除</button>
                    <span class="note-timestamp" id="note-ts-64"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="65" data-tags="博弈论,经济学,市场">
            <div class="day-num " id="daynum-65">D65</div>
            <div class="day-content">
              <div class="day-topic"><em>博弈论</em>纳什均衡</div>
              <div class="day-desc">系统中的一种「稳定状态」。一旦达到这个状态，没有任何人有动力单方面改变自己的策略。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-65" onclick="toggleNote(65)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(65)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-65"></div>
                <div class="note-display-wrap " id="note-display-wrap-65">
                  <div class="note-display-header" onclick="toggleNoteDisplay(65)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-65"></div>
                </div>
                <div class="note-editor" id="note-editor-65">
                  <textarea class="note-textarea" id="note-ta-65" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(65)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(65)">删除</button>
                    <span class="note-timestamp" id="note-ts-65"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="66" data-tags="博弈论,经济学,市场">
            <div class="day-num " id="daynum-66">D66</div>
            <div class="day-content">
              <div class="day-topic"><em>博弈论</em>重复博弈与合作演化</div>
              <div class="day-desc">「以牙还牙（Tit for Tat）」是陌生人社会中建立合作的最优数学解。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈论',this);">博弈论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-66" onclick="toggleNote(66)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(66)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-66"></div>
                <div class="note-display-wrap " id="note-display-wrap-66">
                  <div class="note-display-header" onclick="toggleNoteDisplay(66)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-66"></div>
                </div>
                <div class="note-editor" id="note-editor-66">
                  <textarea class="note-textarea" id="note-ta-66" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(66)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(66)">删除</button>
                    <span class="note-timestamp" id="note-ts-66"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="67" data-tags="交叉学科,经济学,博弈,市场">
            <div class="day-num " id="daynum-67">D67</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：理性的算计</div>
              <div class="day-desc">思考题：HR在设计绩效考核时，是在引导员工走向「囚徒困境」（互踩），还是「重复博弈」（协作）？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('市场',this);">市场</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-67" onclick="toggleNote(67)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(67)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-67"></div>
                <div class="note-display-wrap " id="note-display-wrap-67">
                  <div class="note-display-header" onclick="toggleNoteDisplay(67)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-67"></div>
                </div>
                <div class="note-editor" id="note-editor-67">
                  <textarea class="note-textarea" id="note-ta-67" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(67)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(67)">删除</button>
                    <span class="note-timestamp" id="note-ts-67"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W12 · 金融学与政治学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="68" data-tags="金融学,货币,金融,经济学">
            <div class="day-num " id="daynum-68">D68</div>
            <div class="day-content">
              <div class="day-topic"><em>金融学</em>货币：信用的具象化</div>
              <div class="day-desc">现代货币早已脱离金本位。钱不是财富，钱是对社会资源的一种「索取权」和债务凭证。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融学',this);">金融学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('货币',this);">货币</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融',this);">金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-68" onclick="toggleNote(68)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(68)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-68"></div>
                <div class="note-display-wrap " id="note-display-wrap-68">
                  <div class="note-display-header" onclick="toggleNoteDisplay(68)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-68"></div>
                </div>
                <div class="note-editor" id="note-editor-68">
                  <textarea class="note-textarea" id="note-ta-68" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(68)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(68)">删除</button>
                    <span class="note-timestamp" id="note-ts-68"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="69" data-tags="金融学,金融,复利,杠杆">
            <div class="day-num " id="daynum-69">D69</div>
            <div class="day-content">
              <div class="day-topic"><em>金融学</em>杠杆与复利</div>
              <div class="day-desc">复利是时间维度的非线性增长；杠杆是空间维度的力量放大器。两者结合能创造奇迹，也能导致毁灭。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融学',this);">金融学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融',this);">金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复利',this);">复利</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('杠杆',this);">杠杆</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-69" onclick="toggleNote(69)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(69)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-69"></div>
                <div class="note-display-wrap " id="note-display-wrap-69">
                  <div class="note-display-header" onclick="toggleNoteDisplay(69)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-69"></div>
                </div>
                <div class="note-editor" id="note-editor-69">
                  <textarea class="note-textarea" id="note-ta-69" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(69)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(69)">删除</button>
                    <span class="note-timestamp" id="note-ts-69"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="70" data-tags="金融学,经济周期,金融,债务">
            <div class="day-num " id="daynum-70">D70</div>
            <div class="day-content">
              <div class="day-topic"><em>金融学</em>债务周期模型</div>
              <div class="day-desc">达利欧模型：经济的繁荣与衰退不是随机的，而是信贷扩张与收缩的必然周期节律。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融学',this);">金融学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济周期',this);">经济周期</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融',this);">金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('债务',this);">债务</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-70" onclick="toggleNote(70)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(70)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-70"></div>
                <div class="note-display-wrap " id="note-display-wrap-70">
                  <div class="note-display-header" onclick="toggleNoteDisplay(70)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-70"></div>
                </div>
                <div class="note-editor" id="note-editor-70">
                  <textarea class="note-textarea" id="note-ta-70" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(70)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(70)">删除</button>
                    <span class="note-timestamp" id="note-ts-70"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="71" data-tags="政治学,权力">
            <div class="day-num " id="daynum-71">D71</div>
            <div class="day-content">
              <div class="day-topic"><em>政治学</em>社会契约论</div>
              <div class="day-desc">国家是如何诞生的？人类出让一部分绝对自由给「利维坦」（政府），换取生命与财产的安全。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-71" onclick="toggleNote(71)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(71)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-71"></div>
                <div class="note-display-wrap " id="note-display-wrap-71">
                  <div class="note-display-header" onclick="toggleNoteDisplay(71)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-71"></div>
                </div>
                <div class="note-editor" id="note-editor-71">
                  <textarea class="note-textarea" id="note-ta-71" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(71)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(71)">删除</button>
                    <span class="note-timestamp" id="note-ts-71"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="72" data-tags="政治学,权力">
            <div class="day-num " id="daynum-72">D72</div>
            <div class="day-content">
              <div class="day-topic"><em>政治学</em>暴力的合法垄断</div>
              <div class="day-desc">马克斯·韦伯的洞见：一个政权之所以能制定规则，底层逻辑在于它垄断了合法使用暴力的权力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-72" onclick="toggleNote(72)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(72)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-72"></div>
                <div class="note-display-wrap " id="note-display-wrap-72">
                  <div class="note-display-header" onclick="toggleNoteDisplay(72)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-72"></div>
                </div>
                <div class="note-editor" id="note-editor-72">
                  <textarea class="note-textarea" id="note-ta-72" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(72)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(72)">删除</button>
                    <span class="note-timestamp" id="note-ts-72"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="73" data-tags="政治学,权力">
            <div class="day-num " id="daynum-73">D73</div>
            <div class="day-content">
              <div class="day-topic"><em>政治学</em>权力制衡与防错设计</div>
              <div class="day-desc">为什么三权分立效率很低，但却被认为是好制度？因为政治设计的核心不是追求效率，而是防止单点故障。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-73" onclick="toggleNote(73)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(73)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-73"></div>
                <div class="note-display-wrap " id="note-display-wrap-73">
                  <div class="note-display-header" onclick="toggleNoteDisplay(73)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-73"></div>
                </div>
                <div class="note-editor" id="note-editor-73">
                  <textarea class="note-textarea" id="note-ta-73" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(73)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(73)">删除</button>
                    <span class="note-timestamp" id="note-ts-73"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="74" data-tags="交叉学科,权力,经济学,复盘">
            <div class="day-num " id="daynum-74">D74</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：权力与财富的绑定</div>
              <div class="day-desc">将「资本（经济）」与「强制力（政治）」结合来看，理解为什么所有的商业巨头最终都会触碰规则边界。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-74" onclick="toggleNote(74)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(74)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-74"></div>
                <div class="note-display-wrap " id="note-display-wrap-74">
                  <div class="note-display-header" onclick="toggleNoteDisplay(74)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-74"></div>
                </div>
                <div class="note-editor" id="note-editor-74">
                  <textarea class="note-textarea" id="note-ta-74" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(74)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(74)">删除</button>
                    <span class="note-timestamp" id="note-ts-74"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W13 · 社会学与法学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="75" data-tags="社会学,马太效应">
            <div class="day-num " id="daynum-75">D75</div>
            <div class="day-content">
              <div class="day-topic"><em>社会学</em>阶级固化与马太效应</div>
              <div class="day-desc">「凡有的，还要加给他。」理解社会财富和资源为何会自然而然地向头部网络节点集中。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('马太效应',this);">马太效应</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-75" onclick="toggleNote(75)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(75)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-75"></div>
                <div class="note-display-wrap " id="note-display-wrap-75">
                  <div class="note-display-header" onclick="toggleNoteDisplay(75)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-75"></div>
                </div>
                <div class="note-editor" id="note-editor-75">
                  <textarea class="note-textarea" id="note-ta-75" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(75)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(75)">删除</button>
                    <span class="note-timestamp" id="note-ts-75"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="76" data-tags="社会学,网络">
            <div class="day-num " id="daynum-76">D76</div>
            <div class="day-content">
              <div class="day-topic"><em>社会学</em>弱联系的力量</div>
              <div class="day-desc">为什么找工作往往靠不太熟的人？信息破圈的底层网络逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络',this);">网络</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-76" onclick="toggleNote(76)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(76)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-76"></div>
                <div class="note-display-wrap " id="note-display-wrap-76">
                  <div class="note-display-header" onclick="toggleNoteDisplay(76)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-76"></div>
                </div>
                <div class="note-editor" id="note-editor-76">
                  <textarea class="note-textarea" id="note-ta-76" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(76)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(76)">删除</button>
                    <span class="note-timestamp" id="note-ts-76"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="77" data-tags="社会学,群体">
            <div class="day-num " id="daynum-77">D77</div>
            <div class="day-content">
              <div class="day-topic"><em>社会学</em>乌合之众与群体降智</div>
              <div class="day-desc">为什么个体是理性的，但汇聚成群体后就会变得盲目、情绪化且极具破坏力？（去个性化机制）</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('群体',this);">群体</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-77" onclick="toggleNote(77)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(77)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-77"></div>
                <div class="note-display-wrap " id="note-display-wrap-77">
                  <div class="note-display-header" onclick="toggleNoteDisplay(77)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-77"></div>
                </div>
                <div class="note-editor" id="note-editor-77">
                  <textarea class="note-textarea" id="note-ta-77" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(77)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(77)">删除</button>
                    <span class="note-timestamp" id="note-ts-77"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="78" data-tags="社会学,消费">
            <div class="day-num " id="daynum-78">D78</div>
            <div class="day-content">
              <div class="day-topic"><em>社会学</em>消费主义与符号互动</div>
              <div class="day-desc">你买的不是商品，而是「身份标签」。理解商业社会是如何通过制造焦虑来逼迫你进行符号消费的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('消费',this);">消费</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-78" onclick="toggleNote(78)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(78)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-78"></div>
                <div class="note-display-wrap " id="note-display-wrap-78">
                  <div class="note-display-header" onclick="toggleNoteDisplay(78)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-78"></div>
                </div>
                <div class="note-editor" id="note-editor-78">
                  <textarea class="note-textarea" id="note-ta-78" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(78)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(78)">删除</button>
                    <span class="note-timestamp" id="note-ts-78"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="79" data-tags="法学">
            <div class="day-num " id="daynum-79">D79</div>
            <div class="day-content">
              <div class="day-topic"><em>法学</em>程序正义 vs 实体正义</div>
              <div class="day-desc">为什么宁可放走坏人，也不能违规取证？理解为了维护整个系统规则的绝对信用，必须容忍局部的错误。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('法学',this);">法学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-79" onclick="toggleNote(79)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(79)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-79"></div>
                <div class="note-display-wrap " id="note-display-wrap-79">
                  <div class="note-display-header" onclick="toggleNoteDisplay(79)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-79"></div>
                </div>
                <div class="note-editor" id="note-editor-79">
                  <textarea class="note-textarea" id="note-ta-79" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(79)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(79)">删除</button>
                    <span class="note-timestamp" id="note-ts-79"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="80" data-tags="法学,产权">
            <div class="day-num " id="daynum-80">D80</div>
            <div class="day-content">
              <div class="day-topic"><em>法学</em>财产权的底层逻辑</div>
              <div class="day-desc">如果你的东西不属于你，你就不会去创造。明确的产权界定，是所有复杂商业社会运作的第一块基石。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('法学',this);">法学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('产权',this);">产权</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-80" onclick="toggleNote(80)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(80)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-80"></div>
                <div class="note-display-wrap " id="note-display-wrap-80">
                  <div class="note-display-header" onclick="toggleNoteDisplay(80)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-80"></div>
                </div>
                <div class="note-editor" id="note-editor-80">
                  <textarea class="note-textarea" id="note-ta-80" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(80)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(80)">删除</button>
                    <span class="note-timestamp" id="note-ts-80"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="81" data-tags="交叉学科,社会学,复盘">
            <div class="day-num " id="daynum-81">D81</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：群体的无意识网络</div>
              <div class="day-desc">结合心理学与社会学，剖析「为什么我们总是身不由己地被卷入某种社会洪流」。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-81" onclick="toggleNote(81)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(81)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-81"></div>
                <div class="note-display-wrap " id="note-display-wrap-81">
                  <div class="note-display-header" onclick="toggleNoteDisplay(81)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-81"></div>
                </div>
                <div class="note-editor" id="note-editor-81">
                  <textarea class="note-textarea" id="note-ta-81" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(81)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(81)">删除</button>
                    <span class="note-timestamp" id="note-ts-81"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W14 · 管理学与复杂网络</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="82" data-tags="管理学,组织">
            <div class="day-num " id="daynum-82">D82</div>
            <div class="day-content">
              <div class="day-topic"><em>管理学</em>科层制的利与弊</div>
              <div class="day-desc">剖析你最讨厌的「形式主义」：为什么庞大的组织必须依赖死板的流程和无聊的表格，即便它抹杀了人性？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织',this);">组织</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-82" onclick="toggleNote(82)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(82)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-82"></div>
                <div class="note-display-wrap " id="note-display-wrap-82">
                  <div class="note-display-header" onclick="toggleNoteDisplay(82)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-82"></div>
                </div>
                <div class="note-editor" id="note-editor-82">
                  <textarea class="note-textarea" id="note-ta-82" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(82)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(82)">删除</button>
                    <span class="note-timestamp" id="note-ts-82"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="83" data-tags="管理学,委托代理">
            <div class="day-num " id="daynum-83">D83</div>
            <div class="day-content">
              <div class="day-topic"><em>管理学</em>委托-代理问题</div>
              <div class="day-desc">老板（委托人）想压榨，员工（代理人）想摸鱼。两者利益根本不一致时，如何通过制度绑定？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('委托代理',this);">委托代理</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-83" onclick="toggleNote(83)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(83)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-83"></div>
                <div class="note-display-wrap " id="note-display-wrap-83">
                  <div class="note-display-header" onclick="toggleNoteDisplay(83)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-83"></div>
                </div>
                <div class="note-editor" id="note-editor-83">
                  <textarea class="note-textarea" id="note-ta-83" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(83)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(83)">删除</button>
                    <span class="note-timestamp" id="note-ts-83"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="84" data-tags="管理学,指标">
            <div class="day-num " id="daynum-84">D84</div>
            <div class="day-content">
              <div class="day-topic"><em>管理学</em>古德哈特定律</div>
              <div class="day-desc">「当一个指标变成目标时，它就不再是一个好指标。」KPI为什么往往导致数据造假和动作变形。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('指标',this);">指标</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-84" onclick="toggleNote(84)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(84)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-84"></div>
                <div class="note-display-wrap " id="note-display-wrap-84">
                  <div class="note-display-header" onclick="toggleNoteDisplay(84)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-84"></div>
                </div>
                <div class="note-editor" id="note-editor-84">
                  <textarea class="note-textarea" id="note-ta-84" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(84)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(84)">删除</button>
                    <span class="note-timestamp" id="note-ts-84"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="85" data-tags="管理学,组织">
            <div class="day-num " id="daynum-85">D85</div>
            <div class="day-content">
              <div class="day-topic"><em>管理学</em>帕金森定律与彼得原理</div>
              <div class="day-desc">为什么公司部门只会越来越臃肿？为什么平庸的员工总会被晋升到他无法胜任的岗位上？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织',this);">组织</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-85" onclick="toggleNote(85)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(85)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-85"></div>
                <div class="note-display-wrap " id="note-display-wrap-85">
                  <div class="note-display-header" onclick="toggleNoteDisplay(85)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-85"></div>
                </div>
                <div class="note-editor" id="note-editor-85">
                  <textarea class="note-textarea" id="note-ta-85" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(85)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(85)">删除</button>
                    <span class="note-timestamp" id="note-ts-85"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="86" data-tags="复杂网络,复杂系统,幂律,网络">
            <div class="day-num " id="daynum-86">D86</div>
            <div class="day-content">
              <div class="day-topic"><em>复杂网络</em>节点、枢纽与幂律分布</div>
              <div class="day-desc">世界上绝大多数事物不符合「正态分布（钟形曲线）」，而是符合极其不平等的「80/20法则」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂网络',this);">复杂网络</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('幂律',this);">幂律</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络',this);">网络</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-86" onclick="toggleNote(86)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(86)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-86"></div>
                <div class="note-display-wrap " id="note-display-wrap-86">
                  <div class="note-display-header" onclick="toggleNoteDisplay(86)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-86"></div>
                </div>
                <div class="note-editor" id="note-editor-86">
                  <textarea class="note-textarea" id="note-ta-86" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(86)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(86)">删除</button>
                    <span class="note-timestamp" id="note-ts-86"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="87" data-tags="复杂网络,复杂系统,反脆弱,熵">
            <div class="day-num " id="daynum-87">D87</div>
            <div class="day-content">
              <div class="day-topic"><em>复杂网络</em>反脆弱性</div>
              <div class="day-desc">脆弱的系统怕风，而火苗却借风势越烧越旺。如何在充满混乱和不确定性的时代构建自己的反脆弱系统？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂网络',this);">复杂网络</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('反脆弱',this);">反脆弱</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-87" onclick="toggleNote(87)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(87)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-87"></div>
                <div class="note-display-wrap " id="note-display-wrap-87">
                  <div class="note-display-header" onclick="toggleNoteDisplay(87)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-87"></div>
                </div>
                <div class="note-editor" id="note-editor-87">
                  <textarea class="note-textarea" id="note-ta-87" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(87)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(87)">删除</button>
                    <span class="note-timestamp" id="note-ts-87"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="88" data-tags="复杂网络,黑天鹅,复杂系统">
            <div class="day-num " id="daynum-88">D88</div>
            <div class="day-content">
              <div class="day-topic"><em>复杂网络</em>黑天鹅事件</div>
              <div class="day-desc">未知中的未知。为什么基于过往数据的预测模型，在极端罕见事件面前不堪一击？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂网络',this);">复杂网络</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('黑天鹅',this);">黑天鹅</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-88" onclick="toggleNote(88)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(88)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-88"></div>
                <div class="note-display-wrap " id="note-display-wrap-88">
                  <div class="note-display-header" onclick="toggleNoteDisplay(88)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-88"></div>
                </div>
                <div class="note-editor" id="note-editor-88">
                  <textarea class="note-textarea" id="note-ta-88" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(88)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(88)">删除</button>
                    <span class="note-timestamp" id="note-ts-88"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W15 · 第三月复盘</span>
            <span class="week-days-count">2 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="89" data-tags="交叉学科,管理学,复盘">
            <div class="day-num " id="daynum-89">D89</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：直面系统的漏洞</div>
              <div class="day-desc">用这周学到的网络法则，重新审视HR专业背景，写下3条对公司管理制度的致命吐槽。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-89" onclick="toggleNote(89)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(89)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-89"></div>
                <div class="note-display-wrap " id="note-display-wrap-89">
                  <div class="note-display-header" onclick="toggleNoteDisplay(89)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-89"></div>
                </div>
                <div class="note-editor" id="note-editor-89">
                  <textarea class="note-textarea" id="note-ta-89" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(89)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(89)">删除</button>
                    <span class="note-timestamp" id="note-ts-89"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="90" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-90">D90</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第三月复盘：规则与反叛</div>
              <div class="day-desc">我们学会了世界的规则，是为了在其中游刃有余，更是为了在必要时精准地打破它。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-90" onclick="toggleNote(90)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(90)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-90"></div>
                <div class="note-display-wrap " id="note-display-wrap-90">
                  <div class="note-display-header" onclick="toggleNoteDisplay(90)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-90"></div>
                </div>
                <div class="note-editor" id="note-editor-90">
                  <textarea class="note-textarea" id="note-ta-90" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(90)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(90)">删除</button>
                    <span class="note-timestamp" id="note-ts-90"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-4">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#c8975a"></div>
        <div class="module-icon" style="background:#c8975a18; color:#c8975a">⚙️</div>
        <div class="module-meta">
          <div class="module-num">MODULE 04</div>
          <div class="module-title" style="color:#c8975a">技术与文明重启
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">系统的「用户界面」</span>
          </div>
          <div class="module-days" style="color:#c8975a77">工程学·信息论·计算机·AI·美学·3D打印·文明重建</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#c8975a44;color:#c8975a99">Day 91–120</span>
          <span class="module-chevron" style="color:#c8975a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W16 · 工程学与信息论</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="91" data-tags="工程学,系统论">
            <div class="day-num " id="daynum-91">D91</div>
            <div class="day-content">
              <div class="day-topic"><em>工程学</em>模块化思维与解耦</div>
              <div class="day-desc">复杂系统如何运转？将其拆分为互不干扰的黑盒模块。和写代码时封装函数是同一套逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('工程学',this);">工程学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-91" onclick="toggleNote(91)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(91)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-91"></div>
                <div class="note-display-wrap " id="note-display-wrap-91">
                  <div class="note-display-header" onclick="toggleNoteDisplay(91)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-91"></div>
                </div>
                <div class="note-editor" id="note-editor-91">
                  <textarea class="note-textarea" id="note-ta-91" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(91)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(91)">删除</button>
                    <span class="note-timestamp" id="note-ts-91"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="92" data-tags="工程学,系统论">
            <div class="day-num " id="daynum-92">D92</div>
            <div class="day-content">
              <div class="day-topic"><em>工程学</em>冗余设计与容错率</div>
              <div class="day-desc">为什么飞机有两套引擎？在关键节点故意制造「浪费」（冗余），是系统对抗突发性崩溃的唯一工程学手段。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('工程学',this);">工程学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-92" onclick="toggleNote(92)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(92)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-92"></div>
                <div class="note-display-wrap " id="note-display-wrap-92">
                  <div class="note-display-header" onclick="toggleNoteDisplay(92)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-92"></div>
                </div>
                <div class="note-editor" id="note-editor-92">
                  <textarea class="note-textarea" id="note-ta-92" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(92)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(92)">删除</button>
                    <span class="note-timestamp" id="note-ts-92"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="93" data-tags="工程学,系统论,负反馈">
            <div class="day-num " id="daynum-93">D93</div>
            <div class="day-content">
              <div class="day-topic"><em>工程学</em>负反馈控制系统</div>
              <div class="day-desc">恒温器原理。系统如何通过检测「输出结果」并反向抑制「输入」，来维持自身的动态平衡。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('工程学',this);">工程学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('负反馈',this);">负反馈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-93" onclick="toggleNote(93)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(93)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-93"></div>
                <div class="note-display-wrap " id="note-display-wrap-93">
                  <div class="note-display-header" onclick="toggleNoteDisplay(93)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-93"></div>
                </div>
                <div class="note-editor" id="note-editor-93">
                  <textarea class="note-textarea" id="note-ta-93" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(93)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(93)">删除</button>
                    <span class="note-timestamp" id="note-ts-93"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="94" data-tags="信息论,熵,香农,信息">
            <div class="day-num " id="daynum-94">D94</div>
            <div class="day-content">
              <div class="day-topic"><em>信息论</em>香农熵与比特</div>
              <div class="day-desc">与Day1的热力学熵呼应。信息是可以被精确量化的，消除不确定性所需要的代价，就是信息的本质。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息论',this);">信息论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('香农',this);">香农</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-94" onclick="toggleNote(94)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(94)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-94"></div>
                <div class="note-display-wrap " id="note-display-wrap-94">
                  <div class="note-display-header" onclick="toggleNoteDisplay(94)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-94"></div>
                </div>
                <div class="note-editor" id="note-editor-94">
                  <textarea class="note-textarea" id="note-ta-94" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(94)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(94)">删除</button>
                    <span class="note-timestamp" id="note-ts-94"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="95" data-tags="计算机,信息论">
            <div class="day-num " id="daynum-95">D95</div>
            <div class="day-content">
              <div class="day-topic"><em>计算机</em>图灵机与计算的极限</div>
              <div class="day-desc">一条无限长的纸带和几个简单规则，就能模拟宇宙中一切可计算的过程。数字世界的「第一性原理」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('计算机',this);">计算机</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息论',this);">信息论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-95" onclick="toggleNote(95)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(95)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-95"></div>
                <div class="note-display-wrap " id="note-display-wrap-95">
                  <div class="note-display-header" onclick="toggleNoteDisplay(95)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-95"></div>
                </div>
                <div class="note-editor" id="note-editor-95">
                  <textarea class="note-textarea" id="note-ta-95" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(95)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(95)">删除</button>
                    <span class="note-timestamp" id="note-ts-95"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="96" data-tags="计算机,算法">
            <div class="day-num " id="daynum-96">D96</div>
            <div class="day-content">
              <div class="day-topic"><em>计算机</em>算法与时间复杂度</div>
              <div class="day-desc">为什么有的程序秒出，有的要跑一年？理解Big O表示法，看透效率背后的数学天花板。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('计算机',this);">计算机</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('算法',this);">算法</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-96" onclick="toggleNote(96)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(96)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-96"></div>
                <div class="note-display-wrap " id="note-display-wrap-96">
                  <div class="note-display-header" onclick="toggleNoteDisplay(96)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-96"></div>
                </div>
                <div class="note-editor" id="note-editor-96">
                  <textarea class="note-textarea" id="note-ta-96" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(96)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(96)">删除</button>
                    <span class="note-timestamp" id="note-ts-96"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="97" data-tags="交叉学科,系统论,复盘">
            <div class="day-num " id="daynum-97">D97</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：虚拟世界的架构</div>
              <div class="day-desc">尝试用「模块化」和「负反馈」的逻辑，去分析你正在使用的某个AI自动化工作流。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-97" onclick="toggleNote(97)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(97)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-97"></div>
                <div class="note-display-wrap " id="note-display-wrap-97">
                  <div class="note-display-header" onclick="toggleNoteDisplay(97)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-97"></div>
                </div>
                <div class="note-editor" id="note-editor-97">
                  <textarea class="note-textarea" id="note-ta-97" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(97)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(97)">删除</button>
                    <span class="note-timestamp" id="note-ts-97"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W17 · AI与美学原理</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="98" data-tags="互联网,网络">
            <div class="day-num " id="daynum-98">D98</div>
            <div class="day-content">
              <div class="day-topic"><em>互联网</em>去中心化与TCP/IP</div>
              <div class="day-desc">为什么核打击摧毁不了互联网？理解分布式网络如何通过「协议」而非「中央集权」来实现无损信息传输。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('互联网',this);">互联网</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络',this);">网络</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-98" onclick="toggleNote(98)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(98)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-98"></div>
                <div class="note-display-wrap " id="note-display-wrap-98">
                  <div class="note-display-header" onclick="toggleNoteDisplay(98)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-98"></div>
                </div>
                <div class="note-editor" id="note-editor-98">
                  <textarea class="note-textarea" id="note-ta-98" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(98)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(98)">删除</button>
                    <span class="note-timestamp" id="note-ts-98"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="99" data-tags="人工智能,AI,神经网络">
            <div class="day-num " id="daynum-99">D99</div>
            <div class="day-content">
              <div class="day-topic"><em>人工智能</em>神经网络的底层仿生</div>
              <div class="day-desc">让机器像婴儿一样，通过海量数据去「调整权重」，模拟人脑的突触连接。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人工智能',this);">人工智能</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经网络',this);">神经网络</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-99" onclick="toggleNote(99)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(99)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-99"></div>
                <div class="note-display-wrap " id="note-display-wrap-99">
                  <div class="note-display-header" onclick="toggleNoteDisplay(99)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-99"></div>
                </div>
                <div class="note-editor" id="note-editor-99">
                  <textarea class="note-textarea" id="note-ta-99" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(99)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(99)">删除</button>
                    <span class="note-timestamp" id="note-ts-99"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="100" data-tags="人工智能,AI,熵,扩散模型">
            <div class="day-num " id="daynum-100">D100</div>
            <div class="day-content">
              <div class="day-topic"><em>人工智能</em>扩散模型（Diffusion）</div>
              <div class="day-desc">通过在一张纯噪声图里不断「降噪（减熵）」，强行挤压出极其有序的精美图像。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人工智能',this);">人工智能</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('扩散模型',this);">扩散模型</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-100" onclick="toggleNote(100)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(100)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-100"></div>
                <div class="note-display-wrap " id="note-display-wrap-100">
                  <div class="note-display-header" onclick="toggleNoteDisplay(100)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-100"></div>
                </div>
                <div class="note-editor" id="note-editor-100">
                  <textarea class="note-textarea" id="note-ta-100" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(100)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(100)">删除</button>
                    <span class="note-timestamp" id="note-ts-100"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="101" data-tags="人工智能,AI,大模型">
            <div class="day-num " id="daynum-101">D101</div>
            <div class="day-content">
              <div class="day-topic"><em>人工智能</em>大语言模型与涌现能力</div>
              <div class="day-desc">仅仅是做「文字接龙」，当参数量大到一定程度时，为何会自动涌现出惊人的逻辑推理能力？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人工智能',this);">人工智能</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大模型',this);">大模型</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-101" onclick="toggleNote(101)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(101)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-101"></div>
                <div class="note-display-wrap " id="note-display-wrap-101">
                  <div class="note-display-header" onclick="toggleNoteDisplay(101)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-101"></div>
                </div>
                <div class="note-editor" id="note-editor-101">
                  <textarea class="note-textarea" id="note-ta-101" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(101)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(101)">删除</button>
                    <span class="note-timestamp" id="note-ts-101"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="102" data-tags="人工智能,AI">
            <div class="day-num " id="daynum-102">D102</div>
            <div class="day-content">
              <div class="day-topic"><em>人工智能</em>智能体（Agent）系统</div>
              <div class="day-desc">AI是如何从「只会陪聊」进化为能够自己调用浏览器、操作软件、执行复杂工作流的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人工智能',this);">人工智能</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-102" onclick="toggleNote(102)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(102)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-102"></div>
                <div class="note-display-wrap " id="note-display-wrap-102">
                  <div class="note-display-header" onclick="toggleNoteDisplay(102)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-102"></div>
                </div>
                <div class="note-editor" id="note-editor-102">
                  <textarea class="note-textarea" id="note-ta-102" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(102)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(102)">删除</button>
                    <span class="note-timestamp" id="note-ts-102"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="103" data-tags="美学原理,美学,数学">
            <div class="day-num " id="daynum-103">D103</div>
            <div class="day-content">
              <div class="day-topic"><em>美学原理</em>透视法与空间几何</div>
              <div class="day-desc">文艺复兴的降维打击。如何在二维平面上用极其严格的数学规则，欺骗人类大脑产生三维空间的深度错觉。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学原理',this);">美学原理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-103" onclick="toggleNote(103)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(103)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-103"></div>
                <div class="note-display-wrap " id="note-display-wrap-103">
                  <div class="note-display-header" onclick="toggleNoteDisplay(103)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-103"></div>
                </div>
                <div class="note-editor" id="note-editor-103">
                  <textarea class="note-textarea" id="note-ta-103" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(103)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(103)">删除</button>
                    <span class="note-timestamp" id="note-ts-103"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="104" data-tags="交叉学科,AI,美学,复盘">
            <div class="day-num " id="daynum-104">D104</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：机器视角与人类审美</div>
              <div class="day-desc">当AI生成图片和3D模型时，它「理解」美吗？还是它只是拟合了人类历史上所有美的数学分布？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-104" onclick="toggleNote(104)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(104)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-104"></div>
                <div class="note-display-wrap " id="note-display-wrap-104">
                  <div class="note-display-header" onclick="toggleNoteDisplay(104)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-104"></div>
                </div>
                <div class="note-editor" id="note-editor-104">
                  <textarea class="note-textarea" id="note-ta-104" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(104)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(104)">删除</button>
                    <span class="note-timestamp" id="note-ts-104"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W18 · 设计·制造·文明底层</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="105" data-tags="美学原理,美学,色彩">
            <div class="day-num " id="daynum-105">D105</div>
            <div class="day-content">
              <div class="day-topic"><em>美学原理</em>色彩空间（RGB与CMYK）</div>
              <div class="day-desc">光的加法与物质的减法。为什么屏幕上的颜色永远无法在纸上完美打印？理解色彩的物理学局限。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学原理',this);">美学原理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('色彩',this);">色彩</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-105" onclick="toggleNote(105)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(105)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-105"></div>
                <div class="note-display-wrap " id="note-display-wrap-105">
                  <div class="note-display-header" onclick="toggleNoteDisplay(105)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-105"></div>
                </div>
                <div class="note-editor" id="note-editor-105">
                  <textarea class="note-textarea" id="note-ta-105" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(105)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(105)">删除</button>
                    <span class="note-timestamp" id="note-ts-105"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="106" data-tags="设计学,设计,美学">
            <div class="day-num " id="daynum-106">D106</div>
            <div class="day-content">
              <div class="day-topic"><em>设计学</em>形式追随功能（包豪斯）</div>
              <div class="day-desc">现代设计的绝对铁律。不要无意义的装饰，一件物品的长相，必须由它的用途来决定。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计学',this);">设计学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计',this);">设计</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-106" onclick="toggleNote(106)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(106)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-106"></div>
                <div class="note-display-wrap " id="note-display-wrap-106">
                  <div class="note-display-header" onclick="toggleNoteDisplay(106)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-106"></div>
                </div>
                <div class="note-editor" id="note-editor-106">
                  <textarea class="note-textarea" id="note-ta-106" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(106)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(106)">删除</button>
                    <span class="note-timestamp" id="note-ts-106"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="107" data-tags="制造学,工程学,制造">
            <div class="day-num " id="daynum-107">D107</div>
            <div class="day-content">
              <div class="day-topic"><em>制造学</em>增材制造（3D打印）</div>
              <div class="day-desc">告别传统的「切削（减材）」。通过逐层堆叠材料、几乎无浪费的新型制造逻辑对供应链的颠覆。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('制造学',this);">制造学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('工程学',this);">工程学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('制造',this);">制造</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-107" onclick="toggleNote(107)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(107)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-107"></div>
                <div class="note-display-wrap " id="note-display-wrap-107">
                  <div class="note-display-header" onclick="toggleNoteDisplay(107)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-107"></div>
                </div>
                <div class="note-editor" id="note-editor-107">
                  <textarea class="note-textarea" id="note-ta-107" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(107)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(107)">删除</button>
                    <span class="note-timestamp" id="note-ts-107"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="108" data-tags="科技史,能源">
            <div class="day-num " id="daynum-108">D108</div>
            <div class="day-content">
              <div class="day-topic"><em>科技史</em>能源阶跃图谱</div>
              <div class="day-desc">柴草、煤炭、石油、核裂变。人类文明的每一次大升级，本质上都是找到了能量密度更高的「电池」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('科技史',this);">科技史</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-108" onclick="toggleNote(108)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(108)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-108"></div>
                <div class="note-display-wrap " id="note-display-wrap-108">
                  <div class="note-display-header" onclick="toggleNoteDisplay(108)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-108"></div>
                </div>
                <div class="note-editor" id="note-editor-108">
                  <textarea class="note-textarea" id="note-ta-108" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(108)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(108)">删除</button>
                    <span class="note-timestamp" id="note-ts-108"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="109" data-tags="文明重启,文明,能源">
            <div class="day-num " id="daynum-109">D109</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>农业与卡路里防线</div>
              <div class="day-desc">假设明天文明毁灭。如何通过固氮、选种和堆肥，守住人类存活的第一条底线：卡路里输入。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-109" onclick="toggleNote(109)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(109)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-109"></div>
                <div class="note-display-wrap " id="note-display-wrap-109">
                  <div class="note-display-header" onclick="toggleNoteDisplay(109)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-109"></div>
                </div>
                <div class="note-editor" id="note-editor-109">
                  <textarea class="note-textarea" id="note-ta-109" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(109)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(109)">删除</button>
                    <span class="note-timestamp" id="note-ts-109"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="110" data-tags="文明重启,文明,化学">
            <div class="day-num " id="daynum-110">D110</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>基础化工（三酸两碱）</div>
              <div class="day-desc">硫酸、盐酸、硝酸。没有它们，就没有化肥、炸药和塑料。这些工业血液是如何从零提炼出来的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('化学',this);">化学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-110" onclick="toggleNote(110)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(110)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-110"></div>
                <div class="note-display-wrap " id="note-display-wrap-110">
                  <div class="note-display-header" onclick="toggleNoteDisplay(110)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-110"></div>
                </div>
                <div class="note-editor" id="note-editor-110">
                  <textarea class="note-textarea" id="note-ta-110" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(110)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(110)">删除</button>
                    <span class="note-timestamp" id="note-ts-110"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="111" data-tags="交叉学科,文明,复盘">
            <div class="day-num " id="daynum-111">D111</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：从造物到造境</div>
              <div class="day-desc">从屏幕里的3D建模，跨越到了废土世界中如何用泥土和石头重新捏出工业文明。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-111" onclick="toggleNote(111)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(111)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-111"></div>
                <div class="note-display-wrap " id="note-display-wrap-111">
                  <div class="note-display-header" onclick="toggleNoteDisplay(111)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-111"></div>
                </div>
                <div class="note-editor" id="note-editor-111">
                  <textarea class="note-textarea" id="note-ta-111" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(111)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(111)">删除</button>
                    <span class="note-timestamp" id="note-ts-111"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W19-20 · 文明重启与第四月复盘</span>
            <span class="week-days-count">9 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="112" data-tags="文明重启,文明">
            <div class="day-num " id="daynum-112">D112</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>玻璃：文明的放大镜</div>
              <div class="day-desc">烧制沙子。为什么玻璃是科学诞生的前置条件？（显微镜看细菌，望远镜看宇宙，光纤传输数据）</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-112" onclick="toggleNote(112)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(112)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-112"></div>
                <div class="note-display-wrap " id="note-display-wrap-112">
                  <div class="note-display-header" onclick="toggleNoteDisplay(112)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-112"></div>
                </div>
                <div class="note-editor" id="note-editor-112">
                  <textarea class="note-textarea" id="note-ta-112" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(112)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(112)">删除</button>
                    <span class="note-timestamp" id="note-ts-112"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="113" data-tags="文明重启,文明,能源">
            <div class="day-num " id="daynum-113">D113</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>发电机与电力网络</div>
              <div class="day-desc">法拉第的奇迹：如何用磁铁和铜线圈的相对运动，凭空创造出驱动现代世界的幽灵——电。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-113" onclick="toggleNote(113)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(113)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-113"></div>
                <div class="note-display-wrap " id="note-display-wrap-113">
                  <div class="note-display-header" onclick="toggleNoteDisplay(113)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-113"></div>
                </div>
                <div class="note-editor" id="note-editor-113">
                  <textarea class="note-textarea" id="note-ta-113" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(113)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(113)">删除</button>
                    <span class="note-timestamp" id="note-ts-113"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="114" data-tags="文明重启,文明,医学">
            <div class="day-num " id="daynum-114">D114</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>细菌学说与抗生素</div>
              <div class="day-desc">青霉素的发现是如何将人类平均寿命从40岁强行拉升到80岁的？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('医学',this);">医学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-114" onclick="toggleNote(114)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(114)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-114"></div>
                <div class="note-display-wrap " id="note-display-wrap-114">
                  <div class="note-display-header" onclick="toggleNoteDisplay(114)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-114"></div>
                </div>
                <div class="note-editor" id="note-editor-114">
                  <textarea class="note-textarea" id="note-ta-114" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(114)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(114)">删除</button>
                    <span class="note-timestamp" id="note-ts-114"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="115" data-tags="文明重启,文明,机械">
            <div class="day-num " id="daynum-115">D115</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>机械传动与内燃机</div>
              <div class="day-desc">如何将热量（无序的膨胀）转化为稳定的、定向的物理旋转（有序的机械功）？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('机械',this);">机械</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-115" onclick="toggleNote(115)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(115)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-115"></div>
                <div class="note-display-wrap " id="note-display-wrap-115">
                  <div class="note-display-header" onclick="toggleNoteDisplay(115)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-115"></div>
                </div>
                <div class="note-editor" id="note-editor-115">
                  <textarea class="note-textarea" id="note-ta-115" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(115)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(115)">删除</button>
                    <span class="note-timestamp" id="note-ts-115"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="116" data-tags="文明重启,文明,通信">
            <div class="day-num " id="daynum-116">D116</div>
            <div class="day-content">
              <div class="day-topic"><em>文明重启</em>无线电与远距离通信</div>
              <div class="day-desc">如何将人的声音编码到看不见的电磁波上，跨越重洋重建人类网络？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明重启',this);">文明重启</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('通信',this);">通信</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-116" onclick="toggleNote(116)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(116)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-116"></div>
                <div class="note-display-wrap " id="note-display-wrap-116">
                  <div class="note-display-header" onclick="toggleNoteDisplay(116)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-116"></div>
                </div>
                <div class="note-editor" id="note-editor-116">
                  <textarea class="note-textarea" id="note-ta-116" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(116)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(116)">删除</button>
                    <span class="note-timestamp" id="note-ts-116"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="117" data-tags="前沿科技,文明,能源">
            <div class="day-num " id="daynum-117">D117</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿科技</em>卡尔达肖夫指数</div>
              <div class="day-desc">评估文明等级的终极标尺：掌控行星级能源（I型）、恒星级能源（II型）与星系级能源（III型）。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿科技',this);">前沿科技</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-117" onclick="toggleNote(117)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(117)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-117"></div>
                <div class="note-display-wrap " id="note-display-wrap-117">
                  <div class="note-display-header" onclick="toggleNoteDisplay(117)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-117"></div>
                </div>
                <div class="note-editor" id="note-editor-117">
                  <textarea class="note-textarea" id="note-ta-117" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(117)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(117)">删除</button>
                    <span class="note-timestamp" id="note-ts-117"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="118" data-tags="前沿科技,文明,能源">
            <div class="day-num " id="daynum-118">D118</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿科技</em>戴森球与终极能源</div>
              <div class="day-desc">一个极其宏大的工程构想：用太阳能板把整个恒星包裹起来，彻底榨干它的全部能量。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿科技',this);">前沿科技</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-118" onclick="toggleNote(118)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(118)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-118"></div>
                <div class="note-display-wrap " id="note-display-wrap-118">
                  <div class="note-display-header" onclick="toggleNoteDisplay(118)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-118"></div>
                </div>
                <div class="note-editor" id="note-editor-118">
                  <textarea class="note-textarea" id="note-ta-118" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(118)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(118)">删除</button>
                    <span class="note-timestamp" id="note-ts-118"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="119" data-tags="哲学回归,AI,奇点,技术奇点">
            <div class="day-num " id="daynum-119">D119</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学回归</em>技术奇点与人类终局</div>
              <div class="day-desc">当机器的智力超越人类，进化的主导权将首次从碳基生命转移到硅基生命手中。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学回归',this);">哲学回归</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('奇点',this);">奇点</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('技术奇点',this);">技术奇点</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-119" onclick="toggleNote(119)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(119)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-119"></div>
                <div class="note-display-wrap " id="note-display-wrap-119">
                  <div class="note-display-header" onclick="toggleNoteDisplay(119)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-119"></div>
                </div>
                <div class="note-editor" id="note-editor-119">
                  <textarea class="note-textarea" id="note-ta-119" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(119)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(119)">删除</button>
                    <span class="note-timestamp" id="note-ts-119"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="120" data-tags="大复盘,文明,复盘">
            <div class="day-num " id="daynum-120">D120</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第四月复盘：赛博时代的文明备忘录</div>
              <div class="day-desc">总结技术演化史。如果你要把人类文明的最高智慧刻在一个硬盘上留给后代，你会写下哪10个方程？</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文明',this);">文明</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-120" onclick="toggleNote(120)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(120)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-120"></div>
                <div class="note-display-wrap " id="note-display-wrap-120">
                  <div class="note-display-header" onclick="toggleNoteDisplay(120)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-120"></div>
                </div>
                <div class="note-editor" id="note-editor-120">
                  <textarea class="note-textarea" id="note-ta-120" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(120)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(120)">删除</button>
                    <span class="note-timestamp" id="note-ts-120"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-5">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#a05ac8"></div>
        <div class="module-icon" style="background:#a05ac818; color:#a05ac8">🎨</div>
        <div class="module-meta">
          <div class="module-num">MODULE 05</div>
          <div class="module-title" style="color:#a05ac8">艺术、媒介与视觉美学
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">渲染世界的参数</span>
          </div>
          <div class="module-days" style="color:#a05ac877">艺术史·建筑美学·设计学·媒介理论·符号学·AI美学</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#a05ac844;color:#a05ac899">Day 121–150</span>
          <span class="module-chevron" style="color:#a05ac888">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W21 · 西方绘画史</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="121" data-tags="艺术起源,艺术,美学">
            <div class="day-num " id="daynum-121">D121</div>
            <div class="day-content">
              <div class="day-topic"><em>艺术起源</em>洞穴壁画与原始符号</div>
              <div class="day-desc">艺术不是吃饱了撑的。早期的壁画本质上是远古智人为了生存（打猎）而进行的「虚拟现实（VR）演练」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术起源',this);">艺术起源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-121" onclick="toggleNote(121)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(121)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-121"></div>
                <div class="note-display-wrap " id="note-display-wrap-121">
                  <div class="note-display-header" onclick="toggleNoteDisplay(121)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-121"></div>
                </div>
                <div class="note-editor" id="note-editor-121">
                  <textarea class="note-textarea" id="note-ta-121" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(121)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(121)">删除</button>
                    <span class="note-timestamp" id="note-ts-121"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="122" data-tags="古典美学,艺术,美学,数学">
            <div class="day-num " id="daynum-122">D122</div>
            <div class="day-content">
              <div class="day-topic"><em>古典美学</em>古希腊：黄金分割与比例</div>
              <div class="day-desc">毕达哥拉斯学派的执念：美是可以被精确计算的数学公式。比例与对称如何在视觉上唤起人类底层的安全感。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('古典美学',this);">古典美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-122" onclick="toggleNote(122)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(122)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-122"></div>
                <div class="note-display-wrap " id="note-display-wrap-122">
                  <div class="note-display-header" onclick="toggleNoteDisplay(122)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-122"></div>
                </div>
                <div class="note-editor" id="note-editor-122">
                  <textarea class="note-textarea" id="note-ta-122" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(122)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(122)">删除</button>
                    <span class="note-timestamp" id="note-ts-122"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="123" data-tags="古典美学,艺术,美学">
            <div class="day-num " id="daynum-123">D123</div>
            <div class="day-content">
              <div class="day-topic"><em>古典美学</em>文艺复兴：透视法的降维打击</div>
              <div class="day-desc">人类是如何在二维画布上，通过「消失点」建立一套绝对理性的3D空间坐标系的？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('古典美学',this);">古典美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-123" onclick="toggleNote(123)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(123)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-123"></div>
                <div class="note-display-wrap " id="note-display-wrap-123">
                  <div class="note-display-header" onclick="toggleNoteDisplay(123)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-123"></div>
                </div>
                <div class="note-editor" id="note-editor-123">
                  <textarea class="note-textarea" id="note-ta-123" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(123)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(123)">删除</button>
                    <span class="note-timestamp" id="note-ts-123"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="124" data-tags="古典美学,艺术,光影">
            <div class="day-num " id="daynum-124">D124</div>
            <div class="day-content">
              <div class="day-topic"><em>古典美学</em>光影大师（卡拉瓦乔/伦勃朗）</div>
              <div class="day-desc">绘画界最早的「全局光照（GI）」与「光线追踪」。通过极端的明暗对比来引导观众视觉焦点的控制术。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('古典美学',this);">古典美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('光影',this);">光影</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-124" onclick="toggleNote(124)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(124)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-124"></div>
                <div class="note-display-wrap " id="note-display-wrap-124">
                  <div class="note-display-header" onclick="toggleNoteDisplay(124)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-124"></div>
                </div>
                <div class="note-editor" id="note-editor-124">
                  <textarea class="note-textarea" id="note-ta-124" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(124)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(124)">删除</button>
                    <span class="note-timestamp" id="note-ts-124"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="125" data-tags="现代美学,艺术,美学">
            <div class="day-num " id="daynum-125">D125</div>
            <div class="day-content">
              <div class="day-topic"><em>现代美学</em>印象派：捕捉瞬时光照</div>
              <div class="day-desc">对古典主义的背叛。不再追求物体的「固有色」，只记录特定时间点光子打在视网膜上的瞬间状态。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('现代美学',this);">现代美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-125" onclick="toggleNote(125)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(125)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-125"></div>
                <div class="note-display-wrap " id="note-display-wrap-125">
                  <div class="note-display-header" onclick="toggleNoteDisplay(125)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-125"></div>
                </div>
                <div class="note-editor" id="note-editor-125">
                  <textarea class="note-textarea" id="note-ta-125" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(125)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(125)">删除</button>
                    <span class="note-timestamp" id="note-ts-125"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="126" data-tags="现代美学,艺术,美学">
            <div class="day-num " id="daynum-126">D126</div>
            <div class="day-content">
              <div class="day-topic"><em>现代美学</em>立体主义（毕加索）</div>
              <div class="day-desc">打破单机位限制。尝试在同一张2D平面上，同时渲染一个物体的正面、侧面和顶面——本质上是对四维空间的视觉折叠。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('现代美学',this);">现代美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-126" onclick="toggleNote(126)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(126)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-126"></div>
                <div class="note-display-wrap " id="note-display-wrap-126">
                  <div class="note-display-header" onclick="toggleNoteDisplay(126)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-126"></div>
                </div>
                <div class="note-editor" id="note-editor-126">
                  <textarea class="note-textarea" id="note-ta-126" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(126)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(126)">删除</button>
                    <span class="note-timestamp" id="note-ts-126"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="127" data-tags="交叉学科,艺术,AI,复盘">
            <div class="day-num " id="daynum-127">D127</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：绘画史的「算法迭代」</div>
              <div class="day-desc">人类绘画史从追求「像（高保真渲染）」到「不像（抽象提取）」，这与AI生成图像的逻辑有何异同？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-127" onclick="toggleNote(127)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(127)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-127"></div>
                <div class="note-display-wrap " id="note-display-wrap-127">
                  <div class="note-display-header" onclick="toggleNoteDisplay(127)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-127"></div>
                </div>
                <div class="note-editor" id="note-editor-127">
                  <textarea class="note-textarea" id="note-ta-127" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(127)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(127)">删除</button>
                    <span class="note-timestamp" id="note-ts-127"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W22 · 建筑美学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="128" data-tags="建筑美学,建筑,美学">
            <div class="day-num " id="daynum-128">D128</div>
            <div class="day-content">
              <div class="day-topic"><em>建筑美学</em>古典柱式与承重逻辑</div>
              <div class="day-desc">为什么古希腊神庙长那样？建筑最初的美感完全来源于对重力（物理学）的对抗。形式是被材料强度逼出来的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑美学',this);">建筑美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-128" onclick="toggleNote(128)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(128)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-128"></div>
                <div class="note-display-wrap " id="note-display-wrap-128">
                  <div class="note-display-header" onclick="toggleNoteDisplay(128)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-128"></div>
                </div>
                <div class="note-editor" id="note-editor-128">
                  <textarea class="note-textarea" id="note-ta-128" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(128)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(128)">删除</button>
                    <span class="note-timestamp" id="note-ts-128"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="129" data-tags="建筑美学,建筑,美学">
            <div class="day-num " id="daynum-129">D129</div>
            <div class="day-content">
              <div class="day-topic"><em>建筑美学</em>哥特式建筑的工程奇迹</div>
              <div class="day-desc">飞扶壁、尖肋骨架。这是中世纪最顶尖的「骨骼拓扑结构」优化，为了让墙壁消失、让光线（神性）透进来。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑美学',this);">建筑美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-129" onclick="toggleNote(129)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(129)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-129"></div>
                <div class="note-display-wrap " id="note-display-wrap-129">
                  <div class="note-display-header" onclick="toggleNoteDisplay(129)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-129"></div>
                </div>
                <div class="note-editor" id="note-editor-129">
                  <textarea class="note-textarea" id="note-ta-129" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(129)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(129)">删除</button>
                    <span class="note-timestamp" id="note-ts-129"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="130" data-tags="建筑美学,建筑,设计,美学">
            <div class="day-num " id="daynum-130">D130</div>
            <div class="day-content">
              <div class="day-topic"><em>建筑美学</em>现代主义：形式追随功能</div>
              <div class="day-desc">剥离一切无意义的雕花装饰，只保留最核心的几何体。这不仅是设计法则，更是最高效的组织架构设计原则。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑美学',this);">建筑美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计',this);">设计</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-130" onclick="toggleNote(130)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(130)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-130"></div>
                <div class="note-display-wrap " id="note-display-wrap-130">
                  <div class="note-display-header" onclick="toggleNoteDisplay(130)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-130"></div>
                </div>
                <div class="note-editor" id="note-editor-130">
                  <textarea class="note-textarea" id="note-ta-130" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(130)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(130)">删除</button>
                    <span class="note-timestamp" id="note-ts-130"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="131" data-tags="建筑美学,建筑,权力">
            <div class="day-num " id="daynum-131">D131</div>
            <div class="day-content">
              <div class="day-topic"><em>建筑美学</em>苏维埃巨型建筑</div>
              <div class="day-desc">权力、乌托邦与绝对几何。理解那种粗野主义（Brutalism）和巨大体量带来的压迫感，是如何传达政治意志的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑美学',this);">建筑美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-131" onclick="toggleNote(131)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(131)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-131"></div>
                <div class="note-display-wrap " id="note-display-wrap-131">
                  <div class="note-display-header" onclick="toggleNoteDisplay(131)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-131"></div>
                </div>
                <div class="note-editor" id="note-editor-131">
                  <textarea class="note-textarea" id="note-ta-131" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(131)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(131)">删除</button>
                    <span class="note-timestamp" id="note-ts-131"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="132" data-tags="建筑美学,建筑,美学">
            <div class="day-num " id="daynum-132">D132</div>
            <div class="day-content">
              <div class="day-topic"><em>建筑美学</em>赛博朋克与失控的都市</div>
              <div class="day-desc">High Tech, Low Life。霓虹灯、错乱的管线、密集的贫民窟，如何在3D场景中构建这种极致的废土冲突美感。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑美学',this);">建筑美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-132" onclick="toggleNote(132)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(132)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-132"></div>
                <div class="note-display-wrap " id="note-display-wrap-132">
                  <div class="note-display-header" onclick="toggleNoteDisplay(132)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-132"></div>
                </div>
                <div class="note-editor" id="note-editor-132">
                  <textarea class="note-textarea" id="note-ta-132" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(132)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(132)">删除</button>
                    <span class="note-timestamp" id="note-ts-132"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="133" data-tags="设计美学,设计,美学,信息">
            <div class="day-num " id="daynum-133">D133</div>
            <div class="day-content">
              <div class="day-topic"><em>设计美学</em>极简主义与信息降噪</div>
              <div class="day-desc">减少多边形（Low Poly）的哲学。在信息过载的时代，极致的留白和简化的线条，是抢占用户注意力的最高级策略。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计美学',this);">设计美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计',this);">设计</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-133" onclick="toggleNote(133)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(133)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-133"></div>
                <div class="note-display-wrap " id="note-display-wrap-133">
                  <div class="note-display-header" onclick="toggleNoteDisplay(133)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-133"></div>
                </div>
                <div class="note-editor" id="note-editor-133">
                  <textarea class="note-textarea" id="note-ta-133" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(133)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(133)">删除</button>
                    <span class="note-timestamp" id="note-ts-133"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="134" data-tags="交叉学科,建筑,权力,复盘">
            <div class="day-num " id="daynum-134">D134</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：空间的权力与压迫</div>
              <div class="day-desc">从神庙到巨型重工业建筑，总结空间尺度和材质是如何在潜意识里操纵人类情绪的。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('建筑',this);">建筑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-134" onclick="toggleNote(134)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(134)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-134"></div>
                <div class="note-display-wrap " id="note-display-wrap-134">
                  <div class="note-display-header" onclick="toggleNoteDisplay(134)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-134"></div>
                </div>
                <div class="note-editor" id="note-editor-134">
                  <textarea class="note-textarea" id="note-ta-134" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(134)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(134)">删除</button>
                    <span class="note-timestamp" id="note-ts-134"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W23 · 媒介理论与当代艺术</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="135" data-tags="媒介理论,媒介,信息">
            <div class="day-num " id="daynum-135">D135</div>
            <div class="day-content">
              <div class="day-topic"><em>媒介理论</em>麦克卢汉：媒介即讯息</div>
              <div class="day-desc">真正改变社会的不是电视里播了什么，而是「电视」这个工具本身。媒介重塑了你的思考链路。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介理论',this);">媒介理论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-135" onclick="toggleNote(135)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(135)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-135"></div>
                <div class="note-display-wrap " id="note-display-wrap-135">
                  <div class="note-display-header" onclick="toggleNoteDisplay(135)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-135"></div>
                </div>
                <div class="note-editor" id="note-editor-135">
                  <textarea class="note-textarea" id="note-ta-135" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(135)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(135)">删除</button>
                    <span class="note-timestamp" id="note-ts-135"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="136" data-tags="符号学,信息">
            <div class="day-num " id="daynum-136">D136</div>
            <div class="day-content">
              <div class="day-topic"><em>符号学</em>能指与所指的剥离</div>
              <div class="day-desc">一张玫瑰的图片（能指）如何与浪漫（所指）绑定？理解视觉符号是如何被社会文化强行编码和解读的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('符号学',this);">符号学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-136" onclick="toggleNote(136)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(136)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-136"></div>
                <div class="note-display-wrap " id="note-display-wrap-136">
                  <div class="note-display-header" onclick="toggleNoteDisplay(136)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-136"></div>
                </div>
                <div class="note-editor" id="note-editor-136">
                  <textarea class="note-textarea" id="note-ta-136" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(136)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(136)">删除</button>
                    <span class="note-timestamp" id="note-ts-136"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="137" data-tags="摄影与电影,媒介,认知">
            <div class="day-num " id="daynum-137">D137</div>
            <div class="day-content">
              <div class="day-topic"><em>摄影与电影</em>蒙太奇：时间的剪辑术</div>
              <div class="day-desc">将两段毫不相干的视频拼接在一起，大脑会自动脑补出因果逻辑（库里肖夫效应）。人类大脑「强行建立联系」的漏洞。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('摄影与电影',this);">摄影与电影</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-137" onclick="toggleNote(137)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(137)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-137"></div>
                <div class="note-display-wrap " id="note-display-wrap-137">
                  <div class="note-display-header" onclick="toggleNoteDisplay(137)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-137"></div>
                </div>
                <div class="note-editor" id="note-editor-137">
                  <textarea class="note-textarea" id="note-ta-137" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(137)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(137)">删除</button>
                    <span class="note-timestamp" id="note-ts-137"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="138" data-tags="当代艺术,艺术,符号学">
            <div class="day-num " id="daynum-138">D138</div>
            <div class="day-content">
              <div class="day-topic"><em>当代艺术</em>杜尚的泉与概念艺术</div>
              <div class="day-desc">把小便池放进美术馆。艺术的定义权从「手工技术」彻底变成了「定义语境」。想法和Prompt成了最重要的资产。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('当代艺术',this);">当代艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('符号学',this);">符号学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-138" onclick="toggleNote(138)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(138)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-138"></div>
                <div class="note-display-wrap " id="note-display-wrap-138">
                  <div class="note-display-header" onclick="toggleNoteDisplay(138)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-138"></div>
                </div>
                <div class="note-editor" id="note-editor-138">
                  <textarea class="note-textarea" id="note-ta-138" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(138)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(138)">删除</button>
                    <span class="note-timestamp" id="note-ts-138"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="139" data-tags="波普艺术,媒介,消费">
            <div class="day-num " id="daynum-139">D139</div>
            <div class="day-content">
              <div class="day-topic"><em>波普艺术</em>复制、拼贴与模因（Meme）</div>
              <div class="day-desc">当安迪·沃霍尔开始批量丝网印刷玛丽莲·梦露，艺术失去了光晕，变成了可以被病毒式传播的视觉快消品。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('波普艺术',this);">波普艺术</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('消费',this);">消费</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-139" onclick="toggleNote(139)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(139)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-139"></div>
                <div class="note-display-wrap " id="note-display-wrap-139">
                  <div class="note-display-header" onclick="toggleNoteDisplay(139)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-139"></div>
                </div>
                <div class="note-editor" id="note-editor-139">
                  <textarea class="note-textarea" id="note-ta-139" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(139)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(139)">删除</button>
                    <span class="note-timestamp" id="note-ts-139"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="140" data-tags="前沿美学,AI,潜空间,信息">
            <div class="day-num " id="daynum-140">D140</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿美学</em>潜空间（Latent Space）游历</div>
              <div class="day-desc">AI眼中的世界。理解生成式模型是如何将整个人类视觉历史压缩到一个高维数学空间，并在其中进行「概率漫游」的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿美学',this);">前沿美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('潜空间',this);">潜空间</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-140" onclick="toggleNote(140)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(140)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-140"></div>
                <div class="note-display-wrap " id="note-display-wrap-140">
                  <div class="note-display-header" onclick="toggleNoteDisplay(140)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-140"></div>
                </div>
                <div class="note-editor" id="note-editor-140">
                  <textarea class="note-textarea" id="note-ta-140" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(140)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(140)">删除</button>
                    <span class="note-timestamp" id="note-ts-140"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="141" data-tags="交叉学科,媒介,AI,复盘">
            <div class="day-num " id="daynum-141">D141</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：媒介的进化</div>
              <div class="day-desc">回顾从岩壁雕刻到大模型潜在空间的媒介跳跃。记录你在使用AI出图时，是如何通过调整Seed值在这片空间里「寻宝」的。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-141" onclick="toggleNote(141)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(141)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-141"></div>
                <div class="note-display-wrap " id="note-display-wrap-141">
                  <div class="note-display-header" onclick="toggleNoteDisplay(141)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-141"></div>
                </div>
                <div class="note-editor" id="note-editor-141">
                  <textarea class="note-textarea" id="note-ta-141" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(141)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(141)">删除</button>
                    <span class="note-timestamp" id="note-ts-141"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W24-25 · 艺术终局与第五月复盘</span>
            <span class="week-days-count">9 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="142" data-tags="跨界博弈,消费,美学">
            <div class="day-num " id="daynum-142">D142</div>
            <div class="day-content">
              <div class="day-topic"><em>跨界博弈</em>消费主义下的包装美学</div>
              <div class="day-desc">商品为何要过度包装？理解视觉设计是如何成为一种「心理锚定」工具，强行提升商品在消费者心中的心理溢价的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('跨界博弈',this);">跨界博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('消费',this);">消费</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-142" onclick="toggleNote(142)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(142)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-142"></div>
                <div class="note-display-wrap " id="note-display-wrap-142">
                  <div class="note-display-header" onclick="toggleNoteDisplay(142)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-142"></div>
                </div>
                <div class="note-editor" id="note-editor-142">
                  <textarea class="note-textarea" id="note-ta-142" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(142)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(142)">删除</button>
                    <span class="note-timestamp" id="note-ts-142"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="143" data-tags="跨界博弈,美学">
            <div class="day-num " id="daynum-143">D143</div>
            <div class="day-content">
              <div class="day-topic"><em>跨界博弈</em>丑学（Ugly Aesthetics）</div>
              <div class="day-desc">为什么有时候「审丑」反而能获得巨大流量？理解打破常规美学秩序所带来的瞬间神经刺激与网络传播效应。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('跨界博弈',this);">跨界博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-143" onclick="toggleNote(143)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(143)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-143"></div>
                <div class="note-display-wrap " id="note-display-wrap-143">
                  <div class="note-display-header" onclick="toggleNoteDisplay(143)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-143"></div>
                </div>
                <div class="note-editor" id="note-editor-143">
                  <textarea class="note-textarea" id="note-ta-143" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(143)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(143)">删除</button>
                    <span class="note-timestamp" id="note-ts-143"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="144" data-tags="工具演化,AI,设计">
            <div class="day-num " id="daynum-144">D144</div>
            <div class="day-content">
              <div class="day-topic"><em>工具演化</em>3D软件的底层逻辑</div>
              <div class="day-desc">从网格（Mesh）、材质节点（Material Node）到物理渲染（PBR）。计算机是如何用数学公式极其逼真地欺骗人类眼睛的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('工具演化',this);">工具演化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('设计',this);">设计</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-144" onclick="toggleNote(144)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(144)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-144"></div>
                <div class="note-display-wrap " id="note-display-wrap-144">
                  <div class="note-display-header" onclick="toggleNoteDisplay(144)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-144"></div>
                </div>
                <div class="note-editor" id="note-editor-144">
                  <textarea class="note-textarea" id="note-ta-144" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(144)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(144)">删除</button>
                    <span class="note-timestamp" id="note-ts-144"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="145" data-tags="交互美学,游戏,反馈">
            <div class="day-num " id="daynum-145">D145</div>
            <div class="day-content">
              <div class="day-topic"><em>交互美学</em>游戏引擎的即时反馈</div>
              <div class="day-desc">为什么游戏让人上瘾？它提供了一套极其完美的、基于物理法则和数值体系的「即时行动-反馈」闭环。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交互美学',this);">交互美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('游戏',this);">游戏</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('反馈',this);">反馈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-145" onclick="toggleNote(145)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(145)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-145"></div>
                <div class="note-display-wrap " id="note-display-wrap-145">
                  <div class="note-display-header" onclick="toggleNoteDisplay(145)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-145"></div>
                </div>
                <div class="note-editor" id="note-editor-145">
                  <textarea class="note-textarea" id="note-ta-145" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(145)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(145)">删除</button>
                    <span class="note-timestamp" id="note-ts-145"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="146" data-tags="组织美学,管理学,美学">
            <div class="day-num " id="daynum-146">D146</div>
            <div class="day-content">
              <div class="day-topic"><em>组织美学</em>完美制度的反思</div>
              <div class="day-desc">将美学视角带入对HR的认知中：一个过度完美、没有旷野和冗余的职业轨迹或组织结构，是不是反而非常脆弱且无趣？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织美学',this);">组织美学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('美学',this);">美学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-146" onclick="toggleNote(146)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(146)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-146"></div>
                <div class="note-display-wrap " id="note-display-wrap-146">
                  <div class="note-display-header" onclick="toggleNoteDisplay(146)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-146"></div>
                </div>
                <div class="note-editor" id="note-editor-146">
                  <textarea class="note-textarea" id="note-ta-146" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(146)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(146)">删除</button>
                    <span class="note-timestamp" id="note-ts-146"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="147" data-tags="技术伦理,AI,伦理">
            <div class="day-num " id="daynum-147">D147</div>
            <div class="day-content">
              <div class="day-topic"><em>技术伦理</em>深度伪造与真实性的消亡</div>
              <div class="day-desc">当「眼见为实」这一人类文明最后的底线被AI击穿，社会将如何重建信用体系？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('技术伦理',this);">技术伦理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('伦理',this);">伦理</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-147" onclick="toggleNote(147)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(147)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-147"></div>
                <div class="note-display-wrap " id="note-display-wrap-147">
                  <div class="note-display-header" onclick="toggleNoteDisplay(147)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-147"></div>
                </div>
                <div class="note-editor" id="note-editor-147">
                  <textarea class="note-textarea" id="note-ta-147" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(147)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(147)">删除</button>
                    <span class="note-timestamp" id="note-ts-147"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="148" data-tags="艺术终局,AI,艺术">
            <div class="day-num " id="daynum-148">D148</div>
            <div class="day-content">
              <div class="day-topic"><em>艺术终局</em>碳基与硅基的联合创作</div>
              <div class="day-desc">未来的创作者不再是画匠，而是「文明牧羊人」。我们提出方向、制定审美边界，由机器去填充无穷无尽的细节。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术终局',this);">艺术终局</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('艺术',this);">艺术</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-148" onclick="toggleNote(148)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(148)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-148"></div>
                <div class="note-display-wrap " id="note-display-wrap-148">
                  <div class="note-display-header" onclick="toggleNoteDisplay(148)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-148"></div>
                </div>
                <div class="note-editor" id="note-editor-148">
                  <textarea class="note-textarea" id="note-ta-148" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(148)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(148)">删除</button>
                    <span class="note-timestamp" id="note-ts-148"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="149" data-tags="大一统,哲学">
            <div class="day-num " id="daynum-149">D149</div>
            <div class="day-content">
              <div class="day-topic"><em>大一统</em>发现所有事物内部的运行逻辑</div>
              <div class="day-desc">哲学、物理学、社会学和美学，在最高层面上是相通的。真正的快乐，正是来源于这种内部运作逻辑的发现与迁移。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-149" onclick="toggleNote(149)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(149)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-149"></div>
                <div class="note-display-wrap " id="note-display-wrap-149">
                  <div class="note-display-header" onclick="toggleNoteDisplay(149)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-149"></div>
                </div>
                <div class="note-editor" id="note-editor-149">
                  <textarea class="note-textarea" id="note-ta-149" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(149)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(149)">删除</button>
                    <span class="note-timestamp" id="note-ts-149"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="150" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-150">D150</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第五月复盘：成为文明的「逆向工程」师</div>
              <div class="day-desc">这30天，我们拆解了人类视觉的源代码。至此，你对任何一张图、一座建筑、一个网页的观察，都将深入到其底层的参数逻辑。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-150" onclick="toggleNote(150)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(150)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-150"></div>
                <div class="note-display-wrap " id="note-display-wrap-150">
                  <div class="note-display-header" onclick="toggleNoteDisplay(150)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-150"></div>
                </div>
                <div class="note-editor" id="note-editor-150">
                  <textarea class="note-textarea" id="note-ta-150" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(150)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(150)">删除</button>
                    <span class="note-timestamp" id="note-ts-150"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-6">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#5ac8b4"></div>
        <div class="module-icon" style="background:#5ac8b418; color:#5ac8b4">∞</div>
        <div class="module-meta">
          <div class="module-num">MODULE 06</div>
          <div class="module-title" style="color:#5ac8b4">数学、密码学与复杂系统
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">万物的底层代码</span>
          </div>
          <div class="module-days" style="color:#5ac8b477">数学·逻辑学·统计学·密码学·区块链·网络科学·系统论</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#5ac8b444;color:#5ac8b499">Day 151–180</span>
          <span class="module-chevron" style="color:#5ac8b488">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W26 · 数学基础</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="151" data-tags="数学">
            <div class="day-num " id="daynum-151">D151</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>零与无穷大</div>
              <div class="day-desc">打破日常认知的极限。理解「无」与「无限」这两个极其反直觉的数学概念，是如何推翻人类常识的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-151" onclick="toggleNote(151)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(151)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-151"></div>
                <div class="note-display-wrap " id="note-display-wrap-151">
                  <div class="note-display-header" onclick="toggleNoteDisplay(151)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-151"></div>
                </div>
                <div class="note-editor" id="note-editor-151">
                  <textarea class="note-textarea" id="note-ta-151" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(151)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(151)">删除</button>
                    <span class="note-timestamp" id="note-ts-151"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="152" data-tags="数学,密码学">
            <div class="day-num " id="daynum-152">D152</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>素数：数字的原子</div>
              <div class="day-desc">万物皆数，而素数是构成所有数字的积木。这看似纯粹的数论游戏，却是现代互联网加密通讯的绝对基石。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('密码学',this);">密码学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-152" onclick="toggleNote(152)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(152)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-152"></div>
                <div class="note-display-wrap " id="note-display-wrap-152">
                  <div class="note-display-header" onclick="toggleNoteDisplay(152)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-152"></div>
                </div>
                <div class="note-editor" id="note-editor-152">
                  <textarea class="note-textarea" id="note-ta-152" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(152)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(152)">删除</button>
                    <span class="note-timestamp" id="note-ts-152"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="153" data-tags="数学,AI,线性代数">
            <div class="day-num " id="daynum-153">D153</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>线性代数与高维矩阵</div>
              <div class="day-desc">成千上万个数据同时运算。这是彻底弄懂AI（大语言模型、扩散模型）如何处理庞大信息的底层说明书。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('线性代数',this);">线性代数</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-153" onclick="toggleNote(153)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(153)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-153"></div>
                <div class="note-display-wrap " id="note-display-wrap-153">
                  <div class="note-display-header" onclick="toggleNoteDisplay(153)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-153"></div>
                </div>
                <div class="note-editor" id="note-editor-153">
                  <textarea class="note-textarea" id="note-ta-153" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(153)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(153)">删除</button>
                    <span class="note-timestamp" id="note-ts-153"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="154" data-tags="数学,AI,微积分">
            <div class="day-num " id="daynum-154">D154</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>微积分：捕捉变化的终极武器</div>
              <div class="day-desc">静态的数学无法描述动态的世界。理解导数与极限，你就理解了AI训练时至关重要的「梯度下降」是在干什么。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('微积分',this);">微积分</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-154" onclick="toggleNote(154)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(154)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-154"></div>
                <div class="note-display-wrap " id="note-display-wrap-154">
                  <div class="note-display-header" onclick="toggleNoteDisplay(154)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-154"></div>
                </div>
                <div class="note-editor" id="note-editor-154">
                  <textarea class="note-textarea" id="note-ta-154" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(154)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(154)">删除</button>
                    <span class="note-timestamp" id="note-ts-154"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="155" data-tags="数学,拓扑">
            <div class="day-num " id="daynum-155">D155</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>拓扑学：咖啡杯与甜甜圈</div>
              <div class="day-desc">抛开距离和角度，只关注空间的「连续变形」。这会彻底重塑你对3D网格布线和几何建模的认知。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('拓扑',this);">拓扑</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-155" onclick="toggleNote(155)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(155)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-155"></div>
                <div class="note-display-wrap " id="note-display-wrap-155">
                  <div class="note-display-header" onclick="toggleNoteDisplay(155)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-155"></div>
                </div>
                <div class="note-editor" id="note-editor-155">
                  <textarea class="note-textarea" id="note-ta-155" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(155)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(155)">删除</button>
                    <span class="note-timestamp" id="note-ts-155"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="156" data-tags="数学,复杂系统,分形">
            <div class="day-num " id="daynum-156">D156</div>
            <div class="day-content">
              <div class="day-topic"><em>数学</em>分形几何与混沌的秩序</div>
              <div class="day-desc">大自然不按直线和圆生长。一棵树、一片雪花，其实都是一段极简数学公式在不断「自我递归」和循环。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('分形',this);">分形</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-156" onclick="toggleNote(156)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(156)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-156"></div>
                <div class="note-display-wrap " id="note-display-wrap-156">
                  <div class="note-display-header" onclick="toggleNoteDisplay(156)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-156"></div>
                </div>
                <div class="note-editor" id="note-editor-156">
                  <textarea class="note-textarea" id="note-ta-156" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(156)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(156)">删除</button>
                    <span class="note-timestamp" id="note-ts-156"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="157" data-tags="逻辑学,哲学,逻辑">
            <div class="day-num " id="daynum-157">D157</div>
            <div class="day-content">
              <div class="day-topic"><em>逻辑学</em>哥德尔不完备定理</div>
              <div class="day-desc">理性的终极叹息。任何足够复杂的逻辑系统，都必然存在「既不能被证明，也不能被证伪」的真理。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑学',this);">逻辑学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('逻辑',this);">逻辑</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-157" onclick="toggleNote(157)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(157)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-157"></div>
                <div class="note-display-wrap " id="note-display-wrap-157">
                  <div class="note-display-header" onclick="toggleNoteDisplay(157)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-157"></div>
                </div>
                <div class="note-editor" id="note-editor-157">
                  <textarea class="note-textarea" id="note-ta-157" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(157)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(157)">删除</button>
                    <span class="note-timestamp" id="note-ts-157"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W27 · 统计学与密码学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="158" data-tags="统计学,决策">
            <div class="day-num " id="daynum-158">D158</div>
            <div class="day-content">
              <div class="day-topic"><em>统计学</em>贝叶斯定理：动态更新的智慧</div>
              <div class="day-desc">先给出一个「先验概率」，然后根据不断出现的新证据，动态调整自己的认知。极具实用价值的决策模型。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('统计学',this);">统计学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-158" onclick="toggleNote(158)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(158)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-158"></div>
                <div class="note-display-wrap " id="note-display-wrap-158">
                  <div class="note-display-header" onclick="toggleNoteDisplay(158)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-158"></div>
                </div>
                <div class="note-editor" id="note-editor-158">
                  <textarea class="note-textarea" id="note-ta-158" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(158)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(158)">删除</button>
                    <span class="note-timestamp" id="note-ts-158"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="159" data-tags="统计学">
            <div class="day-num " id="daynum-159">D159</div>
            <div class="day-content">
              <div class="day-topic"><em>统计学</em>大数定律与均值回归</div>
              <div class="day-desc">为什么运气总会用光？为什么极致的高绩效员工极容易在第二年表现平庸？认清数据的引力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('统计学',this);">统计学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-159" onclick="toggleNote(159)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(159)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-159"></div>
                <div class="note-display-wrap " id="note-display-wrap-159">
                  <div class="note-display-header" onclick="toggleNoteDisplay(159)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-159"></div>
                </div>
                <div class="note-editor" id="note-editor-159">
                  <textarea class="note-textarea" id="note-ta-159" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(159)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(159)">删除</button>
                    <span class="note-timestamp" id="note-ts-159"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="160" data-tags="统计学,数据">
            <div class="day-num " id="daynum-160">D160</div>
            <div class="day-content">
              <div class="day-topic"><em>统计学</em>辛普森悖论与数据谎言</div>
              <div class="day-desc">局部数据看起来在增长，汇总到全局却在下跌。警惕那些看似完美、却隐瞒了关键变量的「业务增长报表」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('统计学',this);">统计学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('数据',this);">数据</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-160" onclick="toggleNote(160)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(160)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-160"></div>
                <div class="note-display-wrap " id="note-display-wrap-160">
                  <div class="note-display-header" onclick="toggleNoteDisplay(160)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-160"></div>
                </div>
                <div class="note-editor" id="note-editor-160">
                  <textarea class="note-textarea" id="note-ta-160" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(160)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(160)">删除</button>
                    <span class="note-timestamp" id="note-ts-160"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="161" data-tags="密码学,信息">
            <div class="day-num " id="daynum-161">D161</div>
            <div class="day-content">
              <div class="day-topic"><em>密码学</em>恩尼格玛机与信息战</div>
              <div class="day-desc">战争的胜负不再取决于前线，而取决于后方破译密码的速度。理解信息的加密与解密是如何改变历史走向的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('密码学',this);">密码学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-161" onclick="toggleNote(161)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(161)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-161"></div>
                <div class="note-display-wrap " id="note-display-wrap-161">
                  <div class="note-display-header" onclick="toggleNoteDisplay(161)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-161"></div>
                </div>
                <div class="note-editor" id="note-editor-161">
                  <textarea class="note-textarea" id="note-ta-161" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(161)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(161)">删除</button>
                    <span class="note-timestamp" id="note-ts-161"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="162" data-tags="密码学,信任">
            <div class="day-num " id="daynum-162">D162</div>
            <div class="day-content">
              <div class="day-topic"><em>密码学</em>非对称加密：互联网信任基石</div>
              <div class="day-desc">公开一把锁（公钥）让所有人都能锁上信息，但只有你手里的钥匙（私钥）能打开。陌生人社会的终极信任解法。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('密码学',this);">密码学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信任',this);">信任</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-162" onclick="toggleNote(162)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(162)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-162"></div>
                <div class="note-display-wrap " id="note-display-wrap-162">
                  <div class="note-display-header" onclick="toggleNoteDisplay(162)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-162"></div>
                </div>
                <div class="note-editor" id="note-editor-162">
                  <textarea class="note-textarea" id="note-ta-162" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(162)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(162)">删除</button>
                    <span class="note-timestamp" id="note-ts-162"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="163" data-tags="密码学,哈希,信息">
            <div class="day-num " id="daynum-163">D163</div>
            <div class="day-content">
              <div class="day-topic"><em>密码学</em>哈希函数：数字的唯一指纹</div>
              <div class="day-desc">无论是一句话还是一部100G的电影，经过算法都能变成一段定长的乱码。只要改动一个像素，指纹就会天翻地覆。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('密码学',this);">密码学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哈希',this);">哈希</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-163" onclick="toggleNote(163)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(163)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-163"></div>
                <div class="note-display-wrap " id="note-display-wrap-163">
                  <div class="note-display-header" onclick="toggleNoteDisplay(163)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-163"></div>
                </div>
                <div class="note-editor" id="note-editor-163">
                  <textarea class="note-textarea" id="note-ta-163" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(163)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(163)">删除</button>
                    <span class="note-timestamp" id="note-ts-163"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="164" data-tags="区块链">
            <div class="day-num " id="daynum-164">D164</div>
            <div class="day-content">
              <div class="day-topic"><em>区块链</em>智能合约的无情执行</div>
              <div class="day-desc">将业务流程和契约写进代码。一旦条件触发，程序自动执行，无需任何人际沟通和审批。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区块链',this);">区块链</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-164" onclick="toggleNote(164)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(164)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-164"></div>
                <div class="note-display-wrap " id="note-display-wrap-164">
                  <div class="note-display-header" onclick="toggleNoteDisplay(164)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-164"></div>
                </div>
                <div class="note-editor" id="note-editor-164">
                  <textarea class="note-textarea" id="note-ta-164" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(164)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(164)">删除</button>
                    <span class="note-timestamp" id="note-ts-164"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W28 · 网络科学与系统论</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="165" data-tags="交叉学科,密码学,复盘">
            <div class="day-num " id="daynum-165">D165</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：代码即法律</div>
              <div class="day-desc">构思一个完全由算法、哈希值和智能合约驱动的全自动人事或内容分发系统，它将如何屠宰现有的枯燥流程？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('密码学',this);">密码学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-165" onclick="toggleNote(165)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(165)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-165"></div>
                <div class="note-display-wrap " id="note-display-wrap-165">
                  <div class="note-display-header" onclick="toggleNoteDisplay(165)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-165"></div>
                </div>
                <div class="note-editor" id="note-editor-165">
                  <textarea class="note-textarea" id="note-ta-165" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(165)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(165)">删除</button>
                    <span class="note-timestamp" id="note-ts-165"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="166" data-tags="网络科学,图论">
            <div class="day-num " id="daynum-166">D166</div>
            <div class="day-content">
              <div class="day-topic"><em>网络科学</em>柯尼斯堡七桥问题</div>
              <div class="day-desc">图论的起源。抛弃地理位置，只看「节点」和「边」。理解现实世界中的交通、人际网络如何被抽象成数学图表。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络科学',this);">网络科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('图论',this);">图论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-166" onclick="toggleNote(166)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(166)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-166"></div>
                <div class="note-display-wrap " id="note-display-wrap-166">
                  <div class="note-display-header" onclick="toggleNoteDisplay(166)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-166"></div>
                </div>
                <div class="note-editor" id="note-editor-166">
                  <textarea class="note-textarea" id="note-ta-166" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(166)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(166)">删除</button>
                    <span class="note-timestamp" id="note-ts-166"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="167" data-tags="网络科学,小世界">
            <div class="day-num " id="daynum-167">D167</div>
            <div class="day-content">
              <div class="day-topic"><em>网络科学</em>小世界网络与六度分隔</div>
              <div class="day-desc">为什么你只需通过几个人就能认识世界上的任何人？理解复杂系统中的「捷径」是如何让庞大的网络变得异常紧凑的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络科学',this);">网络科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('小世界',this);">小世界</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-167" onclick="toggleNote(167)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(167)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-167"></div>
                <div class="note-display-wrap " id="note-display-wrap-167">
                  <div class="note-display-header" onclick="toggleNoteDisplay(167)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-167"></div>
                </div>
                <div class="note-editor" id="note-editor-167">
                  <textarea class="note-textarea" id="note-ta-167" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(167)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(167)">删除</button>
                    <span class="note-timestamp" id="note-ts-167"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="168" data-tags="网络科学,幂律,马太效应">
            <div class="day-num " id="daynum-168">D168</div>
            <div class="day-content">
              <div class="day-topic"><em>网络科学</em>标度自由与富者愈富</div>
              <div class="day-desc">网络的发展是不公平的。新节点总是优先连接已经拥有很多连接的「枢纽节点」。破解互联网巨头垄断的底层法则。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('网络科学',this);">网络科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('幂律',this);">幂律</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('马太效应',this);">马太效应</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-168" onclick="toggleNote(168)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(168)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-168"></div>
                <div class="note-display-wrap " id="note-display-wrap-168">
                  <div class="note-display-header" onclick="toggleNoteDisplay(168)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-168"></div>
                </div>
                <div class="note-editor" id="note-editor-168">
                  <textarea class="note-textarea" id="note-ta-168" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(168)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(168)">删除</button>
                    <span class="note-timestamp" id="note-ts-168"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="169" data-tags="系统论,熵,负熵流,耗散结构">
            <div class="day-num " id="daynum-169">D169</div>
            <div class="day-content">
              <div class="day-topic"><em>系统论</em>动态平衡与负熵流</div>
              <div class="day-desc">为什么活着的系统需要不断「吃东西」？理解生命和企业如何在持续消耗能量中维持自身的稳定结构。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('负熵流',this);">负熵流</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('耗散结构',this);">耗散结构</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-169" onclick="toggleNote(169)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(169)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-169"></div>
                <div class="note-display-wrap " id="note-display-wrap-169">
                  <div class="note-display-header" onclick="toggleNoteDisplay(169)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-169"></div>
                </div>
                <div class="note-editor" id="note-editor-169">
                  <textarea class="note-textarea" id="note-ta-169" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(169)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(169)">删除</button>
                    <span class="note-timestamp" id="note-ts-169"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="170" data-tags="系统论,熵,耗散结构">
            <div class="day-num " id="daynum-170">D170</div>
            <div class="day-content">
              <div class="day-topic"><em>系统论</em>耗散结构：在边缘寻找生机</div>
              <div class="day-desc">系统只有在「远离平衡态」且与外界剧烈交换能量时，才能产生新的有序结构。为什么「安逸舒适」的组织往往走向灭亡。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('耗散结构',this);">耗散结构</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-170" onclick="toggleNote(170)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(170)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-170"></div>
                <div class="note-display-wrap " id="note-display-wrap-170">
                  <div class="note-display-header" onclick="toggleNoteDisplay(170)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-170"></div>
                </div>
                <div class="note-editor" id="note-editor-170">
                  <textarea class="note-textarea" id="note-ta-170" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(170)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(170)">删除</button>
                    <span class="note-timestamp" id="note-ts-170"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="171" data-tags="决策学,决策,模拟">
            <div class="day-num " id="daynum-171">D171</div>
            <div class="day-content">
              <div class="day-topic"><em>决策学</em>蒙特卡洛模拟</div>
              <div class="day-desc">算力即暴力。当问题复杂到无法用数学公式解出时，就利用计算机掷千万次骰子，用海量的随机穷举来逼近真相。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策学',this);">决策学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('模拟',this);">模拟</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-171" onclick="toggleNote(171)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(171)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-171"></div>
                <div class="note-display-wrap " id="note-display-wrap-171">
                  <div class="note-display-header" onclick="toggleNoteDisplay(171)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-171"></div>
                </div>
                <div class="note-editor" id="note-editor-171">
                  <textarea class="note-textarea" id="note-ta-171" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(171)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(171)">删除</button>
                    <span class="note-timestamp" id="note-ts-171"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W29-30 · 决策学与第六月复盘</span>
            <span class="week-days-count">9 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="172" data-tags="决策学,决策,金融,风险">
            <div class="day-num " id="daynum-172">D172</div>
            <div class="day-content">
              <div class="day-topic"><em>决策学</em>凯利公式：筹码的数学解</div>
              <div class="day-desc">在胜率确定的情况下，你应该押注多少资金或精力？理解风险控制与收益最大化之间的数学奇点，拒绝盲目梭哈。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策学',this);">决策学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融',this);">金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('风险',this);">风险</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-172" onclick="toggleNote(172)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(172)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-172"></div>
                <div class="note-display-wrap " id="note-display-wrap-172">
                  <div class="note-display-header" onclick="toggleNoteDisplay(172)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-172"></div>
                </div>
                <div class="note-editor" id="note-editor-172">
                  <textarea class="note-textarea" id="note-ta-172" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(172)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(172)">删除</button>
                    <span class="note-timestamp" id="note-ts-172"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="173" data-tags="交叉学科,复杂系统,演化论">
            <div class="day-num " id="daynum-173">D173</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>康威生命游戏（元胞自动机）</div>
              <div class="day-desc">只需要三条极其简单的「邻居生存规则」，就能在一个网格世界里演化出无限复杂的、有生命的移动图案。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复杂系统',this);">复杂系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('演化论',this);">演化论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-173" onclick="toggleNote(173)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(173)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-173"></div>
                <div class="note-display-wrap " id="note-display-wrap-173">
                  <div class="note-display-header" onclick="toggleNoteDisplay(173)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-173"></div>
                </div>
                <div class="note-editor" id="note-editor-173">
                  <textarea class="note-textarea" id="note-ta-173" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(173)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(173)">删除</button>
                    <span class="note-timestamp" id="note-ts-173"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="174" data-tags="信息学,熵,信息论,信息,麦克斯韦">
            <div class="day-num " id="daynum-174">D174</div>
            <div class="day-content">
              <div class="day-topic"><em>信息学</em>麦克斯韦妖与信息即能量</div>
              <div class="day-desc">信息的本质是什么？获取信息，就能让系统从无序变得有序。在这场思想实验里，知识和数据真正等价于物理能量。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息学',this);">信息学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息论',this);">信息论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('麦克斯韦',this);">麦克斯韦</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-174" onclick="toggleNote(174)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(174)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-174"></div>
                <div class="note-display-wrap " id="note-display-wrap-174">
                  <div class="note-display-header" onclick="toggleNoteDisplay(174)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-174"></div>
                </div>
                <div class="note-editor" id="note-editor-174">
                  <textarea class="note-textarea" id="note-ta-174" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(174)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(174)">删除</button>
                    <span class="note-timestamp" id="note-ts-174"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="175" data-tags="心理反思,认知偏差,AI,信息">
            <div class="day-num " id="daynum-175">D175</div>
            <div class="day-content">
              <div class="day-topic"><em>心理反思</em>确认偏误与算法囚笼</div>
              <div class="day-desc">当我们理解了数据的力量，却发现推荐算法正在利用人性的弱点，给我们喂食我们想看的东西。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理反思',this);">心理反思</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-175" onclick="toggleNote(175)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(175)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-175"></div>
                <div class="note-display-wrap " id="note-display-wrap-175">
                  <div class="note-display-header" onclick="toggleNoteDisplay(175)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-175"></div>
                </div>
                <div class="note-editor" id="note-editor-175">
                  <textarea class="note-textarea" id="note-ta-175" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(175)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(175)">删除</button>
                    <span class="note-timestamp" id="note-ts-175"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="176" data-tags="应用迁移,AI,算法,组织">
            <div class="day-num " id="daynum-176">D176</div>
            <div class="day-content">
              <div class="day-topic"><em>应用迁移</em>算法驱动的组织结构</div>
              <div class="day-desc">分析一家完全由数据、API和自动化脚本驱动的现代企业，是如何实现效率极化的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('应用迁移',this);">应用迁移</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('算法',this);">算法</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织',this);">组织</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-176" onclick="toggleNote(176)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(176)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-176"></div>
                <div class="note-display-wrap " id="note-display-wrap-176">
                  <div class="note-display-header" onclick="toggleNoteDisplay(176)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-176"></div>
                </div>
                <div class="note-editor" id="note-editor-176">
                  <textarea class="note-textarea" id="note-ta-176" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(176)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(176)">删除</button>
                    <span class="note-timestamp" id="note-ts-176"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="177" data-tags="前沿视角,AI,潜空间">
            <div class="day-num " id="daynum-177">D177</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿视角</em>潜空间（Latent Space）的漫游</div>
              <div class="day-desc">理解我们在生成图像或音乐时，其实是在一个高维的、由数学公式构成的概率海洋中打捞结果。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿视角',this);">前沿视角</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('潜空间',this);">潜空间</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-177" onclick="toggleNote(177)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(177)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-177"></div>
                <div class="note-display-wrap " id="note-display-wrap-177">
                  <div class="note-display-header" onclick="toggleNoteDisplay(177)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-177"></div>
                </div>
                <div class="note-editor" id="note-editor-177">
                  <textarea class="note-textarea" id="note-ta-177" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(177)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(177)">删除</button>
                    <span class="note-timestamp" id="note-ts-177"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="178" data-tags="前沿视角,AI,数学,光影">
            <div class="day-num " id="daynum-178">D178</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿视角</em>渲染方程的数学本质</div>
              <div class="day-desc">你在屏幕上看到的每一道逼真的光影，本质上都是计算机在极速解算极其复杂的微积分能量传递方程。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿视角',this);">前沿视角</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('数学',this);">数学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('光影',this);">光影</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-178" onclick="toggleNote(178)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(178)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-178"></div>
                <div class="note-display-wrap " id="note-display-wrap-178">
                  <div class="note-display-header" onclick="toggleNoteDisplay(178)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-178"></div>
                </div>
                <div class="note-editor" id="note-editor-178">
                  <textarea class="note-textarea" id="note-ta-178" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(178)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(178)">删除</button>
                    <span class="note-timestamp" id="note-ts-178"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="179" data-tags="大一统">
            <div class="day-num " id="daynum-179">D179</div>
            <div class="day-content">
              <div class="day-topic"><em>大一统</em>寻找多学科的共通参数</div>
              <div class="day-desc">将人力资源管理、3D建模软件、自动化内容分发部署放在同一个数学视角下，找出它们底层共享的逻辑链路。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-179" onclick="toggleNote(179)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(179)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-179"></div>
                <div class="note-display-wrap " id="note-display-wrap-179">
                  <div class="note-display-header" onclick="toggleNoteDisplay(179)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-179"></div>
                </div>
                <div class="note-editor" id="note-editor-179">
                  <textarea class="note-textarea" id="note-ta-179" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(179)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(179)">删除</button>
                    <span class="note-timestamp" id="note-ts-179"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="180" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-180">D180</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第六月复盘：掌握万物的操作台</div>
              <div class="day-desc">180天的旅程过半。世界不再是由表象组成的，在你的眼里，万事万物都已经化为涌动的数据流和严密的算法逻辑。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-180" onclick="toggleNote(180)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(180)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-180"></div>
                <div class="note-display-wrap " id="note-display-wrap-180">
                  <div class="note-display-header" onclick="toggleNoteDisplay(180)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-180"></div>
                </div>
                <div class="note-editor" id="note-editor-180">
                  <textarea class="note-textarea" id="note-ta-180" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(180)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(180)">删除</button>
                    <span class="note-timestamp" id="note-ts-180"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-7">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#c8c85a"></div>
        <div class="module-icon" style="background:#c8c85a18; color:#c8c85a">🌍</div>
        <div class="module-meta">
          <div class="module-num">MODULE 07</div>
          <div class="module-title" style="color:#c8c85a">地缘、资源与大国博弈
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">地球的权力沙盘</span>
          </div>
          <div class="module-days" style="color:#c8c85a77">地缘政治·宏观地理·资源经济·金融霸权·科技地缘·区域分析</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#c8c85a44;color:#c8c85a99">Day 181–210</span>
          <span class="module-chevron" style="color:#c8c85a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W31 · 地缘政治基础</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="181" data-tags="宏观地理,地缘,地理">
            <div class="day-num " id="daynum-181">D181</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观地理</em>地理决定论的幽灵</div>
              <div class="day-desc">为什么文明的差异这么大？山脉如何阻断交通导致语言碎裂，平原如何催生中央集权。地形是人类历史最底层的「物理引擎限制」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观地理',this);">宏观地理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地理',this);">地理</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-181" onclick="toggleNote(181)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(181)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-181"></div>
                <div class="note-display-wrap " id="note-display-wrap-181">
                  <div class="note-display-header" onclick="toggleNoteDisplay(181)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-181"></div>
                </div>
                <div class="note-editor" id="note-editor-181">
                  <textarea class="note-textarea" id="note-ta-181" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(181)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(181)">删除</button>
                    <span class="note-timestamp" id="note-ts-181"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="182" data-tags="地缘政治,地缘,权力">
            <div class="day-num " id="daynum-182">D182</div>
            <div class="day-content">
              <div class="day-topic"><em>地缘政治</em>麦金德「心脏地带」理论</div>
              <div class="day-desc">「谁控制了东欧，谁就控制了心脏地带；谁控制了世界岛，谁就控制了世界。」理解欧亚大陆这块超级棋盘的核心战略眼。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘政治',this);">地缘政治</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-182" onclick="toggleNote(182)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(182)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-182"></div>
                <div class="note-display-wrap " id="note-display-wrap-182">
                  <div class="note-display-header" onclick="toggleNoteDisplay(182)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-182"></div>
                </div>
                <div class="note-editor" id="note-editor-182">
                  <textarea class="note-textarea" id="note-ta-182" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(182)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(182)">删除</button>
                    <span class="note-timestamp" id="note-ts-182"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="183" data-tags="地缘政治,地缘,海权">
            <div class="day-num " id="daynum-183">D183</div>
            <div class="day-content">
              <div class="day-topic"><em>地缘政治</em>马汉「海权论」</div>
              <div class="day-desc">为什么近代霸主（英、美）都是海洋国家？理解海洋不是阻隔，而是摩擦力极小的「超级高速公路」。控制咽喉海峡就等于扼住了全球贸易的咽喉。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘政治',this);">地缘政治</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('海权',this);">海权</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-183" onclick="toggleNote(183)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(183)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-183"></div>
                <div class="note-display-wrap " id="note-display-wrap-183">
                  <div class="note-display-header" onclick="toggleNoteDisplay(183)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-183"></div>
                </div>
                <div class="note-editor" id="note-editor-183">
                  <textarea class="note-textarea" id="note-ta-183" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(183)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(183)">删除</button>
                    <span class="note-timestamp" id="note-ts-183"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="184" data-tags="宏观经济,资源,经济学">
            <div class="day-num " id="daynum-184">D184</div>
            <div class="day-content">
              <div class="day-topic"><em>宏观经济</em>资源诅咒（Resource Curse）</div>
              <div class="day-desc">为什么家里有矿的国家往往陷入贫困和战乱？理解极度单一的高利润资源是如何摧毁一个国家的工业化动力和人才结构的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宏观经济',this);">宏观经济</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('资源',this);">资源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-184" onclick="toggleNote(184)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(184)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-184"></div>
                <div class="note-display-wrap " id="note-display-wrap-184">
                  <div class="note-display-header" onclick="toggleNoteDisplay(184)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-184"></div>
                </div>
                <div class="note-editor" id="note-editor-184">
                  <textarea class="note-textarea" id="note-ta-184" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(184)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(184)">删除</button>
                    <span class="note-timestamp" id="note-ts-184"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="185" data-tags="人口学,人口,社会学">
            <div class="day-num " id="daynum-185">D185</div>
            <div class="day-content">
              <div class="day-topic"><em>人口学</em>人口结构的倒金字塔</div>
              <div class="day-desc">老龄化与少子化的不可逆。从HR的视角看宏观：当一个国家的「劳动力供给池」枯竭，它在国际博弈中的底牌如何被彻底抽空。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人口学',this);">人口学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人口',this);">人口</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-185" onclick="toggleNote(185)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(185)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-185"></div>
                <div class="note-display-wrap " id="note-display-wrap-185">
                  <div class="note-display-header" onclick="toggleNoteDisplay(185)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-185"></div>
                </div>
                <div class="note-editor" id="note-editor-185">
                  <textarea class="note-textarea" id="note-ta-185" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(185)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(185)">删除</button>
                    <span class="note-timestamp" id="note-ts-185"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="186" data-tags="全球化,供应链">
            <div class="day-num " id="daynum-186">D186</div>
            <div class="day-content">
              <div class="day-topic"><em>全球化</em>供应链与海上咽喉</div>
              <div class="day-desc">马六甲、苏伊士、巴拿马。剖析这几个一旦堵塞就能让全球工厂停工的地理Bug。理解现代商业对「准时制（JIT）」物流的极度依赖与脆弱。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('全球化',this);">全球化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('供应链',this);">供应链</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-186" onclick="toggleNote(186)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(186)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-186"></div>
                <div class="note-display-wrap " id="note-display-wrap-186">
                  <div class="note-display-header" onclick="toggleNoteDisplay(186)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-186"></div>
                </div>
                <div class="note-editor" id="note-editor-186">
                  <textarea class="note-textarea" id="note-ta-186" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(186)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(186)">删除</button>
                    <span class="note-timestamp" id="note-ts-186"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="187" data-tags="交叉学科,地缘,复盘">
            <div class="day-num " id="daynum-187">D187</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：物理版图的诅咒</div>
              <div class="day-desc">思考题：如果你在一个3D游戏里设计一个必胜的国家，你会如何设置它的山川河流与矿产分布？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-187" onclick="toggleNote(187)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(187)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-187"></div>
                <div class="note-display-wrap " id="note-display-wrap-187">
                  <div class="note-display-header" onclick="toggleNoteDisplay(187)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-187"></div>
                </div>
                <div class="note-editor" id="note-editor-187">
                  <textarea class="note-textarea" id="note-ta-187" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(187)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(187)">删除</button>
                    <span class="note-timestamp" id="note-ts-187"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W32 · 金融霸权与科技地缘</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="188" data-tags="生态地缘,气候,地缘">
            <div class="day-num " id="daynum-188">D188</div>
            <div class="day-content">
              <div class="day-topic"><em>生态地缘</em>气候变迁与帝国周期</div>
              <div class="day-desc">降水线的微小移动，如何导致游牧民族南下入侵农耕文明。地球恒温器的微调，是如何成为历史朝代更迭的终极催化剂的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生态地缘',this);">生态地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('气候',this);">气候</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-188" onclick="toggleNote(188)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(188)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-188"></div>
                <div class="note-display-wrap " id="note-display-wrap-188">
                  <div class="note-display-header" onclick="toggleNoteDisplay(188)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-188"></div>
                </div>
                <div class="note-editor" id="note-editor-188">
                  <textarea class="note-textarea" id="note-ta-188" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(188)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(188)">删除</button>
                    <span class="note-timestamp" id="note-ts-188"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="189" data-tags="金融霸权,金融,货币,霸权">
            <div class="day-num " id="daynum-189">D189</div>
            <div class="day-content">
              <div class="day-topic"><em>金融霸权</em>石油美元的闭环</div>
              <div class="day-desc">脱离金本位后，美元如何通过绑定全球工业血液（石油）来维持霸权？这是世界上设计得最庞大、最精密的「金融抽水机」系统。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融霸权',this);">金融霸权</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融',this);">金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('货币',this);">货币</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('霸权',this);">霸权</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-189" onclick="toggleNote(189)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(189)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-189"></div>
                <div class="note-display-wrap " id="note-display-wrap-189">
                  <div class="note-display-header" onclick="toggleNoteDisplay(189)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-189"></div>
                </div>
                <div class="note-editor" id="note-editor-189">
                  <textarea class="note-textarea" id="note-ta-189" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(189)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(189)">删除</button>
                    <span class="note-timestamp" id="note-ts-189"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="190" data-tags="科技地缘,AI,科技,地缘">
            <div class="day-num " id="daynum-190">D190</div>
            <div class="day-content">
              <div class="day-topic"><em>科技地缘</em>芯片战争与硅幕降临</div>
              <div class="day-desc">算力即权力。AI时代的石油是半导体。理解光刻机和先进制程为何成了现代国家博弈的核武器。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('科技地缘',this);">科技地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('科技',this);">科技</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-190" onclick="toggleNote(190)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(190)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-190"></div>
                <div class="note-display-wrap " id="note-display-wrap-190">
                  <div class="note-display-header" onclick="toggleNoteDisplay(190)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-190"></div>
                </div>
                <div class="note-editor" id="note-editor-190">
                  <textarea class="note-textarea" id="note-ta-190" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(190)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(190)">删除</button>
                    <span class="note-timestamp" id="note-ts-190"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="191" data-tags="生存底线,粮食,资源">
            <div class="day-num " id="daynum-191">D191</div>
            <div class="day-content">
              <div class="day-topic"><em>生存底线</em>粮食霸权与农业基因</div>
              <div class="day-desc">控制了种子，就控制了人类。拆解四大粮商（ABCD）是如何通过转基因专利和化肥供应链，从最底层的卡路里维度控制全球命脉的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生存底线',this);">生存底线</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('粮食',this);">粮食</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('资源',this);">资源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-191" onclick="toggleNote(191)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(191)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-191"></div>
                <div class="note-display-wrap " id="note-display-wrap-191">
                  <div class="note-display-header" onclick="toggleNoteDisplay(191)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-191"></div>
                </div>
                <div class="note-editor" id="note-editor-191">
                  <textarea class="note-textarea" id="note-ta-191" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(191)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(191)">删除</button>
                    <span class="note-timestamp" id="note-ts-191"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="192" data-tags="能源地图,能源,地缘">
            <div class="day-num " id="daynum-192">D192</div>
            <div class="day-content">
              <div class="day-topic"><em>能源地图</em>从化石到新能源的洗牌</div>
              <div class="day-desc">为什么大家都在疯狂卷电动车和光伏？这不仅是环保问题，更是为了摆脱化石燃料地缘限制，重塑全球能源权力的重新洗牌。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源地图',this);">能源地图</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-192" onclick="toggleNote(192)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(192)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-192"></div>
                <div class="note-display-wrap " id="note-display-wrap-192">
                  <div class="note-display-header" onclick="toggleNoteDisplay(192)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-192"></div>
                </div>
                <div class="note-editor" id="note-editor-192">
                  <textarea class="note-textarea" id="note-ta-192" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(192)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(192)">删除</button>
                    <span class="note-timestamp" id="note-ts-192"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="193" data-tags="跨国组织,权力,全球化">
            <div class="day-num " id="daynum-193">D193</div>
            <div class="day-content">
              <div class="day-topic"><em>跨国组织</em>主权国家 vs 跨国寡头</div>
              <div class="day-desc">当一个科技巨头（如苹果、谷歌）的现金流和用户量超过大多数中等国家时，「国家主权」的边界在哪里？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('跨国组织',this);">跨国组织</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('全球化',this);">全球化</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-193" onclick="toggleNote(193)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(193)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-193"></div>
                <div class="note-display-wrap " id="note-display-wrap-193">
                  <div class="note-display-header" onclick="toggleNoteDisplay(193)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-193"></div>
                </div>
                <div class="note-editor" id="note-editor-193">
                  <textarea class="note-textarea" id="note-ta-193" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(193)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(193)">删除</button>
                    <span class="note-timestamp" id="note-ts-193"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="194" data-tags="交叉学科,地缘,信息,复盘">
            <div class="day-num " id="daynum-194">D194</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：看不见的战争</div>
              <div class="day-desc">战争早已不在战壕里打响，它发生在代码库、SWIFT结算系统、大豆期货市场和极紫外光刻机的图纸上。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-194" onclick="toggleNote(194)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(194)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-194"></div>
                <div class="note-display-wrap " id="note-display-wrap-194">
                  <div class="note-display-header" onclick="toggleNoteDisplay(194)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-194"></div>
                </div>
                <div class="note-editor" id="note-editor-194">
                  <textarea class="note-textarea" id="note-ta-194" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(194)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(194)">删除</button>
                    <span class="note-timestamp" id="note-ts-194"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W33-34 · 区域分析</span>
            <span class="week-days-count">14 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="195" data-tags="信息地缘,互联网,地缘,信息">
            <div class="day-num " id="daynum-195">D195</div>
            <div class="day-content">
              <div class="day-topic"><em>信息地缘</em>海底光缆与数据霸权</div>
              <div class="day-desc">你以为互联网在云端？不，全球95%的跨国数据跑在极其脆弱的海底光缆里。谁控制了这些物理线缆的节点，谁就拥有了「天眼」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息地缘',this);">信息地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('互联网',this);">互联网</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-195" onclick="toggleNote(195)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(195)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-195"></div>
                <div class="note-display-wrap " id="note-display-wrap-195">
                  <div class="note-display-header" onclick="toggleNoteDisplay(195)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-195"></div>
                </div>
                <div class="note-editor" id="note-editor-195">
                  <textarea class="note-textarea" id="note-ta-195" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(195)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(195)">删除</button>
                    <span class="note-timestamp" id="note-ts-195"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="196" data-tags="太空地缘,太空,地缘">
            <div class="day-num " id="daynum-196">D196</div>
            <div class="day-content">
              <div class="day-topic"><em>太空地缘</em>近地轨道与星链系统</div>
              <div class="day-desc">轨道坑位是有限的。理解低轨卫星网络如何彻底无视地面的物理国界，建立起一套覆盖全球的、全新的通信和打击协议。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('太空地缘',this);">太空地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('太空',this);">太空</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-196" onclick="toggleNote(196)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(196)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-196"></div>
                <div class="note-display-wrap " id="note-display-wrap-196">
                  <div class="note-display-header" onclick="toggleNoteDisplay(196)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-196"></div>
                </div>
                <div class="note-editor" id="note-editor-196">
                  <textarea class="note-textarea" id="note-ta-196" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(196)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(196)">删除</button>
                    <span class="note-timestamp" id="note-ts-196"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="197" data-tags="文化博弈,媒介,文化,权力">
            <div class="day-num " id="daynum-197">D197</div>
            <div class="day-content">
              <div class="day-topic"><em>文化博弈</em>软实力与文化输出</div>
              <div class="day-desc">好莱坞和动漫不是单纯的娱乐。它们是最高级的「思想植入工具」，通过塑造「何为美好生活」的标准，兵不血刃地征服受众的大脑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文化博弈',this);">文化博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文化',this);">文化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-197" onclick="toggleNote(197)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(197)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-197"></div>
                <div class="note-display-wrap " id="note-display-wrap-197">
                  <div class="note-display-header" onclick="toggleNoteDisplay(197)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-197"></div>
                </div>
                <div class="note-editor" id="note-editor-197">
                  <textarea class="note-textarea" id="note-ta-197" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(197)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(197)">删除</button>
                    <span class="note-timestamp" id="note-ts-197"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="198" data-tags="国际秩序,全球化,政治学">
            <div class="day-num " id="daynum-198">D198</div>
            <div class="day-content">
              <div class="day-topic"><em>国际秩序</em>联合国与WTO的底层协议</div>
              <div class="day-desc">二战后人类建立的这套「全球操作系统」是如何运行的？以及在逆全球化周期中，这套系统是如何面临崩溃和重构的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('国际秩序',this);">国际秩序</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('全球化',this);">全球化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-198" onclick="toggleNote(198)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(198)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-198"></div>
                <div class="note-display-wrap " id="note-display-wrap-198">
                  <div class="note-display-header" onclick="toggleNoteDisplay(198)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-198"></div>
                </div>
                <div class="note-editor" id="note-editor-198">
                  <textarea class="note-textarea" id="note-ta-198" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(198)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(198)">删除</button>
                    <span class="note-timestamp" id="note-ts-198"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="199" data-tags="博弈手段,博弈,权力">
            <div class="day-num " id="daynum-199">D199</div>
            <div class="day-content">
              <div class="day-topic"><em>博弈手段</em>经济制裁的武器化</div>
              <div class="day-desc">不动用一兵一卒，如何让一个现代国家的工业体系瞬间瘫痪？拆解金融断网与技术封锁背后的杀伤力与反噬效应。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈手段',this);">博弈手段</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-199" onclick="toggleNote(199)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(199)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-199"></div>
                <div class="note-display-wrap " id="note-display-wrap-199">
                  <div class="note-display-header" onclick="toggleNoteDisplay(199)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-199"></div>
                </div>
                <div class="note-editor" id="note-editor-199">
                  <textarea class="note-textarea" id="note-ta-199" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(199)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(199)">删除</button>
                    <span class="note-timestamp" id="note-ts-199"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="200" data-tags="地缘政治,地缘,博弈">
            <div class="day-num " id="daynum-200">D200</div>
            <div class="day-content">
              <div class="day-topic"><em>地缘政治</em>边缘地带与代理人战争</div>
              <div class="day-desc">为什么大国从不直接下场互殴？理解「缓冲区」战略，以及小国如何沦为超级大国测试武器和消耗对手的「演兵场」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘政治',this);">地缘政治</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-200" onclick="toggleNote(200)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(200)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-200"></div>
                <div class="note-display-wrap " id="note-display-wrap-200">
                  <div class="note-display-header" onclick="toggleNoteDisplay(200)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-200"></div>
                </div>
                <div class="note-editor" id="note-editor-200">
                  <textarea class="note-textarea" id="note-ta-200" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(200)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(200)">删除</button>
                    <span class="note-timestamp" id="note-ts-200"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="201" data-tags="交叉学科,地缘,AI,复盘">
            <div class="day-num " id="daynum-201">D201</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：维度的升维打击</div>
              <div class="day-desc">如果你是一个AI公司的CEO，在出海布局时，你要如何应对这些比代码复杂一万倍的地缘政治阻力？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-201" onclick="toggleNote(201)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(201)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-201"></div>
                <div class="note-display-wrap " id="note-display-wrap-201">
                  <div class="note-display-header" onclick="toggleNoteDisplay(201)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-201"></div>
                </div>
                <div class="note-editor" id="note-editor-201">
                  <textarea class="note-textarea" id="note-ta-201" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(201)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(201)">删除</button>
                    <span class="note-timestamp" id="note-ts-201"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="202" data-tags="区域剖析,地缘,政治学">
            <div class="day-num " id="daynum-202">D202</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>欧洲的碎片化与一体化</div>
              <div class="day-desc">为什么欧洲历史就是一部无休止的内战史？理解欧盟试图将几十个主权国家缝合在一起的巨大经济收益与致命的政治阻力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-202" onclick="toggleNote(202)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(202)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-202"></div>
                <div class="note-display-wrap " id="note-display-wrap-202">
                  <div class="note-display-header" onclick="toggleNoteDisplay(202)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-202"></div>
                </div>
                <div class="note-editor" id="note-editor-202">
                  <textarea class="note-textarea" id="note-ta-202" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(202)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(202)">删除</button>
                    <span class="note-timestamp" id="note-ts-202"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="203" data-tags="区域剖析,地缘">
            <div class="day-num " id="daynum-203">D203</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>北美的天选之局</div>
              <div class="day-desc">东西两大洋，南北无强国，内部拥有极其庞大的可航行水系和耕地。从地理参数来看，理解这块大陆自带的「作弊级」防御和发育属性。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-203" onclick="toggleNote(203)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(203)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-203"></div>
                <div class="note-display-wrap " id="note-display-wrap-203">
                  <div class="note-display-header" onclick="toggleNoteDisplay(203)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-203"></div>
                </div>
                <div class="note-editor" id="note-editor-203">
                  <textarea class="note-textarea" id="note-ta-203" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(203)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(203)">删除</button>
                    <span class="note-timestamp" id="note-ts-203"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="204" data-tags="区域剖析,地缘,供应链">
            <div class="day-num " id="daynum-204">D204</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>亚洲的季风与供应链</div>
              <div class="day-desc">极其密集的人口、极度依赖季风的农业，以及如今全球最庞大的「世界工厂」集群。理解东亚怪兽级别的制造产能是如何诞生的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('供应链',this);">供应链</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-204" onclick="toggleNote(204)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(204)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-204"></div>
                <div class="note-display-wrap " id="note-display-wrap-204">
                  <div class="note-display-header" onclick="toggleNoteDisplay(204)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-204"></div>
                </div>
                <div class="note-editor" id="note-editor-204">
                  <textarea class="note-textarea" id="note-ta-204" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(204)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(204)">删除</button>
                    <span class="note-timestamp" id="note-ts-204"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="205" data-tags="区域剖析,地缘,资源,能源">
            <div class="day-num " id="daynum-205">D205</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>中东的战略枢纽诅咒</div>
              <div class="day-desc">连接三大洲的十字路口+地下涌动的石油。极佳的地理位置反而成了它永无宁日的根源，剖析中东地缘的死结。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('资源',this);">资源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('能源',this);">能源</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-205" onclick="toggleNote(205)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(205)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-205"></div>
                <div class="note-display-wrap " id="note-display-wrap-205">
                  <div class="note-display-header" onclick="toggleNoteDisplay(205)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-205"></div>
                </div>
                <div class="note-editor" id="note-editor-205">
                  <textarea class="note-textarea" id="note-ta-205" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(205)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(205)">删除</button>
                    <span class="note-timestamp" id="note-ts-205"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="206" data-tags="区域剖析,地缘,殖民">
            <div class="day-num " id="daynum-206">D206</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>非洲的觉醒与被剥削</div>
              <div class="day-desc">资源极度丰富，为何却极度贫穷？剖析殖民者用直尺画下的国界线，是如何让这片大陆陷入无休止的部落冲突和资源掠夺的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('殖民',this);">殖民</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-206" onclick="toggleNote(206)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(206)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-206"></div>
                <div class="note-display-wrap " id="note-display-wrap-206">
                  <div class="note-display-header" onclick="toggleNoteDisplay(206)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-206"></div>
                </div>
                <div class="note-editor" id="note-editor-206">
                  <textarea class="note-textarea" id="note-ta-206" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(206)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(206)">删除</button>
                    <span class="note-timestamp" id="note-ts-206"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="207" data-tags="区域剖析,经济学,地缘">
            <div class="day-num " id="daynum-207">D207</div>
            <div class="day-content">
              <div class="day-topic"><em>区域剖析</em>拉美的中等收入陷阱</div>
              <div class="day-desc">为什么早早独立、资源丰富的拉美国家，会在达到一定收入水平后集体陷入停滞和混乱？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('区域剖析',this);">区域剖析</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济学',this);">经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-207" onclick="toggleNote(207)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(207)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-207"></div>
                <div class="note-display-wrap " id="note-display-wrap-207">
                  <div class="note-display-header" onclick="toggleNoteDisplay(207)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-207"></div>
                </div>
                <div class="note-editor" id="note-editor-207">
                  <textarea class="note-textarea" id="note-ta-207" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(207)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(207)">删除</button>
                    <span class="note-timestamp" id="note-ts-207"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="208" data-tags="未来地缘,地缘,气候">
            <div class="day-num " id="daynum-208">D208</div>
            <div class="day-content">
              <div class="day-topic"><em>未来地缘</em>极地航道与北极博弈</div>
              <div class="day-desc">随着气候变暖，冰川融化。一条能缩短三分之一航程的「北极航线」即将出现，它将如何彻底改写当下的全球海权版图？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('未来地缘',this);">未来地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('地缘',this);">地缘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('气候',this);">气候</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-208" onclick="toggleNote(208)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(208)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-208"></div>
                <div class="note-display-wrap " id="note-display-wrap-208">
                  <div class="note-display-header" onclick="toggleNoteDisplay(208)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-208"></div>
                </div>
                <div class="note-editor" id="note-editor-208">
                  <textarea class="note-textarea" id="note-ta-208" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(208)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(208)">删除</button>
                    <span class="note-timestamp" id="note-ts-208"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W35 · 第七月复盘</span>
            <span class="week-days-count">2 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="209" data-tags="交叉学科,复盘">
            <div class="day-num " id="daynum-209">D209</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：区域破局的密码</div>
              <div class="day-desc">俯瞰全球六大板块，找找看有没有哪个被忽略的角落，隐藏着下一个时代的爆发节点？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-209" onclick="toggleNote(209)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(209)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-209"></div>
                <div class="note-display-wrap " id="note-display-wrap-209">
                  <div class="note-display-header" onclick="toggleNoteDisplay(209)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-209"></div>
                </div>
                <div class="note-editor" id="note-editor-209">
                  <textarea class="note-textarea" id="note-ta-209" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(209)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(209)">删除</button>
                    <span class="note-timestamp" id="note-ts-209"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="210" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-210">D210</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第七月复盘：成为合格的「地球玩家」</div>
              <div class="day-desc">地理不再是死板的地图，而是利益流动的管道。你现在已经拥有了一双能够看透国际风云变换的「X光眼」。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-210" onclick="toggleNote(210)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(210)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-210"></div>
                <div class="note-display-wrap " id="note-display-wrap-210">
                  <div class="note-display-header" onclick="toggleNoteDisplay(210)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-210"></div>
                </div>
                <div class="note-editor" id="note-editor-210">
                  <textarea class="note-textarea" id="note-ta-210" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(210)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(210)">删除</button>
                    <span class="note-timestamp" id="note-ts-210"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-8">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#c87a5a"></div>
        <div class="module-icon" style="background:#c87a5a18; color:#c87a5a">💰</div>
        <div class="module-meta">
          <div class="module-num">MODULE 08</div>
          <div class="module-title" style="color:#c87a5a">商业帝国、资本流转与组织演化
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">现实世界的「财富引擎」</span>
          </div>
          <div class="module-days" style="color:#c87a5a77">企业本质·财务·资本逻辑·商业演化·组织病理·平台经济</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#c87a5a44;color:#c87a5a99">Day 211–240</span>
          <span class="module-chevron" style="color:#c87a5a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W36 · 企业本质与财务</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="211" data-tags="企业本质,心理学,认知">
            <div class="day-num " id="daynum-211">D211</div>
            <div class="day-content">
              <div class="day-topic"><em>企业本质</em>科斯定理与交易成本</div>
              <div class="day-desc">为什么我们不全都是自由职业者？企业的诞生，本质上是为了用「内部管理成本」去抵消「外部交易成本」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('企业本质',this);">企业本质</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-211" onclick="toggleNote(211)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(211)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-211"></div>
                <div class="note-display-wrap " id="note-display-wrap-211">
                  <div class="note-display-header" onclick="toggleNoteDisplay(211)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-211"></div>
                </div>
                <div class="note-editor" id="note-editor-211">
                  <textarea class="note-textarea" id="note-ta-211" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(211)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(211)">删除</button>
                    <span class="note-timestamp" id="note-ts-211"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="212" data-tags="管理溯源,心理学,动机">
            <div class="day-num " id="daynum-212">D212</div>
            <div class="day-content">
              <div class="day-topic"><em>管理溯源</em>泰勒制与科学管理</div>
              <div class="day-desc">现代职场的底层诅咒。理解一百年前的工厂是如何把人剥夺为机器上的「标准化零件」的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理溯源',this);">管理溯源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('动机',this);">动机</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-212" onclick="toggleNote(212)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(212)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-212"></div>
                <div class="note-display-wrap " id="note-display-wrap-212">
                  <div class="note-display-header" onclick="toggleNoteDisplay(212)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-212"></div>
                </div>
                <div class="note-editor" id="note-editor-212">
                  <textarea class="note-textarea" id="note-ta-212" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(212)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(212)">删除</button>
                    <span class="note-timestamp" id="note-ts-212"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="213" data-tags="财务思维,心理学,创伤">
            <div class="day-num " id="daynum-213">D213</div>
            <div class="day-content">
              <div class="day-topic"><em>财务思维</em>资产负债表的「上帝视角」</div>
              <div class="day-desc">理解一家公司的健康程度，完全取决于它的钱从哪里来（负债/权益），又去了哪里（资产）。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('财务思维',this);">财务思维</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('创伤',this);">创伤</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-213" onclick="toggleNote(213)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(213)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-213"></div>
                <div class="note-display-wrap " id="note-display-wrap-213">
                  <div class="note-display-header" onclick="toggleNoteDisplay(213)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-213"></div>
                </div>
                <div class="note-editor" id="note-editor-213">
                  <textarea class="note-textarea" id="note-ta-213" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(213)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(213)">删除</button>
                    <span class="note-timestamp" id="note-ts-213"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="214" data-tags="财务思维,心理学,意识">
            <div class="day-num " id="daynum-214">D214</div>
            <div class="day-content">
              <div class="day-topic"><em>财务思维</em>现金流：企业的真实血液</div>
              <div class="day-desc">为什么很多账面疯狂盈利的公司会突然倒闭？利润只是会计的「意见」，而现金流才是冰冷的「事实」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('财务思维',this);">财务思维</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-214" onclick="toggleNote(214)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(214)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-214"></div>
                <div class="note-display-wrap " id="note-display-wrap-214">
                  <div class="note-display-header" onclick="toggleNoteDisplay(214)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-214"></div>
                </div>
                <div class="note-editor" id="note-editor-214">
                  <textarea class="note-textarea" id="note-ta-214" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(214)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(214)">删除</button>
                    <span class="note-timestamp" id="note-ts-214"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="215" data-tags="资本逻辑,心理学">
            <div class="day-num " id="daynum-215">D215</div>
            <div class="day-content">
              <div class="day-topic"><em>资本逻辑</em>风险投资（VC）与幂律法则</div>
              <div class="day-desc">为什么资本愿意砸钱让互联网公司无限亏损？VC追求的不是「稳赚」，而是押注那个能带来100倍回报的超级黑马。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('资本逻辑',this);">资本逻辑</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-215" onclick="toggleNote(215)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(215)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-215"></div>
                <div class="note-display-wrap " id="note-display-wrap-215">
                  <div class="note-display-header" onclick="toggleNoteDisplay(215)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-215"></div>
                </div>
                <div class="note-editor" id="note-editor-215">
                  <textarea class="note-textarea" id="note-ta-215" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(215)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(215)">删除</button>
                    <span class="note-timestamp" id="note-ts-215"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="216" data-tags="护城河,心理学,认知偏差">
            <div class="day-num " id="daynum-216">D216</div>
            <div class="day-content">
              <div class="day-topic"><em>护城河</em>垄断的暴利（从0到1）</div>
              <div class="day-desc">竞争是留给失败者的。真正伟大的企业从不竞争，它们通过技术、网络效应或规模经济，直接创造并垄断一个全新的生态位。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('护城河',this);">护城河</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-216" onclick="toggleNote(216)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(216)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-216"></div>
                <div class="note-display-wrap " id="note-display-wrap-216">
                  <div class="note-display-header" onclick="toggleNoteDisplay(216)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-216"></div>
                </div>
                <div class="note-editor" id="note-editor-216">
                  <textarea class="note-textarea" id="note-ta-216" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(216)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(216)">删除</button>
                    <span class="note-timestamp" id="note-ts-216"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="217" data-tags="交叉学科,复盘">
            <div class="day-num " id="daynum-217">D217</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：解剖一头「利润怪兽」</div>
              <div class="day-desc">尝试用资产负债表和交易成本的视角，去拆解你之前待过的公司，或者你正在分析的某个行业巨头。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-217" onclick="toggleNote(217)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(217)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-217"></div>
                <div class="note-display-wrap " id="note-display-wrap-217">
                  <div class="note-display-header" onclick="toggleNoteDisplay(217)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-217"></div>
                </div>
                <div class="note-editor" id="note-editor-217">
                  <textarea class="note-textarea" id="note-ta-217" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(217)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(217)">删除</button>
                    <span class="note-timestamp" id="note-ts-217"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W37 · 商业演化与护城河</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="218" data-tags="商业演化,心理学">
            <div class="day-num " id="daynum-218">D218</div>
            <div class="day-content">
              <div class="day-topic"><em>商业演化</em>创新者的窘境</div>
              <div class="day-desc">为什么极其优秀、管理完美的大公司，注定会被不起眼的新技术颠覆？因为它们被现有的利润基本盘和高端客户彻底「绑架」了。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('商业演化',this);">商业演化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-218" onclick="toggleNote(218)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(218)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-218"></div>
                <div class="note-display-wrap " id="note-display-wrap-218">
                  <div class="note-display-header" onclick="toggleNoteDisplay(218)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-218"></div>
                </div>
                <div class="note-editor" id="note-editor-218">
                  <textarea class="note-textarea" id="note-ta-218" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(218)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(218)">删除</button>
                    <span class="note-timestamp" id="note-ts-218"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="219" data-tags="商业演化,认知偏差,心理学">
            <div class="day-num " id="daynum-219">D219</div>
            <div class="day-content">
              <div class="day-topic"><em>商业演化</em>网络效应的绝对壁垒</div>
              <div class="day-desc">微信、淘宝为什么无法被替代？当一个产品的价值随着用户数量增加而呈指数级暴增时，先发优势将变成绝对的物理壁垒。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('商业演化',this);">商业演化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-219" onclick="toggleNote(219)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(219)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-219"></div>
                <div class="note-display-wrap " id="note-display-wrap-219">
                  <div class="note-display-header" onclick="toggleNoteDisplay(219)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-219"></div>
                </div>
                <div class="note-editor" id="note-editor-219">
                  <textarea class="note-textarea" id="note-ta-219" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(219)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(219)">删除</button>
                    <span class="note-timestamp" id="note-ts-219"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="220" data-tags="商业演化,心理学">
            <div class="day-num " id="daynum-220">D220</div>
            <div class="day-content">
              <div class="day-topic"><em>商业演化</em>规模经济与范围经济</div>
              <div class="day-desc">摊薄固定成本的魔法。理解为什么工厂越大、产品线越广，边际成本就越趋近于零，从而形成对小作坊的降维打击。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('商业演化',this);">商业演化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-220" onclick="toggleNote(220)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(220)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-220"></div>
                <div class="note-display-wrap " id="note-display-wrap-220">
                  <div class="note-display-header" onclick="toggleNoteDisplay(220)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-220"></div>
                </div>
                <div class="note-editor" id="note-editor-220">
                  <textarea class="note-textarea" id="note-ta-220" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(220)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(220)">删除</button>
                    <span class="note-timestamp" id="note-ts-220"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="221" data-tags="商业暗面,心理学">
            <div class="day-num " id="daynum-221">D221</div>
            <div class="day-content">
              <div class="day-topic"><em>商业暗面</em>寻租行为（Rent-seeking）</div>
              <div class="day-desc">不创造任何新财富，仅仅依靠垄断资源、政策壁垒或信息差，强行从系统中切走蛋糕的寄生虫逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('商业暗面',this);">商业暗面</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-221" onclick="toggleNote(221)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(221)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-221"></div>
                <div class="note-display-wrap " id="note-display-wrap-221">
                  <div class="note-display-header" onclick="toggleNoteDisplay(221)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-221"></div>
                </div>
                <div class="note-editor" id="note-editor-221">
                  <textarea class="note-textarea" id="note-ta-221" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(221)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(221)">删除</button>
                    <span class="note-timestamp" id="note-ts-221"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="222" data-tags="商业暗面,心理学,意识">
            <div class="day-num " id="daynum-222">D222</div>
            <div class="day-content">
              <div class="day-topic"><em>商业暗面</em>供应链的「牛鞭效应」</div>
              <div class="day-desc">为什么终端消费的一个微小波动，传导到上游工厂会变成巨大的库存灾难？理解信息在商业链路中传递时的极度失真。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('商业暗面',this);">商业暗面</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('意识',this);">意识</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-222" onclick="toggleNote(222)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(222)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-222"></div>
                <div class="note-display-wrap " id="note-display-wrap-222">
                  <div class="note-display-header" onclick="toggleNoteDisplay(222)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-222"></div>
                </div>
                <div class="note-editor" id="note-editor-222">
                  <textarea class="note-textarea" id="note-ta-222" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(222)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(222)">删除</button>
                    <span class="note-timestamp" id="note-ts-222"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="223" data-tags="价值评估,心理学,神经科学">
            <div class="day-num " id="daynum-223">D223</div>
            <div class="day-content">
              <div class="day-topic"><em>价值评估</em>品牌与无形资产</div>
              <div class="day-desc">为什么贴个Logo就能卖贵十倍？理解「品牌」是如何在消费者大脑中占据极其稀缺的认知带宽，从而转化为真金白银的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('价值评估',this);">价值评估</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('神经科学',this);">神经科学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-223" onclick="toggleNote(223)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(223)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-223"></div>
                <div class="note-display-wrap " id="note-display-wrap-223">
                  <div class="note-display-header" onclick="toggleNoteDisplay(223)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-223"></div>
                </div>
                <div class="note-editor" id="note-editor-223">
                  <textarea class="note-textarea" id="note-ta-223" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(223)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(223)">删除</button>
                    <span class="note-timestamp" id="note-ts-223"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="224" data-tags="交叉学科,心理学,复盘">
            <div class="day-num " id="daynum-224">D224</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：护城河的深浅</div>
              <div class="day-desc">观察你日常使用的各种AI开发工具和平台，分析它们中谁具有真正的「网络效应」，谁又随时可能被开源大模型替代。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-224" onclick="toggleNote(224)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(224)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-224"></div>
                <div class="note-display-wrap " id="note-display-wrap-224">
                  <div class="note-display-header" onclick="toggleNoteDisplay(224)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-224"></div>
                </div>
                <div class="note-editor" id="note-editor-224">
                  <textarea class="note-textarea" id="note-ta-224" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(224)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(224)">删除</button>
                    <span class="note-timestamp" id="note-ts-224"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W38-39 · 组织演化与终极进化</span>
            <span class="week-days-count">15 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="225" data-tags="组织病理,人际,社会学">
            <div class="day-num " id="daynum-225">D225</div>
            <div class="day-content">
              <div class="day-topic"><em>组织病理</em>《狗屁工作》（Bullshit Jobs）</div>
              <div class="day-desc">为什么技术越发达，社会上反而涌现出越多毫无意义的流程、审批和PPT岗位？理解官僚体系自我繁殖的荒谬逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织病理',this);">组织病理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-225" onclick="toggleNote(225)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(225)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-225"></div>
                <div class="note-display-wrap " id="note-display-wrap-225">
                  <div class="note-display-header" onclick="toggleNoteDisplay(225)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-225"></div>
                </div>
                <div class="note-editor" id="note-editor-225">
                  <textarea class="note-textarea" id="note-ta-225" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(225)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(225)">删除</button>
                    <span class="note-timestamp" id="note-ts-225"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="226" data-tags="组织病理,人际,权力">
            <div class="day-num " id="daynum-226">D226</div>
            <div class="day-content">
              <div class="day-topic"><em>组织病理</em>劳动的异化与螺丝钉困境</div>
              <div class="day-desc">马克思的幽灵。当你无法掌握生产工具，且看不到自己工作最终成果的全貌时，工作不仅不带来成就感，反而变成长期的精神损耗。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织病理',this);">组织病理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-226" onclick="toggleNote(226)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(226)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-226"></div>
                <div class="note-display-wrap " id="note-display-wrap-226">
                  <div class="note-display-header" onclick="toggleNoteDisplay(226)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-226"></div>
                </div>
                <div class="note-editor" id="note-editor-226">
                  <textarea class="note-textarea" id="note-ta-226" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(226)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(226)">删除</button>
                    <span class="note-timestamp" id="note-ts-226"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="227" data-tags="组织创新,人际,社会学">
            <div class="day-num " id="daynum-227">D227</div>
            <div class="day-content">
              <div class="day-topic"><em>组织创新</em>稻盛和夫的阿米巴经营</div>
              <div class="day-desc">将庞大的企业彻底击碎成一个个独立核算盈亏的小团队。打破大锅饭，让末端员工直接感受到市场的寒气与利润。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织创新',this);">组织创新</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('社会学',this);">社会学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-227" onclick="toggleNote(227)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(227)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-227"></div>
                <div class="note-display-wrap " id="note-display-wrap-227">
                  <div class="note-display-header" onclick="toggleNoteDisplay(227)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-227"></div>
                </div>
                <div class="note-editor" id="note-editor-227">
                  <textarea class="note-textarea" id="note-ta-227" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(227)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(227)">删除</button>
                    <span class="note-timestamp" id="note-ts-227"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="228" data-tags="平台经济,人际,博弈">
            <div class="day-num " id="daynum-228">D228</div>
            <div class="day-content">
              <div class="day-topic"><em>平台经济</em>零工经济与数字游民</div>
              <div class="day-desc">Uber、外卖平台背后的「平台资本主义」。理解系统是如何通过算法接管传统HR的管理职能，并将风险彻底转嫁给个体的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('平台经济',this);">平台经济</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-228" onclick="toggleNote(228)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(228)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-228"></div>
                <div class="note-display-wrap " id="note-display-wrap-228">
                  <div class="note-display-header" onclick="toggleNoteDisplay(228)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-228"></div>
                </div>
                <div class="note-editor" id="note-editor-228">
                  <textarea class="note-textarea" id="note-ta-228" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(228)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(228)">删除</button>
                    <span class="note-timestamp" id="note-ts-228"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="229" data-tags="权力重构,人际,边界">
            <div class="day-num " id="daynum-229">D229</div>
            <div class="day-content">
              <div class="day-topic"><em>权力重构</em>去中心化自治组织（DAO）</div>
              <div class="day-desc">当「智能合约」代替了管理层，当代币经济代替了工资和期权。设想一种没有老板、完全由代码和共识驱动的极端组织形态。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力重构',this);">权力重构</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('边界',this);">边界</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-229" onclick="toggleNote(229)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(229)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-229"></div>
                <div class="note-display-wrap " id="note-display-wrap-229">
                  <div class="note-display-header" onclick="toggleNoteDisplay(229)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-229"></div>
                </div>
                <div class="note-editor" id="note-editor-229">
                  <textarea class="note-textarea" id="note-ta-229" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(229)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(229)">删除</button>
                    <span class="note-timestamp" id="note-ts-229"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="230" data-tags="生存策略,人际">
            <div class="day-num " id="daynum-230">D230</div>
            <div class="day-content">
              <div class="day-topic"><em>生存策略</em>杠杆与个人商业模式</div>
              <div class="day-desc">普通人出售时间，聪明人出售可无限复制的数字产品，顶尖者利用资本和他人时间作为杠杆。审视你自己的「变现协议」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生存策略',this);">生存策略</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-230" onclick="toggleNote(230)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(230)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-230"></div>
                <div class="note-display-wrap " id="note-display-wrap-230">
                  <div class="note-display-header" onclick="toggleNoteDisplay(230)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-230"></div>
                </div>
                <div class="note-editor" id="note-editor-230">
                  <textarea class="note-textarea" id="note-ta-230" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(230)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(230)">删除</button>
                    <span class="note-timestamp" id="note-ts-230"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="231" data-tags="交叉学科,人际,复盘">
            <div class="day-num " id="daynum-231">D231</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：猎杀形式主义</div>
              <div class="day-desc">结合你对自动化代码部署工具的掌握，构思：如何用AI智能体（Agent）彻底干掉一家公司里80%的「狗屁工作」？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-231" onclick="toggleNote(231)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(231)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-231"></div>
                <div class="note-display-wrap " id="note-display-wrap-231">
                  <div class="note-display-header" onclick="toggleNoteDisplay(231)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-231"></div>
                </div>
                <div class="note-editor" id="note-editor-231">
                  <textarea class="note-textarea" id="note-ta-231" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(231)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(231)">删除</button>
                    <span class="note-timestamp" id="note-ts-231"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="232" data-tags="博弈实战,HR,组织,管理学">
            <div class="day-num " id="daynum-232">D232</div>
            <div class="day-content">
              <div class="day-topic"><em>博弈实战</em>B2B复杂销售与采购逻辑</div>
              <div class="day-desc">To B的生意不是卖产品，而是卖「免责声明」。理解企业采购中极其复杂的决策链条、利益输送与防御性心理。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈实战',this);">博弈实战</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织',this);">组织</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-232" onclick="toggleNote(232)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(232)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-232"></div>
                <div class="note-display-wrap " id="note-display-wrap-232">
                  <div class="note-display-header" onclick="toggleNoteDisplay(232)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-232"></div>
                </div>
                <div class="note-editor" id="note-editor-232">
                  <textarea class="note-textarea" id="note-ta-232" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(232)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(232)">删除</button>
                    <span class="note-timestamp" id="note-ts-232"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="233" data-tags="金融掠夺,HR,招聘">
            <div class="day-num " id="daynum-233">D233</div>
            <div class="day-content">
              <div class="day-topic"><em>金融掠夺</em>杠杆收购（LBO）的野蛮人</div>
              <div class="day-desc">华尔街的终极猎杀。如何仅用极少的本金，通过借债买下一家现金流充沛的公司，然后疯狂裁员、拆分变卖来还债并套现。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('金融掠夺',this);">金融掠夺</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('招聘',this);">招聘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-233" onclick="toggleNote(233)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(233)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-233"></div>
                <div class="note-display-wrap " id="note-display-wrap-233">
                  <div class="note-display-header" onclick="toggleNoteDisplay(233)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-233"></div>
                </div>
                <div class="note-editor" id="note-editor-233">
                  <textarea class="note-textarea" id="note-ta-233" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(233)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(233)">删除</button>
                    <span class="note-timestamp" id="note-ts-233"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="234" data-tags="全球避税,HR,激励,管理学">
            <div class="day-num " id="daynum-234">D234</div>
            <div class="day-content">
              <div class="day-topic"><em>全球避税</em>双层爱尔兰与荷兰三明治</div>
              <div class="day-desc">顶级跨国巨头是如何通过极其复杂的离岸架构、知识产权转移，将数百亿美元的利润合法「洗」到免税天堂的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('全球避税',this);">全球避税</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('激励',this);">激励</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-234" onclick="toggleNote(234)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(234)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-234"></div>
                <div class="note-display-wrap " id="note-display-wrap-234">
                  <div class="note-display-header" onclick="toggleNoteDisplay(234)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-234"></div>
                </div>
                <div class="note-editor" id="note-editor-234">
                  <textarea class="note-textarea" id="note-ta-234" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(234)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(234)">删除</button>
                    <span class="note-timestamp" id="note-ts-234"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="235" data-tags="行为金融,HR,组织,管理学">
            <div class="day-num " id="daynum-235">D235</div>
            <div class="day-content">
              <div class="day-topic"><em>行为金融</em>市场的非理性繁荣</div>
              <div class="day-desc">为什么散户总是追涨杀跌？人类演化出的「羊群效应」和「损失厌恶」，在面对冰冷的金融市场时，是如何变成最致命的缺陷的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('行为金融',this);">行为金融</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('组织',this);">组织</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-235" onclick="toggleNote(235)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(235)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-235"></div>
                <div class="note-display-wrap " id="note-display-wrap-235">
                  <div class="note-display-header" onclick="toggleNoteDisplay(235)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-235"></div>
                </div>
                <div class="note-editor" id="note-editor-235">
                  <textarea class="note-textarea" id="note-ta-235" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(235)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(235)">删除</button>
                    <span class="note-timestamp" id="note-ts-235"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="236" data-tags="终极进化,HR,法学">
            <div class="day-num " id="daynum-236">D236</div>
            <div class="day-content">
              <div class="day-topic"><em>终极进化</em>AI时代的「一人企业」</div>
              <div class="day-desc">当大模型可以代替文案，代码助手可以代替开发，自动化工作流可以代替运营，理解「超级个体」崛起的必然性。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('终极进化',this);">终极进化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('法学',this);">法学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-236" onclick="toggleNote(236)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(236)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-236"></div>
                <div class="note-display-wrap " id="note-display-wrap-236">
                  <div class="note-display-header" onclick="toggleNoteDisplay(236)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-236"></div>
                </div>
                <div class="note-editor" id="note-editor-236">
                  <textarea class="note-textarea" id="note-ta-236" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(236)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(236)">删除</button>
                    <span class="note-timestamp" id="note-ts-236"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="237" data-tags="终极进化,HR,薪酬">
            <div class="day-num " id="daynum-237">D237</div>
            <div class="day-content">
              <div class="day-topic"><em>终极进化</em>边缘创新与「车库精神」</div>
              <div class="day-desc">为什么颠覆性的突破往往不在拥有无限资源的巨头大厦里，而是在那些不受监管、不受KPI束缚的边缘地带爆发。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('终极进化',this);">终极进化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('薪酬',this);">薪酬</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-237" onclick="toggleNote(237)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(237)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-237"></div>
                <div class="note-display-wrap " id="note-display-wrap-237">
                  <div class="note-display-header" onclick="toggleNoteDisplay(237)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-237"></div>
                </div>
                <div class="note-editor" id="note-editor-237">
                  <textarea class="note-textarea" id="note-ta-237" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(237)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(237)">删除</button>
                    <span class="note-timestamp" id="note-ts-237"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="238" data-tags="系统重置,HR,管理学">
            <div class="day-num " id="daynum-238">D238</div>
            <div class="day-content">
              <div class="day-topic"><em>系统重置</em>反脆弱的职业档案</div>
              <div class="day-desc">抛弃「依赖单一系统」的线性简历。学会将自己的能力模块化，在剧烈震荡的失业周期中，建立多条互不干扰的独立收益线。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统重置',this);">系统重置</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-238" onclick="toggleNote(238)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(238)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-238"></div>
                <div class="note-display-wrap " id="note-display-wrap-238">
                  <div class="note-display-header" onclick="toggleNoteDisplay(238)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-238"></div>
                </div>
                <div class="note-editor" id="note-editor-238">
                  <textarea class="note-textarea" id="note-ta-238" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(238)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(238)">删除</button>
                    <span class="note-timestamp" id="note-ts-238"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="239" data-tags="交叉学科,HR,AI,复盘">
            <div class="day-num " id="daynum-239">D239</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：超级个体的武装</div>
              <div class="day-desc">盘点你武器库里的兵器（HR底层逻辑+3D建模能力+自动化工作流部署），计算一下你现在的「个人运转杠杆率」有多高。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('HR',this);">HR</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-239" onclick="toggleNote(239)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(239)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-239"></div>
                <div class="note-display-wrap " id="note-display-wrap-239">
                  <div class="note-display-header" onclick="toggleNoteDisplay(239)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-239"></div>
                </div>
                <div class="note-editor" id="note-editor-239">
                  <textarea class="note-textarea" id="note-ta-239" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(239)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(239)">删除</button>
                    <span class="note-timestamp" id="note-ts-239"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W40 · 第八月复盘</span>
            <span class="week-days-count">1 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="240" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-240">D240</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第八月复盘：看透矩阵（The Matrix）</div>
              <div class="day-desc">这一刻，公司、资本、薪酬体系在你眼中不再是神圣的实体，而仅仅是一堆可以被拆解、被优化的规则代码和资源管道。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-240" onclick="toggleNote(240)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(240)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-240"></div>
                <div class="note-display-wrap " id="note-display-wrap-240">
                  <div class="note-display-header" onclick="toggleNoteDisplay(240)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-240"></div>
                </div>
                <div class="note-editor" id="note-editor-240">
                  <textarea class="note-textarea" id="note-ta-240" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(240)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(240)">删除</button>
                    <span class="note-timestamp" id="note-ts-240"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-9">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#8ac8c8"></div>
        <div class="module-icon" style="background:#8ac8c818; color:#8ac8c8">🔤</div>
        <div class="module-meta">
          <div class="module-num">MODULE 09</div>
          <div class="module-title" style="color:#8ac8c8">语言、符号与思想架构
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">心智的「编译语言」</span>
          </div>
          <div class="module-days" style="color:#8ac8c877">语言起源·认知语言学·符号学·修辞学·话语权力·叙事学</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#8ac8c844;color:#8ac8c899">Day 241–270</span>
          <span class="module-chevron" style="color:#8ac8c888">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W41 · 语言起源与结构</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="241" data-tags="语言起源,语言,符号学">
            <div class="day-num " id="daynum-241">D241</div>
            <div class="day-content">
              <div class="day-topic"><em>语言起源</em>聊八卦与虚构的能力</div>
              <div class="day-desc">为什么只有智人统治了地球？我们的语言不仅能描述「河边有狮子」（事实），还能描述「河神会发怒」（虚构），从而组织起亿万人的协作。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言起源',this);">语言起源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('符号学',this);">符号学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-241" onclick="toggleNote(241)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(241)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-241"></div>
                <div class="note-display-wrap " id="note-display-wrap-241">
                  <div class="note-display-header" onclick="toggleNoteDisplay(241)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-241"></div>
                </div>
                <div class="note-editor" id="note-editor-241">
                  <textarea class="note-textarea" id="note-ta-241" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(241)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(241)">删除</button>
                    <span class="note-timestamp" id="note-ts-241"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="242" data-tags="认知语言学,语言,认知">
            <div class="day-num " id="daynum-242">D242</div>
            <div class="day-content">
              <div class="day-topic"><em>认知语言学</em>萨丕尔-沃尔夫假说</div>
              <div class="day-desc">你的母语物理性地限制了你的世界观。如果一个部落的语言里没有「明天」这个词，他们就真的无法理解储蓄和规划的概念。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知语言学',this);">认知语言学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-242" onclick="toggleNote(242)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(242)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-242"></div>
                <div class="note-display-wrap " id="note-display-wrap-242">
                  <div class="note-display-header" onclick="toggleNoteDisplay(242)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-242"></div>
                </div>
                <div class="note-editor" id="note-editor-242">
                  <textarea class="note-textarea" id="note-ta-242" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(242)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(242)">删除</button>
                    <span class="note-timestamp" id="note-ts-242"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="243" data-tags="结构主义,语言,符号学">
            <div class="day-num " id="daynum-243">D243</div>
            <div class="day-content">
              <div class="day-topic"><em>结构主义</em>索绪尔的语言网络</div>
              <div class="day-desc">词语本身没有任何绝对意义。意义只存在于词与词之间的「差异网络」中。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('结构主义',this);">结构主义</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('符号学',this);">符号学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-243" onclick="toggleNote(243)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(243)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-243"></div>
                <div class="note-display-wrap " id="note-display-wrap-243">
                  <div class="note-display-header" onclick="toggleNoteDisplay(243)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-243"></div>
                </div>
                <div class="note-editor" id="note-editor-243">
                  <textarea class="note-textarea" id="note-ta-243" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(243)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(243)">删除</button>
                    <span class="note-timestamp" id="note-ts-243"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="244" data-tags="语用学,语言">
            <div class="day-num " id="daynum-244">D244</div>
            <div class="day-content">
              <div class="day-topic"><em>语用学</em>言语行为理论（Speech Acts）</div>
              <div class="day-desc">语言不仅描述世界，还能「物理性地改变世界」。比如法官说「我宣布你们结为夫妻」，这句话一旦说出，现实的法律关系瞬间重构。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('语用学',this);">语用学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-244" onclick="toggleNote(244)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(244)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-244"></div>
                <div class="note-display-wrap " id="note-display-wrap-244">
                  <div class="note-display-header" onclick="toggleNoteDisplay(244)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-244"></div>
                </div>
                <div class="note-editor" id="note-editor-244">
                  <textarea class="note-textarea" id="note-ta-244" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(244)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(244)">删除</button>
                    <span class="note-timestamp" id="note-ts-244"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="245" data-tags="模因论,模因,语言,信息">
            <div class="day-num " id="daynum-245">D245</div>
            <div class="day-content">
              <div class="day-topic"><em>模因论</em>语言的自私基因（Meme）</div>
              <div class="day-desc">为什么有些洗脑神曲或网络烂梗能像病毒一样劫持你的大脑？思想也是一种寄生物，它们会利用你的嘴巴进行自我繁殖。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('模因论',this);">模因论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('模因',this);">模因</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-245" onclick="toggleNote(245)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(245)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-245"></div>
                <div class="note-display-wrap " id="note-display-wrap-245">
                  <div class="note-display-header" onclick="toggleNoteDisplay(245)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-245"></div>
                </div>
                <div class="note-editor" id="note-editor-245">
                  <textarea class="note-textarea" id="note-ta-245" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(245)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(245)">删除</button>
                    <span class="note-timestamp" id="note-ts-245"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="246" data-tags="隐喻机制,语言,认知,隐喻">
            <div class="day-num " id="daynum-246">D246</div>
            <div class="day-content">
              <div class="day-topic"><em>隐喻机制</em>我们赖以生存的隐喻</div>
              <div class="day-desc">「争论是战争」、「时间是金钱」。人类极其缺乏抽象思考能力，所有高级复杂的概念，底层全部是建立在简单的身体物理隐喻之上的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('隐喻机制',this);">隐喻机制</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('隐喻',this);">隐喻</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-246" onclick="toggleNote(246)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(246)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-246"></div>
                <div class="note-display-wrap " id="note-display-wrap-246">
                  <div class="note-display-header" onclick="toggleNoteDisplay(246)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-246"></div>
                </div>
                <div class="note-editor" id="note-editor-246">
                  <textarea class="note-textarea" id="note-ta-246" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(246)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(246)">删除</button>
                    <span class="note-timestamp" id="note-ts-246"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="247" data-tags="交叉学科,语言,复盘">
            <div class="day-num " id="daynum-247">D247</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：审视「职场黑话」</div>
              <div class="day-desc">挑出你以前做HR时最讨厌的5个词（如赋能、抓手、闭环），拆解它们是如何通过「隐喻」来掩盖管理无能和压榨本质的。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-247" onclick="toggleNote(247)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(247)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-247"></div>
                <div class="note-display-wrap " id="note-display-wrap-247">
                  <div class="note-display-header" onclick="toggleNoteDisplay(247)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-247"></div>
                </div>
                <div class="note-editor" id="note-editor-247">
                  <textarea class="note-textarea" id="note-ta-247" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(247)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(247)">删除</button>
                    <span class="note-timestamp" id="note-ts-247"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W42 · AI语言学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="248" data-tags="符号学,媒介">
            <div class="day-num " id="daynum-248">D248</div>
            <div class="day-content">
              <div class="day-topic"><em>符号学</em>罗兰·巴特的神话学</div>
              <div class="day-desc">一张照片、一件衣服、一杯咖啡，是如何被偷偷塞进意识形态「私货」的？破解消费社会是如何用视觉符号给你洗脑的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('符号学',this);">符号学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-248" onclick="toggleNote(248)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(248)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-248"></div>
                <div class="note-display-wrap " id="note-display-wrap-248">
                  <div class="note-display-header" onclick="toggleNoteDisplay(248)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-248"></div>
                </div>
                <div class="note-editor" id="note-editor-248">
                  <textarea class="note-textarea" id="note-ta-248" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(248)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(248)">删除</button>
                    <span class="note-timestamp" id="note-ts-248"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="249" data-tags="计算语言学,语言,AI,认知">
            <div class="day-num " id="daynum-249">D249</div>
            <div class="day-content">
              <div class="day-topic"><em>计算语言学</em>乔姆斯基的普遍语法</div>
              <div class="day-desc">极其硬核的假设：人类大脑里是不是天生就插着一块「语法芯片」？为什么小孩子不用学语法就能自动说出复杂的长句？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('计算语言学',this);">计算语言学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-249" onclick="toggleNote(249)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(249)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-249"></div>
                <div class="note-display-wrap " id="note-display-wrap-249">
                  <div class="note-display-header" onclick="toggleNoteDisplay(249)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-249"></div>
                </div>
                <div class="note-editor" id="note-editor-249">
                  <textarea class="note-textarea" id="note-ta-249" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(249)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(249)">删除</button>
                    <span class="note-timestamp" id="note-ts-249"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="250" data-tags="自然语言处理,AI,语言,词向量">
            <div class="day-num " id="daynum-250">D250</div>
            <div class="day-content">
              <div class="day-topic"><em>自然语言处理</em>词向量（Word2Vec）</div>
              <div class="day-desc">AI时代的必修课。机器如何把抽象的词汇变成多维空间里的数学坐标？（国王 - 男人 + 女人 = 女王，语言变成了纯粹的几何距离）</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('自然语言处理',this);">自然语言处理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('词向量',this);">词向量</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-250" onclick="toggleNote(250)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(250)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-250"></div>
                <div class="note-display-wrap " id="note-display-wrap-250">
                  <div class="note-display-header" onclick="toggleNoteDisplay(250)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-250"></div>
                </div>
                <div class="note-editor" id="note-editor-250">
                  <textarea class="note-textarea" id="note-ta-250" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(250)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(250)">删除</button>
                    <span class="note-timestamp" id="note-ts-250"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="251" data-tags="大模型原理,AI,大模型,语言">
            <div class="day-num " id="daynum-251">D251</div>
            <div class="day-content">
              <div class="day-topic"><em>大模型原理</em>Token的物理机制</div>
              <div class="day-desc">为什么AI不懂「字」，只懂「Token」？揭开大语言模型（如ChatGPT、Claude）做文字接龙的底层概率学真相。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大模型原理',this);">大模型原理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大模型',this);">大模型</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-251" onclick="toggleNote(251)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(251)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-251"></div>
                <div class="note-display-wrap " id="note-display-wrap-251">
                  <div class="note-display-header" onclick="toggleNoteDisplay(251)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-251"></div>
                </div>
                <div class="note-editor" id="note-editor-251">
                  <textarea class="note-textarea" id="note-ta-251" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(251)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(251)">删除</button>
                    <span class="note-timestamp" id="note-ts-251"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="252" data-tags="翻译哲学,语言,文化">
            <div class="day-num " id="daynum-252">D252</div>
            <div class="day-content">
              <div class="day-topic"><em>翻译哲学</em>语言的不可译性</div>
              <div class="day-desc">为什么最高级的诗歌和最深的幽默，永远无法跨语言完美传输？语言的底层绑定了极其深厚的局部历史经验。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('翻译哲学',this);">翻译哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文化',this);">文化</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-252" onclick="toggleNote(252)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(252)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-252"></div>
                <div class="note-display-wrap " id="note-display-wrap-252">
                  <div class="note-display-header" onclick="toggleNoteDisplay(252)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-252"></div>
                </div>
                <div class="note-editor" id="note-editor-252">
                  <textarea class="note-textarea" id="note-ta-252" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(252)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(252)">删除</button>
                    <span class="note-timestamp" id="note-ts-252"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="253" data-tags="信息损耗,信息,沟通,信息论">
            <div class="day-num " id="daynum-253">D253</div>
            <div class="day-content">
              <div class="day-topic"><em>信息损耗</em>编码与解码的漏斗效应</div>
              <div class="day-desc">为什么你说明白了，对方却听不懂？信息在两个碳基大脑间传输时，要经过「我想-我说-他听-他懂」四层严重的降噪衰减。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息损耗',this);">信息损耗</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('沟通',this);">沟通</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息论',this);">信息论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-253" onclick="toggleNote(253)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(253)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-253"></div>
                <div class="note-display-wrap " id="note-display-wrap-253">
                  <div class="note-display-header" onclick="toggleNoteDisplay(253)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-253"></div>
                </div>
                <div class="note-editor" id="note-editor-253">
                  <textarea class="note-textarea" id="note-ta-253" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(253)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(253)">删除</button>
                    <span class="note-timestamp" id="note-ts-253"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="254" data-tags="交叉学科,AI,语言,复盘">
            <div class="day-num " id="daynum-254">D254</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：提示词工程师的觉醒</div>
              <div class="day-desc">用NLP词向量的逻辑，重新审视你用来生成3D模型和图像的Prompt。如何用「机器的语言习惯」去控制机器，而不是用人类的废话。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-254" onclick="toggleNote(254)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(254)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-254"></div>
                <div class="note-display-wrap " id="note-display-wrap-254">
                  <div class="note-display-header" onclick="toggleNoteDisplay(254)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-254"></div>
                </div>
                <div class="note-editor" id="note-editor-254">
                  <textarea class="note-textarea" id="note-ta-254" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(254)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(254)">删除</button>
                    <span class="note-timestamp" id="note-ts-254"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W43-44 · 修辞·权力话语·叙事</span>
            <span class="week-days-count">14 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="255" data-tags="修辞学,修辞,权力">
            <div class="day-num " id="daynum-255">D255</div>
            <div class="day-content">
              <div class="day-topic"><em>修辞学</em>亚里士多德的三大诉诸</div>
              <div class="day-desc">说服他人的终极公式：Ethos（人格信用）、Pathos（情感共鸣）、Logos（逻辑推理）。缺一不可的操控术。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('修辞学',this);">修辞学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('修辞',this);">修辞</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-255" onclick="toggleNote(255)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(255)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-255"></div>
                <div class="note-display-wrap " id="note-display-wrap-255">
                  <div class="note-display-header" onclick="toggleNoteDisplay(255)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-255"></div>
                </div>
                <div class="note-editor" id="note-editor-255">
                  <textarea class="note-textarea" id="note-ta-255" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(255)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(255)">删除</button>
                    <span class="note-timestamp" id="note-ts-255"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="256" data-tags="权力话语,权力,话语">
            <div class="day-num " id="daynum-256">D256</div>
            <div class="day-content">
              <div class="day-topic"><em>权力话语</em>福柯的监狱与疯人院</div>
              <div class="day-desc">谁掌握了「精神病」、「罪犯」和「正常」的定义权，谁就掌握了社会的绝对控制权。话语权就是最顶级的暴力。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力话语',this);">权力话语</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('话语',this);">话语</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-256" onclick="toggleNote(256)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(256)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-256"></div>
                <div class="note-display-wrap " id="note-display-wrap-256">
                  <div class="note-display-header" onclick="toggleNoteDisplay(256)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-256"></div>
                </div>
                <div class="note-editor" id="note-editor-256">
                  <textarea class="note-textarea" id="note-ta-256" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(256)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(256)">删除</button>
                    <span class="note-timestamp" id="note-ts-256"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="257" data-tags="宣传学,权力,心理学">
            <div class="day-num " id="daynum-257">D257</div>
            <div class="day-content">
              <div class="day-topic"><em>宣传学</em>群体洗脑术与戈培尔效应</div>
              <div class="day-desc">极简的口号、不断地重复。为什么越反智、越极端的语言，在群体中的煽动性反而越强？（警惕任何口号式的管理标语）</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宣传学',this);">宣传学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-257" onclick="toggleNote(257)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(257)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-257"></div>
                <div class="note-display-wrap " id="note-display-wrap-257">
                  <div class="note-display-header" onclick="toggleNoteDisplay(257)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-257"></div>
                </div>
                <div class="note-editor" id="note-editor-257">
                  <textarea class="note-textarea" id="note-ta-257" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(257)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(257)">删除</button>
                    <span class="note-timestamp" id="note-ts-257"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="258" data-tags="政治正确,政治学,语言,权力">
            <div class="day-num " id="daynum-258">D258</div>
            <div class="day-content">
              <div class="day-topic"><em>政治正确</em>《1984》的新话（Newspeak）</div>
              <div class="day-desc">现实版的思想阉割：如果你把字典里「造反」这个词彻底删掉，人们还能造反吗？词汇库的缩小等同于思维带宽的萎缩。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治正确',this);">政治正确</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('政治学',this);">政治学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-258" onclick="toggleNote(258)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(258)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-258"></div>
                <div class="note-display-wrap " id="note-display-wrap-258">
                  <div class="note-display-header" onclick="toggleNoteDisplay(258)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-258"></div>
                </div>
                <div class="note-editor" id="note-editor-258">
                  <textarea class="note-textarea" id="note-ta-258" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(258)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(258)">删除</button>
                    <span class="note-timestamp" id="note-ts-258"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="259" data-tags="心理学,幽默">
            <div class="day-num " id="daynum-259">D259</div>
            <div class="day-content">
              <div class="day-topic"><em>心理学</em>幽默与笑的底层机制</div>
              <div class="day-desc">乖讧论与预期失调：为什么我们会笑？那是大脑的预期被建立，然后突然被打破时，系统给予的一种认知补偿奖励。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('幽默',this);">幽默</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-259" onclick="toggleNote(259)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(259)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-259"></div>
                <div class="note-display-wrap " id="note-display-wrap-259">
                  <div class="note-display-header" onclick="toggleNoteDisplay(259)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-259"></div>
                </div>
                <div class="note-editor" id="note-editor-259">
                  <textarea class="note-textarea" id="note-ta-259" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(259)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(259)">删除</button>
                    <span class="note-timestamp" id="note-ts-259"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="260" data-tags="叙事学,叙事,模因">
            <div class="day-num " id="daynum-260">D260</div>
            <div class="day-content">
              <div class="day-topic"><em>叙事学</em>英雄之旅（The Hero's Journey）</div>
              <div class="day-desc">为什么好莱坞大片和神话故事，底层的剧情公式几千年来一模一样？掌握这套公式，你就掌握了打造爆款内容的终极说明书。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('叙事学',this);">叙事学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('叙事',this);">叙事</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('模因',this);">模因</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-260" onclick="toggleNote(260)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(260)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-260"></div>
                <div class="note-display-wrap " id="note-display-wrap-260">
                  <div class="note-display-header" onclick="toggleNoteDisplay(260)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-260"></div>
                </div>
                <div class="note-editor" id="note-editor-260">
                  <textarea class="note-textarea" id="note-ta-260" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(260)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(260)">删除</button>
                    <span class="note-timestamp" id="note-ts-260"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="261" data-tags="交叉学科,语言,权力,复盘">
            <div class="day-num " id="daynum-261">D261</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：解剖老板的演讲稿</div>
              <div class="day-desc">用这周学的修辞和权力话语理论，去解剖一篇充斥着「画大饼」的内部演讲稿。你会发现它漏洞百出，全是情绪操控的套路。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('权力',this);">权力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-261" onclick="toggleNote(261)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(261)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-261"></div>
                <div class="note-display-wrap " id="note-display-wrap-261">
                  <div class="note-display-header" onclick="toggleNoteDisplay(261)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-261"></div>
                </div>
                <div class="note-editor" id="note-editor-261">
                  <textarea class="note-textarea" id="note-ta-261" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(261)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(261)">删除</button>
                    <span class="note-timestamp" id="note-ts-261"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="262" data-tags="媒介变迁,媒介,记忆">
            <div class="day-num " id="daynum-262">D262</div>
            <div class="day-content">
              <div class="day-topic"><em>媒介变迁</em>文字对记忆的剥夺</div>
              <div class="day-desc">柏拉图的古老担忧：为什么文字的发明让人类记忆力急速衰退，却让文明得以指数级累积和保存？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介变迁',this);">媒介变迁</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('记忆',this);">记忆</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-262" onclick="toggleNote(262)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(262)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-262"></div>
                <div class="note-display-wrap " id="note-display-wrap-262">
                  <div class="note-display-header" onclick="toggleNoteDisplay(262)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-262"></div>
                </div>
                <div class="note-editor" id="note-editor-262">
                  <textarea class="note-textarea" id="note-ta-262" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(262)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(262)">删除</button>
                    <span class="note-timestamp" id="note-ts-262"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="263" data-tags="视觉语言,媒介,认知">
            <div class="day-num " id="daynum-263">D263</div>
            <div class="day-content">
              <div class="day-topic"><em>视觉语言</em>从抽象退回直觉</div>
              <div class="day-desc">短视频时代的退化：我们是如何从需要深度脑力解析的「抽象文字逻辑」，退化回猴子般条件反射的「视觉多巴胺刺激」的？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('视觉语言',this);">视觉语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('媒介',this);">媒介</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-263" onclick="toggleNote(263)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(263)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-263"></div>
                <div class="note-display-wrap " id="note-display-wrap-263">
                  <div class="note-display-header" onclick="toggleNoteDisplay(263)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-263"></div>
                </div>
                <div class="note-editor" id="note-editor-263">
                  <textarea class="note-textarea" id="note-ta-263" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(263)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(263)">删除</button>
                    <span class="note-timestamp" id="note-ts-263"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="264" data-tags="身体语言,心理学,沟通">
            <div class="day-num " id="daynum-264">D264</div>
            <div class="day-content">
              <div class="day-topic"><em>身体语言</em>测谎与微表情代码</div>
              <div class="day-desc">90%的信息传递不靠嘴。理解面部肌肉和肢体动作中无法掩饰的潜意识代码，这是看透人际伪装的X光。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('身体语言',this);">身体语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('沟通',this);">沟通</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-264" onclick="toggleNote(264)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(264)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-264"></div>
                <div class="note-display-wrap " id="note-display-wrap-264">
                  <div class="note-display-header" onclick="toggleNoteDisplay(264)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-264"></div>
                </div>
                <div class="note-editor" id="note-editor-264">
                  <textarea class="note-textarea" id="note-ta-264" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(264)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(264)">删除</button>
                    <span class="note-timestamp" id="note-ts-264"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="265" data-tags="文化语境,文化,沟通">
            <div class="day-num " id="daynum-265">D265</div>
            <div class="day-content">
              <div class="day-topic"><em>文化语境</em>高语境与低语境</div>
              <div class="day-desc">为什么东方的沟通「尽在不言中」（高语境），而西方的沟通必须「契约写死」（低语境）？跨国协作和沟通的终极鸿沟。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('文化语境',this);">文化语境</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('文化',this);">文化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('沟通',this);">沟通</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-265" onclick="toggleNote(265)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(265)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-265"></div>
                <div class="note-display-wrap " id="note-display-wrap-265">
                  <div class="note-display-header" onclick="toggleNoteDisplay(265)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-265"></div>
                </div>
                <div class="note-editor" id="note-editor-265">
                  <textarea class="note-textarea" id="note-ta-265" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(265)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(265)">删除</button>
                    <span class="note-timestamp" id="note-ts-265"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="266" data-tags="哲学,语言">
            <div class="day-num " id="daynum-266">D266</div>
            <div class="day-content">
              <div class="day-topic"><em>哲学</em>维特根斯坦的叹息</div>
              <div class="day-desc">「我的语言的界限，就是我的世界的界限。凡是不可言说的，必须保持沉默。」承认人类表达能力的终极天花板。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-266" onclick="toggleNote(266)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(266)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-266"></div>
                <div class="note-display-wrap " id="note-display-wrap-266">
                  <div class="note-display-header" onclick="toggleNoteDisplay(266)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-266"></div>
                </div>
                <div class="note-editor" id="note-editor-266">
                  <textarea class="note-textarea" id="note-ta-266" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(266)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(266)">删除</button>
                    <span class="note-timestamp" id="note-ts-266"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="267" data-tags="存在主义,哲学,孤独">
            <div class="day-num " id="daynum-267">D267</div>
            <div class="day-content">
              <div class="day-topic"><em>存在主义</em>沟通的终极悲剧与孤独</div>
              <div class="day-desc">无论语言多么精确，你永远无法将自己的痛感、快乐或迷茫100%地传递给另一个人。我们被永远锁死在自己的头骨里。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('存在主义',this);">存在主义</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('孤独',this);">孤独</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-267" onclick="toggleNote(267)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(267)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-267"></div>
                <div class="note-display-wrap " id="note-display-wrap-267">
                  <div class="note-display-header" onclick="toggleNoteDisplay(267)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-267"></div>
                </div>
                <div class="note-editor" id="note-editor-267">
                  <textarea class="note-textarea" id="note-ta-267" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(267)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(267)">删除</button>
                    <span class="note-timestamp" id="note-ts-267"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="268" data-tags="人机交互,AI,脑机,语言">
            <div class="day-num " id="daynum-268">D268</div>
            <div class="day-content">
              <div class="day-topic"><em>人机交互</em>脑机接口（BCI）的未来</div>
              <div class="day-desc">如果我们能直接通过意念交换神经信号，语言这种低效、容易产生误解的协议会被彻底淘汰吗？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人机交互',this);">人机交互</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('脑机',this);">脑机</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-268" onclick="toggleNote(268)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(268)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-268"></div>
                <div class="note-display-wrap " id="note-display-wrap-268">
                  <div class="note-display-header" onclick="toggleNoteDisplay(268)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-268"></div>
                </div>
                <div class="note-editor" id="note-editor-268">
                  <textarea class="note-textarea" id="note-ta-268" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(268)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(268)">删除</button>
                    <span class="note-timestamp" id="note-ts-268"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W45 · 第九月复盘</span>
            <span class="week-days-count">2 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="269" data-tags="交叉学科,语言,复盘">
            <div class="day-num " id="daynum-269">D269</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：低能耗的防御工具</div>
              <div class="day-desc">在你极度厌恶的「无效社交」中，如何把语言从「真心话」转变为一种极低能耗的、格式化的防御和破冰工具？</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('语言',this);">语言</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-269" onclick="toggleNote(269)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(269)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-269"></div>
                <div class="note-display-wrap " id="note-display-wrap-269">
                  <div class="note-display-header" onclick="toggleNoteDisplay(269)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-269"></div>
                </div>
                <div class="note-editor" id="note-editor-269">
                  <textarea class="note-textarea" id="note-ta-269" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(269)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(269)">删除</button>
                    <span class="note-timestamp" id="note-ts-269"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="270" data-tags="大复盘,复盘">
            <div class="day-num " id="daynum-270">D270</div>
            <div class="day-content">
              <div class="day-topic"><em>大复盘</em>第九月复盘：万物皆为文本</div>
              <div class="day-desc">掌握了语言和符号的源代码，你就不再是被流行词汇操纵的提线木偶，而是现实逻辑的重构者。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大复盘',this);">大复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-270" onclick="toggleNote(270)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(270)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-270"></div>
                <div class="note-display-wrap " id="note-display-wrap-270">
                  <div class="note-display-header" onclick="toggleNoteDisplay(270)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-270"></div>
                </div>
                <div class="note-editor" id="note-editor-270">
                  <textarea class="note-textarea" id="note-ta-270" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(270)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(270)">删除</button>
                    <span class="note-timestamp" id="note-ts-270"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div><div class="module" id="module-10">
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:#c8a07a"></div>
        <div class="module-icon" style="background:#c8a07a18; color:#c8a07a">🎯</div>
        <div class="module-meta">
          <div class="module-num">MODULE 10</div>
          <div class="module-title" style="color:#c8a07a">心智算法·未来视野·大一统闭环
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">个体破局的底层代码</span>
          </div>
          <div class="module-days" style="color:#c8a07a77">行为经济学·决策科学·未来科技·大一统验证·个人重构</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:#c8a07a44;color:#c8a07a99">Day 271–365</span>
          <span class="module-chevron" style="color:#c8a07a88">▶</span>
        </div>
      </div>
      <div class="weeks">
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W46 · 行为经济学与决策科学</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="271" data-tags="行为经济学,认知偏差,决策">
            <div class="day-num " id="daynum-271">D271</div>
            <div class="day-content">
              <div class="day-topic"><em>行为经济学</em>锚定效应（Anchoring）</div>
              <div class="day-desc">为什么第一印象或第一个报价会锁死后续所有的谈判？理解大脑在缺乏信息时，是如何死死抓住任意一个随机数字作为参照物的。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('行为经济学',this);">行为经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-271" onclick="toggleNote(271)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(271)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-271"></div>
                <div class="note-display-wrap " id="note-display-wrap-271">
                  <div class="note-display-header" onclick="toggleNoteDisplay(271)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-271"></div>
                </div>
                <div class="note-editor" id="note-editor-271">
                  <textarea class="note-textarea" id="note-ta-271" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(271)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(271)">删除</button>
                    <span class="note-timestamp" id="note-ts-271"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="272" data-tags="行为经济学,认知偏差,决策">
            <div class="day-num " id="daynum-272">D272</div>
            <div class="day-content">
              <div class="day-topic"><em>行为经济学</em>前景理论与损失厌恶</div>
              <div class="day-desc">捡到100块的快乐，远远抵消不了丢掉100块的痛苦。理解为什么在面对职业转型时，人们总是极度抗拒离开「安全区」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('行为经济学',this);">行为经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-272" onclick="toggleNote(272)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(272)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-272"></div>
                <div class="note-display-wrap " id="note-display-wrap-272">
                  <div class="note-display-header" onclick="toggleNoteDisplay(272)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-272"></div>
                </div>
                <div class="note-editor" id="note-editor-272">
                  <textarea class="note-textarea" id="note-ta-272" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(272)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(272)">删除</button>
                    <span class="note-timestamp" id="note-ts-272"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="273" data-tags="行为经济学,认知偏差">
            <div class="day-num " id="daynum-273">D273</div>
            <div class="day-content">
              <div class="day-topic"><em>行为经济学</em>禀赋效应（Endowment Effect）</div>
              <div class="day-desc">为什么一旦你拥有了某样东西（比如一个鸡肋的岗位），你对它的估值就会莫名其妙地变高？拆解「敝帚自珍」的非理性逻辑。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('行为经济学',this);">行为经济学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-273" onclick="toggleNote(273)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(273)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-273"></div>
                <div class="note-display-wrap " id="note-display-wrap-273">
                  <div class="note-display-header" onclick="toggleNoteDisplay(273)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-273"></div>
                </div>
                <div class="note-editor" id="note-editor-273">
                  <textarea class="note-textarea" id="note-ta-273" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(273)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(273)">删除</button>
                    <span class="note-timestamp" id="note-ts-273"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="274" data-tags="决策科学,决策,认知偏差">
            <div class="day-num " id="daynum-274">D274</div>
            <div class="day-content">
              <div class="day-topic"><em>决策科学</em>沉没成本谬误</div>
              <div class="day-desc">过去投入的时间和金钱，都是无法收回的「死钱」。理性的决策应该只看「未来的收益」。如何果断斩断一条走不通的代码链路或错误规划。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策科学',this);">决策科学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-274" onclick="toggleNote(274)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(274)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-274"></div>
                <div class="note-display-wrap " id="note-display-wrap-274">
                  <div class="note-display-header" onclick="toggleNoteDisplay(274)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-274"></div>
                </div>
                <div class="note-editor" id="note-editor-274">
                  <textarea class="note-textarea" id="note-ta-274" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(274)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(274)">删除</button>
                    <span class="note-timestamp" id="note-ts-274"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="275" data-tags="认知偏差,统计学">
            <div class="day-num " id="daynum-275">D275</div>
            <div class="day-content">
              <div class="day-topic"><em>认知偏差</em>幸存者偏差</div>
              <div class="day-desc">死人不会说话。为什么你看到的成功学或爆款项目都是骗人的？因为你根本没看到那99%遵循同样逻辑却死在水底的失败者。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('统计学',this);">统计学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-275" onclick="toggleNote(275)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(275)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-275"></div>
                <div class="note-display-wrap " id="note-display-wrap-275">
                  <div class="note-display-header" onclick="toggleNoteDisplay(275)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-275"></div>
                </div>
                <div class="note-editor" id="note-editor-275">
                  <textarea class="note-textarea" id="note-ta-275" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(275)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(275)">删除</button>
                    <span class="note-timestamp" id="note-ts-275"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="276" data-tags="认知偏差">
            <div class="day-num " id="daynum-276">D276</div>
            <div class="day-content">
              <div class="day-topic"><em>认知偏差</em>达克效应（Dunning-Kruger Effect）</div>
              <div class="day-desc">越无知的人越自信，越专业的人越自我怀疑。警惕那种「我已掌握全貌」的愚昧之巅幻觉。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知偏差',this);">认知偏差</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-276" onclick="toggleNote(276)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(276)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-276"></div>
                <div class="note-display-wrap " id="note-display-wrap-276">
                  <div class="note-display-header" onclick="toggleNoteDisplay(276)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-276"></div>
                </div>
                <div class="note-editor" id="note-editor-276">
                  <textarea class="note-textarea" id="note-ta-276" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(276)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(276)">删除</button>
                    <span class="note-timestamp" id="note-ts-276"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="277" data-tags="交叉学科,决策,复盘">
            <div class="day-num " id="daynum-277">D277</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：大脑的Bug清单</div>
              <div class="day-desc">盘点过去一年里，你因为「损失厌恶」或「沉没成本」而拖延去做的一项重要决定。现在用冷酷的算法逻辑重新审视它。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-277" onclick="toggleNote(277)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(277)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-277"></div>
                <div class="note-display-wrap " id="note-display-wrap-277">
                  <div class="note-display-header" onclick="toggleNoteDisplay(277)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-277"></div>
                </div>
                <div class="note-editor" id="note-editor-277">
                  <textarea class="note-textarea" id="note-ta-277" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(277)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(277)">删除</button>
                    <span class="note-timestamp" id="note-ts-277"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W47-48 · 决策模型与心智管理</span>
            <span class="week-days-count">13 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="278" data-tags="决策模型,决策,探索与利用">
            <div class="day-num " id="daynum-278">D278</div>
            <div class="day-content">
              <div class="day-topic"><em>决策模型</em>探索与利用困境（Explore vs. Exploit）</div>
              <div class="day-desc">吃饭是去老字号（利用已知高收益），还是去试新店（探索未知可能）？如何分配「死磕旧技能」与「尝试新插件」的数学时间比。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策模型',this);">决策模型</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('探索与利用',this);">探索与利用</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-278" onclick="toggleNote(278)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(278)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-278"></div>
                <div class="note-display-wrap " id="note-display-wrap-278">
                  <div class="note-display-header" onclick="toggleNoteDisplay(278)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-278"></div>
                </div>
                <div class="note-editor" id="note-editor-278">
                  <textarea class="note-textarea" id="note-ta-278" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(278)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(278)">删除</button>
                    <span class="note-timestamp" id="note-ts-278"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="279" data-tags="决策模型,决策,逆向思维">
            <div class="day-num " id="daynum-279">D279</div>
            <div class="day-content">
              <div class="day-topic"><em>决策模型</em>逆向思维（Inversion）</div>
              <div class="day-desc">查理·芒格的绝招：如果你不知道怎么做才能成功，那就先列出所有会导致你失败的事情，然后死死避开它们。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策模型',this);">决策模型</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('逆向思维',this);">逆向思维</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-279" onclick="toggleNote(279)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(279)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-279"></div>
                <div class="note-display-wrap " id="note-display-wrap-279">
                  <div class="note-display-header" onclick="toggleNoteDisplay(279)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-279"></div>
                </div>
                <div class="note-editor" id="note-editor-279">
                  <textarea class="note-textarea" id="note-ta-279" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(279)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(279)">删除</button>
                    <span class="note-timestamp" id="note-ts-279"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="280" data-tags="概率思维,决策,概率,风险">
            <div class="day-num " id="daynum-280">D280</div>
            <div class="day-content">
              <div class="day-topic"><em>概率思维</em>期望值计算与底线思维</div>
              <div class="day-desc">不看单次输赢，只算长期期望。在选择投入精力去做一个新项目时，如何计算它长期的复利价值是否大于单次的痛苦折磨。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('概率思维',this);">概率思维</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('概率',this);">概率</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('风险',this);">风险</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-280" onclick="toggleNote(280)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(280)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-280"></div>
                <div class="note-display-wrap " id="note-display-wrap-280">
                  <div class="note-display-header" onclick="toggleNoteDisplay(280)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-280"></div>
                </div>
                <div class="note-editor" id="note-editor-280">
                  <textarea class="note-textarea" id="note-ta-280" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(280)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(280)">删除</button>
                    <span class="note-timestamp" id="note-ts-280"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="281" data-tags="信息过滤,信息,认知,噪声">
            <div class="day-num " id="daynum-281">D281</div>
            <div class="day-content">
              <div class="day-topic"><em>信息过滤</em>信号与噪声</div>
              <div class="day-desc">为什么每天刷到海量的新AI工具会让人极度焦虑？因为99%是换汤不换药的噪声。学会关闭感官，只捕捉底层的技术「信号」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息过滤',this);">信息过滤</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('认知',this);">认知</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('噪声',this);">噪声</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-281" onclick="toggleNote(281)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(281)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-281"></div>
                <div class="note-display-wrap " id="note-display-wrap-281">
                  <div class="note-display-header" onclick="toggleNoteDisplay(281)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-281"></div>
                </div>
                <div class="note-editor" id="note-editor-281">
                  <textarea class="note-textarea" id="note-ta-281" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(281)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(281)">删除</button>
                    <span class="note-timestamp" id="note-ts-281"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="282" data-tags="心智管理,心理学,边界">
            <div class="day-num " id="daynum-282">D282</div>
            <div class="day-content">
              <div class="day-topic"><em>心智管理</em>课题分离（阿德勒心理学）</div>
              <div class="day-desc">「别人怎么评价我，那是别人的课题；我怎么做事，是我的课题。」这是在物理和心理层面，屠宰无意义人际内耗的终极武器。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('心智管理',this);">心智管理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('边界',this);">边界</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-282" onclick="toggleNote(282)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(282)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-282"></div>
                <div class="note-display-wrap " id="note-display-wrap-282">
                  <div class="note-display-header" onclick="toggleNoteDisplay(282)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-282"></div>
                </div>
                <div class="note-editor" id="note-editor-282">
                  <textarea class="note-textarea" id="note-ta-282" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(282)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(282)">删除</button>
                    <span class="note-timestamp" id="note-ts-282"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="283" data-tags="个体心理,心理学">
            <div class="day-num " id="daynum-283">D283</div>
            <div class="day-content">
              <div class="day-topic"><em>个体心理</em>习得性无助与归因理论</div>
              <div class="day-desc">为什么大象会被一根细绳拴住？理解系统性的打击是如何摧毁个体的反抗意志的，以及如何通过微小的「可控感」重新夺回生活的主导权。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('个体心理',this);">个体心理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心理学',this);">心理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-283" onclick="toggleNote(283)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(283)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-283"></div>
                <div class="note-display-wrap " id="note-display-wrap-283">
                  <div class="note-display-header" onclick="toggleNoteDisplay(283)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-283"></div>
                </div>
                <div class="note-editor" id="note-editor-283">
                  <textarea class="note-textarea" id="note-ta-283" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(283)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(283)">删除</button>
                    <span class="note-timestamp" id="note-ts-283"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="284" data-tags="交叉学科,决策,复盘">
            <div class="day-num " id="daynum-284">D284</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：冷酷的概率玩家</div>
              <div class="day-desc">结合这周的决策模型，为你正在进行的「多线并行学习计划」设定一个数学上的止损点和收益期望值。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-284" onclick="toggleNote(284)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(284)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-284"></div>
                <div class="note-display-wrap " id="note-display-wrap-284">
                  <div class="note-display-header" onclick="toggleNoteDisplay(284)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-284"></div>
                </div>
                <div class="note-editor" id="note-editor-284">
                  <textarea class="note-textarea" id="note-ta-284" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(284)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(284)">删除</button>
                    <span class="note-timestamp" id="note-ts-284"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="285" data-tags="深度状态,心流">
            <div class="day-num " id="daynum-285">D285</div>
            <div class="day-content">
              <div class="day-topic"><em>深度状态</em>心流理论（Flow）</div>
              <div class="day-desc">为什么在调整3D模型参数或Vibe Coding时，几个小时会瞬间消失？理解挑战与技能绝对匹配时，大脑进入的那种极致免打扰的狂喜状态。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('深度状态',this);">深度状态</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('心流',this);">心流</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-285" onclick="toggleNote(285)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(285)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-285"></div>
                <div class="note-display-wrap " id="note-display-wrap-285">
                  <div class="note-display-header" onclick="toggleNoteDisplay(285)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-285"></div>
                </div>
                <div class="note-editor" id="note-editor-285">
                  <textarea class="note-textarea" id="note-ta-285" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(285)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(285)">删除</button>
                    <span class="note-timestamp" id="note-ts-285"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="286" data-tags="技能习得,学习,刻意练习">
            <div class="day-num " id="daynum-286">D286</div>
            <div class="day-content">
              <div class="day-topic"><em>技能习得</em>刻意练习（Deliberate Practice）</div>
              <div class="day-desc">为什么单纯的重复毫无意义？真正的精进需要走出舒适区、建立高度专注的反馈循环，并对内部运作逻辑进行极其痛苦的「拆解重组」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('技能习得',this);">技能习得</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('学习',this);">学习</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('刻意练习',this);">刻意练习</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-286" onclick="toggleNote(286)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(286)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-286"></div>
                <div class="note-display-wrap " id="note-display-wrap-286">
                  <div class="note-display-header" onclick="toggleNoteDisplay(286)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-286"></div>
                </div>
                <div class="note-editor" id="note-editor-286">
                  <textarea class="note-textarea" id="note-ta-286" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(286)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(286)">删除</button>
                    <span class="note-timestamp" id="note-ts-286"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="287" data-tags="系统习惯,习惯,身份认同">
            <div class="day-num " id="daynum-287">D287</div>
            <div class="day-content">
              <div class="day-topic"><em>系统习惯</em>身份认同与微小习惯</div>
              <div class="day-desc">改变行为的最高境界不是设定目标（「我要学编程」），而是改变身份认同（「我是一个通过代码解决问题的人」）。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统习惯',this);">系统习惯</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('习惯',this);">习惯</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('身份认同',this);">身份认同</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-287" onclick="toggleNote(287)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(287)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-287"></div>
                <div class="note-display-wrap " id="note-display-wrap-287">
                  <div class="note-display-header" onclick="toggleNoteDisplay(287)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-287"></div>
                </div>
                <div class="note-editor" id="note-editor-287">
                  <textarea class="note-textarea" id="note-ta-287" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(287)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(287)">删除</button>
                    <span class="note-timestamp" id="note-ts-287"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="288" data-tags="精力管理,精力,系统">
            <div class="day-num " id="daynum-288">D288</div>
            <div class="day-content">
              <div class="day-topic"><em>精力管理</em>能量节律与抗压防线</div>
              <div class="day-desc">时间管理是伪命题，精力管理才是真相。如何根据自己的生理波峰波谷，来安排高强度的逻辑推演与低强度的机械性日常任务。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('精力管理',this);">精力管理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('精力',this);">精力</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统',this);">系统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-288" onclick="toggleNote(288)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(288)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-288"></div>
                <div class="note-display-wrap " id="note-display-wrap-288">
                  <div class="note-display-header" onclick="toggleNoteDisplay(288)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-288"></div>
                </div>
                <div class="note-editor" id="note-editor-288">
                  <textarea class="note-textarea" id="note-ta-288" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(288)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(288)">删除</button>
                    <span class="note-timestamp" id="note-ts-288"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="289" data-tags="人际博弈,人际,博弈">
            <div class="day-num " id="daynum-289">D289</div>
            <div class="day-content">
              <div class="day-topic"><em>人际博弈</em>关系中的权力与边界</div>
              <div class="day-desc">无效社交的本质是缺乏核心交换价值。如何通过建立不可替代的「硬核技术杠杆」，让繁琐的职场人际关系变得毫无必要。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际博弈',this);">人际博弈</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('人际',this);">人际</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('博弈',this);">博弈</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-289" onclick="toggleNote(289)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(289)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-289"></div>
                <div class="note-display-wrap " id="note-display-wrap-289">
                  <div class="note-display-header" onclick="toggleNoteDisplay(289)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-289"></div>
                </div>
                <div class="note-editor" id="note-editor-289">
                  <textarea class="note-textarea" id="note-ta-289" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(289)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(289)">删除</button>
                    <span class="note-timestamp" id="note-ts-289"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="290" data-tags="沟通模型,沟通,信息">
            <div class="day-num " id="daynum-290">D290</div>
            <div class="day-content">
              <div class="day-topic"><em>沟通模型</em>非暴力沟通与事实陈述</div>
              <div class="day-desc">剥离情绪，只陈述事实、感受和具体需求。这是一种像写代码一样精确、不易产生Bug的高级沟通协议。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('沟通模型',this);">沟通模型</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('沟通',this);">沟通</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-290" onclick="toggleNote(290)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(290)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-290"></div>
                <div class="note-display-wrap " id="note-display-wrap-290">
                  <div class="note-display-header" onclick="toggleNoteDisplay(290)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-290"></div>
                </div>
                <div class="note-editor" id="note-editor-290">
                  <textarea class="note-textarea" id="note-ta-290" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(290)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(290)">删除</button>
                    <span class="note-timestamp" id="note-ts-290"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W49 · 未来视野与技术奇点</span>
            <span class="week-days-count">7 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="291" data-tags="交叉学科,决策,系统,复盘">
            <div class="day-num " id="daynum-291">D291</div>
            <div class="day-content">
              <div class="day-topic"><em>交叉学科</em>周总结：构建个人操作系统</div>
              <div class="day-desc">梳理出一份属于你的「SOP（标准作业程序）」：当你面对一个全新的、复杂的技能挑战时，你第一步做什么，第二步做什么。</div>
              <span class="tag tag-review">月复盘</span><span class="tag tag-cross">交叉学科</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('交叉学科',this);">交叉学科</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('决策',this);">决策</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统',this);">系统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-291" onclick="toggleNote(291)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(291)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-291"></div>
                <div class="note-display-wrap " id="note-display-wrap-291">
                  <div class="note-display-header" onclick="toggleNoteDisplay(291)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-291"></div>
                </div>
                <div class="note-editor" id="note-editor-291">
                  <textarea class="note-textarea" id="note-ta-291" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(291)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(291)">删除</button>
                    <span class="note-timestamp" id="note-ts-291"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="292" data-tags="个体演化,学习,策略">
            <div class="day-num " id="daynum-292">D292</div>
            <div class="day-content">
              <div class="day-topic"><em>个体演化</em>刺猬与狐狸理论</div>
              <div class="day-desc">狐狸知道很多事情（懂很多零碎的工具），而刺猬只知道一件大事（掌握极其深度的底层逻辑）。在不同阶段，如何切换这两种生存策略？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('个体演化',this);">个体演化</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('学习',this);">学习</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('策略',this);">策略</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-292" onclick="toggleNote(292)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(292)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-292"></div>
                <div class="note-display-wrap " id="note-display-wrap-292">
                  <div class="note-display-header" onclick="toggleNoteDisplay(292)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-292"></div>
                </div>
                <div class="note-editor" id="note-editor-292">
                  <textarea class="note-textarea" id="note-ta-292" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(292)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(292)">删除</button>
                    <span class="note-timestamp" id="note-ts-292"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="293" data-tags="风险管理,风险,杠杆,反脆弱">
            <div class="day-num " id="daynum-293">D293</div>
            <div class="day-content">
              <div class="day-topic"><em>风险管理</em>杠铃策略（Barbell Strategy）</div>
              <div class="day-desc">塔勒布的生存哲学：把90%的精力放在极其安全、有保底的领域，把10%的精力投在风险极高但可能带来百倍回报的新鲜事物上。拒绝平庸的中等风险。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('风险管理',this);">风险管理</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('风险',this);">风险</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('杠杆',this);">杠杆</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('反脆弱',this);">反脆弱</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-293" onclick="toggleNote(293)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(293)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-293"></div>
                <div class="note-display-wrap " id="note-display-wrap-293">
                  <div class="note-display-header" onclick="toggleNoteDisplay(293)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-293"></div>
                </div>
                <div class="note-editor" id="note-editor-293">
                  <textarea class="note-textarea" id="note-ta-293" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(293)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(293)">删除</button>
                    <span class="note-timestamp" id="note-ts-293"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="294" data-tags="极简主义,极简,信息">
            <div class="day-num " id="daynum-294">D294</div>
            <div class="day-content">
              <div class="day-topic"><em>极简主义</em>物质与信息的断舍离</div>
              <div class="day-desc">每一件拥有的物品和每一个关注的信息源，都在暗中消耗你的系统内存。切断非必要的物理和数字连接，实现算力最大化。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('极简主义',this);">极简主义</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('极简',this);">极简</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('信息',this);">信息</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-294" onclick="toggleNote(294)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(294)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-294"></div>
                <div class="note-display-wrap " id="note-display-wrap-294">
                  <div class="note-display-header" onclick="toggleNoteDisplay(294)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-294"></div>
                </div>
                <div class="note-editor" id="note-editor-294">
                  <textarea class="note-textarea" id="note-ta-294" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(294)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(294)">删除</button>
                    <span class="note-timestamp" id="note-ts-294"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="295" data-tags="情绪调控,哲学,斯多葛,情绪">
            <div class="day-num " id="daynum-295">D295</div>
            <div class="day-content">
              <div class="day-topic"><em>情绪调控</em>斯多葛学派（Stoicism）的现代应用</div>
              <div class="day-desc">区分「你能控制的」和「你绝对无法控制的」。将所有的算力全部集中在你能控制的代码、设计和健身上，对外部的评价和经济大环境保持冷酷的漠然。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('情绪调控',this);">情绪调控</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('斯多葛',this);">斯多葛</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('情绪',this);">情绪</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-295" onclick="toggleNote(295)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(295)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-295"></div>
                <div class="note-display-wrap " id="note-display-wrap-295">
                  <div class="note-display-header" onclick="toggleNoteDisplay(295)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-295"></div>
                </div>
                <div class="note-editor" id="note-editor-295">
                  <textarea class="note-textarea" id="note-ta-295" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(295)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(295)">删除</button>
                    <span class="note-timestamp" id="note-ts-295"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="296" data-tags="复利思维,技能,复利,跨界">
            <div class="day-num " id="daynum-296">D296</div>
            <div class="day-content">
              <div class="day-topic"><em>复利思维</em>跨界知识的乘法效应</div>
              <div class="day-desc">一个在前25%的HR加上一个前25%的AI工具应用者，其稀缺性远远大于一个前1%的纯HR。理解技能栈的组合杠杆。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('复利思维',this);">复利思维</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('技能',this);">技能</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复利',this);">复利</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('跨界',this);">跨界</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-296" onclick="toggleNote(296)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(296)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-296"></div>
                <div class="note-display-wrap " id="note-display-wrap-296">
                  <div class="note-display-header" onclick="toggleNoteDisplay(296)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-296"></div>
                </div>
                <div class="note-editor" id="note-editor-296">
                  <textarea class="note-textarea" id="note-ta-296" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(296)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(296)">删除</button>
                    <span class="note-timestamp" id="note-ts-296"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="297" data-tags="终极拷问,大一统">
            <div class="day-num " id="daynum-297">D297</div>
            <div class="day-content">
              <div class="day-topic"><em>终极拷问</em>你的核心算法是什么？</div>
              <div class="day-desc">抛开所有的外部标签（专业、学历、所在地），如果用一段代码或一个数学公式来描述你的行事风格，它应该是什么样子？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('终极拷问',this);">终极拷问</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-297" onclick="toggleNote(297)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(297)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-297"></div>
                <div class="note-display-wrap " id="note-display-wrap-297">
                  <div class="note-display-header" onclick="toggleNoteDisplay(297)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-297"></div>
                </div>
                <div class="note-editor" id="note-editor-297">
                  <textarea class="note-textarea" id="note-ta-297" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(297)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(297)">删除</button>
                    <span class="note-timestamp" id="note-ts-297"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div>
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">W50-52 · 大一统闭环与毕业</span>
            <span class="week-days-count">10 days</span>
          </div>
          <div class="days">
          <div class="day" data-day="301" data-tags="前沿计算,AI,奇点,技术奇点,大一统">
            <div class="day-num " id="daynum-301">D301</div>
            <div class="day-content">
              <div class="day-topic"><em>前沿计算</em>通用人工智能（AGI）的临界点</div>
              <div class="day-desc">当机器的智力在每一个单一领域都全面碾压人类时，社会的底层运转逻辑将发生何种根本性断裂？理解「奇点」的物理和哲学意义。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('前沿计算',this);">前沿计算</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('奇点',this);">奇点</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('技术奇点',this);">技术奇点</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-301" onclick="toggleNote(301)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(301)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-301"></div>
                <div class="note-display-wrap " id="note-display-wrap-301">
                  <div class="note-display-header" onclick="toggleNoteDisplay(301)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-301"></div>
                </div>
                <div class="note-editor" id="note-editor-301">
                  <textarea class="note-textarea" id="note-ta-301" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(301)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(301)">删除</button>
                    <span class="note-timestamp" id="note-ts-301"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="305" data-tags="生物科技,基因,生物,AI">
            <div class="day-num " id="daynum-305">D305</div>
            <div class="day-content">
              <div class="day-topic"><em>生物科技</em>合成生物学与CRISPR</div>
              <div class="day-desc">DNA本质上是一套可读写的四进制代码。理解人类如何像敲代码一样剪切基因，将细胞改造成生产新材料、新药物的微观工厂。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('生物科技',this);">生物科技</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('基因',this);">基因</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('生物',this);">生物</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('AI',this);">AI</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-305" onclick="toggleNote(305)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(305)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-305"></div>
                <div class="note-display-wrap " id="note-display-wrap-305">
                  <div class="note-display-header" onclick="toggleNoteDisplay(305)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-305"></div>
                </div>
                <div class="note-editor" id="note-editor-305">
                  <textarea class="note-textarea" id="note-ta-305" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(305)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(305)">删除</button>
                    <span class="note-timestamp" id="note-ts-305"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="317" data-tags="空间哲学,哲学,宇宙,模拟假说">
            <div class="day-num " id="daynum-317">D317</div>
            <div class="day-content">
              <div class="day-topic"><em>空间哲学</em>模拟宇宙假说（Simulation Theory）</div>
              <div class="day-desc">如果我们在电脑里模拟宇宙的技术越来越强，那么概率上讲，我们自己目前处于「最原始基础宇宙」的概率几乎为零。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('空间哲学',this);">空间哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('哲学',this);">哲学</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙',this);">宇宙</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('模拟假说',this);">模拟假说</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-317" onclick="toggleNote(317)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(317)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-317"></div>
                <div class="note-display-wrap " id="note-display-wrap-317">
                  <div class="note-display-header" onclick="toggleNoteDisplay(317)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-317"></div>
                </div>
                <div class="note-editor" id="note-editor-317">
                  <textarea class="note-textarea" id="note-ta-317" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(317)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(317)">删除</button>
                    <span class="note-timestamp" id="note-ts-317"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="322" data-tags="宇宙尺度,宇宙起源,费米悖论">
            <div class="day-num " id="daynum-322">D322</div>
            <div class="day-content">
              <div class="day-topic"><em>宇宙尺度</em>费米悖论（Fermi Paradox）</div>
              <div class="day-desc">宇宙这么老，星星这么多，为什么我们至今没有看到外星人？这背后隐藏着极其令人不安的统计学真相。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙尺度',this);">宇宙尺度</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙起源',this);">宇宙起源</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('费米悖论',this);">费米悖论</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-322" onclick="toggleNote(322)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(322)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-322"></div>
                <div class="note-display-wrap " id="note-display-wrap-322">
                  <div class="note-display-header" onclick="toggleNoteDisplay(322)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-322"></div>
                </div>
                <div class="note-editor" id="note-editor-322">
                  <textarea class="note-textarea" id="note-ta-322" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(322)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(322)">删除</button>
                    <span class="note-timestamp" id="note-ts-322"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="328" data-tags="宇宙宏图,熵,宇宙,大一统">
            <div class="day-num " id="daynum-328">D328</div>
            <div class="day-content">
              <div class="day-topic"><em>宇宙宏图</em>熵寂的终极对抗</div>
              <div class="day-desc">回归Day1。如果宇宙的终局注定是冷寂的虚无，那么生命和文明这些不断制造「低熵结构」的努力，在百亿年的尺度下意义何在？</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙宏图',this);">宇宙宏图</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('宇宙',this);">宇宙</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-328" onclick="toggleNote(328)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(328)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-328"></div>
                <div class="note-display-wrap " id="note-display-wrap-328">
                  <div class="note-display-header" onclick="toggleNoteDisplay(328)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-328"></div>
                </div>
                <div class="note-editor" id="note-editor-328">
                  <textarea class="note-textarea" id="note-ta-328" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(328)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(328)">删除</button>
                    <span class="note-timestamp" id="note-ts-328"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="331" data-tags="大一统,熵,经济周期">
            <div class="day-num " id="daynum-331">D331</div>
            <div class="day-content">
              <div class="day-topic"><em>大一统</em>物理与经济的缝合</div>
              <div class="day-desc">为什么市场会崩溃？用「热力学第二定律（熵增）」重新解释经济学中的周期律。理解每一次经济危机，本质上都是系统在强制排解累积的高熵（泡沫）。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('经济周期',this);">经济周期</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-331" onclick="toggleNote(331)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(331)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-331"></div>
                <div class="note-display-wrap " id="note-display-wrap-331">
                  <div class="note-display-header" onclick="toggleNoteDisplay(331)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-331"></div>
                </div>
                <div class="note-editor" id="note-editor-331">
                  <textarea class="note-textarea" id="note-ta-331" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(331)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(331)">删除</button>
                    <span class="note-timestamp" id="note-ts-331"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="335" data-tags="大一统,熵,管理学">
            <div class="day-num " id="daynum-335">D335</div>
            <div class="day-content">
              <div class="day-topic"><em>大一统</em>热力学与组织管理的终极对齐</div>
              <div class="day-desc">公司的本质就是一台「耗散结构机器」。它必须疯狂从外界吞噬利润（低熵），以对抗内部不可避免的流程腐化与人浮于事（高熵）。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('熵',this);">熵</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('管理学',this);">管理学</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-335" onclick="toggleNote(335)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(335)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-335"></div>
                <div class="note-display-wrap " id="note-display-wrap-335">
                  <div class="note-display-header" onclick="toggleNoteDisplay(335)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-335"></div>
                </div>
                <div class="note-editor" id="note-editor-335">
                  <textarea class="note-textarea" id="note-ta-335" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(335)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(335)">删除</button>
                    <span class="note-timestamp" id="note-ts-335"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="345" data-tags="行动部署,系统论,工作流,大一统">
            <div class="day-num " id="daynum-345">D345</div>
            <div class="day-content">
              <div class="day-topic"><em>行动部署</em>万物皆为工作流（Workflow）</div>
              <div class="day-desc">从细胞内质网的蛋白合成，到你在电脑上跑通第一个API接口。将生活和创作中的一切复杂问题，强制拆解为有输入、有处理、有输出的SOP模块。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('行动部署',this);">行动部署</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('系统论',this);">系统论</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('工作流',this);">工作流</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-345" onclick="toggleNote(345)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(345)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-345"></div>
                <div class="note-display-wrap " id="note-display-wrap-345">
                  <div class="note-display-header" onclick="toggleNoteDisplay(345)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-345"></div>
                </div>
                <div class="note-editor" id="note-editor-345">
                  <textarea class="note-textarea" id="note-ta-345" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(345)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(345)">删除</button>
                    <span class="note-timestamp" id="note-ts-345"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="357" data-tags="终极基建,大一统,学习">
            <div class="day-num " id="daynum-357">D357</div>
            <div class="day-content">
              <div class="day-topic"><em>终极基建</em>构建个人的绝对「护城河」</div>
              <div class="day-desc">你掌握的最核心竞争力，一定不是某个很快会过时的具体工具，而是你这一年练就的、能够瞬间看透任何新事物内部逻辑的「逆向工程能力」。</div>
              
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('终极基建',this);">终极基建</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('学习',this);">学习</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-357" onclick="toggleNote(357)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(357)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-357"></div>
                <div class="note-display-wrap " id="note-display-wrap-357">
                  <div class="note-display-header" onclick="toggleNoteDisplay(357)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-357"></div>
                </div>
                <div class="note-editor" id="note-editor-357">
                  <textarea class="note-textarea" id="note-ta-357" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(357)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(357)">删除</button>
                    <span class="note-timestamp" id="note-ts-357"></span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="day" data-day="365" data-tags="毕业典礼,复盘,大一统">
            <div class="day-num " id="daynum-365">D365</div>
            <div class="day-content">
              <div class="day-topic"><em>毕业典礼</em>毕业典礼：成为「文明架构师」</div>
              <div class="day-desc">一年的时间，每天1小时，365个底层逻辑基站。此时此刻，当你重新睁开眼睛看这个世界，它再也没有秘密。游戏开始。</div>
              <span class="tag tag-review">月复盘</span>
              <div class="day-tags"><span class="tag-chip" onclick="event.stopPropagation();filterTag('毕业典礼',this);">毕业典礼</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('复盘',this);">复盘</span><span class="tag-chip" onclick="event.stopPropagation();filterTag('大一统',this);">大一统</span></div>
              <div class="note-area">
                <button class="note-toggle " id="note-toggle-365" onclick="toggleNote(365)">
                  <span class="nt-icon"></span>
                  <span class="nt-label">记录感悟</span>
                </button>
                <button class="link-btn" onclick="addLink(365)" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-365"></div>
                <div class="note-display-wrap " id="note-display-wrap-365">
                  <div class="note-display-header" onclick="toggleNoteDisplay(365)">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)"></span>
                  </div>
                  <div class="note-display" id="note-display-365"></div>
                </div>
                <div class="note-editor" id="note-editor-365">
                  <textarea class="note-textarea" id="note-ta-365" placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……"></textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(365)">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(365)">删除</button>
                    <span class="note-timestamp" id="note-ts-365"></span>
                  </div>
                </div>
              </div>
            </div>
          </div></div>
        </div></div></div></div>

<div class="timeline">
  <div class="timeline-title">— 全年学习进程 —</div>
  <div class="timeline-track" id="timeline-track"></div>
  <div class="timeline-labels" id="timeline-labels"></div>
</div>

<footer class="footer">
  <div style="display:flex;justify-content:center;gap:40px;flex-wrap:wrap;margin-bottom:24px;padding:0 20px;">
    <div style="text-align:center">
      <div style="font-family:'Cinzel',serif;font-size:22px;color:var(--accent1);line-height:1">365</div>
      <div style="font-size:10px;color:var(--text3);letter-spacing:2px;margin-top:3px">DAYS</div>
    </div>
    <div style="text-align:center">
      <div style="font-family:'Cinzel',serif;font-size:22px;color:var(--accent2);line-height:1">10</div>
      <div style="font-size:10px;color:var(--text3);letter-spacing:2px;margin-top:3px">MODULES</div>
    </div>
    <div style="text-align:center">
      <div style="font-family:'Cinzel',serif;font-size:22px;color:var(--accent3);line-height:1">52</div>
      <div style="font-size:10px;color:var(--text3);letter-spacing:2px;margin-top:3px">WEEKS</div>
    </div>
    <div style="text-align:center">
      <div style="font-family:'Cinzel',serif;font-size:22px;color:var(--accent5);line-height:1">∞</div>
      <div style="font-size:10px;color:var(--text3);letter-spacing:2px;margin-top:3px">CONNECTIONS</div>
    </div>
  </div>
  <div style="font-family:'Cinzel',serif;font-size:9px;letter-spacing:4px;color:var(--text3);margin-bottom:8px;">
    KNOWLEDGE COSMOS · CIVILIZATION ARCHITECT
  </div>
  <span style="color:var(--accent1)">通识知识体系</span> · 十大模块 · 从宇宙硬件到文明架构师 · 游戏开始
</footer>

<script>
const MODULES = [
  {
    id: 1,
    icon: "⚛️",
    color: "#7ac87a",
    days: "Day 1–30",
    range: [1, 30],
    title: "自然科学与演化",
    subtitle: "宇宙的「硬件驱动」",
    desc: "物理·化学·生物·演化论·脑科学·生态学",
    weeks: [
      {
        title: "W1 · 物理学基础",
        days: [
          { n:1, topic:"熵增定律", field:"物理学", desc:"理解为什么有序必然走向无序。无论组织管理还是整理房间，本质上都是在「抗熵」。" },
          { n:2, topic:"牛顿力学与决定论", field:"物理学", desc:"只要知道初始状态，就能预测未来吗？理解宏观世界的「确定性」与系统控制的错觉。" },
          { n:3, topic:"量子力学的概率世界", field:"物理学", desc:"观察者如何改变结果？理解微观层面的「不确定性」和叠加态，打破绝对的客观真实。" },
          { n:4, topic:"相对论：时空的弹性", field:"物理学", desc:"时间和空间不是绝对的容器，而是受质量扭曲的网。" },
          { n:5, topic:"能量守恒与转化", field:"热力学", desc:"能量不会凭空产生，只能转移。识别现实中的「永动机陷阱」和不可避免的系统损耗。" },
          { n:6, topic:"物质的微观结构", field:"物理学", desc:"从原子到夸克，世界如何从几种最简单的基本粒子「堆叠」出无限复杂的可能性。" },
          { n:7, topic:"周总结：物理定律迁移", field:"交叉学科", desc:"用这一周的物理词汇，描述你研究的系统中哪些部分在模拟这些物理法则。", review:true, cross:true },
        ]
      },
      {
        title: "W2 · 宇宙学与化学",
        days: [
          { n:8, topic:"大爆炸与宇宙膨胀", field:"宇宙学", desc:"理解时间与空间的起点，万物皆始于一个极度低熵的奇点。" },
          { n:9, topic:"恒星演化：宇宙的熔炉", field:"宇宙学", desc:"我们都是星尘。理解恒星如何通过核聚变产生构建生命的重元素。" },
          { n:10, topic:"元素周期表：原子的秩序", field:"化学", desc:"看透物质的内在逻辑：原子最外层电子的排布如何决定物质的「性格」。" },
          { n:11, topic:"化学键：结合的底层动力", field:"化学", desc:"物质为什么会结合？寻找更低、更稳定的能量状态是万物连接的终极驱动力。" },
          { n:12, topic:"碳基密码：生命的乐高", field:"化学", desc:"为什么生命选择了碳？理解碳原子的四价键结构是构建复杂系统的「数学最优解」。" },
          { n:13, topic:"DNA：生命的代码本", field:"生物学", desc:"破译四进制的基因编码系统。生命的本质是一套极度精密的信息存储与复制程序。" },
          { n:14, topic:"周总结：从星尘到代码", field:"交叉学科", desc:"回顾物质如何从无机的元素，一步步跨越到具有自我复制能力的「有机程序」。", review:true, cross:true },
        ]
      },
      {
        title: "W3 · 生物学与演化论",
        days: [
          { n:15, topic:"细胞：精密的微观工厂", field:"细胞学", desc:"将细胞视作高度分工的组织，理解内部SOP是如何高效运转的。" },
          { n:16, topic:"ATP：生命的通用货币", field:"生物学", desc:"理解所有生命体内的「能量结算」系统。" },
          { n:17, topic:"物竞天择：无目的的演化", field:"演化论", desc:"打破「进化是为了变得更完美」的迷思。环境是唯一的考官，适者生存非强者生存。" },
          { n:18, topic:"基因突变：创新的Bug", field:"演化论", desc:"复制过程中的错误，是系统产生多样性的唯一来源。「不完美」才是系统不被淘汰的关键。" },
          { n:19, topic:"自私的基因", field:"演化论", desc:"个体只是基因生存和传递的「运载机器」，生物的所有利他与博弈皆受此底层逻辑驱动。" },
          { n:20, topic:"免疫系统：边界的防御", field:"生理学", desc:"系统如何精确区分「自我」与「非我」，并在遭受外部攻击时启动记忆与反击机制。" },
          { n:21, topic:"周总结：演化算法的应用", field:"交叉学科", desc:"将「基因、突变、选择」的演化思维套用在AI工具的迭代与淘汰竞争中。", review:true, cross:true },
        ]
      },
      {
        title: "W4 · 脑科学与生态学",
        days: [
          { n:22, topic:"神经元：意识的物理学", field:"脑科学", desc:"所有的思想、意志和情感，本质上都只是神经突触间微弱的物理电信号放电。" },
          { n:23, topic:"视觉重构：大脑的渲染", field:"脑科学", desc:"大脑不是照相机，而是「渲染引擎」。你看到的世界是大脑在暗箱中推测出来的。" },
          { n:24, topic:"多巴胺回路：动机代码", field:"心理学", desc:"揭开行为的底层驱动力：大脑在预测奖赏时分泌的化学物质如何控制我们的习惯。" },
          { n:25, topic:"情绪的价值：避险算法", field:"心理学", desc:"负面情绪不是缺陷，而是漫长演化写进基因里的高效避险快捷键。" },
          { n:26, topic:"生态位与资源网络", field:"生态学", desc:"任何系统都是复杂的资源分配网络，「不要在同一个生态位上死磕」的生存智慧。" },
          { n:27, topic:"能量递减定律", field:"生态学", desc:"能量每向上级传递就损耗极大，解释了为什么顶级掠食者注定稀少，层级过多的组织为何低效。" },
          { n:28, topic:"周总结：感知与复杂网络", field:"交叉学科", desc:"总结人类如何通过极其有限的感官，在复杂的能量网络中寻找生存策略。", review:true, cross:true },
        ]
      },
      {
        title: "W5 · 涌现与大复盘",
        days: [
          { n:29, topic:"涌现：量变到质变的魔法", field:"系统论", desc:"当大量简单的个体遵循简单规则互动时，如何自发产生出单个个体完全不具备的复杂高级特征。" },
          { n:30, topic:"第一月复盘：搭建自然科学底座", field:"大复盘", desc:"串联前29天的逻辑卡片：如果宇宙是一台机器，生命是如何在这台机器里钻漏洞生存的？", review:true },
        ]
      },
    ]
  },
  {
    id: 2,
    icon: "🧠",
    color: "#5a8fc8",
    days: "Day 31–60",
    range: [31, 60],
    title: "认知与人文精神",
    subtitle: "系统的「操作系统」",
    desc: "逻辑学·哲学·东方哲学·心理学·宏观历史",
    weeks: [
      {
        title: "W6 · 逻辑学与认知科学",
        days: [
          { n:31, topic:"概念与定义界定", field:"逻辑学", desc:"清晰的边界是思考的前提。大多数争论并非观点不合，而是对同一个词的定义不同。" },
          { n:32, topic:"演绎推理与三段论", field:"逻辑学", desc:"从普遍规律推导具体结论的必然性。建立不可被驳倒的硬逻辑。" },
          { n:33, topic:"归纳推理与黑天鹅", field:"逻辑学", desc:"从经验中总结规律的危险性。「过去一直这样」无法推导出「未来一定这样」。" },
          { n:34, topic:"常见逻辑谬误", field:"逻辑学", desc:"识别滑坡谬误、稻草人谬误、诉诸人身等逻辑漏洞。给大脑「杀毒」。" },
          { n:35, topic:"第一性原理思维", field:"认知科学", desc:"将事物拆解到最基础、不可证伪的物理或数学要素，然后从头重构。" },
          { n:36, topic:"奥卡姆剃刀原则", field:"认知科学", desc:"「如无必要，勿增实体。」在解释复杂现象时，最简单的那个往往最接近正确。" },
          { n:37, topic:"周总结：思维的除草", field:"交叉学科", desc:"审视过去的直觉判断，用第一性原理将其完全拆解并重组一次。", review:true, cross:true },
        ]
      },
      {
        title: "W7 · 西方哲学",
        days: [
          { n:38, topic:"苏格拉底的牛虻精神", field:"哲学", desc:"哲学的起点是「承认无知」。提问比给答案更重要，通过不断追问打破理所当然的日常幻觉。" },
          { n:39, topic:"柏拉图的洞穴之喻", field:"哲学", desc:"现实可能只是更高维「理念世界」的投影。重新思考眼前看到的「真实」到底有几分可信。" },
          { n:40, topic:"笛卡尔：我思故我在", field:"哲学", desc:"当你把世界上一切东西都怀疑掉之后，唯一不能怀疑的，就是「你正在怀疑」这个意识本身。" },
          { n:41, topic:"康德与「物自体」", field:"哲学", desc:"人类永远戴着「时空和因果律」的有色眼镜看世界，永远无法触及事物本身的绝对面貌。" },
          { n:42, topic:"尼采与「超人」哲学", field:"哲学", desc:"在没有绝对价值锚点的虚无世界里，人必须拥有强大的生命意志，为自己创造全新的法则。" },
          { n:43, topic:"萨特与存在主义", field:"哲学", desc:"「存在先于本质」。人没有被预先设定好的出厂目的，面对不确定性，自由是一种沉重的责任。" },
          { n:44, topic:"周总结：自我意义的赋予", field:"交叉学科", desc:"结合存在主义，不去寻找「标准人生路径」，纯粹依靠当下的行动去定义自身价值。", review:true, cross:true },
        ]
      },
      {
        title: "W8 · 东方哲学",
        days: [
          { n:45, topic:"孔子的世俗秩序系统", field:"东方哲学", desc:"「克己复礼」的本质：通过建立明确的伦理名分和仪式，极大降低人与人之间的协作与沟通成本。" },
          { n:46, topic:"老子的系统反向控制", field:"东方哲学", desc:"「无为而无不为」。承认系统的混沌性，不强行干预，顺应自然规律反而能达到最优的控制效果。" },
          { n:47, topic:"庄子的相对主义自由", field:"东方哲学", desc:"「齐物论」：打破功利、大小、对错的二元对立视角，跳出世俗评价体系，获得高维度的心理自由。" },
          { n:48, topic:"释迦牟尼的苦集灭道", field:"东方哲学", desc:"揭示多巴胺的骗局：人类的痛苦源于对无常事物的执着。切断贪欲的算法，是内心平静的终极路径。" },
          { n:49, topic:"法家的管理控制论", field:"东方哲学", desc:"纯粹基于人性趋利避害的特点，通过冷酷的「赏罚分明」来驱动庞大组织的运转。" },
          { n:50, topic:"禅宗的「指月之指」", field:"东方哲学", desc:"语言、概念和工具都只是指向月亮的那根「手指」。警惕沉迷于工具本身，而忘记了真正要达成的目的。" },
          { n:51, topic:"周总结：组织架构的文化张力", field:"交叉学科", desc:"对比东西方：个人意志与集体和谐的碰撞，透视现代企业规章制度与文化建设底层的矛盾与融合。", review:true, cross:true },
        ]
      },
      {
        title: "W9 · 心理学与宏观历史",
        days: [
          { n:52, topic:"丹尼尔·卡尼曼的双系统", field:"心理学", desc:"思考的快与慢。大脑为了节能，95%的时间在使用直觉（系统1），这种偷懒导致大量偏见和失误。" },
          { n:53, topic:"认知失调的自欺机制", field:"心理学", desc:"当现实行为与内在信念发生冲突时，人类最擅长的不是改变行为，而是扭曲事实让内心重新感到自洽。" },
          { n:54, topic:"认知革命与虚构故事", field:"宏观历史", desc:"智人之所以能统治地球，是因为拥有谈论「不存在之物」并因此达成大规模协作的能力。" },
          { n:55, topic:"农业革命的内卷陷阱", field:"宏观历史", desc:"技术的反噬：小麦驯化了人类，将人锁死在土地上。效率工具的引入未必带来轻松，反而可能拉高生存门槛。" },
          { n:56, topic:"想象的共同体与货币", field:"宏观历史", desc:"钞票本身没有价值，它是一套基于集体信任的协议。一切社会秩序底层都建立在「相信同一个故事」上。" },
          { n:57, topic:"科学革命的范式转移", field:"科技史", desc:"从「古人已经知道一切」转变为「承认我们的无知」。观察、实验和数学工具打破了教条主义的封印。" },
          { n:58, topic:"工业革命与能源解放", field:"科技史", desc:"化石燃料的引入不仅改变了生产力，更从根本上重塑了全球的阶级与权力结构。" },
        ]
      },
      {
        title: "W10 · 历史演化与第二月复盘",
        days: [
          { n:59, topic:"历史演化的必然与偶然", field:"宏观历史", desc:"如果没有爱迪生，灯泡依然会被发明。技术演化有其客观的涌现规律，但关键时刻的走向由偶然性决定。" },
          { n:60, topic:"第二月复盘：拆解人类的「源代码」", field:"大复盘", desc:"从逻辑、哲学到宏观历史，总结人类是如何用脆弱的肉身，通过一套虚构的「协议」建立庞大文明机器的。", review:true },
        ]
      },
    ]
  },
  {
    id: 3,
    icon: "⚖️",
    color: "#c85a7a",
    days: "Day 61–90",
    range: [61, 90],
    title: "社会秩序与博弈",
    subtitle: "系统的「网络协议」",
    desc: "经济学·博弈论·金融学·政治学·社会学·管理学",
    weeks: [
      {
        title: "W11 · 经济学与博弈论",
        days: [
          { n:61, topic:"稀缺性与机会成本", field:"经济学", desc:"世界上没有免费的午餐。你做出任何选择，真正的代价是你为了它而放弃的最高价值的选项。" },
          { n:62, topic:"边际效用递减", field:"经济学", desc:"为什么拥有越多，快乐越少？理解「新增的一单位」带来的价值是如何随着总量增加而暴跌的。" },
          { n:63, topic:"价格机制的本质", field:"经济学", desc:"价格不是由成本决定的，而是由供需决定的。价格本质上是整个社会网络在传递「资源往哪走」的信息。" },
          { n:64, topic:"囚徒困境与零和博弈", field:"博弈论", desc:"为什么极其聪明的个人，在特定规则下会做出对集体极其愚蠢的决定？（透视职场内卷的底层机制）" },
          { n:65, topic:"纳什均衡", field:"博弈论", desc:"系统中的一种「稳定状态」。一旦达到这个状态，没有任何人有动力单方面改变自己的策略。" },
          { n:66, topic:"重复博弈与合作演化", field:"博弈论", desc:"「以牙还牙（Tit for Tat）」是陌生人社会中建立合作的最优数学解。" },
          { n:67, topic:"周总结：理性的算计", field:"交叉学科", desc:"思考题：HR在设计绩效考核时，是在引导员工走向「囚徒困境」（互踩），还是「重复博弈」（协作）？", review:true, cross:true },
        ]
      },
      {
        title: "W12 · 金融学与政治学",
        days: [
          { n:68, topic:"货币：信用的具象化", field:"金融学", desc:"现代货币早已脱离金本位。钱不是财富，钱是对社会资源的一种「索取权」和债务凭证。" },
          { n:69, topic:"杠杆与复利", field:"金融学", desc:"复利是时间维度的非线性增长；杠杆是空间维度的力量放大器。两者结合能创造奇迹，也能导致毁灭。" },
          { n:70, topic:"债务周期模型", field:"金融学", desc:"达利欧模型：经济的繁荣与衰退不是随机的，而是信贷扩张与收缩的必然周期节律。" },
          { n:71, topic:"社会契约论", field:"政治学", desc:"国家是如何诞生的？人类出让一部分绝对自由给「利维坦」（政府），换取生命与财产的安全。" },
          { n:72, topic:"暴力的合法垄断", field:"政治学", desc:"马克斯·韦伯的洞见：一个政权之所以能制定规则，底层逻辑在于它垄断了合法使用暴力的权力。" },
          { n:73, topic:"权力制衡与防错设计", field:"政治学", desc:"为什么三权分立效率很低，但却被认为是好制度？因为政治设计的核心不是追求效率，而是防止单点故障。" },
          { n:74, topic:"周总结：权力与财富的绑定", field:"交叉学科", desc:"将「资本（经济）」与「强制力（政治）」结合来看，理解为什么所有的商业巨头最终都会触碰规则边界。", review:true, cross:true },
        ]
      },
      {
        title: "W13 · 社会学与法学",
        days: [
          { n:75, topic:"阶级固化与马太效应", field:"社会学", desc:"「凡有的，还要加给他。」理解社会财富和资源为何会自然而然地向头部网络节点集中。" },
          { n:76, topic:"弱联系的力量", field:"社会学", desc:"为什么找工作往往靠不太熟的人？信息破圈的底层网络逻辑。" },
          { n:77, topic:"乌合之众与群体降智", field:"社会学", desc:"为什么个体是理性的，但汇聚成群体后就会变得盲目、情绪化且极具破坏力？（去个性化机制）" },
          { n:78, topic:"消费主义与符号互动", field:"社会学", desc:"你买的不是商品，而是「身份标签」。理解商业社会是如何通过制造焦虑来逼迫你进行符号消费的。" },
          { n:79, topic:"程序正义 vs 实体正义", field:"法学", desc:"为什么宁可放走坏人，也不能违规取证？理解为了维护整个系统规则的绝对信用，必须容忍局部的错误。" },
          { n:80, topic:"财产权的底层逻辑", field:"法学", desc:"如果你的东西不属于你，你就不会去创造。明确的产权界定，是所有复杂商业社会运作的第一块基石。" },
          { n:81, topic:"周总结：群体的无意识网络", field:"交叉学科", desc:"结合心理学与社会学，剖析「为什么我们总是身不由己地被卷入某种社会洪流」。", review:true, cross:true },
        ]
      },
      {
        title: "W14 · 管理学与复杂网络",
        days: [
          { n:82, topic:"科层制的利与弊", field:"管理学", desc:"剖析你最讨厌的「形式主义」：为什么庞大的组织必须依赖死板的流程和无聊的表格，即便它抹杀了人性？" },
          { n:83, topic:"委托-代理问题", field:"管理学", desc:"老板（委托人）想压榨，员工（代理人）想摸鱼。两者利益根本不一致时，如何通过制度绑定？" },
          { n:84, topic:"古德哈特定律", field:"管理学", desc:"「当一个指标变成目标时，它就不再是一个好指标。」KPI为什么往往导致数据造假和动作变形。" },
          { n:85, topic:"帕金森定律与彼得原理", field:"管理学", desc:"为什么公司部门只会越来越臃肿？为什么平庸的员工总会被晋升到他无法胜任的岗位上？" },
          { n:86, topic:"节点、枢纽与幂律分布", field:"复杂网络", desc:"世界上绝大多数事物不符合「正态分布（钟形曲线）」，而是符合极其不平等的「80/20法则」。" },
          { n:87, topic:"反脆弱性", field:"复杂网络", desc:"脆弱的系统怕风，而火苗却借风势越烧越旺。如何在充满混乱和不确定性的时代构建自己的反脆弱系统？" },
          { n:88, topic:"黑天鹅事件", field:"复杂网络", desc:"未知中的未知。为什么基于过往数据的预测模型，在极端罕见事件面前不堪一击？" },
        ]
      },
      {
        title: "W15 · 第三月复盘",
        days: [
          { n:89, topic:"周总结：直面系统的漏洞", field:"交叉学科", desc:"用这周学到的网络法则，重新审视HR专业背景，写下3条对公司管理制度的致命吐槽。", review:true, cross:true },
          { n:90, topic:"第三月复盘：规则与反叛", field:"大复盘", desc:"我们学会了世界的规则，是为了在其中游刃有余，更是为了在必要时精准地打破它。", review:true },
        ]
      },
    ]
  },
  {
    id: 4,
    icon: "⚙️",
    color: "#c8975a",
    days: "Day 91–120",
    range: [91, 120],
    title: "技术与文明重启",
    subtitle: "系统的「用户界面」",
    desc: "工程学·信息论·计算机·AI·美学·3D打印·文明重建",
    weeks: [
      {
        title: "W16 · 工程学与信息论",
        days: [
          { n:91, topic:"模块化思维与解耦", field:"工程学", desc:"复杂系统如何运转？将其拆分为互不干扰的黑盒模块。和写代码时封装函数是同一套逻辑。" },
          { n:92, topic:"冗余设计与容错率", field:"工程学", desc:"为什么飞机有两套引擎？在关键节点故意制造「浪费」（冗余），是系统对抗突发性崩溃的唯一工程学手段。" },
          { n:93, topic:"负反馈控制系统", field:"工程学", desc:"恒温器原理。系统如何通过检测「输出结果」并反向抑制「输入」，来维持自身的动态平衡。" },
          { n:94, topic:"香农熵与比特", field:"信息论", desc:"与Day1的热力学熵呼应。信息是可以被精确量化的，消除不确定性所需要的代价，就是信息的本质。" },
          { n:95, topic:"图灵机与计算的极限", field:"计算机", desc:"一条无限长的纸带和几个简单规则，就能模拟宇宙中一切可计算的过程。数字世界的「第一性原理」。" },
          { n:96, topic:"算法与时间复杂度", field:"计算机", desc:"为什么有的程序秒出，有的要跑一年？理解Big O表示法，看透效率背后的数学天花板。" },
          { n:97, topic:"周总结：虚拟世界的架构", field:"交叉学科", desc:"尝试用「模块化」和「负反馈」的逻辑，去分析你正在使用的某个AI自动化工作流。", review:true, cross:true },
        ]
      },
      {
        title: "W17 · AI与美学原理",
        days: [
          { n:98, topic:"去中心化与TCP/IP", field:"互联网", desc:"为什么核打击摧毁不了互联网？理解分布式网络如何通过「协议」而非「中央集权」来实现无损信息传输。" },
          { n:99, topic:"神经网络的底层仿生", field:"人工智能", desc:"让机器像婴儿一样，通过海量数据去「调整权重」，模拟人脑的突触连接。" },
          { n:100, topic:"扩散模型（Diffusion）", field:"人工智能", desc:"通过在一张纯噪声图里不断「降噪（减熵）」，强行挤压出极其有序的精美图像。" },
          { n:101, topic:"大语言模型与涌现能力", field:"人工智能", desc:"仅仅是做「文字接龙」，当参数量大到一定程度时，为何会自动涌现出惊人的逻辑推理能力？" },
          { n:102, topic:"智能体（Agent）系统", field:"人工智能", desc:"AI是如何从「只会陪聊」进化为能够自己调用浏览器、操作软件、执行复杂工作流的。" },
          { n:103, topic:"透视法与空间几何", field:"美学原理", desc:"文艺复兴的降维打击。如何在二维平面上用极其严格的数学规则，欺骗人类大脑产生三维空间的深度错觉。" },
          { n:104, topic:"周总结：机器视角与人类审美", field:"交叉学科", desc:"当AI生成图片和3D模型时，它「理解」美吗？还是它只是拟合了人类历史上所有美的数学分布？", review:true, cross:true },
        ]
      },
      {
        title: "W18 · 设计·制造·文明底层",
        days: [
          { n:105, topic:"色彩空间（RGB与CMYK）", field:"美学原理", desc:"光的加法与物质的减法。为什么屏幕上的颜色永远无法在纸上完美打印？理解色彩的物理学局限。" },
          { n:106, topic:"形式追随功能（包豪斯）", field:"设计学", desc:"现代设计的绝对铁律。不要无意义的装饰，一件物品的长相，必须由它的用途来决定。" },
          { n:107, topic:"增材制造（3D打印）", field:"制造学", desc:"告别传统的「切削（减材）」。通过逐层堆叠材料、几乎无浪费的新型制造逻辑对供应链的颠覆。" },
          { n:108, topic:"能源阶跃图谱", field:"科技史", desc:"柴草、煤炭、石油、核裂变。人类文明的每一次大升级，本质上都是找到了能量密度更高的「电池」。" },
          { n:109, topic:"农业与卡路里防线", field:"文明重启", desc:"假设明天文明毁灭。如何通过固氮、选种和堆肥，守住人类存活的第一条底线：卡路里输入。" },
          { n:110, topic:"基础化工（三酸两碱）", field:"文明重启", desc:"硫酸、盐酸、硝酸。没有它们，就没有化肥、炸药和塑料。这些工业血液是如何从零提炼出来的。" },
          { n:111, topic:"周总结：从造物到造境", field:"交叉学科", desc:"从屏幕里的3D建模，跨越到了废土世界中如何用泥土和石头重新捏出工业文明。", review:true, cross:true },
        ]
      },
      {
        title: "W19-20 · 文明重启与第四月复盘",
        days: [
          { n:112, topic:"玻璃：文明的放大镜", field:"文明重启", desc:"烧制沙子。为什么玻璃是科学诞生的前置条件？（显微镜看细菌，望远镜看宇宙，光纤传输数据）" },
          { n:113, topic:"发电机与电力网络", field:"文明重启", desc:"法拉第的奇迹：如何用磁铁和铜线圈的相对运动，凭空创造出驱动现代世界的幽灵——电。" },
          { n:114, topic:"细菌学说与抗生素", field:"文明重启", desc:"青霉素的发现是如何将人类平均寿命从40岁强行拉升到80岁的？" },
          { n:115, topic:"机械传动与内燃机", field:"文明重启", desc:"如何将热量（无序的膨胀）转化为稳定的、定向的物理旋转（有序的机械功）？" },
          { n:116, topic:"无线电与远距离通信", field:"文明重启", desc:"如何将人的声音编码到看不见的电磁波上，跨越重洋重建人类网络？" },
          { n:117, topic:"卡尔达肖夫指数", field:"前沿科技", desc:"评估文明等级的终极标尺：掌控行星级能源（I型）、恒星级能源（II型）与星系级能源（III型）。" },
          { n:118, topic:"戴森球与终极能源", field:"前沿科技", desc:"一个极其宏大的工程构想：用太阳能板把整个恒星包裹起来，彻底榨干它的全部能量。" },
          { n:119, topic:"技术奇点与人类终局", field:"哲学回归", desc:"当机器的智力超越人类，进化的主导权将首次从碳基生命转移到硅基生命手中。" },
          { n:120, topic:"第四月复盘：赛博时代的文明备忘录", field:"大复盘", desc:"总结技术演化史。如果你要把人类文明的最高智慧刻在一个硬盘上留给后代，你会写下哪10个方程？", review:true },
        ]
      },
    ]
  },
  {
    id: 5,
    icon: "🎨",
    color: "#a05ac8",
    days: "Day 121–150",
    range: [121, 150],
    title: "艺术、媒介与视觉美学",
    subtitle: "渲染世界的参数",
    desc: "艺术史·建筑美学·设计学·媒介理论·符号学·AI美学",
    weeks: [
      {
        title: "W21 · 西方绘画史",
        days: [
          { n:121, topic:"洞穴壁画与原始符号", field:"艺术起源", desc:"艺术不是吃饱了撑的。早期的壁画本质上是远古智人为了生存（打猎）而进行的「虚拟现实（VR）演练」。" },
          { n:122, topic:"古希腊：黄金分割与比例", field:"古典美学", desc:"毕达哥拉斯学派的执念：美是可以被精确计算的数学公式。比例与对称如何在视觉上唤起人类底层的安全感。" },
          { n:123, topic:"文艺复兴：透视法的降维打击", field:"古典美学", desc:"人类是如何在二维画布上，通过「消失点」建立一套绝对理性的3D空间坐标系的？" },
          { n:124, topic:"光影大师（卡拉瓦乔/伦勃朗）", field:"古典美学", desc:"绘画界最早的「全局光照（GI）」与「光线追踪」。通过极端的明暗对比来引导观众视觉焦点的控制术。" },
          { n:125, topic:"印象派：捕捉瞬时光照", field:"现代美学", desc:"对古典主义的背叛。不再追求物体的「固有色」，只记录特定时间点光子打在视网膜上的瞬间状态。" },
          { n:126, topic:"立体主义（毕加索）", field:"现代美学", desc:"打破单机位限制。尝试在同一张2D平面上，同时渲染一个物体的正面、侧面和顶面——本质上是对四维空间的视觉折叠。" },
          { n:127, topic:"周总结：绘画史的「算法迭代」", field:"交叉学科", desc:"人类绘画史从追求「像（高保真渲染）」到「不像（抽象提取）」，这与AI生成图像的逻辑有何异同？", review:true, cross:true },
        ]
      },
      {
        title: "W22 · 建筑美学",
        days: [
          { n:128, topic:"古典柱式与承重逻辑", field:"建筑美学", desc:"为什么古希腊神庙长那样？建筑最初的美感完全来源于对重力（物理学）的对抗。形式是被材料强度逼出来的。" },
          { n:129, topic:"哥特式建筑的工程奇迹", field:"建筑美学", desc:"飞扶壁、尖肋骨架。这是中世纪最顶尖的「骨骼拓扑结构」优化，为了让墙壁消失、让光线（神性）透进来。" },
          { n:130, topic:"现代主义：形式追随功能", field:"建筑美学", desc:"剥离一切无意义的雕花装饰，只保留最核心的几何体。这不仅是设计法则，更是最高效的组织架构设计原则。" },
          { n:131, topic:"苏维埃巨型建筑", field:"建筑美学", desc:"权力、乌托邦与绝对几何。理解那种粗野主义（Brutalism）和巨大体量带来的压迫感，是如何传达政治意志的。" },
          { n:132, topic:"赛博朋克与失控的都市", field:"建筑美学", desc:"High Tech, Low Life。霓虹灯、错乱的管线、密集的贫民窟，如何在3D场景中构建这种极致的废土冲突美感。" },
          { n:133, topic:"极简主义与信息降噪", field:"设计美学", desc:"减少多边形（Low Poly）的哲学。在信息过载的时代，极致的留白和简化的线条，是抢占用户注意力的最高级策略。" },
          { n:134, topic:"周总结：空间的权力与压迫", field:"交叉学科", desc:"从神庙到巨型重工业建筑，总结空间尺度和材质是如何在潜意识里操纵人类情绪的。", review:true, cross:true },
        ]
      },
      {
        title: "W23 · 媒介理论与当代艺术",
        days: [
          { n:135, topic:"麦克卢汉：媒介即讯息", field:"媒介理论", desc:"真正改变社会的不是电视里播了什么，而是「电视」这个工具本身。媒介重塑了你的思考链路。" },
          { n:136, topic:"能指与所指的剥离", field:"符号学", desc:"一张玫瑰的图片（能指）如何与浪漫（所指）绑定？理解视觉符号是如何被社会文化强行编码和解读的。" },
          { n:137, topic:"蒙太奇：时间的剪辑术", field:"摄影与电影", desc:"将两段毫不相干的视频拼接在一起，大脑会自动脑补出因果逻辑（库里肖夫效应）。人类大脑「强行建立联系」的漏洞。" },
          { n:138, topic:"杜尚的泉与概念艺术", field:"当代艺术", desc:"把小便池放进美术馆。艺术的定义权从「手工技术」彻底变成了「定义语境」。想法和Prompt成了最重要的资产。" },
          { n:139, topic:"复制、拼贴与模因（Meme）", field:"波普艺术", desc:"当安迪·沃霍尔开始批量丝网印刷玛丽莲·梦露，艺术失去了光晕，变成了可以被病毒式传播的视觉快消品。" },
          { n:140, topic:"潜空间（Latent Space）游历", field:"前沿美学", desc:"AI眼中的世界。理解生成式模型是如何将整个人类视觉历史压缩到一个高维数学空间，并在其中进行「概率漫游」的。" },
          { n:141, topic:"周总结：媒介的进化", field:"交叉学科", desc:"回顾从岩壁雕刻到大模型潜在空间的媒介跳跃。记录你在使用AI出图时，是如何通过调整Seed值在这片空间里「寻宝」的。", review:true, cross:true },
        ]
      },
      {
        title: "W24-25 · 艺术终局与第五月复盘",
        days: [
          { n:142, topic:"消费主义下的包装美学", field:"跨界博弈", desc:"商品为何要过度包装？理解视觉设计是如何成为一种「心理锚定」工具，强行提升商品在消费者心中的心理溢价的。" },
          { n:143, topic:"丑学（Ugly Aesthetics）", field:"跨界博弈", desc:"为什么有时候「审丑」反而能获得巨大流量？理解打破常规美学秩序所带来的瞬间神经刺激与网络传播效应。" },
          { n:144, topic:"3D软件的底层逻辑", field:"工具演化", desc:"从网格（Mesh）、材质节点（Material Node）到物理渲染（PBR）。计算机是如何用数学公式极其逼真地欺骗人类眼睛的。" },
          { n:145, topic:"游戏引擎的即时反馈", field:"交互美学", desc:"为什么游戏让人上瘾？它提供了一套极其完美的、基于物理法则和数值体系的「即时行动-反馈」闭环。" },
          { n:146, topic:"完美制度的反思", field:"组织美学", desc:"将美学视角带入对HR的认知中：一个过度完美、没有旷野和冗余的职业轨迹或组织结构，是不是反而非常脆弱且无趣？" },
          { n:147, topic:"深度伪造与真实性的消亡", field:"技术伦理", desc:"当「眼见为实」这一人类文明最后的底线被AI击穿，社会将如何重建信用体系？" },
          { n:148, topic:"碳基与硅基的联合创作", field:"艺术终局", desc:"未来的创作者不再是画匠，而是「文明牧羊人」。我们提出方向、制定审美边界，由机器去填充无穷无尽的细节。" },
          { n:149, topic:"发现所有事物内部的运行逻辑", field:"大一统", desc:"哲学、物理学、社会学和美学，在最高层面上是相通的。真正的快乐，正是来源于这种内部运作逻辑的发现与迁移。" },
          { n:150, topic:"第五月复盘：成为文明的「逆向工程」师", field:"大复盘", desc:"这30天，我们拆解了人类视觉的源代码。至此，你对任何一张图、一座建筑、一个网页的观察，都将深入到其底层的参数逻辑。", review:true },
        ]
      },
    ]
  },
  {
    id: 6,
    icon: "∞",
    color: "#5ac8b4",
    days: "Day 151–180",
    range: [151, 180],
    title: "数学、密码学与复杂系统",
    subtitle: "万物的底层代码",
    desc: "数学·逻辑学·统计学·密码学·区块链·网络科学·系统论",
    weeks: [
      {
        title: "W26 · 数学基础",
        days: [
          { n:151, topic:"零与无穷大", field:"数学", desc:"打破日常认知的极限。理解「无」与「无限」这两个极其反直觉的数学概念，是如何推翻人类常识的。" },
          { n:152, topic:"素数：数字的原子", field:"数学", desc:"万物皆数，而素数是构成所有数字的积木。这看似纯粹的数论游戏，却是现代互联网加密通讯的绝对基石。" },
          { n:153, topic:"线性代数与高维矩阵", field:"数学", desc:"成千上万个数据同时运算。这是彻底弄懂AI（大语言模型、扩散模型）如何处理庞大信息的底层说明书。" },
          { n:154, topic:"微积分：捕捉变化的终极武器", field:"数学", desc:"静态的数学无法描述动态的世界。理解导数与极限，你就理解了AI训练时至关重要的「梯度下降」是在干什么。" },
          { n:155, topic:"拓扑学：咖啡杯与甜甜圈", field:"数学", desc:"抛开距离和角度，只关注空间的「连续变形」。这会彻底重塑你对3D网格布线和几何建模的认知。" },
          { n:156, topic:"分形几何与混沌的秩序", field:"数学", desc:"大自然不按直线和圆生长。一棵树、一片雪花，其实都是一段极简数学公式在不断「自我递归」和循环。" },
          { n:157, topic:"哥德尔不完备定理", field:"逻辑学", desc:"理性的终极叹息。任何足够复杂的逻辑系统，都必然存在「既不能被证明，也不能被证伪」的真理。" },
        ]
      },
      {
        title: "W27 · 统计学与密码学",
        days: [
          { n:158, topic:"贝叶斯定理：动态更新的智慧", field:"统计学", desc:"先给出一个「先验概率」，然后根据不断出现的新证据，动态调整自己的认知。极具实用价值的决策模型。" },
          { n:159, topic:"大数定律与均值回归", field:"统计学", desc:"为什么运气总会用光？为什么极致的高绩效员工极容易在第二年表现平庸？认清数据的引力。" },
          { n:160, topic:"辛普森悖论与数据谎言", field:"统计学", desc:"局部数据看起来在增长，汇总到全局却在下跌。警惕那些看似完美、却隐瞒了关键变量的「业务增长报表」。" },
          { n:161, topic:"恩尼格玛机与信息战", field:"密码学", desc:"战争的胜负不再取决于前线，而取决于后方破译密码的速度。理解信息的加密与解密是如何改变历史走向的。" },
          { n:162, topic:"非对称加密：互联网信任基石", field:"密码学", desc:"公开一把锁（公钥）让所有人都能锁上信息，但只有你手里的钥匙（私钥）能打开。陌生人社会的终极信任解法。" },
          { n:163, topic:"哈希函数：数字的唯一指纹", field:"密码学", desc:"无论是一句话还是一部100G的电影，经过算法都能变成一段定长的乱码。只要改动一个像素，指纹就会天翻地覆。" },
          { n:164, topic:"智能合约的无情执行", field:"区块链", desc:"将业务流程和契约写进代码。一旦条件触发，程序自动执行，无需任何人际沟通和审批。" },
        ]
      },
      {
        title: "W28 · 网络科学与系统论",
        days: [
          { n:165, topic:"周总结：代码即法律", field:"交叉学科", desc:"构思一个完全由算法、哈希值和智能合约驱动的全自动人事或内容分发系统，它将如何屠宰现有的枯燥流程？", review:true, cross:true },
          { n:166, topic:"柯尼斯堡七桥问题", field:"网络科学", desc:"图论的起源。抛弃地理位置，只看「节点」和「边」。理解现实世界中的交通、人际网络如何被抽象成数学图表。" },
          { n:167, topic:"小世界网络与六度分隔", field:"网络科学", desc:"为什么你只需通过几个人就能认识世界上的任何人？理解复杂系统中的「捷径」是如何让庞大的网络变得异常紧凑的。" },
          { n:168, topic:"标度自由与富者愈富", field:"网络科学", desc:"网络的发展是不公平的。新节点总是优先连接已经拥有很多连接的「枢纽节点」。破解互联网巨头垄断的底层法则。" },
          { n:169, topic:"动态平衡与负熵流", field:"系统论", desc:"为什么活着的系统需要不断「吃东西」？理解生命和企业如何在持续消耗能量中维持自身的稳定结构。" },
          { n:170, topic:"耗散结构：在边缘寻找生机", field:"系统论", desc:"系统只有在「远离平衡态」且与外界剧烈交换能量时，才能产生新的有序结构。为什么「安逸舒适」的组织往往走向灭亡。" },
          { n:171, topic:"蒙特卡洛模拟", field:"决策学", desc:"算力即暴力。当问题复杂到无法用数学公式解出时，就利用计算机掷千万次骰子，用海量的随机穷举来逼近真相。" },
        ]
      },
      {
        title: "W29-30 · 决策学与第六月复盘",
        days: [
          { n:172, topic:"凯利公式：筹码的数学解", field:"决策学", desc:"在胜率确定的情况下，你应该押注多少资金或精力？理解风险控制与收益最大化之间的数学奇点，拒绝盲目梭哈。" },
          { n:173, topic:"康威生命游戏（元胞自动机）", field:"交叉学科", desc:"只需要三条极其简单的「邻居生存规则」，就能在一个网格世界里演化出无限复杂的、有生命的移动图案。" },
          { n:174, topic:"麦克斯韦妖与信息即能量", field:"信息学", desc:"信息的本质是什么？获取信息，就能让系统从无序变得有序。在这场思想实验里，知识和数据真正等价于物理能量。" },
          { n:175, topic:"确认偏误与算法囚笼", field:"心理反思", desc:"当我们理解了数据的力量，却发现推荐算法正在利用人性的弱点，给我们喂食我们想看的东西。" },
          { n:176, topic:"算法驱动的组织结构", field:"应用迁移", desc:"分析一家完全由数据、API和自动化脚本驱动的现代企业，是如何实现效率极化的。" },
          { n:177, topic:"潜空间（Latent Space）的漫游", field:"前沿视角", desc:"理解我们在生成图像或音乐时，其实是在一个高维的、由数学公式构成的概率海洋中打捞结果。" },
          { n:178, topic:"渲染方程的数学本质", field:"前沿视角", desc:"你在屏幕上看到的每一道逼真的光影，本质上都是计算机在极速解算极其复杂的微积分能量传递方程。" },
          { n:179, topic:"寻找多学科的共通参数", field:"大一统", desc:"将人力资源管理、3D建模软件、自动化内容分发部署放在同一个数学视角下，找出它们底层共享的逻辑链路。" },
          { n:180, topic:"第六月复盘：掌握万物的操作台", field:"大复盘", desc:"180天的旅程过半。世界不再是由表象组成的，在你的眼里，万事万物都已经化为涌动的数据流和严密的算法逻辑。", review:true },
        ]
      },
    ]
  },
  {
    id: 7,
    icon: "🌍",
    color: "#c8c85a",
    days: "Day 181–210",
    range: [181, 210],
    title: "地缘、资源与大国博弈",
    subtitle: "地球的权力沙盘",
    desc: "地缘政治·宏观地理·资源经济·金融霸权·科技地缘·区域分析",
    weeks: [
      {
        title: "W31 · 地缘政治基础",
        days: [
          { n:181, topic:"地理决定论的幽灵", field:"宏观地理", desc:"为什么文明的差异这么大？山脉如何阻断交通导致语言碎裂，平原如何催生中央集权。地形是人类历史最底层的「物理引擎限制」。" },
          { n:182, topic:"麦金德「心脏地带」理论", field:"地缘政治", desc:"「谁控制了东欧，谁就控制了心脏地带；谁控制了世界岛，谁就控制了世界。」理解欧亚大陆这块超级棋盘的核心战略眼。" },
          { n:183, topic:"马汉「海权论」", field:"地缘政治", desc:"为什么近代霸主（英、美）都是海洋国家？理解海洋不是阻隔，而是摩擦力极小的「超级高速公路」。控制咽喉海峡就等于扼住了全球贸易的咽喉。" },
          { n:184, topic:"资源诅咒（Resource Curse）", field:"宏观经济", desc:"为什么家里有矿的国家往往陷入贫困和战乱？理解极度单一的高利润资源是如何摧毁一个国家的工业化动力和人才结构的。" },
          { n:185, topic:"人口结构的倒金字塔", field:"人口学", desc:"老龄化与少子化的不可逆。从HR的视角看宏观：当一个国家的「劳动力供给池」枯竭，它在国际博弈中的底牌如何被彻底抽空。" },
          { n:186, topic:"供应链与海上咽喉", field:"全球化", desc:"马六甲、苏伊士、巴拿马。剖析这几个一旦堵塞就能让全球工厂停工的地理Bug。理解现代商业对「准时制（JIT）」物流的极度依赖与脆弱。" },
          { n:187, topic:"周总结：物理版图的诅咒", field:"交叉学科", desc:"思考题：如果你在一个3D游戏里设计一个必胜的国家，你会如何设置它的山川河流与矿产分布？", review:true, cross:true },
        ]
      },
      {
        title: "W32 · 金融霸权与科技地缘",
        days: [
          { n:188, topic:"气候变迁与帝国周期", field:"生态地缘", desc:"降水线的微小移动，如何导致游牧民族南下入侵农耕文明。地球恒温器的微调，是如何成为历史朝代更迭的终极催化剂的。" },
          { n:189, topic:"石油美元的闭环", field:"金融霸权", desc:"脱离金本位后，美元如何通过绑定全球工业血液（石油）来维持霸权？这是世界上设计得最庞大、最精密的「金融抽水机」系统。" },
          { n:190, topic:"芯片战争与硅幕降临", field:"科技地缘", desc:"算力即权力。AI时代的石油是半导体。理解光刻机和先进制程为何成了现代国家博弈的核武器。" },
          { n:191, topic:"粮食霸权与农业基因", field:"生存底线", desc:"控制了种子，就控制了人类。拆解四大粮商（ABCD）是如何通过转基因专利和化肥供应链，从最底层的卡路里维度控制全球命脉的。" },
          { n:192, topic:"从化石到新能源的洗牌", field:"能源地图", desc:"为什么大家都在疯狂卷电动车和光伏？这不仅是环保问题，更是为了摆脱化石燃料地缘限制，重塑全球能源权力的重新洗牌。" },
          { n:193, topic:"主权国家 vs 跨国寡头", field:"跨国组织", desc:"当一个科技巨头（如苹果、谷歌）的现金流和用户量超过大多数中等国家时，「国家主权」的边界在哪里？" },
          { n:194, topic:"周总结：看不见的战争", field:"交叉学科", desc:"战争早已不在战壕里打响，它发生在代码库、SWIFT结算系统、大豆期货市场和极紫外光刻机的图纸上。", review:true, cross:true },
        ]
      },
      {
        title: "W33-34 · 区域分析",
        days: [
          { n:195, topic:"海底光缆与数据霸权", field:"信息地缘", desc:"你以为互联网在云端？不，全球95%的跨国数据跑在极其脆弱的海底光缆里。谁控制了这些物理线缆的节点，谁就拥有了「天眼」。" },
          { n:196, topic:"近地轨道与星链系统", field:"太空地缘", desc:"轨道坑位是有限的。理解低轨卫星网络如何彻底无视地面的物理国界，建立起一套覆盖全球的、全新的通信和打击协议。" },
          { n:197, topic:"软实力与文化输出", field:"文化博弈", desc:"好莱坞和动漫不是单纯的娱乐。它们是最高级的「思想植入工具」，通过塑造「何为美好生活」的标准，兵不血刃地征服受众的大脑。" },
          { n:198, topic:"联合国与WTO的底层协议", field:"国际秩序", desc:"二战后人类建立的这套「全球操作系统」是如何运行的？以及在逆全球化周期中，这套系统是如何面临崩溃和重构的。" },
          { n:199, topic:"经济制裁的武器化", field:"博弈手段", desc:"不动用一兵一卒，如何让一个现代国家的工业体系瞬间瘫痪？拆解金融断网与技术封锁背后的杀伤力与反噬效应。" },
          { n:200, topic:"边缘地带与代理人战争", field:"地缘政治", desc:"为什么大国从不直接下场互殴？理解「缓冲区」战略，以及小国如何沦为超级大国测试武器和消耗对手的「演兵场」。" },
          { n:201, topic:"周总结：维度的升维打击", field:"交叉学科", desc:"如果你是一个AI公司的CEO，在出海布局时，你要如何应对这些比代码复杂一万倍的地缘政治阻力？", review:true, cross:true },
          { n:202, topic:"欧洲的碎片化与一体化", field:"区域剖析", desc:"为什么欧洲历史就是一部无休止的内战史？理解欧盟试图将几十个主权国家缝合在一起的巨大经济收益与致命的政治阻力。" },
          { n:203, topic:"北美的天选之局", field:"区域剖析", desc:"东西两大洋，南北无强国，内部拥有极其庞大的可航行水系和耕地。从地理参数来看，理解这块大陆自带的「作弊级」防御和发育属性。" },
          { n:204, topic:"亚洲的季风与供应链", field:"区域剖析", desc:"极其密集的人口、极度依赖季风的农业，以及如今全球最庞大的「世界工厂」集群。理解东亚怪兽级别的制造产能是如何诞生的。" },
          { n:205, topic:"中东的战略枢纽诅咒", field:"区域剖析", desc:"连接三大洲的十字路口+地下涌动的石油。极佳的地理位置反而成了它永无宁日的根源，剖析中东地缘的死结。" },
          { n:206, topic:"非洲的觉醒与被剥削", field:"区域剖析", desc:"资源极度丰富，为何却极度贫穷？剖析殖民者用直尺画下的国界线，是如何让这片大陆陷入无休止的部落冲突和资源掠夺的。" },
          { n:207, topic:"拉美的中等收入陷阱", field:"区域剖析", desc:"为什么早早独立、资源丰富的拉美国家，会在达到一定收入水平后集体陷入停滞和混乱？" },
          { n:208, topic:"极地航道与北极博弈", field:"未来地缘", desc:"随着气候变暖，冰川融化。一条能缩短三分之一航程的「北极航线」即将出现，它将如何彻底改写当下的全球海权版图？" },
        ]
      },
      {
        title: "W35 · 第七月复盘",
        days: [
          { n:209, topic:"周总结：区域破局的密码", field:"交叉学科", desc:"俯瞰全球六大板块，找找看有没有哪个被忽略的角落，隐藏着下一个时代的爆发节点？", review:true, cross:true },
          { n:210, topic:"第七月复盘：成为合格的「地球玩家」", field:"大复盘", desc:"地理不再是死板的地图，而是利益流动的管道。你现在已经拥有了一双能够看透国际风云变换的「X光眼」。", review:true },
        ]
      },
    ]
  },
  {
    id: 8,
    icon: "💰",
    color: "#c87a5a",
    days: "Day 211–240",
    range: [211, 240],
    title: "商业帝国、资本流转与组织演化",
    subtitle: "现实世界的「财富引擎」",
    desc: "企业本质·财务·资本逻辑·商业演化·组织病理·平台经济",
    weeks: [
      {
        title: "W36 · 企业本质与财务",
        days: [
          { n:211, topic:"科斯定理与交易成本", field:"企业本质", desc:"为什么我们不全都是自由职业者？企业的诞生，本质上是为了用「内部管理成本」去抵消「外部交易成本」。" },
          { n:212, topic:"泰勒制与科学管理", field:"管理溯源", desc:"现代职场的底层诅咒。理解一百年前的工厂是如何把人剥夺为机器上的「标准化零件」的。" },
          { n:213, topic:"资产负债表的「上帝视角」", field:"财务思维", desc:"理解一家公司的健康程度，完全取决于它的钱从哪里来（负债/权益），又去了哪里（资产）。" },
          { n:214, topic:"现金流：企业的真实血液", field:"财务思维", desc:"为什么很多账面疯狂盈利的公司会突然倒闭？利润只是会计的「意见」，而现金流才是冰冷的「事实」。" },
          { n:215, topic:"风险投资（VC）与幂律法则", field:"资本逻辑", desc:"为什么资本愿意砸钱让互联网公司无限亏损？VC追求的不是「稳赚」，而是押注那个能带来100倍回报的超级黑马。" },
          { n:216, topic:"垄断的暴利（从0到1）", field:"护城河", desc:"竞争是留给失败者的。真正伟大的企业从不竞争，它们通过技术、网络效应或规模经济，直接创造并垄断一个全新的生态位。" },
          { n:217, topic:"周总结：解剖一头「利润怪兽」", field:"交叉学科", desc:"尝试用资产负债表和交易成本的视角，去拆解你之前待过的公司，或者你正在分析的某个行业巨头。", review:true, cross:true },
        ]
      },
      {
        title: "W37 · 商业演化与护城河",
        days: [
          { n:218, topic:"创新者的窘境", field:"商业演化", desc:"为什么极其优秀、管理完美的大公司，注定会被不起眼的新技术颠覆？因为它们被现有的利润基本盘和高端客户彻底「绑架」了。" },
          { n:219, topic:"网络效应的绝对壁垒", field:"商业演化", desc:"微信、淘宝为什么无法被替代？当一个产品的价值随着用户数量增加而呈指数级暴增时，先发优势将变成绝对的物理壁垒。" },
          { n:220, topic:"规模经济与范围经济", field:"商业演化", desc:"摊薄固定成本的魔法。理解为什么工厂越大、产品线越广，边际成本就越趋近于零，从而形成对小作坊的降维打击。" },
          { n:221, topic:"寻租行为（Rent-seeking）", field:"商业暗面", desc:"不创造任何新财富，仅仅依靠垄断资源、政策壁垒或信息差，强行从系统中切走蛋糕的寄生虫逻辑。" },
          { n:222, topic:"供应链的「牛鞭效应」", field:"商业暗面", desc:"为什么终端消费的一个微小波动，传导到上游工厂会变成巨大的库存灾难？理解信息在商业链路中传递时的极度失真。" },
          { n:223, topic:"品牌与无形资产", field:"价值评估", desc:"为什么贴个Logo就能卖贵十倍？理解「品牌」是如何在消费者大脑中占据极其稀缺的认知带宽，从而转化为真金白银的。" },
          { n:224, topic:"周总结：护城河的深浅", field:"交叉学科", desc:"观察你日常使用的各种AI开发工具和平台，分析它们中谁具有真正的「网络效应」，谁又随时可能被开源大模型替代。", review:true, cross:true },
        ]
      },
      {
        title: "W38-39 · 组织演化与终极进化",
        days: [
          { n:225, topic:"《狗屁工作》（Bullshit Jobs）", field:"组织病理", desc:"为什么技术越发达，社会上反而涌现出越多毫无意义的流程、审批和PPT岗位？理解官僚体系自我繁殖的荒谬逻辑。" },
          { n:226, topic:"劳动的异化与螺丝钉困境", field:"组织病理", desc:"马克思的幽灵。当你无法掌握生产工具，且看不到自己工作最终成果的全貌时，工作不仅不带来成就感，反而变成长期的精神损耗。" },
          { n:227, topic:"稻盛和夫的阿米巴经营", field:"组织创新", desc:"将庞大的企业彻底击碎成一个个独立核算盈亏的小团队。打破大锅饭，让末端员工直接感受到市场的寒气与利润。" },
          { n:228, topic:"零工经济与数字游民", field:"平台经济", desc:"Uber、外卖平台背后的「平台资本主义」。理解系统是如何通过算法接管传统HR的管理职能，并将风险彻底转嫁给个体的。" },
          { n:229, topic:"去中心化自治组织（DAO）", field:"权力重构", desc:"当「智能合约」代替了管理层，当代币经济代替了工资和期权。设想一种没有老板、完全由代码和共识驱动的极端组织形态。" },
          { n:230, topic:"杠杆与个人商业模式", field:"生存策略", desc:"普通人出售时间，聪明人出售可无限复制的数字产品，顶尖者利用资本和他人时间作为杠杆。审视你自己的「变现协议」。" },
          { n:231, topic:"周总结：猎杀形式主义", field:"交叉学科", desc:"结合你对自动化代码部署工具的掌握，构思：如何用AI智能体（Agent）彻底干掉一家公司里80%的「狗屁工作」？", review:true, cross:true },
          { n:232, topic:"B2B复杂销售与采购逻辑", field:"博弈实战", desc:"To B的生意不是卖产品，而是卖「免责声明」。理解企业采购中极其复杂的决策链条、利益输送与防御性心理。" },
          { n:233, topic:"杠杆收购（LBO）的野蛮人", field:"金融掠夺", desc:"华尔街的终极猎杀。如何仅用极少的本金，通过借债买下一家现金流充沛的公司，然后疯狂裁员、拆分变卖来还债并套现。" },
          { n:234, topic:"双层爱尔兰与荷兰三明治", field:"全球避税", desc:"顶级跨国巨头是如何通过极其复杂的离岸架构、知识产权转移，将数百亿美元的利润合法「洗」到免税天堂的。" },
          { n:235, topic:"市场的非理性繁荣", field:"行为金融", desc:"为什么散户总是追涨杀跌？人类演化出的「羊群效应」和「损失厌恶」，在面对冰冷的金融市场时，是如何变成最致命的缺陷的。" },
          { n:236, topic:"AI时代的「一人企业」", field:"终极进化", desc:"当大模型可以代替文案，代码助手可以代替开发，自动化工作流可以代替运营，理解「超级个体」崛起的必然性。" },
          { n:237, topic:"边缘创新与「车库精神」", field:"终极进化", desc:"为什么颠覆性的突破往往不在拥有无限资源的巨头大厦里，而是在那些不受监管、不受KPI束缚的边缘地带爆发。" },
          { n:238, topic:"反脆弱的职业档案", field:"系统重置", desc:"抛弃「依赖单一系统」的线性简历。学会将自己的能力模块化，在剧烈震荡的失业周期中，建立多条互不干扰的独立收益线。" },
          { n:239, topic:"周总结：超级个体的武装", field:"交叉学科", desc:"盘点你武器库里的兵器（HR底层逻辑+3D建模能力+自动化工作流部署），计算一下你现在的「个人运转杠杆率」有多高。", review:true, cross:true },
        ]
      },
      {
        title: "W40 · 第八月复盘",
        days: [
          { n:240, topic:"第八月复盘：看透矩阵（The Matrix）", field:"大复盘", desc:"这一刻，公司、资本、薪酬体系在你眼中不再是神圣的实体，而仅仅是一堆可以被拆解、被优化的规则代码和资源管道。", review:true },
        ]
      },
    ]
  },
  {
    id: 9,
    icon: "🔤",
    color: "#8ac8c8",
    days: "Day 241–270",
    range: [241, 270],
    title: "语言、符号与思想架构",
    subtitle: "心智的「编译语言」",
    desc: "语言起源·认知语言学·符号学·修辞学·话语权力·叙事学",
    weeks: [
      {
        title: "W41 · 语言起源与结构",
        days: [
          { n:241, topic:"聊八卦与虚构的能力", field:"语言起源", desc:"为什么只有智人统治了地球？我们的语言不仅能描述「河边有狮子」（事实），还能描述「河神会发怒」（虚构），从而组织起亿万人的协作。" },
          { n:242, topic:"萨丕尔-沃尔夫假说", field:"认知语言学", desc:"你的母语物理性地限制了你的世界观。如果一个部落的语言里没有「明天」这个词，他们就真的无法理解储蓄和规划的概念。" },
          { n:243, topic:"索绪尔的语言网络", field:"结构主义", desc:"词语本身没有任何绝对意义。意义只存在于词与词之间的「差异网络」中。" },
          { n:244, topic:"言语行为理论（Speech Acts）", field:"语用学", desc:"语言不仅描述世界，还能「物理性地改变世界」。比如法官说「我宣布你们结为夫妻」，这句话一旦说出，现实的法律关系瞬间重构。" },
          { n:245, topic:"语言的自私基因（Meme）", field:"模因论", desc:"为什么有些洗脑神曲或网络烂梗能像病毒一样劫持你的大脑？思想也是一种寄生物，它们会利用你的嘴巴进行自我繁殖。" },
          { n:246, topic:"我们赖以生存的隐喻", field:"隐喻机制", desc:"「争论是战争」、「时间是金钱」。人类极其缺乏抽象思考能力，所有高级复杂的概念，底层全部是建立在简单的身体物理隐喻之上的。" },
          { n:247, topic:"周总结：审视「职场黑话」", field:"交叉学科", desc:"挑出你以前做HR时最讨厌的5个词（如赋能、抓手、闭环），拆解它们是如何通过「隐喻」来掩盖管理无能和压榨本质的。", review:true, cross:true },
        ]
      },
      {
        title: "W42 · AI语言学",
        days: [
          { n:248, topic:"罗兰·巴特的神话学", field:"符号学", desc:"一张照片、一件衣服、一杯咖啡，是如何被偷偷塞进意识形态「私货」的？破解消费社会是如何用视觉符号给你洗脑的。" },
          { n:249, topic:"乔姆斯基的普遍语法", field:"计算语言学", desc:"极其硬核的假设：人类大脑里是不是天生就插着一块「语法芯片」？为什么小孩子不用学语法就能自动说出复杂的长句？" },
          { n:250, topic:"词向量（Word2Vec）", field:"自然语言处理", desc:"AI时代的必修课。机器如何把抽象的词汇变成多维空间里的数学坐标？（国王 - 男人 + 女人 = 女王，语言变成了纯粹的几何距离）" },
          { n:251, topic:"Token的物理机制", field:"大模型原理", desc:"为什么AI不懂「字」，只懂「Token」？揭开大语言模型（如ChatGPT、Claude）做文字接龙的底层概率学真相。" },
          { n:252, topic:"语言的不可译性", field:"翻译哲学", desc:"为什么最高级的诗歌和最深的幽默，永远无法跨语言完美传输？语言的底层绑定了极其深厚的局部历史经验。" },
          { n:253, topic:"编码与解码的漏斗效应", field:"信息损耗", desc:"为什么你说明白了，对方却听不懂？信息在两个碳基大脑间传输时，要经过「我想-我说-他听-他懂」四层严重的降噪衰减。" },
          { n:254, topic:"周总结：提示词工程师的觉醒", field:"交叉学科", desc:"用NLP词向量的逻辑，重新审视你用来生成3D模型和图像的Prompt。如何用「机器的语言习惯」去控制机器，而不是用人类的废话。", review:true, cross:true },
        ]
      },
      {
        title: "W43-44 · 修辞·权力话语·叙事",
        days: [
          { n:255, topic:"亚里士多德的三大诉诸", field:"修辞学", desc:"说服他人的终极公式：Ethos（人格信用）、Pathos（情感共鸣）、Logos（逻辑推理）。缺一不可的操控术。" },
          { n:256, topic:"福柯的监狱与疯人院", field:"权力话语", desc:"谁掌握了「精神病」、「罪犯」和「正常」的定义权，谁就掌握了社会的绝对控制权。话语权就是最顶级的暴力。" },
          { n:257, topic:"群体洗脑术与戈培尔效应", field:"宣传学", desc:"极简的口号、不断地重复。为什么越反智、越极端的语言，在群体中的煽动性反而越强？（警惕任何口号式的管理标语）" },
          { n:258, topic:"《1984》的新话（Newspeak）", field:"政治正确", desc:"现实版的思想阉割：如果你把字典里「造反」这个词彻底删掉，人们还能造反吗？词汇库的缩小等同于思维带宽的萎缩。" },
          { n:259, topic:"幽默与笑的底层机制", field:"心理学", desc:"乖讧论与预期失调：为什么我们会笑？那是大脑的预期被建立，然后突然被打破时，系统给予的一种认知补偿奖励。" },
          { n:260, topic:"英雄之旅（The Hero's Journey）", field:"叙事学", desc:"为什么好莱坞大片和神话故事，底层的剧情公式几千年来一模一样？掌握这套公式，你就掌握了打造爆款内容的终极说明书。" },
          { n:261, topic:"周总结：解剖老板的演讲稿", field:"交叉学科", desc:"用这周学的修辞和权力话语理论，去解剖一篇充斥着「画大饼」的内部演讲稿。你会发现它漏洞百出，全是情绪操控的套路。", review:true, cross:true },
          { n:262, topic:"文字对记忆的剥夺", field:"媒介变迁", desc:"柏拉图的古老担忧：为什么文字的发明让人类记忆力急速衰退，却让文明得以指数级累积和保存？" },
          { n:263, topic:"从抽象退回直觉", field:"视觉语言", desc:"短视频时代的退化：我们是如何从需要深度脑力解析的「抽象文字逻辑」，退化回猴子般条件反射的「视觉多巴胺刺激」的？" },
          { n:264, topic:"测谎与微表情代码", field:"身体语言", desc:"90%的信息传递不靠嘴。理解面部肌肉和肢体动作中无法掩饰的潜意识代码，这是看透人际伪装的X光。" },
          { n:265, topic:"高语境与低语境", field:"文化语境", desc:"为什么东方的沟通「尽在不言中」（高语境），而西方的沟通必须「契约写死」（低语境）？跨国协作和沟通的终极鸿沟。" },
          { n:266, topic:"维特根斯坦的叹息", field:"哲学", desc:"「我的语言的界限，就是我的世界的界限。凡是不可言说的，必须保持沉默。」承认人类表达能力的终极天花板。" },
          { n:267, topic:"沟通的终极悲剧与孤独", field:"存在主义", desc:"无论语言多么精确，你永远无法将自己的痛感、快乐或迷茫100%地传递给另一个人。我们被永远锁死在自己的头骨里。" },
          { n:268, topic:"脑机接口（BCI）的未来", field:"人机交互", desc:"如果我们能直接通过意念交换神经信号，语言这种低效、容易产生误解的协议会被彻底淘汰吗？" },
        ]
      },
      {
        title: "W45 · 第九月复盘",
        days: [
          { n:269, topic:"周总结：低能耗的防御工具", field:"交叉学科", desc:"在你极度厌恶的「无效社交」中，如何把语言从「真心话」转变为一种极低能耗的、格式化的防御和破冰工具？", review:true, cross:true },
          { n:270, topic:"第九月复盘：万物皆为文本", field:"大复盘", desc:"掌握了语言和符号的源代码，你就不再是被流行词汇操纵的提线木偶，而是现实逻辑的重构者。", review:true },
        ]
      },
    ]
  },
  {
    id: 10,
    icon: "🎯",
    color: "#c8a07a",
    days: "Day 271–365",
    range: [271, 365],
    title: "心智算法·未来视野·大一统闭环",
    subtitle: "个体破局的底层代码",
    desc: "行为经济学·决策科学·未来科技·大一统验证·个人重构",
    weeks: [
      {
        title: "W46 · 行为经济学与决策科学",
        days: [
          { n:271, topic:"锚定效应（Anchoring）", field:"行为经济学", desc:"为什么第一印象或第一个报价会锁死后续所有的谈判？理解大脑在缺乏信息时，是如何死死抓住任意一个随机数字作为参照物的。" },
          { n:272, topic:"前景理论与损失厌恶", field:"行为经济学", desc:"捡到100块的快乐，远远抵消不了丢掉100块的痛苦。理解为什么在面对职业转型时，人们总是极度抗拒离开「安全区」。" },
          { n:273, topic:"禀赋效应（Endowment Effect）", field:"行为经济学", desc:"为什么一旦你拥有了某样东西（比如一个鸡肋的岗位），你对它的估值就会莫名其妙地变高？拆解「敝帚自珍」的非理性逻辑。" },
          { n:274, topic:"沉没成本谬误", field:"决策科学", desc:"过去投入的时间和金钱，都是无法收回的「死钱」。理性的决策应该只看「未来的收益」。如何果断斩断一条走不通的代码链路或错误规划。" },
          { n:275, topic:"幸存者偏差", field:"认知偏差", desc:"死人不会说话。为什么你看到的成功学或爆款项目都是骗人的？因为你根本没看到那99%遵循同样逻辑却死在水底的失败者。" },
          { n:276, topic:"达克效应（Dunning-Kruger Effect）", field:"认知偏差", desc:"越无知的人越自信，越专业的人越自我怀疑。警惕那种「我已掌握全貌」的愚昧之巅幻觉。" },
          { n:277, topic:"周总结：大脑的Bug清单", field:"交叉学科", desc:"盘点过去一年里，你因为「损失厌恶」或「沉没成本」而拖延去做的一项重要决定。现在用冷酷的算法逻辑重新审视它。", review:true, cross:true },
        ]
      },
      {
        title: "W47-48 · 决策模型与心智管理",
        days: [
          { n:278, topic:"探索与利用困境（Explore vs. Exploit）", field:"决策模型", desc:"吃饭是去老字号（利用已知高收益），还是去试新店（探索未知可能）？如何分配「死磕旧技能」与「尝试新插件」的数学时间比。" },
          { n:279, topic:"逆向思维（Inversion）", field:"决策模型", desc:"查理·芒格的绝招：如果你不知道怎么做才能成功，那就先列出所有会导致你失败的事情，然后死死避开它们。" },
          { n:280, topic:"期望值计算与底线思维", field:"概率思维", desc:"不看单次输赢，只算长期期望。在选择投入精力去做一个新项目时，如何计算它长期的复利价值是否大于单次的痛苦折磨。" },
          { n:281, topic:"信号与噪声", field:"信息过滤", desc:"为什么每天刷到海量的新AI工具会让人极度焦虑？因为99%是换汤不换药的噪声。学会关闭感官，只捕捉底层的技术「信号」。" },
          { n:282, topic:"课题分离（阿德勒心理学）", field:"心智管理", desc:"「别人怎么评价我，那是别人的课题；我怎么做事，是我的课题。」这是在物理和心理层面，屠宰无意义人际内耗的终极武器。" },
          { n:283, topic:"习得性无助与归因理论", field:"个体心理", desc:"为什么大象会被一根细绳拴住？理解系统性的打击是如何摧毁个体的反抗意志的，以及如何通过微小的「可控感」重新夺回生活的主导权。" },
          { n:284, topic:"周总结：冷酷的概率玩家", field:"交叉学科", desc:"结合这周的决策模型，为你正在进行的「多线并行学习计划」设定一个数学上的止损点和收益期望值。", review:true, cross:true },
          { n:285, topic:"心流理论（Flow）", field:"深度状态", desc:"为什么在调整3D模型参数或Vibe Coding时，几个小时会瞬间消失？理解挑战与技能绝对匹配时，大脑进入的那种极致免打扰的狂喜状态。" },
          { n:286, topic:"刻意练习（Deliberate Practice）", field:"技能习得", desc:"为什么单纯的重复毫无意义？真正的精进需要走出舒适区、建立高度专注的反馈循环，并对内部运作逻辑进行极其痛苦的「拆解重组」。" },
          { n:287, topic:"身份认同与微小习惯", field:"系统习惯", desc:"改变行为的最高境界不是设定目标（「我要学编程」），而是改变身份认同（「我是一个通过代码解决问题的人」）。" },
          { n:288, topic:"能量节律与抗压防线", field:"精力管理", desc:"时间管理是伪命题，精力管理才是真相。如何根据自己的生理波峰波谷，来安排高强度的逻辑推演与低强度的机械性日常任务。" },
          { n:289, topic:"关系中的权力与边界", field:"人际博弈", desc:"无效社交的本质是缺乏核心交换价值。如何通过建立不可替代的「硬核技术杠杆」，让繁琐的职场人际关系变得毫无必要。" },
          { n:290, topic:"非暴力沟通与事实陈述", field:"沟通模型", desc:"剥离情绪，只陈述事实、感受和具体需求。这是一种像写代码一样精确、不易产生Bug的高级沟通协议。" },
        ]
      },
      {
        title: "W49 · 未来视野与技术奇点",
        days: [
          { n:291, topic:"周总结：构建个人操作系统", field:"交叉学科", desc:"梳理出一份属于你的「SOP（标准作业程序）」：当你面对一个全新的、复杂的技能挑战时，你第一步做什么，第二步做什么。", review:true, cross:true },
          { n:292, topic:"刺猬与狐狸理论", field:"个体演化", desc:"狐狸知道很多事情（懂很多零碎的工具），而刺猬只知道一件大事（掌握极其深度的底层逻辑）。在不同阶段，如何切换这两种生存策略？" },
          { n:293, topic:"杠铃策略（Barbell Strategy）", field:"风险管理", desc:"塔勒布的生存哲学：把90%的精力放在极其安全、有保底的领域，把10%的精力投在风险极高但可能带来百倍回报的新鲜事物上。拒绝平庸的中等风险。" },
          { n:294, topic:"物质与信息的断舍离", field:"极简主义", desc:"每一件拥有的物品和每一个关注的信息源，都在暗中消耗你的系统内存。切断非必要的物理和数字连接，实现算力最大化。" },
          { n:295, topic:"斯多葛学派（Stoicism）的现代应用", field:"情绪调控", desc:"区分「你能控制的」和「你绝对无法控制的」。将所有的算力全部集中在你能控制的代码、设计和健身上，对外部的评价和经济大环境保持冷酷的漠然。" },
          { n:296, topic:"跨界知识的乘法效应", field:"复利思维", desc:"一个在前25%的HR加上一个前25%的AI工具应用者，其稀缺性远远大于一个前1%的纯HR。理解技能栈的组合杠杆。" },
          { n:297, topic:"你的核心算法是什么？", field:"终极拷问", desc:"抛开所有的外部标签（专业、学历、所在地），如果用一段代码或一个数学公式来描述你的行事风格，它应该是什么样子？" },
        ]
      },
      {
        title: "W50-52 · 大一统闭环与毕业",
        days: [
          { n:301, topic:"通用人工智能（AGI）的临界点", field:"前沿计算", desc:"当机器的智力在每一个单一领域都全面碾压人类时，社会的底层运转逻辑将发生何种根本性断裂？理解「奇点」的物理和哲学意义。" },
          { n:305, topic:"合成生物学与CRISPR", field:"生物科技", desc:"DNA本质上是一套可读写的四进制代码。理解人类如何像敲代码一样剪切基因，将细胞改造成生产新材料、新药物的微观工厂。" },
          { n:317, topic:"模拟宇宙假说（Simulation Theory）", field:"空间哲学", desc:"如果我们在电脑里模拟宇宙的技术越来越强，那么概率上讲，我们自己目前处于「最原始基础宇宙」的概率几乎为零。" },
          { n:322, topic:"费米悖论（Fermi Paradox）", field:"宇宙尺度", desc:"宇宙这么老，星星这么多，为什么我们至今没有看到外星人？这背后隐藏着极其令人不安的统计学真相。" },
          { n:328, topic:"熵寂的终极对抗", field:"宇宙宏图", desc:"回归Day1。如果宇宙的终局注定是冷寂的虚无，那么生命和文明这些不断制造「低熵结构」的努力，在百亿年的尺度下意义何在？" },
          { n:331, topic:"物理与经济的缝合", field:"大一统", desc:"为什么市场会崩溃？用「热力学第二定律（熵增）」重新解释经济学中的周期律。理解每一次经济危机，本质上都是系统在强制排解累积的高熵（泡沫）。" },
          { n:335, topic:"热力学与组织管理的终极对齐", field:"大一统", desc:"公司的本质就是一台「耗散结构机器」。它必须疯狂从外界吞噬利润（低熵），以对抗内部不可避免的流程腐化与人浮于事（高熵）。" },
          { n:345, topic:"万物皆为工作流（Workflow）", field:"行动部署", desc:"从细胞内质网的蛋白合成，到你在电脑上跑通第一个API接口。将生活和创作中的一切复杂问题，强制拆解为有输入、有处理、有输出的SOP模块。" },
          { n:357, topic:"构建个人的绝对「护城河」", field:"终极基建", desc:"你掌握的最核心竞争力，一定不是某个很快会过时的具体工具，而是你这一年练就的、能够瞬间看透任何新事物内部逻辑的「逆向工程能力」。" },
          { n:365, topic:"毕业典礼：成为「文明架构师」", field:"毕业典礼", desc:"一年的时间，每天1小时，365个底层逻辑基站。此时此刻，当你重新睁开眼睛看这个世界，它再也没有秘密。游戏开始。", review:true },
        ]
      },
    ]
  },
];

// ════════════════════════════════════════
// 知识标签系统 — 概念标签映射
// ════════════════════════════════════════
// 核心概念跨模块关联标签（手工定义的跨界概念）
const CONCEPT_TAGS = {
  1:  ['熵','热力学','宇宙起源'],
  2:  ['宇宙起源','量子力学'],
  3:  ['量子力学','宇宙起源'],
  4:  ['量子力学'],
  5:  ['相对论','时空'],
  6:  ['宇宙起源'],
  7:  ['复盘','演化论'],
  8:  ['演化论','基因'],
  9:  ['演化论','基因'],
  10: ['演化论','复杂系统'],
  11: ['博弈论','博弈'],
  12: ['博弈论','博弈'],
  13: ['博弈论','博弈'],
  14: ['复杂系统'],
  15: ['复杂系统'],
  16: ['认知偏差','心理学'],
  17: ['认知偏差','心理学'],
  18: ['认知偏差','心理学'],
  19: ['意识','心理学'],
  20: ['意识','心理学'],
  21: ['意识','神经科学'],
  22: ['神经科学','认知'],
  23: ['认知','神经科学'],
  24: ['心流'],
  25: ['心理学','认知'],
  26: ['认知偏差','决策'],
  27: ['复盘'],
  28: ['系统论','复杂系统'],
  29: ['系统论','复杂系统','熵'],
  30: ['复盘'],
  31: ['经济学','市场'],
  32: ['经济学','市场'],
  33: ['经济学','博弈'],
  34: ['经济学','市场'],
  35: ['经济学','复杂系统'],
  36: ['经济学'],
  37: ['复盘'],
  38: ['进化论','演化论'],
  39: ['演化论'],
  40: ['基因','演化论'],
  41: ['演化论','基因'],
  42: ['神经科学','意识'],
  43: ['神经科学'],
  44: ['心理学'],
  45: ['心理学'],
  46: ['心理学','认知'],
  47: ['复盘'],
  48: ['信息论','复杂系统'],
  49: ['复杂系统','熵'],
  50: ['复杂系统'],
  51: ['复杂系统'],
  52: ['复杂系统','博弈'],
  53: ['博弈论','博弈'],
  54: ['博弈论','博弈'],
  55: ['博弈论'],
  56: ['复盘'],
  57: ['哲学','认识论'],
  58: ['哲学'],
  59: ['哲学','认识论'],
  60: ['哲学'],
  61: ['哲学','伦理'],
  62: ['伦理','哲学'],
  63: ['哲学'],
  64: ['复盘'],
  65: ['经济学','市场'],
  66: ['经济学','市场'],
  67: ['经济学','博弈','市场'],
  68: ['货币','金融','经济学'],
  69: ['金融','复利','杠杆'],
  70: ['经济周期','金融','债务'],
  71: ['政治学','权力'],
  72: ['权力','政治学'],
  73: ['权力','政治学'],
  74: ['权力','经济学','复盘'],
  75: ['社会学','马太效应'],
  76: ['社会学','网络'],
  77: ['社会学','群体'],
  78: ['社会学','消费'],
  79: ['法学'],
  80: ['法学','产权'],
  81: ['社会学','复盘'],
  82: ['管理学','组织'],
  83: ['管理学','委托代理'],
  84: ['管理学','指标'],
  85: ['管理学','组织'],
  86: ['复杂系统','幂律','网络'],
  87: ['复杂系统','反脆弱','熵'],
  88: ['黑天鹅','复杂系统'],
  89: ['管理学','复盘'],
  90: ['复盘'],
  91: ['系统论','工程学'],
  92: ['系统论','工程学'],
  93: ['系统论','工程学','负反馈'],
  94: ['熵','信息论','香农','信息'],
  95: ['计算机','信息论'],
  96: ['计算机','算法'],
  97: ['系统论','复盘'],
  98: ['互联网','网络'],
  99: ['AI','人工智能','神经网络'],
  100: ['AI','人工智能','熵','扩散模型'],
  101: ['AI','人工智能','大模型'],
  102: ['AI','人工智能'],
  103: ['美学','数学'],
  104: ['AI','美学','复盘'],
  105: ['美学','色彩'],
  106: ['设计','美学'],
  107: ['工程学','制造'],
  108: ['能源','科技史'],
  109: ['文明','能源'],
  110: ['文明','化学'],
  111: ['文明','复盘'],
  112: ['文明'],
  113: ['文明','能源'],
  114: ['文明','医学'],
  115: ['文明','机械'],
  116: ['文明','通信'],
  117: ['文明','能源'],
  118: ['文明','能源'],
  119: ['AI','奇点','技术奇点'],
  120: ['文明','复盘'],
  121: ['艺术','美学'],
  122: ['艺术','美学','数学'],
  123: ['艺术','美学'],
  124: ['艺术','光影'],
  125: ['艺术','美学'],
  126: ['艺术','美学'],
  127: ['艺术','AI','复盘'],
  128: ['建筑','美学'],
  129: ['建筑','美学'],
  130: ['建筑','设计','美学'],
  131: ['建筑','权力'],
  132: ['建筑','美学'],
  133: ['设计','美学','信息'],
  134: ['建筑','权力','复盘'],
  135: ['媒介','信息'],
  136: ['符号学','信息'],
  137: ['媒介','认知'],
  138: ['艺术','符号学'],
  139: ['媒介','消费'],
  140: ['AI','潜空间','信息'],
  141: ['媒介','AI','复盘'],
  142: ['消费','美学'],
  143: ['美学'],
  144: ['AI','设计'],
  145: ['游戏','反馈'],
  146: ['管理学','美学'],
  147: ['AI','伦理'],
  148: ['AI','艺术'],
  149: ['哲学','大一统'],
  150: ['复盘'],
  151: ['数学'],
  152: ['数学','密码学'],
  153: ['数学','AI','线性代数'],
  154: ['数学','AI','微积分'],
  155: ['数学','拓扑'],
  156: ['数学','复杂系统','分形'],
  157: ['哲学','逻辑'],
  158: ['统计学','决策'],
  159: ['统计学'],
  160: ['统计学','数据'],
  161: ['密码学','信息'],
  162: ['密码学','信任'],
  163: ['密码学','哈希','信息'],
  164: ['区块链'],
  165: ['密码学','复盘'],
  166: ['网络科学','图论'],
  167: ['网络科学','小世界'],
  168: ['网络科学','幂律','马太效应'],
  169: ['熵','系统论','负熵流','耗散结构'],
  170: ['熵','系统论','耗散结构'],
  171: ['决策','模拟'],
  172: ['决策','金融','风险'],
  173: ['复杂系统','演化论'],
  174: ['熵','信息论','信息','麦克斯韦'],
  175: ['认知偏差','AI','信息'],
  176: ['AI','算法','组织'],
  177: ['AI','潜空间'],
  178: ['AI','数学','光影'],
  179: ['大一统'],
  180: ['复盘'],
  181: ['地缘','地理'],
  182: ['地缘','权力'],
  183: ['地缘','海权'],
  184: ['资源','经济学'],
  185: ['人口','社会学'],
  186: ['全球化','供应链'],
  187: ['地缘','复盘'],
  188: ['气候','地缘'],
  189: ['金融','货币','霸权'],
  190: ['AI','科技','地缘'],
  191: ['粮食','资源'],
  192: ['能源','地缘'],
  193: ['权力','全球化'],
  194: ['地缘','信息','复盘'],
  195: ['互联网','地缘','信息'],
  196: ['太空','地缘'],
  197: ['媒介','文化','权力'],
  198: ['全球化','政治学'],
  199: ['博弈','权力'],
  200: ['地缘','博弈'],
  201: ['地缘','AI','复盘'],
  202: ['地缘','政治学'],
  203: ['地缘'],
  204: ['地缘','供应链'],
  205: ['地缘','资源','能源'],
  206: ['地缘','殖民'],
  207: ['经济学','地缘'],
  208: ['地缘','气候'],
  209: ['复盘'],
  210: ['复盘'],
  211: ['心理学','认知'],
  212: ['心理学','动机'],
  213: ['心理学','创伤'],
  214: ['心理学','意识'],
  215: ['心理学'],
  216: ['心理学','认知偏差'],
  217: ['复盘'],
  218: ['心理学'],
  219: ['认知偏差','心理学'],
  220: ['心理学'],
  221: ['心理学'],
  222: ['心理学','意识'],
  223: ['心理学','神经科学'],
  224: ['心理学','复盘'],
  225: ['人际','社会学'],
  226: ['人际','权力'],
  227: ['人际','社会学'],
  228: ['人际','博弈'],
  229: ['人际','边界'],
  230: ['人际'],
  231: ['人际','复盘'],
  232: ['HR','组织','管理学'],
  233: ['HR','招聘'],
  234: ['HR','激励','管理学'],
  235: ['HR','组织','管理学'],
  236: ['HR','法学'],
  237: ['HR','薪酬'],
  238: ['HR','管理学'],
  239: ['HR','AI','复盘'],
  240: ['复盘'],
  241: ['语言','符号学'],
  242: ['语言','认知'],
  243: ['语言','符号学'],
  244: ['语言'],
  245: ['模因','语言','信息'],
  246: ['语言','认知','隐喻'],
  247: ['语言','复盘'],
  248: ['符号学','媒介'],
  249: ['语言','AI','认知'],
  250: ['AI','语言','词向量'],
  251: ['AI','大模型','语言'],
  252: ['语言','文化'],
  253: ['信息','沟通','信息论'],
  254: ['AI','语言','复盘'],
  255: ['修辞','权力'],
  256: ['权力','话语'],
  257: ['权力','心理学'],
  258: ['政治学','语言','权力'],
  259: ['心理学','幽默'],
  260: ['叙事','模因'],
  261: ['语言','权力','复盘'],
  262: ['媒介','记忆'],
  263: ['媒介','认知'],
  264: ['心理学','沟通'],
  265: ['文化','沟通'],
  266: ['哲学','语言'],
  267: ['哲学','存在主义','孤独'],
  268: ['AI','脑机','语言'],
  269: ['语言','复盘'],
  270: ['复盘'],
  271: ['认知偏差','决策','行为经济学'],
  272: ['认知偏差','决策','行为经济学'],
  273: ['认知偏差','行为经济学'],
  274: ['决策','认知偏差'],
  275: ['认知偏差','统计学'],
  276: ['认知偏差'],
  277: ['决策','复盘'],
  278: ['决策','探索与利用'],
  279: ['决策','逆向思维'],
  280: ['决策','概率','风险'],
  281: ['信息','认知','噪声'],
  282: ['心理学','边界'],
  283: ['心理学'],
  284: ['决策','复盘'],
  285: ['心流','深度状态'],
  286: ['学习','刻意练习'],
  287: ['习惯','身份认同'],
  288: ['精力','系统'],
  289: ['人际','博弈'],
  290: ['沟通','信息'],
  291: ['决策','系统','复盘'],
  292: ['学习','策略'],
  293: ['风险','杠杆','反脆弱'],
  294: ['极简','信息'],
  295: ['哲学','斯多葛','情绪'],
  296: ['技能','复利','跨界'],
  297: ['大一统'],
  301: ['AI','奇点','技术奇点','大一统'],
  305: ['基因','生物','AI'],
  317: ['哲学','宇宙','模拟假说'],
  322: ['宇宙起源','费米悖论'],
  328: ['熵','宇宙','大一统'],
  331: ['熵','经济周期','大一统'],
  335: ['熵','管理学','大一统'],
  345: ['系统论','工作流','大一统'],
  357: ['大一统','学习'],
  365: ['复盘','大一统'],
};

function getDayTags(d) {
  const extras = CONCEPT_TAGS[d.n] || [];
  const all = [...new Set([d.field, ...extras])];
  return all;
}
function getDayTagsStr(d) { return getDayTags(d).join(','); }

// Render legend
const legend = document.getElementById('legend');
MODULES.forEach(m => {
  const item = document.createElement('div');
  item.className = 'legend-item';
  item.innerHTML = `<div class="legend-dot" style="background:${m.color}"></div><span>${m.title}</span>`;
  item.onclick = () => scrollToModule(m.id);
  legend.appendChild(item);
});

function scrollToModule(id) {
  const el = document.getElementById('module-' + id);
  if (el) el.scrollIntoView({ behavior: 'smooth', block: 'center' });
}

// Render grid
const grid = document.getElementById('grid');
// ─── NOTE SYSTEM：文件自携带数据，保存即下载 ───
// 数据存在隐藏 div 的 data-notes 属性里，outerHTML 序列化完全可靠

let memNotes = {};

function loadNotesFromFile() {
  try {
    const raw = document.getElementById('notes-store').getAttribute('data-notes');
    if (raw && raw !== '{}' && raw.trim()) memNotes = JSON.parse(raw);
  } catch(e) { memNotes = {}; }
  // 同时从 localStorage 读取，取更新的那份（两份都有时合并，以文件为准）
  try {
    const ls = JSON.parse(localStorage.getItem('tongshi_notes') || '{}');
    // 以 memNotes 为主，ls 补充没有的条目
    Object.keys(ls).forEach(k => { if (!memNotes[k]) memNotes[k] = ls[k]; });
  } catch(e) {}
}

function persistNotes() {
  // 1. 写入隐藏 div（供 outerHTML 序列化）
  const store = document.getElementById('notes-store');
  if (store) store.setAttribute('data-notes', JSON.stringify(memNotes));
  // 2. 同时写入 localStorage（当次会话内随时可读，下载后打开新文件也不丢）
  try { localStorage.setItem('tongshi_notes', JSON.stringify(memNotes)); } catch(e) {}
}

function updateProgress() {
  const count = Object.keys(memNotes).filter(k => memNotes[k] && memNotes[k].text).length;
  document.getElementById('progress-fill').style.width = Math.round(count / 365 * 100) + '%';
  document.getElementById('progress-count').textContent = `${count} / 365 天`;
}

function setSyncUI(msg, cls) {
  const el = document.getElementById('sync-status');
  if (el) { el.textContent = msg; el.className = 'sync-status ' + cls; }
}

function toggleNoteDisplay(dayNum) {
  const wrap = document.getElementById('note-display-wrap-' + dayNum);
  if (wrap) wrap.classList.toggle('collapsed');
}

function toggleNote(dayNum) {
  const editor = document.getElementById('note-editor-' + dayNum);
  const wrap   = document.getElementById('note-display-wrap-' + dayNum);
  if (editor.classList.contains('open')) {
    editor.classList.remove('open');
    if (memNotes[dayNum] && memNotes[dayNum].text) wrap.classList.add('visible');
  } else {
    editor.classList.add('open');
    wrap.classList.remove('visible');
    document.getElementById('note-ta-' + dayNum).focus();
  }
}

function saveNote(dayNum) {
  const ta       = document.getElementById('note-ta-'           + dayNum);
  const ts       = document.getElementById('note-ts-'           + dayNum);
  const toggle   = document.getElementById('note-toggle-'       + dayNum);
  const display  = document.getElementById('note-display-'      + dayNum);
  const wrap     = document.getElementById('note-display-wrap-' + dayNum);
  const dayNumEl = document.getElementById('daynum-'            + dayNum);
  const text     = ta.value.trim();

  if (text) {
    const now     = new Date();
    const dateStr = `${now.getFullYear()}/${now.getMonth()+1}/${now.getDate()} ` +
                    `${now.getHours()}:${String(now.getMinutes()).padStart(2,'0')}`;
    memNotes[dayNum] = { text, date: dateStr };
    ts.textContent   = dateStr + ' 已保存';
    toggle.classList.add('has-note');
    toggle.querySelector('.nt-label').textContent = '编辑感悟';
    display.textContent = text;
    wrap.classList.add('visible');
    wrap.classList.remove('collapsed');
    if (dayNumEl) dayNumEl.classList.add('noted');
  } else {
    delete memNotes[dayNum];
    ts.textContent = '';
    toggle.classList.remove('has-note');
    toggle.querySelector('.nt-label').textContent = '记录感悟';
    display.textContent = '';
    wrap.classList.remove('visible');
    if (dayNumEl) dayNumEl.classList.remove('noted');
  }

  persistNotes();
  updateProgress();
  injectMonthlySummary();
  downloadFile();
}

function downloadFile() {
  setSyncUI('⬇ 生成中…', 'sync-saving');

  // outerHTML 此时已包含最新的 data-notes 属性
  const html  = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
  const blob  = new Blob([html], { type: 'text/html;charset=utf-8' });
  const url   = URL.createObjectURL(blob);
  const a     = document.createElement('a');
  const now   = new Date();
  const stamp = `${now.getFullYear()}${String(now.getMonth()+1).padStart(2,'0')}${String(now.getDate()).padStart(2,'0')}`;
  a.href      = url;
  a.download  = `通识框架_${stamp}.html`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);

  setSyncUI('✓ 已下载', 'sync-saved');
  setTimeout(() => setSyncUI('◈ 文件即数据库', 'sync-idle'), 2500);
}

function clearNote(dayNum) {
  if (!confirm('确定删除这条感悟笔记？')) return;
  document.getElementById('note-ta-' + dayNum).value = '';
  document.getElementById('note-editor-' + dayNum).classList.remove('open');
  saveNote(dayNum);
}

// ─── RENDER ───
function renderAll() {
  const grid = document.getElementById('grid');
  grid.innerHTML = '';

  MODULES.forEach(m => {
    const card = document.createElement('div');
    card.className = 'module';
    card.id = 'module-' + m.id;

    const weeksHTML = m.weeks.map(w => {
      const daysHTML = w.days.map(d => {
        const tags = [];
        if (d.review) tags.push('<span class="tag tag-review">月复盘</span>');
        if (d.cross)  tags.push('<span class="tag tag-cross">交叉学科</span>');

        const savedNote    = memNotes[d.n];
        const hasNote      = savedNote && savedNote.text;
        const noteText     = hasNote ? savedNote.text : '';
        const noteDate     = hasNote ? savedNote.date : '';
        const notedClass   = hasNote ? 'noted' : '';
        const hasNoteClass = hasNote ? 'has-note' : '';
        const toggleLabel  = hasNote ? '编辑感悟' : '记录感悟';
        const wrapVis      = hasNote ? 'visible' : '';

        // 计算标签
        const dayTagsArr = getDayTags(d);
        const dayTagsStr = dayTagsArr.join(',');
        const tagChipsHTML = dayTagsArr.map(t =>
          `<span class="tag-chip" onclick="event.stopPropagation();filterTag('${t.replace(/'/g,"\\'")}',this);">${t}</span>`
        ).join('');

        return `
          <div class="day" data-day="${d.n}" data-tags="${dayTagsStr}">
            <div class="day-num ${notedClass}" id="daynum-${d.n}">D${d.n}${hasNote ? ' ✦' : ''}</div>
            <div class="day-content">
              <div class="day-topic"><em>${d.field}</em>${d.topic}</div>
              <div class="day-desc">${d.desc}</div>
              ${tags.join('')}
              <div class="day-tags">${tagChipsHTML}</div>
              <div class="note-area">
                <button class="note-toggle ${hasNoteClass}" id="note-toggle-${d.n}" onclick="toggleNote(${d.n})">
                  <span class="nt-icon"></span>
                  <span class="nt-label">${toggleLabel}</span>
                </button>
                <button class="link-btn" onclick="addLink(${d.n})" title="添加跨模块关联">🔗</button>
                <div class="day-links" id="day-links-${d.n}"></div>
                <div class="note-display-wrap ${wrapVis}" id="note-display-wrap-${d.n}">
                  <div class="note-display-header" onclick="toggleNoteDisplay(${d.n})">
                    <span class="note-display-label">✦ 我的感悟 <span class="note-display-arrow">▾</span></span>
                    <span style="font-size:10px;color:var(--text3)">${noteDate}</span>
                  </div>
                  <div class="note-display" id="note-display-${d.n}">${noteText}</div>
                </div>
                <div class="note-editor" id="note-editor-${d.n}">
                  <textarea class="note-textarea" id="note-ta-${d.n}"
                    placeholder="在这里写下今天的感悟、重要知识点、联想或疑问……">${noteText}</textarea>
                  <div class="note-actions">
                    <button class="note-save" onclick="saveNote(${d.n})">保存并下载</button>
                    <button class="note-clear" onclick="clearNote(${d.n})">删除</button>
                    <span class="note-timestamp" id="note-ts-${d.n}">${noteDate ? noteDate + ' 已保存' : ''}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>`;
      }).join('');

      return `
        <div class="week">
          <div class="week-header" onclick="toggleWeek(this)">
            <span class="week-arrow">▶</span>
            <span class="week-title">${w.title}</span>
            <span class="week-days-count">${w.days.length} days</span>
          </div>
          <div class="days">${daysHTML}</div>
        </div>`;
    }).join('');

    card.innerHTML = `
      <div class="module-header" onclick="toggleModule(this.parentElement)">
        <div class="module-accent" style="background:${m.color}"></div>
        <div class="module-icon" style="background:${m.color}18; color:${m.color}">${m.icon}</div>
        <div class="module-meta">
          <div class="module-num">MODULE ${String(m.id).padStart(2,'0')}</div>
          <div class="module-title" style="color:${m.color}">${m.title}
            <span style="font-family:'Noto Sans SC';font-size:11px;font-weight:400;color:var(--text3);margin-left:8px;">${m.subtitle}</span>
          </div>
          <div class="module-days" style="color:${m.color}77">${m.desc}</div>
        </div>
        <div class="module-right">
          <span class="module-range-badge" style="border-color:${m.color}44;color:${m.color}99">${m.days}</span>
          <span class="module-chevron" style="color:${m.color}88">▶</span>
        </div>
      </div>
      <div class="weeks">${weeksHTML}</div>`;
    grid.appendChild(card);
  });

  updateProgress();
}

// ─── BOOT ───
loadNotesFromFile();
renderAll();
setSyncUI('◈ 文件即数据库', 'sync-idle');
highlightToday();
initEbbinghaus();

// ════════════════════════════════════════
// ① 今日高亮
// ════════════════════════════════════════
function highlightToday() {
  // 计算今天是第几天：从文件创建/首次打开日起算
  // 用 localStorage 记录首次打开日期
  let startStr = localStorage.getItem('tongshi_start');
  if (!startStr) {
    startStr = new Date().toISOString().slice(0, 10);
    localStorage.setItem('tongshi_start', startStr);
  }
  const start   = new Date(startStr);
  const today   = new Date();
  today.setHours(0, 0, 0, 0);
  start.setHours(0, 0, 0, 0);
  const dayNum  = Math.floor((today - start) / 86400000) + 1;
  if (dayNum < 1 || dayNum > 365) return;

  // 找到对应 day 元素，展开它所在的 module + week，并高亮
  const dayNumEl = document.getElementById('daynum-' + dayNum);
  if (!dayNumEl) return;
  const dayEl  = dayNumEl.closest('.day');
  const weekEl = dayNumEl.closest('.week');
  const modEl  = dayNumEl.closest('.module');
  if (dayEl)  dayEl.classList.add('today');
  if (dayNumEl) dayNumEl.classList.add('today-num');
  // 在主题后插入 TODAY 标记
  const topicEl = dayEl.querySelector('.day-topic');
  if (topicEl && !topicEl.querySelector('.today-badge')) {
    const badge = document.createElement('span');
    badge.className = 'today-badge';
    badge.textContent = 'TODAY';
    topicEl.appendChild(badge);
  }
  // 自动展开
  if (modEl)  modEl.classList.add('active');
  if (weekEl) weekEl.classList.add('open');
  // 平滑滚动
  setTimeout(() => dayEl.scrollIntoView({ behavior: 'smooth', block: 'center' }), 400);
}

// ════════════════════════════════════════
// ② 搜索
// ════════════════════════════════════════
// ② 搜索 — 结果列表模式，可点击跳转
// ════════════════════════════════════════
let searchTimer = null;
// 预先建立全量 day 数据索引（含模块信息），避免每次搜索遍历 DOM
let _daySearchIndex = null;
function getDaySearchIndex() {
  if (_daySearchIndex) return _daySearchIndex;
  _daySearchIndex = [];
  MODULES.forEach(m => {
    m.weeks.forEach(w => {
      w.days.forEach(d => {
        _daySearchIndex.push({
          n: d.n,
          topic: d.topic,
          field: d.field,
          desc: d.desc,
          moduleTitle: m.title,
          moduleColor: m.color,
        });
      });
    });
  });
  return _daySearchIndex;
}

function doSearch(q) {
  clearTimeout(searchTimer);
  searchTimer = setTimeout(() => _execSearch(q.trim()), 160);
}

function _execSearch(q) {
  const countEl   = document.getElementById('search-count');
  const resultsEl = document.getElementById('search-results');

  if (!q) {
    countEl.textContent = '';
    resultsEl.classList.remove('open');
    resultsEl.innerHTML = '';
    return;
  }

  const lower = q.toLowerCase();
  const idx   = getDaySearchIndex();
  const hits  = [];

  idx.forEach(d => {
    const noteObj  = memNotes[d.n];
    const noteText = noteObj ? noteObj.text : '';
    const combined = (d.topic + d.field + d.desc + noteText).toLowerCase();
    if (!combined.includes(lower)) return;

    // 生成高亮片段
    function hl(str) {
      if (!str) return '';
      const esc = q.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
      return str.replace(new RegExp(esc, 'gi'), m => `<span class="sr-hl">${m}</span>`);
    }
    // 摘要：取 desc 或 note 里匹配的上下文
    let noteSnippet = '';
    if (noteText && noteText.toLowerCase().includes(lower)) {
      const pos   = noteText.toLowerCase().indexOf(lower);
      const start = Math.max(0, pos - 20);
      const raw   = (start > 0 ? '…' : '') + noteText.slice(start, pos + q.length + 40) + '…';
      noteSnippet = hl(raw);
    }

    hits.push({ ...d, noteText, noteSnippet, hlTopic: hl(d.topic), hlField: hl(d.field) });
  });

  countEl.textContent = hits.length ? `${hits.length} 条` : '无结果';

  if (!hits.length) {
    resultsEl.innerHTML = `<div class="search-no-result">没有找到「${q}」相关内容</div>`;
    resultsEl.classList.add('open');
    return;
  }

  resultsEl.innerHTML = hits.map(h => `
    <div class="search-result-item" onclick="jumpToDay(${h.n});clearSearch()">
      <div class="sr-num">D${h.n}</div>
      <div class="sr-body">
        <div class="sr-topic">${h.hlTopic}</div>
        <div class="sr-meta">${h.hlField} · ${h.moduleTitle}</div>
        ${h.noteSnippet ? `<div class="sr-note">✦ ${h.noteSnippet}</div>` : ''}
      </div>
    </div>`).join('');
  resultsEl.classList.add('open');
}

function clearSearch() {
  const inp = document.getElementById('search-input');
  inp.value = '';
  _execSearch('');
}

// ════════════════════════════════════════
// ③ 学习日志（笔记汇总页）
// ════════════════════════════════════════

// 建立 dayNum → {topic, field, moduleTitle} 的索引
function buildDayIndex() {
  const idx = {};
  MODULES.forEach(m => {
    m.weeks.forEach(w => {
      w.days.forEach(d => {
        idx[d.n] = { topic: d.topic, field: d.field, moduleTitle: m.title };
      });
    });
  });
  return idx;
}

function openJournal() {
  const overlay = document.getElementById('journal-overlay');
  const content = document.getElementById('journal-content');
  const idx     = buildDayIndex();

  const entries = Object.keys(memNotes)
    .filter(k => memNotes[k] && memNotes[k].text)
    .sort((a, b) => b - a); // 倒序（最近在上）

  if (!entries.length) {
    content.innerHTML = `<div class="journal-empty">还没有任何感悟笔记。<br>学完第一天，回来写下你的第一条感悟吧。</div>`;
  } else {
    content.innerHTML = entries.map(k => {
      const note = memNotes[k];
      const info = idx[k] || { topic: 'Day ' + k, field: '', moduleTitle: '' };
      return `
        <div class="journal-entry" onclick="jumpToDay(${k})">
          <div class="journal-entry-head">
            <span class="journal-day-num">DAY ${k}</span>
            <span class="journal-topic">${info.topic}</span>
            <span class="journal-module">${info.moduleTitle}</span>
          </div>
          <div class="journal-date">${note.date} · ${info.field}</div>
          <div class="journal-text">${note.text}</div>
        </div>`;
    }).join('');
  }
  overlay.classList.add('open');
}

function closeJournal() {
  document.getElementById('journal-overlay').classList.remove('open');
}

function jumpToDay(dayNum) {
  closeJournal();
  const el = document.getElementById('daynum-' + dayNum);
  if (!el) return;
  el.closest('.module')?.classList.add('active');
  el.closest('.week')?.classList.add('open');
  setTimeout(() => el.closest('.day').scrollIntoView({ behavior: 'smooth', block: 'center' }), 200);
}

// ════════════════════════════════════════
// ④ 跨模块关联标注
// ════════════════════════════════════════
function getLinks() {
  try { return JSON.parse(localStorage.getItem('tongshi_links') || '{}'); } catch { return {}; }
}
function saveLinks(links) {
  localStorage.setItem('tongshi_links', JSON.stringify(links));
  // 同步写入 data-links 属性供文件导出
  document.getElementById('notes-store').setAttribute('data-links', JSON.stringify(links));
}

function addLink(fromDay) {
  const target = prompt(`将 Day ${fromDay} 关联到哪一天？（输入天数，如 94）`);
  if (!target || isNaN(target)) return;
  const t = parseInt(target);
  if (t < 1 || t > 365 || t === fromDay) return alert('请输入 1–365 之间的有效天数');

  const idx   = buildDayIndex();
  const info  = idx[t];
  const label = info ? `Day ${t} · ${info.topic}` : `Day ${t}`;

  const links = getLinks();
  if (!links[fromDay]) links[fromDay] = [];
  if (links[fromDay].find(l => l.to === t)) return alert('已存在该关联');
  links[fromDay].push({ to: t, label });
  saveLinks(links);
  renderLinks(fromDay);
  downloadFile();
}

function removeLink(fromDay, toDay) {
  const links = getLinks();
  if (!links[fromDay]) return;
  links[fromDay] = links[fromDay].filter(l => l.to !== toDay);
  if (!links[fromDay].length) delete links[fromDay];
  saveLinks(links);
  renderLinks(fromDay);
  downloadFile();
}

function renderLinks(dayNum) {
  const container = document.getElementById('day-links-' + dayNum);
  if (!container) return;
  const links = getLinks();
  const myLinks = links[dayNum] || [];
  container.innerHTML = myLinks.map(l =>
    `<span class="link-chip" onclick="jumpToDay(${l.to})">
      🔗 ${l.label}
      <span class="remove-link" onclick="event.stopPropagation();removeLink(${dayNum},${l.to})">×</span>
    </span>`
  ).join('');
}

function initAllLinks() {
  // 从 data-links 属性恢复（文件自携带）
  try {
    const raw = document.getElementById('notes-store').getAttribute('data-links');
    if (raw && raw !== '{}') localStorage.setItem('tongshi_links', raw);
  } catch(e) {}
  // 渲染所有已有 link 的天
  const links = getLinks();
  Object.keys(links).forEach(k => renderLinks(parseInt(k)));
}

// ════════════════════════════════════════
// ⑧ 知识标签高亮筛选
// ════════════════════════════════════════
let _activeTag = null;

function filterTag(tag, triggerEl) {
  if (_activeTag === tag) { clearTagFilter(); return; }
  _activeTag = tag;

  // 高亮提示条
  const bar  = document.getElementById('tag-filter-bar');
  const info = document.getElementById('tag-filter-info');
  bar.classList.add('visible');

  // 找到所有匹配的 day 元素
  const allDays = document.querySelectorAll('.day[data-tags]');
  let matchCount = 0;
  const matchedModules = new Set();
  const matchedWeeks   = new Set();

  allDays.forEach(el => {
    const tags = (el.getAttribute('data-tags') || '').split(',');
    if (tags.includes(tag)) {
      el.classList.remove('tag-dimmed');
      el.classList.add('tag-matched');
      matchCount++;
      const modEl  = el.closest('.module');
      const weekEl = el.closest('.week');
      if (modEl)  matchedModules.add(modEl);
      if (weekEl) matchedWeeks.add(weekEl);
    } else {
      el.classList.add('tag-dimmed');
      el.classList.remove('tag-matched');
    }
  });

  // 自动展开包含匹配项的 module/week，折叠不含匹配项的
  document.querySelectorAll('.module').forEach(m => {
    if (matchedModules.has(m)) m.classList.add('active');
    else m.classList.remove('active');
  });
  document.querySelectorAll('.week').forEach(w => {
    if (matchedWeeks.has(w)) w.classList.add('open');
    else w.classList.remove('open');
  });

  // 高亮 tag-chip
  document.querySelectorAll('.tag-chip').forEach(chip => {
    chip.classList.toggle('active', chip.textContent === tag);
  });

  info.textContent = `标签「${tag}」共 ${matchCount} 个知识节点`;

  // 显示迷你关系网弹窗
  showTagGraph(tag, triggerEl);

  // 平滑滚动到第一个匹配项
  const first = document.querySelector('.day.tag-matched');
  if (first) setTimeout(() => first.scrollIntoView({ behavior:'smooth', block:'center' }), 300);
}

function clearTagFilter() {
  _activeTag = null;
  document.getElementById('tag-filter-bar').classList.remove('visible');
  document.querySelectorAll('.day').forEach(el => {
    el.classList.remove('tag-dimmed', 'tag-matched');
  });
  document.querySelectorAll('.tag-chip').forEach(c => c.classList.remove('active'));
  closeTagGraph();
}

// ════════════════════════════════════════
// ⑩ 标签迷你关系网浮窗
// ════════════════════════════════════════
let _tgpNodes = [], _tgpEdges = [], _tgpTimer = null;
let _tgpDrag = null, _tgpPanStart = null;
let _tgpOffX = 0, _tgpOffY = 0, _tgpScale = 1;

function showTagGraph(tag, triggerEl) {
  // Collect all days sharing this tag
  const popup  = document.getElementById('tag-graph-popup');
  const canvas = document.getElementById('tag-graph-canvas');
  const W = canvas.width, H = canvas.height;
  const ctx = canvas.getContext('2d');

  // Build nodes from MODULES data
  _tgpNodes = []; _tgpEdges = [];
  const nodeMap = {};
  MODULES.forEach(m => {
    m.weeks.forEach(w => {
      w.days.forEach(d => {
        const tags = getDayTags(d);
        if (!tags.includes(tag)) return;
        const idx = _tgpNodes.length;
        nodeMap[d.n] = idx;
        _tgpNodes.push({
          n: d.n, topic: d.topic, field: d.field,
          tags, color: m.color, moduleId: m.id, moduleTitle: m.title,
          hasNote: !!(memNotes[d.n] && memNotes[d.n].text),
          x: W/2 + (Math.random()-0.5)*W*0.6,
          y: H/2 + (Math.random()-0.5)*H*0.6,
          vx: 0, vy: 0,
        });
      });
    });
  });

  if (_tgpNodes.length === 0) return;

  // Edges: between any two nodes that share ≥1 overlapping concept tag
  const edgeSet = new Set();
  // Also include user-defined links between these nodes
  const links = getLinks();
  _tgpNodes.forEach((a, i) => {
    _tgpNodes.forEach((b, j) => {
      if (j <= i) return;
      // shared tags beyond the current one
      const shared = a.tags.filter(t => b.tags.includes(t)).length;
      const key = i + '-' + j;
      if (shared >= 1 && !edgeSet.has(key)) {
        edgeSet.add(key); _tgpEdges.push({a:i, b:j});
      }
    });
    // user links
    (links[a.n] || []).forEach(lnk => {
      const bi = nodeMap[lnk.to];
      if (bi === undefined) return;
      const k = Math.min(i,bi)+'-'+Math.max(i,bi);
      if (!edgeSet.has(k)) { edgeSet.add(k); _tgpEdges.push({a:i,b:bi,userLink:true}); }
    });
  });

  // Position popup near trigger or center
  _tgpOffX = 0; _tgpOffY = 0; _tgpScale = 1;
  popup.classList.add('open');
  document.getElementById('tgp-title').textContent = '「' + tag + '」关系网';
  document.getElementById('tgp-count').textContent = _tgpNodes.length + ' 个节点';

  // Footer legend: unique module colors
  const mods = [...new Map(_tgpNodes.map(n => [n.moduleId, n])).values()];
  document.getElementById('tgp-footer').innerHTML =
    mods.map(n => `<span><span class="tgp-footer-dot" style="background:${n.color}"></span>${n.moduleTitle.slice(0,6)}</span>`).join(' ') +
    '<span class="tgp-hint">点击跳转 · 拖拽移动 · 滚轮缩放</span>';

  // Position popup
  positionTagPopup(triggerEl);

  // Run mini sim
  let ticks = 0;
  function simStep() {
    const REPEL = 1400, SPRING_K = 0.05, SPRING_LEN = 80, DAMP = 0.82, GRAVITY = 0.025;
    _tgpNodes.forEach(n => { n.fx = 0; n.fy = 0; });
    for (let i = 0; i < _tgpNodes.length; i++) {
      for (let j = i+1; j < _tgpNodes.length; j++) {
        const a = _tgpNodes[i], b = _tgpNodes[j];
        let dx = b.x-a.x, dy = b.y-a.y;
        const d2 = dx*dx+dy*dy+1, d = Math.sqrt(d2);
        const f = REPEL/d2;
        a.fx -= f*dx/d; a.fy -= f*dy/d;
        b.fx += f*dx/d; b.fy += f*dy/d;
      }
    }
    _tgpEdges.forEach(e => {
      const a = _tgpNodes[e.a], b = _tgpNodes[e.b];
      const dx = b.x-a.x, dy = b.y-a.y;
      const d = Math.max(Math.sqrt(dx*dx+dy*dy), 1);
      const f = SPRING_K*(d-SPRING_LEN);
      a.fx += f*dx/d; a.fy += f*dy/d;
      b.fx -= f*dx/d; b.fy -= f*dy/d;
    });
    _tgpNodes.forEach(n => {
      n.fx += (W/2-n.x)*GRAVITY; n.fy += (H/2-n.y)*GRAVITY;
      n.vx = (n.vx+n.fx)*DAMP; n.vy = (n.vy+n.fy)*DAMP;
      n.x = Math.max(26,Math.min(W-26, n.x+n.vx));
      n.y = Math.max(26,Math.min(H-26, n.y+n.vy));
    });
  }
  function drawTgp() {
    ctx.clearRect(0,0,W,H);
    ctx.save();
    ctx.translate(_tgpOffX, _tgpOffY);
    ctx.scale(_tgpScale, _tgpScale);

    // Draw edges
    _tgpEdges.forEach(e => {
      const a = _tgpNodes[e.a], b = _tgpNodes[e.b];
      ctx.beginPath(); ctx.moveTo(a.x,a.y); ctx.lineTo(b.x,b.y);
      ctx.strokeStyle = e.userLink ? '#5a8fc877' : '#c8975855';
      ctx.lineWidth = e.userLink ? 1.8/_tgpScale : 1/_tgpScale;
      ctx.stroke();
    });

    // Draw nodes
    _tgpNodes.forEach((n, i) => {
      const r = n.hasNote ? 11 : 8;
      // Glow for has-note nodes
      if (n.hasNote) {
        ctx.beginPath(); ctx.arc(n.x,n.y,r+4,0,Math.PI*2);
        ctx.fillStyle = n.color+'22'; ctx.fill();
      }
      ctx.beginPath(); ctx.arc(n.x,n.y,r,0,Math.PI*2);
      ctx.fillStyle = n.color+'cc'; ctx.fill();
      ctx.strokeStyle = n.color; ctx.lineWidth = 1.5/_tgpScale; ctx.stroke();

      // Label
      ctx.fillStyle = '#e8e0d0dd';
      ctx.font = `bold ${Math.round(9/_tgpScale)}px 'Noto Sans SC', sans-serif`;
      ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
      ctx.fillText('D'+n.n, n.x, n.y);

      // Topic below
      ctx.fillStyle = '#9a908088';
      ctx.font = `${Math.round(8/_tgpScale)}px 'Noto Sans SC', sans-serif`;
      const label = n.topic.length > 7 ? n.topic.slice(0,6)+'…' : n.topic;
      ctx.fillText(label, n.x, n.y + r + 9/_tgpScale);
    });
    ctx.restore();
  }
  function tick() {
    simStep(); drawTgp();
    if (++ticks < 180) _tgpTimer = requestAnimationFrame(tick);
    else _tgpTimer = null;
  }
  if (_tgpTimer) cancelAnimationFrame(_tgpTimer);
  _tgpTimer = requestAnimationFrame(tick);

  // Events
  setupTgpEvents(canvas);
}

function positionTagPopup(triggerEl) {
  const popup = document.getElementById('tag-graph-popup');
  if (triggerEl) {
    const rect = triggerEl.getBoundingClientRect();
    let top  = rect.bottom + 8;
    let left = rect.left;
    const pw = 420, ph = 320;
    if (left + pw > window.innerWidth - 10) left = window.innerWidth - pw - 10;
    if (top  + ph > window.innerHeight - 10) top = rect.top - ph - 8;
    if (left < 10) left = 10;
    popup.style.top  = top  + 'px';
    popup.style.left = left + 'px';
  } else {
    popup.style.top  = '80px';
    popup.style.left = Math.max(10, (window.innerWidth - 420) / 2) + 'px';
  }
}

function closeTagGraph() {
  document.getElementById('tag-graph-popup').classList.remove('open');
  if (_tgpTimer) { cancelAnimationFrame(_tgpTimer); _tgpTimer = null; }
}

function setupTgpEvents(canvas) {
  const newC = canvas.cloneNode(true);
  canvas.parentNode.replaceChild(newC, canvas);
  const c = newC;
  const W = c.width, H = c.height;

  function localXY(e) {
    const rect = c.getBoundingClientRect();
    return [(e.clientX-rect.left-_tgpOffX)/_tgpScale,
            (e.clientY-rect.top -_tgpOffY)/_tgpScale];
  }
  function hitNode(lx, ly) {
    let best = -1, bestD = Infinity;
    _tgpNodes.forEach((n,i) => {
      const d = Math.hypot(n.x-lx, n.y-ly);
      if (d < 18/_tgpScale && d < bestD) { bestD=d; best=i; }
    });
    return best;
  }

  c.addEventListener('mousedown', e => {
    const [lx,ly] = localXY(e);
    const h = hitNode(lx,ly);
    if (h >= 0) _tgpDrag = { i:h };
    else _tgpPanStart = { x:e.clientX, y:e.clientY, ox:_tgpOffX, oy:_tgpOffY };
    e.stopPropagation();
  });
  c.addEventListener('mousemove', e => {
    if (_tgpDrag) {
      const [lx,ly] = localXY(e);
      _tgpNodes[_tgpDrag.i].x = lx;
      _tgpNodes[_tgpDrag.i].y = ly;
      _tgpNodes[_tgpDrag.i].vx = _tgpNodes[_tgpDrag.i].vy = 0;
      // Redraw immediately
      const ctx2 = c.getContext('2d');
      ctx2.clearRect(0,0,W,H); ctx2.save();
      ctx2.translate(_tgpOffX,_tgpOffY); ctx2.scale(_tgpScale,_tgpScale);
      _tgpEdges.forEach(edge => {
        const a=_tgpNodes[edge.a], b=_tgpNodes[edge.b];
        ctx2.beginPath(); ctx2.moveTo(a.x,a.y); ctx2.lineTo(b.x,b.y);
        ctx2.strokeStyle='#c8975855'; ctx2.lineWidth=1; ctx2.stroke();
      });
      _tgpNodes.forEach(n => {
        ctx2.beginPath(); ctx2.arc(n.x,n.y,8,0,Math.PI*2);
        ctx2.fillStyle=n.color+'cc'; ctx2.fill();
      });
      ctx2.restore();
      return;
    }
    if (_tgpPanStart) {
      _tgpOffX = _tgpPanStart.ox + (e.clientX - _tgpPanStart.x);
      _tgpOffY = _tgpPanStart.oy + (e.clientY - _tgpPanStart.y);
    }
  });
  c.addEventListener('mouseup', e => {
    if (_tgpDrag) {
      const [lx,ly] = localXY(e);
      const h = hitNode(lx,ly);
      if (h >= 0) {
        closeTagGraph();
        jumpToDay(_tgpNodes[h].n);
      }
      _tgpDrag = null;
    }
    _tgpPanStart = null;
  });
  c.addEventListener('wheel', e => {
    e.preventDefault();
    const f = e.deltaY < 0 ? 1.12 : 0.9;
    const rect = c.getBoundingClientRect();
    const mx = e.clientX-rect.left, my = e.clientY-rect.top;
    _tgpOffX = mx - f*(mx-_tgpOffX);
    _tgpOffY = my - f*(my-_tgpOffY);
    _tgpScale = Math.max(0.3, Math.min(4, _tgpScale*f));
  }, { passive:false });

  // Header drag (move the popup)
  const header = document.getElementById('tgp-header');
  let hDrag = null;
  header.addEventListener('mousedown', e => {
    const popup = document.getElementById('tag-graph-popup');
    const rect  = popup.getBoundingClientRect();
    hDrag = { x:e.clientX, y:e.clientY, l:rect.left, t:rect.top };
    e.stopPropagation();
  });
  document.addEventListener('mousemove', e => {
    if (!hDrag) return;
    const popup = document.getElementById('tag-graph-popup');
    popup.style.left = (hDrag.l + e.clientX - hDrag.x) + 'px';
    popup.style.top  = (hDrag.t + e.clientY - hDrag.y) + 'px';
  });
  document.addEventListener('mouseup', () => { hDrag = null; });
}

// ════════════════════════════════════════
// ⑨ 3D 星空知识图谱 · Knowledge Cosmos
// ════════════════════════════════════════
let graphNodes = [], graphEdges = [];
let graphSelected = -1, graphHovered = -1;
let graphFilterMode = 'all';
let graphRenderTimer = null;
let _graphW = 800, _graphH = 600;

// ── 相机状态
let camRotX = 0.25, camRotY = 0.0;
let camFov   = 680;
let camZoom  = 1.0;
let _autoRot = true;          // 空闲时自动慢转
let _isDragging = false;

// ── 背景装饰星（非知识节点）
let bgStars3D = [];

function generateBgStars() {
  bgStars3D = [];
  const golden = Math.PI * (1 + Math.sqrt(5));
  for (let i = 0; i < 700; i++) {
    const y   = 1 - (i / 699) * 2;
    const r   = Math.sqrt(Math.max(0, 1 - y*y));
    const theta = golden * i;
    const R = 500 + (i % 7) * 60;
    bgStars3D.push({
      x: R * r * Math.cos(theta),
      y: R * y,
      z: R * r * Math.sin(theta),
      bright:  0.06 + (i % 5) * 0.05,
      size:    0.25 + (i % 4) * 0.15,
      twPhase: Math.random() * Math.PI * 2,
      twSpeed: 0.004 + Math.random() * 0.012,
    });
  }
}

// ── 构建节点 & 边
function buildGraphData() {
  const nodeMap = {};
  graphNodes = [];
  MODULES.forEach(m => {
    m.weeks.forEach(w => {
      w.days.forEach(d => {
        nodeMap[d.n] = graphNodes.length;
        graphNodes.push({
          n: d.n, topic: d.topic, field: d.field, desc: d.desc || '',
          tags: getDayTags(d), color: m.color,
          moduleId: m.id, moduleTitle: m.title,
          hasNote: !!(memNotes[d.n] && memNotes[d.n].text),
          x3d: 0, y3d: 0, z3d: 0,
          twPhase: Math.random() * Math.PI * 2,
          twSpeed: 0.005 + Math.random() * 0.012,
        });
      });
    });
  });

  graphEdges = [];
  const edgeSet = new Set();
  const links = getLinks();
  Object.keys(links).forEach(from => {
    (links[from] || []).forEach(lnk => {
      const a = nodeMap[parseInt(from)], b = nodeMap[lnk.to];
      if (a === undefined || b === undefined) return;
      const key = Math.min(a,b)+'-'+Math.max(a,b);
      if (!edgeSet.has(key)) { edgeSet.add(key); graphEdges.push({a, b, type:'link'}); }
    });
  });

  const bridgeTags = ['熵','大一统','技术奇点','AI','系统论','负熵流','耗散结构',
    '反脆弱','黑天鹅','博弈论','信息论','演化论','密码学','幂律','复利','心流',
    '模因','潜空间','马太效应','权力','经济周期'];
  const tagMap = {};
  graphNodes.forEach((nd, i) => {
    nd.tags.forEach(t => {
      if (!bridgeTags.includes(t)) return;
      (tagMap[t] = tagMap[t] || []).push(i);
    });
  });
  Object.values(tagMap).forEach(arr => {
    for (let i = 0; i < arr.length; i++) for (let j = i+1; j < arr.length; j++) {
      const key = Math.min(arr[i],arr[j])+'-'+Math.max(arr[i],arr[j]);
      if (!edgeSet.has(key)) { edgeSet.add(key); graphEdges.push({a:arr[i], b:arr[j], type:'tag'}); }
    }
  });
}

// ── 3D 初始化：各模块分布在球面上，节点散布在各模块球簇内
function init3DPositions() {
  // 10个模块均匀分布在球面（黄金螺线）
  const modPos = {};
  const R_sphere = 260;
  MODULES.forEach((m, mi) => {
    const y     = 1 - (mi / 9) * 2;
    const r     = Math.sqrt(Math.max(0, 1 - y*y));
    const theta = Math.PI * (1 + Math.sqrt(5)) * mi;
    modPos[m.id] = { x: R_sphere*r*Math.cos(theta), y: R_sphere*y, z: R_sphere*r*Math.sin(theta) };
  });

  // 每颗知识星用黄金角螺线确定性分布在模块球簇内
  const dayCountPerMod = {};
  graphNodes.forEach(n => { dayCountPerMod[n.moduleId] = (dayCountPerMod[n.moduleId]||0)+1; });
  const dayIdxPerMod = {};
  graphNodes.forEach(n => {
    if (dayIdxPerMod[n.moduleId] === undefined) dayIdxPerMod[n.moduleId] = 0;
    const mc  = modPos[n.moduleId];
    const idx = dayIdxPerMod[n.moduleId]++;
    const tot = dayCountPerMod[n.moduleId];
    // 在模块中心周围用球面均匀分布
    const yy   = 1 - (idx / Math.max(tot-1,1)) * 2;
    const rr   = Math.sqrt(Math.max(0, 1 - yy*yy));
    const ang  = Math.PI * (1 + Math.sqrt(5)) * idx;
    const spread = 75;
    n.x3d = mc.x + spread * rr * Math.cos(ang);
    n.y3d = mc.y + spread * yy;
    n.z3d = mc.z + spread * rr * Math.sin(ang);
  });
}

// ── 透视投影（输入3D坐标 → 屏幕坐标）
function projectPt(x3, y3, z3) {
  // 旋转 Y 轴（水平拖动）
  const cy = Math.cos(camRotY), sy = Math.sin(camRotY);
  const rx = x3*cy + z3*sy;
  const rz = -x3*sy + z3*cy;
  // 旋转 X 轴（垂直拖动）
  const cx = Math.cos(camRotX), sx = Math.sin(camRotX);
  const ry  = y3*cx - rz*sx;
  const rz2 = y3*sx + rz*cx;

  const dist = rz2 + camFov * camZoom;
  if (dist < 20) return null;
  const s = (camFov * camZoom) / dist;
  return { sx: rx*s + _graphW/2, sy: ry*s + _graphH/2, depth: rz2, s };
}

// ── 主渲染
let _t = 0;
function drawGraph() {
  const canvas = document.getElementById('graph-canvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  const W = _graphW, H = _graphH;
  _t += 0.016;

  // 自动慢转
  if (_autoRot && !_isDragging) camRotY += 0.0025;

  ctx.clearRect(0,0,W,H);

  // ── 1. 深空背景渐变
  const bg = ctx.createRadialGradient(W*0.45, H*0.4, 0, W*0.5, H*0.5, W*0.75);
  bg.addColorStop(0, '#07091c'); bg.addColorStop(0.5, '#04060f'); bg.addColorStop(1, '#020307');
  ctx.fillStyle = bg; ctx.fillRect(0,0,W,H);

  // 星云光晕
  [[W*0.28,H*0.32,W*0.32,'rgba(70,50,150,0.055)'],[W*0.7,H*0.62,W*0.25,'rgba(40,80,160,0.04)']].forEach(([nx,ny,nr,col])=>{
    const neb = ctx.createRadialGradient(nx,ny,0,nx,ny,nr);
    neb.addColorStop(0,col); neb.addColorStop(1,'transparent');
    ctx.fillStyle=neb; ctx.fillRect(0,0,W,H);
  });

  // ── 2. 收集所有可见节点 + 背景星，按深度排序（远→近）
  const items = [];

  // 背景装饰星
  bgStars3D.forEach((s, i) => {
    s.twPhase += s.twSpeed;
    const p = projectPt(s.x, s.y, s.z);
    if (!p || p.sx < -20 || p.sx > W+20 || p.sy < -20 || p.sy > H+20) return;
    const tw = 0.75 + 0.25*Math.sin(s.twPhase);
    items.push({ type:'bg', p, bright: s.bright*tw, size: s.size });
  });

  // 知识节点（按 filterMode 过滤）
  const connSet = new Set();
  if (graphSelected >= 0) graphEdges.forEach(e=>{
    if(e.a===graphSelected) connSet.add(e.b);
    if(e.b===graphSelected) connSet.add(e.a);
  });
  const hovConnSet = new Set();
  if (graphHovered >= 0 && graphHovered !== graphSelected) graphEdges.forEach(e=>{
    if(e.a===graphHovered) hovConnSet.add(e.b);
    if(e.b===graphHovered) hovConnSet.add(e.a);
  });

  const visFilter = getVisibleNodeSet();
  graphNodes.forEach((n, i) => {
    if (!visFilter.has(i)) return;
    n.twPhase += n.twSpeed;
    const p = projectPt(n.x3d, n.y3d, n.z3d);
    if (!p || p.sx < -40 || p.sx > W+40 || p.sy < -40 || p.sy > H+40) return;
    const isSel  = i === graphSelected;
    const isConn = connSet.has(i) || hovConnSet.has(i);
    const isHov  = i === graphHovered;
    items.push({ type:'node', i, n, p, isSel, isConn, isHov });
  });

  // 按深度排序：最远的先画
  items.sort((a, b) => (b.p.depth - a.p.depth));

  // ── 3. 画选中节点的连线（在所有星点之前）
  if (graphSelected >= 0) {
    const selNode = graphNodes[graphSelected];
    const pSel = projectPt(selNode.x3d, selNode.y3d, selNode.z3d);
    if (pSel) {
      graphEdges.forEach(e => {
        const other = (e.a === graphSelected) ? e.b : (e.b === graphSelected) ? e.a : -1;
        if (other < 0) return;
        const pOth = projectPt(graphNodes[other].x3d, graphNodes[other].y3d, graphNodes[other].z3d);
        if (!pOth) return;
        // 连线颜色：link=蓝，tag=金
        const col = e.type==='link' ? '#5a8fc8' : '#c8975a';
        const grad = ctx.createLinearGradient(pSel.sx, pSel.sy, pOth.sx, pOth.sy);
        grad.addColorStop(0, col+'cc'); grad.addColorStop(1, col+'22');
        ctx.beginPath(); ctx.moveTo(pSel.sx, pSel.sy); ctx.lineTo(pOth.sx, pOth.sy);
        ctx.strokeStyle = grad; ctx.lineWidth = 0.8; ctx.globalAlpha = 0.7; ctx.stroke();
        ctx.globalAlpha = 1;
      });
    }
  }

  // ── 4. 画所有星点
  items.forEach(item => {
    if (item.type === 'bg') {
      drawParticleStar(ctx, item.p.sx, item.p.sy, item.size * 0.9, item.bright, '#aabde0', false, false, item.p.s);
      return;
    }
    const { i, n, p, isSel, isConn, isHov } = item;

    // 连接度 → 基础大小
    const deg = graphEdges.filter(e=>e.a===i||e.b===i).length;
    const mag = deg > 8 ? 3 : deg > 3 ? 2 : deg > 0 ? 1 : 0;

    // 透视缩放后的物理大小（近大远小）
    const baseSize = ([1.0, 1.5, 2.2, 3.0][mag] + (n.hasNote ? 0.6 : 0)) * Math.min(p.s * 1.2, 2.4);
    const tw = 0.78 + 0.22*Math.sin(n.twPhase);

    // 淡出未相关节点
    let gAlpha = [0.30, 0.52, 0.72, 0.90][mag] * tw;
    if (graphSelected >= 0 && !isSel && !isConn) gAlpha *= 0.06;
    else if (graphHovered >= 0 && graphSelected < 0 && !isHov && !isConn) gAlpha *= 0.15;

    // 颜色：默认冷白，激活时用模块色
    const col = (isSel||isHov||isConn) ? n.color : '#d8e8ff';
    drawParticleStar(ctx, p.sx, p.sy, baseSize * (isSel ? 2.0 : isHov ? 1.5 : 1), gAlpha, col, isSel, isHov||isConn, p.s);
  });
}

// ── 单颗粒子星绘制（纯高斯光晕，无硬边）
function drawParticleStar(ctx, x, y, size, alpha, color, isSelected, isBright, perspScale) {
  if (alpha < 0.01) return;
  ctx.save();

  // 外层大光晕（极淡，营造星云感）
  if (size > 0.5 || isSelected) {
    const outerR = size * (isSelected ? 12 : isBright ? 7 : 4);
    const outerA = alpha * (isSelected ? 0.12 : 0.05);
    if (outerA > 0.005) {
      const g0 = ctx.createRadialGradient(x, y, 0, x, y, outerR);
      g0.addColorStop(0, color + Math.round(outerA*255).toString(16).padStart(2,'0'));
      g0.addColorStop(1, 'transparent');
      ctx.globalAlpha = 1; ctx.fillStyle = g0;
      ctx.beginPath(); ctx.arc(x, y, outerR, 0, Math.PI*2); ctx.fill();
    }
  }

  // 中层柔光（高斯型）
  const midR = size * (isSelected ? 5 : isBright ? 3.2 : 2.2);
  const midA = alpha * (isSelected ? 0.55 : isBright ? 0.38 : 0.28);
  const gMid = ctx.createRadialGradient(x, y, 0, x, y, midR);
  gMid.addColorStop(0,   '#ffffff' + Math.round(midA * 255).toString(16).padStart(2,'0'));
  gMid.addColorStop(0.45, color + Math.round(midA * 0.4 * 255).toString(16).padStart(2,'0'));
  gMid.addColorStop(1,   'transparent');
  ctx.globalAlpha = 1; ctx.fillStyle = gMid;
  ctx.beginPath(); ctx.arc(x, y, midR, 0, Math.PI*2); ctx.fill();

  // 亮核（小而锐，是视觉焦点）
  const coreR = Math.max(0.5, size * 0.55);
  const coreA = Math.min(alpha * (isSelected ? 1.0 : 0.90), 1);
  const gCore = ctx.createRadialGradient(x, y, 0, x, y, coreR);
  gCore.addColorStop(0, '#ffffff');
  gCore.addColorStop(0.6, isSelected ? color+'ee' : '#eef4ff');
  gCore.addColorStop(1, 'transparent');
  ctx.globalAlpha = coreA; ctx.fillStyle = gCore;
  ctx.beginPath(); ctx.arc(x, y, coreR, 0, Math.PI*2); ctx.fill();

  ctx.restore();
}

// ── 可见节点集合
function getVisibleNodeSet() {
  if (graphFilterMode === 'linked') {
    const s = new Set(); graphEdges.forEach(e=>{s.add(e.a);s.add(e.b);}); return s;
  }
  if (graphFilterMode === 'noted') {
    const s = new Set(); graphNodes.forEach((n,i)=>{if(n.hasNote)s.add(i);}); return s;
  }
  return new Set(graphNodes.map((_,i)=>i));
}

// ── 屏幕坐标命中测试（找最近节点）
function hitTest3D(mx, my) {
  const vis = getVisibleNodeSet();
  let best = -1, bestD = 40;  // 40px 点击容差
  graphNodes.forEach((n, i) => {
    if (!vis.has(i)) return;
    const p = projectPt(n.x3d, n.y3d, n.z3d);
    if (!p) return;
    const d = Math.hypot(p.sx - mx, p.sy - my);
    if (d < bestD) { bestD = d; best = i; }
  });
  return best;
}

// ── 侧面板
function openGraphPanel(nodeIdx) {
  const panel   = document.getElementById('graph-panel');
  const badge   = document.getElementById('gp-day-badge');
  const topic   = document.getElementById('gp-topic');
  const field   = document.getElementById('gp-field');
  const descEl  = document.getElementById('gp-desc');
  const jumpBtn = document.getElementById('gp-jump-btn');
  const sectT   = document.getElementById('gp-section-title');
  const connL   = document.getElementById('gp-connections');
  const hint    = document.getElementById('graph-hint');

  if (nodeIdx < 0) { panel.classList.remove('open'); hint.style.display='block'; return; }

  const n = graphNodes[nodeIdx];
  badge.textContent  = `DAY ${n.n} · MODULE ${String(n.moduleId).padStart(2,'0')}`;
  badge.style.color  = n.color+'99';
  topic.textContent  = n.topic; topic.style.color = n.color;
  field.textContent  = `${n.field}  ·  ${n.moduleTitle}`;
  descEl.textContent = n.desc;
  jumpBtn.style.display = 'inline-flex';
  jumpBtn.style.borderColor = n.color+'66';
  jumpBtn.style.color = n.color;

  const conns = [], seen = new Set();
  graphEdges.forEach(e => {
    if (e.a===nodeIdx && !seen.has(e.b)) { seen.add(e.b); conns.push({ni:e.b,type:e.type}); }
    if (e.b===nodeIdx && !seen.has(e.a)) { seen.add(e.a); conns.push({ni:e.a,type:e.type}); }
  });

  if (conns.length) {
    sectT.style.display = 'block';
    connL.innerHTML = conns.map(c => {
      const cn = graphNodes[c.ni];
      return `<div class="gp-conn-item" onclick="graphFocusNode(${c.ni})">
        <div class="gp-conn-dot" style="background:${cn.color};color:${cn.color}"></div>
        <div class="gp-conn-body">
          <div class="gp-conn-day">DAY ${cn.n}</div>
          <div class="gp-conn-topic">${cn.topic}</div>
          <div class="gp-conn-field">${cn.field}</div>
        </div>
        <div class="gp-conn-type ${c.type}">${c.type==='link'?'链接':'标签'}</div>
      </div>`;
    }).join('');
  } else {
    sectT.style.display='none';
    connL.innerHTML='<div class="gp-empty">暂无关联<br><span style="font-size:9px">可在主视图中用🔗手动添加</span></div>';
  }
  panel.classList.add('open');
  hint.style.display = 'none';
}

function graphJumpSelected() {
  if (graphSelected < 0) return;
  const n = graphNodes[graphSelected]; closeGraph(); jumpToDay(n.n);
}
function graphFocusNode(ni) { graphSelected=ni; openGraphPanel(ni); }

// ── 主入口
function openGraph() {
  const overlay = document.getElementById('graph-overlay');
  overlay.classList.add('open');
  requestAnimationFrame(() => {
    const body = document.querySelector('.graph-body');
    const canvas = document.getElementById('graph-canvas');
    _graphW = body.clientWidth; _graphH = body.clientHeight;
    canvas.width = _graphW; canvas.height = _graphH;

    buildGraphData();
    generateBgStars();
    init3DPositions();
    graphSelected = -1; graphHovered = -1;
    camRotX = 0.25; camRotY = 0.0; camZoom = 1.0; _autoRot = true;

    openGraphPanel(-1);

    const legendEl = document.getElementById('graph-legend');
    legendEl.innerHTML = MODULES.map(m =>
      `<div class="graph-legend-item" onclick="graphFilterModule(${m.id})">
        <div class="graph-legend-dot" style="background:${m.color};color:${m.color}"></div>${m.title}
      </div>`).join('');

    if (graphRenderTimer) cancelAnimationFrame(graphRenderTimer);
    let lastTime = 0;
    function loop(ts) {
      // 节流到约 40fps，兼顾流畅和性能
      if (ts - lastTime > 24) { lastTime = ts; drawGraph(); }
      graphRenderTimer = requestAnimationFrame(loop);
    }
    graphRenderTimer = requestAnimationFrame(loop);

    setupGraphEvents(canvas);
  });
}

function closeGraph() {
  document.getElementById('graph-overlay').classList.remove('open');
  if (graphRenderTimer) { cancelAnimationFrame(graphRenderTimer); graphRenderTimer = null; }
}

function graphFilter(mode) {
  graphFilterMode = mode;
  ['all','linked','noted'].forEach(m =>
    document.getElementById('graph-btn-'+m)?.classList.toggle('active', m===mode));
}

function graphFilterModule(moduleId) {
  graphNodes.forEach((n,i) => { if(n.moduleId===moduleId) graphSelected=i; });
  openGraphPanel(graphSelected);
}

function graphReset() {
  camRotX=0.25; camRotY=0.0; camZoom=1.0; _autoRot=true;
  graphSelected=-1; graphHovered=-1;
  openGraphPanel(-1);
}

// ── 3D 交互事件
function setupGraphEvents(canvas) {
  const fresh = canvas.cloneNode(true);
  canvas.parentNode.replaceChild(fresh, canvas);
  const c = fresh;

  let lastX = 0, lastY = 0, dragDist = 0;

  function onDown(x, y) { _isDragging=true; _autoRot=false; lastX=x; lastY=y; dragDist=0; }
  function onMove(x, y) {
    if (!_isDragging) {
      // 悬停检测（限速）
      const hit = hitTest3D(x, y);
      if (hit !== graphHovered) { graphHovered = hit; c.style.cursor = hit>=0?'pointer':'grab'; }
      return;
    }
    const dx = x - lastX, dy = y - lastY;
    dragDist += Math.hypot(dx, dy);
    camRotY += dx * 0.007;
    camRotX += dy * 0.007;
    camRotX  = Math.max(-1.4, Math.min(1.4, camRotX));  // 防止翻转
    lastX=x; lastY=y;
  }
  function onUp(x, y) {
    _isDragging = false;
    // 短按（移动少）= 点击选择
    if (dragDist < 8) {
      const hit = hitTest3D(x, y);
      if (hit >= 0) {
        graphSelected = (graphSelected === hit) ? -1 : hit;
        openGraphPanel(graphSelected);
      } else {
        graphSelected = -1; openGraphPanel(-1);
      }
    }
    // 停止拖动后延迟恢复自动旋转
    setTimeout(()=>{ if(!_isDragging) _autoRot=true; }, 3000);
  }

  // 鼠标
  c.addEventListener('mousedown', e=>{ e.preventDefault(); onDown(e.clientX-c.getBoundingClientRect().left, e.clientY-c.getBoundingClientRect().top); });
  c.addEventListener('mousemove', e=>{ const r=c.getBoundingClientRect(); onMove(e.clientX-r.left, e.clientY-r.top); });
  c.addEventListener('mouseup',   e=>{ const r=c.getBoundingClientRect(); onUp(e.clientX-r.left, e.clientY-r.top); });
  c.addEventListener('mouseleave',()=>{ _isDragging=false; });

  // 触摸
  c.addEventListener('touchstart', e=>{ e.preventDefault(); const t=e.touches[0]; const r=c.getBoundingClientRect(); onDown(t.clientX-r.left,t.clientY-r.top); },{passive:false});
  c.addEventListener('touchmove',  e=>{ e.preventDefault(); const t=e.touches[0]; const r=c.getBoundingClientRect(); onMove(t.clientX-r.left,t.clientY-r.top); },{passive:false});
  c.addEventListener('touchend',   e=>{ const t=e.changedTouches[0]; const r=c.getBoundingClientRect(); onUp(t.clientX-r.left,t.clientY-r.top); },{passive:false});

  // 滚轮缩放
  c.addEventListener('wheel', e=>{
    e.preventDefault();
    camZoom *= e.deltaY < 0 ? 1.08 : 0.93;
    camZoom = Math.max(0.3, Math.min(4, camZoom));
  },{passive:false});
}


// ════════════════════════════════════════
// ⑤ 月度复盘自动摘要（在复盘日注入）
// ════════════════════════════════════════
const REVIEW_DAYS = [30,60,90,120,150,180,210,240,270,300,330,365];

function injectMonthlySummary() {
  const idx = buildDayIndex();
  REVIEW_DAYS.forEach(reviewDay => {
    const el = document.getElementById('note-editor-' + reviewDay);
    if (!el) return;
    // 计算本月范围
    const monthStart = reviewDay - 29;
    const noteEntries = [];
    for (let d = monthStart; d <= reviewDay; d++) {
      if (memNotes[d] && memNotes[d].text) {
        const info = idx[d] || {};
        noteEntries.push(`Day ${d}·${info.topic || ''}：${memNotes[d].text}`);
      }
    }
    if (!noteEntries.length) return;
    // 找到 note-editor 旁边插入摘要提示
    const area = el.closest('.note-area');
    if (!area) return;
    let summEl = area.querySelector('.monthly-summary');
    if (!summEl) {
      summEl = document.createElement('div');
      summEl.className = 'monthly-summary';
      summEl.style.cssText = `margin-top:8px;padding:8px 10px;border:1px dashed ${
        'var(--accent1)'}44;border-radius:6px;font-size:11px;color:var(--text2);line-height:1.7;`;
      area.appendChild(summEl);
    }
    summEl.innerHTML = `<div style="font-size:10px;color:var(--accent1);font-family:'Cinzel',serif;margin-bottom:4px;letter-spacing:1px">
      ◈ 本月感悟速览（${noteEntries.length} 条）</div>` +
      noteEntries.slice(0, 5).map(e => `<div style="margin-bottom:3px">· ${e.slice(0,60)}${e.length>60?'…':''}</div>`).join('') +
      (noteEntries.length > 5 ? `<div style="color:var(--text3)">…共 ${noteEntries.length} 条</div>` : '');
  });
}

// ════════════════════════════════════════
// ⑥ 明暗主题切换
// ════════════════════════════════════════
function toggleTheme() {
  const body = document.body;
  const btn  = document.querySelector('.theme-btn');
  body.classList.toggle('light');
  const isLight = body.classList.contains('light');
  btn.textContent = isLight ? '🌙' : '☀';
  localStorage.setItem('tongshi_theme', isLight ? 'light' : 'dark');
}

function initTheme() {
  const saved = localStorage.getItem('tongshi_theme');
  if (saved === 'light') {
    document.body.classList.add('light');
    const btn = document.querySelector('.theme-btn');
    if (btn) btn.textContent = '🌙';
  }
}

// ════════════════════════════════════════
// ⑦ 笔记导出（Markdown 文件）
// ════════════════════════════════════════
function exportNotes() {
  const idx     = buildDayIndex();
  const entries = Object.keys(memNotes)
    .filter(k => memNotes[k] && memNotes[k].text)
    .sort((a, b) => a - b);

  if (!entries.length) { alert('还没有任何感悟笔记可以导出'); return; }

  let md = `# 365天通识框架 · 学习感悟\n\n`;
  md += `> 导出时间：${new Date().toLocaleString('zh-CN')}\n`;
  md += `> 共 ${entries.length} 条笔记\n\n---\n\n`;

  let lastModule = '';
  entries.forEach(k => {
    const note = memNotes[k];
    const info = idx[k] || { topic: 'Day ' + k, field: '', moduleTitle: '' };
    if (info.moduleTitle !== lastModule) {
      md += `\n## ${info.moduleTitle}\n\n`;
      lastModule = info.moduleTitle;
    }
    md += `### Day ${k} · ${info.topic}\n`;
    md += `*${info.field} · ${note.date}*\n\n`;
    md += `${note.text}\n\n---\n\n`;
  });

  const blob = new Blob([md], { type: 'text/markdown;charset=utf-8' });
  const url  = URL.createObjectURL(blob);
  const a    = document.createElement('a');
  const now  = new Date();
  const stamp = `${now.getFullYear()}${String(now.getMonth()+1).padStart(2,'0')}${String(now.getDate()).padStart(2,'0')}`;
  a.href     = url;
  a.download = `通识笔记_${stamp}.md`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

// ════════════════════════════════════════
// 初始化所有功能
// ════════════════════════════════════════
initTheme();
initAllLinks();
injectMonthlySummary();

function toggleModule(el) {
  el.classList.toggle('active');
}

function toggleWeek(header) {
  header.parentElement.classList.toggle('open');
}

function expandAll() {
  document.querySelectorAll('.module').forEach(m => m.classList.add('active'));
}

function collapseAll() {
  document.querySelectorAll('.module').forEach(m => m.classList.remove('active'));
  document.querySelectorAll('.week').forEach(w => w.classList.remove('open'));
}

function expandAllWeeks() {
  document.querySelectorAll('.module').forEach(m => m.classList.add('active'));
  document.querySelectorAll('.week').forEach(w => w.classList.add('open'));
}

// ════════════════════════════════════════
// 艾宾浩斯复习提醒
// ════════════════════════════════════════
function initEbbinghaus() {
  const bar      = document.getElementById('ebbinghaus-bar');
  const cards    = document.getElementById('ebb-cards');
  const idx      = buildDayIndex();
  const GAPS     = [1, 7, 30]; // 艾宾浩斯复习间隔（天）
  const LABELS   = ['1天前', '7天前', '30天前'];
  const CLASSES  = ['ebb-label-1', 'ebb-label-7', 'ebb-label-30'];

  const results = [];

  // 对每条已有笔记，检测其保存日期距今是否正好落在复习窗口内（±1天容差）
  Object.keys(memNotes).forEach(k => {
    const note = memNotes[k];
    if (!note || !note.text || !note.date) return;

    // 解析保存日期：格式 "YYYY/M/D HH:mm"
    const parts = note.date.match(/(\d+)\/(\d+)\/(\d+)/);
    if (!parts) return;
    const saved = new Date(parts[1], parts[2] - 1, parts[3]);
    saved.setHours(0, 0, 0, 0);
    const today = new Date(); today.setHours(0, 0, 0, 0);
    const diffDays = Math.round((today - saved) / 86400000);

    GAPS.forEach((gap, i) => {
      if (Math.abs(diffDays - gap) <= 1) {
        results.push({ dayNum: parseInt(k), note, gapIdx: i });
      }
    });
  });

  if (!results.length) {
    bar.classList.add('empty');
    return;
  }

  bar.classList.remove('empty');

  // 按 gap 排序（1天 → 7天 → 30天）
  results.sort((a, b) => a.gapIdx - b.gapIdx);

  cards.innerHTML = results.map(r => {
    const info    = idx[r.dayNum] || { topic: 'Day ' + r.dayNum, field: '' };
    const snippet = r.note.text.slice(0, 60) + (r.note.text.length > 60 ? '…' : '');
    return `
      <div class="ebb-card" onclick="jumpToDay(${r.dayNum})">
        <div class="ebb-card-label ${CLASSES[r.gapIdx]}">
          ↩ 复习提醒 · ${LABELS[r.gapIdx]}
        </div>
        <div class="ebb-card-day">Day ${r.dayNum} · ${info.field}</div>
        <div class="ebb-card-topic">${info.topic}</div>
        <div class="ebb-card-note">${snippet}</div>
      </div>`;
  }).join('');
}

function toggleEbb() {
  document.getElementById('ebbinghaus-bar').classList.toggle('collapsed');
}

// ════════════════════════════════════════
// 随机漫游
// ════════════════════════════════════════
function randomWander() {
  const keys = Object.keys(memNotes).filter(k => memNotes[k] && memNotes[k].text);
  if (!keys.length) {
    alert('还没有任何感悟笔记。先写几天再来随机漫游吧！');
    return;
  }
  const pick = parseInt(keys[Math.floor(Math.random() * keys.length)]);

  // 闪烁动画提示
  const dayEl = document.getElementById('daynum-' + pick)?.closest('.day');
  jumpToDay(pick);
  if (dayEl) {
    setTimeout(() => {
      dayEl.style.transition = 'background 0.3s';
      dayEl.style.background = 'var(--accent1)22';
      setTimeout(() => { dayEl.style.background = ''; }, 800);
    }, 500);
  }
}

const labels = document.getElementById('timeline-labels');
MODULES.forEach(m => {
  const total = 365;
  const width = (m.range[1] - m.range[0] + 1) / total * 100;
  const seg = document.createElement('div');
  seg.className = 'timeline-seg';
  seg.style.cssText = `width:${width}%; background:${m.color};`;
  seg.title = m.title;
  seg.onclick = () => scrollToModule(m.id);
  track.appendChild(seg);

  const left = (m.range[0] - 1) / total * 100;
  const lbl = document.createElement('div');
  lbl.className = 'timeline-label';
  lbl.style.left = (left + width / 2) + '%';
  lbl.textContent = m.id;
  labels.appendChild(lbl);
});
</script>
<!-- 标签关系网迷你弹窗 -->
<div class="tag-graph-popup" id="tag-graph-popup">
  <div class="tgp-header" id="tgp-header">
    <span class="tgp-icon">🕸</span>
    <span class="tgp-title" id="tgp-title">概念网络</span>
    <span class="tgp-count" id="tgp-count"></span>
    <button class="tgp-close" onclick="closeTagGraph()">✕</button>
  </div>
  <canvas id="tag-graph-canvas" width="380" height="260"></canvas>
  <div class="tgp-footer" id="tgp-footer"></div>
</div>

<div id="notes-store" data-notes="{&quot;1&quot;:{&quot;text&quot;:&quot;熵增定律    Q1-物理学/热力学    2026-03-29\n1. 核心逻辑 (The \&quot;Why\&quot;)\n用一句话描述这个概念揭示了世界的什么本质规律？\nEG：在一个封闭系统中，无序度只会自发增加，除非有外部能量输入。\n2. 降维解释 (ELI5)\n如果要把这个概念讲给一个不具备专业背景的人，你会用什么类比？\nEG：不收拾的房间会自动变乱；洗牌只会越洗越乱。\n3. 跨界迁移 (Cross-Domain Bridge)\n这个逻辑如何解释另一个领域的现象？\nEG：公司不进行流程优化就会滑向人浮于事；模型训练是在噪声中强行制造秩序。\n4. 衍生思考/行动建议 (Actionable Insight)\n这个知识点改变了你对某件事的看法吗？你打算如何应用它？\nEG：承认混乱是常态，所以不再为“琐碎的杂事”焦虑，而是要有意识地投入“高质量能量”去对抗它。\n\n熵增定律：宇宙的终极宿命\n第一幕：从一个房间开始\n想象你的房间。\n早上你刚整理完，一切井井有条：书在书架上，衣服叠好，桌面干净。然后你开始生活——住了一周之后，房间自然变乱了。\n现在问你一个问题：你有没有见过一个房间，在没有人打扫的情况下，自己从乱变整齐的？\n没有。从来没有。\n这不是巧合，这是宇宙的一条铁律。\n为什么乱是\&quot;自然\&quot;的？\n假设你把一副扑克牌按顺序排好：A、2、3……K，四种花色全部有序。然后你开始随机洗牌。\n洗一次——乱了。\n再洗——更乱。\n你能洗回原来的顺序吗？理论上可以，但概率极低，低到你洗一辈子也几乎不可能发生。\n原因很简单：有序的排列方式只有极少数，无序的排列方式有天文数字那么多。 随机发生的事，几乎必然落在\&quot;无序\&quot;这一侧。\n这就是熵的本质——\n熵，是一个系统\&quot;混乱程度\&quot;的度量。混乱越高，熵越高。\n热力学第二定律（熵增定律）用一句话说就是：\n在一个封闭的系统里，熵只会增加，永远不会自发减少。\n宇宙不会自己从乱变整齐。能量不会自己从分散变集中。时间只朝一个方向走。\n\n第二幕：熵是时间的方向\n这里有一件很奇怪的事，值得你停下来想一想。\n物理学里几乎所有的方程，时间倒过来也成立。一颗球从空中落下，你把这个过程倒放，从地面弹回手里——这在物理上是完全合法的。引力方程不管时间正反。\n但有一件事，倒放就会显得荒谬——\n一杯热咖啡放在桌上，慢慢变凉。你把这个过程倒放：一杯冷咖啡，自己越来越热，热量从空气中聚集回杯子里。这绝对不会发生。\n为什么？\n因为热量自发地从高温流向低温，是熵在增加。反过来，热量自发从低温流向高温，熵会减少——而熵不会自发减少。\n所以熵增定律，实际上定义了时间的方向。\n我们感知到\&quot;过去\&quot;和\&quot;未来\&quot;的区别，根本原因就在这里。物理学家卡洛·罗韦利说：时间之所以流动，是因为宇宙的熵在增加。如果熵不增加，时间就没有方向，\&quot;昨天\&quot;和\&quot;明天\&quot;将没有区别。\n你现在正在经历\&quot;时间流逝\&quot;这件事，本质上是你在感知宇宙的熵增。\n\n第三幕：宇宙的终局——热寂\n现在把视野放到最大。\n宇宙是一个（近似的）封闭系统。熵增定律对它也适用。\n宇宙诞生于138亿年前的大爆炸。那一刻，宇宙处于一种极度有序、极度低熵的状态——所有的能量高度集中。从那以后，宇宙一直在膨胀，能量一直在扩散，熵一直在增加。\n星星燃烧，是在把核能转化为热和光向外散射——熵在增加。\n生命新陈代谢，是在消耗有序的能量——熵在增加。\n你今天读这篇文章，你的大脑消耗葡萄糖——熵在增加。\n一切活动，无一例外，都在推动宇宙走向同一个终点。\n这个终点叫做\&quot;热寂\&quot;（Heat Death）。\n在热寂状态下：\n宇宙中所有的能量完全均匀分布，没有任何温差\n没有温差就没有能量流动，没有能量流动就没有任何事情发生\n没有星星，没有生命，没有运动，没有时间意义上的\&quot;变化\&quot;\n宇宙进入永恒的、均匀的、死寂的平衡\n这不是爆炸式的终结，而是一种极度安静的消亡——宇宙慢慢\&quot;散\&quot;掉了。\n时间尺度是10的100次方年以后的事。但方向，从大爆炸那一刻起就已注定。\n\n第四幕：那生命算什么？\n学到这里，你可能会有一个很自然的困惑：\n如果熵只能增加，那生命是怎么回事？\n一颗受精卵变成婴儿，婴儿长大成人——这明明是从简单变复杂，从无序变有序，熵在减少。这不是违反了定律吗？\n没有违反。这是整个主题最精彩的地方。\n1944年，物理学家薛定谔在《生命是什么》里给出了答案——\n生命是靠\&quot;吃\&quot;负熵为生的。\n什么意思？\n熵增定律说的是封闭系统。但生命不是封闭系统，生命一直在和外界交换物质和能量。\n植物吸收阳光（高质量、低熵的能量），释放热量（低质量、高熵的能量）。在这个过程里，植物内部的秩序增加了——但代价是，它把更多的熵排放到了外界环境中。\n你吃饭，消化食物，用其中有序的化学能维持你身体的复杂结构。同时你呼出CO₂、散发热量，把熵排放到外面。\n生命从来没有消灭熵，只是把熵转移出去了。 局部的有序，是以周围环境更大的无序为代价换来的。算总账，整个宇宙的熵依然在增加。\n这给了我们一个非常深刻的视角来理解生命的本质：\n生命是宇宙中一种暂时的、局部的、对抗熵增的结构。 它不违反热力学第二定律，它只是在规则允许的范围内，尽可能地延缓自身的瓦解。\n所有的生命活动——进食、繁殖、进化、文明的建立——从物理角度看，都是同一件事：从环境中汲取低熵，维持自身的有序，同时向外输出更多的熵。\n这件事会一直持续，直到太阳熄灭，直到所有的星星熄灭，直到宇宙热寂。\n\n检验时间\n问题一（概念）\n冰箱能把食物从热变冷，这是不是违反了熵增定律？为什么？\n问题二（应用）\n一座城市从小村庄发展成现代都市，变得越来越有序复杂——这是熵在减少吗？\n问题三（思辨）\n如果宇宙最终走向热寂，你觉得这对\&quot;意义\&quot;这个概念意味着什么？\n\nQ1：不是，因为冰箱先是吸收了食物的热气，熵增了，同时又通过发动机把热气排放出去，是一个正向的但是内部会循环的熵增过程 \n评：你抓住了关键——冰箱不是封闭系统，它在向外排热。这个方向完全对。\n但有一个地方需要纠正：\&quot;吸收食物热气，熵增了\&quot;——这里的主语搞混了。食物变冷，是食物自身的熵在减少。冰箱把这部分热量排到了房间里，房间的熵增加，而且增加得更多。所以总账上，熵是净增加的。\n一句话总结你应该说的：冰箱让食物局部降熵，代价是让外部环境熵增更多，符合定律。\n迁：一个公司如果不从外部获取人才和订单（能量），内部流程只会越来越僵化、混乱。\n\nQ2：不是，这只是形式上的排列聚集，而非能量上的\n评：城市的“有序”代价极其高昂。为了维持一座城市的运转，我们燃烧了海量的煤炭、石油（低熵），排放了巨量的二氧化碳和废热（高熵）。城市是宇宙中一个巨大的熵增放大器。所以城市是和生命一样的东西：局部有序，全局加速熵增。\n\nQ3：这个时候还有概念这个词吗\n评：热寂之后没有观察者，没有语言，没有思维，\&quot;意义\&quot;这个词连同说出它的人一起消失了。意义不是宇宙的属性，它只存在于低熵结构（也就是生命）短暂存在的窗口期里。\n这个答案的哲学名字叫反实在论——意义不是被发现的，是被制造的，而制造它的机器（生命）是暂时的。\n\n答疑\n问：植物吸收阳光（高质量、低熵的能量），释放热量（低质量、高熵的能量）\n答：先从\&quot;能量质量\&quot;这个说法开始\n能量有高低质量之分，不是指能量多少，而是指它能不能被用来做事。\n阳光是高质量能量。光子集中、定向、有秩序地从太阳射来，你可以用它驱动化学反应、发电、让植物生长。它是\&quot;可用的\&quot;。\n热量是低质量能量。分子随机乱撞产生的热，分散、无序、方向混乱。你很难再从它身上提取有用的功了。\n一个比喻：同样是100块钱，一张整钞和一堆硬币散在地上——面值一样，但你能用整钞做的事，散币做不到。阳光是整钞，热量是散币。\n回到植物这个例子\n植物吸收一份高质量的阳光能量，用它把CO₂和水组装成葡萄糖——这是在建造有序的化学结构，植物自身的熵降低了。\n但这个过程不是免费的。植物同时向外释放热量，而且释放出去的热量，比它吸收的阳光能量更\&quot;散\&quot;、更无序。\n所以：\n植物内部：熵减少 ✓\n外部环境：熵增加，而且增加更多 ✓\n总账：熵净增加 ✓\n一句话的本质\n阳光的低熵被植物\&quot;消费\&quot;掉，换成了植物体内的有序结构。但消费过程本身产生了更多的无序热量排出去。\n就像你花100块整钞买了一件有用的东西，但找零回来的全是散币，而且散币加起来只有90块。有序的钱变成了东西，但同时损耗掉一部分变成了更无序的形式。\n这个道理对所有生命都成立，对所有机器也成立——没有任何转换过程是不产生\&quot;散币\&quot;的。&quot;,&quot;date&quot;:&quot;2026/3/31 22:28&quot;},&quot;2&quot;:{&quot;text&quot;:&quot;经典力学与决定论    Q1-物理学/哲学    2026-03-31\n1. 核心逻辑 (The \&quot;Why\&quot;)：\n如果世界遵循固定的因果方程（如 F = ma），那么只要掌握所有初始数据，未来就是可以被精确计算的。\n2. 降维解释 (ELI5)：\n宇宙是一台巨大的、在大爆炸时就上好了发条的精密钟表，每一个齿轮的转动都是注定的。\n3. 跨界迁移 (Cross-Domain Bridge)：\n管理学：试图通过模型和数据预测一切，是典型的决定论思维；\n历史学：大趋势（生产力发展）可能是决定的，但英雄人物的偶然选择是混沌的种子。\n4. 衍生思考 (Actionable Insight)：\n接受宏观上的“不可抗力”，但在微观瞬间保持“选择感”。即便自由意志可能是幻觉，这种“主观能动性的体验”也是对抗熵增、维持生命有序的唯一动力。\n\n牛顿力学与决定论：宇宙是一台钟表吗？\n第一幕：一个苹果引发的革命\n1687年之前，人类对\&quot;为什么东西会动\&quot;这个问题的回答是混乱的。\n亚里士多德说：物体有\&quot;天然位置\&quot;，石头落地是因为它想回到自己的位置。行星转动是因为有神在推动。不同的现象有不同的解释，天上一套规则，地上另一套规则。\n然后牛顿出现了，用三条定律和一个公式，把天上和地下统一了。\n牛顿三定律，用最直白的话说：\n第一定律（惯性）：\n东西不会无缘无故改变运动状态。静止的东西会一直静止，运动的东西会一直匀速直线运动——除非有外力。\n你坐车急刹，身体往前冲，就是惯性。你的身体\&quot;想\&quot;保持原来的速度，是刹车的力打断了它。\n第二定律（F=ma）：\n力等于质量乘以加速度。你推一个物体，质量越大越难推动，力越大加速越快。\n这条定律的革命性在于：它是一个方程。 你只要知道一个物体受到多大的力，就能精确计算出它下一秒在哪里，后一秒在哪里，一年后在哪里。\n第三定律（作用力与反作用力）：\n你推墙，墙也在推你。力永远成对出现，方向相反，大小相等。\n万有引力：把天和地缝合在一起\n牛顿还发现，任何两个有质量的物体之间都存在引力，大小和质量成正比，和距离的平方成反比。\n这一条的意义是毁天灭地的——\n苹果落地和月球绕地球转，是同一种力在起作用。地球拉着苹果往下，也拉着月球往下。月球之所以没有掉下来，是因为它同时在横向运动，一直在\&quot;落\&quot;但一直在\&quot;跑\&quot;，就这样绕着圈。\n天上和地下，第一次被同一套方程描述了。\n\n第二幕：宇宙是一台钟表\n牛顿定律一旦成立，一个极其深刻的推论就出现了。\nF=ma 是一个因果方程。给定初始位置和速度，给定所有的力，你就能计算出任何时刻这个物体在哪里、速度是多少。\n这对一个物体成立。对两个物体成立。对太阳系里所有行星成立——事实上，天文学家用牛顿方程预测哈雷彗星的轨道，精确到几十年后它会在哪一天回来，误差极小。\n那么问题来了：如果对所有物体都成立呢？\n1814年，法国数学家拉普拉斯把这个推论说得非常直白——\n假设有一个智能存在，它在某一时刻知道宇宙中每一个粒子的位置和速度，并且掌握所有的力。那么对它来说，宇宙的过去和未来将没有任何不确定性，一切都像眼前一样清晰。\n这个假想的存在后来被称为**\&quot;拉普拉斯妖\&quot;**。\n它描述的世界观叫做决定论：\n宇宙的每一个时刻，都由上一个时刻完全决定。过去决定现在，现在决定未来。整个宇宙的历史，从大爆炸到热寂，在第一秒就已经写好了。\n宇宙是一台钟表。发条在大爆炸时上好，然后一格一格地走，每一格都精确无误，没有任何意外，没有任何\&quot;本来可以不这样\&quot;。\n这套世界观的震撼之处\n牛顿力学成立之后的100年里，这台\&quot;钟表宇宙\&quot;的图景深深影响了西方思想。\n科学家和哲学家们开始认为：原则上，一切都是可以预测的。战争为什么爆发、瘟疫为什么蔓延、一个人为什么做了某个决定——如果你知道足够多的初始条件，全都可以用方程算出来。\n这带来了巨大的知识乐观主义——人类只要足够努力，就能理解一切、预测一切。\n但同时，它也带来了一个让人极度不安的推论。\n\n第三幕：你有自由意志吗？\n如果宇宙是决定论的，那你的大脑也是宇宙的一部分。\n你的大脑由神经元组成，神经元由原子组成，原子遵循牛顿定律。如果拉普拉斯妖存在，它能算出你大脑里每一个粒子在下一秒的状态——也就是说，它能算出你下一秒会想什么、说什么、做什么。\n你今天早上选择吃什么早饭，你此刻决定继续读下去，你未来会爱上谁、选择什么职业、在哪一天死去——\n在决定论的宇宙里，这些全部在大爆炸的那一刻就已经注定了。\n你以为你在\&quot;选择\&quot;，但那个选择本身，也只是粒子按照方程运动的结果。\n自由意志，可能只是一个幻觉。\n这是牛顿力学最深的哲学刺。它不只是一套计算工具，它是一种关于现实本质的主张——宇宙没有真正的偶然，没有真正的自由，只有因果链条的无尽延伸。\n\n第四幕：钟表被打破了\n故事到这里还没结束。因为20世纪发生了两件事，把这台钟表砸碎了。\n第一件：量子力学\n20世纪初，物理学家发现，在极小的尺度上，粒子的行为是根本不可预测的。\n电子在被观测之前，没有确定的位置，只有一团概率云。你无法同时精确知道一个粒子的位置和速度——不是测量工具不够精确，而是自然界本来就不存在这个确定的值。这叫海森堡不确定性原理。\n这直接杀死了拉普拉斯妖。它要求知道每个粒子的精确位置和速度——但这在物理上是不可能的，不是技术上不可能，是逻辑上不可能。\n宇宙的底层，不是决定论的，而是概率性的。\n第二件：混沌理论\n即使不考虑量子力学，决定论也有另一个致命问题。\n1960年代，气象学家洛伦兹发现：某些系统对初始条件极度敏感。一只蝴蝶在巴西扇动翅膀，可能引发德克萨斯州的一场龙卷风。\n这就是蝴蝶效应。\n在混沌系统里，初始条件哪怕有极其微小的误差，预测结果就会在短时间内完全失效。而现实世界中，初始条件的测量永远有误差。\n所以即使宇宙在方程层面是决定论的，在实践层面也是根本不可预测的。\n所以最终的图景是这样的：\n牛顿建造了一台完美的钟表，运行了200年。\n量子力学告诉我们，钟表的齿轮其实是随机跳动的。\n混沌理论告诉我们，就算齿轮是确定的，我们也永远算不准。\n决定论作为一种绝对真理倒下了。但它留下的问题——自由意志是否存在——至今没有答案，因为这已经不是物理学问题，而是哲学问题了。\n\n检验时间\n问题一（概念）\n用你自己的比喻，解释一下什么是惯性。不要用课本的说法。\n问题二（应用）\n天气预报为什么永远不能做到100%准确？用今天学的内容解释。\n问题三（思辨）\n量子力学证明了宇宙底层是随机的，所以自由意志存在——你同意这个说法吗？\n\nQ1：惯性是受到外力影响的条件下，立时反应出的不符合外力作用但符合本来该物体前进方向的一种现象\n评：你说的\&quot;立时反应\&quot;暗示惯性是一种主动的、瞬间的响应——但惯性其实更像是一种被动的、持续的抵抗。更准确的图景是：物体根本不\&quot;想\&quot;做任何事，它只是懒得改变。外力来之前它怎样，它就想继续怎样。外力是打断这种\&quot;懒\&quot;的东西。惯性的本质是物体对改变的抵抗，是一种“质量带来的固执”，而不是一种反应。\n迁：这在组织管理（HR）中非常常见：一个成熟的部门（质量大）即便面临市场改革（外力），也会由于惯性保持原有的运作习惯（前进方向）。这就是变革阻力的由来。\n\nQ2：因为天气是由空气中的水分含量决定的，而依据混沌理论，只要其中某个水分子的位置发生了某些微小的变动，原本的天气轨迹就有可能被打乱，从而出现预报不准确的情况\n评：你所说的正是混沌理论的精髓——对初始条件的极度敏感。但天气不准还有第二层原因，就是我们的测量本身有误差。混沌系统里，测量误差再小，经过足够多的迭代计算，最终结果也会完全偏离。所以是双重不可预测：系统本身敏感，测量本身也有限。\n\nQ3：这只是证明了宇宙底层具有一定的随机性，但牛顿力学证明的庞大的逻辑框架我觉得是具有合理性的，所以我并不觉得自由意志是完全存在的，换个说法，我觉得历史轨道上不存在自由意志，而某些个体存在。我认为集体的走向是被决定的，个体在某些瞬间存在选择空间，普通人在日常微小瞬间里的选择——历史不在乎，但本人真实感受到了自由\n评：宏观决定论：你认为历史轨迹有其必然性。这就像是物理学中的 F = ma，大环境的力决定了群体的加速度。微观选择感：你强调了“本人真实感受到自由”的重要性。这非常有力量——即便宇宙是一台钟表，我们在齿轮缝隙里产生的那一点点“想要往左还是往右”的念头，就是生命对抗冷冰冰方程的唯一证据。\n你实际上在说：自由意志不需要改变历史才算数，它只需要被感受到。\n这在哲学里有一个名字，叫相容论——决定论和自由意志不是非此即彼的，它们可以同时为真。宇宙的因果链条是真实的，但人在那个链条里感受到的选择感，也是真实的，而且那个感受本身就是自由意志的全部含义。\n但我要给你一个真正的追问：\n你说\&quot;本人真实感受到了自由\&quot;——\n如果这个\&quot;感受\&quot;本身，也是大脑神经元按照物理规律放电的结果呢？\n也就是说：你感受到自由，但这个感受是被决定的。一个被决定的\&quot;自由感\&quot;，还算自由吗？&quot;,&quot;date&quot;:&quot;2026/3/31 22:22&quot;}}" style="display:none"></div>
<!-- ══════════════════════════════════════ -->
<!-- 🎵 背景音乐播放器                      -->
<!-- ══════════════════════════════════════ -->
<audio id="bg-audio" loop preload="none" src="bg-music.mp3"></audio>


<style>
  #music-player {
    position: fixed;
    bottom: 24px;
    right: 24px;
    z-index: 9999;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 8px;
    pointer-events: auto;
  }
  #music-panel {
    background: var(--surface2, #181c24);
    border: 1px solid var(--border, #252a35);
    border-radius: 14px;
    padding: 12px 14px;
    display: flex;
    align-items: center;
    gap: 10px;
    opacity: 0;
    transform: translateY(8px) scale(0.95);
    pointer-events: none;
    transition: opacity 0.2s ease, transform 0.2s ease;
    box-shadow: 0 4px 24px rgba(0,0,0,0.4);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    min-width: 160px;
  }
  #music-panel.open {
    opacity: 1;
    transform: translateY(0) scale(1);
    pointer-events: auto;
  }
  #music-vol-icon {
    font-size: 14px;
    flex-shrink: 0;
    opacity: 0.7;
  }
  #music-volume {
    -webkit-appearance: none;
    appearance: none;
    width: 100px;
    height: 4px;
    border-radius: 2px;
    outline: none;
    cursor: pointer;
    flex: 1;
    background: linear-gradient(
      to right,
      var(--accent1, #c8975a) 0%,
      var(--accent1, #c8975a) var(--vol-pct, 30%),
      var(--border, #252a35) var(--vol-pct, 30%),
      var(--border, #252a35) 100%
    );
  }
  #music-volume::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 14px; height: 14px;
    border-radius: 50%;
    background: var(--accent1, #c8975a);
    cursor: pointer;
    transition: transform 0.15s;
    box-shadow: 0 1px 4px rgba(0,0,0,0.3);
  }
  #music-volume::-webkit-slider-thumb:hover { transform: scale(1.2); }
  #music-volume::-moz-range-thumb {
    width: 14px; height: 14px;
    border-radius: 50%;
    background: var(--accent1, #c8975a);
    border: none;
    cursor: pointer;
  }
  #music-toggle {
    width: 42px; height: 42px;
    border-radius: 50%;
    border: 1px solid var(--border, #252a35);
    background: var(--surface2, #181c24);
    color: var(--text2, #9a9080);
    font-size: 16px;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.2s;
    box-shadow: 0 2px 12px rgba(0,0,0,0.35);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    flex-shrink: 0;
    position: relative;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
  }
  #music-toggle:hover {
    border-color: var(--accent1, #c8975a);
    color: var(--accent1, #c8975a);
    transform: scale(1.06);
  }
  #music-toggle.playing {
    border-color: var(--accent1, #c8975a);
    color: var(--accent1, #c8975a);
    box-shadow: 0 0 0 1px var(--accent1, #c8975a)44, 0 2px 16px rgba(0,0,0,0.4);
  }
  #music-toggle.playing::after {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    border: 1px solid var(--accent1, #c8975a);
    opacity: 0;
    animation: music-pulse 2.4s ease-out infinite;
  }
  @keyframes music-pulse {
    0%   { transform: scale(1);    opacity: 0.5; }
    100% { transform: scale(1.45); opacity: 0; }
  }
  body.light #music-toggle,
  body.light #music-panel {
    background: var(--surface2, #e4dfd4);
    border-color: var(--border, #d0c9bc);
    box-shadow: 0 2px 12px rgba(0,0,0,0.12);
  }
  @media (max-width: 480px) {
    #music-player { bottom: 16px; right: 16px; }
    #music-toggle { width: 38px; height: 38px; font-size: 14px; }
    #music-volume { width: 80px; }
  }
  body.overlay-open #music-player {
    opacity: 0.4;
    transition: opacity 0.3s;
  }
  body.overlay-open #music-player:hover,
  body.overlay-open #music-player:focus-within {
    opacity: 1;
  }
</style>

<div id="music-player">
  <div id="music-panel">
    <span id="music-vol-icon">🔈</span>
    <input type="range" id="music-volume" min="0" max="100" value="30" title="调节音量" aria-label="背景音乐音量" style="--vol-pct: 30%;">
  </div>
  <button id="music-toggle" title="播放背景音乐" aria-label="背景音乐开关" onclick="toggleMusic()">
    ♪
  </button>
</div>

<script>
(function() {
  var audio     = document.getElementById('bg-audio');
  var btn       = document.getElementById('music-toggle');
  var panel     = document.getElementById('music-panel');
  var volSlider = document.getElementById('music-volume');
  var volIcon   = document.getElementById('music-vol-icon');

  var isPlaying = false;
  var panelOpen = false;
  var hideTimer = null;

  audio.volume = 0.30;
  setSliderFill(30);

  window.toggleMusic = function() {
    if (isPlaying) {
      audio.pause();
      isPlaying = false;
      btn.innerHTML = '♪';
      btn.classList.remove('playing');
      btn.title = '播放背景音乐';
    } else {
      var p = audio.play();
      if (p !== undefined) {
        p.then(function() {
          isPlaying = true;
          btn.innerHTML = '&#10074;&#10074;';
          btn.classList.add('playing');
          btn.title = '暂停背景音乐';
        }).catch(function(err) {
          console.warn('Audio play failed:', err);
        });
      } else {
        isPlaying = true;
        btn.innerHTML = '&#10074;&#10074;';
        btn.classList.add('playing');
        btn.title = '暂停背景音乐';
      }
    }
    showPanel();
  };

  function showPanel() {
    panel.classList.add('open');
    panelOpen = true;
    resetHideTimer();
  }
  function hidePanel() {
    panel.classList.remove('open');
    panelOpen = false;
  }
  function resetHideTimer() {
    clearTimeout(hideTimer);
    hideTimer = setTimeout(hidePanel, 3000);
  }

  btn.addEventListener('contextmenu', function(e) {
    e.preventDefault();
    if (panelOpen) hidePanel(); else showPanel();
  });
  panel.addEventListener('mouseenter', function() { clearTimeout(hideTimer); });
  panel.addEventListener('mouseleave', resetHideTimer);
  panel.addEventListener('touchstart', function() { clearTimeout(hideTimer); }, {passive:true});

  volSlider.addEventListener('input', function() {
    var v = parseInt(this.value);
    audio.volume = v / 100;
    setSliderFill(v);
    if (v === 0)     volIcon.textContent = '🔇';
    else if (v < 40) volIcon.textContent = '🔈';
    else if (v < 70) volIcon.textContent = '🔉';
    else             volIcon.textContent = '🔊';
    resetHideTimer();
  });

  function setSliderFill(v) {
    volSlider.style.setProperty('--vol-pct', v + '%');
  }

  /* overlay 状态检测 */
  if (window.MutationObserver) {
    var observer = new MutationObserver(function() {
      var anyOpen = !!(
        document.querySelector('#journal-overlay.open') ||
        document.querySelector('.tag-graph-popup.open')
      );
      document.body.classList.toggle('overlay-open', anyOpen);
    });
    observer.observe(document.body, {
      subtree: true, attributes: true, attributeFilter: ['class']
    });
  }

  /* iOS Safari 预加载 */
  document.addEventListener('touchend', function onFirstTouch() {
    audio.load();
    document.removeEventListener('touchend', onFirstTouch);
  }, {once: true});

})();
</script>


</body></html>
