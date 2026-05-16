<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Engineering PMO System</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Myanmar:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg:#0a0e1a; --bg2:#0f1629; --bg3:#162040; --bg4:#1e2d55;
  --border:#1e3060; --border2:#2a4080;
  --accent:#4f8ef7; --accent2:#00d4aa; --accent3:#ff6b6b; --accent4:#ffd166; --accent5:#a78bfa;
  --text:#e8f0ff; --text2:#8fa8d0; --text3:#4a6090;
  --card:#0f1629; --radius:12px;
  --font:'Inter','Noto Sans Myanmar',sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{font-family:var(--font);background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;}

/* BG GRID */
body::before{
  content:'';position:fixed;inset:0;
  background-image:linear-gradient(rgba(79,142,247,0.03) 1px,transparent 1px),linear-gradient(90deg,rgba(79,142,247,0.03) 1px,transparent 1px);
  background-size:40px 40px;pointer-events:none;z-index:0;
}

/* TOPBAR */
.topbar{
  position:sticky;top:0;z-index:200;
  background:rgba(10,14,26,0.92);
  border-bottom:1px solid var(--border);
  backdrop-filter:blur(20px);
  padding:0 28px;height:60px;
  display:flex;align-items:center;justify-content:space-between;
}
.logo-area{display:flex;align-items:center;gap:14px;}
.logo-icon{
  width:36px;height:36px;border-radius:8px;
  background:linear-gradient(135deg,var(--accent),var(--accent2));
  display:flex;align-items:center;justify-content:center;font-size:16px;
}
.logo-text{font-size:15px;font-weight:700;letter-spacing:0.5px;}
.logo-sub{font-size:10px;color:var(--text2);letter-spacing:1px;margin-top:1px;}
.topbar-right{display:flex;align-items:center;gap:12px;}
.lang-toggle{
  display:flex;border:1px solid var(--border2);border-radius:8px;overflow:hidden;
}
.lang-btn{
  padding:6px 14px;font-size:12px;font-weight:600;cursor:pointer;border:none;
  background:transparent;color:var(--text2);transition:all 0.2s;font-family:var(--font);
}
.lang-btn.active{background:var(--accent);color:#fff;}
.time-chip{
  font-size:11px;color:var(--text2);
  background:var(--bg3);border:1px solid var(--border);
  padding:5px 12px;border-radius:6px;font-variant-numeric:tabular-nums;
}
.user-chip{
  display:flex;align-items:center;gap:8px;
  background:var(--bg3);border:1px solid var(--border);
  padding:5px 12px 5px 6px;border-radius:8px;font-size:12px;cursor:pointer;
}
.user-avatar{
  width:24px;height:24px;border-radius:50%;
  background:linear-gradient(135deg,var(--accent),var(--accent5));
  display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;
}

/* SIDEBAR */
.layout{display:flex;position:relative;z-index:1;}
.sidebar{
  width:220px;min-height:calc(100vh - 60px);
  background:rgba(15,22,41,0.8);
  border-right:1px solid var(--border);
  padding:20px 12px;position:sticky;top:60px;
  flex-shrink:0;
}
.nav-section{font-size:10px;color:var(--text3);letter-spacing:1.2px;font-weight:600;
  padding:12px 10px 6px;text-transform:uppercase;}
.nav-item{
  display:flex;align-items:center;gap:10px;
  padding:9px 12px;border-radius:8px;cursor:pointer;
  font-size:13px;color:var(--text2);transition:all 0.15s;margin-bottom:2px;
}
.nav-item:hover{background:var(--bg3);color:var(--text);}
.nav-item.active{background:rgba(79,142,247,0.15);color:var(--accent);border:1px solid rgba(79,142,247,0.3);}
.nav-icon{font-size:16px;width:20px;text-align:center;}
.nav-badge{
  margin-left:auto;font-size:10px;font-weight:600;
  background:var(--accent3);color:#fff;
  padding:2px 7px;border-radius:10px;
}

/* CONTENT */
.content{flex:1;padding:24px;min-width:0;}
.page{display:none;animation:fadeIn 0.3s ease;}
.page.active{display:block;}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* PAGE HEADER */
.page-header{margin-bottom:24px;}
.page-title{font-size:22px;font-weight:700;}
.page-sub{font-size:13px;color:var(--text2);margin-top:4px;}

/* CARDS */
.card{
  background:var(--card);border:1px solid var(--border);
  border-radius:var(--radius);padding:20px;position:relative;overflow:hidden;
}
.card::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,rgba(79,142,247,0.03),transparent);
  pointer-events:none;
}
.card-title{font-size:11px;font-weight:600;color:var(--text2);
  text-transform:uppercase;letter-spacing:1px;margin-bottom:14px;}

/* GRIDS */
.g2{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:14px;}
.g4{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;}
@media(max-width:900px){.g2,.g3,.g4{grid-template-columns:1fr;} .sidebar{display:none;}}

/* STAT CARDS */
.stat-card{
  background:var(--card);border:1px solid var(--border);
  border-radius:var(--radius);padding:18px 20px;
  position:relative;overflow:hidden;
}
.stat-top{display:flex;align-items:flex-start;justify-content:space-between;}
.stat-icon{
  width:42px;height:42px;border-radius:10px;
  display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0;
}
.stat-val{font-size:30px;font-weight:700;margin-top:10px;line-height:1;}
.stat-label{font-size:12px;color:var(--text2);margin-top:5px;}
.stat-trend{font-size:11px;margin-top:8px;display:flex;align-items:center;gap:4px;}
.trend-up{color:var(--accent2);}
.trend-down{color:var(--accent3);}
.stat-bar{height:3px;background:var(--bg3);border-radius:2px;margin-top:12px;overflow:hidden;}
.stat-bar-fill{height:100%;border-radius:2px;transition:width 1s;}

/* PERFORMANCE CHART */
.perf-ring{
  width:80px;height:80px;position:relative;flex-shrink:0;
}
.perf-ring svg{transform:rotate(-90deg);}
.perf-ring .ring-bg{fill:none;stroke:var(--bg3);stroke-width:8;}
.perf-ring .ring-fill{fill:none;stroke-width:8;stroke-linecap:round;transition:stroke-dashoffset 1s;}
.perf-center{
  position:absolute;inset:0;display:flex;align-items:center;
  justify-content:center;font-size:14px;font-weight:700;
}

/* STAFF PERFORMANCE CARD */
.staff-perf-card{
  background:var(--card);border:1px solid var(--border);
  border-radius:var(--radius);padding:16px;
  display:flex;align-items:center;gap:16px;
  transition:all 0.2s;cursor:pointer;
}
.staff-perf-card:hover{border-color:var(--border2);transform:translateY(-2px);
  box-shadow:0 8px 24px rgba(0,0,0,0.3);}
.staff-av{
  width:48px;height:48px;border-radius:12px;
  display:flex;align-items:center;justify-content:center;
  font-size:16px;font-weight:700;flex-shrink:0;
}
.staff-info{flex:1;min-width:0;}
.staff-name-big{font-size:13px;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.staff-role-sm{font-size:11px;color:var(--text2);margin-top:2px;}
.staff-metrics{display:flex;gap:10px;margin-top:8px;}
.metric-chip{
  font-size:10px;padding:2px 8px;border-radius:4px;font-weight:600;
  background:rgba(255,255,255,0.05);color:var(--text2);
}

/* PILL */
.pill{display:inline-flex;align-items:center;gap:4px;padding:3px 10px;border-radius:20px;font-size:11px;font-weight:600;}
.pill-green{background:rgba(0,212,170,0.15);color:var(--accent2);border:1px solid rgba(0,212,170,0.3);}
.pill-blue{background:rgba(79,142,247,0.15);color:var(--accent);border:1px solid rgba(79,142,247,0.3);}
.pill-yellow{background:rgba(255,209,102,0.15);color:var(--accent4);border:1px solid rgba(255,209,102,0.3);}
.pill-red{background:rgba(255,107,107,0.15);color:var(--accent3);border:1px solid rgba(255,107,107,0.3);}
.pill-purple{background:rgba(167,139,250,0.15);color:var(--accent5);border:1px solid rgba(167,139,250,0.3);}

/* FORM */
.form-group{margin-bottom:16px;}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:16px;}
.form-row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-bottom:16px;}
label{display:block;font-size:12px;font-weight:500;color:var(--text2);margin-bottom:6px;letter-spacing:0.3px;}
label .my{font-size:11px;color:var(--text3);}
input,select,textarea{
  width:100%;background:var(--bg3);border:1px solid var(--border2);
  border-radius:8px;color:var(--text);font-family:var(--font);
  font-size:13px;padding:10px 14px;outline:none;transition:all 0.15s;
}
input:focus,select:focus,textarea:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(79,142,247,0.1);}
textarea{resize:vertical;min-height:90px;line-height:1.6;}
select option{background:var(--bg2);}

/* BUTTONS */
.btn{
  display:inline-flex;align-items:center;gap:7px;
  padding:10px 20px;border-radius:8px;font-family:var(--font);
  font-size:13px;font-weight:600;cursor:pointer;border:none;transition:all 0.2s;
}
.btn-primary{background:linear-gradient(135deg,var(--accent),#6366f1);color:#fff;}
.btn-primary:hover{opacity:0.9;transform:translateY(-1px);box-shadow:0 4px 16px rgba(79,142,247,0.3);}
.btn-success{background:linear-gradient(135deg,var(--accent2),#00b894);color:#0a0e1a;}
.btn-success:hover{opacity:0.9;transform:translateY(-1px);}
.btn-outline{background:transparent;border:1px solid var(--border2);color:var(--text);}
.btn-outline:hover{border-color:var(--accent);color:var(--accent);}
.btn-purple{background:linear-gradient(135deg,var(--accent5),#8b5cf6);color:#fff;}
.btn-purple:hover{opacity:0.9;transform:translateY(-1px);}
.btn-sm{padding:6px 14px;font-size:12px;}
.btn-danger{background:rgba(255,107,107,0.15);border:1px solid rgba(255,107,107,0.4);color:var(--accent3);}

/* TABLE */
.tbl-wrap{overflow-x:auto;}
table{width:100%;border-collapse:collapse;}
th{font-size:11px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:0.8px;
  padding:11px 16px;border-bottom:1px solid var(--border);text-align:left;white-space:nowrap;}
td{padding:13px 16px;border-bottom:1px solid rgba(30,48,96,0.5);font-size:13px;color:var(--text);}
tr:last-child td{border-bottom:none;}
tr:hover td{background:rgba(79,142,247,0.03);}

/* PROGRESS */
.prog-bar{background:var(--bg3);border-radius:6px;height:8px;overflow:hidden;}
.prog-fill{height:100%;border-radius:6px;transition:width 0.8s;}

/* AI BOX */
.ai-box{
  background:linear-gradient(135deg,rgba(79,142,247,0.08),rgba(167,139,250,0.08));
  border:1px solid rgba(79,142,247,0.3);border-radius:var(--radius);
  padding:20px;position:relative;overflow:hidden;
}
.ai-box::before{
  content:'✦ AI';position:absolute;right:16px;top:12px;
  font-size:10px;color:var(--accent);opacity:0.6;letter-spacing:1px;font-weight:700;
}
.ai-loading{
  display:flex;align-items:center;gap:10px;color:var(--text2);font-size:13px;padding:10px 0;
}
.ai-dots span{
  display:inline-block;width:6px;height:6px;border-radius:50%;
  background:var(--accent);margin:0 2px;animation:dot 1.2s infinite;
}
.ai-dots span:nth-child(2){animation-delay:0.2s;}
.ai-dots span:nth-child(3){animation-delay:0.4s;}
@keyframes dot{0%,80%,100%{transform:scale(0.6);opacity:0.4;}40%{transform:scale(1);opacity:1;}}
.ai-result{font-size:13px;line-height:1.8;color:var(--text);white-space:pre-wrap;}
.ai-result .ai-head{color:var(--accent);font-weight:700;}
.ai-result .ai-good{color:var(--accent2);}
.ai-result .ai-warn{color:var(--accent4);}
.ai-result .ai-bad{color:var(--accent3);}

/* REPORT BOX */
.report-box{
  background:var(--bg);border:1px solid var(--border);border-radius:8px;
  padding:20px;font-size:12px;line-height:1.9;color:var(--text2);
  white-space:pre-wrap;max-height:400px;overflow-y:auto;font-family:'Courier New',monospace;
}
.report-box .r-h{color:var(--accent);font-weight:700;}
.report-box .r-l{color:var(--accent4);}
.report-box .r-v{color:var(--text);}

/* DIVIDER */
hr{border:none;border-top:1px solid var(--border);margin:20px 0;}

/* TOAST */
#toast{
  position:fixed;bottom:24px;right:24px;z-index:9999;
  padding:13px 22px;border-radius:10px;font-size:13px;font-weight:600;
  opacity:0;transform:translateY(12px);transition:all 0.3s;pointer-events:none;
  box-shadow:0 8px 24px rgba(0,0,0,0.4);
}
#toast.show{opacity:1;transform:translateY(0);}

/* MODAL */
.modal-overlay{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,0.75);
  z-index:500;align-items:center;justify-content:center;backdrop-filter:blur(4px);
}
.modal-overlay.open{display:flex;}
.modal-box{
  background:var(--bg2);border:1px solid var(--border2);border-radius:16px;
  max-width:780px;width:95%;max-height:88vh;overflow:hidden;
  display:flex;flex-direction:column;
}
.modal-header{
  padding:18px 24px;border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
}
.modal-body{padding:24px;overflow-y:auto;}

/* SCORE BADGE */
.score-badge{
  width:56px;height:56px;border-radius:12px;
  display:flex;align-items:center;justify-content:center;
  font-size:18px;font-weight:800;flex-shrink:0;
}

/* MISC */
.mt16{margin-top:16px;} .mt20{margin-top:20px;} .mb16{margin-bottom:16px;}
.flex{display:flex;} .flex-gap{display:flex;gap:10px;flex-wrap:wrap;}
.ai-c{align-items:center;} .jb{justify-content:space-between;} .je{justify-content:flex-end;}
.span2{grid-column:span 2;}
.text2{color:var(--text2);} .text3{color:var(--text3);}
.fw6{font-weight:600;} .fs12{font-size:12px;} .fs11{font-size:11px;}
</style>
</head>
<body>

<!-- TOPBAR -->
<div class="topbar">
  <div class="logo-area">
    <div class="logo-icon">⚙</div>
    <div>
      <div class="logo-text" id="t-logo">Engineering PMO System</div>
      <div class="logo-sub" id="t-logosub">PERFORMANCE MONITORING</div>
    </div>
  </div>
  <div class="topbar-right">
    <div class="lang-toggle">
      <button class="lang-btn active" onclick="setLang('en')">EN</button>
      <button class="lang-btn" onclick="setLang('my')">မြန်မာ</button>
    </div>
    <div class="time-chip" id="clock">--:--:--</div>
    <div class="user-chip">
      <div class="user-avatar">PMO</div>
      <span id="t-pmo">PMO Officer</span>
    </div>
  </div>
</div>

<div class="layout">
<!-- SIDEBAR -->
<div class="sidebar">
  <div class="nav-section" id="t-nav-main">MAIN</div>
  <div class="nav-item active" onclick="nav('dashboard')">
    <span class="nav-icon">📊</span><span id="t-nav-dash">Dashboard</span>
  </div>
  <div class="nav-item" onclick="nav('daily')">
    <span class="nav-icon">📝</span><span id="t-nav-daily">Daily Report</span>
    <span class="nav-badge" id="pending-badge" style="display:none">!</span>
  </div>
  <div class="nav-item" onclick="nav('monthly')">
    <span class="nav-icon">📅</span><span id="t-nav-monthly">Monthly Summary</span>
  </div>
  <div class="nav-section" id="t-nav-analysis">ANALYSIS</div>
  <div class="nav-item" onclick="nav('performance')">
    <span class="nav-icon">🏆</span><span id="t-nav-perf">Performance</span>
  </div>
  <div class="nav-item" onclick="nav('ai-analysis')">
    <span class="nav-icon">🤖</span><span id="t-nav-ai">AI Analysis</span>
  </div>
  <div class="nav-section" id="t-nav-manage">MANAGE</div>
  <div class="nav-item" onclick="nav('records')">
    <span class="nav-icon">🗂</span><span id="t-nav-rec">Records</span>
  </div>
  <div class="nav-item" onclick="nav('staff')">
    <span class="nav-icon">👥</span><span id="t-nav-staff">Staff</span>
  </div>
</div>

<!-- CONTENT -->
<div class="content">

<!-- ══ DASHBOARD ══ -->
<div id="page-dashboard" class="page active">
  <div class="page-header">
    <div class="page-title" id="t-dash-title">📊 Overview Dashboard</div>
    <div class="page-sub" id="t-dash-sub">Engineering Team — Real-time PMO Monitoring</div>
  </div>

  <!-- Stat Row -->
  <div class="g4 mb16">
    <div class="stat-card">
      <div class="stat-top">
        <div>
          <div style="font-size:11px;color:var(--text2);font-weight:600;text-transform:uppercase;letter-spacing:0.8px" id="t-s1">Reports This Month</div>
        </div>
        <div class="stat-icon" style="background:rgba(79,142,247,0.15)">📝</div>
      </div>
      <div class="stat-val" id="s-reports">0</div>
      <div class="stat-label" id="t-s1b">Daily submissions</div>
      <div class="stat-bar mt16"><div class="stat-bar-fill" id="sb-reports" style="background:var(--accent);width:0%"></div></div>
    </div>
    <div class="stat-card">
      <div class="stat-top">
        <div><div style="font-size:11px;color:var(--text2);font-weight:600;text-transform:uppercase;letter-spacing:0.8px" id="t-s2">Team Performance</div></div>
        <div class="stat-icon" style="background:rgba(0,212,170,0.15)">🏆</div>
      </div>
      <div class="stat-val" id="s-perf">—</div>
      <div class="stat-label" id="t-s2b">Avg score / 100</div>
      <div class="stat-bar mt16"><div class="stat-bar-fill" id="sb-perf" style="background:var(--accent2);width:0%"></div></div>
    </div>
    <div class="stat-card">
      <div class="stat-top">
        <div><div style="font-size:11px;color:var(--text2);font-weight:600;text-transform:uppercase;letter-spacing:0.8px" id="t-s3">Issues Reported</div></div>
        <div class="stat-icon" style="background:rgba(255,107,107,0.15)">⚠️</div>
      </div>
      <div class="stat-val" id="s-issues">0</div>
      <div class="stat-label" id="t-s3b">Total open issues</div>
      <div class="stat-bar mt16"><div class="stat-bar-fill" id="sb-issues" style="background:var(--accent3);width:0%"></div></div>
    </div>
    <div class="stat-card">
      <div class="stat-top">
        <div><div style="font-size:11px;color:var(--text2);font-weight:600;text-transform:uppercase;letter-spacing:0.8px" id="t-s4">Avg Progress</div></div>
        <div class="stat-icon" style="background:rgba(255,209,102,0.15)">📈</div>
      </div>
      <div class="stat-val" id="s-progress">—</div>
      <div class="stat-label" id="t-s4b">Work completion rate</div>
      <div class="stat-bar mt16"><div class="stat-bar-fill" id="sb-progress" style="background:var(--accent4);width:0%"></div></div>
    </div>
  </div>

  <div class="g2">
    <!-- Staff Performance Quick View -->
    <div class="card">
      <div class="card-title" id="t-staffperf">STAFF PERFORMANCE OVERVIEW</div>
      <div id="dash-staff-list" style="display:flex;flex-direction:column;gap:10px;"></div>
    </div>

    <!-- Recent Activity -->
    <div class="card">
      <div class="card-title" id="t-recent">RECENT REPORTS</div>
      <div class="tbl-wrap">
        <table>
          <thead><tr>
            <th id="t-th-date">Date</th>
            <th id="t-th-staff">Staff</th>
            <th id="t-th-prog">Progress</th>
            <th id="t-th-status">Status</th>
          </tr></thead>
          <tbody id="dash-recent"></tbody>
        </table>
      </div>
    </div>
  </div>
</div>

<!-- ══ DAILY REPORT ══ -->
<div id="page-daily" class="page">
  <div class="page-header">
    <div class="page-title" id="t-daily-title">📝 Daily Report</div>
    <div class="page-sub" id="t-daily-sub">Submit daily engineering activity report to PMO</div>
  </div>
  <div class="card">
    <div class="form-row">
      <div class="form-group">
        <label id="t-f-date">Report Date <span class="my">/ နေ့စဥ် အစီရင်ခံချိန်</span></label>
        <input type="date" id="d-date">
      </div>
      <div class="form-group">
        <label id="t-f-rep">Submitted By <span class="my">/ တင်သွင်းသူ</span></label>
        <select id="d-reporter">
          <option value="">— Select / ရွေးချယ်ပါ —</option>
          <option value="Phyo Thiha Kyaw">Phyo Thiha Kyaw (PMO Assistant)</option>
          <option value="Tay Zar">Tay Zar (PMO Assistant)</option>
          <option value="Daw Pan Ei Phyu">Daw Pan Ei Phyu (Co-Unit Leader)</option>
          <option value="Daw Shune Yati Hmue">Daw Shune Yati Hmue (Co-Unit Leader)</option>
          <option value="U Hein Kyaw Lin">U Hein Kyaw Lin (Engineering Supervisor)</option>
          <option value="U San Lin Naing">U San Lin Naing (Co-Unit Leader C-1,C-2)</option>
          <option value="U Kyaw Soe Lwin">U Kyaw Soe Lwin (Machinery Supervisor)</option>
          <option value="U Myo Naing">U Myo Naing (Machinery Supervisor)</option>
        </select>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label id="t-f-unit">Unit <span class="my">/ တပ်ဖွဲ့</span></label>
        <select id="d-unit">
          <option value="">— Select —</option>
          <option>PMO</option><option>Engineering Unit</option>
          <option>C-1 Unit</option><option>C-2 Unit</option><option>Machinery Unit</option>
        </select>
      </div>
      <div class="form-group">
        <label id="t-f-prog">Work Progress % <span class="my">/ လုပ်ငန်းတိုးတက်မှု</span></label>
        <input type="number" id="d-progress" min="0" max="100" placeholder="0 – 100">
      </div>
    </div>
    <div class="form-group">
      <label id="t-f-tasks">Tasks Completed <span class="my">/ ပြီးစီးသောလုပ်ငန်းများ</span></label>
      <textarea id="d-tasks" placeholder="List tasks completed today... / ယနေ့ပြီးစီးသောလုပ်ငန်းများ တစ်ကြောင်းစီ ထည့်ပါ..."></textarea>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label id="t-f-issues">Issues Encountered <span class="my">/ ကြုံတွေ့ပြဿနာများ</span></label>
        <textarea id="d-issues" placeholder="Problems / issues..."></textarea>
      </div>
      <div class="form-group">
        <label id="t-f-sol">Solutions Taken <span class="my">/ ဖြေရှင်းနည်းများ</span></label>
        <textarea id="d-solutions" placeholder="Actions taken..."></textarea>
      </div>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label id="t-f-plan">Tomorrow's Plan <span class="my">/ မနက်ဖြန် အစီအစဥ်</span></label>
        <textarea id="d-plan" placeholder="Planned tasks..."></textarea>
      </div>
      <div class="form-group">
        <label id="t-f-rem">Remarks <span class="my">/ မှတ်ချက်</span></label>
        <textarea id="d-remarks" placeholder="Additional notes..."></textarea>
      </div>
    </div>
    <!-- Performance Self-Score -->
    <div class="card" style="background:rgba(79,142,247,0.05);border-color:rgba(79,142,247,0.2);margin-bottom:16px">
      <div class="card-title" id="t-selfscore">SELF-ASSESSMENT / ကိုယ်တိုင်အကဲဖြတ်ချက်</div>
      <div class="form-row3">
        <div class="form-group" style="margin-bottom:0">
          <label id="t-qa">Work Quality (1–10) <span class="my">/ လုပ်ငန်းအရည်အသွေး</span></label>
          <input type="number" id="d-quality" min="1" max="10" placeholder="1–10">
        </div>
        <div class="form-group" style="margin-bottom:0">
          <label id="t-pa">Punctuality (1–10) <span class="my">/ အချိန်တိကျမှု</span></label>
          <input type="number" id="d-punctuality" min="1" max="10" placeholder="1–10">
        </div>
        <div class="form-group" style="margin-bottom:0">
          <label id="t-ta">Teamwork (1–10) <span class="my">/ အဖွဲ့လုပ်ဆောင်မှု</span></label>
          <input type="number" id="d-teamwork" min="1" max="10" placeholder="1–10">
        </div>
      </div>
    </div>
    <hr>
    <div class="flex flex-gap je">
      <button class="btn btn-outline" onclick="previewDaily()" id="t-btn-preview">👁 Preview</button>
      <button class="btn btn-purple" onclick="aiAnalyzeDaily()" id="t-btn-ai">🤖 AI Analysis</button>
      <button class="btn btn-success" onclick="submitDaily()" id="t-btn-submit">✅ Submit to PMO</button>
    </div>
  </div>

  <!-- Preview -->
  <div id="daily-preview-wrap" style="display:none;margin-top:20px">
    <div class="card">
      <div class="flex jb ai-c mb16">
        <div class="card-title" id="t-prev-head">REPORT PREVIEW</div>
        <div class="flex-gap">
          <button class="btn btn-outline btn-sm" onclick="copyTxt('daily-preview')">📋 Copy</button>
          <button class="btn btn-primary btn-sm" onclick="window.print()">🖨 Print</button>
        </div>
      </div>
      <div class="report-box" id="daily-preview"></div>
    </div>
  </div>

  <!-- AI Result for Daily -->
  <div id="daily-ai-wrap" style="display:none;margin-top:20px">
    <div class="ai-box">
      <div class="card-title" id="t-ai-daily-head" style="color:var(--accent)">🤖 AI ANALYSIS RESULT</div>
      <div id="daily-ai-content"></div>
    </div>
  </div>
</div>

<!-- ══ MONTHLY ══ -->
<div id="page-monthly" class="page">
  <div class="page-header">
    <div class="page-title" id="t-mo-title">📅 Monthly Summary Report</div>
    <div class="page-sub" id="t-mo-sub">Auto-generate monthly performance summary for PMO</div>
  </div>
  <div class="card">
    <div class="form-row3">
      <div class="form-group">
        <label id="t-mo-month">Month <span class="my">/ လ</span></label>
        <select id="m-month">
          <option>January</option><option>February</option><option>March</option>
          <option>April</option><option>May</option><option>June</option>
          <option>July</option><option>August</option><option>September</option>
          <option>October</option><option>November</option><option>December</option>
        </select>
      </div>
      <div class="form-group">
        <label>Year <span class="my">/ နှစ်</span></label>
        <input type="number" id="m-year" value="2025">
      </div>
      <div class="form-group">
        <label id="t-mo-staff">Focus Staff <span class="my">/ ဝန်ထမ်း</span></label>
        <select id="m-staff">
          <option value="ALL">All Staff / ဝန်ထမ်းအားလုံး</option>
          <option value="Phyo Thiha Kyaw">Phyo Thiha Kyaw</option>
          <option value="Tay Zar">Tay Zar</option>
          <option value="Daw Pan Ei Phyu">Daw Pan Ei Phyu</option>
          <option value="Daw Shune Yati Hmue">Daw Shune Yati Hmue</option>
          <option value="U Hein Kyaw Lin">U Hein Kyaw Lin</option>
          <option value="U San Lin Naing">U San Lin Naing</option>
          <option value="U Kyaw Soe Lwin">U Kyaw Soe Lwin</option>
          <option value="U Myo Naing">U Myo Naing</option>
        </select>
      </div>
    </div>
    <div class="form-group">
      <label id="t-mo-ach">Key Achievements <span class="my">/ အဓိကအောင်မြင်မှုများ</span></label>
      <textarea id="m-achievements" placeholder="Major achievements this month..."></textarea>
    </div>
    <div class="form-row">
      <div class="form-group">
        <label id="t-mo-iss">Issues & Resolutions <span class="my">/ ပြဿနာနှင့်ဖြေရှင်းချက်</span></label>
        <textarea id="m-issues" placeholder="Issues encountered and resolved..."></textarea>
      </div>
      <div class="form-group">
        <label id="t-mo-next">Next Month Plan <span class="my">/ နောက်လ အစီအစဥ်</span></label>
        <textarea id="m-nextplan" placeholder="Planned activities..."></textarea>
      </div>
    </div>
    <div class="form-group">
      <label id="t-mo-rec">Recommendations to PMO <span class="my">/ PMO သို့ အကြံပြုချက်</span></label>
      <textarea id="m-recommendations" placeholder="Recommendations..."></textarea>
    </div>
    <hr>
    <div class="flex flex-gap je">
      <button class="btn btn-outline" onclick="previewMonthly()" id="t-mo-prev">👁 Preview</button>
      <button class="btn btn-purple" onclick="aiMonthlyAnalysis()" id="t-mo-ai">🤖 Auto AI Analysis</button>
      <button class="btn btn-success" onclick="submitMonthly()" id="t-mo-save">💾 Save Report</button>
    </div>
  </div>
  <div id="monthly-preview-wrap" style="display:none;margin-top:20px">
    <div class="card">
      <div class="flex jb ai-c mb16">
        <div class="card-title">MONTHLY REPORT PREVIEW</div>
        <div class="flex-gap">
          <button class="btn btn-outline btn-sm" onclick="copyTxt('monthly-preview')">📋 Copy</button>
          <button class="btn btn-primary btn-sm" onclick="window.print()">🖨 Print</button>
        </div>
      </div>
      <div class="report-box" id="monthly-preview"></div>
    </div>
  </div>
  <div id="monthly-ai-wrap" style="display:none;margin-top:20px">
    <div class="ai-box">
      <div class="card-title" style="color:var(--accent)">🤖 AI MONTHLY ANALYSIS</div>
      <div id="monthly-ai-content"></div>
    </div>
  </div>
</div>

<!-- ══ PERFORMANCE DASHBOARD ══ -->
<div id="page-performance" class="page">
  <div class="page-header">
    <div class="flex jb ai-c">
      <div>
        <div class="page-title" id="t-perf-title">🏆 Performance Dashboard</div>
        <div class="page-sub" id="t-perf-sub">Individual staff performance metrics & rankings</div>
      </div>
      <button class="btn btn-purple btn-sm" onclick="aiTeamAnalysis()" id="t-perf-ai">🤖 AI Team Review</button>
    </div>
  </div>

  <!-- Leaderboard -->
  <div class="card mb16">
    <div class="card-title" id="t-leader">PERFORMANCE LEADERBOARD</div>
    <div id="leaderboard-list" style="display:flex;flex-direction:column;gap:8px;"></div>
  </div>

  <!-- Individual Cards -->
  <div class="card-title" id="t-indiv" style="margin-bottom:12px;">INDIVIDUAL METRICS</div>
  <div class="g2" id="staff-perf-grid"></div>

  <!-- AI Team Analysis -->
  <div id="team-ai-wrap" style="display:none;margin-top:20px">
    <div class="ai-box">
      <div class="card-title" style="color:var(--accent)">🤖 AI TEAM PERFORMANCE REVIEW</div>
      <div id="team-ai-content"></div>
    </div>
  </div>
</div>

<!-- ══ AI ANALYSIS PAGE ══ -->
<div id="page-ai-analysis" class="page">
  <div class="page-header">
    <div class="page-title" id="t-ai-title">🤖 AI Monthly Analysis Center</div>
    <div class="page-sub" id="t-ai-sub">PMO automated review — select staff and month to generate analysis</div>
  </div>
  <div class="card mb16">
    <div class="form-row3">
      <div class="form-group" style="margin-bottom:0">
        <label id="t-ai-sel-staff">Select Staff <span class="my">/ ဝန်ထမ်းရွေးပါ</span></label>
        <select id="ai-sel-staff">
          <option value="ALL">All Staff</option>
          <option value="Phyo Thiha Kyaw">Phyo Thiha Kyaw</option>
          <option value="Tay Zar">Tay Zar</option>
          <option value="Daw Pan Ei Phyu">Daw Pan Ei Phyu</option>
          <option value="Daw Shune Yati Hmue">Daw Shune Yati Hmue</option>
          <option value="U Hein Kyaw Lin">U Hein Kyaw Lin</option>
          <option value="U San Lin Naing">U San Lin Naing</option>
          <option value="U Kyaw Soe Lwin">U Kyaw Soe Lwin</option>
          <option value="U Myo Naing">U Myo Naing</option>
        </select>
      </div>
      <div class="form-group" style="margin-bottom:0">
        <label id="t-ai-sel-month">Month <span class="my">/ လ</span></label>
        <select id="ai-sel-month">
          <option>January</option><option>February</option><option>March</option>
          <option>April</option><option>May</option><option>June</option>
          <option>July</option><option>August</option><option>September</option>
          <option>October</option><option>November</option><option>December</option>
        </select>
      </div>
      <div class="form-group" style="margin-bottom:0;display:flex;align-items:flex-end">
        <button class="btn btn-purple" style="width:100%" onclick="runAIAnalysis()" id="t-run-ai">🤖 Generate Analysis</button>
      </div>
    </div>
  </div>
  <div id="ai-analysis-result"></div>
</div>

<!-- ══ RECORDS ══ -->
<div id="page-records" class="page">
  <div class="page-header">
    <div class="flex jb ai-c">
      <div>
        <div class="page-title" id="t-rec-title">🗂 Report Records</div>
        <div class="page-sub" id="t-rec-sub">All submitted daily and monthly reports</div>
      </div>
      <div class="flex-gap">
        <select id="filter-type" onchange="renderRecords()" style="width:130px;padding:8px 12px;font-size:12px">
          <option value="all">All Types</option>
          <option value="daily">Daily</option>
          <option value="monthly">Monthly</option>
        </select>
        <select id="filter-staff" onchange="renderRecords()" style="width:160px;padding:8px 12px;font-size:12px">
          <option value="all">All Staff</option>
          <option value="Phyo Thiha Kyaw">Phyo Thiha Kyaw</option>
          <option value="Tay Zar">Tay Zar</option>
          <option value="Daw Pan Ei Phyu">Daw Pan Ei Phyu</option>
          <option value="Daw Shune Yati Hmue">Daw Shune Yati Hmue</option>
          <option value="U Hein Kyaw Lin">U Hein Kyaw Lin</option>
          <option value="U San Lin Naing">U San Lin Naing</option>
          <option value="U Kyaw Soe Lwin">U Kyaw Soe Lwin</option>
          <option value="U Myo Naing">U Myo Naing</option>
        </select>
        <button class="btn btn-danger btn-sm" onclick="clearAll()">🗑 Clear All</button>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="tbl-wrap">
      <table>
        <thead><tr>
          <th id="t-r-date">Date</th><th id="t-r-type">Type</th>
          <th id="t-r-staff">Staff</th><th id="t-r-unit">Unit</th>
          <th id="t-r-prog">Progress</th><th id="t-r-score">Score</th>
          <th id="t-r-status">Status</th><th>Actions</th>
        </tr></thead>
        <tbody id="records-table"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ══ STAFF ══ -->
<div id="page-staff" class="page">
  <div class="page-header">
    <div class="page-title" id="t-staff-title">👥 Engineering Team</div>
    <div class="page-sub" id="t-staff-sub">Staff directory, roles & performance summary</div>
  </div>
  <div class="g2" id="staff-grid"></div>
</div>

</div><!-- /content -->
</div><!-- /layout -->

<!-- MODAL -->
<div class="modal-overlay" id="modal">
  <div class="modal-box">
    <div class="modal-header">
      <div style="font-weight:600;font-size:15px" id="modal-title">Report Detail</div>
      <button onclick="closeModal()" class="btn btn-outline btn-sm">✕ Close</button>
    </div>
    <div class="modal-body">
      <div class="report-box" id="modal-content"></div>
      <div id="modal-ai-wrap" style="margin-top:16px;display:none">
        <div class="ai-box">
          <div class="card-title" style="color:var(--accent)">🤖 AI REVIEW</div>
          <div id="modal-ai-content"></div>
        </div>
      </div>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
// ═══════════════════════════════════════════════
// DATA
// ═══════════════════════════════════════════════
const STAFF_LIST = [
  {id:'phyo', name:'Phyo Thiha Kyaw', role:'PMO Assistant', unit:'PMO', color:'#4f8ef7', avatar:'PT'},
  {id:'tay',  name:'Tay Zar',         role:'PMO Assistant', unit:'PMO', color:'#6366f1', avatar:'TZ'},
  {id:'pan',  name:'Daw Pan Ei Phyu', role:'Co-Unit Leader', unit:'Engineering', color:'#00d4aa', avatar:'PE'},
  {id:'shun', name:'Daw Shune Yati Hmue', role:'Co-Unit Leader', unit:'Engineering', color:'#34d399', avatar:'SY'},
  {id:'hein', name:'U Hein Kyaw Lin', role:'Engineering Supervisor', unit:'Engineering', color:'#ffd166', avatar:'HK'},
  {id:'san',  name:'U San Lin Naing', role:'Co-Unit Leader (C-1,C-2)', unit:'C-1/C-2', color:'#f78166', avatar:'SL'},
  {id:'kyaw', name:'U Kyaw Soe Lwin', role:'Machinery Supervisor', unit:'Machinery', color:'#a78bfa', avatar:'KS'},
  {id:'myo',  name:'U Myo Naing',     role:'Machinery Supervisor', unit:'Machinery', color:'#f472b6', avatar:'MN'},
];

let records = JSON.parse(localStorage.getItem('eng_pmo_v2')||'[]');
let lang = 'en';

// ═══════════════════════════════════════════════
// TRANSLATIONS
// ═══════════════════════════════════════════════
const T = {
  en:{
    logo:'Engineering PMO System', logosub:'PERFORMANCE MONITORING',
    pmo:'PMO Officer',
    'nav-main':'MAIN','nav-dash':'Dashboard','nav-daily':'Daily Report',
    'nav-monthly':'Monthly Summary','nav-analysis':'ANALYSIS',
    'nav-perf':'Performance','nav-ai':'AI Analysis',
    'nav-manage':'MANAGE','nav-rec':'Records','nav-staff':'Staff',
    'dash-title':'📊 Overview Dashboard','dash-sub':'Engineering Team — Real-time PMO Monitoring',
    's1':'Reports This Month','s1b':'Daily submissions',
    's2':'Team Performance','s2b':'Avg score / 100',
    's3':'Issues Reported','s3b':'Total open issues',
    's4':'Avg Progress','s4b':'Work completion rate',
    'staffperf':'STAFF PERFORMANCE OVERVIEW','recent':'RECENT REPORTS',
    'th-date':'Date','th-staff':'Staff','th-prog':'Progress','th-status':'Status',
    'daily-title':'📝 Daily Report','daily-sub':'Submit daily engineering activity report to PMO',
    'f-date':'Report Date','f-rep':'Submitted By','f-unit':'Unit','f-prog':'Work Progress %',
    'f-tasks':'Tasks Completed','f-issues':'Issues Encountered','f-sol':'Solutions Taken',
    'f-plan':"Tomorrow's Plan",'f-rem':'Remarks',
    'selfscore':'SELF-ASSESSMENT','qa':'Work Quality (1–10)','pa':'Punctuality (1–10)','ta':'Teamwork (1–10)',
    'btn-preview':'👁 Preview','btn-ai':'🤖 AI Analysis','btn-submit':'✅ Submit to PMO',
    'prev-head':'REPORT PREVIEW',
    'mo-title':'📅 Monthly Summary Report','mo-sub':'Auto-generate monthly performance summary for PMO',
    'mo-month':'Month','mo-staff':'Focus Staff',
    'mo-ach':'Key Achievements','mo-iss':'Issues & Resolutions',
    'mo-next':"Next Month Plan",'mo-rec':'Recommendations to PMO',
    'mo-prev':'👁 Preview','mo-ai':'🤖 Auto AI Analysis','mo-save':'💾 Save Report',
    'perf-title':'🏆 Performance Dashboard','perf-sub':'Individual staff performance metrics & rankings',
    'perf-ai':'🤖 AI Team Review','leader':'PERFORMANCE LEADERBOARD','indiv':'INDIVIDUAL METRICS',
    'ai-title':'🤖 AI Monthly Analysis Center',
    'ai-sub':'PMO automated review — select staff and month to generate analysis',
    'ai-sel-staff':'Select Staff','ai-sel-month':'Month',
    'run-ai':'🤖 Generate Analysis',
    'rec-title':'🗂 Report Records','rec-sub':'All submitted daily and monthly reports',
    'r-date':'Date','r-type':'Type','r-staff':'Staff','r-unit':'Unit',
    'r-prog':'Progress','r-score':'Score','r-status':'Status',
    'staff-title':'👥 Engineering Team','staff-sub':'Staff directory, roles & performance summary',
    'ai-daily-head':'🤖 AI ANALYSIS RESULT',
  },
  my:{
    logo:'အင်ဂျင်နီယာ PMO စနစ်', logosub:'စွမ်းဆောင်ရည် စောင့်ကြည့်ရေး',
    pmo:'PMO အရာရှိ',
    'nav-main':'အဓိက','nav-dash':'ဒက်ရှ်ဘုတ်','nav-daily':'နေ့စဥ်အစီရင်ခံစာ',
    'nav-monthly':'လစဥ်အကျဉ်းချုပ်','nav-analysis':'ခွဲခြမ်းစိတ်ဖြာမှု',
    'nav-perf':'စွမ်းဆောင်ရည်','nav-ai':'AI ခွဲခြမ်းစိတ်ဖြာ',
    'nav-manage':'စီမံခန့်ခွဲမှု','nav-rec':'မှတ်တမ်းများ','nav-staff':'ဝန်ထမ်းများ',
    'dash-title':'📊 ခြုံငုံသုံးသပ်မှု ဒက်ရှ်ဘုတ်','dash-sub':'အင်ဂျင်နီယာအဖွဲ့ — PMO အချိန်နှင့်တပြေးညီ စောင့်ကြည့်မှု',
    's1':'ဤလ အစီရင်ခံစာ','s1b':'နေ့စဥ် တင်သွင်းမှု',
    's2':'အဖွဲ့ စွမ်းဆောင်ရည်','s2b':'ပျမ်းမျှ ရမှတ် / ၁၀၀',
    's3':'တင်ပြသောပြဿနာ','s3b':'ဖွင့်ထားသောပြဿနာ စုစုပေါင်း',
    's4':'ပျမ်းမျှ တိုးတက်မှု','s4b':'လုပ်ငန်းပြီးစီးနှုန်း',
    'staffperf':'ဝန်ထမ်းစွမ်းဆောင်ရည် ခြုံငုံမှု','recent':'နောက်ဆုံးအစီရင်ခံစာများ',
    'th-date':'နေ့စွဲ','th-staff':'ဝန်ထမ်း','th-prog':'တိုးတက်မှု','th-status':'အခြေအနေ',
    'daily-title':'📝 နေ့စဥ်အစီရင်ခံစာ','daily-sub':'နေ့စဥ် လုပ်ငန်းဆောင်တာများကို PMO သို့ တင်သွင်းပါ',
    'f-date':'အစီရင်ခံသည့်ရက်','f-rep':'တင်သွင်းသူ','f-unit':'တပ်ဖွဲ့','f-prog':'လုပ်ငန်းတိုးတက်မှု %',
    'f-tasks':'ပြီးစီးသောလုပ်ငန်းများ','f-issues':'ကြုံတွေ့ပြဿနာများ','f-sol':'ဖြေရှင်းချက်များ',
    'f-plan':'မနက်ဖြန် အစီအစဥ်','f-rem':'မှတ်ချက်',
    'selfscore':'ကိုယ်တိုင် အကဲဖြတ်ချက်','qa':'လုပ်ငန်းအရည်အသွေး (၁–၁၀)','pa':'အချိန်တိကျမှု (၁–၁၀)','ta':'အဖွဲ့လုပ်ဆောင်မှု (၁–၁၀)',
    'btn-preview':'👁 ကြိုကြည့်','btn-ai':'🤖 AI ခွဲခြမ်း','btn-submit':'✅ PMO သို့ တင်သွင်း',
    'prev-head':'အစီရင်ခံစာ ကြိုကြည့်မှု',
    'mo-title':'📅 လစဥ် အကျဉ်းချုပ်အစီရင်ခံစာ','mo-sub':'PMO အတွက် လစဥ် စွမ်းဆောင်ရည် အကျဉ်းချုပ်ကို အလိုအလျောက် ထုတ်လုပ်ပါ',
    'mo-month':'လ','mo-staff':'အာရုံစိုက်မည့် ဝန်ထမ်း',
    'mo-ach':'အဓိကအောင်မြင်မှုများ','mo-iss':'ပြဿနာနှင့်ဖြေရှင်းချက်',
    'mo-next':'နောက်လ အစီအစဥ်','mo-rec':'PMO သို့ အကြံပြုချက်',
    'mo-prev':'👁 ကြိုကြည့်','mo-ai':'🤖 AI အလိုအလျောက် ခွဲခြမ်း','mo-save':'💾 သိမ်းဆည်း',
    'perf-title':'🏆 စွမ်းဆောင်ရည် ဒက်ရှ်ဘုတ်','perf-sub':'ဝန်ထမ်းတစ်ဦးချင်းစီ၏ စွမ်းဆောင်ရည် မက်ထရစ်နှင့် အဆင့်သတ်မှတ်မှု',
    'perf-ai':'🤖 AI အဖွဲ့ စစ်ဆေးမှု','leader':'စွမ်းဆောင်ရည် အဆင့်ကြည့်','indiv':'တစ်ဦးချင်း မက်ထရစ်',
    'ai-title':'🤖 AI လစဥ် ခွဲခြမ်းစိတ်ဖြာ ဗဟိုဌာန',
    'ai-sub':'PMO အလိုအလျောက် စစ်ဆေးမှု — ဝန်ထမ်းနှင့် လကို ရွေးပြီး ခွဲခြမ်းစိတ်ဖြာချက် ထုတ်လုပ်ပါ',
    'ai-sel-staff':'ဝန်ထမ်းရွေးပါ','ai-sel-month':'လ',
    'run-ai':'🤖 ခွဲခြမ်းစိတ်ဖြာချက် ထုတ်လုပ်',
    'rec-title':'🗂 အစီရင်ခံစာ မှတ်တမ်းများ','rec-sub':'တင်သွင်းထားသော နေ့စဥ်နှင့် လစဥ် အစီရင်ခံစာများ အားလုံး',
    'r-date':'နေ့စွဲ','r-type':'အမျိုးအစား','r-staff':'ဝန်ထမ်း','r-unit':'တပ်ဖွဲ့',
    'r-prog':'တိုးတက်မှု','r-score':'ရမှတ်','r-status':'အခြေအနေ',
    'staff-title':'👥 အင်ဂျင်နီယာအဖွဲ့','staff-sub':'ဝန်ထမ်းစာရင်း၊ ရာထူးများနှင့် စွမ်းဆောင်ရည် အကျဉ်းချုပ်',
    'ai-daily-head':'🤖 AI ခွဲခြမ်းစိတ်ဖြာချက် ရလဒ်',
  }
};

function setLang(l){
  lang=l;
  document.querySelectorAll('.lang-btn').forEach(b=>{
    b.classList.toggle('active',b.textContent.trim().toLowerCase()===l||(l==='my'&&b.textContent.includes('မ')));
  });
  const t=T[l];
  for(const[k,v] of Object.entries(t)){
    const el=document.getElementById('t-'+k);
    if(el) el.textContent=v;
  }
}

// ═══════════════════════════════════════════════
// CLOCK
// ═══════════════════════════════════════════════
function updateClock(){
  const n=new Date();
  document.getElementById('clock').textContent=
    n.toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'})+
    ' '+n.toLocaleTimeString();
}
setInterval(updateClock,1000);updateClock();

// ═══════════════════════════════════════════════
// NAVIGATION
// ═══════════════════════════════════════════════
function nav(page){
  document.querySelectorAll('.nav-item').forEach(el=>el.classList.remove('active'));
  const pages=['dashboard','daily','monthly','performance','ai-analysis','records','staff'];
  const navs=document.querySelectorAll('.nav-item');
  const idx=pages.indexOf(page);
  if(idx>=0&&navs[idx]) navs[idx].classList.add('active');
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const pg=document.getElementById('page-'+page);
  if(pg) pg.classList.add('active');
  if(page==='performance') renderPerformance();
  if(page==='records') renderRecords();
  if(page==='dashboard') renderDashboard();
}

// ═══════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════
document.addEventListener('DOMContentLoaded',()=>{
  const now=new Date();
  const d=document.getElementById('d-date');
  if(d) d.value=now.toISOString().split('T')[0];
  const months=['January','February','March','April','May','June','July','August','September','October','November','December'];
  const mm=document.getElementById('m-month');
  if(mm) mm.value=months[now.getMonth()];
  const mmo=document.getElementById('ai-sel-month');
  if(mmo) mmo.value=months[now.getMonth()];
  const my=document.getElementById('m-year');
  if(my) my.value=now.getFullYear();
  renderStaff();
  renderDashboard();
  renderPerformance();
});

// ═══════════════════════════════════════════════
// HELPERS
// ═══════════════════════════════════════════════
const gv=id=>(document.getElementById(id)||{}).value||'';

function scoreColor(s){
  if(s>=80) return 'var(--accent2)';
  if(s>=60) return 'var(--accent4)';
  if(s>=40) return 'var(--accent)';
  return 'var(--accent3)';
}
function scorePill(s){
  if(s>=80) return 'pill-green';
  if(s>=60) return 'pill-yellow';
  return 'pill-red';
}
function gradeLabel(s){
  if(s>=90) return lang==='my'?'ထူးချွန်':'Excellent';
  if(s>=80) return lang==='my'?'ကောင်းမွန်':'Very Good';
  if(s>=70) return lang==='my'?'ကောင်း':'Good';
  if(s>=60) return lang==='my'?'သင့်တင့်':'Fair';
  return lang==='my'?'ပိုမိုကြိုးစားရန်':'Needs Improvement';
}

function calcStaffScore(staffName){
  const recs=records.filter(r=>r.reporter===staffName&&r.type==='daily');
  if(!recs.length) return null;
  const prog=recs.map(r=>parseInt(r.progress||50)).reduce((a,b)=>a+b,0)/recs.length;
  const qual=recs.map(r=>parseInt(r.quality||5)).reduce((a,b)=>a+b,0)/recs.length;
  const punc=recs.map(r=>parseInt(r.punctuality||5)).reduce((a,b)=>a+b,0)/recs.length;
  const team=recs.map(r=>parseInt(r.teamwork||5)).reduce((a,b)=>a+b,0)/recs.length;
  const issues=recs.filter(r=>r.issues&&r.issues.trim()).length;
  const issueDeduct=Math.min(issues*2,15);
  const score=Math.round((prog*0.4)+(qual*10*0.25)+(punc*10*0.2)+(team*10*0.15)-issueDeduct);
  return {score:Math.min(100,Math.max(0,score)),count:recs.length,prog:Math.round(prog),qual:Math.round(qual*10),punc:Math.round(punc*10),team:Math.round(team*10),issues};
}

// ═══════════════════════════════════════════════
// RENDER STAFF PAGE
// ═══════════════════════════════════════════════
function renderStaff(){
  const grid=document.getElementById('staff-grid');
  if(!grid) return;
  grid.innerHTML=STAFF_LIST.map(s=>{
    const sc=calcStaffScore(s.name);
    const score=sc?sc.score:null;
    return `
    <div class="card" style="border-color:${s.color}33">
      <div style="display:flex;gap:16px;align-items:flex-start">
        <div style="width:52px;height:52px;border-radius:12px;background:${s.color}22;color:${s.color};display:flex;align-items:center;justify-content:center;font-size:17px;font-weight:700;flex-shrink:0">${s.avatar}</div>
        <div style="flex:1">
          <div style="font-size:14px;font-weight:700;color:var(--text)">${s.name}</div>
          <div style="font-size:12px;color:var(--text2);margin-top:3px">${s.role}</div>
          <div style="margin-top:6px"><span class="pill" style="background:${s.color}18;color:${s.color};border:1px solid ${s.color}44;font-size:10px">${s.unit}</span></div>
        </div>
        ${score!==null?`<div style="width:52px;height:52px;border-radius:10px;background:${scoreColor(score)}18;color:${scoreColor(score)};display:flex;align-items:center;justify-content:center;font-size:18px;font-weight:800;flex-shrink:0">${score}</div>`:''}
      </div>
      ${sc?`
      <div style="margin-top:14px;display:grid;grid-template-columns:1fr 1fr;gap:8px">
        <div><div style="font-size:10px;color:var(--text3);margin-bottom:4px">${lang==='my'?'တိုးတက်မှု':'Progress'}</div><div class="prog-bar"><div class="prog-fill" style="width:${sc.prog}%;background:${s.color}"></div></div><div style="font-size:11px;color:var(--text2);margin-top:3px">${sc.prog}%</div></div>
        <div><div style="font-size:10px;color:var(--text3);margin-bottom:4px">${lang==='my'?'အရည်အသွေး':'Quality'}</div><div class="prog-bar"><div class="prog-fill" style="width:${sc.qual}%;background:var(--accent2)"></div></div><div style="font-size:11px;color:var(--text2);margin-top:3px">${sc.qual}%</div></div>
      </div>
      <div style="margin-top:10px;display:flex;gap:8px;flex-wrap:wrap">
        <span class="metric-chip">${sc.count} ${lang==='my'?'ရက်':'days'}</span>
        <span class="metric-chip">⚠ ${sc.issues}</span>
        <span class="pill ${scorePill(score)}" style="font-size:10px">${gradeLabel(score)}</span>
      </div>`:
      `<div style="margin-top:12px;font-size:12px;color:var(--text3)">${lang==='my'?'မှတ်တမ်းမရှိသေးပါ':'No reports yet'}</div>`}
    </div>`;
  }).join('');
}

// ═══════════════════════════════════════════════
// RENDER DASHBOARD
// ═══════════════════════════════════════════════
function renderDashboard(){
  const now=new Date();
  const thisMonthRecs=records.filter(r=>{
    const d=new Date(r.date||r.id);
    return d.getMonth()===now.getMonth()&&d.getFullYear()===now.getFullYear()&&r.type==='daily';
  });
  const total=thisMonthRecs.length;
  document.getElementById('s-reports').textContent=total;
  document.getElementById('sb-reports').style.width=Math.min(total*4,100)+'%';

  const scores=STAFF_LIST.map(s=>calcStaffScore(s.name)).filter(Boolean);
  const avgScore=scores.length?Math.round(scores.reduce((a,b)=>a+b.score,0)/scores.length):null;
  document.getElementById('s-perf').textContent=avgScore!==null?avgScore+'':'—';
  document.getElementById('sb-perf').style.width=(avgScore||0)+'%';

  const issues=records.reduce((a,r)=>a+(r.issues&&r.issues.trim()?1:0),0);
  document.getElementById('s-issues').textContent=issues;
  document.getElementById('sb-issues').style.width=Math.min(issues*5,100)+'%';

  const progs=records.filter(r=>r.progress).map(r=>parseInt(r.progress));
  const avgProg=progs.length?Math.round(progs.reduce((a,b)=>a+b,0)/progs.length):null;
  document.getElementById('s-progress').textContent=avgProg!==null?avgProg+'%':'—';
  document.getElementById('sb-progress').style.width=(avgProg||0)+'%';

  // Staff overview
  const sl=document.getElementById('dash-staff-list');
  if(sl){
    sl.innerHTML=STAFF_LIST.map(s=>{
      const sc=calcStaffScore(s.name);
      return `<div style="display:flex;align-items:center;gap:10px;padding:6px 0;border-bottom:1px solid var(--border)">
        <div style="width:8px;height:8px;border-radius:50%;background:${s.color};flex-shrink:0"></div>
        <div style="flex:1;font-size:12px;font-weight:500">${s.name}</div>
        <div style="font-size:11px;color:var(--text2)">${s.role.split(' ')[0]}</div>
        ${sc?`<span class="pill ${scorePill(sc.score)}" style="font-size:10px">${sc.score}</span>`:
        '<span style="font-size:10px;color:var(--text3)">—</span>'}
      </div>`;
    }).join('');
  }

  // Recent table
  const tbody=document.getElementById('dash-recent');
  if(tbody){
    const recent=[...records].reverse().slice(0,6);
    if(!recent.length){
      tbody.innerHTML=`<tr><td colspan="4" style="text-align:center;padding:24px;color:var(--text3)">${lang==='my'?'မှတ်တမ်းမရှိသေးပါ':'No reports yet'}</td></tr>`;
    } else {
      tbody.innerHTML=recent.map(r=>`
        <tr>
          <td style="font-size:12px;font-family:'Courier New',monospace">${r.date||'—'}</td>
          <td style="font-size:12px">${r.reporter?r.reporter.split('(')[0].trim():'—'}</td>
          <td>${r.progress?`<div style="min-width:60px"><div style="font-size:11px;margin-bottom:3px">${r.progress}%</div><div class="prog-bar"><div class="prog-fill" style="width:${r.progress}%;background:var(--accent2)"></div></div></div>`:'-'}</td>
          <td><span class="pill ${r.status==='Submitted'?'pill-green':'pill-yellow'}">${r.status}</span></td>
        </tr>`).join('');
    }
  }
}

// ═══════════════════════════════════════════════
// PERFORMANCE PAGE
// ═══════════════════════════════════════════════
function renderPerformance(){
  // Leaderboard
  const lb=document.getElementById('leaderboard-list');
  if(lb){
    const ranked=STAFF_LIST.map(s=>({...s,sc:calcStaffScore(s.name)})).sort((a,b)=>(b.sc?b.sc.score:0)-(a.sc?a.sc.score:0));
    lb.innerHTML=ranked.map((s,i)=>{
      const sc=s.sc;
      const medals=['🥇','🥈','🥉'];
      return `<div style="display:flex;align-items:center;gap:14px;padding:12px 14px;background:var(--bg3);border-radius:8px;border:1px solid ${i===0?s.color+'44':'var(--border)'}">
        <div style="font-size:20px;width:28px;text-align:center">${medals[i]||'#'+(i+1)}</div>
        <div style="width:36px;height:36px;border-radius:8px;background:${s.color}22;color:${s.color};display:flex;align-items:center;justify-content:center;font-weight:700;font-size:13px;flex-shrink:0">${s.avatar}</div>
        <div style="flex:1">
          <div style="font-size:13px;font-weight:600">${s.name}</div>
          <div style="font-size:11px;color:var(--text2)">${s.role}</div>
        </div>
        ${sc?`
        <div style="text-align:right">
          <div style="font-size:22px;font-weight:800;color:${scoreColor(sc.score)}">${sc.score}</div>
          <div style="font-size:10px;color:var(--text2)">${sc.count} ${lang==='my'?'ရက်':'days'}</div>
        </div>
        <div style="width:80px">
          <div class="prog-bar"><div class="prog-fill" style="width:${sc.score}%;background:${scoreColor(sc.score)}"></div></div>
          <div style="font-size:10px;color:var(--text2);margin-top:3px">${gradeLabel(sc.score)}</div>
        </div>`:
        `<div style="font-size:12px;color:var(--text3)">${lang==='my'?'မှတ်တမ်းမရှိ':'No data'}</div>`}
      </div>`;
    }).join('');
  }

  // Individual cards
  const grid=document.getElementById('staff-perf-grid');
  if(grid){
    grid.innerHTML=STAFF_LIST.map(s=>{
      const sc=calcStaffScore(s.name);
      const metrics=[
        {label:lang==='my'?'တိုးတက်မှု':'Progress',val:sc?sc.prog:0,color:s.color},
        {label:lang==='my'?'အရည်အသွေး':'Quality',val:sc?sc.qual:0,color:'var(--accent2)'},
        {label:lang==='my'?'အချိန်တိကျမှု':'Punctuality',val:sc?sc.punc:0,color:'var(--accent4)'},
        {label:lang==='my'?'အဖွဲ့လုပ်ဆောင်':'Teamwork',val:sc?sc.team:0,color:'var(--accent5)'},
      ];
      return `<div class="card" onclick="openStaffModal('${s.name}')" style="cursor:pointer;border-color:${s.color}22">
        <div style="display:flex;align-items:center;gap:12px;margin-bottom:14px">
          <div style="width:42px;height:42px;border-radius:10px;background:${s.color}22;color:${s.color};display:flex;align-items:center;justify-content:center;font-weight:700;font-size:15px">${s.avatar}</div>
          <div style="flex:1">
            <div style="font-size:13px;font-weight:600">${s.name}</div>
            <div style="font-size:11px;color:var(--text2)">${s.role}</div>
          </div>
          ${sc?`<div style="font-size:24px;font-weight:800;color:${scoreColor(sc.score)}">${sc.score}</div>`:
          `<div style="font-size:13px;color:var(--text3)">—</div>`}
        </div>
        ${metrics.map(m=>`
          <div style="margin-bottom:8px">
            <div style="display:flex;justify-content:space-between;margin-bottom:3px">
              <span style="font-size:11px;color:var(--text2)">${m.label}</span>
              <span style="font-size:11px;font-weight:600;color:${m.color}">${m.val}%</span>
            </div>
            <div class="prog-bar"><div class="prog-fill" style="width:${m.val}%;background:${m.color}"></div></div>
          </div>`).join('')}
        ${sc?`<div style="margin-top:10px;display:flex;gap:6px;flex-wrap:wrap">
          <span class="metric-chip">${sc.count} ${lang==='my'?'ရက်':'reports'}</span>
          <span class="metric-chip">⚠ ${sc.issues} ${lang==='my'?'ပြဿနာ':'issues'}</span>
          <span class="pill ${scorePill(sc.score)}" style="font-size:10px">${gradeLabel(sc.score)}</span>
        </div>`:
        `<div style="font-size:12px;color:var(--text3);margin-top:8px">${lang==='my'?'မှတ်တမ်းမရှိသေးပါ':'No records yet'}</div>`}
      </div>`;
    }).join('');
  }
}

// ═══════════════════════════════════════════════
// DAILY REPORT
// ═══════════════════════════════════════════════
function buildDailyText(){
  const d=gv('d-date'),rep=gv('d-reporter'),unit=gv('d-unit'),prog=gv('d-progress'),
    tasks=gv('d-tasks'),ong=gv('d-ongoing')||'—',issues=gv('d-issues'),sol=gv('d-solutions'),
    plan=gv('d-plan'),rem=gv('d-remarks'),qual=gv('d-quality'),punc=gv('d-punctuality'),team=gv('d-teamwork');
  const now=new Date().toLocaleString();
  if(lang==='my'){
    return `<span class="r-h">══════════════════════════════════════════════
  အင်ဂျင်နီယာအဖွဲ့ — နေ့စဥ်အစီရင်ခံစာ
  PMO စောင့်ကြည့်ရေးစနစ်
══════════════════════════════════════════════</span>

<span class="r-l">အစီရင်ခံသည့်ရက်   :</span> <span class="r-v">${d}</span>
<span class="r-l">ထုတ်ပေးသောအချိန်  :</span> <span class="r-v">${now}</span>
<span class="r-l">တင်သွင်းသူ        :</span> <span class="r-v">${rep}</span>
<span class="r-l">တပ်ဖွဲ့           :</span> <span class="r-v">${unit}</span>
<span class="r-l">လုပ်ငန်းတိုးတက်မှု :</span> <span class="r-v">${prog?prog+'%':'မဖြည့်သွင်းရသေး'}</span>

──────────────────────────────────────────────
<span class="r-h">၁. ပြီးစီးသောလုပ်ငန်းများ</span>
──────────────────────────────────────────────
<span class="r-v">${tasks||'(ထည့်သွင်းမထားပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">၂. ကြုံတွေ့ပြဿနာများ</span>
──────────────────────────────────────────────
<span class="r-v">${issues||'(မရှိပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">၃. ဖြေရှင်းချက်များ</span>
──────────────────────────────────────────────
<span class="r-v">${sol||'(မရှိပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">၄. မနက်ဖြန် အစီအစဥ်</span>
──────────────────────────────────────────────
<span class="r-v">${plan||'(ထည့်သွင်းမထားပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">၅. ကိုယ်တိုင်အကဲဖြတ်ချက်</span>
──────────────────────────────────────────────
<span class="r-l">လုပ်ငန်းအရည်အသွေး :</span> <span class="r-v">${qual||'—'} / ၁၀</span>
<span class="r-l">အချိန်တိကျမှု     :</span> <span class="r-v">${punc||'—'} / ၁၀</span>
<span class="r-l">အဖွဲ့လုပ်ဆောင်မှု  :</span> <span class="r-v">${team||'—'} / ၁၀</span>

──────────────────────────────────────────────
<span class="r-h">မှတ်ချက်</span>
──────────────────────────────────────────────
<span class="r-v">${rem||'(မရှိပါ)'}</span>

══════════════════════════════════════════════
<span class="r-l">လက်မှတ်  :</span> <span class="r-v">${rep}</span>
<span class="r-l">တင်ပြသည် :</span> <span class="r-v">PMO (အင်ဂျင်နီယာအဖွဲ့)</span>
══════════════════════════════════════════════`;
  }
  return `<span class="r-h">══════════════════════════════════════════════
  ENGINEERING TEAM — DAILY REPORT
  PMO MONITORING SYSTEM
══════════════════════════════════════════════</span>

<span class="r-l">Report Date   :</span> <span class="r-v">${d}</span>
<span class="r-l">Generated     :</span> <span class="r-v">${now}</span>
<span class="r-l">Submitted By  :</span> <span class="r-v">${rep}</span>
<span class="r-l">Unit          :</span> <span class="r-v">${unit}</span>
<span class="r-l">Progress      :</span> <span class="r-v">${prog?prog+'%':'N/A'}</span>

──────────────────────────────────────────────
<span class="r-h">1. TASKS COMPLETED</span>
──────────────────────────────────────────────
<span class="r-v">${tasks||'(none entered)'}</span>

──────────────────────────────────────────────
<span class="r-h">2. ISSUES ENCOUNTERED</span>
──────────────────────────────────────────────
<span class="r-v">${issues||'(none)'}</span>

──────────────────────────────────────────────
<span class="r-h">3. SOLUTIONS TAKEN</span>
──────────────────────────────────────────────
<span class="r-v">${sol||'(none)'}</span>

──────────────────────────────────────────────
<span class="r-h">4. TOMORROW'S PLAN</span>
──────────────────────────────────────────────
<span class="r-v">${plan||'(none entered)'}</span>

──────────────────────────────────────────────
<span class="r-h">5. SELF-ASSESSMENT</span>
──────────────────────────────────────────────
<span class="r-l">Work Quality  :</span> <span class="r-v">${qual||'—'} / 10</span>
<span class="r-l">Punctuality   :</span> <span class="r-v">${punc||'—'} / 10</span>
<span class="r-l">Teamwork      :</span> <span class="r-v">${team||'—'} / 10</span>

──────────────────────────────────────────────
<span class="r-h">6. REMARKS</span>
──────────────────────────────────────────────
<span class="r-v">${rem||'(none)'}</span>

══════════════════════════════════════════════
<span class="r-l">Signature :</span> <span class="r-v">${rep}</span>
<span class="r-l">Report To :</span> <span class="r-v">PMO (Engineering Team)</span>
══════════════════════════════════════════════`;
}

function previewDaily(){
  document.getElementById('daily-preview').innerHTML=buildDailyText();
  document.getElementById('daily-preview-wrap').style.display='block';
  document.getElementById('daily-preview-wrap').scrollIntoView({behavior:'smooth'});
}

function submitDaily(){
  const d=gv('d-date'),rep=gv('d-reporter'),unit=gv('d-unit');
  if(!d||!rep||!unit){showToast(lang==='my'?'ရက်စွဲ၊ ဝန်ထမ်းနှင့် တပ်ဖွဲ့ ဖြည့်ပါ':'Please fill Date, Reporter and Unit.','var(--accent3)');return;}
  const record={
    id:Date.now(),type:'daily',date:d,reporter:rep,unit,
    progress:gv('d-progress'),tasks:gv('d-tasks'),ongoing:gv('d-ongoing'),
    issues:gv('d-issues'),solutions:gv('d-solutions'),plan:gv('d-plan'),
    remarks:gv('d-remarks'),quality:gv('d-quality'),punctuality:gv('d-punctuality'),
    teamwork:gv('d-teamwork'),status:'Submitted',rawText:buildDailyText().replace(/<[^>]+>/g,'')
  };
  records.push(record);
  save();renderDashboard();renderPerformance();renderStaff();
  showToast(lang==='my'?'PMO သို့ နေ့စဥ်အစီရင်ခံစာ တင်သွင်းပြီးပါပြီ!':'Daily report submitted to PMO!');
  previewDaily();
  document.getElementById('pending-badge').style.display='none';
}

// ═══════════════════════════════════════════════
// AI ANALYSIS — DAILY
// ═══════════════════════════════════════════════
async function aiAnalyzeDaily(){
  const rep=gv('d-reporter'),tasks=gv('d-tasks'),issues=gv('d-issues'),
    prog=gv('d-progress'),qual=gv('d-quality'),punc=gv('d-punctuality'),team=gv('d-teamwork'),plan=gv('d-plan');
  if(!rep){showToast(lang==='my'?'ဝန်ထမ်းနှင့် လုပ်ငန်းများ ဖြည့်ပါ':'Please fill reporter and tasks first','var(--accent3)');return;}
  const wrap=document.getElementById('daily-ai-wrap');
  const content=document.getElementById('daily-ai-content');
  wrap.style.display='block';
  content.innerHTML=`<div class="ai-loading"><div class="ai-dots"><span></span><span></span><span></span></div> ${lang==='my'?'AI ခွဲခြမ်းစိတ်ဖြာနေသည်...':'AI is analyzing...'}</div>`;
  wrap.scrollIntoView({behavior:'smooth'});

  const prompt = lang==='my'?
  `သင်သည် PMO (Project Management Office) ၏ AI ခွဲခြမ်းစိတ်ဖြာပေးသူဖြစ်သည်။ မြန်မာဘာသာဖြင့် ဖြေပါ။
  
  ဝန်ထမ်း: ${rep}
  လုပ်ငန်းတိုးတက်မှု: ${prog}%
  ပြီးစီးသောလုပ်ငန်းများ: ${tasks}
  ကြုံတွေ့ပြဿနာ: ${issues||'မရှိပါ'}
  အရည်အသွေးအဆင့်(ကိုယ်တိုင်): ${qual}/10
  အချိန်တိကျမှု(ကိုယ်တိုင်): ${punc}/10
  အဖွဲ့လုပ်ဆောင်မှု(ကိုယ်တိုင်): ${team}/10
  မနက်ဖြန်အစီအစဥ်: ${plan||'—'}
  
  PMO အနေနဲ့ ဤနေ့စဥ်အစီရင်ခံစာကို စစ်ဆေးပြီး:
  1. လုပ်ငန်းဆောင်တာ ခြုံငုံသုံးသပ်ချက်
  2. ပြဿနာများနှင့် အကြံပြုချက်
  3. ရမှတ် (100 အနက်မှ) နှင့် အဆင့်
  4. နောက်ရက် လုပ်ဆောင်ရန် အကြံပြုချက်
  တို့ကို ရေးသားပေးပါ။`:
  `You are a PMO AI analyst for an Engineering team in Myanmar. Analyze this daily report and respond in English.
  
  Staff: ${rep}
  Progress: ${prog}%
  Tasks Done: ${tasks}
  Issues: ${issues||'None'}
  Self-Quality: ${qual}/10, Punctuality: ${punc}/10, Teamwork: ${team}/10
  Tomorrow Plan: ${plan||'—'}
  
  As PMO officer, provide:
  1. Work performance summary
  2. Issues & recommendations
  3. Performance score (/100) with grade
  4. Suggestions for next day
  Be concise and constructive.`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':'','anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    const txt=data.content?.[0]?.text||'Analysis failed.';
    content.innerHTML=`<div class="ai-result">${txt}</div>`;
  }catch(e){
    content.innerHTML=`<div class="ai-result" style="color:var(--accent3)">Error: ${e.message}</div>`;
  }
}

// ═══════════════════════════════════════════════
// MONTHLY PREVIEW & SUBMIT
// ═══════════════════════════════════════════════
function buildMonthlyText(){
  const mon=gv('m-month'),yr=gv('m-year'),staff=gv('m-staff'),
    ach=gv('m-achievements'),iss=gv('m-issues'),next=gv('m-nextplan'),rec=gv('m-recommendations');
  const now=new Date().toLocaleString();
  const staffRecs=records.filter(r=>r.type==='daily'&&(staff==='ALL'||r.reporter===staff)&&r.date&&r.date.includes(yr));
  const avgProg=staffRecs.length?Math.round(staffRecs.reduce((a,r)=>a+parseInt(r.progress||50),0)/staffRecs.length):0;
  const issueCount=staffRecs.filter(r=>r.issues&&r.issues.trim()).length;

  if(lang==='my'){
    return `<span class="r-h">══════════════════════════════════════════════
  အင်ဂျင်နီယာအဖွဲ့ — လစဥ် အကျဉ်းချုပ်အစီရင်ခံစာ
  ${mon} ${yr} | PMO စောင့်ကြည့်ရေးစနစ်
══════════════════════════════════════════════</span>

<span class="r-l">အစီရင်ခံကာလ     :</span> <span class="r-v">${mon} ${yr}</span>
<span class="r-l">ထုတ်ပေးသောအချိန် :</span> <span class="r-v">${now}</span>
<span class="r-l">ဝန်ထမ်း         :</span> <span class="r-v">${staff==='ALL'?'ဝန်ထမ်းအားလုံး':staff}</span>
<span class="r-l">ပျမ်းမျှတိုးတက်မှု:</span> <span class="r-v">${avgProg}%</span>
<span class="r-l">တင်သွင်းသောရက်   :</span> <span class="r-v">${staffRecs.length} ရက်</span>
<span class="r-l">ပြဿနာကြုံတွေ့မှု :</span> <span class="r-v">${issueCount} ကြိမ်</span>

──────────────────────────────────────────────
<span class="r-h">က. အဓိကအောင်မြင်မှုများ</span>
──────────────────────────────────────────────
<span class="r-v">${ach||'(ထည့်သွင်းမထားပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">ခ. ပြဿနာများနှင့် ဖြေရှင်းချက်</span>
──────────────────────────────────────────────
<span class="r-v">${iss||'(မရှိပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">ဂ. နောက်လ အစီအစဥ်</span>
──────────────────────────────────────────────
<span class="r-v">${next||'(ထည့်သွင်းမထားပါ)'}</span>

──────────────────────────────────────────────
<span class="r-h">ဃ. PMO သို့ အကြံပြုချက်</span>
──────────────────────────────────────────────
<span class="r-v">${rec||'(မရှိပါ)'}</span>

══════════════════════════════════════════════
<span class="r-l">တင်ပြသည် :</span> <span class="r-v">PMO (အင်ဂျင်နီယာအဖွဲ့)</span>
══════════════════════════════════════════════`;
  }
  return `<span class="r-h">══════════════════════════════════════════════
  ENGINEERING TEAM — MONTHLY SUMMARY REPORT
  ${mon.toUpperCase()} ${yr} | PMO MONITORING SYSTEM
══════════════════════════════════════════════</span>

<span class="r-l">Period       :</span> <span class="r-v">${mon} ${yr}</span>
<span class="r-l">Generated    :</span> <span class="r-v">${now}</span>
<span class="r-l">Staff        :</span> <span class="r-v">${staff==='ALL'?'All Staff':staff}</span>
<span class="r-l">Avg Progress :</span> <span class="r-v">${avgProg}%</span>
<span class="r-l">Days Reported:</span> <span class="r-v">${staffRecs.length} days</span>
<span class="r-l">Issue Count  :</span> <span class="r-v">${issueCount}</span>

──────────────────────────────────────────────
<span class="r-h">A. KEY ACHIEVEMENTS</span>
──────────────────────────────────────────────
<span class="r-v">${ach||'(not provided)'}</span>

──────────────────────────────────────────────
<span class="r-h">B. ISSUES & RESOLUTIONS</span>
──────────────────────────────────────────────
<span class="r-v">${iss||'(none)'}</span>

──────────────────────────────────────────────
<span class="r-h">C. NEXT MONTH PLAN</span>
──────────────────────────────────────────────
<span class="r-v">${next||'(not provided)'}</span>

──────────────────────────────────────────────
<span class="r-h">D. RECOMMENDATIONS TO PMO</span>
──────────────────────────────────────────────
<span class="r-v">${rec||'(none)'}</span>

══════════════════════════════════════════════
<span class="r-l">Report To    :</span> <span class="r-v">PMO (Engineering Team)</span>
<span class="r-l">Co-Leaders   :</span> <span class="r-v">Daw Pan Ei Phyu / Daw Shune Yati Hmue</span>
══════════════════════════════════════════════`;
}

function previewMonthly(){
  document.getElementById('monthly-preview').innerHTML=buildMonthlyText();
  document.getElementById('monthly-preview-wrap').style.display='block';
  document.getElementById('monthly-preview-wrap').scrollIntoView({behavior:'smooth'});
}

function submitMonthly(){
  const mon=gv('m-month'),yr=gv('m-year');
  const record={
    id:Date.now(),type:'monthly',date:`${yr}-${mon}`,reporter:gv('m-staff')||'All Staff',
    unit:'All Units',progress:0,issues:gv('m-issues'),status:'Submitted',
    rawText:buildMonthlyText().replace(/<[^>]+>/g,'')
  };
  records.push(record);save();renderRecords();
  showToast(lang==='my'?'လစဥ်အစီရင်ခံစာ သိမ်းဆည်းပြီးပါပြီ!':'Monthly report saved!');
  previewMonthly();
}

// ═══════════════════════════════════════════════
// AI MONTHLY ANALYSIS
// ═══════════════════════════════════════════════
async function aiMonthlyAnalysis(){
  const mon=gv('m-month'),yr=gv('m-year'),staff=gv('m-staff');
  const staffRecs=records.filter(r=>r.type==='daily'&&(staff==='ALL'||r.reporter===staff));
  const wrap=document.getElementById('monthly-ai-wrap');
  const content=document.getElementById('monthly-ai-content');
  wrap.style.display='block';
  content.innerHTML=`<div class="ai-loading"><div class="ai-dots"><span></span><span></span><span></span></div> ${lang==='my'?'AI လစဥ် ခွဲခြမ်းစိတ်ဖြာနေသည်...':'Generating AI monthly analysis...'}</div>`;
  wrap.scrollIntoView({behavior:'smooth'});

  const summaryData=staffRecs.map(r=>`${r.date}: ${r.reporter} — Progress:${r.progress}%, Issues:${r.issues||'none'}`).join('\n');
  const prompt=lang==='my'?
  `သင်သည် PMO AI ခွဲခြမ်းစိတ်ဖြာပေးသူဖြစ်သည်။ မြန်မာဘာသာဖြင့် ဖြေပါ။
  
  ${mon} ${yr} လ — ဝန်ထမ်း: ${staff==='ALL'?'အားလုံး':staff}
  
  နေ့စဥ်မှတ်တမ်းများ:
  ${summaryData||'(မှတ်တမ်းမရှိပါ)'}
  
  PMO ၏ လစဥ် စစ်ဆေးချက်အနေနဲ့:
  ✦ လပတ်စွမ်းဆောင်ရည် အကဲဖြတ်ချက် (ရမှတ် 100 အနက်)
  ✦ ဝန်ထမ်းတစ်ဦးချင်းစီ၏ အားသာချက်/အားနည်းချက်
  ✦ PMO ထံ တင်ပြသင့်သောကြောင်းများ
  ✦ နောက်လ အကြံပြုချက်များ
  �ို့ကို အသေးစိတ် ရေးသားပေးပါ။`:
  `You are a PMO AI analyst. Review the engineering team's monthly data and provide analysis in English.
  
  Month: ${mon} ${yr}, Staff: ${staff==='ALL'?'All':staff}
  
  Daily Records:
  ${summaryData||'(no records yet — provide sample analysis framework)'}
  
  As PMO officer provide:
  ✦ Monthly performance assessment (score /100)
  ✦ Individual strengths and areas for improvement
  ✦ Key observations to report to PMO head
  ✦ Recommendations for next month
  Be analytical and actionable.`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':'','anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1200,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    content.innerHTML=`<div class="ai-result">${data.content?.[0]?.text||'Analysis failed.'}</div>`;
  }catch(e){
    content.innerHTML=`<div class="ai-result" style="color:var(--accent3)">Error: ${e.message}</div>`;
  }
}

// ═══════════════════════════════════════════════
// AI TEAM ANALYSIS (PERFORMANCE PAGE)
// ═══════════════════════════════════════════════
async function aiTeamAnalysis(){
  const wrap=document.getElementById('team-ai-wrap');
  const content=document.getElementById('team-ai-content');
  wrap.style.display='block';
  content.innerHTML=`<div class="ai-loading"><div class="ai-dots"><span></span><span></span><span></span></div> ${lang==='my'?'AI အဖွဲ့ ခွဲခြမ်းစိတ်ဖြာနေသည်...':'Analyzing team performance...'}</div>`;
  wrap.scrollIntoView({behavior:'smooth'});

  const teamSummary=STAFF_LIST.map(s=>{
    const sc=calcStaffScore(s.name);
    return sc?`${s.name} (${s.role}): Score=${sc.score}, Progress=${sc.prog}%, Issues=${sc.issues}, Reports=${sc.count}`:`${s.name}: No data`;
  }).join('\n');

  const prompt=lang==='my'?
  `PMO AI ၏ ဘူမြောက်သောအဖွဲ့ စစ်ဆေးချက် မြန်မာဘာသာ:
  
  အဖွဲ့ဝင်များ ရမှတ်များ:
  ${teamSummary}
  
  ၁. အဖွဲ့ နှိုင်းယှဉ်ခြမ်းစိတ်ဖြာချက်
  ၂. အကောင်းဆုံး/အညံ့ဆုံးစွမ်းဆောင်မှုများ
  ၃. PMO မှ ဆောင်ရွက်သင့်သောအချက်များ
  ၄. အဖွဲ့ ပြုပြင်တိုးတက်ရေး အကြံပြုချက်
  တို့ကို ရေးသားပေးပါ။`:
  `As PMO AI analyst, evaluate the engineering team performance:
  
  Team Scores:
  ${teamSummary}
  
  Provide:
  1. Team comparative analysis
  2. Top & bottom performers with reasoning
  3. PMO action items
  4. Team improvement recommendations
  Be specific and professional.`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':'','anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1200,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    content.innerHTML=`<div class="ai-result">${data.content?.[0]?.text||'Analysis failed.'}</div>`;
  }catch(e){
    content.innerHTML=`<div class="ai-result" style="color:var(--accent3)">Error: ${e.message}</div>`;
  }
}

// ═══════════════════════════════════════════════
// AI ANALYSIS PAGE
// ═══════════════════════════════════════════════
async function runAIAnalysis(){
  const staff=gv('ai-sel-staff'),mon=gv('ai-sel-month');
  const result=document.getElementById('ai-analysis-result');
  result.innerHTML=`<div class="ai-box"><div class="ai-loading"><div class="ai-dots"><span></span><span></span><span></span></div> ${lang==='my'?'ခွဲခြမ်းစိတ်ဖြာနေသည်...':'Generating analysis...'}</div></div>`;

  const staffRecs=records.filter(r=>r.type==='daily'&&(staff==='ALL'||r.reporter===staff));
  const scoresData=staff==='ALL'?
    STAFF_LIST.map(s=>{const sc=calcStaffScore(s.name);return sc?`${s.name}: ${sc.score}/100 (${sc.count} reports, ${sc.prog}% avg progress)`:null;}).filter(Boolean).join('\n'):
    `${staff}: ${staffRecs.length} reports, Avg Progress: ${staffRecs.length?Math.round(staffRecs.reduce((a,r)=>a+parseInt(r.progress||50),0)/staffRecs.length):0}%`;

  const recDetail=staffRecs.slice(-10).map(r=>`${r.date}: Progress ${r.progress}%, Issues: ${r.issues?'Yes':'No'}, Quality: ${r.quality||'?'}/10`).join('\n');

  const prompt=lang==='my'?
  `PMO AI ခွဲခြမ်းစိတ်ဖြာပေးသူ — မြန်မာဘာသာ:
  
  စစ်ဆေးခဲ့သောဝန်ထမ်း: ${staff==='ALL'?'ဝန်ထမ်းအားလုံး':staff}
  စစ်ဆေးသောလ: ${mon}
  
  ရမှတ်/မှတ်တမ်းများ:
  ${scoresData||'မှတ်တမ်းမရှိသေးပါ'}
  
  နောက်ဆုံး မှတ်တမ်းများ:
  ${recDetail||'(မရှိပါ)'}
  
  PMO ၏ လစဥ် စစ်ဆေးချက်အနေနဲ့ အသေးစိတ် ခွဲခြမ်းစိတ်ဖြာချက် ရေးပေးပါ။ ရမှတ်၊ အဆင့်သတ်မှတ်မှု၊ အကြံပြုချက်များ ပါဝင်ပါစေ။`:
  `PMO AI Monthly Reviewer — English:
  
  Staff: ${staff==='ALL'?'All Staff':staff}, Month: ${mon}
  
  Data:
  ${scoresData||'No records yet'}
  
  Recent entries:
  ${recDetail||'(none)'}
  
  Provide a detailed PMO monthly review with: performance grade, key findings, staff comparison (if all), and specific improvement recommendations. Be professional and data-driven.`;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':'','anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1500,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    const txt=data.content?.[0]?.text||'Failed.';
    result.innerHTML=`
    <div class="ai-box">
      <div class="flex jb ai-c mb16">
        <div class="card-title" style="color:var(--accent)">🤖 ${lang==='my'?'AI ခွဲခြမ်းစိတ်ဖြာချက် ရလဒ်':'AI ANALYSIS RESULT'} — ${staff==='ALL'?lang==='my'?'ဝန်ထမ်းအားလုံး':'All Staff':staff} | ${mon}</div>
        <button class="btn btn-outline btn-sm" onclick="copyTxt2('ai-res-txt')">📋 ${lang==='my'?'ကူးယူ':'Copy'}</button>
      </div>
      <div class="ai-result" id="ai-res-txt">${txt}</div>
    </div>`;
  }catch(e){
    result.innerHTML=`<div class="ai-box"><div style="color:var(--accent3)">Error: ${e.message}</div></div>`;
  }
}

// ═══════════════════════════════════════════════
// RECORDS
// ═══════════════════════════════════════════════
function renderRecords(){
  const ft=gv('filter-type')||'all';
  const fs=gv('filter-staff')||'all';
  let filtered=records.filter(r=>(ft==='all'||r.type===ft)&&(fs==='all'||r.reporter===fs));
  const tbody=document.getElementById('records-table');
  if(!tbody) return;
  if(!filtered.length){
    tbody.innerHTML=`<tr><td colspan="8" style="text-align:center;padding:32px;color:var(--text3)">${lang==='my'?'မှတ်တမ်းမရှိသေးပါ':'No records found'}</td></tr>`;return;
  }
  tbody.innerHTML=[...filtered].reverse().map(r=>{
    const sc=r.quality?Math.round((parseInt(r.progress||50)*0.4)+(parseInt(r.quality||5)*10*0.25)+(parseInt(r.punctuality||5)*10*0.2)+(parseInt(r.teamwork||5)*10*0.15)):null;
    return `<tr>
      <td style="font-size:12px;font-family:'Courier New',monospace">${r.date||'—'}</td>
      <td><span class="pill ${r.type==='daily'?'pill-blue':'pill-yellow'}">${r.type}</span></td>
      <td style="font-size:12px">${r.reporter?r.reporter.split('(')[0].trim():'—'}</td>
      <td style="font-size:12px">${r.unit||'—'}</td>
      <td>${r.progress?`<div style="min-width:70px"><div style="font-size:11px;margin-bottom:3px">${r.progress}%</div><div class="prog-bar"><div class="prog-fill" style="width:${r.progress}%;background:var(--accent2)"></div></div></div>`:'-'}</td>
      <td>${sc!==null?`<span class="pill ${scorePill(sc)}">${Math.min(100,Math.max(0,sc))}</span>`:'-'}</td>
      <td><span class="pill ${r.status==='Submitted'?'pill-green':'pill-yellow'}">${r.status}</span></td>
      <td><div class="flex-gap">
        <button class="btn btn-outline btn-sm" onclick="viewRecord(${r.id})">${lang==='my'?'ကြည့်':'View'}</button>
        <button class="btn btn-danger btn-sm" onclick="delRecord(${r.id})">✕</button>
      </div></td>
    </tr>`;
  }).join('');
}

function viewRecord(id){
  const r=records.find(x=>x.id===id);if(!r)return;
  document.getElementById('modal-title').textContent=`${r.type.toUpperCase()} — ${r.date} — ${r.reporter}`;
  document.getElementById('modal-content').innerHTML=r.rawText||'(no content)';
  document.getElementById('modal-ai-wrap').style.display='none';
  document.getElementById('modal').classList.add('open');
}
function closeModal(){document.getElementById('modal').classList.remove('open');}
function delRecord(id){records=records.filter(r=>r.id!==id);save();renderRecords();renderDashboard();renderPerformance();showToast(lang==='my'?'ဖျက်ပြီးပါပြီ':'Deleted','var(--accent3)');}
function clearAll(){if(!confirm(lang==='my'?'မှတ်တမ်းအားလုံး ဖျက်မည်လား?':'Clear all records?'))return;records=[];save();renderRecords();renderDashboard();renderPerformance();renderStaff();}

// ═══════════════════════════════════════════════
// STAFF MODAL
// ═══════════════════════════════════════════════
async function openStaffModal(name){
  const s=STAFF_LIST.find(x=>x.name===name);
  const sc=calcStaffScore(name);
  document.getElementById('modal-title').textContent=`${name} — ${lang==='my'?'စွမ်းဆောင်ရည်စစ်ဆေးချက်':'Performance Review'}`;
  const recs=records.filter(r=>r.reporter===name&&r.type==='daily');
  document.getElementById('modal-content').textContent=sc?
  `Performance Score: ${sc.score}/100 | Grade: ${gradeLabel(sc.score)}
Reports Submitted: ${sc.count}
Avg Progress: ${sc.prog}%
Quality: ${sc.qual}% | Punctuality: ${sc.punc}% | Teamwork: ${sc.team}%
Issues Reported: ${sc.issues}

Recent Tasks:
${recs.slice(-3).map(r=>`• ${r.date}: ${r.tasks||'—'}`).join('\n')}`:
  lang==='my'?'မှတ်တမ်းမရှိသေးပါ':'No records yet.';
  document.getElementById('modal-ai-wrap').style.display='block';
  document.getElementById('modal-ai-content').innerHTML=`<div class="ai-loading"><div class="ai-dots"><span></span><span></span><span></span></div> ${lang==='my'?'AI စစ်ဆေးနေသည်...':'AI reviewing...'}</div>`;
  document.getElementById('modal').classList.add('open');

  const prompt=lang==='my'?
  `PMO AI — ဝန်ထမ်း ${name} (${s.role}) ၏ စွမ်းဆောင်ရည် စစ်ဆေးချက် မြန်မာဘာသာ:
  ရမှတ်: ${sc?sc.score:0}/100
  မှတ်တမ်း: ${sc?sc.count:0} ရက်
  ပုဂ္ဂိုလ်ရေး အကြံပြုချက်နှင့် တိုးတက်ရေးနည်းလမ်းများ ရေးပေးပါ။`:
  `PMO AI — Brief performance feedback for ${name} (${s.role}):
  Score: ${sc?sc.score:0}/100, Reports: ${sc?sc.count:0}
  Avg Progress: ${sc?sc.prog:0}%
  Give 3-4 specific, constructive feedback points.`;
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',headers:{'Content-Type':'application/json','x-api-key':'','anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:600,messages:[{role:'user',content:prompt}]})
    });
    const data=await res.json();
    document.getElementById('modal-ai-content').innerHTML=`<div class="ai-result">${data.content?.[0]?.text||'—'}</div>`;
  }catch(e){
    document.getElementById('modal-ai-content').innerHTML=`<div style="color:var(--accent3);font-size:12px">AI Error: ${e.message}</div>`;
  }
}

// ═══════════════════════════════════════════════
// UTILS
// ═══════════════════════════════════════════════
function save(){localStorage.setItem('eng_pmo_v2',JSON.stringify(records));}

function showToast(msg,color){
  const t=document.getElementById('toast');
  t.textContent=msg;
  t.style.background=color||'var(--accent2)';
  t.style.color=color?'#fff':'#0a0e1a';
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),3000);
}
function copyTxt(id){
  const el=document.getElementById(id);
  navigator.clipboard.writeText(el.innerText||el.textContent);
  showToast(lang==='my'?'ကူးယူပြီးပါပြီ!':'Copied to clipboard!');
}
function copyTxt2(id){
  const el=document.getElementById(id);
  if(el) navigator.clipboard.writeText(el.innerText||el.textContent);
  showToast(lang==='my'?'ကူးယူပြီးပါပြီ!':'Copied!');
}
document.getElementById('modal').addEventListener('click',function(e){if(e.target===this)closeModal();});
</script>
</body>
</html>
