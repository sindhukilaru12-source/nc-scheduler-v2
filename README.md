<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NC Scheduler — Interview Scheduler</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,300&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
<style>
  :root {
    --bg: #F7F5F0;
    --bg-card: #FFFFFF;
    --bg-sidebar: #1A1A2E;
    --bg-sidebar-hover: #16213E;
    --text-primary: #1A1A2E;
    --text-secondary: #6B7280;
    --text-muted: #9CA3AF;
    --accent: #4F46E5;
    --accent-light: #EEF2FF;
    --accent-dark: #3730A3;
    --success: #059669;
    --success-light: #D1FAE5;
    --warning: #D97706;
    --warning-light: #FEF3C7;
    --danger: #DC2626;
    --danger-light: #FEE2E2;
    --border: #E5E7EB;
    --border-light: #F3F4F6;
    --shadow: 0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06);
    --shadow-md: 0 4px 6px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.06);
    --shadow-lg: 0 10px 15px rgba(0,0,0,0.08), 0 4px 6px rgba(0,0,0,0.05);
    --radius: 10px;
    --radius-sm: 6px;
    --radius-lg: 14px;
    --sidebar-w: 240px;
    --header-h: 60px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text-primary);
    height: 100vh;
    display: flex;
    overflow: hidden;
    font-size: 14px;
  }

  /* ── Sidebar ── */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--bg-sidebar);
    display: flex;
    flex-direction: column;
    flex-shrink: 0;
    height: 100vh;
    overflow-y: auto;
  }

  .sidebar-logo {
    padding: 20px 20px 16px;
    border-bottom: 1px solid rgba(255,255,255,0.08);
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .logo-icon {
    width: 32px; height: 32px;
    background: var(--accent);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    color: #fff;
    font-size: 16px;
  }

  .logo-text {
    font-family: 'Instrument Serif', serif;
    font-size: 18px;
    color: #fff;
    letter-spacing: -0.3px;
  }

  .logo-text span { color: #818CF8; }

  .sidebar-section {
    padding: 20px 12px 8px;
  }

  .sidebar-label {
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.3);
    padding: 0 8px;
    margin-bottom: 6px;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 9px 12px;
    border-radius: 8px;
    color: rgba(255,255,255,0.55);
    cursor: pointer;
    transition: all 0.15s;
    font-size: 13.5px;
    font-weight: 400;
    position: relative;
  }

  .nav-item:hover { background: rgba(255,255,255,0.07); color: rgba(255,255,255,0.85); }

  .nav-item.active {
    background: rgba(79,70,229,0.25);
    color: #fff;
    font-weight: 500;
  }

  .nav-item.active::before {
    content: '';
    position: absolute;
    left: 0; top: 50%; transform: translateY(-50%);
    width: 3px; height: 18px;
    background: #818CF8;
    border-radius: 0 3px 3px 0;
  }

  .nav-item .ti { font-size: 17px; }

  .nav-badge {
    margin-left: auto;
    background: var(--accent);
    color: #fff;
    font-size: 10px;
    font-weight: 600;
    padding: 1px 7px;
    border-radius: 99px;
    min-width: 20px;
    text-align: center;
  }

  .sidebar-bottom {
    margin-top: auto;
    padding: 12px;
    border-top: 1px solid rgba(255,255,255,0.08);
  }

  .user-pill {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 8px 10px;
    border-radius: 8px;
    cursor: pointer;
  }

  .user-pill:hover { background: rgba(255,255,255,0.07); }

  .user-avatar {
    width: 30px; height: 30px;
    border-radius: 50%;
    background: linear-gradient(135deg, #818CF8, #4F46E5);
    display: flex; align-items: center; justify-content: center;
    color: #fff;
    font-size: 11px;
    font-weight: 600;
    flex-shrink: 0;
  }

  .user-name { font-size: 12.5px; color: rgba(255,255,255,0.75); font-weight: 500; }
  .user-role { font-size: 11px; color: rgba(255,255,255,0.35); }

  /* ── Main ── */
  .main {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .topbar {
    height: var(--header-h);
    background: var(--bg-card);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    padding: 0 24px;
    gap: 16px;
    flex-shrink: 0;
  }

  .topbar-title {
    font-size: 16px;
    font-weight: 600;
    color: var(--text-primary);
  }

  .topbar-subtitle {
    font-size: 12.5px;
    color: var(--text-muted);
    margin-left: 4px;
  }

  .topbar-right {
    margin-left: auto;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 8px 16px;
    border-radius: var(--radius-sm);
    font-size: 13px;
    font-weight: 500;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    border: 1px solid transparent;
    transition: all 0.15s;
    text-decoration: none;
  }

  .btn-primary {
    background: var(--accent);
    color: #fff;
    border-color: var(--accent);
  }

  .btn-primary:hover { background: var(--accent-dark); border-color: var(--accent-dark); }

  .btn-secondary {
    background: var(--bg-card);
    color: var(--text-primary);
    border-color: var(--border);
  }

  .btn-secondary:hover { background: var(--bg); }

  .btn-ghost {
    background: transparent;
    color: var(--text-secondary);
    border-color: transparent;
    padding: 6px 10px;
  }

  .btn-ghost:hover { background: var(--bg); color: var(--text-primary); }

  .btn-sm { padding: 5px 12px; font-size: 12px; }
  .btn-icon { padding: 7px; }

  .content {
    flex: 1;
    overflow-y: auto;
    padding: 24px;
  }

  /* ── Pages ── */
  .page { display: none; }
  .page.active { display: block; }

  /* ── Stats Row ── */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 14px;
    margin-bottom: 24px;
  }

  .stat-card {
    background: var(--bg-card);
    border-radius: var(--radius);
    padding: 18px 20px;
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
  }

  .stat-label {
    font-size: 12px;
    color: var(--text-muted);
    font-weight: 500;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .stat-label .ti { font-size: 14px; }

  .stat-value {
    font-size: 26px;
    font-weight: 600;
    color: var(--text-primary);
    line-height: 1;
    margin-bottom: 6px;
  }

  .stat-change {
    font-size: 11.5px;
    display: flex;
    align-items: center;
    gap: 3px;
  }

  .stat-change.up { color: var(--success); }
  .stat-change.neutral { color: var(--text-muted); }

  /* ── Section header ── */
  .section-header {
    display: flex;
    align-items: center;
    margin-bottom: 14px;
    gap: 12px;
  }

  .section-title {
    font-size: 15px;
    font-weight: 600;
    color: var(--text-primary);
  }

  .section-count {
    background: var(--bg);
    color: var(--text-secondary);
    font-size: 11px;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 99px;
    border: 1px solid var(--border);
  }

  .section-actions { margin-left: auto; display: flex; gap: 8px; align-items: center; }

  /* ── Table ── */
  .table-card {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    overflow: hidden;
    margin-bottom: 24px;
  }

  table { width: 100%; border-collapse: collapse; }

  thead th {
    padding: 11px 16px;
    text-align: left;
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: var(--text-muted);
    background: var(--bg);
    border-bottom: 1px solid var(--border);
  }

  tbody tr {
    border-bottom: 1px solid var(--border-light);
    transition: background 0.1s;
    cursor: pointer;
  }

  tbody tr:last-child { border-bottom: none; }
  tbody tr:hover { background: #FAFAFA; }

  td {
    padding: 13px 16px;
    font-size: 13.5px;
    color: var(--text-primary);
    vertical-align: middle;
  }

  /* ── Badges ── */
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    padding: 3px 9px;
    border-radius: 99px;
    font-size: 11.5px;
    font-weight: 500;
  }

  .badge-scheduled { background: var(--accent-light); color: var(--accent); }
  .badge-completed { background: var(--success-light); color: var(--success); }
  .badge-pending { background: var(--warning-light); color: var(--warning); }
  .badge-cancelled { background: var(--danger-light); color: var(--danger); }
  .badge-technical { background: #F0FDF4; color: #166534; }
  .badge-hr { background: #FFF7ED; color: #9A3412; }
  .badge-culture { background: #F5F3FF; color: #5B21B6; }
  .badge-final { background: #EFF6FF; color: #1D4ED8; }

  /* ── Candidate info ── */
  .candidate-cell {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .candidate-avatar {
    width: 32px; height: 32px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 11px;
    font-weight: 600;
    flex-shrink: 0;
    color: #fff;
  }

  .candidate-name { font-weight: 500; font-size: 13.5px; }
  .candidate-role { font-size: 11.5px; color: var(--text-muted); }

  /* ── Schedule Form ── */
  .form-card {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    padding: 24px;
    margin-bottom: 20px;
  }

  .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }
  .form-grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 18px; }
  .form-full { grid-column: 1 / -1; }

  .form-group { display: flex; flex-direction: column; gap: 6px; }

  label {
    font-size: 12.5px;
    font-weight: 500;
    color: var(--text-secondary);
  }

  label .required { color: var(--danger); margin-left: 2px; }

  input, select, textarea {
    font-family: 'DM Sans', sans-serif;
    font-size: 13.5px;
    padding: 9px 12px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    color: var(--text-primary);
    background: var(--bg-card);
    outline: none;
    transition: border-color 0.15s, box-shadow 0.15s;
    width: 100%;
  }

  input:focus, select:focus, textarea:focus {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(79,70,229,0.1);
  }

  textarea { resize: vertical; min-height: 80px; }

  .form-hint { font-size: 11px; color: var(--text-muted); }

  .form-actions {
    display: flex;
    align-items: center;
    gap: 10px;
    padding-top: 6px;
  }

  /* ── Calendar ── */
  .cal-wrap {
    display: grid;
    grid-template-columns: 1fr 320px;
    gap: 20px;
  }

  .calendar-card {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    overflow: hidden;
  }

  .cal-header {
    display: flex;
    align-items: center;
    padding: 16px 20px;
    border-bottom: 1px solid var(--border);
    gap: 10px;
  }

  .cal-month {
    font-size: 15px;
    font-weight: 600;
  }

  .cal-grid {
    padding: 12px 16px 16px;
  }

  .cal-days-header {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    text-align: center;
    margin-bottom: 8px;
  }

  .cal-days-header span {
    font-size: 11px;
    font-weight: 600;
    color: var(--text-muted);
    padding: 4px 0;
    text-transform: uppercase;
    letter-spacing: 0.04em;
  }

  .cal-dates {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 3px;
  }

  .cal-date {
    aspect-ratio: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    font-size: 13px;
    cursor: pointer;
    position: relative;
    transition: all 0.12s;
  }

  .cal-date:hover { background: var(--bg); }
  .cal-date.today { font-weight: 700; color: var(--accent); }

  .cal-date.selected {
    background: var(--accent);
    color: #fff;
    font-weight: 600;
  }

  .cal-date.has-interviews::after {
    content: '';
    position: absolute;
    bottom: 3px;
    width: 4px; height: 4px;
    border-radius: 50%;
    background: var(--accent);
  }

  .cal-date.selected::after { background: rgba(255,255,255,0.7); }

  .cal-date.other-month { color: var(--text-muted); opacity: 0.4; }

  .cal-date.disabled { color: var(--text-muted); opacity: 0.3; cursor: default; }

  /* Day panel */
  .day-panel {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .day-panel-header {
    padding: 16px 18px;
    border-bottom: 1px solid var(--border);
  }

  .day-panel-date { font-size: 15px; font-weight: 600; }
  .day-panel-sub { font-size: 12px; color: var(--text-muted); margin-top: 2px; }

  .day-slots {
    flex: 1;
    overflow-y: auto;
    padding: 12px;
  }

  .time-slot {
    display: flex;
    gap: 10px;
    padding: 10px;
    border-radius: var(--radius-sm);
    margin-bottom: 8px;
    border: 1px solid var(--border-light);
    transition: all 0.12s;
    cursor: pointer;
  }

  .time-slot:hover {
    border-color: var(--accent);
    background: var(--accent-light);
  }

  .slot-time {
    font-size: 12px;
    color: var(--text-muted);
    font-weight: 500;
    min-width: 52px;
    padding-top: 2px;
  }

  .slot-info { flex: 1; min-width: 0; }
  .slot-name { font-size: 13px; font-weight: 500; }
  .slot-role { font-size: 11.5px; color: var(--text-muted); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }

  .slot-bar {
    width: 3px;
    border-radius: 99px;
    flex-shrink: 0;
  }

  .empty-slots {
    text-align: center;
    padding: 32px 20px;
    color: var(--text-muted);
  }

  .empty-slots .ti { font-size: 28px; display: block; margin-bottom: 8px; }

  /* ── ATS Panel ── */
  .ats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-bottom: 24px;
  }

  .ats-source {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    box-shadow: var(--shadow);
    padding: 20px;
  }

  .ats-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 16px;
    padding-bottom: 14px;
    border-bottom: 1px solid var(--border);
  }

  .ats-logo {
    width: 38px; height: 38px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
    border: 1px solid var(--border);
  }

  .ats-name { font-weight: 600; font-size: 14px; }
  .ats-status { font-size: 11.5px; color: var(--text-muted); }

  .ats-connected { color: var(--success); font-weight: 500; }
  .ats-disconnected { color: var(--danger); font-weight: 500; }

  .sync-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 9px 0;
    border-bottom: 1px solid var(--border-light);
    font-size: 13px;
  }

  .sync-item:last-child { border-bottom: none; }
  .sync-label { color: var(--text-secondary); }
  .sync-value { font-weight: 500; }

  .toggle-switch {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .switch {
    position: relative;
    width: 34px;
    height: 18px;
  }

  .switch input { opacity: 0; width: 0; height: 0; }

  .slider-switch {
    position: absolute;
    inset: 0;
    background: var(--border);
    border-radius: 18px;
    cursor: pointer;
    transition: background 0.2s;
  }

  .slider-switch:before {
    content: '';
    position: absolute;
    width: 12px; height: 12px;
    border-radius: 50%;
    background: #fff;
    left: 3px; top: 3px;
    transition: transform 0.2s;
  }

  input:checked + .slider-switch { background: var(--accent); }
  input:checked + .slider-switch:before { transform: translateX(16px); }

  /* ── Pipeline view ── */
  .pipeline-board {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    align-items: start;
  }

  .pipeline-col {
    background: var(--bg);
    border-radius: var(--radius);
    border: 1px solid var(--border);
    overflow: hidden;
  }

  .pipeline-col-header {
    padding: 12px 14px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--bg-card);
  }

  .pipeline-col-title { font-size: 12.5px; font-weight: 600; }

  .pipeline-col-count {
    margin-left: auto;
    background: var(--bg);
    font-size: 11px;
    font-weight: 600;
    color: var(--text-muted);
    padding: 1px 7px;
    border-radius: 99px;
    border: 1px solid var(--border);
  }

  .pipeline-cards { padding: 10px; display: flex; flex-direction: column; gap: 8px; }

  .pipeline-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 12px 13px;
    cursor: pointer;
    transition: all 0.15s;
    box-shadow: var(--shadow);
  }

  .pipeline-card:hover {
    border-color: var(--accent);
    box-shadow: var(--shadow-md);
    transform: translateY(-1px);
  }

  .pc-name { font-weight: 500; font-size: 13px; margin-bottom: 4px; }
  .pc-role { font-size: 11.5px; color: var(--text-muted); margin-bottom: 10px; }

  .pc-meta {
    display: flex;
    align-items: center;
    gap: 6px;
    flex-wrap: wrap;
  }

  /* ── Modal ── */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.45);
    z-index: 1000;
    align-items: center;
    justify-content: center;
    padding: 24px;
  }

  .modal-overlay.open { display: flex; }

  .modal {
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
    width: 100%;
    max-width: 560px;
    max-height: 90vh;
    overflow-y: auto;
    animation: slideUp 0.2s ease;
  }

  @keyframes slideUp {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .modal-header {
    padding: 20px 24px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
  }

  .modal-title { font-size: 16px; font-weight: 600; }

  .modal-body { padding: 0 24px; }

  .modal-footer {
    padding: 20px 24px;
    display: flex;
    gap: 10px;
    justify-content: flex-end;
    border-top: 1px solid var(--border);
    margin-top: 20px;
  }

  /* ── Search / Filter bar ── */
  .filter-bar {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 16px;
    flex-wrap: wrap;
  }

  .search-input-wrap {
    position: relative;
    flex: 1;
    min-width: 200px;
  }

  .search-input-wrap .ti {
    position: absolute;
    left: 10px; top: 50%; transform: translateY(-50%);
    color: var(--text-muted);
    font-size: 16px;
  }

  .search-input {
    padding-left: 34px !important;
    width: 100%;
  }

  /* ── Notification toast ── */
  .toast-container {
    position: fixed;
    top: 16px;
    right: 16px;
    z-index: 9999;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .toast {
    background: var(--bg-sidebar);
    color: #fff;
    padding: 12px 16px;
    border-radius: var(--radius);
    font-size: 13px;
    display: flex;
    align-items: center;
    gap: 10px;
    box-shadow: var(--shadow-lg);
    animation: slideIn 0.25s ease, fadeOut 0.3s 2.7s forwards;
    min-width: 260px;
  }

  .toast .ti { font-size: 17px; color: #6EE7B7; }

  @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
  @keyframes fadeOut { from { opacity: 1; } to { opacity: 0; pointer-events: none; } }

  /* ── Misc ── */
  .divider { height: 1px; background: var(--border); margin: 16px 0; }

  .pill-row { display: flex; flex-wrap: wrap; gap: 6px; }

  .interviewer-pill {
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 4px 10px 4px 4px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 99px;
    font-size: 12px;
    color: var(--text-secondary);
  }

  .interviewer-pill .i-av {
    width: 20px; height: 20px;
    border-radius: 50%;
    font-size: 9px;
    font-weight: 600;
    color: #fff;
    display: flex; align-items: center; justify-content: center;
  }

  /* Checklist */
  .checklist { display: flex; flex-direction: column; gap: 8px; }

  .check-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 13.5px;
    color: var(--text-primary);
    cursor: pointer;
    padding: 2px 0;
  }

  .check-item input[type=checkbox] { accent-color: var(--accent); width: 15px; height: 15px; }

  /* Color bars for pipeline */
  .col-bar { width: 3px; height: 14px; border-radius: 99px; flex-shrink: 0; }

  .activity-list { display: flex; flex-direction: column; }

  .activity-item {
    display: flex;
    gap: 12px;
    padding: 12px 0;
    border-bottom: 1px solid var(--border-light);
  }

  .activity-item:last-child { border-bottom: none; }

  .activity-dot {
    width: 28px; height: 28px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 13px;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .activity-content { flex: 1; }
  .activity-text { font-size: 13px; }
  .activity-text strong { font-weight: 500; }
  .activity-time { font-size: 11.5px; color: var(--text-muted); margin-top: 2px; }

  .progress-bar-wrap { height: 5px; background: var(--border); border-radius: 99px; overflow: hidden; margin-top: 6px; }
  .progress-bar { height: 100%; border-radius: 99px; background: var(--accent); transition: width 0.4s; }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 5px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 99px; }

  /* ── Rejection Email styles ── */
  .reject-banner {
    display: flex; align-items: center; gap: 10px;
    background: var(--danger-light);
    border: 1px solid rgba(220,38,38,0.2);
    border-radius: var(--radius-sm);
    padding: 10px 13px;
    margin-bottom: 14px;
    font-size: 13px;
    color: #7F1D1D;
  }
  .reject-banner .ti { font-size: 17px; color: var(--danger); flex-shrink: 0; }

  .email-preview-box {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 14px 16px;
    font-size: 13px;
    line-height: 1.75;
    color: var(--text-primary);
    white-space: pre-wrap;
    min-height: 120px;
    max-height: 220px;
    overflow-y: auto;
    font-family: 'DM Sans', sans-serif;
    resize: vertical;
  }

  .upload-zone {
    border: 2px dashed var(--border);
    border-radius: var(--radius);
    padding: 28px 20px;
    text-align: center;
    cursor: pointer;
    transition: all 0.15s;
    background: var(--bg);
  }
  .upload-zone:hover, .upload-zone.drag-over {
    border-color: var(--accent);
    background: var(--accent-light);
  }
  .upload-zone .ti { font-size: 28px; color: var(--text-muted); display: block; margin-bottom: 8px; }
  .upload-zone.has-file { border-color: var(--success); background: var(--success-light); }
  .upload-zone.has-file .ti { color: var(--success); }

  .tab-row {
    display: flex;
    border-bottom: 1px solid var(--border);
    margin-bottom: 16px;
  }
  .tab-btn {
    padding: 8px 16px;
    font-size: 13px;
    font-weight: 500;
    color: var(--text-muted);
    cursor: pointer;
    border-bottom: 2px solid transparent;
    margin-bottom: -1px;
    transition: all 0.15s;
    background: none;
    border-top: none; border-left: none; border-right: none;
    font-family: 'DM Sans', sans-serif;
  }
  .tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
  .tab-panel { display: none; }
  .tab-panel.active { display: block; }

  .template-tag {
    display: inline-flex; align-items: center; gap: 4px;
    background: var(--accent-light); color: var(--accent);
    border: 1px solid rgba(79,70,229,0.2);
    border-radius: var(--radius-sm);
    padding: 2px 8px; font-size: 11.5px; font-weight: 500;
    cursor: pointer;
    transition: background 0.12s;
  }
  .template-tag:hover { background: rgba(79,70,229,0.15); }
</style>
</head>
<body>

<!-- ── SIDEBAR ── -->
<aside class="sidebar">
  <div class="sidebar-logo">
    <div class="logo-icon"><i class="ti ti-calendar-event"></i></div>
    <span class="logo-text">NC <span>Scheduler</span></span>
  </div>

  <div class="sidebar-section">
    <div class="sidebar-label">Main</div>
    <div class="nav-item active" data-page="dashboard" onclick="navigate('dashboard', this)">
      <i class="ti ti-layout-dashboard"></i> Dashboard
    </div>
    <div class="nav-item" data-page="schedule" onclick="navigate('schedule', this)">
      <i class="ti ti-calendar-plus"></i> Schedule Interview
    </div>
    <div class="nav-item" data-page="calendar" onclick="navigate('calendar', this)">
      <i class="ti ti-calendar"></i> Calendar
    </div>
    <div class="nav-item" data-page="interviews" onclick="navigate('interviews', this)">
      <i class="ti ti-list-check"></i> All Interviews
      <span class="nav-badge">12</span>
    </div>
  </div>

  <div class="sidebar-section">
    <div class="sidebar-label">Recruitment</div>
    <div class="nav-item" data-page="pipeline" onclick="navigate('pipeline', this)">
      <i class="ti ti-hierarchy-2"></i> Pipeline
    </div>
    <div class="nav-item" data-page="candidates" onclick="navigate('candidates', this)">
      <i class="ti ti-users"></i> Candidates
    </div>
  </div>

  <div class="sidebar-section">
    <div class="sidebar-label">Integrations</div>
    <div class="nav-item" data-page="ats" onclick="navigate('ats', this)">
      <i class="ti ti-plug-connected"></i> ATS Integration
    </div>
    <div class="nav-item" data-page="settings" onclick="navigate('settings', this)">
      <i class="ti ti-settings"></i> Settings
    </div>
  </div>

  <div class="sidebar-bottom">
    <div class="user-pill">
      <div class="user-avatar">SR</div>
      <div>
        <div class="user-name">Sarah Rodriguez</div>
        <div class="user-role">Talent Acquisition Lead</div>
      </div>
    </div>
  </div>
</aside>

<!-- ── MAIN ── -->
<main class="main">

  <!-- Dashboard -->
  <div id="page-dashboard" class="page active">
    <div class="topbar">
      <div>
        <div class="topbar-title">Dashboard</div>
      </div>
      <div class="topbar-right">
        <span style="font-size:12px;color:var(--text-muted);">May 2025</span>
        <button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))">
          <i class="ti ti-plus"></i> Schedule
        </button>
      </div>
    </div>
    <div class="content">

      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-label"><i class="ti ti-calendar-event"></i> This Week</div>
          <div class="stat-value">14</div>
          <div class="stat-change up"><i class="ti ti-trending-up"></i> +3 from last week</div>
        </div>
        <div class="stat-card">
          <div class="stat-label"><i class="ti ti-user-check"></i> Confirmed</div>
          <div class="stat-value">11</div>
          <div class="stat-change neutral"><i class="ti ti-minus"></i> 79% acceptance rate</div>
        </div>
        <div class="stat-card">
          <div class="stat-label"><i class="ti ti-clock-hour-4"></i> Avg. Time-to-Schedule</div>
          <div class="stat-value">1.2<span style="font-size:14px;font-weight:400;color:var(--text-muted)"> days</span></div>
          <div class="stat-change up"><i class="ti ti-trending-up"></i> 0.4 days faster</div>
        </div>
        <div class="stat-card">
          <div class="stat-label"><i class="ti ti-plug-connected"></i> ATS Synced</div>
          <div class="stat-value">48</div>
          <div class="stat-change neutral"><i class="ti ti-refresh"></i> Last synced 2 min ago</div>
        </div>
      </div>

      <div style="display:grid;grid-template-columns:2fr 1fr;gap:20px;margin-bottom:24px;">

        <!-- Upcoming -->
        <div>
          <div class="section-header">
            <span class="section-title">Upcoming Interviews</span>
            <span class="section-count">6 today</span>
            <div class="section-actions">
              <button class="btn btn-ghost btn-sm" onclick="navigate('interviews', document.querySelector('[data-page="interviews"]'))">View all</button>
            </div>
          </div>
          <div class="table-card">
            <table>
              <thead>
                <tr>
                  <th>Candidate</th>
                  <th>Time</th>
                  <th>Type</th>
                  <th>Interviewer</th>
                  <th>Status</th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <tr onclick="openInterviewModal('Priya Mehta')">
                  <td>
                    <div class="candidate-cell">
                      <div class="candidate-avatar" style="background:#6D28D9">PM</div>
                      <div>
                        <div class="candidate-name">Priya Mehta</div>
                        <div class="candidate-role">Senior Frontend Engineer</div>
                      </div>
                    </div>
                  </td>
                  <td style="color:var(--text-secondary)">10:00 AM</td>
                  <td><span class="badge badge-technical">Technical</span></td>
                  <td style="color:var(--text-secondary)">A. Kumar</td>
                  <td><span class="badge badge-scheduled">Scheduled</span></td>
                  <td><button class="btn btn-ghost btn-icon btn-sm"><i class="ti ti-dots-vertical"></i></button></td>
                </tr>
                <tr onclick="openInterviewModal('James Okafor')">
                  <td>
                    <div class="candidate-cell">
                      <div class="candidate-avatar" style="background:#0891B2">JO</div>
                      <div>
                        <div class="candidate-name">James Okafor</div>
                        <div class="candidate-role">Product Manager</div>
                      </div>
                    </div>
                  </td>
                  <td style="color:var(--text-secondary)">11:30 AM</td>
                  <td><span class="badge badge-culture">Culture Fit</span></td>
                  <td style="color:var(--text-secondary)">L. Chen</td>
                  <td><span class="badge badge-scheduled">Scheduled</span></td>
                  <td><button class="btn btn-ghost btn-icon btn-sm"><i class="ti ti-dots-vertical"></i></button></td>
                </tr>
                <tr onclick="openInterviewModal('Ananya Iyer')">
                  <td>
                    <div class="candidate-cell">
                      <div class="candidate-avatar" style="background:#059669">AI</div>
                      <div>
                        <div class="candidate-name">Ananya Iyer</div>
                        <div class="candidate-role">Data Scientist</div>
                      </div>
                    </div>
                  </td>
                  <td style="color:var(--text-secondary)">2:00 PM</td>
                  <td><span class="badge badge-hr">HR Round</span></td>
                  <td style="color:var(--text-secondary)">S. Rodriguez</td>
                  <td><span class="badge badge-pending">Pending</span></td>
                  <td><button class="btn btn-ghost btn-icon btn-sm"><i class="ti ti-dots-vertical"></i></button></td>
                </tr>
                <tr onclick="openInterviewModal('Marco Rossi')">
                  <td>
                    <div class="candidate-cell">
                      <div class="candidate-avatar" style="background:#B45309">MR</div>
                      <div>
                        <div class="candidate-name">Marco Rossi</div>
                        <div class="candidate-role">Backend Engineer</div>
                      </div>
                    </div>
                  </td>
                  <td style="color:var(--text-secondary)">4:00 PM</td>
                  <td><span class="badge badge-final">Final Round</span></td>
                  <td style="color:var(--text-secondary)">T. Obi</td>
                  <td><span class="badge badge-scheduled">Scheduled</span></td>
                  <td><button class="btn btn-ghost btn-icon btn-sm"><i class="ti ti-dots-vertical"></i></button></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Activity -->
        <div>
          <div class="section-header">
            <span class="section-title">Recent Activity</span>
          </div>
          <div class="table-card" style="padding:4px 16px 8px;">
            <div class="activity-list">
              <div class="activity-item">
                <div class="activity-dot" style="background:var(--accent-light)"><i class="ti ti-calendar-plus" style="font-size:14px;color:var(--accent)"></i></div>
                <div class="activity-content">
                  <div class="activity-text">Interview scheduled for <strong>Priya Mehta</strong></div>
                  <div class="activity-time">2 min ago · via Greenhouse</div>
                </div>
              </div>
              <div class="activity-item">
                <div class="activity-dot" style="background:var(--success-light)"><i class="ti ti-check" style="font-size:14px;color:var(--success)"></i></div>
                <div class="activity-content">
                  <div class="activity-text"><strong>Rahul Sharma</strong> confirmed interview</div>
                  <div class="activity-time">14 min ago</div>
                </div>
              </div>
              <div class="activity-item">
                <div class="activity-dot" style="background:var(--warning-light)"><i class="ti ti-refresh" style="font-size:14px;color:var(--warning)"></i></div>
                <div class="activity-content">
                  <div class="activity-text">ATS sync completed — 48 candidates</div>
                  <div class="activity-time">1 hr ago · Workday</div>
                </div>
              </div>
              <div class="activity-item">
                <div class="activity-dot" style="background:var(--danger-light)"><i class="ti ti-x" style="font-size:14px;color:var(--danger)"></i></div>
                <div class="activity-content">
                  <div class="activity-text"><strong>Eva Nguyen</strong> cancelled interview</div>
                  <div class="activity-time">3 hr ago</div>
                </div>
              </div>
              <div class="activity-item">
                <div class="activity-dot" style="background:var(--accent-light)"><i class="ti ti-send" style="font-size:14px;color:var(--accent)"></i></div>
                <div class="activity-content">
                  <div class="activity-text">Reminders sent to <strong>6 candidates</strong></div>
                  <div class="activity-time">4 hr ago · Automated</div>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>

      <!-- Role stats -->
      <div class="section-header">
        <span class="section-title">Interview Completion by Role</span>
      </div>
      <div class="table-card" style="padding:16px 20px;margin-bottom:0;">
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:24px;">
          <div>
            <div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:6px;">
              <span>Frontend Engineering</span><span style="color:var(--text-muted)">7/10</span>
            </div>
            <div class="progress-bar-wrap"><div class="progress-bar" style="width:70%"></div></div>
          </div>
          <div>
            <div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:6px;">
              <span>Product Management</span><span style="color:var(--text-muted)">4/6</span>
            </div>
            <div class="progress-bar-wrap"><div class="progress-bar" style="width:67%;background:#059669"></div></div>
          </div>
          <div>
            <div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:6px;">
              <span>Data Science</span><span style="color:var(--text-muted)">3/8</span>
            </div>
            <div class="progress-bar-wrap"><div class="progress-bar" style="width:37%;background:#D97706"></div></div>
          </div>
        </div>
      </div>

    </div>
  </div>

  <!-- Schedule Interview -->
  <div id="page-schedule" class="page">
    <div class="topbar">
      <div>
        <div class="topbar-title">Schedule Interview</div>
      </div>
    </div>
    <div class="content">

      <div style="display:grid;grid-template-columns:1fr 340px;gap:20px;align-items:start;">
        <div>
          <div class="form-card">
            <div style="font-size:14px;font-weight:600;margin-bottom:16px;display:flex;align-items:center;gap:8px;">
              <i class="ti ti-user-search" style="color:var(--accent)"></i> Candidate Details
            </div>
            <div class="form-grid">
              <div class="form-group">
                <label>Candidate <span class="required">*</span></label>
                <select>
                  <option value="">Search or select candidate…</option>
                  <option>Priya Mehta — Frontend Engineer</option>
                  <option>James Okafor — Product Manager</option>
                  <option>Ananya Iyer — Data Scientist</option>
                  <option>Marco Rossi — Backend Engineer</option>
                  <option>Divya Sharma — UX Designer</option>
                </select>
                <span class="form-hint">Synced from connected ATS</span>
              </div>
              <div class="form-group">
                <label>Job Opening <span class="required">*</span></label>
                <select>
                  <option value="">Select job opening…</option>
                  <option>Senior Frontend Engineer — Bangalore</option>
                  <option>Product Manager — Mumbai</option>
                  <option>Data Scientist — Remote</option>
                  <option>Backend Engineer — Pune</option>
                </select>
              </div>
              <div class="form-group">
                <label>Interview Stage <span class="required">*</span></label>
                <select>
                  <option>HR Screening</option>
                  <option>Technical Round 1</option>
                  <option>Technical Round 2</option>
                  <option>Culture Fit</option>
                  <option>Final Round</option>
                </select>
              </div>
              <div class="form-group">
                <label>Interview Format</label>
                <select>
                  <option>Video Call (Google Meet)</option>
                  <option>Video Call (Zoom)</option>
                  <option>In-Person</option>
                  <option>Phone Call</option>
                </select>
              </div>
            </div>
          </div>

          <div class="form-card">
            <div style="font-size:14px;font-weight:600;margin-bottom:16px;display:flex;align-items:center;gap:8px;">
              <i class="ti ti-clock" style="color:var(--accent)"></i> Date & Time
            </div>
            <div class="form-grid-3">
              <div class="form-group">
                <label>Date <span class="required">*</span></label>
                <input type="date" value="2025-05-16">
              </div>
              <div class="form-group">
                <label>Start Time <span class="required">*</span></label>
                <input type="time" value="10:00">
              </div>
              <div class="form-group">
                <label>Duration</label>
                <select>
                  <option>30 minutes</option>
                  <option selected>45 minutes</option>
                  <option>60 minutes</option>
                  <option>90 minutes</option>
                </select>
              </div>
            </div>
            <div style="margin-top:14px;" class="form-group">
              <label>Timezone</label>
              <select>
                <option>IST — India Standard Time (UTC+5:30)</option>
                <option>PST — Pacific Standard Time (UTC-8)</option>
                <option>EST — Eastern Standard Time (UTC-5)</option>
                <option>GMT — Greenwich Mean Time (UTC+0)</option>
              </select>
            </div>
          </div>

          <div class="form-card">
            <div style="font-size:14px;font-weight:600;margin-bottom:16px;display:flex;align-items:center;gap:8px;">
              <i class="ti ti-users" style="color:var(--accent)"></i> Interviewers &amp; Panel
            </div>
            <div class="form-grid" style="margin-bottom:14px;">
              <div class="form-group">
                <label>Panel Name</label>
                <input type="text" id="panelNameInput" placeholder="e.g. Engineering Panel A, Design Review Board…" oninput="updatePanelPreview()">
                <span class="form-hint">Optional — groups this interview under a named panel</span>
              </div>
              <div class="form-group">
                <label>Panel Type</label>
                <select id="panelTypeSelect" onchange="updatePanelPreview()">
                  <option value="">— None —</option>
                  <option value="Technical Panel">Technical Panel</option>
                  <option value="Leadership Panel">Leadership Panel</option>
                  <option value="Cross-functional Panel">Cross-functional Panel</option>
                  <option value="Hiring Committee">Hiring Committee</option>
                  <option value="Custom">Custom</option>
                </select>
              </div>
            </div>
            <div id="panelPreview" style="display:none;align-items:center;gap:10px;padding:10px 13px;background:var(--accent-light);border:1px solid rgba(79,70,229,0.18);border-radius:var(--radius-sm);margin-bottom:14px;">
              <i class="ti ti-layout-board" style="color:var(--accent);font-size:16px;"></i>
              <div>
                <div id="panelPreviewName" style="font-size:13px;font-weight:600;color:var(--accent-dark);"></div>
                <div id="panelPreviewType" style="font-size:11.5px;color:var(--accent);"></div>
              </div>
              <button class="btn btn-ghost btn-sm btn-icon" style="margin-left:auto;" onclick="clearPanel()"><i class="ti ti-x" style="font-size:13px;color:var(--accent)"></i></button>
            </div>
            <div class="divider" style="margin:0 0 14px;"></div>
            <div class="form-group" style="margin-bottom:14px;">
              <label>Add Interviewers <span class="required">*</span></label>
              <select onchange="addInterviewer(this)">
                <option value="">Select interviewer…</option>
                <option>Anil Kumar — Engineering Lead</option>
                <option>Lena Chen — Product Director</option>
                <option>Sarah Rodriguez — Talent Lead</option>
                <option>Tanvir Obi — CTO</option>
                <option>Riya Patel — UX Lead</option>
              </select>
            </div>
            <div class="pill-row" id="interviewer-pills">
              <div class="interviewer-pill">
                <div class="i-av" style="background:#6D28D9">AK</div>
                Anil Kumar
                <i class="ti ti-x" style="font-size:12px;cursor:pointer;color:var(--text-muted)" onclick="this.closest('.interviewer-pill').remove()"></i>
              </div>
            </div>
          </div>

          <div class="form-card">
            <div style="font-size:14px;font-weight:600;margin-bottom:16px;display:flex;align-items:center;gap:8px;">
              <i class="ti ti-notes" style="color:var(--accent)"></i> Additional Details
            </div>
            <div class="form-grid">
              <div class="form-group form-full">
                <label>Interview Notes / Preparation Guide</label>
                <textarea placeholder="Add context for interviewers — topics to cover, candidate background, evaluation criteria…"></textarea>
              </div>
              <div class="form-group">
                <label>Meeting Link</label>
                <input type="text" placeholder="Auto-generated or paste your link" value="meet.google.com/xyz-abc-123">
              </div>
              <div class="form-group">
                <label>Location (if in-person)</label>
                <input type="text" placeholder="Room / Office address">
              </div>
            </div>
            <div class="divider"></div>
            <div style="font-size:13px;font-weight:500;margin-bottom:10px;">Notifications</div>
            <div class="checklist">
              <label class="check-item"><input type="checkbox" checked> Send calendar invite to candidate</label>
              <label class="check-item"><input type="checkbox" checked> Send calendar invite to interviewers</label>
              <label class="check-item"><input type="checkbox" checked> Send reminder 24 hours before</label>
              <label class="check-item"><input type="checkbox"> Send reminder 1 hour before</label>
              <label class="check-item"><input type="checkbox" checked> Update status in ATS after scheduling</label>
            </div>
          </div>

          <div class="form-actions">
            <button class="btn btn-primary" onclick="scheduleInterview()">
              <i class="ti ti-calendar-check"></i> Schedule Interview
            </button>
            <button class="btn btn-secondary">Save as Draft</button>
            <button class="btn btn-ghost">Cancel</button>
          </div>
        </div>

        <!-- Sidebar hints -->
        <div>
          <div class="form-card" style="background:var(--accent-light);border-color:rgba(79,70,229,0.2);">
            <div style="font-size:13.5px;font-weight:600;color:var(--accent-dark);margin-bottom:12px;">
              <i class="ti ti-sparkles" style="margin-right:6px"></i>Smart Scheduling
            </div>
            <div style="font-size:12.5px;color:var(--accent-dark);line-height:1.7;">
              HireFlow checks interviewer calendars and suggests optimal time slots to avoid conflicts.
            </div>
            <button class="btn btn-secondary btn-sm" style="margin-top:12px;width:100%;justify-content:center">
              <i class="ti ti-wand"></i> Find Best Slots
            </button>
          </div>

          <div class="form-card" style="margin-top:0;">
            <div style="font-size:13.5px;font-weight:600;margin-bottom:12px;">
              <i class="ti ti-plug-connected" style="margin-right:6px;color:var(--success)"></i>ATS Connections
            </div>
            <div class="sync-item">
              <span class="sync-label">Greenhouse</span>
              <span class="ats-connected">● Connected</span>
            </div>
            <div class="sync-item">
              <span class="sync-label">Workday</span>
              <span class="ats-connected">● Connected</span>
            </div>
            <div class="sync-item">
              <span class="sync-label">Lever</span>
              <span class="ats-disconnected">● Disconnected</span>
            </div>
          </div>

          <div class="form-card" style="margin-top:0;">
            <div style="font-size:13.5px;font-weight:600;margin-bottom:10px;">Interviewer Availability</div>
            <div style="font-size:12.5px;color:var(--text-secondary);line-height:1.8;">
              <div style="display:flex;justify-content:space-between;">
                <span>Anil Kumar</span>
                <span style="color:var(--success);font-weight:500">✓ Free</span>
              </div>
              <div style="display:flex;justify-content:space-between;">
                <span>Lena Chen</span>
                <span style="color:var(--warning);font-weight:500">⚠ Busy 2–4 PM</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Calendar -->
  <div id="page-calendar" class="page">
    <div class="topbar">
      <div><div class="topbar-title">Calendar View</div></div>
      <div class="topbar-right">
        <button class="btn btn-secondary btn-sm"><i class="ti ti-chevron-left"></i></button>
        <span style="font-size:13.5px;font-weight:500">May 2025</span>
        <button class="btn btn-secondary btn-sm"><i class="ti ti-chevron-right"></i></button>
        <button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))">
          <i class="ti ti-plus"></i> New
        </button>
      </div>
    </div>
    <div class="content">
      <div class="cal-wrap">
        <div class="calendar-card">
          <div class="cal-header">
            <i class="ti ti-calendar" style="color:var(--accent)"></i>
            <span class="cal-month">May 2025</span>
          </div>
          <div class="cal-grid">
            <div class="cal-days-header">
              <span>Sun</span><span>Mon</span><span>Tue</span><span>Wed</span>
              <span>Thu</span><span>Fri</span><span>Sat</span>
            </div>
            <div class="cal-dates" id="calDates"></div>
          </div>
        </div>

        <div class="day-panel">
          <div class="day-panel-header">
            <div class="day-panel-date" id="dayPanelDate">Thursday, 15 May</div>
            <div class="day-panel-sub" id="dayPanelSub">4 interviews scheduled</div>
          </div>
          <div class="day-slots" id="daySlots"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- All Interviews -->
  <div id="page-interviews" class="page">
    <div class="topbar">
      <div><div class="topbar-title">All Interviews</div></div>
      <div class="topbar-right">
        <button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))">
          <i class="ti ti-plus"></i> Schedule
        </button>
      </div>
    </div>
    <div class="content">
      <div class="filter-bar">
        <div class="search-input-wrap">
          <i class="ti ti-search"></i>
          <input type="text" class="search-input" placeholder="Search candidates, roles…">
        </div>
        <select style="width:auto;">
          <option>All Stages</option>
          <option>HR Screening</option>
          <option>Technical Round</option>
          <option>Culture Fit</option>
          <option>Final Round</option>
        </select>
        <select style="width:auto;">
          <option>All Status</option>
          <option>Scheduled</option>
          <option>Pending</option>
          <option>Completed</option>
          <option>Cancelled</option>
        </select>
        <select style="width:auto;">
          <option>This Week</option>
          <option>This Month</option>
          <option>Custom Range</option>
        </select>
      </div>

      <div class="table-card">
        <table>
          <thead>
            <tr>
              <th>Candidate</th>
              <th>Date & Time</th>
              <th>Stage</th>
              <th>Interviewers</th>
              <th>Format</th>
              <th>Status</th>
              <th>ATS</th>
              <th></th>
            </tr>
          </thead>
          <tbody id="interviewsTable">
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- Pipeline -->
  <div id="page-pipeline" class="page">
    <div class="topbar">
      <div><div class="topbar-title">Interview Pipeline</div></div>
    </div>
    <div class="content">
      <div class="pipeline-board">
        <div class="pipeline-col">
          <div class="pipeline-col-header">
            <div class="col-bar" style="background:#6D28D9"></div>
            <span class="pipeline-col-title">HR Screening</span>
            <span class="pipeline-col-count">5</span>
          </div>
          <div class="pipeline-cards">
            <div class="pipeline-card" onclick="openInterviewModal('Divya Sharma')">
              <div class="pc-name">Divya Sharma</div>
              <div class="pc-role">UX Designer</div>
              <div class="pc-meta">
                <span class="badge badge-hr" style="font-size:10.5px;">HR</span>
                <span style="font-size:11px;color:var(--text-muted)">May 17</span>
              </div>
            </div>
            <div class="pipeline-card" onclick="openInterviewModal('Kenji Tanaka')">
              <div class="pc-name">Kenji Tanaka</div>
              <div class="pc-role">iOS Developer</div>
              <div class="pc-meta">
                <span class="badge badge-hr" style="font-size:10.5px;">HR</span>
                <span style="font-size:11px;color:var(--text-muted)">May 18</span>
              </div>
            </div>
            <div class="pipeline-card">
              <div class="pc-name">Fatima Al-Hassan</div>
              <div class="pc-role">ML Engineer</div>
              <div class="pc-meta">
                <span class="badge badge-pending" style="font-size:10.5px;">Pending</span>
              </div>
            </div>
          </div>
        </div>

        <div class="pipeline-col">
          <div class="pipeline-col-header">
            <div class="col-bar" style="background:#059669"></div>
            <span class="pipeline-col-title">Technical Round</span>
            <span class="pipeline-col-count">4</span>
          </div>
          <div class="pipeline-cards">
            <div class="pipeline-card" onclick="openInterviewModal('Priya Mehta')">
              <div class="pc-name">Priya Mehta</div>
              <div class="pc-role">Frontend Engineer</div>
              <div class="pc-meta">
                <span class="badge badge-technical" style="font-size:10.5px;">Technical</span>
                <span style="font-size:11px;color:var(--text-muted)">Today</span>
              </div>
            </div>
            <div class="pipeline-card" onclick="openInterviewModal('Ananya Iyer')">
              <div class="pc-name">Ananya Iyer</div>
              <div class="pc-role">Data Scientist</div>
              <div class="pc-meta">
                <span class="badge badge-scheduled" style="font-size:10.5px;">Scheduled</span>
                <span style="font-size:11px;color:var(--text-muted)">May 16</span>
              </div>
            </div>
          </div>
        </div>

        <div class="pipeline-col">
          <div class="pipeline-col-header">
            <div class="col-bar" style="background:#0891B2"></div>
            <span class="pipeline-col-title">Culture Fit</span>
            <span class="pipeline-col-count">3</span>
          </div>
          <div class="pipeline-cards">
            <div class="pipeline-card" onclick="openInterviewModal('James Okafor')">
              <div class="pc-name">James Okafor</div>
              <div class="pc-role">Product Manager</div>
              <div class="pc-meta">
                <span class="badge badge-culture" style="font-size:10.5px;">Culture</span>
                <span style="font-size:11px;color:var(--text-muted)">Today</span>
              </div>
            </div>
            <div class="pipeline-card">
              <div class="pc-name">Rahul Sharma</div>
              <div class="pc-role">DevOps Engineer</div>
              <div class="pc-meta">
                <span class="badge badge-completed" style="font-size:10.5px;">Completed</span>
              </div>
            </div>
          </div>
        </div>

        <div class="pipeline-col">
          <div class="pipeline-col-header">
            <div class="col-bar" style="background:#1D4ED8"></div>
            <span class="pipeline-col-title">Final Round</span>
            <span class="pipeline-col-count">2</span>
          </div>
          <div class="pipeline-cards">
            <div class="pipeline-card" onclick="openInterviewModal('Marco Rossi')">
              <div class="pc-name">Marco Rossi</div>
              <div class="pc-role">Backend Engineer</div>
              <div class="pc-meta">
                <span class="badge badge-final" style="font-size:10.5px;">Final</span>
                <span style="font-size:11px;color:var(--text-muted)">Today 4 PM</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Candidates -->
  <div id="page-candidates" class="page">
    <div class="topbar">
      <div><div class="topbar-title">Candidates</div></div>
    </div>
    <div class="content">
      <div class="filter-bar">
        <div class="search-input-wrap">
          <i class="ti ti-search"></i>
          <input type="text" class="search-input" placeholder="Search candidates…">
        </div>
      </div>
      <div class="table-card">
        <table>
          <thead>
            <tr>
              <th>Candidate</th>
              <th>Applied Role</th>
              <th>Stage</th>
              <th>Source</th>
              <th>Last Activity</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><div class="candidate-cell"><div class="candidate-avatar" style="background:#6D28D9">PM</div><div><div class="candidate-name">Priya Mehta</div><div class="candidate-role">priya@email.com</div></div></div></td>
              <td>Senior Frontend Engineer</td>
              <td><span class="badge badge-technical">Technical R1</span></td>
              <td style="color:var(--text-muted)">Greenhouse</td>
              <td style="color:var(--text-muted)">Today</td>
              <td><button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))"><i class="ti ti-calendar-plus"></i> Schedule</button></td>
            </tr>
            <tr>
              <td><div class="candidate-cell"><div class="candidate-avatar" style="background:#0891B2">JO</div><div><div class="candidate-name">James Okafor</div><div class="candidate-role">james.o@email.com</div></div></div></td>
              <td>Product Manager</td>
              <td><span class="badge badge-culture">Culture Fit</span></td>
              <td style="color:var(--text-muted)">Workday</td>
              <td style="color:var(--text-muted)">Today</td>
              <td><button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))"><i class="ti ti-calendar-plus"></i> Schedule</button></td>
            </tr>
            <tr>
              <td><div class="candidate-cell"><div class="candidate-avatar" style="background:#059669">AI</div><div><div class="candidate-name">Ananya Iyer</div><div class="candidate-role">ananya@email.com</div></div></div></td>
              <td>Data Scientist</td>
              <td><span class="badge badge-hr">HR Round</span></td>
              <td style="color:var(--text-muted)">Greenhouse</td>
              <td style="color:var(--text-muted)">Yesterday</td>
              <td><button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))"><i class="ti ti-calendar-plus"></i> Schedule</button></td>
            </tr>
            <tr>
              <td><div class="candidate-cell"><div class="candidate-avatar" style="background:#B45309">MR</div><div><div class="candidate-name">Marco Rossi</div><div class="candidate-role">marco@email.com</div></div></div></td>
              <td>Backend Engineer</td>
              <td><span class="badge badge-final">Final Round</span></td>
              <td style="color:var(--text-muted)">Lever</td>
              <td style="color:var(--text-muted)">2 days ago</td>
              <td><button class="btn btn-primary btn-sm" onclick="navigate('schedule', document.querySelector('[data-page="schedule"]'))"><i class="ti ti-calendar-plus"></i> Schedule</button></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ATS Integration -->
  <div id="page-ats" class="page">
    <div class="topbar">
      <div><div class="topbar-title">ATS Integration</div></div>
      <div class="topbar-right">
        <button class="btn btn-secondary btn-sm"><i class="ti ti-refresh"></i> Sync Now</button>
      </div>
    </div>
    <div class="content">

      <div style="background:var(--success-light);border:1px solid rgba(5,150,105,0.2);border-radius:var(--radius);padding:12px 16px;margin-bottom:20px;display:flex;align-items:center;gap:10px;font-size:13px;color:#065F46;">
        <i class="ti ti-circle-check" style="font-size:18px;color:var(--success)"></i>
        <div><strong>2 ATS platforms connected.</strong> Last sync: 2 minutes ago · 48 candidates imported · 0 errors</div>
        <button class="btn btn-ghost btn-sm" style="margin-left:auto;color:var(--success)">View log</button>
      </div>

      <div class="ats-grid">
        <div class="ats-source">
          <div class="ats-header">
            <div class="ats-logo" style="background:#1EB564;border-color:rgba(30,181,100,0.3);font-size:20px;">🌿</div>
            <div>
              <div class="ats-name">Greenhouse</div>
              <div class="ats-status ats-connected">● Connected</div>
            </div>
            <button class="btn btn-ghost btn-sm" style="margin-left:auto;">Configure</button>
          </div>
          <div class="sync-item"><span class="sync-label">Candidates Synced</span><span class="sync-value">31</span></div>
          <div class="sync-item"><span class="sync-label">Open Jobs</span><span class="sync-value">8</span></div>
          <div class="sync-item"><span class="sync-label">Last Sync</span><span class="sync-value">2 min ago</span></div>
          <div class="sync-item"><span class="sync-label">Auto-Sync</span>
            <label class="toggle-switch"><div class="switch"><input type="checkbox" checked><span class="slider-switch"></span></div></label>
          </div>
          <div class="sync-item"><span class="sync-label">Push status updates</span>
            <label class="toggle-switch"><div class="switch"><input type="checkbox" checked><span class="slider-switch"></span></div></label>
          </div>
          <div class="sync-item"><span class="sync-label">Create interviews in Greenhouse</span>
            <label class="toggle-switch"><div class="switch"><input type="checkbox" checked><span class="slider-switch"></span></div></label>
          </div>
          <div style="margin-top:14px;display:flex;gap:8px;">
            <button class="btn btn-secondary btn-sm" style="flex:1;justify-content:center"><i class="ti ti-refresh"></i> Sync Now</button>
            <button class="btn btn-ghost btn-sm" style="color:var(--danger)">Disconnect</button>
          </div>
        </div>

        <div class="ats-source">
          <div class="ats-header">
            <div class="ats-logo" style="background:#1A44C4;border-color:rgba(26,68,196,0.3);font-size:20px;">⚙️</div>
            <div>
              <div class="ats-name">Workday</div>
              <div class="ats-status ats-connected">● Connected</div>
            </div>
            <button class="btn btn-ghost btn-sm" style="margin-left:auto;">Configure</button>
          </div>
          <div class="sync-item"><span class="sync-label">Candidates Synced</span><span class="sync-value">17</span></div>
          <div class="sync-item"><span class="sync-label">Open Jobs</span><span class="sync-value">5</span></div>
          <div class="sync-item"><span class="sync-label">Last Sync</span><span class="sync-value">2 min ago</span></div>
          <div class="sync-item"><span class="sync-label">Auto-Sync</span>
            <label class="toggle-switch"><div class="switch"><input type="checkbox" checked><span class="slider-switch"></span></div></label>
          </div>
          <div class="sync-item"><span class="sync-label">Push status updates</span>
            <label class="toggle-switch"><div class="switch"><input type="checkbox"><span class="slider-switch"></span></div></label>
          </div>
          <div style="margin-top:14px;display:flex;gap:8px;">
            <button class="btn btn-secondary btn-sm" style="flex:1;justify-content:center"><i class="ti ti-refresh"></i> Sync Now</button>
            <button class="btn btn-ghost btn-sm" style="color:var(--danger)">Disconnect</button>
          </div>
        </div>

        <div class="ats-source" style="border-style:dashed;background:var(--bg);opacity:0.8;">
          <div class="ats-header">
            <div class="ats-logo" style="background:#FF5D00;border-color:rgba(255,93,0,0.3);font-size:20px;">🔗</div>
            <div>
              <div class="ats-name">Lever</div>
              <div class="ats-status ats-disconnected">● Disconnected</div>
            </div>
          </div>
          <div style="font-size:13px;color:var(--text-muted);margin-bottom:14px;line-height:1.6;">Connect Lever to automatically import candidates and sync interview schedules.</div>
          <button class="btn btn-primary btn-sm" onclick="showToast('Lever connection flow started')">
            <i class="ti ti-plug-connected"></i> Connect Lever
          </button>
        </div>

        <div class="ats-source" style="border-style:dashed;background:var(--bg);opacity:0.8;">
          <div class="ats-header">
            <div class="ats-logo" style="font-size:20px;border-color:var(--border)">📋</div>
            <div>
              <div class="ats-name">SmartRecruiters</div>
              <div class="ats-status" style="color:var(--text-muted)">Available</div>
            </div>
          </div>
          <div style="font-size:13px;color:var(--text-muted);margin-bottom:14px;line-height:1.6;">Connect SmartRecruiters to streamline your end-to-end hiring process.</div>
          <button class="btn btn-secondary btn-sm" onclick="showToast('SmartRecruiters connection flow started')">
            <i class="ti ti-plug"></i> Connect
          </button>
        </div>
      </div>

      <!-- Webhook section -->
      <div class="section-header"><span class="section-title">Webhooks & API</span></div>
      <div class="form-card">
        <div class="form-grid">
          <div class="form-group">
            <label>API Key</label>
            <div style="display:flex;gap:8px;">
              <input type="password" value="hf_live_sk_abc123xyz789" style="flex:1;font-family:monospace">
              <button class="btn btn-ghost btn-sm"><i class="ti ti-copy"></i></button>
            </div>
          </div>
          <div class="form-group">
            <label>Webhook URL</label>
            <div style="display:flex;gap:8px;">
              <input type="text" value="https://api.ncscheduler.io/webhooks/events" style="flex:1;font-family:monospace;font-size:12px;">
              <button class="btn btn-ghost btn-sm"><i class="ti ti-copy"></i></button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Settings -->
  <div id="page-settings" class="page">
    <div class="topbar">
      <div><div class="topbar-title">Settings</div></div>
    </div>
    <div class="content" style="max-width:680px;">
      <div class="form-card">
        <div style="font-size:14px;font-weight:600;margin-bottom:16px;">Company & Branding</div>
        <div class="form-grid">
          <div class="form-group"><label>Company Name</label><input value="Acme Technologies Pvt. Ltd."></div>
          <div class="form-group"><label>Primary Contact</label><input value="Sarah Rodriguez"></div>
          <div class="form-group form-full"><label>Default Meeting Platform</label>
            <select><option>Google Meet</option><option>Zoom</option><option>Microsoft Teams</option></select>
          </div>
        </div>
      </div>
      <div class="form-card">
        <div style="font-size:14px;font-weight:600;margin-bottom:14px;">Notification Defaults</div>
        <div class="checklist">
          <label class="check-item"><input type="checkbox" checked> Auto-send calendar invites on schedule</label>
          <label class="check-item"><input type="checkbox" checked> 24-hour reminder emails</label>
          <label class="check-item"><input type="checkbox"> 1-hour reminder emails</label>
          <label class="check-item"><input type="checkbox" checked> Notify interviewers of new schedules</label>
          <label class="check-item"><input type="checkbox" checked> Slack notifications for team</label>
        </div>
      </div>
      <div class="form-card">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;">
          <div>
            <div style="font-size:14px;font-weight:600;">Rejection Email Template</div>
            <div style="font-size:12px;color:var(--text-muted);margin-top:2px;">Used when marking candidates as rejected at any interview stage</div>
          </div>
          <button class="btn btn-secondary btn-sm" onclick="openUploadModal()">
            <i class="ti ti-upload"></i> Upload Template
          </button>
        </div>
        <div id="settingsTemplateStatus" style="display:flex;align-items:center;gap:10px;padding:12px 14px;background:var(--success-light);border:1px solid rgba(5,150,105,0.2);border-radius:var(--radius-sm);margin-bottom:14px;">
          <i class="ti ti-circle-check" style="color:var(--success);font-size:18px;"></i>
          <div>
            <div style="font-size:13px;font-weight:500;color:#065F46;">Standard Rejection Email · Active</div>
            <div style="font-size:11.5px;color:#047857;">Last updated: Today · rejection_template_v3.txt</div>
          </div>
          <button class="btn btn-ghost btn-sm" style="margin-left:auto;color:var(--success)" onclick="openUploadModal()"><i class="ti ti-edit"></i> Edit</button>
        </div>
        <div class="form-group" style="margin-bottom:12px;">
          <label>Template Preview</label>
          <div class="email-preview-box" id="settingsTemplatePreview" style="min-height:100px;max-height:160px;cursor:text;" contenteditable="true">Dear {{candidate_name}},

Thank you for your time and interest in the {{role}} position at {{company_name}}. We truly appreciated the opportunity to learn about your background and experience during the {{stage}}.

After careful consideration, we have decided to move forward with other candidates whose experience more closely aligns with our current needs. This was a difficult decision, as we were impressed by your profile.

We encourage you to apply for future openings at {{company_name}} that match your skills and experience.

We wish you all the best in your career journey.

Warm regards,
{{interviewer_name}}
Talent Acquisition Team, {{company_name}}</div>
        </div>
        <div style="display:flex;gap:6px;flex-wrap:wrap;">
          <span class="template-tag" onclick="insertSettingsVar('{{candidate_name}}')">{{candidate_name}}</span>
          <span class="template-tag" onclick="insertSettingsVar('{{role}}')">{{role}}</span>
          <span class="template-tag" onclick="insertSettingsVar('{{stage}}')">{{stage}}</span>
          <span class="template-tag" onclick="insertSettingsVar('{{company_name}}')">{{company_name}}</span>
          <span class="template-tag" onclick="insertSettingsVar('{{interviewer_name}}')">{{interviewer_name}}</span>
        </div>
        <div style="margin-top:14px;" class="form-group">
          <label>Default Subject Line</label>
          <input type="text" id="settingsSubjectTemplate" value="Your application at {{company_name}}">
        </div>
        <div style="margin-top:12px;display:flex;align-items:center;gap:10px;">
          <label class="check-item" style="font-size:12.5px;"><input type="checkbox" checked> Auto-populate rejection email when marking candidate as rejected</label>
        </div>
      </div>
      <div class="form-actions">
        <button class="btn btn-primary" onclick="showToast('Settings saved successfully')"><i class="ti ti-check"></i> Save Settings</button>
      </div>
    </div>
  </div>
</main>

<!-- Rejection Email Modal -->
<div class="modal-overlay" id="rejectionModal" onclick="if(event.target===this) closeRejectionModal()">
  <div class="modal" style="max-width:620px;">
    <div class="modal-header">
      <span class="modal-title" style="color:var(--danger)"><i class="ti ti-mail-x" style="margin-right:6px"></i>Send Rejection Email</span>
      <button class="btn btn-ghost btn-icon btn-sm" onclick="closeRejectionModal()"><i class="ti ti-x"></i></button>
    </div>
    <div class="modal-body">
      <div class="reject-banner">
        <i class="ti ti-alert-triangle"></i>
        <div>Marking <strong id="rejectCandidateName">—</strong> as rejected at <strong id="rejectStageName">—</strong>. This will update their status in the ATS.</div>
      </div>

      <div class="tab-row">
        <button class="tab-btn active" onclick="switchTab('compose', this)">Compose Email</button>
        <button class="tab-btn" onclick="switchTab('preview', this)">Preview</button>
      </div>

      <div id="tab-compose" class="tab-panel active">
        <div class="form-group" style="margin-bottom:12px;">
          <label>From</label>
          <input type="text" value="talent@acmetech.com" style="background:var(--bg);" readonly>
        </div>
        <div class="form-group" style="margin-bottom:12px;">
          <label>To</label>
          <input type="text" id="rejectToField" value="" readonly style="background:var(--bg);">
        </div>
        <div class="form-group" style="margin-bottom:12px;">
          <label>Subject</label>
          <input type="text" id="rejectSubject" value="Your application at Acme Technologies">
        </div>
        <div class="form-group" style="margin-bottom:10px;">
          <label>Email Body</label>
          <textarea id="rejectBody" style="min-height:180px;font-size:13px;line-height:1.75;"></textarea>
        </div>
        <div style="margin-bottom:4px;">
          <div style="font-size:11.5px;color:var(--text-muted);margin-bottom:6px;font-weight:500;">Insert variable</div>
          <div style="display:flex;flex-wrap:wrap;gap:6px;">
            <span class="template-tag" onclick="insertVar('{{candidate_name}}')">{{candidate_name}}</span>
            <span class="template-tag" onclick="insertVar('{{role}}')">{{role}}</span>
            <span class="template-tag" onclick="insertVar('{{stage}}')">{{stage}}</span>
            <span class="template-tag" onclick="insertVar('{{company_name}}')">{{company_name}}</span>
            <span class="template-tag" onclick="insertVar('{{interviewer_name}}')">{{interviewer_name}}</span>
          </div>
        </div>
      </div>

      <div id="tab-preview" class="tab-panel">
        <div style="font-size:11.5px;color:var(--text-muted);margin-bottom:8px;font-weight:500;">Rendered email preview</div>
        <div class="email-preview-box" id="rejectPreviewBox"></div>
      </div>

      <div class="divider"></div>
      <div style="display:flex;align-items:center;gap:10px;">
        <label class="check-item" style="font-size:12.5px;">
          <input type="checkbox" checked id="chkUpdateAts"> Update ATS status to <strong>Rejected</strong>
        </label>
        <label class="check-item" style="font-size:12.5px;">
          <input type="checkbox" id="chkNotifyTeam"> Notify hiring team
        </label>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeRejectionModal()">Cancel</button>
      <button class="btn btn-secondary" onclick="showToast('Draft saved');closeRejectionModal()"><i class="ti ti-device-floppy"></i> Save Draft</button>
      <button class="btn btn-primary" style="background:var(--danger);border-color:var(--danger);" onclick="sendRejection()">
        <i class="ti ti-send"></i> Send Rejection Email
      </button>
    </div>
  </div>
</div>

<!-- Upload Standard Rejection Email Modal -->
<div class="modal-overlay" id="uploadTemplateModal" onclick="if(event.target===this) closeUploadModal()">
  <div class="modal" style="max-width:560px;">
    <div class="modal-header">
      <span class="modal-title"><i class="ti ti-file-upload" style="margin-right:6px;color:var(--accent)"></i>Upload Standard Rejection Email</span>
      <button class="btn btn-ghost btn-icon btn-sm" onclick="closeUploadModal()"><i class="ti ti-x"></i></button>
    </div>
    <div class="modal-body">
      <div style="font-size:13px;color:var(--text-secondary);margin-bottom:16px;line-height:1.7;">
        Upload your company's standard rejection email template. Supported formats: <strong>.txt, .html, .docx</strong>. Variables like <code style="background:var(--bg);padding:1px 5px;border-radius:3px;font-size:12px;">{{candidate_name}}</code> will be auto-filled when sending.
      </div>

      <div class="upload-zone" id="uploadZone" onclick="document.getElementById('templateFileInput').click()"
        ondragover="event.preventDefault();this.classList.add('drag-over')"
        ondragleave="this.classList.remove('drag-over')"
        ondrop="handleTemplateDrop(event)">
        <i class="ti ti-cloud-upload" id="uploadIcon"></i>
        <div id="uploadLabel" style="font-size:13.5px;font-weight:500;color:var(--text-secondary);margin-bottom:4px;">Drop your template file here</div>
        <div id="uploadSub" style="font-size:12px;color:var(--text-muted)">or click to browse — .txt, .html, .docx</div>
        <input type="file" id="templateFileInput" accept=".txt,.html,.docx" style="display:none" onchange="handleTemplateFile(this)">
      </div>

      <div id="templatePasteSection" style="margin-top:16px;">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:10px;">
          <div style="flex:1;height:1px;background:var(--border);"></div>
          <span style="font-size:12px;color:var(--text-muted);">or paste directly</span>
          <div style="flex:1;height:1px;background:var(--border);"></div>
        </div>
        <div class="form-group" style="margin-bottom:10px;">
          <label>Email Subject Template</label>
          <input type="text" id="uploadSubjectField" placeholder="e.g. Your application at {{company_name}}" value="Your application at Acme Technologies">
        </div>
        <div class="form-group">
          <label>Email Body Template</label>
          <textarea id="uploadBodyField" style="min-height:160px;font-size:13px;line-height:1.75;" placeholder="Dear {{candidate_name}},&#10;&#10;Thank you for taking the time to interview for the {{role}} position at {{company_name}}..."></textarea>
        </div>
      </div>

      <div id="templateVariableHint" style="margin-top:12px;padding:10px 13px;background:var(--accent-light);border-radius:var(--radius-sm);border:1px solid rgba(79,70,229,0.15);">
        <div style="font-size:12px;font-weight:600;color:var(--accent-dark);margin-bottom:6px;">Available variables</div>
        <div style="display:flex;flex-wrap:wrap;gap:5px;">
          <span class="template-tag">{{candidate_name}}</span>
          <span class="template-tag">{{role}}</span>
          <span class="template-tag">{{stage}}</span>
          <span class="template-tag">{{company_name}}</span>
          <span class="template-tag">{{interviewer_name}}</span>
        </div>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" onclick="closeUploadModal()">Cancel</button>
      <button class="btn btn-primary" onclick="saveTemplate()"><i class="ti ti-check"></i> Save Template</button>
    </div>
  </div>
</div>

<!-- Interview Detail Modal -->
<div class="modal-overlay" id="interviewModal" onclick="if(event.target===this) closeModal()">
  <div class="modal">
    <div class="modal-header">
      <span class="modal-title" id="modalCandidateName">Priya Mehta</span>
      <button class="btn btn-ghost btn-icon btn-sm" onclick="closeModal()"><i class="ti ti-x"></i></button>
    </div>
    <div class="modal-body">
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:18px;padding:14px;background:var(--bg);border-radius:var(--radius-sm);">
        <div class="candidate-avatar" style="background:#6D28D9;width:44px;height:44px;font-size:14px;" id="modalAvatar">PM</div>
        <div>
          <div style="font-weight:600;font-size:15px;" id="modalName">Priya Mehta</div>
          <div style="font-size:12.5px;color:var(--text-muted);" id="modalRole">Senior Frontend Engineer</div>
          <div style="margin-top:6px;display:flex;gap:6px;flex-wrap:wrap;" id="modalBadges"></div>
        </div>
      </div>
      <div class="form-grid" style="gap:14px;">
        <div><div style="font-size:11px;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:0.05em;margin-bottom:4px;">Date & Time</div>
        <div style="font-size:13.5px;font-weight:500;">Today · 10:00 AM — 10:45 AM</div></div>
        <div><div style="font-size:11px;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:0.05em;margin-bottom:4px;">Format</div>
        <div style="font-size:13.5px;font-weight:500;"><i class="ti ti-video" style="color:var(--accent)"></i> Google Meet</div></div>
        <div><div style="font-size:11px;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:0.05em;margin-bottom:4px;">Interviewer(s)</div>
        <div style="font-size:13.5px;font-weight:500;">Anil Kumar</div></div>
        <div><div style="font-size:11px;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:0.05em;margin-bottom:4px;">ATS Source</div>
        <div style="font-size:13.5px;font-weight:500;">Greenhouse 🌿</div></div>
      </div>
      <div class="divider"></div>
      <div style="font-size:12.5px;font-weight:600;color:var(--text-muted);text-transform:uppercase;letter-spacing:0.05em;margin-bottom:10px;">Meeting Link</div>
      <div style="display:flex;gap:8px;align-items:center;padding:10px 12px;background:var(--accent-light);border-radius:var(--radius-sm);border:1px solid rgba(79,70,229,0.15);">
        <i class="ti ti-link" style="color:var(--accent)"></i>
        <span style="font-size:13px;color:var(--accent);font-family:monospace;">meet.google.com/xyz-abc-123</span>
        <button class="btn btn-ghost btn-sm btn-icon" style="margin-left:auto" onclick="showToast('Link copied to clipboard')"><i class="ti ti-copy"></i></button>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost" style="color:var(--danger)" onclick="closeModal()"><i class="ti ti-trash"></i> Cancel Interview</button>
      <button class="btn btn-secondary" onclick="closeModal()"><i class="ti ti-edit"></i> Reschedule</button>
      <button class="btn btn-secondary" style="color:var(--danger);border-color:rgba(220,38,38,0.3);" onclick="openRejectionModal()">
        <i class="ti ti-user-x"></i> Mark as Rejected
      </button>
      <button class="btn btn-primary" onclick="showToast('Reminder sent!');closeModal()"><i class="ti ti-send"></i> Send Reminder</button>
    </div>
  </div>
</div>

<!-- Toast Container -->
<div class="toast-container" id="toastContainer"></div>

<script>
// ── Navigation ──
function navigate(pageId, navEl) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + pageId).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  if (navEl) navEl.classList.add('active');
}

// ── Toast ──
function showToast(msg) {
  const c = document.getElementById('toastContainer');
  const t = document.createElement('div');
  t.className = 'toast';
  t.innerHTML = `<i class="ti ti-circle-check"></i>${msg}`;
  c.appendChild(t);
  setTimeout(() => t.remove(), 3100);
}

// ── Modal ──
const avatarColors = {'Priya Mehta':'#6D28D9','James Okafor':'#0891B2','Ananya Iyer':'#059669','Marco Rossi':'#B45309','Divya Sharma':'#D97706','Kenji Tanaka':'#4F46E5'};

function openInterviewModal(name) {
  document.getElementById('modalCandidateName').textContent = name;
  document.getElementById('modalName').textContent = name;
  const av = name.split(' ').map(w=>w[0]).join('');
  document.getElementById('modalAvatar').textContent = av;
  document.getElementById('modalAvatar').style.background = avatarColors[name] || '#6D28D9';
  document.getElementById('interviewModal').classList.add('open');
}

function closeModal() {
  document.getElementById('interviewModal').classList.remove('open');
}

// ── Schedule ──
const interviewerData = {
  'Anil Kumar — Engineering Lead': {av:'AK', color:'#6D28D9'},
  'Lena Chen — Product Director': {av:'LC', color:'#0891B2'},
  'Sarah Rodriguez — Talent Lead': {av:'SR', color:'#059669'},
  'Tanvir Obi — CTO': {av:'TO', color:'#B45309'},
  'Riya Patel — UX Lead': {av:'RP', color:'#D97706'}
};

function addInterviewer(sel) {
  const val = sel.value;
  if (!val) return;
  const d = interviewerData[val];
  if (!d) return;
  const name = val.split(' — ')[0];
  const pill = document.createElement('div');
  pill.className = 'interviewer-pill';
  pill.innerHTML = `<div class="i-av" style="background:${d.color}">${d.av}</div>${name}<i class="ti ti-x" style="font-size:12px;cursor:pointer;color:var(--text-muted)" onclick="this.closest('.interviewer-pill').remove()"></i>`;
  document.getElementById('interviewer-pills').appendChild(pill);
  sel.value = '';
}

function updatePanelPreview() {
  const name = document.getElementById('panelNameInput').value.trim();
  const type = document.getElementById('panelTypeSelect').value;
  const preview = document.getElementById('panelPreview');
  if (name || type) {
    preview.style.display = 'flex';
    document.getElementById('panelPreviewName').textContent = name || type;
    document.getElementById('panelPreviewType').textContent = name && type ? type : (name ? 'No type selected' : '');
  } else {
    preview.style.display = 'none';
  }
}

function clearPanel() {
  document.getElementById('panelNameInput').value = '';
  document.getElementById('panelTypeSelect').value = '';
  document.getElementById('panelPreview').style.display = 'none';
}

function scheduleInterview() {
  const panelName = document.getElementById('panelNameInput').value.trim();
  const panelType = document.getElementById('panelTypeSelect').value;
  const msg = panelName
    ? 'Interview scheduled under panel “' + panelName + '”! Invites sent.'
    : 'Interview scheduled! Invites sent.';
  showToast(msg);
  navigate('dashboard', document.querySelector('[data-page="dashboard"]'));
}

// ── Calendar ──
function buildCalendar() {
  const datesEl = document.getElementById('calDates');
  const today = 15;
  const daysInMonth = 31;
  const startDay = 4; // Thursday (May 1 2025)
  const interviewDays = [8, 12, 13, 14, 15, 16, 19, 20, 22, 23];

  datesEl.innerHTML = '';

  for (let i = 0; i < startDay; i++) {
    const d = document.createElement('div');
    d.className = 'cal-date other-month';
    d.textContent = 30 - startDay + i + 1;
    datesEl.appendChild(d);
  }

  for (let d = 1; d <= daysInMonth; d++) {
    const el = document.createElement('div');
    el.className = 'cal-date' + (d === today ? ' today selected' : '') + (d < today ? ' other-month' : '');
    if (interviewDays.includes(d)) el.classList.add('has-interviews');
    el.textContent = d;
    el.onclick = () => selectDay(d, el);
    datesEl.appendChild(el);
  }
}

const dayInterviews = {
  15: [
    {time:'10:00 AM', name:'Priya Mehta', role:'Frontend Engineer · Technical', color:'#6D28D9'},
    {time:'11:30 AM', name:'James Okafor', role:'Product Manager · Culture Fit', color:'#0891B2'},
    {time:'2:00 PM', name:'Ananya Iyer', role:'Data Scientist · HR Round', color:'#059669'},
    {time:'4:00 PM', name:'Marco Rossi', role:'Backend Engineer · Final Round', color:'#B45309'},
  ],
  16: [
    {time:'9:00 AM', name:'Divya Sharma', role:'UX Designer · HR Screen', color:'#D97706'},
    {time:'11:00 AM', name:'Kenji Tanaka', role:'iOS Dev · Technical', color:'#4F46E5'},
  ],
  19: [
    {time:'10:30 AM', name:'Rahul Sharma', role:'DevOps · Final Round', color:'#DC2626'},
  ]
};

function selectDay(d, el) {
  document.querySelectorAll('.cal-date').forEach(x => x.classList.remove('selected'));
  el.classList.add('selected');
  const months = ['January','February','March','April','May','June','July','August','September','October','November','December'];
  const days = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
  const dt = new Date(2025, 4, d);
  document.getElementById('dayPanelDate').textContent = days[dt.getDay()] + ', ' + d + ' May';
  const slots = dayInterviews[d] || [];
  document.getElementById('dayPanelSub').textContent = slots.length ? `${slots.length} interview${slots.length>1?'s':''} scheduled` : 'No interviews scheduled';
  const slotsEl = document.getElementById('daySlots');
  if (!slots.length) {
    slotsEl.innerHTML = `<div class="empty-slots"><i class="ti ti-calendar-off"></i>No interviews<br><span style="font-size:12px">Schedule one for this day</span></div>`;
    return;
  }
  slotsEl.innerHTML = slots.map(s => `
    <div class="time-slot" onclick="openInterviewModal('${s.name}')">
      <div class="slot-bar" style="background:${s.color}"></div>
      <div class="slot-time">${s.time}</div>
      <div class="slot-info">
        <div class="slot-name">${s.name}</div>
        <div class="slot-role">${s.role}</div>
      </div>
    </div>
  `).join('');
}

// ── All Interviews table ──
const allInterviews = [
  {name:'Priya Mehta', role:'Frontend Engineer', date:'Today 10:00 AM', stage:'Technical', interviewer:'A. Kumar', format:'Meet', status:'scheduled', ats:'Greenhouse'},
  {name:'James Okafor', role:'Product Manager', date:'Today 11:30 AM', stage:'Culture Fit', interviewer:'L. Chen', format:'Zoom', status:'scheduled', ats:'Workday'},
  {name:'Ananya Iyer', role:'Data Scientist', date:'Today 2:00 PM', stage:'HR', interviewer:'S. Rodriguez', format:'Meet', status:'pending', ats:'Greenhouse'},
  {name:'Marco Rossi', role:'Backend Engineer', date:'Today 4:00 PM', stage:'Final', interviewer:'T. Obi', format:'In-Person', status:'scheduled', ats:'Lever'},
  {name:'Divya Sharma', role:'UX Designer', date:'May 17 9:00 AM', stage:'HR', interviewer:'R. Patel', format:'Meet', status:'scheduled', ats:'Greenhouse'},
  {name:'Kenji Tanaka', role:'iOS Developer', date:'May 18 11:00 AM', stage:'Technical', interviewer:'A. Kumar', format:'Zoom', status:'pending', ats:'Workday'},
  {name:'Rahul Sharma', role:'DevOps Engineer', date:'May 12 3:00 PM', stage:'Culture Fit', interviewer:'L. Chen', format:'Meet', status:'completed', ats:'Greenhouse'},
  {name:'Eva Nguyen', role:'ML Engineer', date:'May 10 10:00 AM', stage:'Final', interviewer:'T. Obi', format:'Meet', status:'cancelled', ats:'Workday'},
];

const avatarBg = ['#6D28D9','#0891B2','#059669','#B45309','#D97706','#4F46E5','#DC2626','#9D174D'];
const stageBadge = {Technical:'badge-technical', 'Culture Fit':'badge-culture', HR:'badge-hr', Final:'badge-final'};
const statusBadge = {scheduled:'badge-scheduled', pending:'badge-pending', completed:'badge-completed', cancelled:'badge-cancelled'};

function buildInterviewsTable() {
  const tbody = document.getElementById('interviewsTable');
  tbody.innerHTML = allInterviews.map((iv, i) => {
    const av = iv.name.split(' ').map(w=>w[0]).join('');
    return `<tr onclick="openInterviewModal('${iv.name}')">
      <td><div class="candidate-cell"><div class="candidate-avatar" style="background:${avatarBg[i]}">${av}</div><div><div class="candidate-name">${iv.name}</div><div class="candidate-role">${iv.role}</div></div></div></td>
      <td style="color:var(--text-secondary);font-size:12.5px;">${iv.date}</td>
      <td><span class="badge ${stageBadge[iv.stage]||'badge-hr'}">${iv.stage}</span></td>
      <td style="color:var(--text-secondary)">${iv.interviewer}</td>
      <td style="color:var(--text-secondary)">${iv.format}</td>
      <td><span class="badge ${statusBadge[iv.status]}">${iv.status.charAt(0).toUpperCase()+iv.status.slice(1)}</span></td>
      <td style="font-size:12px;color:var(--text-muted)">${iv.ats}</td>
      <td><button class="btn btn-ghost btn-icon btn-sm"><i class="ti ti-dots-vertical"></i></button></td>
    </tr>`;
  }).join('');
}

// ── Init ──
buildCalendar();
selectDay(15, document.querySelector('.cal-date.today'));
buildInterviewsTable();

// ── Rejection Email ──
let currentRejectCandidate = '';
let currentRejectStage = 'Technical Round';

const defaultTemplate = `Dear {{candidate_name}},

Thank you for your time and interest in the {{role}} position at {{company_name}}. We truly appreciated the opportunity to learn about your background and experience during the {{stage}}.

After careful consideration, we have decided to move forward with other candidates whose experience more closely aligns with our current needs. This was a difficult decision, as we were impressed by your profile.

We encourage you to apply for future openings at {{company_name}} that match your skills and experience.

We wish you all the best in your career journey.

Warm regards,
{{interviewer_name}}
Talent Acquisition Team, {{company_name}}`;

function getTemplate() {
  const settings = document.getElementById('settingsTemplatePreview');
  return settings ? settings.innerText : defaultTemplate;
}

function getSubjectTemplate() {
  const el = document.getElementById('settingsSubjectTemplate');
  return el ? el.value : 'Your application at {{company_name}}';
}

function fillTemplate(tpl, name, role, stage) {
  return tpl
    .replace(/{{candidate_name}}/g, name)
    .replace(/{{role}}/g, role)
    .replace(/{{stage}}/g, stage)
    .replace(/{{company_name}}/g, 'Acme Technologies')
    .replace(/{{interviewer_name}}/g, 'Sarah Rodriguez');
}

function openRejectionModal() {
  const name = document.getElementById('modalName').textContent || 'Candidate';
  currentRejectCandidate = name;
  closeModal();
  document.getElementById('rejectCandidateName').textContent = name;
  document.getElementById('rejectStageName').textContent = currentRejectStage;
  document.getElementById('rejectToField').value = name.toLowerCase().replace(' ', '.') + '@email.com';
  const role = 'the open position';
  const bodyTpl = getTemplate();
  const subjTpl = getSubjectTemplate();
  document.getElementById('rejectBody').value = fillTemplate(bodyTpl, name, role, currentRejectStage);
  document.getElementById('rejectSubject').value = fillTemplate(subjTpl, name, role, currentRejectStage);
  switchTab('compose', document.querySelector('#rejectionModal .tab-btn'));
  document.getElementById('rejectionModal').classList.add('open');
}

function closeRejectionModal() {
  document.getElementById('rejectionModal').classList.remove('open');
}

function sendRejection() {
  closeRejectionModal();
  showToast('Rejection email sent to ' + currentRejectCandidate);
}

function switchTab(tabId, btn) {
  const modal = btn.closest('.modal');
  modal.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  modal.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  btn.classList.add('active');
  modal.querySelector('#tab-' + tabId).classList.add('active');
  if (tabId === 'preview') {
    const body = document.getElementById('rejectBody').value;
    document.getElementById('rejectPreviewBox').textContent = body;
  }
}

function insertVar(v) {
  const ta = document.getElementById('rejectBody');
  const start = ta.selectionStart, end = ta.selectionEnd;
  ta.value = ta.value.slice(0, start) + v + ta.value.slice(end);
  ta.selectionStart = ta.selectionEnd = start + v.length;
  ta.focus();
}

function insertSettingsVar(v) {
  const el = document.getElementById('settingsTemplatePreview');
  el.focus();
  const sel = window.getSelection();
  if (sel && sel.rangeCount) {
    const range = sel.getRangeAt(0);
    range.deleteContents();
    range.insertNode(document.createTextNode(v));
    range.collapse(false);
    sel.removeAllRanges();
    sel.addRange(range);
  } else {
    el.textContent += v;
  }
}

// ── Upload Template Modal ──
function openUploadModal() {
  document.getElementById('uploadTemplateModal').classList.add('open');
}

function closeUploadModal() {
  document.getElementById('uploadTemplateModal').classList.remove('open');
}

function handleTemplateFile(input) {
  const file = input.files[0];
  if (!file) return;
  const zone = document.getElementById('uploadZone');
  zone.classList.add('has-file');
  document.getElementById('uploadIcon').className = 'ti ti-circle-check';
  document.getElementById('uploadLabel').textContent = file.name;
  document.getElementById('uploadSub').textContent = (file.size / 1024).toFixed(1) + ' KB · Click to replace';
  const reader = new FileReader();
  reader.onload = e => {
    document.getElementById('uploadBodyField').value = e.target.result;
  };
  reader.readAsText(file);
}

function handleTemplateDrop(e) {
  e.preventDefault();
  document.getElementById('uploadZone').classList.remove('drag-over');
  const file = e.dataTransfer.files[0];
  if (file) {
    const dt = new DataTransfer();
    dt.items.add(file);
    document.getElementById('templateFileInput').files = dt.files;
    handleTemplateFile(document.getElementById('templateFileInput'));
  }
}

function saveTemplate() {
  const body = document.getElementById('uploadBodyField').value.trim();
  const subj = document.getElementById('uploadSubjectField').value.trim();
  if (body) {
    document.getElementById('settingsTemplatePreview').innerText = body;
  }
  if (subj) {
    document.getElementById('settingsSubjectTemplate').value = subj;
  }
  closeUploadModal();
  showToast('Rejection email template saved!');
}

</script>
</body>
</html>
