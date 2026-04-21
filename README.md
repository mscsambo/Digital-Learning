<html lang="km">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ប្រព័ន្ធគ្រប់គ្រងបុគ្គលិក | Employee Management System</title>
<link href="https://fonts.googleapis.com/css2?family=Hanuman:wght@100;300;400;700;900&family=Kantumruy+Pro:wght@300;400;500;600;700&family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
:root {
  --primary: #1a3a5c;
  --primary-light: #1e4d78;
  --accent: #e8a020;
  --accent-light: #f5b942;
  --danger: #e53e3e;
  --success: #38a169;
  --warning: #d69e2e;
  --info: #3182ce;
  --bg: #f0f4f8;
  --surface: #ffffff;
  --surface2: #f7fafc;
  --border: #e2e8f0;
  --text: #1a202c;
  --text-muted: #718096;
  --shadow: 0 4px 24px rgba(26,58,92,0.10);
  --shadow-lg: 0 8px 40px rgba(26,58,92,0.18);
  --radius: 14px;
  --radius-sm: 8px;
  --sidebar-w: 260px;
  --header-h: 64px;
  --font-km: 'Kantumruy Pro', 'Hanuman', serif;
  --font-en: 'DM Sans', sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--font-km);background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}
body.lang-en{font-family:var(--font-en)}

/* ========== LOGIN ========== */
#loginPage{
  display:flex;align-items:center;justify-content:center;
  min-height:100vh;
  background: linear-gradient(135deg, #0f2744 0%, #1a3a5c 40%, #1e5280 70%, #e8a020 100%);
  position:relative;overflow:hidden;
}
#loginPage::before{
  content:'';position:absolute;inset:0;
  background: radial-gradient(ellipse at 20% 50%, rgba(232,160,32,0.18) 0%, transparent 60%),
              radial-gradient(ellipse at 80% 20%, rgba(30,82,128,0.3) 0%, transparent 50%);
}
.login-bg-shape{
  position:absolute;width:600px;height:600px;border-radius:50%;
  border:1px solid rgba(255,255,255,0.06);
  top:-100px;right:-100px;pointer-events:none;
}
.login-bg-shape:nth-child(2){width:400px;height:400px;bottom:-80px;left:-80px;border-color:rgba(232,160,32,0.1)}
.login-card{
  position:relative;z-index:2;
  background:rgba(255,255,255,0.97);
  border-radius:24px;
  padding:50px 44px;
  width:420px;
  box-shadow: 0 30px 80px rgba(0,0,0,0.35), 0 0 0 1px rgba(255,255,255,0.15);
  animation: loginSlide 0.6s cubic-bezier(.22,.68,0,1.2) both;
}
@keyframes loginSlide{from{opacity:0;transform:translateY(40px) scale(.97)}to{opacity:1;transform:none}}
.login-logo{
  text-align:center;margin-bottom:32px;
}
.login-logo .logo-icon{
  width:72px;height:72px;
  background: linear-gradient(135deg, var(--primary), var(--accent));
  border-radius:20px;margin:0 auto 16px;
  display:flex;align-items:center;justify-content:center;
  font-size:32px;color:#fff;
  box-shadow:0 8px 24px rgba(26,58,92,0.3);
}
.login-logo h1{font-size:1.5rem;color:var(--primary);font-weight:700;line-height:1.3}
.login-logo p{color:var(--text-muted);font-size:.85rem;margin-top:4px}
.lang-toggle{
  display:flex;gap:8px;justify-content:center;margin-bottom:24px;
}
.lang-btn{
  padding:6px 18px;border-radius:20px;border:2px solid var(--border);
  background:transparent;cursor:pointer;font-size:.82rem;font-weight:600;
  color:var(--text-muted);transition:.2s;font-family:inherit;
}
.lang-btn.active{background:var(--primary);color:#fff;border-color:var(--primary)}
.form-group{margin-bottom:18px}
.form-group label{display:block;font-size:.82rem;font-weight:600;color:var(--primary);margin-bottom:6px}
.form-group .input-wrap{position:relative}
.form-group .input-wrap i{
  position:absolute;left:14px;top:50%;transform:translateY(-50%);
  color:var(--text-muted);font-size:.9rem;
}
.form-group input{
  width:100%;padding:12px 14px 12px 42px;
  border:2px solid var(--border);border-radius:var(--radius-sm);
  font-size:.92rem;font-family:inherit;
  transition:.2s;background:var(--surface2);color:var(--text);
}
.form-group input:focus{outline:none;border-color:var(--primary);background:#fff}
.btn-login{
  width:100%;padding:14px;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color:#fff;border:none;border-radius:var(--radius-sm);
  font-size:1rem;font-weight:700;cursor:pointer;font-family:inherit;
  transition:.2s;margin-top:4px;
  box-shadow:0 4px 16px rgba(26,58,92,0.3);
}
.btn-login:hover{transform:translateY(-1px);box-shadow:0 8px 24px rgba(26,58,92,0.4)}
.login-footer{text-align:center;margin-top:20px;color:var(--text-muted);font-size:.78rem}

/* ========== APP LAYOUT ========== */
#app{display:none;min-height:100vh}

/* SIDEBAR */
.sidebar{
  position:fixed;left:0;top:0;bottom:0;width:var(--sidebar-w);
  background: linear-gradient(180deg, #0f2744 0%, #1a3a5c 60%, #16334f 100%);
  z-index:100;display:flex;flex-direction:column;
  box-shadow: 4px 0 24px rgba(0,0,0,0.18);
  transition:.3s;
}
.sidebar-logo{
  padding:22px 20px 18px;border-bottom:1px solid rgba(255,255,255,0.08);
  display:flex;align-items:center;gap:12px;
}
.sidebar-logo .logo-mark{
  width:40px;height:40px;border-radius:10px;
  background:linear-gradient(135deg,var(--accent),#f5b942);
  display:flex;align-items:center;justify-content:center;
  font-size:18px;color:#fff;flex-shrink:0;
  box-shadow:0 4px 12px rgba(232,160,32,0.4);
}
.sidebar-logo .logo-text{color:#fff}
.sidebar-logo .logo-text h2{font-size:.88rem;font-weight:700;line-height:1.2}
.sidebar-logo .logo-text p{font-size:.7rem;color:rgba(255,255,255,0.5);margin-top:2px}
.sidebar-nav{flex:1;overflow-y:auto;padding:12px 0}
.sidebar-nav::-webkit-scrollbar{width:4px}
.sidebar-nav::-webkit-scrollbar-track{background:transparent}
.sidebar-nav::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.15);border-radius:2px}
.nav-section{padding:8px 16px 4px;font-size:.65rem;font-weight:700;
  color:rgba(255,255,255,0.35);letter-spacing:.1em;text-transform:uppercase}
.nav-item{
  display:flex;align-items:center;gap:12px;
  padding:11px 20px;cursor:pointer;
  color:rgba(255,255,255,0.7);font-size:.82rem;font-weight:500;
  transition:.2s;border-left:3px solid transparent;margin:1px 0;
  position:relative;
}
.nav-item:hover{background:rgba(255,255,255,0.07);color:#fff}
.nav-item.active{
  background:rgba(232,160,32,0.15);color:#fff;
  border-left-color:var(--accent);
}
.nav-item i{width:18px;text-align:center;font-size:.9rem;flex-shrink:0}
.nav-badge{
  margin-left:auto;background:var(--accent);color:#fff;
  font-size:.62rem;font-weight:700;
  padding:2px 7px;border-radius:10px;
}
.sidebar-bottom{
  padding:16px;border-top:1px solid rgba(255,255,255,0.08);
}
.sidebar-user{
  display:flex;align-items:center;gap:10px;padding:10px 12px;
  border-radius:var(--radius-sm);background:rgba(255,255,255,0.07);cursor:pointer;
}
.sidebar-user .avatar{
  width:36px;height:36px;border-radius:50%;
  background:linear-gradient(135deg,var(--accent),#e07010);
  display:flex;align-items:center;justify-content:center;
  font-size:.9rem;color:#fff;font-weight:700;flex-shrink:0;
  overflow:hidden;
}
.sidebar-user .avatar img{width:100%;height:100%;object-fit:cover}
.sidebar-user .uinfo{flex:1;min-width:0}
.sidebar-user .uinfo .uname{color:#fff;font-size:.78rem;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.sidebar-user .uinfo .urole{color:rgba(255,255,255,0.45);font-size:.65rem}

/* HEADER */
.header{
  position:fixed;top:0;left:var(--sidebar-w);right:0;height:var(--header-h);
  background:#fff;border-bottom:1px solid var(--border);
  display:flex;align-items:center;padding:0 24px;gap:16px;
  z-index:90;box-shadow:0 2px 12px rgba(0,0,0,0.06);
}
.header-title{font-size:1.05rem;font-weight:700;color:var(--primary);flex:1}
.header-title span{font-size:.75rem;color:var(--text-muted);font-weight:400;display:block;margin-top:1px}
.header-actions{display:flex;align-items:center;gap:10px}
.hbtn{
  width:38px;height:38px;border-radius:var(--radius-sm);
  border:1px solid var(--border);background:#fff;
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:var(--text-muted);font-size:.85rem;
  transition:.2s;position:relative;
}
.hbtn:hover{background:var(--bg);color:var(--primary)}
.hbtn .notif-dot{
  position:absolute;top:6px;right:6px;
  width:8px;height:8px;border-radius:50%;
  background:var(--danger);border:2px solid #fff;
}
.lang-switch{
  display:flex;border:1px solid var(--border);border-radius:var(--radius-sm);overflow:hidden;
}
.lang-switch button{
  padding:6px 12px;border:none;background:#fff;
  font-size:.75rem;font-weight:600;cursor:pointer;
  color:var(--text-muted);font-family:inherit;transition:.2s;
}
.lang-switch button.active{background:var(--primary);color:#fff}

/* MAIN CONTENT */
.main{
  margin-left:var(--sidebar-w);margin-top:var(--header-h);
  padding:28px 28px 40px;min-height:calc(100vh - var(--header-h));
}
.page{display:none}
.page.active{display:block;animation:fadeIn .3s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

/* CARDS & STATS */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:18px;margin-bottom:28px}
.stat-card{
  background:#fff;border-radius:var(--radius);padding:22px;
  box-shadow:var(--shadow);border:1px solid var(--border);
  position:relative;overflow:hidden;
}
.stat-card::after{
  content:'';position:absolute;top:-20px;right:-20px;
  width:80px;height:80px;border-radius:50%;opacity:.08;
}
.stat-card.blue::after{background:var(--primary)}
.stat-card.gold::after{background:var(--accent)}
.stat-card.green::after{background:var(--success)}
.stat-card.red::after{background:var(--danger)}
.stat-card .stat-icon{
  width:46px;height:46px;border-radius:12px;
  display:flex;align-items:center;justify-content:center;
  font-size:1.1rem;margin-bottom:14px;
}
.stat-card.blue .stat-icon{background:rgba(26,58,92,.1);color:var(--primary)}
.stat-card.gold .stat-icon{background:rgba(232,160,32,.12);color:var(--accent)}
.stat-card.green .stat-icon{background:rgba(56,161,105,.1);color:var(--success)}
.stat-card.red .stat-icon{background:rgba(229,62,62,.1);color:var(--danger)}
.stat-card .stat-val{font-size:1.9rem;font-weight:800;color:var(--primary);line-height:1}
.stat-card .stat-label{font-size:.75rem;color:var(--text-muted);margin-top:6px;font-weight:500}
.stat-card .stat-change{
  font-size:.72rem;margin-top:8px;font-weight:600;
}
.stat-card .stat-change.up{color:var(--success)}
.stat-card .stat-change.down{color:var(--danger)}

/* TABLE */
.card{
  background:#fff;border-radius:var(--radius);
  box-shadow:var(--shadow);border:1px solid var(--border);
  overflow:hidden;margin-bottom:22px;
}
.card-header{
  padding:18px 22px;border-bottom:1px solid var(--border);
  display:flex;align-items:center;gap:12px;flex-wrap:wrap;
}
.card-header h3{font-size:.95rem;font-weight:700;color:var(--primary);flex:1}
.card-body{padding:22px}
.table-wrap{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:.82rem}
thead th{
  padding:10px 14px;text-align:left;
  background:var(--bg);color:var(--primary);
  font-weight:700;font-size:.75rem;
  border-bottom:2px solid var(--border);white-space:nowrap;
}
tbody td{
  padding:11px 14px;border-bottom:1px solid var(--border);
  color:var(--text);vertical-align:middle;
}
tbody tr:hover{background:var(--bg)}
tbody tr:last-child td{border-bottom:none}
.emp-name{display:flex;align-items:center;gap:10px}
.emp-avatar{
  width:34px;height:34px;border-radius:50%;
  background:linear-gradient(135deg,var(--primary),var(--accent));
  display:flex;align-items:center;justify-content:center;
  color:#fff;font-weight:700;font-size:.78rem;flex-shrink:0;
  overflow:hidden;
}
.emp-avatar img{width:100%;height:100%;object-fit:cover}
.badge{
  display:inline-flex;align-items:center;gap:4px;
  padding:3px 10px;border-radius:20px;font-size:.68rem;font-weight:700;
}
.badge-green{background:rgba(56,161,105,.12);color:var(--success)}
.badge-red{background:rgba(229,62,62,.1);color:var(--danger)}
.badge-gold{background:rgba(232,160,32,.12);color:#b7791f}
.badge-blue{background:rgba(49,130,206,.1);color:var(--info)}
.badge-gray{background:var(--bg);color:var(--text-muted)}

/* BUTTONS */
.btn{
  display:inline-flex;align-items:center;gap:6px;
  padding:8px 16px;border-radius:var(--radius-sm);
  font-size:.8rem;font-weight:600;cursor:pointer;
  border:none;font-family:inherit;transition:.2s;
}
.btn-primary{background:var(--primary);color:#fff}
.btn-primary:hover{background:var(--primary-light)}
.btn-accent{background:var(--accent);color:#fff}
.btn-accent:hover{background:var(--accent-light)}
.btn-success{background:var(--success);color:#fff}
.btn-danger{background:var(--danger);color:#fff}
.btn-outline{background:#fff;color:var(--primary);border:1.5px solid var(--border)}
.btn-outline:hover{border-color:var(--primary);background:var(--bg)}
.btn-sm{padding:5px 12px;font-size:.73rem}
.btn-icon{width:32px;height:32px;padding:0;justify-content:center}

/* SEARCH & FILTER */
.search-bar{
  position:relative;flex:1;min-width:160px;
}
.search-bar i{
  position:absolute;left:12px;top:50%;transform:translateY(-50%);
  color:var(--text-muted);font-size:.85rem;
}
.search-bar input{
  width:100%;padding:8px 12px 8px 36px;
  border:1.5px solid var(--border);border-radius:var(--radius-sm);
  font-size:.82rem;font-family:inherit;background:var(--bg);
  transition:.2s;
}
.search-bar input:focus{outline:none;border-color:var(--primary);background:#fff}

/* FORMS */
.form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:18px}
.form-field label{display:block;font-size:.78rem;font-weight:600;color:var(--primary);margin-bottom:5px}
.form-field input,.form-field select,.form-field textarea{
  width:100%;padding:9px 12px;
  border:1.5px solid var(--border);border-radius:var(--radius-sm);
  font-size:.82rem;font-family:inherit;background:var(--bg);
  transition:.2s;color:var(--text);
}
.form-field input:focus,.form-field select:focus,.form-field textarea:focus{
  outline:none;border-color:var(--primary);background:#fff;
}
.form-field textarea{min-height:80px;resize:vertical}
.section-title{
  font-size:.82rem;font-weight:800;color:var(--primary);
  text-transform:uppercase;letter-spacing:.05em;
  padding:0 0 10px;border-bottom:2px solid var(--border);
  margin-bottom:18px;
}

/* MODAL */
.modal-overlay{
  display:none;position:fixed;inset:0;
  background:rgba(10,20,40,0.55);z-index:200;
  align-items:center;justify-content:center;
  backdrop-filter:blur(4px);
}
.modal-overlay.open{display:flex;animation:fadeIn .2s ease}
.modal{
  background:#fff;border-radius:20px;
  box-shadow:0 30px 80px rgba(0,0,0,0.3);
  width:90%;max-width:680px;max-height:90vh;overflow-y:auto;
  animation:modalIn .3s cubic-bezier(.22,.68,0,1.2);
}
@keyframes modalIn{from{opacity:0;transform:scale(.94) translateY(20px)}to{opacity:1;transform:none}}
.modal-header{
  padding:22px 26px;border-bottom:1px solid var(--border);
  display:flex;align-items:center;gap:12px;
}
.modal-header h3{font-size:1rem;font-weight:700;color:var(--primary);flex:1}
.modal-body{padding:26px}
.modal-footer{
  padding:16px 26px;border-top:1px solid var(--border);
  display:flex;justify-content:flex-end;gap:10px;
}

/* PHOTO UPLOAD */
.photo-upload{
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  width:120px;height:160px;border:2px dashed var(--border);
  border-radius:var(--radius-sm);cursor:pointer;
  background:var(--bg);color:var(--text-muted);
  font-size:.72rem;text-align:center;gap:8px;
  transition:.2s;position:relative;overflow:hidden;
}
.photo-upload:hover{border-color:var(--primary);color:var(--primary)}
.photo-upload img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover}
.photo-upload input{display:none}

/* EMPLOYEE CARD */
.emp-card-preview{
  background: linear-gradient(135deg, #0f2744 0%, #1a3a5c 60%, #16334f 100%);
  border-radius:16px;padding:24px;color:#fff;
  position:relative;overflow:hidden;width:340px;
  box-shadow:var(--shadow-lg);
}
.emp-card-preview::before{
  content:'';position:absolute;
  width:200px;height:200px;border-radius:50%;
  background:rgba(232,160,32,0.1);
  top:-60px;right:-40px;
}
.emp-card-preview .card-flag{
  width:30px;height:20px;background:url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 3 2"><rect width="3" height="2" fill="%23032ea1"/><path d="M0 .5L1.5 1.8L3 .5L1.5 0z" fill="%23e00025"/></svg>') center/cover;
  border-radius:2px;position:absolute;top:16px;right:16px;
}
.emp-card-preview .card-logo{
  font-size:.7rem;font-weight:700;color:var(--accent);
  letter-spacing:.05em;margin-bottom:16px;
}
.emp-card-preview .card-photo{
  width:72px;height:96px;border-radius:8px;
  background:rgba(255,255,255,.15);
  border:2px solid rgba(232,160,32,.4);
  overflow:hidden;margin-bottom:12px;
}
.emp-card-preview .card-photo img{width:100%;height:100%;object-fit:cover}
.emp-card-preview .card-name{font-size:1rem;font-weight:700}
.emp-card-preview .card-pos{font-size:.72rem;color:rgba(255,255,255,.65);margin-top:3px}
.emp-card-preview .card-info{
  margin-top:14px;display:grid;grid-template-columns:1fr 1fr;gap:8px;
}
.emp-card-preview .card-info-item .ci-label{font-size:.6rem;color:rgba(255,255,255,.4);font-weight:600;text-transform:uppercase}
.emp-card-preview .card-info-item .ci-val{font-size:.73rem;font-weight:600;color:#fff;margin-top:2px}
.emp-card-preview .card-barcode{
  height:30px;margin-top:14px;
  background: repeating-linear-gradient(90deg, rgba(255,255,255,.7) 0, rgba(255,255,255,.7) 2px, transparent 2px, transparent 5px);
  border-radius:2px;
}

/* ATTENDANCE */
.attend-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-top:12px}
.attend-day{
  aspect-ratio:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
  border-radius:8px;font-size:.65rem;font-weight:600;cursor:pointer;
  border:1.5px solid var(--border);background:var(--bg);
  transition:.15s;
}
.attend-day:hover{transform:scale(1.05)}
.attend-day.present{background:rgba(56,161,105,.12);border-color:var(--success);color:var(--success)}
.attend-day.absent{background:rgba(229,62,62,.1);border-color:var(--danger);color:var(--danger)}
.attend-day.holiday{background:rgba(49,130,206,.1);border-color:var(--info);color:var(--info)}
.attend-day.ot{background:rgba(232,160,32,.12);border-color:var(--accent);color:#b7791f}
.attend-day.weekend{background:#f7f7f7;color:#ccc;cursor:default}
.attend-day.today{box-shadow:0 0 0 2px var(--primary)}
.attend-day .ad-num{font-size:.85rem;font-weight:800}

/* SALARY SLIP */
.slip{
  border:2px solid var(--border);border-radius:var(--radius);
  font-size:.82rem;background:#fff;
}
.slip-header{
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color:#fff;padding:22px 26px;border-radius:var(--radius) var(--radius) 0 0;
  display:flex;justify-content:space-between;align-items:center;
}
.slip-section{padding:16px 26px;border-bottom:1px solid var(--border)}
.slip-row{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px dashed var(--border)}
.slip-row:last-child{border:none}
.slip-total{
  background:var(--bg);padding:16px 26px;
  border-radius:0 0 var(--radius) var(--radius);
  display:flex;justify-content:space-between;align-items:center;
}
.slip-total .total-label{font-weight:700;color:var(--primary)}
.slip-total .total-val{font-size:1.2rem;font-weight:800;color:var(--success)}

/* CHARTS placeholder */
.chart-box{
  height:200px;background:var(--bg);border-radius:var(--radius-sm);
  display:flex;align-items:flex-end;gap:6px;padding:16px;
  position:relative;overflow:hidden;
}
.chart-bar{
  flex:1;border-radius:4px 4px 0 0;min-height:4px;
  background: linear-gradient(180deg, var(--accent), var(--primary));
  position:relative;transition:.3s;
}
.chart-bar:hover{opacity:.8}
.chart-bar span{
  position:absolute;top:-18px;left:50%;transform:translateX(-50%);
  font-size:.6rem;font-weight:700;color:var(--primary);white-space:nowrap;
}

/* RESPONSIVE */
@media(max-width:900px){
  :root{--sidebar-w:220px}
}
@media(max-width:700px){
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:none}
  .main{margin-left:0}
  .header{left:0}
  .stats-grid{grid-template-columns:repeat(2,1fr)}
}

/* SCROLLBAR */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:rgba(26,58,92,.2);border-radius:3px}

/* PRINT */
@media print{
  .sidebar,.header,.no-print{display:none!important}
  .main{margin:0;padding:0}
  body{background:#fff}
}

.tabs{display:flex;gap:4px;border-bottom:2px solid var(--border);margin-bottom:20px}
.tab-btn{
  padding:9px 18px;border:none;background:none;cursor:pointer;
  font-size:.82rem;font-weight:600;color:var(--text-muted);font-family:inherit;
  border-bottom:3px solid transparent;margin-bottom:-2px;transition:.2s;
}
.tab-btn.active{color:var(--primary);border-bottom-color:var(--primary)}
.tab-content{display:none}
.tab-content.active{display:block}

.progress-bar{height:6px;background:var(--border);border-radius:3px;overflow:hidden;margin-top:6px}
.progress-fill{height:100%;border-radius:3px;background:linear-gradient(90deg,var(--primary),var(--accent));transition:.4s}

.info-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:14px}
.info-item .ii-label{font-size:.7rem;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:.04em}
.info-item .ii-val{font-size:.88rem;font-weight:600;color:var(--text);margin-top:3px}

.toast{
  position:fixed;bottom:24px;right:24px;z-index:999;
  background:#fff;border-radius:var(--radius-sm);
  padding:14px 20px;box-shadow:var(--shadow-lg);
  border-left:4px solid var(--success);
  display:flex;align-items:center;gap:10px;
  font-size:.83rem;font-weight:600;color:var(--text);
  transform:translateX(120%);transition:.3s cubic-bezier(.22,.68,0,1.2);
  max-width:320px;
}
.toast.show{transform:none}
.toast i{color:var(--success);font-size:1rem}

.dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-right:4px}
.dot-green{background:var(--success)}
.dot-red{background:var(--danger)}
.dot-gold{background:var(--accent)}

select.filter-select{
  padding:7px 12px;border:1.5px solid var(--border);border-radius:var(--radius-sm);
  font-size:.8rem;font-family:inherit;background:#fff;color:var(--text);cursor:pointer;
}
</style>
</head>
<body class="lang-km">

<!-- LOGIN PAGE -->
<div id="loginPage">
  <div class="login-bg-shape"></div>
  <div class="login-bg-shape"></div>
  <div class="login-card">
    <div class="login-logo">
      <div class="logo-icon"><i class="fas fa-building"></i></div>
      <h1 id="loginTitle">ប្រព័ន្ធគ្រប់គ្រងបុគ្គលិក</h1>
      <p id="loginSub">Employee Management System v2.0</p>
    </div>
    <div class="lang-toggle">
      <button class="lang-btn active" onclick="setLang('km',this)" id="loginLangKm">ខ្មែរ</button>
      <button class="lang-btn" onclick="setLang('en',this)" id="loginLangEn">English</button>
    </div>
    <div class="form-group">
      <label id="lbUser">ឈ្មោះអ្នកប្រើប្រាស់</label>
      <div class="input-wrap">
        <i class="fas fa-user"></i>
        <input type="text" id="username" placeholder="admin" value="admin">
      </div>
    </div>
    <div class="form-group">
      <label id="lbPass">ពាក្យសម្ងាត់</label>
      <div class="input-wrap">
        <i class="fas fa-lock"></i>
        <input type="password" id="password" placeholder="••••••••" value="1234">
      </div>
    </div>
    <button class="btn-login" onclick="doLogin()"><span id="lbLoginBtn">ចូលប្រើប្រាស់</span></button>
    <div class="login-footer">admin / 1234 &nbsp;|&nbsp; v2.0 © 2025</div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app">
  <!-- SIDEBAR -->
  <div class="sidebar" id="sidebar">
    <div class="sidebar-logo">
      <div class="logo-mark"><i class="fas fa-building"></i></div>
      <div class="logo-text">
        <h2 id="sb-title">ក្រុមហ៊ុន ABC</h2>
        <p id="sb-sub">គ្រប់គ្រងបុគ្គលិក</p>
      </div>
    </div>
    <div class="sidebar-nav">
      <div class="nav-section t-dashboard">ទំព័រដើម</div>
      <div class="nav-item active" onclick="showPage('dashboard',this)"><i class="fas fa-th-large"></i><span class="t-dashboard">ផ្ទាំងគ្រប់គ្រង</span></div>

      <div class="nav-section t-emp">បុគ្គលិក</div>
      <div class="nav-item" onclick="showPage('employees',this)"><i class="fas fa-users"></i><span class="t-empList">បញ្ជីបុគ្គលិក</span></div>
      <div class="nav-item" onclick="showPage('addEmp',this)"><i class="fas fa-user-plus"></i><span class="t-addEmp">បន្ថែមបុគ្គលិក</span></div>
      <div class="nav-item" onclick="showPage('empCard',this)"><i class="fas fa-id-card"></i><span class="t-empCard">កាតបុគ្គលិក</span></div>

      <div class="nav-section t-attend">វត្តមាន</div>
      <div class="nav-item" onclick="showPage('attendance',this)"><i class="fas fa-calendar-check"></i><span class="t-attendMark">ចុះវត្តមាន</span><span class="nav-badge">ថ្ងៃនេះ</span></div>
      <div class="nav-item" onclick="showPage('attendReport',this)"><i class="fas fa-chart-bar"></i><span class="t-attendReport">របាយការណ៍វត្តមាន</span></div>

      <div class="nav-section t-payroll">ប្រាក់ខែ</div>
      <div class="nav-item" onclick="showPage('overtime',this)"><i class="fas fa-clock"></i><span class="t-overtime">ថែមម៉ោង</span></div>
      <div class="nav-item" onclick="showPage('holiday',this)"><i class="fas fa-umbrella-beach"></i><span class="t-holiday">ឈប់សម្រាក</span></div>
      <div class="nav-item" onclick="showPage('allowance',this)"><i class="fas fa-hand-holding-usd"></i><span class="t-allowance">ប្រាក់ឧបត្ថម្ភ</span></div>
      <div class="nav-item" onclick="showPage('salary',this)"><i class="fas fa-money-bill-wave"></i><span class="t-salary">ប្រាក់បៀវត្ស</span></div>
      <div class="nav-item" onclick="showPage('salaryReport',this)"><i class="fas fa-file-invoice-dollar"></i><span class="t-salaryReport">របាយការណ៍ប្រាក់ខែ</span></div>
      <div class="nav-item" onclick="showPage('otReport',this)"><i class="fas fa-file-alt"></i><span class="t-otReport">របាយការណ៍ថែមម៉ោង</span></div>
    </div>
    <div class="sidebar-bottom">
      <div class="sidebar-user">
        <div class="avatar" id="sbAvatar">A</div>
        <div class="uinfo">
          <div class="uname" id="sbUsername">Administrator</div>
          <div class="urole" id="sbRole">អ្នកគ្រប់គ្រង</div>
        </div>
        <i class="fas fa-sign-out-alt" style="color:rgba(255,255,255,.4);cursor:pointer;font-size:.85rem" onclick="doLogout()" title="Logout"></i>
      </div>
    </div>
  </div>

  <!-- HEADER -->
  <div class="header">
    <div class="header-title" id="headerTitle">ផ្ទាំងគ្រប់គ្រង <span id="headerDate"></span></div>
    <div class="header-actions">
      <div class="lang-switch">
        <button onclick="setLang('km')" id="appLangKm" class="active">ខ្មែរ</button>
        <button onclick="setLang('en')" id="appLangEn">EN</button>
      </div>
      <div class="hbtn" onclick="showPage('attendance',document.querySelector('.nav-item:nth-child(8)'))"><i class="fas fa-bell"></i><div class="notif-dot"></div></div>
      <div class="hbtn"><i class="fas fa-cog"></i></div>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div class="main">

    <!-- DASHBOARD -->
    <div class="page active" id="page-dashboard">
      <div class="stats-grid">
        <div class="stat-card blue">
          <div class="stat-icon"><i class="fas fa-users"></i></div>
          <div class="stat-val" id="totalEmpCount">12</div>
          <div class="stat-label t-totalEmp">បុគ្គលិកសរុប</div>
          <div class="stat-change up">↑ 2 t-thisMonth</div>
        </div>
        <div class="stat-card green">
          <div class="stat-icon"><i class="fas fa-user-check"></i></div>
          <div class="stat-val" id="presentCount">10</div>
          <div class="stat-label t-presentToday">មានវត្តមានថ្ងៃនេះ</div>
          <div class="stat-change up">↑ 83%</div>
        </div>
        <div class="stat-card red">
          <div class="stat-icon"><i class="fas fa-user-times"></i></div>
          <div class="stat-val" id="absentCount">2</div>
          <div class="stat-label t-absentToday">អវត្តមានថ្ងៃនេះ</div>
          <div class="stat-change down">↓ 17%</div>
        </div>
        <div class="stat-card gold">
          <div class="stat-icon"><i class="fas fa-money-bill-wave"></i></div>
          <div class="stat-val">$8,400</div>
          <div class="stat-label t-totalSalary">ប្រាក់ខែសរុប</div>
          <div class="stat-change up">↑ 5%</div>
        </div>
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:22px;flex-wrap:wrap">
        <div class="card" style="grid-column:1/-1">
          <div class="card-header">
            <h3 class="t-recentAttend">វត្តមានថ្ងៃនេះ</h3>
            <button class="btn btn-primary btn-sm" onclick="showPage('attendance')"><i class="fas fa-calendar-check"></i> <span class="t-mark">ចុះ</span></button>
          </div>
          <div class="card-body" style="padding:0">
            <div class="table-wrap">
              <table id="dashTable">
                <thead><tr>
                  <th class="t-empName">ឈ្មោះបុគ្គលិក</th>
                  <th class="t-dept">នាយកដ្ឋាន</th>
                  <th class="t-status">ស្ថានភាព</th>
                  <th class="t-inTime">ម៉ោងចូល</th>
                  <th class="t-outTime">ម៉ោងចេញ</th>
                </tr></thead>
                <tbody id="dashTableBody"></tbody>
              </table>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="card-header"><h3 class="t-monthlyAttend">វត្តមានប្រចាំខែ</h3></div>
          <div class="card-body">
            <div class="chart-box" id="monthChart"></div>
          </div>
        </div>
        <div class="card">
          <div class="card-header"><h3 class="t-salaryDist">ការបែងចែកប្រាក់ខែ</h3></div>
          <div class="card-body">
            <div id="deptList"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- EMPLOYEES LIST -->
    <div class="page" id="page-employees">
      <div class="card">
        <div class="card-header">
          <h3 class="t-empList">បញ្ជីបុគ្គលិក</h3>
          <div class="search-bar"><i class="fas fa-search"></i><input type="text" id="empSearch" placeholder="ស្វែងរក..." oninput="renderEmployeeTable()"></div>
          <select class="filter-select" id="deptFilter" onchange="renderEmployeeTable()">
            <option value="">-- នាយកដ្ឋានទាំងអស់ --</option>
            <option>IT</option><option>HR</option><option>Finance</option><option>Operations</option>
          </select>
          <button class="btn btn-primary" onclick="showPage('addEmp')"><i class="fas fa-plus"></i> <span class="t-addEmp">បន្ថែម</span></button>
          <button class="btn btn-success btn-sm" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
        </div>
        <div class="card-body" style="padding:0">
          <div class="table-wrap">
            <table>
              <thead><tr>
                <th>#</th>
                <th class="t-empName">ឈ្មោះ</th>
                <th class="t-position">តួនាទី</th>
                <th class="t-dept">នាយកដ្ឋាន</th>
                <th class="t-phone">ទូរស័ព្ទ</th>
                <th class="t-salary2">ប្រាក់ខែ</th>
                <th class="t-status">ស្ថានភាព</th>
                <th class="t-action">សកម្មភាព</th>
              </tr></thead>
              <tbody id="empTableBody"></tbody>
            </table>
          </div>
        </div>
      </div>
    </div>

    <!-- ADD EMPLOYEE -->
    <div class="page" id="page-addEmp">
      <div class="card">
        <div class="card-header"><h3 id="addEmpTitle" class="t-addEmpFull">បន្ថែម/កែប្រែបុគ្គលិក</h3></div>
        <div class="card-body">
          <div style="display:flex;gap:28px;flex-wrap:wrap;align-items:flex-start">
            <div>
              <label style="display:block;font-size:.75rem;font-weight:700;color:var(--primary);margin-bottom:8px" class="t-photo">រូបថត (4x6)</label>
              <div class="photo-upload" id="photoUploadArea" onclick="document.getElementById('photoInput').click()">
                <img id="photoPreview" style="display:none">
                <i class="fas fa-camera" id="photoIcon"></i>
                <span id="photoText" class="t-clickUpload">ចុចដើម្បីបញ្ចូលរូប</span>
              </div>
              <input type="file" id="photoInput" accept="image/*" onchange="previewPhoto(this)">
            </div>
            <div style="flex:1;min-width:280px">
              <div class="section-title t-personalInfo">ព័ត៌មានផ្ទាល់ខ្លួន</div>
              <div class="form-grid">
                <div class="form-field"><label class="t-fullName">ឈ្មោះពេញ</label><input type="text" id="fName" placeholder="ចាន់ សុទ្ធា"></div>
                <div class="form-field"><label class="t-nameEn">ឈ្មោះ (English)</label><input type="text" id="fNameEn" placeholder="Chan Sotha"></div>
                <div class="form-field"><label class="t-gender">ភេទ</label>
                  <select id="fGender"><option value="" class="t-select">-- ជ្រើសរើស --</option><option value="ប្រុស" class="t-male">ប្រុស</option><option value="ស្រី" class="t-female">ស្រី</option></select>
                </div>
                <div class="form-field"><label class="t-dob">ថ្ងៃខែឆ្នាំកំណើត</label><input type="date" id="fDob"></div>
                <div class="form-field"><label class="t-national">សញ្ជាតិ</label><input type="text" id="fNational" value="ខ្មែរ"></div>
                <div class="form-field"><label class="t-idCard">លេខអត្តសញ្ញាណប័ណ្ណ</label><input type="text" id="fId" placeholder="012345678"></div>
                <div class="form-field"><label class="t-phone">លេខទូរស័ព្ទ</label><input type="text" id="fPhone" placeholder="012 xxx xxx"></div>
                <div class="form-field"><label>Email</label><input type="email" id="fEmail" placeholder="email@company.com"></div>
                <div class="form-field" style="grid-column:1/-1"><label class="t-address">អាសយដ្ឋាន</label><textarea id="fAddress" placeholder="ផ្ទះ..."></textarea></div>
              </div>
            </div>
          </div>
          <div class="section-title t-jobInfo" style="margin-top:24px">ព័ត៌មានការងារ</div>
          <div class="form-grid">
            <div class="form-field"><label class="t-empId">លេខបុគ្គលិក</label><input type="text" id="fEmpId" placeholder="EMP-001"></div>
            <div class="form-field"><label class="t-position">តួនាទី</label><input type="text" id="fPosition" placeholder="Software Developer"></div>
            <div class="form-field"><label class="t-dept">នាយកដ្ឋាន</label>
              <select id="fDept"><option value="">-- ជ្រើស --</option><option>IT</option><option>HR</option><option>Finance</option><option>Operations</option></select>
            </div>
            <div class="form-field"><label class="t-startDate">ថ្ងៃចាប់ផ្តើមការងារ</label><input type="date" id="fStart"></div>
            <div class="form-field"><label class="t-baseSalary">ប្រាក់ខែមូលដ្ឋាន ($)</label><input type="number" id="fSalary" placeholder="500"></div>
            <div class="form-field"><label class="t-bankAcc">គណនីធនាគារ</label><input type="text" id="fBank" placeholder="ABA - 001234567"></div>
            <div class="form-field"><label class="t-contract">ប្រភេទកិច្ចសន្យា</label>
              <select id="fContract"><option>Full-time</option><option>Part-time</option><option>Contract</option></select>
            </div>
            <div class="form-field"><label class="t-status">ស្ថានភាព</label>
              <select id="fStatus"><option value="Active" class="t-active">Active</option><option value="Inactive" class="t-inactive">Inactive</option></select>
            </div>
          </div>
          <div style="display:flex;gap:10px;justify-content:flex-end;margin-top:24px">
            <button class="btn btn-outline" onclick="clearEmpForm()"><i class="fas fa-times"></i> <span class="t-clear">លុប</span></button>
            <button class="btn btn-primary" onclick="saveEmployee()"><i class="fas fa-save"></i> <span class="t-save">រក្សាទុក</span></button>
          </div>
        </div>
      </div>
    </div>

    <!-- EMPLOYEE CARD -->
    <div class="page" id="page-empCard">
      <div class="card">
        <div class="card-header">
          <h3 class="t-empCard">បង្កើតកាតបុគ្គលិក</h3>
          <select class="filter-select" id="cardEmpSelect" onchange="renderEmpCard()">
            <option value="">-- ជ្រើសបុគ្គលិក --</option>
          </select>
          <button class="btn btn-danger no-print" onclick="printCard()"><i class="fas fa-print"></i> <span class="t-print">បោះពុម្ព</span></button>
          <button class="btn btn-success no-print" onclick="exportCardPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
        </div>
        <div class="card-body">
          <div id="empCardPreview" style="display:inline-block">
            <div class="emp-card-preview" id="theCard">
              <div class="card-flag"></div>
              <div class="card-logo">ABC COMPANY</div>
              <div style="display:flex;gap:16px;align-items:flex-start">
                <div>
                  <div class="card-photo"><img id="cardPhoto" src="" alt="" onerror="this.style.display='none'"></div>
                </div>
                <div style="flex:1">
                  <div class="card-name" id="cardName">-- ជ្រើសបុគ្គលិក --</div>
                  <div class="card-pos" id="cardPos">--</div>
                  <div class="card-info">
                    <div class="card-info-item"><div class="ci-label">ID</div><div class="ci-val" id="cardId">--</div></div>
                    <div class="card-info-item"><div class="ci-label t-dept">Dept</div><div class="ci-val" id="cardDept">--</div></div>
                    <div class="card-info-item"><div class="ci-label t-phone">Tel</div><div class="ci-val" id="cardPhone">--</div></div>
                    <div class="card-info-item"><div class="ci-label t-startDate">Start</div><div class="ci-val" id="cardStart">--</div></div>
                  </div>
                </div>
              </div>
              <div class="card-barcode"></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- ATTENDANCE -->
    <div class="page" id="page-attendance">
      <div class="card">
        <div class="card-header">
          <h3 class="t-attendMark">ចុះវត្តមានប្រចាំថ្ងៃ</h3>
          <input type="date" id="attendDate" class="filter-select" oninput="renderAttendTable()">
          <button class="btn btn-success btn-sm" onclick="saveAllAttend()"><i class="fas fa-save"></i> <span class="t-save">រក្សាទុក</span></button>
          <button class="btn btn-danger btn-sm no-print" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
          <button class="btn btn-success btn-sm no-print" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th>#</th>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-dept">នាយកដ្ឋាន</th>
              <th class="t-status">ស្ថានភាព</th>
              <th class="t-inTime">ម៉ោងចូល</th>
              <th class="t-outTime">ម៉ោងចេញ</th>
              <th class="t-note">ចំណាំ</th>
            </tr></thead>
            <tbody id="attendTableBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ATTENDANCE REPORT -->
    <div class="page" id="page-attendReport">
      <div class="card">
        <div class="card-header">
          <h3 class="t-attendReport">របាយការណ៍វត្តមាន</h3>
          <select class="filter-select" id="arMonth"><option>01</option><option>02</option><option>03</option><option>04</option><option>05</option><option>06</option><option>07</option><option>08</option><option>09</option><option>10</option><option>11</option><option>12</option></select>
          <select class="filter-select" id="arYear"><option>2024</option><option selected>2025</option></select>
          <button class="btn btn-primary btn-sm" onclick="genAttendReport()"><i class="fas fa-sync"></i> <span class="t-generate">បង្កើត</span></button>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
          <button class="btn btn-success btn-sm" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-dept">នាយកដ្ឋាន</th>
              <th class="t-present">ថ្ងៃមក</th>
              <th class="t-absent">ថ្ងៃអវត្តមាន</th>
              <th class="t-late">ចូលយឺត</th>
              <th class="t-ot">ថែមម៉ោង</th>
              <th>%</th>
            </tr></thead>
            <tbody id="arBody"></tbody>
          </table>
        </div>
      </div>
      <div id="monthCalendar" style="margin-top:22px"></div>
    </div>

    <!-- OVERTIME -->
    <div class="page" id="page-overtime">
      <div class="card">
        <div class="card-header">
          <h3 class="t-overtime">ថែមម៉ោង</h3>
          <button class="btn btn-primary" onclick="openOTModal()"><i class="fas fa-plus"></i> <span class="t-addOT">បន្ថែម</span></button>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
          <button class="btn btn-success btn-sm" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-date">កាលបរិច្ឆេទ</th>
              <th class="t-otHours">ម៉ោងថែម</th>
              <th class="t-rate">អត្រា</th>
              <th class="t-amount">ចំនួនទឹកប្រាក់</th>
              <th class="t-reason">មូលហេតុ</th>
              <th class="t-action">សកម្មភាព</th>
            </tr></thead>
            <tbody id="otBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- HOLIDAY WORK -->
    <div class="page" id="page-holiday">
      <div class="card">
        <div class="card-header">
          <h3 class="t-holiday">ថ្ងៃឈប់សម្រាក / ធ្វើការថ្ងៃឈប់</h3>
          <button class="btn btn-primary" onclick="openHolidayModal()"><i class="fas fa-plus"></i> <span class="t-add">បន្ថែម</span></button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-date">កាលបរិច្ឆេទ</th>
              <th class="t-holName">ឈ្មោះថ្ងៃឈប់</th>
              <th class="t-type">ប្រភេទ</th>
              <th class="t-empName">បុគ្គលិក</th>
              <th class="t-pay">ប្រាក់ឈ្នួល</th>
              <th class="t-action">សកម្មភាព</th>
            </tr></thead>
            <tbody id="holidayBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- ALLOWANCE -->
    <div class="page" id="page-allowance">
      <div class="card">
        <div class="card-header">
          <h3 class="t-allowance">ប្រាក់ឧបត្ថម្ភប្រចាំឆ្នាំ</h3>
          <button class="btn btn-primary" onclick="openAllowModal()"><i class="fas fa-plus"></i> <span class="t-add">បន្ថែម</span></button>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-year">ឆ្នាំ</th>
              <th class="t-transport">អ្នកដឹកជញ្ជូន</th>
              <th class="t-food">អាហារ</th>
              <th class="t-health">សុខភាព</th>
              <th class="t-annual">ប្រចាំឆ្នាំ</th>
              <th class="t-total">សរុប</th>
              <th class="t-action">សកម្មភាព</th>
            </tr></thead>
            <tbody id="allowBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- SALARY -->
    <div class="page" id="page-salary">
      <div class="card">
        <div class="card-header">
          <h3 class="t-salary">គណនាប្រាក់បៀវត្ស</h3>
          <select class="filter-select" id="salMonth"><option>01</option><option>02</option><option>03</option><option>04</option><option selected>05</option><option>06</option><option>07</option><option>08</option><option>09</option><option>10</option><option>11</option><option>12</option></select>
          <select class="filter-select" id="salYear"><option>2024</option><option selected>2025</option></select>
          <button class="btn btn-primary" onclick="genSalary()"><i class="fas fa-calculator"></i> <span class="t-calc">គណនា</span></button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-dept">នាយកដ្ឋាន</th>
              <th class="t-baseSalary">ប្រាក់ខែ</th>
              <th class="t-otPay">OT</th>
              <th class="t-allowance2">ឧបត្ថម្ភ</th>
              <th class="t-deduction">កាត់ចេញ</th>
              <th class="t-netSalary">សុទ្ធ</th>
              <th class="t-action">Action</th>
            </tr></thead>
            <tbody id="salBody"></tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- SALARY REPORT -->
    <div class="page" id="page-salaryReport">
      <div class="card">
        <div class="card-header">
          <h3 class="t-salaryReport">របាយការណ៍ប្រាក់ខែ</h3>
          <select class="filter-select" id="srEmp" onchange="showSlip()">
            <option value="">-- ជ្រើសបុគ្គលិក --</option>
          </select>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
          <button class="btn btn-success btn-sm" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
          <button class="btn btn-primary btn-sm" onclick="window.print()"><i class="fas fa-print"></i> <span class="t-print">បោះពុម្ព</span></button>
        </div>
        <div class="card-body" id="slipArea">
          <div style="text-align:center;color:var(--text-muted);padding:40px" class="t-selectEmpFirst">ជ្រើសរើសបុគ្គលិកដើម្បីមើលស្លីប</div>
        </div>
      </div>
    </div>

    <!-- OT REPORT -->
    <div class="page" id="page-otReport">
      <div class="card">
        <div class="card-header">
          <h3 class="t-otReport">របាយការណ៍ថែមម៉ោង</h3>
          <select class="filter-select" id="otrMonth"><option>01</option><option>02</option><option>03</option><option>04</option><option selected>05</option><option>06</option><option>07</option><option>08</option><option>09</option><option>10</option><option>11</option><option>12</option></select>
          <select class="filter-select" id="otrYear"><option>2024</option><option selected>2025</option></select>
          <button class="btn btn-primary btn-sm" onclick="genOTReport()"><i class="fas fa-sync"></i></button>
          <button class="btn btn-danger btn-sm" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
          <button class="btn btn-success btn-sm" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
        </div>
        <div class="card-body" style="padding:0">
          <table>
            <thead><tr>
              <th class="t-empName">ឈ្មោះ</th>
              <th class="t-dept">នាយកដ្ឋាន</th>
              <th class="t-totalOTH">ម៉ោងសរុប</th>
              <th class="t-totalOTPay">ប្រាក់ OT</th>
              <th class="t-times">ចំនួនដង</th>
            </tr></thead>
            <tbody id="otrBody"></tbody>
          </table>
        </div>
      </div>
    </div>

  </div><!-- end main -->
</div><!-- end app -->

<!-- MODALS -->
<div class="modal-overlay" id="empDetailModal">
  <div class="modal" style="max-width:800px">
    <div class="modal-header">
      <h3 class="t-empDetail">ប្រវត្តិរូបបុគ្គលិក</h3>
      <button class="btn btn-outline btn-sm" onclick="closeModal('empDetailModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body" id="empDetailBody"></div>
  </div>
</div>

<div class="modal-overlay" id="otModal">
  <div class="modal">
    <div class="modal-header"><h3 class="t-addOT">បន្ថែមថែមម៉ោង</h3><button class="btn btn-outline btn-sm" onclick="closeModal('otModal')"><i class="fas fa-times"></i></button></div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-field"><label class="t-empName">បុគ្គលិក</label><select id="otEmp"></select></div>
        <div class="form-field"><label class="t-date">ថ្ងៃ</label><input type="date" id="otDate"></div>
        <div class="form-field"><label class="t-otHours">ម៉ោងថែម</label><input type="number" id="otHours" placeholder="2" min="0.5" step="0.5"></div>
        <div class="form-field"><label class="t-rate">អត្រា (x)</label><input type="number" id="otRate" placeholder="1.5" value="1.5" step="0.5"></div>
        <div class="form-field" style="grid-column:1/-1"><label class="t-reason">មូលហេតុ</label><textarea id="otReason" placeholder="..."></textarea></div>
      </div>
    </div>
    <div class="modal-footer"><button class="btn btn-outline" onclick="closeModal('otModal')" class="t-cancel">បោះបង់</button><button class="btn btn-primary" onclick="saveOT()"><i class="fas fa-save"></i> <span class="t-save">រក្សាទុក</span></button></div>
  </div>
</div>

<div class="modal-overlay" id="holidayModal">
  <div class="modal">
    <div class="modal-header"><h3 class="t-holiday">ថ្ងៃឈប់សម្រាក</h3><button class="btn btn-outline btn-sm" onclick="closeModal('holidayModal')"><i class="fas fa-times"></i></button></div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-field"><label class="t-date">ថ្ងៃខែ</label><input type="date" id="holDate"></div>
        <div class="form-field"><label class="t-holName">ឈ្មោះថ្ងៃឈប់</label><input type="text" id="holName" placeholder="ពិធីបុណ្យខ្មែរ"></div>
        <div class="form-field"><label class="t-type">ប្រភេទ</label><select id="holType"><option class="t-publicHol">ថ្ងៃឈប់ជាតិ</option><option class="t-workHol">ធ្វើការ</option></select></div>
        <div class="form-field"><label class="t-empName">បុគ្គលិក</label><select id="holEmp"><option value="all" class="t-allEmp">ទាំងអស់</option></select></div>
        <div class="form-field"><label class="t-pay">ប្រាក់ ($)</label><input type="number" id="holPay" placeholder="0"></div>
      </div>
    </div>
    <div class="modal-footer"><button class="btn btn-outline" onclick="closeModal('holidayModal')">បោះបង់</button><button class="btn btn-primary" onclick="saveHoliday()"><i class="fas fa-save"></i> <span class="t-save">រក្សាទុក</span></button></div>
  </div>
</div>

<div class="modal-overlay" id="allowModal">
  <div class="modal">
    <div class="modal-header"><h3 class="t-allowance">ប្រាក់ឧបត្ថម្ភ</h3><button class="btn btn-outline btn-sm" onclick="closeModal('allowModal')"><i class="fas fa-times"></i></button></div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="form-field"><label class="t-empName">បុគ្គលិក</label><select id="allowEmp"></select></div>
        <div class="form-field"><label class="t-year">ឆ្នាំ</label><input type="number" id="allowYear" value="2025"></div>
        <div class="form-field"><label class="t-transport">ដឹកជញ្ជូន ($)</label><input type="number" id="allowTransport" placeholder="50"></div>
        <div class="form-field"><label class="t-food">អាហារ ($)</label><input type="number" id="allowFood" placeholder="30"></div>
        <div class="form-field"><label class="t-health">សុខភាព ($)</label><input type="number" id="allowHealth" placeholder="20"></div>
        <div class="form-field"><label class="t-annual">ប្រចាំឆ្នាំ ($)</label><input type="number" id="allowAnnual" placeholder="200"></div>
      </div>
    </div>
    <div class="modal-footer"><button class="btn btn-outline" onclick="closeModal('allowModal')">បោះបង់</button><button class="btn btn-primary" onclick="saveAllow()"><i class="fas fa-save"></i> <span class="t-save">រក្សាទុក</span></button></div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"><i class="fas fa-check-circle"></i><span id="toastMsg"></span></div>

<script>
// ==================== DATA ====================
let currentLang = 'km';
let editEmpId = null;

const T = {
  km: {
    dashboard:'ផ្ទាំងគ្រប់គ្រង',empList:'បញ្ជីបុគ្គលិក',addEmp:'បន្ថែមបុគ្គលិក',empCard:'កាតបុគ្គលិក',
    attendMark:'ចុះវត្តមាន',attendReport:'របាយការណ៍វត្តមាន',overtime:'ថែមម៉ោង',
    holiday:'ឈប់សម្រាក',allowance:'ប្រាក់ឧបត្ថម្ភ',salary:'ប្រាក់បៀវត្ស',
    salaryReport:'របាយការណ៍ប្រាក់ខែ',otReport:'របាយការណ៍ថែមម៉ោង',
    empName:'ឈ្មោះបុគ្គលិក',dept:'នាយកដ្ឋាន',status:'ស្ថានភាព',
    save:'រក្សាទុក',cancel:'បោះបង់',delete:'លុប',edit:'កែ',view:'មើល',
    totalEmp:'បុគ្គលិកសរុប',presentToday:'មានវត្តមានថ្ងៃនេះ',absentToday:'អវត្តមានថ្ងៃនេះ',
    totalSalary:'ប្រាក់ខែសរុប',
    saved:'រក្សាទុកដោយជោគជ័យ!',deleted:'លុបដោយជោគជ័យ!',
    present:'មក',absent:'អវត្តមាន',late:'ចូលយឺត',halfday:'កន្លះថ្ងៃ',leave:'ច្បាប់',
    generate:'បង្កើត',calc:'គណនា',print:'បោះពុម្ព',
    thisMonth:'ខែនេះ',recentAttend:'វត្តមានថ្ងៃនេះ',mark:'ចុះ',
    monthlyAttend:'វត្តមានប្រចាំខែ',salaryDist:'ការបែងចែកប្រាក់ខែ',
    addEmpFull:'បន្ថែម / កែប្រែ ព័ត៌មានបុគ្គលិក',
    photo:'រូបថត (4x6)',clickUpload:'ចុចដើម្បីបញ្ចូលរូប',
    personalInfo:'ព័ត៌មានផ្ទាល់ខ្លួន',jobInfo:'ព័ត៌មានការងារ',
    fullName:'ឈ្មោះពេញ',nameEn:'ឈ្មោះ (English)',gender:'ភេទ',dob:'ថ្ងៃខែឆ្នាំកំណើត',
    national:'សញ្ជាតិ',idCard:'អត្តសញ្ញាណប័ណ្ណ',phone:'ទូរស័ព្ទ',address:'អាសយដ្ឋាន',
    empId:'លេខបុគ្គលិក',position:'តួនាទី',startDate:'ថ្ងៃចាប់ផ្តើម',
    baseSalary:'ប្រាក់ខែ ($)',bankAcc:'គណនីធនាគារ',contract:'ប្រភេទកិច្ចសន្យា',
    clear:'លុបទិន្នន័យ',empDetail:'ប្រវត្តិរូបបុគ្គលិក',
    addOT:'បន្ថែមថែមម៉ោង',otHours:'ម៉ោងថែម',rate:'អត្រា',reason:'មូលហេតុ',
    amount:'ចំនួនទឹកប្រាក់',date:'ថ្ងៃ',holName:'ឈ្មោះ',
    publicHol:'ថ្ងៃឈប់ជាតិ',workHol:'ធ្វើការ',allEmp:'ទាំងអស់',pay:'ប្រាក់',
    type:'ប្រភេទ',year:'ឆ្នាំ',transport:'ដឹកជញ្ជូន',food:'អាហារ',
    health:'សុខភាព',annual:'ប្រចាំឆ្នាំ',total:'សរុប',
    baseSalary2:'ប្រាក់ខែ',otPay:'OT',allowance2:'ឧបត្ថម្ភ',deduction:'កាត់',
    netSalary:'សុទ្ធ',action:'ជ្រើស',
    present2:'ថ្ងៃមក',absent2:'ថ្ងៃអវត្តមាន',late2:'ចូលយឺត',ot2:'ថែមម៉ោង',
    totalOTH:'ម៉ោងសរុប',totalOTPay:'ប្រាក់ OT',times:'ចំនួនដង',
    salary2:'ប្រាក់ខែ',inTime:'ម៉ោងចូល',outTime:'ម៉ោងចេញ',note:'ចំណាំ',
    selectEmpFirst:'ជ្រើសរើសបុគ្គលិកដើម្បីមើលស្លីប',
    male:'ប្រុស',female:'ស្រី',active:'Active',inactive:'Inactive',select:'-- ជ្រើស --',
    add:'បន្ថែម',
    sbn:'ប្រព័ន្ធគ្រប់គ្រងបុគ្គលិក',sbs:'គ្រប់គ្រងបុគ្គលិក',
    emp:'បុគ្គលិក',attend:'វត្តមាន',payroll:'ប្រាក់ខែ',
    adminRole:'អ្នកគ្រប់គ្រង',loginTitle:'ប្រព័ន្ធគ្រប់គ្រងបុគ្គលិក',
    loginUser:'ឈ្មោះអ្នកប្រើប្រាស់',loginPass:'ពាក្យសម្ងាត់',loginBtn:'ចូលប្រើប្រាស់',
  },
  en: {
    dashboard:'Dashboard',empList:'Employee List',addEmp:'Add Employee',empCard:'Employee Card',
    attendMark:'Mark Attendance',attendReport:'Attendance Report',overtime:'Overtime',
    holiday:'Holiday',allowance:'Allowance',salary:'Salary',
    salaryReport:'Salary Report',otReport:'OT Report',
    empName:'Employee Name',dept:'Department',status:'Status',
    save:'Save',cancel:'Cancel',delete:'Delete',edit:'Edit',view:'View',
    totalEmp:'Total Employees',presentToday:'Present Today',absentToday:'Absent Today',
    totalSalary:'Total Salary',
    saved:'Saved successfully!',deleted:'Deleted successfully!',
    present:'Present',absent:'Absent',late:'Late',halfday:'Half Day',leave:'Leave',
    generate:'Generate',calc:'Calculate',print:'Print',
    thisMonth:'this month',recentAttend:'Today\'s Attendance',mark:'Mark',
    monthlyAttend:'Monthly Attendance',salaryDist:'Salary Distribution',
    addEmpFull:'Add / Edit Employee Information',
    photo:'Photo (4x6)',clickUpload:'Click to upload photo',
    personalInfo:'Personal Information',jobInfo:'Job Information',
    fullName:'Full Name',nameEn:'Name (English)',gender:'Gender',dob:'Date of Birth',
    national:'Nationality',idCard:'ID Card',phone:'Phone',address:'Address',
    empId:'Employee ID',position:'Position',startDate:'Start Date',
    baseSalary:'Base Salary ($)',bankAcc:'Bank Account',contract:'Contract Type',
    clear:'Clear',empDetail:'Employee Profile',
    addOT:'Add Overtime',otHours:'OT Hours',rate:'Rate',reason:'Reason',
    amount:'Amount',date:'Date',holName:'Holiday Name',
    publicHol:'Public Holiday',workHol:'Work on Holiday',allEmp:'All Employees',pay:'Pay',
    type:'Type',year:'Year',transport:'Transport',food:'Food',
    health:'Health',annual:'Annual Bonus',total:'Total',
    baseSalary2:'Base Salary',otPay:'OT Pay',allowance2:'Allowance',deduction:'Deduction',
    netSalary:'Net Salary',action:'Action',
    present2:'Present Days',absent2:'Absent Days',late2:'Late',ot2:'OT',
    totalOTH:'Total Hours',totalOTPay:'OT Pay',times:'Times',
    salary2:'Salary',inTime:'Time In',outTime:'Time Out',note:'Note',
    selectEmpFirst:'Select an employee to view salary slip',
    male:'Male',female:'Female',active:'Active',inactive:'Inactive',select:'-- Select --',
    add:'Add',
    sbn:'Employee Management System',sbs:'Manage Employees',
    emp:'Employees',attend:'Attendance',payroll:'Payroll',
    adminRole:'Administrator',loginTitle:'Employee Management System',
    loginUser:'Username',loginPass:'Password',loginBtn:'Login',
  }
};

let employees = [
  {id:'EMP-001',name:'ចាន់ សុទ្ធា',nameEn:'Chan Sotha',gender:'ប្រុស',dob:'1992-05-10',national:'ខ្មែរ',idCard:'012345678',phone:'012 345 678',email:'sotha@company.com',address:'ភ្នំពេញ',position:'Software Developer',dept:'IT',start:'2020-01-15',salary:800,bank:'ABA-001234',contract:'Full-time',status:'Active',photo:''},
  {id:'EMP-002',name:'ស្រី លក្ខណ៍',nameEn:'Srey Leak',gender:'ស្រី',dob:'1995-08-22',national:'ខ្មែរ',idCard:'098765432',phone:'015 678 901',email:'leak@company.com',address:'កណ្តាល',position:'HR Manager',dept:'HR',start:'2019-03-01',salary:700,bank:'Acleda-002345',contract:'Full-time',status:'Active',photo:''},
  {id:'EMP-003',name:'ហ៊ុន ដារ៉ា',nameEn:'Hun Dara',gender:'ប្រុស',dob:'1990-12-03',national:'ខ្មែរ',idCard:'034567890',phone:'017 234 567',email:'dara@company.com',address:'ពោធិ៍សាត់',position:'Accountant',dept:'Finance',start:'2021-06-10',salary:650,bank:'Wing-003456',contract:'Full-time',status:'Active',photo:''},
  {id:'EMP-004',name:'ម៉ាន់ ច័ន្ទ',nameEn:'Man Chan',gender:'ស្រី',dob:'1997-03-15',national:'ខ្មែរ',idCard:'056789012',phone:'016 890 123',email:'chan@company.com',address:'ភ្នំពេញ',position:'Marketing',dept:'Operations',start:'2022-09-01',salary:550,bank:'ABA-004567',contract:'Full-time',status:'Active',photo:''},
  {id:'EMP-005',name:'ពេជ្រ រ័ត្ន',nameEn:'Pech Roth',gender:'ប្រុស',dob:'1988-07-20',national:'ខ្មែរ',idCard:'023456789',phone:'011 456 789',email:'roth@company.com',address:'សៀមរាប',position:'Team Leader',dept:'IT',start:'2018-02-14',salary:900,bank:'ABA-005678',contract:'Full-time',status:'Active',photo:''},
  {id:'EMP-006',name:'ខៀវ ស្រីណា',nameEn:'Khiev Sreyna',gender:'ស្រី',dob:'1994-11-08',national:'ខ្មែរ',idCard:'045678901',phone:'077 567 890',email:'sreyna@company.com',address:'ក្រចេះ',position:'Designer',dept:'IT',start:'2023-01-05',salary:600,bank:'ABA-006789',contract:'Part-time',status:'Active',photo:''},
  {id:'EMP-007',name:'លន់ វណ្ណ',nameEn:'Lon Vann',gender:'ប្រុស',dob:'1993-04-25',national:'ខ្មែរ',idCard:'067890123',phone:'089 678 901',email:'vann@company.com',address:'ឧត្តរមានជ័យ',position:'Finance Officer',dept:'Finance',start:'2020-11-20',salary:620,bank:'ABA-007890',contract:'Full-time',status:'Inactive',photo:''},
  {id:'EMP-008',name:'ណារ ស្រីអ៊ី',nameEn:'Nar Srey Ei',gender:'ស្រី',dob:'1996-09-12',national:'ខ្មែរ',idCard:'078901234',phone:'096 789 012',email:'srei@company.com',address:'ភ្នំពេញ',position:'Receptionist',dept:'HR',start:'2022-04-01',salary:450,bank:'Acleda-008901',contract:'Full-time',status:'Active',photo:''},
];

let attendance = {};
let overtimeList = [];
let holidayList = [];
let allowanceList = [];

// Pre-fill some attendance
const today = new Date().toISOString().split('T')[0];
employees.forEach((e,i)=>{
  attendance[today] = attendance[today]||{};
  attendance[today][e.id] = {status:i<6?'present':i===6?'absent':'late',in:i<6?'08:00':'09:30',out:i<6?'17:00':'',note:''};
});

// Pre-fill OT
overtimeList = [
  {empId:'EMP-001',date:'2025-05-01',hours:3,rate:1.5,reason:'Project deadline'},
  {empId:'EMP-005',date:'2025-05-03',hours:4,rate:2.0,reason:'Holiday work'},
];
allowanceList = [
  {empId:'EMP-001',year:2025,transport:50,food:30,health:20,annual:200},
  {empId:'EMP-002',year:2025,transport:40,food:25,health:20,annual:150},
];
holidayList = [
  {date:'2025-04-14',name:'ពិធីបុណ្យចូលឆ្នាំថ្មី',type:'ថ្ងៃឈប់ជាតិ',emp:'all',pay:0},
  {date:'2025-05-01',name:'Khmer New Year Holiday',type:'ធ្វើការ',emp:'EMP-001',pay:60},
];

// ==================== LANGUAGE ====================
function setLang(lang, btn) {
  currentLang = lang;
  document.body.className = lang==='en'?'lang-en':'lang-km';
  // Update all .t-* elements
  const t = T[lang];
  Object.entries(t).forEach(([k,v])=>{
    document.querySelectorAll('.t-'+k).forEach(el=>el.textContent=v);
  });
  // Login page labels
  document.getElementById('loginTitle').textContent = t.loginTitle;
  document.getElementById('lbUser').textContent = t.loginUser;
  document.getElementById('lbPass').textContent = t.loginPass;
  document.getElementById('lbLoginBtn').textContent = t.loginBtn;
  document.getElementById('sb-title').textContent = 'HR '+t.sbn.split(' ').pop();
  document.getElementById('sb-sub').textContent = t.sbs;
  document.getElementById('sbRole').textContent = t.adminRole;
  // Toggle login buttons
  if(document.getElementById('loginLangKm')){
    document.getElementById('loginLangKm').classList.toggle('active',lang==='km');
    document.getElementById('loginLangEn').classList.toggle('active',lang==='en');
  }
  document.getElementById('appLangKm').classList.toggle('active',lang==='km');
  document.getElementById('appLangEn').classList.toggle('active',lang==='en');
  // Re-render current page
  const active = document.querySelector('.page.active');
  if(active) renderPage(active.id.replace('page-',''));
}

// ==================== LOGIN ====================
function doLogin(){
  const u=document.getElementById('username').value;
  const p=document.getElementById('password').value;
  if(u==='admin'&&p==='1234'){
    document.getElementById('loginPage').style.display='none';
    document.getElementById('app').style.display='block';
    document.getElementById('sbUsername').textContent=u;
    document.getElementById('headerDate').textContent=new Date().toLocaleDateString('km-KH',{year:'numeric',month:'long',day:'numeric'});
    document.getElementById('attendDate').value=today;
    populateSelects();
    renderPage('dashboard');
    renderPage('employees');
    renderPage('attendance');
    genAttendReport();
    genOTReport();
    renderOTTable();
    renderHolidayTable();
    renderAllowTable();
    buildMonthChart();
    buildDeptList();
  } else {
    showToast(currentLang==='km'?'ឈ្មោះ ឬ ពាក្យសម្ងាត់មិនត្រឹមត្រូវ!':'Wrong username or password!',true);
  }
}
function doLogout(){
  document.getElementById('loginPage').style.display='flex';
  document.getElementById('app').style.display='none';
}
document.addEventListener('keydown',e=>{if(e.key==='Enter'&&document.getElementById('loginPage').style.display!=='none')doLogin()});

// ==================== NAVIGATION ====================
function showPage(name, el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  const p=document.getElementById('page-'+name);
  if(p)p.classList.add('active');
  if(el)el.classList.add('active');
  const t=T[currentLang];
  const titles={dashboard:t.dashboard,employees:t.empList,addEmp:t.addEmp,empCard:t.empCard,
    attendance:t.attendMark,attendReport:t.attendReport,overtime:t.overtime,
    holiday:t.holiday,allowance:t.allowance,salary:t.salary,
    salaryReport:t.salaryReport,otReport:t.otReport};
  const hdr=document.getElementById('headerTitle');
  if(hdr)hdr.innerHTML=`${titles[name]||name} <span>${new Date().toLocaleDateString('km-KH',{year:'numeric',month:'long',day:'numeric'})}</span>`;
  renderPage(name);
}
function renderPage(name){
  if(name==='employees')renderEmployeeTable();
  if(name==='attendance')renderAttendTable();
  if(name==='empCard'){populateCardSelect();renderEmpCard();}
  if(name==='salary')genSalary();
  if(name==='salaryReport')populateSRSelect();
}

// ==================== EMPLOYEES ====================
function renderEmployeeTable(){
  const q=(document.getElementById('empSearch')||{}).value||'';
  const df=(document.getElementById('deptFilter')||{}).value||'';
  const t=T[currentLang];
  let rows=employees.filter(e=>
    (e.name.includes(q)||e.nameEn.toLowerCase().includes(q.toLowerCase())||e.id.includes(q))&&
    (!df||e.dept===df)
  );
  const tbody=document.getElementById('empTableBody');
  if(!tbody)return;
  tbody.innerHTML=rows.map((e,i)=>`
    <tr>
      <td>${i+1}</td>
      <td><div class="emp-name">
        <div class="emp-avatar">${e.photo?`<img src="${e.photo}">`:''}${!e.photo?e.nameEn[0]:''}</div>
        <div><div style="font-weight:600">${e.name}</div><div style="font-size:.7rem;color:var(--text-muted)">${e.nameEn}</div></div>
      </div></td>
      <td>${e.position}</td>
      <td><span class="badge badge-blue">${e.dept}</span></td>
      <td>${e.phone}</td>
      <td style="font-weight:700;color:var(--success)">$${e.salary}</td>
      <td><span class="badge ${e.status==='Active'?'badge-green':'badge-red'}">${t[e.status.toLowerCase()]||e.status}</span></td>
      <td style="display:flex;gap:4px">
        <button class="btn btn-outline btn-sm btn-icon" onclick="viewEmp('${e.id}')" title="${t.view}"><i class="fas fa-eye"></i></button>
        <button class="btn btn-primary btn-sm btn-icon" onclick="editEmp('${e.id}')" title="${t.edit}"><i class="fas fa-edit"></i></button>
        <button class="btn btn-danger btn-sm btn-icon" onclick="deleteEmp('${e.id}')" title="${t.delete}"><i class="fas fa-trash"></i></button>
      </td>
    </tr>`).join('');
  document.getElementById('totalEmpCount').textContent=employees.length;
}

function viewEmp(id){
  const e=employees.find(x=>x.id===id); if(!e)return;
  const t=T[currentLang];
  document.getElementById('empDetailBody').innerHTML=`
    <div style="display:flex;gap:24px;flex-wrap:wrap">
      <div>
        <div style="width:100px;height:133px;border-radius:8px;overflow:hidden;background:var(--bg);border:2px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:2rem;color:var(--primary)">
          ${e.photo?`<img src="${e.photo}" style="width:100%;height:100%;object-fit:cover">`:`<i class="fas fa-user"></i>`}
        </div>
        <div style="text-align:center;margin-top:8px">
          <div style="font-size:.72rem;color:var(--text-muted)">${e.id}</div>
          <span class="badge ${e.status==='Active'?'badge-green':'badge-red'}" style="margin-top:4px">${e.status}</span>
        </div>
      </div>
      <div style="flex:1;min-width:240px">
        <div class="section-title">${t.personalInfo}</div>
        <div class="info-grid">
          <div class="info-item"><div class="ii-label">${t.fullName}</div><div class="ii-val">${e.name}</div></div>
          <div class="info-item"><div class="ii-label">${t.nameEn}</div><div class="ii-val">${e.nameEn}</div></div>
          <div class="info-item"><div class="ii-label">${t.gender}</div><div class="ii-val">${e.gender}</div></div>
          <div class="info-item"><div class="ii-label">${t.dob}</div><div class="ii-val">${e.dob}</div></div>
          <div class="info-item"><div class="ii-label">${t.phone}</div><div class="ii-val">${e.phone}</div></div>
          <div class="info-item"><div class="ii-label">Email</div><div class="ii-val">${e.email}</div></div>
          <div class="info-item" style="grid-column:1/-1"><div class="ii-label">${t.address}</div><div class="ii-val">${e.address}</div></div>
        </div>
        <div class="section-title" style="margin-top:16px">${t.jobInfo}</div>
        <div class="info-grid">
          <div class="info-item"><div class="ii-label">${t.position}</div><div class="ii-val">${e.position}</div></div>
          <div class="info-item"><div class="ii-label">${t.dept}</div><div class="ii-val">${e.dept}</div></div>
          <div class="info-item"><div class="ii-label">${t.startDate}</div><div class="ii-val">${e.start}</div></div>
          <div class="info-item"><div class="ii-label">${t.baseSalary}</div><div class="ii-val" style="color:var(--success);font-weight:700">$${e.salary}</div></div>
          <div class="info-item"><div class="ii-label">${t.bankAcc}</div><div class="ii-val">${e.bank}</div></div>
          <div class="info-item"><div class="ii-label">${t.contract}</div><div class="ii-val">${e.contract}</div></div>
        </div>
      </div>
    </div>`;
  openModal('empDetailModal');
}
function editEmp(id){
  const e=employees.find(x=>x.id===id); if(!e)return;
  editEmpId=id;
  showPage('addEmp');
  const fields={fName:e.name,fNameEn:e.nameEn,fGender:e.gender,fDob:e.dob,fNational:e.national,
    fId:e.idCard,fPhone:e.phone,fEmail:e.email,fAddress:e.address,
    fEmpId:e.id,fPosition:e.position,fDept:e.dept,fStart:e.start,
    fSalary:e.salary,fBank:e.bank,fContract:e.contract,fStatus:e.status};
  Object.entries(fields).forEach(([k,v])=>{const el=document.getElementById(k);if(el)el.value=v;});
  if(e.photo){
    document.getElementById('photoPreview').src=e.photo;
    document.getElementById('photoPreview').style.display='block';
    document.getElementById('photoIcon').style.display='none';
    document.getElementById('photoText').style.display='none';
  }
}
function deleteEmp(id){
  if(!confirm(currentLang==='km'?'តើអ្នកប្រាកដទេ?':'Are you sure?'))return;
  employees=employees.filter(e=>e.id!==id);
  renderEmployeeTable();
  showToast(T[currentLang].deleted,false);
}
function saveEmployee(){
  const t=T[currentLang];
  const photoEl=document.getElementById('photoPreview');
  const emp={
    id:document.getElementById('fEmpId').value||'EMP-'+(employees.length+1).toString().padStart(3,'0'),
    name:document.getElementById('fName').value,
    nameEn:document.getElementById('fNameEn').value,
    gender:document.getElementById('fGender').value,
    dob:document.getElementById('fDob').value,
    national:document.getElementById('fNational').value,
    idCard:document.getElementById('fId').value,
    phone:document.getElementById('fPhone').value,
    email:document.getElementById('fEmail').value,
    address:document.getElementById('fAddress').value,
    position:document.getElementById('fPosition').value,
    dept:document.getElementById('fDept').value,
    start:document.getElementById('fStart').value,
    salary:parseFloat(document.getElementById('fSalary').value)||0,
    bank:document.getElementById('fBank').value,
    contract:document.getElementById('fContract').value,
    status:document.getElementById('fStatus').value,
    photo:photoEl&&photoEl.style.display!=='none'?photoEl.src:'',
  };
  if(!emp.name){showToast(currentLang==='km'?'សូមបញ្ចូលឈ្មោះ!':'Please enter name!',true);return;}
  if(editEmpId){
    const idx=employees.findIndex(e=>e.id===editEmpId);
    if(idx>=0)employees[idx]=emp;
    editEmpId=null;
  }else{
    if(employees.find(e=>e.id===emp.id)){emp.id='EMP-'+(employees.length+1).toString().padStart(3,'0');}
    employees.push(emp);
  }
  showToast(t.saved);
  populateSelects();
  showPage('employees');
}
function clearEmpForm(){
  ['fName','fNameEn','fGender','fDob','fNational','fId','fPhone','fEmail','fAddress','fEmpId','fPosition','fDept','fStart','fSalary','fBank'].forEach(id=>{
    const el=document.getElementById(id);if(el)el.value='';
  });
  document.getElementById('photoPreview').style.display='none';
  document.getElementById('photoIcon').style.display='block';
  document.getElementById('photoText').style.display='block';
  editEmpId=null;
}

// PHOTO
function previewPhoto(input){
  const file=input.files[0]; if(!file)return;
  const reader=new FileReader();
  reader.onload=e=>{
    const img=document.getElementById('photoPreview');
    img.src=e.target.result;img.style.display='block';
    document.getElementById('photoIcon').style.display='none';
    document.getElementById('photoText').style.display='none';
  };
  reader.readAsDataURL(file);
}

// ==================== ATTENDANCE ====================
function renderAttendTable(){
  const date=(document.getElementById('attendDate')||{}).value||today;
  attendance[date]=attendance[date]||{};
  const t=T[currentLang];
  const statuses=[
    {val:'present',label:t.present,cls:'badge-green'},
    {val:'absent',label:t.absent,cls:'badge-red'},
    {val:'late',label:t.late,cls:'badge-gold'},
    {val:'halfday',label:t.halfday,cls:'badge-blue'},
    {val:'leave',label:t.leave,cls:'badge-gray'},
  ];
  const tbody=document.getElementById('attendTableBody');
  if(!tbody)return;
  tbody.innerHTML=employees.map((e,i)=>{
    const a=attendance[date][e.id]||{status:'absent',in:'',out:'',note:''};
    const opts=statuses.map(s=>`<option value="${s.val}" ${a.status===s.val?'selected':''}>${s.label}</option>`).join('');
    return `<tr>
      <td>${i+1}</td>
      <td><div class="emp-name"><div class="emp-avatar">${e.photo?`<img src="${e.photo}">`:''}${!e.photo?e.nameEn[0]:''}</div>${e.name}</div></td>
      <td><span class="badge badge-blue">${e.dept}</span></td>
      <td><select class="filter-select" id="as-${e.id}" onchange="updateAttend('${e.id}','${date}')">${opts}</select></td>
      <td><input type="time" value="${a.in}" style="border:1.5px solid var(--border);border-radius:6px;padding:4px 8px;font-family:inherit;font-size:.78rem;background:var(--bg)" onchange="setAttendTime('${e.id}','${date}','in',this.value)"></td>
      <td><input type="time" value="${a.out}" style="border:1.5px solid var(--border);border-radius:6px;padding:4px 8px;font-family:inherit;font-size:.78rem;background:var(--bg)" onchange="setAttendTime('${e.id}','${date}','out',this.value)"></td>
      <td><input type="text" value="${a.note}" placeholder="..." style="border:1.5px solid var(--border);border-radius:6px;padding:4px 8px;font-family:inherit;font-size:.78rem;background:var(--bg);width:100%" onchange="setAttendTime('${e.id}','${date}','note',this.value)"></td>
    </tr>`;
  }).join('');
  // Update dashboard
  renderDashTable(date);
}
function updateAttend(empId,date){
  if(!attendance[date])attendance[date]={};
  if(!attendance[date][empId])attendance[date][empId]={status:'absent',in:'',out:'',note:''};
  attendance[date][empId].status=document.getElementById('as-'+empId).value;
}
function setAttendTime(empId,date,field,val){
  if(!attendance[date])attendance[date]={};
  if(!attendance[date][empId])attendance[date][empId]={status:'absent',in:'',out:'',note:''};
  attendance[date][empId][field]=val;
}
function saveAllAttend(){
  showToast(T[currentLang].saved);
  const date=(document.getElementById('attendDate')||{}).value||today;
  employees.forEach(e=>{
    if(!attendance[date])attendance[date]={};
    if(!attendance[date][e.id])attendance[date][e.id]={status:'absent',in:'',out:'',note:''};
  });
  renderDashTable(date);
}
function renderDashTable(date){
  const t=T[currentLang];
  const tbody=document.getElementById('dashTableBody');
  if(!tbody)return;
  const att=attendance[date]||{};
  const badgeMap={present:'badge-green',absent:'badge-red',late:'badge-gold',halfday:'badge-blue',leave:'badge-gray'};
  tbody.innerHTML=employees.slice(0,6).map(e=>{
    const a=att[e.id]||{status:'absent',in:'--',out:'--'};
    return `<tr>
      <td><div class="emp-name"><div class="emp-avatar">${e.photo?`<img src="${e.photo}">`:''}${!e.photo?e.nameEn[0]:''}</div>${e.name}</div></td>
      <td>${e.dept}</td>
      <td><span class="badge ${badgeMap[a.status]||'badge-gray'}">${t[a.status]||a.status}</span></td>
      <td>${a.in||'--'}</td>
      <td>${a.out||'--'}</td>
    </tr>`;
  }).join('');
  const p=Object.values(att).filter(a=>a.status==='present'||a.status==='late').length;
  const ab=employees.length-p;
  document.getElementById('presentCount').textContent=p;
  document.getElementById('absentCount').textContent=ab;
}

// ==================== ATTEND REPORT ====================
function genAttendReport(){
  const month=(document.getElementById('arMonth')||{}).value||'05';
  const year=(document.getElementById('arYear')||{}).value||'2025';
  const tbody=document.getElementById('arBody');
  if(!tbody)return;
  const t=T[currentLang];
  tbody.innerHTML=employees.map(e=>{
    let present=0,absent=0,late=0,ot=0;
    Object.entries(attendance).forEach(([d,day])=>{
      if(d.startsWith(`${year}-${month}`)&&day[e.id]){
        const s=day[e.id].status;
        if(s==='present')present++;
        else if(s==='absent')absent++;
        else if(s==='late'){late++;present++;}
      }
    });
    ot=overtimeList.filter(o=>o.empId===e.id&&o.date.startsWith(`${year}-${month}`)).reduce((s,o)=>s+o.hours,0);
    const workDays=22;
    const pct=Math.round(present/workDays*100);
    return `<tr>
      <td><div class="emp-name"><div class="emp-avatar">${e.nameEn[0]}</div>${e.name}</div></td>
      <td>${e.dept}</td>
      <td style="color:var(--success);font-weight:700">${present}</td>
      <td style="color:var(--danger);font-weight:700">${absent}</td>
      <td style="color:var(--warning)">${late}</td>
      <td style="color:var(--info)">${ot}h</td>
      <td><div style="min-width:80px">
        <div style="display:flex;justify-content:space-between;font-size:.72rem;font-weight:700"><span>${pct}%</span></div>
        <div class="progress-bar"><div class="progress-fill" style="width:${pct}%"></div></div>
      </div></td>
    </tr>`;
  }).join('');
}

// ==================== OVERTIME ====================
function renderOTTable(){
  const tbody=document.getElementById('otBody');
  if(!tbody)return;
  const t=T[currentLang];
  tbody.innerHTML=overtimeList.map((o,i)=>{
    const e=employees.find(x=>x.id===o.empId);
    const amt=((e?e.salary:0)/26/8*o.hours*o.rate).toFixed(2);
    return `<tr>
      <td>${e?e.name:'--'}</td>
      <td>${o.date}</td>
      <td style="font-weight:700">${o.hours}h</td>
      <td>x${o.rate}</td>
      <td style="color:var(--success);font-weight:700">$${amt}</td>
      <td>${o.reason}</td>
      <td><button class="btn btn-danger btn-sm btn-icon" onclick="deleteOT(${i})"><i class="fas fa-trash"></i></button></td>
    </tr>`;
  }).join('');
}
function openOTModal(){
  populateEmpSelect('otEmp');
  document.getElementById('otDate').value=today;
  openModal('otModal');
}
function saveOT(){
  const empId=(document.getElementById('otEmp')||{}).value;
  const date=(document.getElementById('otDate')||{}).value;
  const hours=parseFloat((document.getElementById('otHours')||{}).value)||0;
  const rate=parseFloat((document.getElementById('otRate')||{}).value)||1.5;
  const reason=(document.getElementById('otReason')||{}).value;
  if(!empId||!hours){showToast(currentLang==='km'?'សូមបំពេញទិន្នន័យ!':'Please fill in all fields!',true);return;}
  overtimeList.push({empId,date,hours,rate,reason});
  closeModal('otModal');
  renderOTTable();
  showToast(T[currentLang].saved);
}
function deleteOT(i){overtimeList.splice(i,1);renderOTTable();}

// ==================== HOLIDAY ====================
function renderHolidayTable(){
  const tbody=document.getElementById('holidayBody');
  if(!tbody)return;
  const t=T[currentLang];
  tbody.innerHTML=holidayList.map((h,i)=>{
    const e=h.emp==='all'?t.allEmp:(employees.find(x=>x.id===h.emp)||{}).name||h.emp;
    return `<tr>
      <td>${h.date}</td>
      <td style="font-weight:600">${h.name}</td>
      <td><span class="badge ${h.type==='ធ្វើការ'?'badge-gold':'badge-blue'}">${h.type}</span></td>
      <td>${e}</td>
      <td style="color:var(--success)">$${h.pay}</td>
      <td><button class="btn btn-danger btn-sm btn-icon" onclick="deleteHoliday(${i})"><i class="fas fa-trash"></i></button></td>
    </tr>`;
  }).join('');
}
function openHolidayModal(){
  populateEmpSelect('holEmp');
  document.getElementById('holDate').value=today;
  openModal('holidayModal');
}
function saveHoliday(){
  holidayList.push({
    date:document.getElementById('holDate').value,
    name:document.getElementById('holName').value,
    type:document.getElementById('holType').value,
    emp:document.getElementById('holEmp').value,
    pay:parseFloat(document.getElementById('holPay').value)||0,
  });
  closeModal('holidayModal');
  renderHolidayTable();
  showToast(T[currentLang].saved);
}
function deleteHoliday(i){holidayList.splice(i,1);renderHolidayTable();}

// ==================== ALLOWANCE ====================
function renderAllowTable(){
  const tbody=document.getElementById('allowBody');
  if(!tbody)return;
  tbody.innerHTML=allowanceList.map((a,i)=>{
    const e=employees.find(x=>x.id===a.empId);
    const total=a.transport+a.food+a.health+a.annual;
    return `<tr>
      <td>${e?e.name:'--'}</td>
      <td>${a.year}</td>
      <td>$${a.transport}</td>
      <td>$${a.food}</td>
      <td>$${a.health}</td>
      <td>$${a.annual}</td>
      <td style="font-weight:700;color:var(--success)">$${total}</td>
      <td><button class="btn btn-danger btn-sm btn-icon" onclick="deleteAllow(${i})"><i class="fas fa-trash"></i></button></td>
    </tr>`;
  }).join('');
}
function openAllowModal(){
  populateEmpSelect('allowEmp');
  openModal('allowModal');
}
function saveAllow(){
  allowanceList.push({
    empId:document.getElementById('allowEmp').value,
    year:parseInt(document.getElementById('allowYear').value)||2025,
    transport:parseFloat(document.getElementById('allowTransport').value)||0,
    food:parseFloat(document.getElementById('allowFood').value)||0,
    health:parseFloat(document.getElementById('allowHealth').value)||0,
    annual:parseFloat(document.getElementById('allowAnnual').value)||0,
  });
  closeModal('allowModal');
  renderAllowTable();
  showToast(T[currentLang].saved);
}
function deleteAllow(i){allowanceList.splice(i,1);renderAllowTable();}

// ==================== SALARY ====================
function genSalary(){
  const month=(document.getElementById('salMonth')||{}).value||'05';
  const year=(document.getElementById('salYear')||{}).value||'2025';
  const tbody=document.getElementById('salBody');
  if(!tbody)return;
  const t=T[currentLang];
  tbody.innerHTML=employees.map(e=>{
    const otPay=overtimeList.filter(o=>o.empId===e.id&&o.date.startsWith(`${year}-${month}`))
      .reduce((s,o)=>s+(e.salary/26/8*o.hours*o.rate),0);
    const allow=allowanceList.find(a=>a.empId===e.id&&a.year===parseInt(year));
    const allowTotal=allow?(allow.transport+allow.food+allow.health)/12:0;
    const absences=Object.entries(attendance).filter(([d,day])=>d.startsWith(`${year}-${month}`)&&day[e.id]&&day[e.id].status==='absent').length;
    const deduction=absences*(e.salary/22);
    const net=e.salary+otPay+allowTotal-deduction;
    return `<tr>
      <td>${e.name}</td>
      <td>${e.dept}</td>
      <td>$${e.salary}</td>
      <td style="color:var(--info)">$${otPay.toFixed(2)}</td>
      <td style="color:var(--success)">$${allowTotal.toFixed(2)}</td>
      <td style="color:var(--danger)">-$${deduction.toFixed(2)}</td>
      <td style="font-weight:800;color:var(--success)">$${net.toFixed(2)}</td>
      <td>
        <button class="btn btn-primary btn-sm" onclick="viewSlip('${e.id}','${month}','${year}')"><i class="fas fa-file-alt"></i></button>
      </td>
    </tr>`;
  }).join('');
}
function populateSRSelect(){
  const sel=document.getElementById('srEmp');if(!sel)return;
  sel.innerHTML='<option value="">-- ជ្រើស --</option>'+employees.map(e=>`<option value="${e.id}">${e.name}</option>`).join('');
}
function showSlip(){
  const id=(document.getElementById('srEmp')||{}).value;
  if(id)viewSlip(id,'05','2025');
}
function viewSlip(empId,month,year){
  const e=employees.find(x=>x.id===empId);if(!e)return;
  const t=T[currentLang];
  const otPay=overtimeList.filter(o=>o.empId===e.id&&o.date.startsWith(`${year}-${month}`))
    .reduce((s,o)=>s+(e.salary/26/8*o.hours*o.rate),0);
  const allow=allowanceList.find(a=>a.empId===e.id&&a.year===parseInt(year));
  const allowTotal=allow?(allow.transport+allow.food+allow.health)/12:0;
  const absences=Object.entries(attendance).filter(([d,day])=>d.startsWith(`${year}-${month}`)&&day[e.id]&&day[e.id].status==='absent').length;
  const deduction=absences*(e.salary/22);
  const net=e.salary+otPay+allowTotal-deduction;
  const area=document.getElementById('slipArea');
  if(!area)return;
  area.innerHTML=`
    <div class="slip">
      <div class="slip-header">
        <div><div style="font-size:.72rem;opacity:.6">ABC COMPANY</div><div style="font-size:1.1rem;font-weight:800">Salary Slip</div></div>
        <div style="text-align:right"><div style="font-size:.75rem;opacity:.7">${year}/${month}</div><div style="font-weight:700">${e.id}</div></div>
      </div>
      <div class="slip-section">
        <div style="display:flex;gap:16px;align-items:center">
          <div style="width:50px;height:66px;border-radius:6px;background:rgba(255,255,255,.15);overflow:hidden;border:2px solid var(--border)">
            ${e.photo?`<img src="${e.photo}" style="width:100%;height:100%;object-fit:cover">`:'<div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-size:1.2rem;color:var(--primary)"><i class="fas fa-user"></i></div>'}
          </div>
          <div>
            <div style="font-weight:700;font-size:1rem">${e.name}</div>
            <div style="color:var(--text-muted);font-size:.8rem">${e.nameEn}</div>
            <div style="margin-top:4px"><span class="badge badge-blue">${e.dept}</span> <span class="badge badge-gray">${e.position}</span></div>
          </div>
        </div>
      </div>
      <div class="slip-section">
        <div style="font-weight:700;color:var(--primary);margin-bottom:8px;font-size:.78rem">EARNINGS</div>
        <div class="slip-row"><span>${t.baseSalary2}</span><span style="color:var(--success);font-weight:700">$${e.salary.toFixed(2)}</span></div>
        <div class="slip-row"><span>${t.otPay}</span><span style="color:var(--info)">$${otPay.toFixed(2)}</span></div>
        <div class="slip-row"><span>${t.allowance2} (Transport+Food+Health)/12</span><span style="color:var(--success)">$${allowTotal.toFixed(2)}</span></div>
      </div>
      <div class="slip-section">
        <div style="font-weight:700;color:var(--danger);margin-bottom:8px;font-size:.78rem">DEDUCTIONS</div>
        <div class="slip-row"><span>${t.absent2} (${absences} days x $${(e.salary/22).toFixed(2)})</span><span style="color:var(--danger)">-$${deduction.toFixed(2)}</span></div>
      </div>
      <div class="slip-total">
        <div class="total-label">${t.netSalary}</div>
        <div class="total-val">$${net.toFixed(2)}</div>
      </div>
    </div>
    <div style="display:flex;gap:10px;margin-top:16px">
      <button class="btn btn-danger no-print" onclick="exportPDF()"><i class="fas fa-file-pdf"></i> PDF</button>
      <button class="btn btn-primary no-print" onclick="window.print()"><i class="fas fa-print"></i> ${t.print}</button>
      <button class="btn btn-success no-print" onclick="exportExcel()"><i class="fas fa-file-excel"></i> Excel</button>
    </div>`;
  showPage('salaryReport');
}

// ==================== OT REPORT ====================
function genOTReport(){
  const month=(document.getElementById('otrMonth')||{}).value||'05';
  const year=(document.getElementById('otrYear')||{}).value||'2025';
  const tbody=document.getElementById('otrBody');
  if(!tbody)return;
  tbody.innerHTML=employees.map(e=>{
    const ots=overtimeList.filter(o=>o.empId===e.id&&o.date.startsWith(`${year}-${month}`));
    const totalH=ots.reduce((s,o)=>s+o.hours,0);
    const totalPay=ots.reduce((s,o)=>s+(e.salary/26/8*o.hours*o.rate),0);
    return `<tr>
      <td>${e.name}</td>
      <td>${e.dept}</td>
      <td style="font-weight:700">${totalH}h</td>
      <td style="color:var(--success);font-weight:700">$${totalPay.toFixed(2)}</td>
      <td>${ots.length}</td>
    </tr>`;
  }).join('');
}

// ==================== EMPLOYEE CARD ====================
function populateCardSelect(){
  const sel=document.getElementById('cardEmpSelect');if(!sel)return;
  const cur=sel.value;
  sel.innerHTML='<option value="">-- ជ្រើស --</option>'+employees.map(e=>`<option value="${e.id}">${e.name}</option>`).join('');
  if(cur)sel.value=cur;
}
function renderEmpCard(){
  const id=(document.getElementById('cardEmpSelect')||{}).value;
  const e=employees.find(x=>x.id===id);
  if(!e){
    document.getElementById('cardName').textContent='-- ជ្រើសបុគ្គលិក --';
    document.getElementById('cardPos').textContent='--';
    document.getElementById('cardId').textContent='--';
    document.getElementById('cardDept').textContent='--';
    document.getElementById('cardPhone').textContent='--';
    document.getElementById('cardStart').textContent='--';
    document.getElementById('cardPhoto').src='';
    return;
  }
  document.getElementById('cardName').textContent=e.name;
  document.getElementById('cardPos').textContent=e.position;
  document.getElementById('cardId').textContent=e.id;
  document.getElementById('cardDept').textContent=e.dept;
  document.getElementById('cardPhone').textContent=e.phone;
  document.getElementById('cardStart').textContent=e.start;
  document.getElementById('cardPhoto').src=e.photo;
}
function printCard(){window.print();}
function exportCardPDF(){showToast(currentLang==='km'?'រក្សាទុក PDF ដោយជោគជ័យ!':'Saved as PDF!');}

// ==================== CHARTS ====================
function buildMonthChart(){
  const box=document.getElementById('monthChart');if(!box)return;
  const labels=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  const vals=[18,20,19,22,21,20,22,21,20,22,19,21];
  box.innerHTML=vals.map((v,i)=>`
    <div class="chart-bar" style="height:${v/22*100}%" title="${labels[i]}: ${v}days">
      <span>${v}</span>
    </div>`).join('')+`<div style="position:absolute;left:0;bottom:0;right:0;display:flex;justify-content:space-around;font-size:.55rem;color:var(--text-muted);padding:0 4px">${labels.map(l=>`<span>${l}</span>`).join('')}</div>`;
}
function buildDeptList(){
  const el=document.getElementById('deptList');if(!el)return;
  const depts={IT:0,HR:0,Finance:0,Operations:0};
  employees.forEach(e=>{if(depts[e.dept]!==undefined)depts[e.dept]+=e.salary;});
  const total=Object.values(depts).reduce((a,b)=>a+b,0);
  const colors={IT:'var(--primary)',HR:'var(--success)',Finance:'var(--accent)',Operations:'var(--info)'};
  el.innerHTML=Object.entries(depts).map(([d,v])=>`
    <div style="margin-bottom:12px">
      <div style="display:flex;justify-content:space-between;margin-bottom:4px">
        <span style="font-size:.78rem;font-weight:600">${d}</span>
        <span style="font-size:.78rem;font-weight:700;color:var(--success)">$${v}</span>
      </div>
      <div class="progress-bar"><div class="progress-fill" style="width:${Math.round(v/total*100)}%;background:${colors[d]}"></div></div>
    </div>`).join('');
}

// ==================== HELPERS ====================
function populateSelects(){
  populateEmpSelect('otEmp');
  populateEmpSelect('holEmp');
  populateEmpSelect('allowEmp');
  populateCardSelect();
  populateSRSelect();
}
function populateEmpSelect(id){
  const sel=document.getElementById(id);if(!sel)return;
  const isHol=id==='holEmp';
  sel.innerHTML=(isHol?`<option value="all">${T[currentLang].allEmp}</option>`:'')+
    employees.map(e=>`<option value="${e.id}">${e.name}</option>`).join('');
}
function openModal(id){document.getElementById(id).classList.add('open');}
function closeModal(id){document.getElementById(id).classList.remove('open');}
function showToast(msg,error=false){
  const t=document.getElementById('toast');
  const ic=t.querySelector('i');
  t.style.borderLeftColor=error?'var(--danger)':'var(--success)';
  ic.style.color=error?'var(--danger)':'var(--success)';
  ic.className=error?'fas fa-exclamation-circle':'fas fa-check-circle';
  document.getElementById('toastMsg').textContent=msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),3000);
}
function exportPDF(){
  showToast(currentLang==='km'?'កំពុងបង្កើត PDF...':'Generating PDF...');
  setTimeout(()=>window.print(),500);
}
function exportExcel(){
  // Simple CSV export
  const rows=document.querySelectorAll('#page-'+document.querySelector('.page.active').id.replace('page-','')+' table tbody tr');
  if(!rows.length){showToast('No data to export',true);return;}
  let csv='';
  document.querySelectorAll('.page.active table thead tr th').forEach(th=>csv+=`"${th.textContent}",`);
  csv=csv.slice(0,-1)+'\n';
  rows.forEach(row=>{
    row.querySelectorAll('td').forEach(td=>csv+=`"${td.textContent.trim().replace(/"/g,'""')}",`);
    csv=csv.slice(0,-1)+'\n';
  });
  const blob=new Blob(['\uFEFF'+csv],{type:'text/csv;charset=utf-8;'});
  const url=URL.createObjectURL(blob);
  const a=document.createElement('a');a.href=url;a.download='report.csv';a.click();
  showToast(currentLang==='km'?'Export Excel ដោយជោគជ័យ!':'Exported to Excel!');
}

// Close modal on overlay click
document.querySelectorAll('.modal-overlay').forEach(o=>o.addEventListener('click',function(e){if(e.target===this)this.classList.remove('open')}));

// Init
window.addEventListener('load',()=>{
  document.getElementById('attendDate').value=today;
  setLang('km');
});
</script>
</body>
</html>
