
**<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ProjectSiam</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600;700&family=Space+Grotesk:wght@400;600;700&display=swap');

  :root {
    --bg: #0d0f14;
    --surface: #161a22;
    --card: #1e2330;
    --border: #2a3040;
    --accent: #4f8ef7;
    --accent2: #a78bfa;
    --green: #34d399;
    --orange: #fb923c;
    --text: #e8ecf4;
    --muted: #7a8599;
    --radius: 14px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Sarabun', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
  }

  /* Header */
  header {
    background: linear-gradient(135deg, #0d0f14 0%, #161a22 100%);
    border-bottom: 1px solid var(--border);
    padding: 0 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 62px;
    position: sticky; top: 0; z-index: 100;
  }
  .logo {
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 700;
    font-size: 18px;
    letter-spacing: -0.5px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .header-btns { display: flex; gap: 10px; }
  .btn {
    padding: 8px 18px;
    border-radius: 8px;
    border: none;
    font-family: 'Sarabun', sans-serif;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all .18s;
  }
  .btn-outline {
    background: transparent;
    color: var(--accent);
    border: 1.5px solid var(--accent);
  }
  .btn-outline:hover { background: rgba(79,142,247,.1); }
  .btn-primary {
    background: linear-gradient(135deg, var(--accent), #6366f1);
    color: #fff;
  }
  .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 4px 18px rgba(79,142,247,.35); }

  /* Tabs */
  .tabs {
    display: flex;
    gap: 4px;
    padding: 16px 24px 0;
    border-bottom: 1px solid var(--border);
  }
  .tab {
    padding: 10px 20px;
    border-radius: 8px 8px 0 0;
    border: 1px solid transparent;
    border-bottom: none;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    color: var(--muted);
    background: transparent;
    transition: all .15s;
    font-family: 'Sarabun', sans-serif;
  }
  .tab.active {
    background: var(--surface);
    color: var(--text);
    border-color: var(--border);
  }
  .tab:not(.active):hover { color: var(--text); }

  /* Layout */
  .main { max-width: 1100px; margin: 0 auto; padding: 28px 24px; }

  /* Panel */
  .panel { display: none; }
  .panel.active { display: block; }

  /* Form Card */
  .form-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 28px;
    margin-bottom: 20px;
  }
  .form-title {
    font-size: 18px;
    font-weight: 700;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .form-title .icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
  }
  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 6px; }
  .form-group.full { grid-column: 1 / -1; }
  label { font-size: 13px; color: var(--muted); font-weight: 600; letter-spacing: .3px; }
  input, textarea, select {
    background: var(--card);
    border: 1.5px solid var(--border);
    border-radius: 8px;
    color: var(--text);
    font-family: 'Sarabun', sans-serif;
    font-size: 14px;
    padding: 10px 14px;
    transition: border-color .15s;
    width: 100%;
  }
  input:focus, textarea:focus, select:focus {
    outline: none;
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(79,142,247,.15);
  }
  textarea { resize: vertical; min-height: 90px; }
  select option { background: var(--card); }

  /* Tag input */
  .tag-wrap {
    display: flex; flex-wrap: wrap; gap: 6px;
    background: var(--card);
    border: 1.5px solid var(--border);
    border-radius: 8px;
    padding: 8px 10px;
    min-height: 44px;
    align-items: center;
    cursor: text;
    transition: border-color .15s;
  }
  .tag-wrap:focus-within { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(79,142,247,.15); }
  .tag {
    background: rgba(79,142,247,.15);
    color: var(--accent);
    border-radius: 6px;
    padding: 3px 10px;
    font-size: 12px;
    font-weight: 600;
    display: flex; align-items: center; gap: 5px;
  }
  .tag .remove { cursor: pointer; opacity: .7; font-size: 14px; line-height: 1; }
  .tag .remove:hover { opacity: 1; }
  .tag-input {
    background: transparent; border: none; outline: none;
    color: var(--text); font-size: 14px; font-family: 'Sarabun', sans-serif;
    min-width: 120px; flex: 1;
    padding: 2px 4px;
  }

  /* Member list */
  .member-list { display: flex; flex-direction: column; gap: 8px; margin-top: 8px; }
  .member-item {
    display: flex; align-items: center; gap: 10px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 14px;
  }
  .member-avatar {
    width: 32px; height: 32px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; font-weight: 700; color: #fff;
    flex-shrink: 0;
  }
  .member-name { flex: 1; font-weight: 600; }
  .member-role { font-size: 12px; color: var(--muted); }
  .member-del { color: var(--muted); cursor: pointer; font-size: 18px; line-height: 1; }
  .member-del:hover { color: #f87171; }
  .add-member-row { display: flex; gap: 8px; }
  .add-member-row input { flex: 1; }

  /* Progress bar */
  .progress-wrap { display: flex; flex-direction: column; gap: 6px; }
  .progress-label { display: flex; justify-content: space-between; font-size: 13px; }
  .progress-bar { background: var(--card); border-radius: 100px; height: 6px; overflow: hidden; }
  .progress-fill { height: 100%; border-radius: 100px; background: linear-gradient(90deg, var(--accent), var(--accent2)); transition: width .3s; }

  /* Submit row */
  .submit-row { display: flex; justify-content: flex-end; gap: 10px; margin-top: 20px; }

  /* Projects grid */
  .projects-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 18px; }
  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
    transition: transform .2s, box-shadow .2s;
    cursor: pointer;
  }
  .project-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 40px rgba(0,0,0,.4);
    border-color: rgba(79,142,247,.4);
  }
  .card-banner {
    height: 6px;
  }
  .card-body { padding: 18px; }
  .card-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; }
  .card-title { font-size: 16px; font-weight: 700; line-height: 1.4; }
  .badge {
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 11px;
    font-weight: 700;
    white-space: nowrap;
    flex-shrink: 0;
  }
  .badge-blue { background: rgba(79,142,247,.15); color: var(--accent); }
  .badge-green { background: rgba(52,211,153,.15); color: var(--green); }
  .badge-orange { background: rgba(251,146,60,.15); color: var(--orange); }
  .badge-purple { background: rgba(167,139,250,.15); color: var(--accent2); }
  .card-desc { font-size: 13px; color: var(--muted); line-height: 1.6; margin-bottom: 14px; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
  .card-tags { display: flex; flex-wrap: wrap; gap: 5px; margin-bottom: 14px; }
  .card-tag { font-size: 11px; color: var(--muted); background: var(--card); padding: 2px 8px; border-radius: 4px; }
  .card-footer { display: flex; justify-content: space-between; align-items: center; padding-top: 12px; border-top: 1px solid var(--border); }
  .card-members { display: flex; }
  .card-member-av {
    width: 24px; height: 24px;
    border-radius: 50%;
    border: 2px solid var(--surface);
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-size: 10px; font-weight: 700; color: #fff;
    margin-left: -6px;
  }
  .card-member-av:first-child { margin-left: 0; }
  .card-date { font-size: 11px; color: var(--muted); }
  .card-progress { margin-bottom: 14px; }
  .card-prog-bar { background: var(--card); border-radius: 100px; height: 4px; overflow: hidden; }
  .card-prog-fill { height: 100%; border-radius: 100px; }

  /* Empty state */
  .empty {
    text-align: center;
    padding: 60px 20px;
    color: var(--muted);
  }
  .empty-icon { font-size: 52px; margin-bottom: 16px; opacity: .5; }
  .empty-text { font-size: 16px; }

  /* Filters */
  .filters { display: flex; gap: 10px; margin-bottom: 20px; flex-wrap: wrap; align-items: center; }
  .filter-search {
    flex: 1; min-width: 200px;
    background: var(--surface);
    border: 1.5px solid var(--border);
    border-radius: 8px;
    color: var(--text);
    font-family: 'Sarabun', sans-serif;
    font-size: 14px;
    padding: 9px 14px;
  }
  .filter-search:focus { outline: none; border-color: var(--accent); }
  .filter-select {
    background: var(--surface);
    border: 1.5px solid var(--border);
    border-radius: 8px;
    color: var(--text);
    font-family: 'Sarabun', sans-serif;
    font-size: 13px;
    padding: 9px 14px;
    cursor: pointer;
  }
  .filter-select:focus { outline: none; border-color: var(--accent); }

  /* Modal */
  .modal-overlay {
    position: fixed; inset: 0;
    background: rgba(0,0,0,.7);
    backdrop-filter: blur(4px);
    z-index: 200;
    display: none;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    width: 100%;
    max-width: 680px;
    max-height: 88vh;
    overflow-y: auto;
    animation: slideUp .2s ease;
  }
  @keyframes slideUp {
    from { transform: translateY(20px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }
  .modal-header {
    padding: 20px 24px;
    border-bottom: 1px solid var(--border);
    display: flex; justify-content: space-between; align-items: center;
    position: sticky; top: 0; background: var(--surface); z-index: 1;
  }
  .modal-close {
    width: 32px; height: 32px;
    border-radius: 8px;
    background: var(--card);
    border: none; cursor: pointer;
    color: var(--muted); font-size: 18px;
    display: flex; align-items: center; justify-content: center;
    transition: all .15s;
  }
  .modal-close:hover { background: #f87171; color: #fff; }
  .modal-body { padding: 24px; }
  .modal-banner {
    height: 8px;
    border-radius: var(--radius) var(--radius) 0 0;
  }
  .detail-section { margin-bottom: 24px; }
  .detail-label { font-size: 12px; color: var(--muted); font-weight: 700; letter-spacing: .8px; text-transform: uppercase; margin-bottom: 8px; }
  .detail-value { font-size: 15px; line-height: 1.7; }
  .detail-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .detail-members { display: flex; flex-direction: column; gap: 8px; }
  .detail-member {
    display: flex; align-items: center; gap: 10px;
    background: var(--card);
    border-radius: 8px;
    padding: 10px 14px;
  }
  .ai-section {
    background: var(--card);
    border: 1px solid rgba(79,142,247,.25);
    border-radius: 10px;
    padding: 16px;
    margin-top: 16px;
  }
  .ai-label {
    font-size: 12px;
    color: var(--accent);
    font-weight: 700;
    letter-spacing: .5px;
    margin-bottom: 10px;
    display: flex; align-items: center; gap: 6px;
  }
  .ai-text { font-size: 14px; line-height: 1.7; color: var(--text); }
  .ai-loading { color: var(--muted); font-size: 13px; }
  .spinner { display: inline-block; width: 16px; height: 16px; border: 2px solid var(--border); border-top-color: var(--accent); border-radius: 50%; animation: spin .7s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }

  /* Toast */
  .toast {
    position: fixed; bottom: 24px; right: 24px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 12px 18px;
    font-size: 14px;
    display: flex; align-items: center; gap: 10px;
    z-index: 999;
    transform: translateY(80px); opacity: 0;
    transition: all .3s;
    max-width: 300px;
  }
  .toast.show { transform: translateY(0); opacity: 1; }
  .toast.success { border-color: rgba(52,211,153,.4); }
  .toast.success .toast-icon { color: var(--green); }

  /* Stats */
  .stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-bottom: 24px; }
  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 18px;
  }
  .stat-num { font-size: 28px; font-weight: 700; font-family: 'Space Grotesk', sans-serif; }
  .stat-lbl { font-size: 12px; color: var(--muted); margin-top: 4px; }

  /* Image Upload */
  .img-upload-area {
    border: 2px dashed var(--border);
    border-radius: 10px;
    padding: 24px;
    text-align: center;
    cursor: pointer;
    transition: all .2s;
    background: var(--card);
    position: relative;
  }
  .img-upload-area:hover { border-color: var(--accent); background: rgba(79,142,247,.05); }
  .img-upload-area input[type=file] { position: absolute; inset: 0; opacity: 0; cursor: pointer; width: 100%; height: 100%; }
  .img-upload-icon { font-size: 32px; margin-bottom: 8px; }
  .img-upload-text { font-size: 13px; color: var(--muted); }
  .img-preview-grid { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 12px; }
  .img-thumb {
    position: relative;
    width: 90px; height: 90px;
    border-radius: 8px;
    overflow: hidden;
    border: 1.5px solid var(--border);
  }
  .img-thumb img { width: 100%; height: 100%; object-fit: cover; display: block; }
  .img-thumb .img-del {
    position: absolute; top: 3px; right: 3px;
    width: 20px; height: 20px;
    background: rgba(0,0,0,.7);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    color: #fff; font-size: 12px; cursor: pointer; line-height: 1;
  }
  .img-thumb .img-del:hover { background: #ef4444; }
  .modal-images { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 8px; }
  .modal-img {
    width: 120px; height: 90px;
    border-radius: 8px;
    object-fit: cover;
    border: 1.5px solid var(--border);
    cursor: pointer;
    transition: transform .15s;
  }
  .modal-img:hover { transform: scale(1.04); }
  .lightbox {
    position: fixed; inset: 0;
    background: rgba(0,0,0,.92);
    z-index: 500;
    display: none;
    align-items: center;
    justify-content: center;
  }
  .lightbox.open { display: flex; }
  .lightbox img { max-width: 90vw; max-height: 88vh; border-radius: 10px; }
  .lightbox-close {
    position: absolute; top: 20px; right: 24px;
    color: #fff; font-size: 32px; cursor: pointer; line-height: 1;
    background: rgba(255,255,255,.1); width: 40px; height: 40px;
    border-radius: 50%; display: flex; align-items: center; justify-content: center;
  }

  /* Responsive */
  @media (max-width: 680px) {
    .form-grid { grid-template-columns: 1fr; }
    .detail-grid { grid-template-columns: 1fr; }
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
    .projects-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">🎓 ProjectSiam</div>
  <div class="header-btns">
    <button class="btn btn-primary" onclick="switchTab('add')">+ เพิ่มโครงงาน</button>
  </div>
</header>

<div class="tabs">
  <button class="tab active" onclick="switchTab('browse')" id="tab-browse">📂 โครงงานทั้งหมด</button>
  <button class="tab" onclick="switchTab('add')" id="tab-add">➕ เพิ่มโครงงาน</button>
</div>

<div class="main">

  <!-- Browse Panel -->
  <div class="panel active" id="panel-browse">
    <div class="stats-grid" id="stats-grid">
      <div class="stat-card"><div class="stat-num" id="stat-total">0</div><div class="stat-lbl">โครงงานทั้งหมด</div></div>
      <div class="stat-card"><div class="stat-num" id="stat-prog">0</div><div class="stat-lbl">กำลังดำเนินการ</div></div>
      <div class="stat-card"><div class="stat-num" id="stat-done">0</div><div class="stat-lbl">เสร็จสมบูรณ์</div></div>
      <div class="stat-card"><div class="stat-num" id="stat-members">0</div><div class="stat-lbl">สมาชิกรวม</div></div>
    </div>
    <div class="filters">
      <input type="text" class="filter-search" placeholder="🔍 ค้นหาโครงงาน..." id="searchBox" oninput="renderProjects()">
      <select class="filter-select" id="filterStatus" onchange="renderProjects()">
        <option value="">สถานะทั้งหมด</option>
        <option value="กำลังดำเนินการ">กำลังดำเนินการ</option>
        <option value="เสร็จสมบูรณ์">เสร็จสมบูรณ์</option>
        <option value="รอดำเนินการ">รอดำเนินการ</option>
        <option value="หยุดชั่วคราว">หยุดชั่วคราว</option>
      </select>
      <select class="filter-select" id="filterType" onchange="renderProjects()">
        <option value="">ประเภททั้งหมด</option>
        <option value="โรงเเรม">โรงเเรม</option>
        <option value="เทคโนโลยี">เทคโนโลยี</option>
        <option value="บัญชี">บัญชี</option>
        <option value="ตลาด">ตลาด</option>
        <option value="อื่นๆ">อื่นๆ</option>
      </select>
    </div>
    <div class="projects-grid" id="projects-grid"></div>
  </div>

  <!-- Add Panel -->
  <div class="panel" id="panel-add">
    <div class="form-card">
      <div class="form-title"><div class="icon">📋</div> ข้อมูลโครงงาน</div>
      <div class="form-grid">
        <div class="form-group full">
          <label>ชื่อโครงงาน *</label>
          <input type="text" id="f-title" placeholder="ระบุชื่อโครงงาน..." />
        </div>
        <div class="form-group">
          <label>ประเภทโครงงาน</label>
          <select id="f-type">
            <option value="โรงเเรม">โรงเเรม</option>
        <option value="เทคโนโลยี">เทคโนโลยี</option>
        <option value="บัญชี">บัญชี</option>
        <option value="ตลาด">ตลาด</option>
        <option value="อื่นๆ">อื่นๆ</option>
          </select>
        </div>
        <div class="form-group">
          <label>สถานะ</label>
          <select id="f-status">
            <option value="รอดำเนินการ">รอดำเนินการ</option>
            <option value="กำลังดำเนินการ">กำลังดำเนินการ</option>
            <option value="เสร็จสมบูรณ์">เสร็จสมบูรณ์</option>
            <option value="หยุดชั่วคราว">หยุดชั่วคราว</option>
          </select>
        </div>
        <div class="form-group full">
          <label>คำอธิบายโครงงาน *</label>
          <textarea id="f-desc" placeholder="อธิบายวัตถุประสงค์ วิธีการ และผลลัพธ์ที่คาดหวัง..."></textarea>
        </div>
        <div class="form-group">
          <label>วันที่เริ่มต้น</label>
          <input type="date" id="f-start" />
        </div>
        <div class="form-group">
          <label>วันที่สิ้นสุด</label>
          <input type="date" id="f-end" />
        </div>
        <div class="form-group full">
          <label>ความคืบหน้า (%)</label>
          <div class="progress-wrap">
            <div class="progress-label"><span>0%</span><span id="prog-pct">0%</span></div>
            <input type="range" id="f-progress" min="0" max="100" value="0" oninput="document.getElementById('prog-pct').textContent=this.value+'%'" style="width:100%;accent-color:var(--accent)">
          </div>
        </div>
        <div class="form-group full">
          <label>แท็ก (กด Enter เพื่อเพิ่ม)</label>
          <div class="tag-wrap" id="tag-wrap" onclick="document.getElementById('tag-input').focus()">
            <input type="text" class="tag-input" id="tag-input" placeholder="เพิ่มแท็ก..." onkeydown="handleTag(event)" />
          </div>
        </div>
        <div class="form-group full">
          <label>ลิงก์ / URL (รายงาน, GitHub, ฯลฯ)</label>
          <input type="url" id="f-url" placeholder="https://..." />
        </div>
      </div>
    </div>

    <div class="form-card">
      <div class="form-title"><div class="icon">🖼️</div> รูปภาพโครงงาน</div>
      <div class="img-upload-area" id="upload-area">
        <input type="file" id="f-images" accept="image/*" multiple onchange="handleImages(event)" />
        <div class="img-upload-icon">📁</div>
        <div class="img-upload-text">คลิกหรือลากรูปภาพมาวางที่นี่<br><small>รองรับ JPG, PNG, GIF (สูงสุด 5 รูป)</small></div>
      </div>
      <div class="img-preview-grid" id="img-preview-grid"></div>
    </div>

    <div class="form-card">
      <div class="form-title"><div class="icon">👥</div> สมาชิกในทีม</div>
      <div class="member-list" id="member-list"></div>
      <div class="add-member-row" style="margin-top:12px">
        <input type="text" id="m-name" placeholder="ชื่อสมาชิก" />
        <input type="text" id="m-role" placeholder="บทบาท (เช่น หัวหน้า)" style="max-width:180px" />
        <button class="btn btn-outline" onclick="addMember()">+ เพิ่ม</button>
      </div>
    </div>

    <div class="submit-row">
      <button class="btn btn-outline" onclick="clearForm()">ล้างข้อมูล</button>
      <button class="btn btn-primary" onclick="saveProject()">💾 บันทึกโครงงาน</button>
    </div>
  </div>

</div>

<!-- Modal -->
<div class="modal-overlay" id="modal-overlay" onclick="closeModal(event)">
  <div class="modal" id="modal">
    <div class="modal-banner" id="modal-banner"></div>
    <div class="modal-header">
      <div>
        <div style="font-size:18px;font-weight:700" id="modal-title"></div>
        <div style="font-size:13px;color:var(--muted);margin-top:3px" id="modal-subtitle"></div>
      </div>
      <button class="modal-close" onclick="document.getElementById('modal-overlay').classList.remove('open')">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<!-- Toast -->
<div class="toast" id="toast">
  <span class="toast-icon">✅</span>
  <span id="toast-msg"></span>
</div>

<!-- Lightbox -->
<div class="lightbox" id="lightbox" onclick="document.getElementById('lightbox').classList.remove('open')">
  <div class="lightbox-close">✕</div>
  <img id="lightbox-img" src="" alt="" />
</div>

<script>
// ===================== STATE =====================
let projects = JSON.parse(localStorage.getItem('ph_projects') || '[]');
let tags = [];
let members = [];
let images = []; // base64 array
let editId = null;

// ===================== COLORS =====================
const typeColors = {
  'เทคโนโลยี': ['#4f8ef7','#6366f1'],
  '......': ['#34d399','#059669'],
  '......': ['#fb923c','#ef4444'],
  '.......': ['#a78bfa','#7c3aed'],
  '.......': ['#f472b6','#ec4899'],
  'อื่นๆ': ['#94a3b8','#64748b'],
};
const statusBadge = {
  'กำลังดำเนินการ': 'badge-blue',
  'เสร็จสมบูรณ์': 'badge-green',
  'รอดำเนินการ': 'badge-orange',
  'หยุดชั่วคราว': 'badge-purple',
};

// ===================== TABS =====================
function switchTab(tab) {
  ['browse','add'].forEach(t => {
    document.getElementById('tab-'+t).classList.toggle('active', t===tab);
    document.getElementById('panel-'+t).classList.toggle('active', t===tab);
  });
}

// ===================== TAG INPUT =====================
function handleTag(e) {
  if (e.key === 'Enter' || e.key === ',') {
    e.preventDefault();
    const val = e.target.value.trim().replace(/,$/, '');
    if (val && !tags.includes(val)) {
      tags.push(val);
      renderTagUI();
    }
    e.target.value = '';
  }
}
function removeTag(i) {
  tags.splice(i, 1);
  renderTagUI();
}
function renderTagUI() {
  const wrap = document.getElementById('tag-wrap');
  const inp = document.getElementById('tag-input');
  wrap.innerHTML = '';
  tags.forEach((t, i) => {
    const span = document.createElement('span');
    span.className = 'tag';
    span.innerHTML = `${t}<span class="remove" onclick="removeTag(${i})">×</span>`;
    wrap.appendChild(span);
  });
  wrap.appendChild(inp);
}

// ===================== MEMBERS =====================
function addMember() {
  const n = document.getElementById('m-name').value.trim();
  const r = document.getElementById('m-role').value.trim();
  if (!n) return;
  members.push({ name: n, role: r || 'สมาชิก' });
  document.getElementById('m-name').value = '';
  document.getElementById('m-role').value = '';
  renderMembersUI();
}
function removeMember(i) {
  members.splice(i, 1);
  renderMembersUI();
}
function renderMembersUI() {
  const list = document.getElementById('member-list');
  list.innerHTML = members.map((m, i) => `
    <div class="member-item">
      <div class="member-avatar">${m.name.charAt(0).toUpperCase()}</div>
      <div class="member-name">${m.name}</div>
      <div class="member-role">${m.role}</div>
      <div class="member-del" onclick="removeMember(${i})">×</div>
    </div>
  `).join('');
}

// ===================== IMAGES =====================
function handleImages(e) {
  const files = Array.from(e.target.files);
  const remaining = 5 - images.length;
  files.slice(0, remaining).forEach(file => {
    const reader = new FileReader();
    reader.onload = ev => {
      images.push(ev.target.result);
      renderImgPreview();
    };
    reader.readAsDataURL(file);
  });
  e.target.value = '';
}
function removeImg(i) {
  images.splice(i, 1);
  renderImgPreview();
}
function renderImgPreview() {
  const grid = document.getElementById('img-preview-grid');
  grid.innerHTML = images.map((src, i) => `
    <div class="img-thumb">
      <img src="${src}" />
      <div class="img-del" onclick="removeImg(${i})">✕</div>
    </div>
  `).join('');
}
function openLightbox(src) {
  document.getElementById('lightbox-img').src = src;
  document.getElementById('lightbox').classList.add('open');
}

// ===================== PDF EXPORT =====================
async function exportPDF(id) {
  const p = projects.find(x => x.id === id);
  if (!p) return;
  const [c1] = typeColors[p.type] || ['#4f8ef7','#6366f1'];
  const dateStr = p.created ? new Date(p.created).toLocaleDateString('th-TH', { year:'numeric', month:'long', day:'numeric' }) : '';

  const imgHtml = (p.images || []).map(src =>
    `<img src="${src}" style="width:160px;height:120px;object-fit:cover;border-radius:8px;border:1px solid #e2e8f0;" />`
  ).join('');

  const memHtml = (p.members || []).map(m =>
    `<tr><td style="padding:6px 12px;border-bottom:1px solid #f1f5f9">${m.name}</td><td style="padding:6px 12px;border-bottom:1px solid #f1f5f9;color:#64748b">${m.role}</td></tr>`
  ).join('');

  const tagHtml = (p.tags || []).map(t =>
    `<span style="background:#eff6ff;color:#3b82f6;padding:2px 10px;border-radius:20px;font-size:12px;margin:2px;">${t}</span>`
  ).join('');

  const progColor = p.progress >= 80 ? '#22c55e' : p.progress >= 40 ? '#3b82f6' : '#f97316';

  const html = `<!DOCTYPE html><html><head><meta charset="UTF-8">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600;700&display=swap');
    body { font-family:'Sarabun',sans-serif; margin:0; padding:0; background:#fff; color:#1e293b; }
    .cover { background:linear-gradient(135deg,${c1}22,#f8fafc); border-bottom:4px solid ${c1}; padding:40px 48px 32px; }
    .cover-type { font-size:13px; color:${c1}; font-weight:700; letter-spacing:1px; text-transform:uppercase; margin-bottom:8px; }
    .cover-title { font-size:28px; font-weight:700; margin-bottom:12px; }
    .cover-meta { font-size:13px; color:#64748b; }
    .section { padding:24px 48px; border-bottom:1px solid #f1f5f9; }
    .sec-label { font-size:11px; color:#94a3b8; font-weight:700; letter-spacing:1px; text-transform:uppercase; margin-bottom:8px; }
    .sec-value { font-size:15px; line-height:1.7; }
    .prog-bar { background:#f1f5f9; border-radius:100px; height:10px; overflow:hidden; }
    .prog-fill { height:100%; background:${progColor}; border-radius:100px; }
    .grid2 { display:grid; grid-template-columns:1fr 1fr; gap:24px; }
    table { width:100%; border-collapse:collapse; font-size:14px; }
    th { background:#f8fafc; padding:8px 12px; text-align:left; font-size:12px; color:#64748b; }
    .imgs { display:flex; flex-wrap:wrap; gap:12px; }
    .footer { padding:20px 48px; font-size:12px; color:#94a3b8; display:flex; justify-content:space-between; }
    .badge { display:inline-block; padding:3px 12px; border-radius:20px; font-size:12px; font-weight:700; background:${c1}22; color:${c1}; margin-bottom:12px; }
  </style></head><body>
  <div class="cover">
    <div class="cover-type">${p.type}</div>
    <div class="cover-title">${p.title}</div>
    <div><span class="badge">${p.status}</span></div>
    <div class="cover-meta">วันที่สร้าง: ${dateStr} &nbsp;|&nbsp; ความคืบหน้า: ${p.progress}%</div>
  </div>
  <div class="section">
    <div class="sec-label">คำอธิบายโครงงาน</div>
    <div class="sec-value">${p.desc}</div>
  </div>
  <div class="section">
    <div class="grid2">
      <div><div class="sec-label">วันที่เริ่มต้น</div><div class="sec-value">${p.start || '-'}</div></div>
      <div><div class="sec-label">วันที่สิ้นสุด</div><div class="sec-value">${p.end || '-'}</div></div>
    </div>
  </div>
  <div class="section">
    <div class="sec-label">ความคืบหน้า (${p.progress}%)</div>
    <div class="prog-bar" style="margin-top:8px"><div class="prog-fill" style="width:${p.progress}%"></div></div>
  </div>
  ${p.tags.length ? `<div class="section"><div class="sec-label">แท็ก</div><div style="margin-top:6px">${tagHtml}</div></div>` : ''}
  ${p.members.length ? `<div class="section"><div class="sec-label">สมาชิกในทีม</div><table style="margin-top:8px"><tr><th>ชื่อ</th><th>บทบาท</th></tr>${memHtml}</table></div>` : ''}
  ${p.url ? `<div class="section"><div class="sec-label">ลิงก์</div><div style="margin-top:4px"><a href="${p.url}" style="color:#3b82f6">${p.url}</a></div></div>` : ''}
  ${(p.images||[]).length ? `<div class="section"><div class="sec-label">รูปภาพ</div><div class="imgs" style="margin-top:10px">${imgHtml}</div></div>` : ''}
  <div class="footer"><span>ProjectSiam</span><span>ส่งออก ${new Date().toLocaleDateString('th-TH')}</span></div>
  </body></html>`;

  const blob = new Blob([html], { type: 'text/html' });
  const url = URL.createObjectURL(blob);
  const win = window.open(url, '_blank');
  if (win) {
    win.onload = () => { win.focus(); win.print(); };
  }
  showToast('เปิดหน้าต่างพิมพ์ PDF แล้ว ✓', 'success');
}

// ===================== SAVE =====================
function saveProject() {
  const title = document.getElementById('f-title').value.trim();
  const desc = document.getElementById('f-desc').value.trim();
  if (!title || !desc) { showToast('กรุณากรอกชื่อและคำอธิบายโครงงาน', 'warn'); return; }

  const p = {
    id: editId || Date.now().toString(),
    title,
    desc,
    type: document.getElementById('f-type').value,
    status: document.getElementById('f-status').value,
    start: document.getElementById('f-start').value,
    end: document.getElementById('f-end').value,
    progress: parseInt(document.getElementById('f-progress').value),
    tags: [...tags],
    members: [...members],
    images: [...images],
    url: document.getElementById('f-url').value.trim(),
    created: editId ? (projects.find(x=>x.id===editId)||{}).created || new Date().toISOString() : new Date().toISOString(),
  };

  if (editId) {
    const idx = projects.findIndex(x => x.id === editId);
    if (idx !== -1) projects[idx] = p;
    editId = null;
  } else {
    projects.unshift(p);
  }

  localStorage.setItem('ph_projects', JSON.stringify(projects));
  clearForm();
  renderProjects();
  updateStats();
  switchTab('browse');
  showToast('บันทึกโครงงานเรียบร้อยแล้ว ✓', 'success');
}

function clearForm() {
  ['f-title','f-desc','f-url'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('f-type').value = 'เทคโนโลยี';
  document.getElementById('f-status').value = 'รอดำเนินการ';
  document.getElementById('f-start').value = '';
  document.getElementById('f-end').value = '';
  document.getElementById('f-progress').value = 0;
  document.getElementById('prog-pct').textContent = '0%';
  tags = []; members = []; images = []; editId = null;
  renderTagUI(); renderMembersUI(); renderImgPreview();
}

// ===================== RENDER PROJECTS =====================
function renderProjects() {
  const q = document.getElementById('searchBox').value.toLowerCase();
  const fs = document.getElementById('filterStatus').value;
  const ft = document.getElementById('filterType').value;

  let list = projects.filter(p => {
    const m = !q || p.title.toLowerCase().includes(q) || p.desc.toLowerCase().includes(q) || p.tags.some(t => t.toLowerCase().includes(q));
    const ms = !fs || p.status === fs;
    const mt = !ft || p.type === ft;
    return m && ms && mt;
  });

  const grid = document.getElementById('projects-grid');
  if (!list.length) {
    grid.innerHTML = `<div class="empty" style="grid-column:1/-1"><div class="empty-icon">📭</div><div class="empty-text">ยังไม่มีโครงงาน<br><small style="font-size:13px">คลิก "เพิ่มโครงงาน" เพื่อเริ่มต้น</small></div></div>`;
    return;
  }

  grid.innerHTML = list.map(p => {
    const [c1, c2] = typeColors[p.type] || ['#94a3b8','#64748b'];
    const badge = statusBadge[p.status] || 'badge-blue';
    const dateStr = p.created ? new Date(p.created).toLocaleDateString('th-TH', { year:'numeric', month:'short', day:'numeric' }) : '';
    const avs = p.members.slice(0,4).map(m => `<div class="card-member-av">${m.name.charAt(0).toUpperCase()}</div>`).join('');
    const extra = p.members.length > 4 ? `<div class="card-member-av" style="background:var(--card);color:var(--muted);font-size:9px">+${p.members.length-4}</div>` : '';
    const tagHtml = p.tags.slice(0,4).map(t => `<span class="card-tag">${t}</span>`).join('');
    const progColor = p.progress >= 80 ? '#34d399' : p.progress >= 40 ? '#4f8ef7' : '#fb923c';
    return `
      <div class="project-card" onclick="openProject('${p.id}')">
        <div class="card-banner" style="background:linear-gradient(90deg,${c1},${c2})"></div>
        <div class="card-body">
          <div class="card-top">
            <div class="card-title">${p.title}</div>
            <span class="badge ${badge}" style="margin-left:10px">${p.status}</span>
          </div>
          <div class="card-desc">${p.desc}</div>
          ${p.tags.length ? `<div class="card-tags">${tagHtml}</div>` : ''}
          <div class="card-progress">
            <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:4px">
              <span>ความคืบหน้า</span><span>${p.progress}%</span>
            </div>
            <div class="card-prog-bar"><div class="card-prog-fill" style="width:${p.progress}%;background:linear-gradient(90deg,${progColor},${c2})"></div></div>
          </div>
          <div class="card-footer">
            <div class="card-members">${avs}${extra}</div>
            <div class="card-date">${dateStr}</div>
          </div>
        </div>
      </div>
    `;
  }).join('');
}

// ===================== STATS =====================
function updateStats() {
  document.getElementById('stat-total').textContent = projects.length;
  document.getElementById('stat-prog').textContent = projects.filter(p=>p.status==='กำลังดำเนินการ').length;
  document.getElementById('stat-done').textContent = projects.filter(p=>p.status==='เสร็จสมบูรณ์').length;
  document.getElementById('stat-members').textContent = projects.reduce((a,p)=>a+p.members.length,0);
}

// ===================== MODAL =====================
async function openProject(id) {
  const p = projects.find(x => x.id === id);
  if (!p) return;
  const [c1, c2] = typeColors[p.type] || ['#94a3b8','#64748b'];
  const badge = statusBadge[p.status] || 'badge-blue';
  const dateStr = p.created ? new Date(p.created).toLocaleDateString('th-TH', { year:'numeric', month:'long', day:'numeric' }) : '';

  document.getElementById('modal-banner').style.background = `linear-gradient(90deg,${c1},${c2})`;
  document.getElementById('modal-title').textContent = p.title;
  document.getElementById('modal-subtitle').innerHTML = `<span class="badge ${badge}">${p.status}</span> &nbsp; ${p.type} &nbsp;·&nbsp; ${dateStr}`;

  const memHtml = p.members.length
    ? p.members.map(m => `<div class="detail-member"><div class="member-avatar">${m.name.charAt(0).toUpperCase()}</div><div><div style="font-weight:600;font-size:14px">${m.name}</div><div style="font-size:12px;color:var(--muted)">${m.role}</div></div></div>`).join('')
    : '<div style="color:var(--muted);font-size:13px">ไม่มีสมาชิก</div>';

  const tagHtml = p.tags.length
    ? p.tags.map(t => `<span class="card-tag">${t}</span>`).join(' ')
    : '<span style="color:var(--muted);font-size:13px">ไม่มีแท็ก</span>';

  const urlHtml = p.url ? `<a href="${p.url}" target="_blank" style="color:var(--accent);font-size:14px;word-break:break-all">${p.url}</a>` : '<span style="color:var(--muted);font-size:13px">ไม่มี</span>';

  const progColor = p.progress >= 80 ? '#34d399' : p.progress >= 40 ? '#4f8ef7' : '#fb923c';

  document.getElementById('modal-body').innerHTML = `
    <div class="detail-section">
      <div class="detail-label">คำอธิบาย</div>
      <div class="detail-value">${p.desc}</div>
    </div>
    <div class="detail-grid" style="margin-bottom:24px">
      <div>
        <div class="detail-label">วันที่เริ่มต้น</div>
        <div class="detail-value">${p.start || '-'}</div>
      </div>
      <div>
        <div class="detail-label">วันที่สิ้นสุด</div>
        <div class="detail-value">${p.end || '-'}</div>
      </div>
    </div>
    <div class="detail-section">
      <div class="detail-label">ความคืบหน้า</div>
      <div style="display:flex;align-items:center;gap:14px;margin-top:6px">
        <div style="flex:1;background:var(--card);border-radius:100px;height:8px;overflow:hidden">
          <div style="height:100%;width:${p.progress}%;background:linear-gradient(90deg,${progColor},${c2});border-radius:100px"></div>
        </div>
        <div style="font-size:20px;font-weight:700;font-family:'Space Grotesk',sans-serif;color:${progColor}">${p.progress}%</div>
      </div>
    </div>
    <div class="detail-section">
      <div class="detail-label">แท็ก</div>
      <div style="display:flex;flex-wrap:wrap;gap:6px;margin-top:6px">${tagHtml}</div>
    </div>
    <div class="detail-section">
      <div class="detail-label">สมาชิกในทีม</div>
      <div class="detail-members" style="margin-top:8px">${memHtml}</div>
    </div>
    <div class="detail-section">
      <div class="detail-label">ลิงก์</div>
      <div style="margin-top:4px">${urlHtml}</div>
    </div>
    ${(p.images||[]).length ? `
    <div class="detail-section">
      <div class="detail-label">รูปภาพ (${p.images.length})</div>
      <div class="modal-images">${p.images.map(src=>`<img class="modal-img" src="${src}" onclick="openLightbox('${src}')" />`).join('')}</div>
    </div>` : ''}
    <div class="ai-section" id="ai-section">
      <div class="ai-label">✨ AI วิเคราะห์โครงงาน</div>
      <div class="ai-text ai-loading" id="ai-text">
        <span class="spinner"></span> กำลังวิเคราะห์...
      </div>
    </div>
    <div style="display:flex;gap:10px;margin-top:20px">
      <button class="btn btn-outline" style="flex:1" onclick="editProject('${p.id}')">✏️ แก้ไข</button>
      <button class="btn btn-primary" style="flex:1" onclick="exportPDF('${p.id}')">📄 ส่งออก PDF</button>
      <button class="btn" style="background:#ef444420;color:#f87171;border:1.5px solid #ef444440;padding:8px 14px" onclick="deleteProject('${p.id}')">🗑️</button>
    </div>
  `;

  document.getElementById('modal-overlay').classList.add('open');

  // AI Analysis
  try {
    const resp = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: `วิเคราะห์โครงงานนี้เป็นภาษาไทย (3-4 ประโยค กระชับ ชัดเจน):
ชื่อ: ${p.title}
ประเภท: ${p.type}
สถานะ: ${p.status}
ความคืบหน้า: ${p.progress}%
คำอธิบาย: ${p.desc}
สมาชิก: ${p.members.map(m=>m.name+' ('+m.role+')').join(', ') || 'ไม่มี'}
แท็ก: ${p.tags.join(', ') || 'ไม่มี'}

กรุณาให้:
1. ประเมินสถานะโครงงาน
2. จุดแข็งที่น่าสนใจ
3. ข้อแนะนำเพื่อพัฒนาต่อ`
        }]
      })
    });
    const data = await resp.json();
    const text = data.content?.map(c => c.text || '').join('') || 'ไม่สามารถวิเคราะห์ได้';
    document.getElementById('ai-text').innerHTML = text.replace(/\n/g, '<br>');
  } catch (e) {
    document.getElementById('ai-text').textContent = 'ไม่สามารถเชื่อมต่อ AI ได้ในขณะนี้';
  }
}

function closeModal(e) {
  if (e.target === document.getElementById('modal-overlay')) {
    document.getElementById('modal-overlay').classList.remove('open');
  }
}

function editProject(id) {
  const p = projects.find(x => x.id === id);
  if (!p) return;
  document.getElementById('modal-overlay').classList.remove('open');
  document.getElementById('f-title').value = p.title;
  document.getElementById('f-desc').value = p.desc;
  document.getElementById('f-type').value = p.type;
  document.getElementById('f-status').value = p.status;
  document.getElementById('f-start').value = p.start || '';
  document.getElementById('f-end').value = p.end || '';
  document.getElementById('f-progress').value = p.progress;
  document.getElementById('prog-pct').textContent = p.progress + '%';
  document.getElementById('f-url').value = p.url || '';
  tags = [...p.tags]; members = [...p.members]; images = [...(p.images||[])]; editId = id;
  renderTagUI(); renderMembersUI(); renderImgPreview();
  switchTab('add');
}

function deleteProject(id) {
  if (!confirm('ยืนยันการลบโครงงานนี้?')) return;
  projects = projects.filter(x => x.id !== id);
  localStorage.setItem('ph_projects', JSON.stringify(projects));
  document.getElementById('modal-overlay').classList.remove('open');
  renderProjects(); updateStats();
  showToast('ลบโครงงานแล้ว', 'success');
}

// ===================== TOAST =====================
function showToast(msg, type='success') {
  const t = document.getElementById('toast');
  document.getElementById('toast-msg').textContent = msg;
  t.className = 'toast ' + type;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

// ===================== INIT =====================
renderProjects();
updateStats();

// Set today's date
const today = new Date().toISOString().split('T')[0];
document.getElementById('f-start').value = today;
</script>
</body>
</html>
**
