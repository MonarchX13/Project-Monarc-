<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MONARCH // RENDER COMMISSION DATABASE</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;500;700;900&display=swap');
:root{
  --p:#aaff00;--pd:#77cc00;--pg:rgba(170,255,0,0.12);--pb:rgba(170,255,0,0.4);
  --y:#ffdd00;--g:#55ff44;--am:#ffcc00;--r:#ff3355;--cy:#00ffcc;
  --bg:#070c00;--bg2:#0a1200;--bg3:#0d1800;
  --panel:rgba(8,16,0,0.93);--text:#d8f0b0;--td:#7a9f50;--tb:#eeffcc;
  --gl:rgba(170,255,0,0.07);
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
html,body{height:100%;overflow:hidden;}
body{background:var(--bg);color:var(--text);font-family:'Share Tech Mono',monospace;cursor:crosshair;}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(var(--gl) 1px,transparent 1px),linear-gradient(90deg,var(--gl) 1px,transparent 1px);background-size:40px 40px;pointer-events:none;z-index:0;}
body::after{content:'';position:fixed;inset:0;background:radial-gradient(ellipse at 50% 0%,rgba(170,255,0,0.05) 0%,transparent 60%),radial-gradient(ellipse at 100% 100%,rgba(255,221,0,0.03) 0%,transparent 50%);pointer-events:none;z-index:0;}
.scanline{position:fixed;inset:0;pointer-events:none;z-index:9999;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.025) 2px,rgba(0,0,0,0.025) 4px);}
.flicker{animation:flicker 7s infinite;}
@keyframes flicker{0%,97%,100%{opacity:1}98%{opacity:0.8}}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.3}}
@keyframes drawIn{from{stroke-dashoffset:1000}to{stroke-dashoffset:0}}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

/* ── TOP BAR ── */
.topbar{position:relative;z-index:100;display:flex;align-items:center;justify-content:space-between;padding:0 20px;height:44px;background:rgba(2,6,0,0.98);border-bottom:1px solid var(–pb);box-shadow:0 0 24px rgba(170,255,0,0.08);}
.logo{font-family:‘Orbitron’,sans-serif;font-weight:900;font-size:17px;color:var(–p);text-shadow:0 0 12px var(–p),0 0 30px rgba(170,255,0,0.3);letter-spacing:5px;}
.logo span{color:var(–td);font-weight:400;}
.topbar-tabs{display:flex;gap:2px;margin-left:24px;}
.ttab{padding:5px 14px;font-size:10px;letter-spacing:2px;text-transform:uppercase;border:1px solid transparent;cursor:pointer;transition:all 0.2s;color:var(–td);font-family:‘Share Tech Mono’,monospace;background:transparent;}
.ttab:hover{color:var(–p);border-color:var(–pb);background:var(–pg);}
.ttab.active{color:var(–p);border-color:var(–pb);background:rgba(170,255,0,0.1);box-shadow:0 0 10px rgba(170,255,0,0.1);}
.topbar-right{display:flex;align-items:center;gap:14px;font-size:9px;color:var(–td);}
.sdot{width:6px;height:6px;border-radius:50%;background:var(–g);box-shadow:0 0 6px var(–g);animation:pulse 2s infinite;}

/* ── SYS BAR ── */
.sysbar{position:relative;z-index:100;display:flex;align-items:stretch;padding:0 20px;height:24px;background:rgba(0,4,0,0.9);border-bottom:1px solid rgba(170,255,0,0.12);font-size:9px;color:var(–td);}
.sbi{display:flex;align-items:center;gap:5px;padding:0 12px;border-right:1px solid rgba(170,255,0,0.1);}
.sbi:first-child{padding-left:0;}
.sbv{color:var(–p);}
.sbend{margin-left:auto;display:flex;align-items:center;color:rgba(170,255,0,0.25);letter-spacing:3px;font-size:8px;}

/* ── VIEWS ── */
.view{display:none;position:relative;z-index:10;height:calc(100vh - 68px);overflow:hidden;}
.view.active{display:flex;}

/* ── PANEL ── */
.panel{background:var(–panel);backdrop-filter:blur(10px);position:relative;overflow:hidden;}
.panel::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(–p),transparent);opacity:0.4;pointer-events:none;}
.ph{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px;padding-bottom:8px;border-bottom:1px solid rgba(170,255,0,0.12);}
.pt{font-family:‘Orbitron’,sans-serif;font-size:9px;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(–p);}
.pbb{font-size:8px;padding:2px 6px;border:1px solid var(–pb);color:var(–p);letter-spacing:1px;}

/* ── METRIC ── */
.mblock{margin-bottom:10px;border:1px solid rgba(170,255,0,0.12);background:rgba(0,15,0,0.5);}
.mhdr{padding:5px 10px;font-size:8px;letter-spacing:2px;text-transform:uppercase;color:var(–td);background:rgba(170,255,0,0.04);border-bottom:1px solid rgba(170,255,0,0.08);}
.mval{padding:8px 10px;font-family:‘Orbitron’,sans-serif;font-size:20px;font-weight:700;color:var(–p);text-shadow:0 0 10px rgba(170,255,0,0.4);}
.msub{padding:0 10px 7px;font-size:9px;color:var(–td);}

/* ── MINI BAR ── */
.mbar{display:flex;align-items:center;gap:6px;margin:5px 0;}
.mbl{font-size:8px;width:85px;color:var(–td);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.mbt{flex:1;height:3px;background:rgba(170,255,0,0.08);}
.mbf{height:100%;background:var(–p);box-shadow:0 0 4px var(–p);transition:width 0.8s ease;}
.mbv{font-size:8px;color:var(–p);width:55px;text-align:right;}

/* ── CURRENCY ── */
.crow{display:flex;gap:4px;margin-bottom:10px;flex-wrap:wrap;}
.cbtn{padding:3px 9px;font-size:9px;letter-spacing:1px;border:1px solid rgba(170,255,0,0.18);background:transparent;color:var(–td);cursor:pointer;transition:all 0.2s;font-family:‘Share Tech Mono’,monospace;}
.cbtn.active,.cbtn:hover{border-color:var(–p);color:var(–p);background:var(–pg);}

/* ── BUTTONS ── */
.btn{padding:7px 16px;font-family:‘Orbitron’,sans-serif;font-size:9px;letter-spacing:2px;text-transform:uppercase;cursor:pointer;transition:all 0.2s;border:1px solid;}
.btn-p{background:rgba(170,255,0,0.08);border-color:var(–p);color:var(–p);}
.btn-p:hover{background:rgba(170,255,0,0.18);box-shadow:0 0 12px rgba(170,255,0,0.2);}
.btn-g{background:transparent;border-color:rgba(170,255,0,0.2);color:var(–td);}
.btn-g:hover{border-color:var(–pd);color:var(–pd);}
.btn-new{display:flex;align-items:center;gap:6px;background:rgba(255,221,0,0.08);border:1px solid rgba(255,221,0,0.6);color:#ffdd00;padding:7px 16px;font-family:‘Orbitron’,sans-serif;font-size:9px;letter-spacing:2px;cursor:pointer;transition:all 0.2s;text-shadow:0 0 8px rgba(255,221,0,0.4);}
.btn-new:hover{background:rgba(255,221,0,0.18);box-shadow:0 0 14px rgba(255,221,0,0.25);border-color:rgba(255,221,0,0.9);}

/* ── FORM ── */
.fwrap{background:rgba(0,12,0,0.96);border:1px solid var(–pb);padding:16px;margin:12px;display:none;position:relative;}
.fwrap.open{display:block;}
.fwrap::before{content:’[ NEW COMMISSION RECORD ]’;position:absolute;top:-8px;left:12px;background:var(–bg2);padding:0 6px;font-size:9px;color:var(–p);letter-spacing:2px;}
.fgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:12px;}
.fg{display:flex;flex-direction:column;gap:4px;}
.fl{font-size:8px;color:var(–td);letter-spacing:1px;text-transform:uppercase;}
.fi{background:rgba(170,255,0,0.04);border:1px solid rgba(170,255,0,0.22);color:var(–tb);padding:6px 8px;font-family:‘Share Tech Mono’,monospace;font-size:11px;outline:none;transition:border-color 0.2s;width:100%;}
.fi:focus{border-color:var(–p);box-shadow:0 0 8px rgba(170,255,0,0.1);}
select.fi option{background:#0a1200;}
.facts{display:flex;gap:8px;justify-content:flex-end;}

/* ── TABLE ── */
.twrap{flex:1;overflow-y:auto;padding:0 12px 12px;}
table{width:100%;border-collapse:collapse;}
thead{position:sticky;top:0;z-index:5;}
th{background:rgba(2,8,0,0.99);padding:8px 10px;font-size:8px;letter-spacing:2px;text-transform:uppercase;color:var(–td);border-bottom:2px solid rgba(170,255,0,0.18);text-align:left;white-space:nowrap;}
td{padding:9px 10px;font-size:10px;border-bottom:1px solid rgba(170,255,0,0.05);transition:background 0.12s;}
tr:hover td{background:rgba(170,255,0,0.03);}
.tid{color:var(–td);font-size:9px;}
.tcl{color:var(–tb);font-weight:600;}
.tpr{color:var(–y);}
.tam{color:var(–p);font-family:‘Orbitron’,sans-serif;font-size:11px;text-align:right;}
.tam.paid{color:var(–g);}
.tam.partial{color:var(–am);}
.tdt{color:var(–td);font-size:9px;}

/* ── BADGES ── */
.badge{padding:2px 7px;font-size:8px;letter-spacing:1px;border:1px solid;display:inline-block;}
.bpaid{border-color:rgba(85,255,68,0.4);color:#55ff44;background:rgba(85,255,68,0.07);}
.bpart{border-color:rgba(255,204,0,0.4);color:#ffcc00;background:rgba(255,204,0,0.07);}
.bpend{border-color:rgba(255,221,0,0.35);color:#ffdd00;background:rgba(255,221,0,0.06);}
.bprog{border-color:rgba(170,255,0,0.35);color:#aaff00;background:rgba(170,255,0,0.07);}
.bcanc{border-color:rgba(255,51,85,0.3);color:#ff3355;background:rgba(255,51,85,0.05);}
.tchip{padding:2px 6px;font-size:8px;border-left:2px solid;background:rgba(0,0,0,0.3);}
.tc-arch{border-color:#aaff00;color:#aaff00;}
.tc-char{border-color:#ffdd00;color:#ffdd00;}
.tc-prod{border-color:#88ff44;color:#88ff44;}
.tc-vfx{border-color:#ffaa00;color:#ffaa00;}
.tc-env{border-color:#44ff88;color:#44ff88;}
.tc-anim{border-color:#ff3355;color:#ff3355;}
.tc-viz{border-color:#ccff00;color:#ccff00;}
.tc-3dm{border-color:#00ffcc;color:#00ffcc;}
.tc-plan{border-color:#ff88ff;color:#ff88ff;}
.tc-rend{border-color:#ffff44;color:#ffff44;}
.rbtn{padding:3px 8px;font-size:8px;letter-spacing:1px;border:1px solid;cursor:pointer;background:transparent;font-family:‘Share Tech Mono’,monospace;transition:all 0.15s;margin-left:4px;}
.re{border-color:rgba(170,255,0,0.22);color:var(–pd);}
.re:hover{border-color:var(–p);color:var(–p);background:var(–pg);}
.rd{border-color:rgba(255,51,85,0.2);color:rgba(255,51,85,0.5);}
.rd:hover{border-color:#ff3355;color:#ff3355;background:rgba(255,51,85,0.08);}

/* ── FILTER ── */
.fbar{display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.sw{position:relative;}
.si{position:absolute;left:8px;top:50%;transform:translateY(-50%);font-size:10px;color:var(–td);}
.sinput{background:rgba(170,255,0,0.04);border:1px solid rgba(170,255,0,0.18);color:var(–tb);padding:6px 10px 6px 26px;font-family:‘Share Tech Mono’,monospace;font-size:10px;width:180px;outline:none;}
.sinput::placeholder{color:var(–td);}
.fsel{background:rgba(0,8,0,0.95);border:1px solid rgba(170,255,0,0.18);color:var(–td);padding:6px 10px;font-family:‘Share Tech Mono’,monospace;font-size:10px;outline:none;cursor:pointer;}
.fsel:focus{border-color:var(–p);}

/* ── SCROLLBAR ── */
::-webkit-scrollbar{width:4px;height:4px;}
::-webkit-scrollbar-track{background:rgba(170,255,0,0.02);}
::-webkit-scrollbar-thumb{background:rgba(170,255,0,0.2);}
::-webkit-scrollbar-thumb:hover{background:rgba(170,255,0,0.35);}

/* ── MODAL ── */
.mbg{position:fixed;inset:0;z-index:1000;background:rgba(0,0,0,0.75);backdrop-filter:blur(4px);display:none;align-items:center;justify-content:center;}
.mbg.open{display:flex;}
.modal{background:var(–bg2);border:1px solid var(–pb);box-shadow:0 0 40px rgba(170,255,0,0.12);padding:24px;width:520px;max-width:95vw;position:relative;}
.modal::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(–p),transparent);}
.mtitle{font-family:‘Orbitron’,sans-serif;font-size:11px;letter-spacing:3px;color:var(–p);margin-bottom:16px;text-transform:uppercase;}

/* ── NOTIF ── */
.notif{position:fixed;bottom:20px;right:20px;z-index:2000;background:rgba(4,10,0,0.97);border:1px solid var(–pb);padding:10px 16px;font-size:10px;color:var(–p);letter-spacing:1px;transform:translateY(60px);opacity:0;transition:all 0.3s;}
.notif.show{transform:translateY(0);opacity:1;}
.empty{text-align:center;padding:40px;color:var(–td);font-size:11px;letter-spacing:2px;}

/* ── DASHBOARD LAYOUT ── */
.dlayout{display:grid;grid-template-columns:240px 1fr 240px;height:100%;gap:1px;background:rgba(170,255,0,0.05);width:100%;}
.dleft,.dright{overflow-y:auto;padding:12px;}
.dcenter{display:flex;flex-direction:column;overflow:hidden;}
.dtb{padding:10px 14px;background:var(–panel);border-bottom:1px solid rgba(170,255,0,0.1);display:flex;align-items:center;gap:10px;flex-wrap:wrap;flex-shrink:0;}

/* ── CHARTS ── */
.chart-card{background:rgba(0,14,0,0.88);border:1px solid rgba(170,255,0,0.14);padding:14px;position:relative;animation:fadeUp 0.4s ease;}
.chart-card::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(–p),transparent);opacity:0.35;}
.ctitle{font-family:‘Orbitron’,sans-serif;font-size:8px;letter-spacing:3px;color:var(–p);margin-bottom:10px;text-transform:uppercase;}
.svg-chart{width:100%;overflow:visible;}

/* SVG chart elements */
.grid-line{stroke:rgba(170,255,0,0.08);stroke-width:1;}
.axis-line{stroke:rgba(170,255,0,0.25);stroke-width:1;}
.axis-label{fill:rgba(122,159,80,0.9);font-family:‘Share Tech Mono’,monospace;font-size:9px;}
.bar-rect{transition:opacity 0.2s;}
.bar-rect:hover{opacity:0.8;}
.line-path{fill:none;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;}
.area-path{stroke:none;}
.dot{transition:r 0.2s;}
.dot:hover{r:6;}
.tooltip-box{pointer-events:none;}

/* Donut */
.donut-wrap{display:flex;align-items:center;gap:12px;}
.donut-legend{display:flex;flex-direction:column;gap:5px;flex:1;}
.dl-row{display:flex;align-items:center;gap:6px;font-size:8px;color:var(–td);}
.dl-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;}
.dl-val{margin-left:auto;color:var(–p);font-size:8px;}

/* Heat map */
.hmap{display:grid;gap:2px;}
.hcell{border-radius:1px;transition:opacity 0.3s;}
.hcell:hover{outline:1px solid var(–p);}

/* Radar */
.radar-label{fill:var(–td);font-family:‘Share Tech Mono’,monospace;font-size:8px;}

/* Sparkline row */
.spark-row{display:flex;gap:3px;align-items:flex-end;height:30px;margin:4px 0;}
.spark-bar{flex:1;background:rgba(170,255,0,0.3);border-top:1px solid rgba(170,255,0,0.7);min-height:2px;transition:background 0.2s;}
.spark-bar:hover{background:rgba(170,255,0,0.6);}

/* ANALYTICS GRID */
.agrid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;padding:14px;overflow-y:auto;height:100%;width:100%;}

/* PIPELINE */
.pgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:10px;padding:14px;overflow-y:auto;width:100%;}
.pcard{background:rgba(0,16,0,0.8);border:1px solid rgba(170,255,0,0.18);padding:14px;position:relative;transition:all 0.2s;}
.pcard:hover{border-color:var(–pb);box-shadow:0 0 16px rgba(170,255,0,0.08);}
.pcard::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(–p),transparent);opacity:0.3;}
.pbar{height:3px;background:rgba(170,255,0,0.1);margin-top:4px;}
.pbarfill{height:100%;transition:width 0.8s;}

/* COMM VIEW */
.cvwrap{display:flex;flex-direction:column;height:100%;width:100%;}
.ctbar{padding:10px 14px;border-bottom:1px solid rgba(170,255,0,0.1);display:flex;align-items:center;gap:10px;flex-wrap:wrap;flex-shrink:0;}

/* Corner deco */
.cl,.cr,.cbl,.cbr{position:absolute;width:10px;height:10px;pointer-events:none;}
.cl{top:0;left:0;border-top:1px solid var(–p);border-left:1px solid var(–p);}
.cr{top:0;right:0;border-top:1px solid var(–p);border-right:1px solid var(–p);}
.cbl{bottom:0;left:0;border-bottom:1px solid var(–p);border-left:1px solid var(–p);}
.cbr{bottom:0;right:0;border-bottom:1px solid var(–p);border-right:1px solid var(–p);}

/* pip sidebar */
.pipi{display:flex;align-items:center;gap:8px;padding:6px 8px;margin-bottom:4px;border:1px solid rgba(170,255,0,0.1);background:rgba(0,16,0,0.5);}
.pipi:hover{border-color:var(–pb);}
</style>

</head>
<body>
<div class="scanline"></div>

<!-- TOPBAR -->

<div class="topbar">
  <div style="display:flex;align-items:center;">
    <div class="logo flicker">MONARCH<span>X</span></div>
    <div class="topbar-tabs">
      <button class="ttab active" onclick="switchTab('dashboard',this)">DASHBOARD</button>
      <button class="ttab" onclick="switchTab('commissions',this)">ALL COMMISSIONS</button>
      <button class="ttab" onclick="switchTab('pipeline',this)">PIPELINE</button>
      <button class="ttab" onclick="switchTab('analytics',this)">ANALYTICS</button>
    </div>
  </div>
  <div class="topbar-right">
    <div class="sdot"></div><span>SYS ONLINE</span>
    <span style="opacity:0.3">|</span><span id="clock">--:--:--</span>
    <span style="opacity:0.3">|</span><span>RENDER.DB v3.0</span>
  </div>
</div>

<!-- SYSBAR -->

<div class="sysbar">
  <div class="sbi">NET.IO <span class="sbv">ACTIVE</span></div>
  <div class="sbi">DATALINK <span class="sbv" id="sb-count">00</span></div>
  <div class="sbi">REVENUE <span class="sbv" id="sb-total">—</span></div>
  <div class="sbi">PENDING <span class="sbv" id="sb-pending">—</span></div>
  <div class="sbi">JOBS <span class="sbv" id="sb-jobs">0</span></div>
  <div class="sbi">CURRENCY <span class="sbv" id="sb-currency">USD</span></div>
  <div class="sbend">3D · RENDER · COMMISSION DATABASE · CLASSIFIED</div>
</div>

<!-- ══════ DASHBOARD ══════ -->

<div class="view active" id="view-dashboard">
  <div class="dlayout">
    <!-- Left -->
    <div class="panel dleft">
      <div class="ph"><span class="pt">FINANCIALS</span><span class="pbb">LIVE</span></div>
      <div style="font-size:8px;color:var(--td);letter-spacing:1px;margin-bottom:6px;">CURRENCY</div>
      <div class="crow">
        <button class="cbtn active" onclick="setCurrency('USD','$')">USD</button>
        <button class="cbtn" onclick="setCurrency('EUR','€')">EUR</button>
        <button class="cbtn" onclick="setCurrency('GBP','£')">GBP</button>
        <button class="cbtn" onclick="setCurrency('JPY','¥')">JPY</button>
        <button class="cbtn" onclick="setCurrency('AUD','A$')">AUD</button>
        <button class="cbtn" onclick="setCurrency('CAD','C$')">CAD</button>
        <button class="cbtn" onclick="setCurrency('PHP','₱')">PHP</button>
        <button class="cbtn" onclick="setCurrency('SGD','S$')">SGD</button>
      </div>
      <div class="mblock"><div class="mhdr">TOTAL REVENUE</div><div class="mval" id="m-total">—</div><div class="msub" id="m-total-sub">0 commissions</div></div>
      <div class="mblock"><div class="mhdr">PAID</div><div class="mval" style="color:var(--g)" id="m-paid">—</div><div class="msub" id="m-paid-sub">0 invoices</div></div>
      <div class="mblock"><div class="mhdr">OUTSTANDING</div><div class="mval" style="color:var(--am)" id="m-owed">—</div><div class="msub" id="m-owed-sub">0 open</div></div>
      <div class="mblock"><div class="mhdr">AVG VALUE</div><div class="mval" style="font-size:16px" id="m-avg">—</div></div>
      <div class="mblock"><div class="mhdr">TOTAL RECORDS</div><div class="mval" style="font-size:24px" id="m-count">0</div></div>
      <!-- Donut chart -->
      <div style="font-size:8px;color:var(--td);letter-spacing:1px;margin:10px 0 6px;text-transform:uppercase;border-top:1px solid rgba(170,255,0,0.08);padding-top:10px;">STATUS SPLIT</div>
      <div class="donut-wrap">
        <svg id="donut-svg" width="80" height="80" viewBox="0 0 80 80"></svg>
        <div class="donut-legend" id="donut-legend"></div>
      </div>
    </div>

```
<!-- Center -->
<div class="panel dcenter">
  <div class="dtb">
    <button class="btn-new" onclick="toggleForm()"><span style="font-size:14px;line-height:1">+</span> NEW COMMISSION</button>
    <div style="margin-left:auto;font-size:9px;color:var(--td);">TOTAL: <span style="color:var(--p)" id="dash-count">0</span></div>
  </div>
  <div class="fwrap" id="addForm">
    <div class="cl"></div><div class="cr"></div><div class="cbl"></div><div class="cbr"></div>
    <div class="fgrid">
      <div class="fg"><label class="fl">Client</label><input type="text" class="fi" id="f-client" placeholder="CLIENT NAME"></div>
      <div class="fg"><label class="fl">Project</label><input type="text" class="fi" id="f-project" placeholder="PROJECT TITLE"></div>
      <div class="fg"><label class="fl">Type</label><select class="fi" id="f-type"><option>Architecture</option><option>Character</option><option>Product</option><option>VFX</option><option>Environment</option><option>Animation</option><option>Visualization</option><option>3D Modelling</option><option>Planning</option><option>Rendering</option></select></div>
      <div class="fg"><label class="fl">Amount (<span id="f-curr-lbl">USD</span>)</label><input type="number" class="fi" id="f-amount" placeholder="0.00" min="0" step="0.01"></div>
      <div class="fg"><label class="fl">Status</label><select class="fi" id="f-status"><option>Pending</option><option>In Progress</option><option>Partial</option><option>Paid</option><option>Cancelled</option></select></div>
      <div class="fg"><label class="fl">Date</label><input type="date" class="fi" id="f-date"></div>
      <div class="fg" style="grid-column:1/3"><label class="fl">Notes</label><input type="text" class="fi" id="f-notes" placeholder="NOTES..."></div>
      <div class="fg"><label class="fl">Software</label><input type="text" class="fi" id="f-software" placeholder="Blender, C4D..."></div>
    </div>
    <div class="facts">
      <button class="btn btn-g" onclick="toggleForm()">CANCEL</button>
      <button class="btn btn-p" onclick="submitCommission()">COMMIT RECORD</button>
    </div>
  </div>
  <div class="twrap">
    <table><thead><tr>
      <th>#</th><th>ID</th><th>CLIENT</th><th>PROJECT</th><th>TYPE</th>
      <th>STATUS</th><th style="text-align:right">AMOUNT</th><th>DATE</th><th style="text-align:right">OPS</th>
    </tr></thead><tbody id="dash-tbody"></tbody></table>
  </div>
</div>

<!-- Right -->
<div class="panel dright">
  <div class="ph"><span class="pt">ANALYTICS</span><span class="pbb">LIVE</span></div>
  <!-- Revenue sparkline 6mo -->
  <div style="font-size:8px;color:var(--td);letter-spacing:1px;margin-bottom:4px;">REVENUE 6 MO.</div>
  <svg id="dash-linechart" class="svg-chart" height="60"></svg>
  <div style="display:flex;justify-content:space-between;font-size:7px;color:var(--td);margin-bottom:10px;" id="dash-linelbls"></div>
  <!-- Type bar -->
  <div style="font-size:8px;color:var(--td);letter-spacing:1px;margin:10px 0 6px;border-top:1px solid rgba(170,255,0,0.08);padding-top:10px;">BY TYPE</div>
  <div id="type-breakdown"></div>
  <!-- Pipeline -->
  <div style="font-size:8px;color:var(--td);letter-spacing:1px;margin:10px 0 6px;border-top:1px solid rgba(170,255,0,0.08);padding-top:10px;">ACTIVE PIPELINE</div>
  <div id="dash-pipeline"></div>
</div>
```

  </div>
</div>

<!-- ══════ ALL COMMISSIONS ══════ -->

<div class="view" id="view-commissions">
  <div class="cvwrap">
    <div class="ctbar panel">
      <button class="btn-new" onclick="toggleForm()"><span style="font-size:14px;line-height:1">+</span> NEW COMMISSION</button>
      <div class="fbar">
        <div class="sw"><span class="si">⌕</span><input type="text" class="sinput" placeholder="SEARCH..." id="c-search" oninput="renderCommView()"></div>
        <select class="fsel" id="c-status" onchange="renderCommView()"><option value="">ALL STATUS</option><option value="Paid">PAID</option><option value="Partial">PARTIAL</option><option value="Pending">PENDING</option><option value="In Progress">IN PROGRESS</option><option value="Cancelled">CANCELLED</option></select>
        <select class="fsel" id="c-type" onchange="renderCommView()"><option value="">ALL TYPES</option><option value="Architecture">ARCHITECTURE</option><option value="Character">CHARACTER</option><option value="Product">PRODUCT</option><option value="VFX">VFX</option><option value="Environment">ENVIRONMENT</option><option value="Animation">ANIMATION</option><option value="Visualization">VISUALIZATION</option><option value="3D Modelling">3D MODELLING</option><option value="Planning">PLANNING</option><option value="Rendering">RENDERING</option></select>
        <select class="fsel" id="c-sort" onchange="renderCommView()"><option value="date-desc">DATE ↓</option><option value="date-asc">DATE ↑</option><option value="amount-desc">AMOUNT ↓</option><option value="amount-asc">AMOUNT ↑</option><option value="client">CLIENT A-Z</option></select>
      </div>
      <div style="margin-left:auto;font-size:9px;color:var(--td);">SHOWING <span style="color:var(--p)" id="c-count">0</span></div>
    </div>
    <div class="twrap">
      <table><thead><tr><th>#</th><th>ID</th><th>CLIENT</th><th>PROJECT</th><th>TYPE</th><th>SOFTWARE</th><th>STATUS</th><th style="text-align:right">AMOUNT</th><th>DATE</th><th>NOTES</th><th style="text-align:right">OPS</th></tr></thead><tbody id="comm-tbody"></tbody></table>
    </div>
  </div>
</div>

<!-- ══════ PIPELINE ══════ -->

<div class="view" id="view-pipeline">
  <div style="width:100%;display:flex;flex-direction:column;height:100%;">
    <div class="ctbar panel">
      <span class="pt">ACTIVE PIPELINE</span>
      <span style="font-size:9px;color:var(--td);margin-left:16px;">Pending · In Progress · Partial</span>
      <div style="margin-left:auto;font-size:9px;color:var(--td);">
        <span style="color:var(--p)" id="pipe-count">0</span> ACTIVE &nbsp;·&nbsp; <span style="color:var(--p)" id="pipe-total">—</span>
      </div>
    </div>
    <div class="pgrid" id="pipeline-grid"></div>
  </div>
</div>

<!-- ══════ ANALYTICS ══════ -->

<div class="view" id="view-analytics">
  <div class="agrid" id="agrid">

```
<!-- KPI row -->
<div class="chart-card">
  <div class="ctitle">TOTAL REVENUE</div>
  <div style="font-family:'Orbitron',sans-serif;font-size:26px;font-weight:700;color:var(--p);text-shadow:0 0 14px rgba(170,255,0,0.4)" id="a-total">—</div>
  <div style="font-size:9px;color:var(--td);margin-top:4px" id="a-total-sub">0 commissions</div>
  <!-- Cumulative sparkline -->
  <div style="margin-top:10px;font-size:8px;color:var(--td);letter-spacing:1px;margin-bottom:4px;">CUMULATIVE GROWTH</div>
  <svg id="a-cumul" class="svg-chart" height="40"></svg>
</div>

<div class="chart-card">
  <div class="ctitle">PAID vs PENDING</div>
  <svg id="a-donut2" width="100" height="100" viewBox="0 0 100 100" style="display:block;margin:0 auto 8px;"></svg>
  <div id="a-donut2-legend" style="display:flex;flex-direction:column;gap:4px;"></div>
</div>

<div class="chart-card">
  <div class="ctitle">AVG · HIGH · LOW</div>
  <div style="display:flex;flex-direction:column;gap:8px;margin-top:6px;">
    <div><div style="font-size:8px;color:var(--td)">AVERAGE</div><div style="font-family:'Orbitron',sans-serif;font-size:20px;color:var(--p)" id="a-avg">—</div></div>
    <div><div style="font-size:8px;color:var(--td)">HIGHEST</div><div style="font-family:'Orbitron',sans-serif;font-size:15px;color:var(--g)" id="a-max">—</div></div>
    <div><div style="font-size:8px;color:var(--td)">LOWEST</div><div style="font-family:'Orbitron',sans-serif;font-size:15px;color:var(--y)" id="a-min">—</div></div>
    <div><div style="font-size:8px;color:var(--td)">TOTAL JOBS</div><div style="font-family:'Orbitron',sans-serif;font-size:22px;color:var(--p)" id="a-count2">0</div></div>
  </div>
</div>

<!-- Monthly bar chart 12mo — span 2 cols -->
<div class="chart-card" style="grid-column:1/3;">
  <div class="ctitle">MONTHLY REVENUE BAR CHART — 12 MONTHS</div>
  <svg id="a-monthly-bar" class="svg-chart" height="120"></svg>
  <div style="display:flex;justify-content:space-between;font-size:7px;color:var(--td);margin-top:2px;" id="a-monthly-lbl"></div>
</div>

<!-- Line chart — revenue trend -->
<div class="chart-card">
  <div class="ctitle">REVENUE TREND LINE</div>
  <svg id="a-linechart" class="svg-chart" height="100"></svg>
</div>

<!-- Type donut -->
<div class="chart-card">
  <div class="ctitle">REVENUE BY TYPE</div>
  <div class="donut-wrap">
    <svg id="a-type-donut" width="90" height="90" viewBox="0 0 90 90"></svg>
    <div class="donut-legend" id="a-type-legend" style="font-size:8px;"></div>
  </div>
</div>

<!-- Scatter: amount vs time -->
<div class="chart-card">
  <div class="ctitle">COMMISSION SCATTER PLOT</div>
  <svg id="a-scatter" class="svg-chart" height="100"></svg>
</div>

<!-- Heat map: months x type -->
<div class="chart-card" style="grid-column:1/3;">
  <div class="ctitle">ACTIVITY HEAT MAP — MONTH × TYPE</div>
  <div id="a-heatmap" style="overflow-x:auto;"></div>
</div>

<!-- Radar: type radar chart -->
<div class="chart-card">
  <div class="ctitle">TYPE RADAR — COUNT</div>
  <svg id="a-radar" class="svg-chart" height="160" viewBox="0 0 200 160"></svg>
</div>

<!-- Top clients bar -->
<div class="chart-card">
  <div class="ctitle">TOP CLIENTS REVENUE</div>
  <svg id="a-client-bar" class="svg-chart" height="130"></svg>
</div>

<!-- Status stacked -->
<div class="chart-card">
  <div class="ctitle">STATUS DISTRIBUTION</div>
  <div id="a-status-bars" style="margin-top:6px;"></div>
</div>
```

  </div>
</div>

<!-- EDIT MODAL -->

<div class="mbg" id="editModal">
  <div class="modal">
    <div class="cl"></div><div class="cr"></div><div class="cbl"></div><div class="cbr"></div>
    <div class="mtitle">// EDIT COMMISSION RECORD</div>
    <div class="fgrid">
      <div class="fg"><label class="fl">Client</label><input type="text" class="fi" id="e-client"></div>
      <div class="fg"><label class="fl">Project</label><input type="text" class="fi" id="e-project"></div>
      <div class="fg"><label class="fl">Type</label><select class="fi" id="e-type"><option>Architecture</option><option>Character</option><option>Product</option><option>VFX</option><option>Environment</option><option>Animation</option><option>Visualization</option><option>3D Modelling</option><option>Planning</option><option>Rendering</option></select></div>
      <div class="fg"><label class="fl">Amount</label><input type="number" class="fi" id="e-amount" min="0" step="0.01"></div>
      <div class="fg"><label class="fl">Status</label><select class="fi" id="e-status"><option>Pending</option><option>In Progress</option><option>Partial</option><option>Paid</option><option>Cancelled</option></select></div>
      <div class="fg"><label class="fl">Date</label><input type="date" class="fi" id="e-date"></div>
      <div class="fg" style="grid-column:1/3"><label class="fl">Notes</label><input type="text" class="fi" id="e-notes"></div>
      <div class="fg"><label class="fl">Software</label><input type="text" class="fi" id="e-software"></div>
    </div>
    <div class="facts">
      <button class="btn btn-g" onclick="closeEdit()">CANCEL</button>
      <button class="btn btn-p" onclick="saveEdit()">UPDATE RECORD</button>
    </div>
  </div>
</div>
<div class="notif" id="notif"></div>

<script>
// ══ STATE ══
var C = [];
var currency = {code:'USD',sym:'$',rate:1};
var editIndex = -1;
var RATES = {USD:1,EUR:0.92,GBP:0.79,JPY:149.5,AUD:1.53,CAD:1.36,PHP:56.2,SGD:1.34};
var TYPE_TC = {Architecture:'tc-arch',Character:'tc-char',Product:'tc-prod',VFX:'tc-vfx',Environment:'tc-env',Animation:'tc-anim',Visualization:'tc-viz','3D Modelling':'tc-3dm',Planning:'tc-plan',Rendering:'tc-rend'};
var TYPE_HEX = {Architecture:'#aaff00',Character:'#ffdd00',Product:'#88ff44',VFX:'#ffaa00',Environment:'#44ff88',Animation:'#ff3355',Visualization:'#ccff00','3D Modelling':'#00ffcc',Planning:'#ff88ff',Rendering:'#ffff44'};
var TYPES = ['Architecture','Character','Product','VFX','Environment','Animation','Visualization','3D Modelling','Planning','Rendering'];
var STATUS_BC = {Paid:'bpaid',Partial:'bpart',Pending:'bpend','In Progress':'bprog',Cancelled:'bcanc'};
var STATUS_COL = {Paid:'#55ff44',Partial:'#ffcc00',Pending:'#ffdd00','In Progress':'#aaff00',Cancelled:'#ff3355'};

setInterval(function(){ document.getElementById('clock').textContent=new Date().toTimeString().slice(0,8); },1000);
document.getElementById('f-date').value = new Date().toISOString().slice(0,10);

// ══ TABS ══
function switchTab(tab,el){
  document.querySelectorAll('.ttab').forEach(function(t){t.classList.remove('active');});
  el.classList.add('active');
  document.querySelectorAll('.view').forEach(function(v){v.classList.remove('active');});
  document.getElementById('view-'+tab).classList.add('active');
  renderAll();
}

// ══ CURRENCY ══
function setCurrency(code,sym){
  currency={code:code,sym:sym,rate:RATES[code]};
  document.querySelectorAll('.cbtn').forEach(function(b){b.classList.toggle('active',b.textContent===code);});
  document.getElementById('f-curr-lbl').textContent=code;
  document.getElementById('sb-currency').textContent=code;
  renderAll();
}
function fmt(usd){
  var v=usd*currency.rate;
  if(currency.code==='JPY') return currency.sym+Math.round(v).toLocaleString();
  return currency.sym+v.toLocaleString(undefined,{minimumFractionDigits:2,maximumFractionDigits:2});
}

// ══ HELPERS ══
function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function notify(msg){var n=document.getElementById('notif');n.textContent='// '+msg;n.classList.add('show');clearTimeout(n._t);n._t=setTimeout(function(){n.classList.remove('show');},2800);}
function rowOps(id){return '<button class="rbtn re" onclick="openEdit(\''+id+'\')">EDIT</button><button class="rbtn rd" onclick="deleteC(\''+id+'\')">DEL</button>';}
function typeChip(t){return '<span class="tchip '+(TYPE_TC[t]||'tc-arch')+'">'+esc(t).toUpperCase()+'</span>';}
function statusBadge(s){return '<span class="badge '+(STATUS_BC[s]||'bpend')+'">'+esc(s).toUpperCase()+'</span>';}
function genId(){return 'MRC-'+String(C.length+1).padStart(4,'0')+'-'+Math.random().toString(36).slice(2,5).toUpperCase();}

function getFiltered(search,status,type,sort){
  var d=C.slice();
  if(search){var q=search.toLowerCase();d=d.filter(function(c){return(c.client+c.project+(c.notes||'')+(c.software||'')).toLowerCase().indexOf(q)>=0;});}
  if(status)d=d.filter(function(c){return c.status===status;});
  if(type)d=d.filter(function(c){return c.type===type;});
  d.sort(function(a,b){
    if(sort==='date-desc')return new Date(b.date)-new Date(a.date);
    if(sort==='date-asc')return new Date(a.date)-new Date(b.date);
    if(sort==='amount-desc')return b.amountUSD-a.amountUSD;
    if(sort==='amount-asc')return a.amountUSD-b.amountUSD;
    if(sort==='client')return a.client.localeCompare(b.client);
    return 0;
  });
  return d;
}

// ══ FORM / DATA ══
function toggleForm(){
  var f=document.getElementById('addForm');
  f.classList.toggle('open');
  if(f.classList.contains('open')){document.getElementById('f-date').value=new Date().toISOString().slice(0,10);document.getElementById('f-client').focus();}
}
function submitCommission(){
  var cl=document.getElementById('f-client').value.trim();
  var pr=document.getElementById('f-project').value.trim();
  var am=parseFloat(document.getElementById('f-amount').value)||0;
  if(!cl||!pr){notify('CLIENT & PROJECT REQUIRED');return;}
  C.unshift({id:genId(),client:cl,project:pr,type:document.getElementById('f-type').value,amountUSD:am/currency.rate,status:document.getElementById('f-status').value,date:document.getElementById('f-date').value||new Date().toISOString().slice(0,10),notes:document.getElementById('f-notes').value.trim(),software:document.getElementById('f-software').value.trim(),created:Date.now()});
  ['f-client','f-project','f-amount','f-notes','f-software'].forEach(function(id){document.getElementById(id).value='';});
  document.getElementById('f-date').value=new Date().toISOString().slice(0,10);
  renderAll();notify('COMMISSION RECORDED: '+C[0].id);
}
function deleteC(id){
  if(!confirm('DELETE THIS RECORD?'))return;
  C=C.filter(function(c){return c.id!==id;});
  renderAll();notify('RECORD DELETED');
}
function openEdit(id){
  var i=C.findIndex(function(c){return c.id===id;});
  if(i<0)return;
  editIndex=i;var c=C[i];
  document.getElementById('e-client').value=c.client;
  document.getElementById('e-project').value=c.project;
  document.getElementById('e-type').value=c.type;
  document.getElementById('e-amount').value=(c.amountUSD*currency.rate).toFixed(2);
  document.getElementById('e-status').value=c.status;
  document.getElementById('e-date').value=c.date;
  document.getElementById('e-notes').value=c.notes||'';
  document.getElementById('e-software').value=c.software||'';
  document.getElementById('editModal').classList.add('open');
}
function closeEdit(){document.getElementById('editModal').classList.remove('open');editIndex=-1;}
function saveEdit(){
  if(editIndex<0)return;
  var am=parseFloat(document.getElementById('e-amount').value)||0;
  var c=C[editIndex];
  C[editIndex]={id:c.id,created:c.created,client:document.getElementById('e-client').value.trim(),project:document.getElementById('e-project').value.trim(),type:document.getElementById('e-type').value,amountUSD:am/currency.rate,status:document.getElementById('e-status').value,date:document.getElementById('e-date').value,notes:document.getElementById('e-notes').value.trim(),software:document.getElementById('e-software').value.trim()};
  closeEdit();renderAll();notify('RECORD UPDATED');
}

// ══════════════════════════════════════
// CHART HELPERS
// ══════════════════════════════════════

// SVG namespace helper
function svgEl(tag,attrs){
  var el=document.createElementNS('http://www.w3.org/2000/svg',tag);
  for(var k in attrs)el.setAttribute(k,attrs[k]);
  return el;
}

// Draw a donut chart into an SVG element
function drawDonut(svgId,data,cx,cy,r,thick){
  var svg=document.getElementById(svgId);
  if(!svg)return;
  svg.innerHTML='';
  var total=data.reduce(function(s,d){return s+d.val;},0);
  if(total===0){svg.innerHTML='<text x="'+(cx)+'" y="'+(cy+4)+'" text-anchor="middle" fill="rgba(170,255,0,0.3)" font-family=\'Share Tech Mono\' font-size="9">NO DATA</text>';return;}
  var startAngle=-Math.PI/2;
  data.forEach(function(d){
    var slice=(d.val/total)*Math.PI*2;
    var endAngle=startAngle+slice;
    var x1=cx+r*Math.cos(startAngle),y1=cy+r*Math.sin(startAngle);
    var x2=cx+r*Math.cos(endAngle),y2=cy+r*Math.sin(endAngle);
    var large=slice>Math.PI?1:0;
    var ir=r-thick;
    var ix1=cx+ir*Math.cos(startAngle),iy1=cy+ir*Math.sin(startAngle);
    var ix2=cx+ir*Math.cos(endAngle),iy2=cy+ir*Math.sin(endAngle);
    var path=svgEl('path',{
      d:'M '+x1+' '+y1+' A '+r+' '+r+' 0 '+large+' 1 '+x2+' '+y2+' L '+ix2+' '+iy2+' A '+ir+' '+ir+' 0 '+large+' 0 '+ix1+' '+iy1+' Z',
      fill:d.color,opacity:'0.85'
    });
    path.style.cursor='default';
    path.setAttribute('title',d.label+': '+d.val);
    svg.appendChild(path);
    startAngle=endAngle;
  });
  // center text
  var txt=svgEl('text',{x:cx,y:cy-4,'text-anchor':'middle',fill:'#aaff00','font-family':'Share Tech Mono','font-size':'9','font-weight':'bold'});
  txt.textContent=total;
  svg.appendChild(txt);
  var txt2=svgEl('text',{x:cx,y:cy+8,'text-anchor':'middle',fill:'rgba(122,159,80,0.9)','font-family':'Share Tech Mono','font-size':'7'});
  txt2.textContent='TOTAL';
  svg.appendChild(txt2);
}

// Draw SVG bar chart
function drawBarChart(svgId,labels,values,colors,h){
  var svg=document.getElementById(svgId);
  if(!svg)return;
  var W=svg.parentElement?svg.parentElement.clientWidth-28:300;
  if(W<50)W=300;
  svg.setAttribute('width',W);
  svg.setAttribute('height',h);
  svg.innerHTML='';
  var pad={t:8,b:18,l:4,r:4};
  var n=labels.length;if(n===0)return;
  var cw=W-pad.l-pad.r;
  var ch=h-pad.t-pad.b;
  var maxV=Math.max.apply(null,values.concat([1]));
  var bw=Math.max(4,(cw/n)-3);
  // grid lines
  [0.25,0.5,0.75,1].forEach(function(f){
    var y=pad.t+ch-(ch*f);
    var gl=svgEl('line',{x1:pad.l,y1:y,x2:W-pad.r,y2:y,stroke:'rgba(170,255,0,0.07)',strokeWidth:'1'});
    svg.appendChild(gl);
  });
  values.forEach(function(v,i){
    var bh=Math.max(2,(v/maxV)*ch);
    var x=pad.l+(i*(cw/n))+(cw/n-bw)/2;
    var y=pad.t+ch-bh;
    var col=Array.isArray(colors)?colors[i%colors.length]:colors;
    var rect=svgEl('rect',{x:x,y:y,width:bw,height:bh,fill:col,opacity:'0.8',rx:'1'});
    var glow=svgEl('rect',{x:x,y:y,width:bw,height:2,fill:col,opacity:'0.9',rx:'1'});
    svg.appendChild(rect);
    svg.appendChild(glow);
    // label
    var lbl=svgEl('text',{x:x+bw/2,y:h-3,'text-anchor':'middle',fill:'rgba(122,159,80,0.8)','font-family':'Share Tech Mono','font-size':'7'});
    lbl.textContent=labels[i];
    svg.appendChild(lbl);
    // value tooltip on hover
    rect.addEventListener('mouseenter',function(){
      var tip=svgEl('text',{x:x+bw/2,y:y-3,'text-anchor':'middle',fill:'#aaff00','font-family':'Share Tech Mono','font-size':'8',id:'tip-'+i});
      tip.textContent=fmt(v/currency.rate);
      svg.appendChild(tip);
    });
    rect.addEventListener('mouseleave',function(){var t=svg.querySelector('#tip-'+i);if(t)svg.removeChild(t);});
  });
}

// Draw SVG line chart with area fill
function drawLineChart(svgId,values,color,h,showDots){
  var svg=document.getElementById(svgId);
  if(!svg)return;
  var W=svg.parentElement?svg.parentElement.clientWidth-28:300;
  if(W<50)W=300;
  svg.setAttribute('width',W);
  svg.setAttribute('height',h);
  svg.innerHTML='';
  if(values.length<2)return;
  var pad={t:8,b:8,l:4,r:4};
  var cw=W-pad.l-pad.r;
  var ch=h-pad.t-pad.b;
  var maxV=Math.max.apply(null,values.concat([1]));
  var minV=0;
  var pts=values.map(function(v,i){
    var x=pad.l+(i/(values.length-1))*cw;
    var y=pad.t+ch-((v-minV)/(maxV-minV))*ch;
    return {x:x,y:y,v:v};
  });
  // area
  var areaD='M '+pts[0].x+' '+(pad.t+ch);
  pts.forEach(function(p){areaD+=' L '+p.x+' '+p.y;});
  areaD+=' L '+pts[pts.length-1].x+' '+(pad.t+ch)+' Z';
  var col=color||'#aaff00';
  var area=svgEl('path',{d:areaD,fill:col,opacity:'0.06'});
  svg.appendChild(area);
  // grid
  var gl=svgEl('line',{x1:pad.l,y1:pad.t+ch,x2:W-pad.r,y2:pad.t+ch,stroke:'rgba(170,255,0,0.15)',strokeWidth:'1'});
  svg.appendChild(gl);
  // line
  var pathD='M '+pts[0].x+' '+pts[0].y;
  pts.forEach(function(p,i){if(i>0)pathD+=' L '+p.x+' '+p.y;});
  var line=svgEl('path',{d:pathD,fill:'none',stroke:col,strokeWidth:'1.5',strokeLinecap:'round',strokeLinejoin:'round'});
  svg.appendChild(line);
  // dots
  if(showDots)pts.forEach(function(p){
    var dot=svgEl('circle',{cx:p.x,cy:p.y,r:'2.5',fill:col,opacity:'0.9'});
    svg.appendChild(dot);
  });
}

// Draw scatter plot
function drawScatter(svgId,points,h){
  var svg=document.getElementById(svgId);
  if(!svg)return;
  var W=svg.parentElement?svg.parentElement.clientWidth-28:300;
  if(W<50)W=300;
  svg.setAttribute('width',W);
  svg.setAttribute('height',h);
  svg.innerHTML='';
  if(!points.length)return;
  var pad={t:8,b:8,l:8,r:8};
  var cw=W-pad.l-pad.r,ch=h-pad.t-pad.b;
  var xs=points.map(function(p){return p.x;});
  var ys=points.map(function(p){return p.y;});
  var minX=Math.min.apply(null,xs),maxX=Math.max.apply(null,xs.concat([minX+1]));
  var maxY=Math.max.apply(null,ys.concat([1]));
  // grid
  [0.25,0.5,0.75].forEach(function(f){
    var y=pad.t+ch-(ch*f);
    svg.appendChild(svgEl('line',{x1:pad.l,y1:y,x2:W-pad.r,y2:y,stroke:'rgba(170,255,0,0.06)',strokeWidth:'1'}));
  });
  // axis
  svg.appendChild(svgEl('line',{x1:pad.l,y1:pad.t+ch,x2:W-pad.r,y2:pad.t+ch,stroke:'rgba(170,255,0,0.2)',strokeWidth:'1'}));
  points.forEach(function(p){
    var cx=pad.l+((p.x-minX)/(maxX-minX))*cw;
    var cy=pad.t+ch-(p.y/maxY)*ch;
    var dot=svgEl('circle',{cx:cx,cy:cy,r:'3.5',fill:p.color||'#aaff00',opacity:'0.75'});
    svg.appendChild(dot);
  });
}

// Draw radar chart
function drawRadar(svgId,labels,values,color){
  var svg=document.getElementById(svgId);
  if(!svg)return;
  svg.innerHTML='';
  var cx=100,cy=80,R=58;
  var n=labels.length;
  if(!n)return;
  var maxV=Math.max.apply(null,values.concat([1]));
  // grid rings
  [0.25,0.5,0.75,1].forEach(function(f){
    var pts=[];
    for(var i=0;i<n;i++){var a=-Math.PI/2+(i/n)*Math.PI*2;pts.push((cx+R*f*Math.cos(a))+','+(cy+R*f*Math.sin(a)));}
    svg.appendChild(svgEl('polygon',{points:pts.join(' '),fill:'none',stroke:'rgba(170,255,0,0.1)',strokeWidth:'1'}));
  });
  // spokes
  for(var i=0;i<n;i++){
    var a=-Math.PI/2+(i/n)*Math.PI*2;
    svg.appendChild(svgEl('line',{x1:cx,y1:cy,x2:cx+R*Math.cos(a),y2:cy+R*Math.sin(a),stroke:'rgba(170,255,0,0.12)',strokeWidth:'1'}));
    var lx=cx+(R+12)*Math.cos(a),ly=cy+(R+12)*Math.sin(a);
    var lbl=svgEl('text',{x:lx,y:ly+3,'text-anchor':'middle',fill:'rgba(122,159,80,0.9)','font-family':'Share Tech Mono','font-size':'7'});
    lbl.textContent=labels[i].slice(0,4).toUpperCase();
    svg.appendChild(lbl);
  }
  // data polygon
  var dpts=[];
  for(var i=0;i<n;i++){
    var a=-Math.PI/2+(i/n)*Math.PI*2;
    var r=(values[i]/maxV)*R;
    dpts.push((cx+r*Math.cos(a))+','+(cy+r*Math.sin(a)));
  }
  var col=color||'#aaff00';
  svg.appendChild(svgEl('polygon',{points:dpts.join(' '),fill:col,opacity:'0.15',stroke:col,strokeWidth:'1.5'}));
  // dots
  for(var i=0;i<n;i++){
    var a=-Math.PI/2+(i/n)*Math.PI*2;
    var r=(values[i]/maxV)*R;
    svg.appendChild(svgEl('circle',{cx:cx+r*Math.cos(a),cy:cy+r*Math.sin(a),r:'3',fill:col,opacity:'0.9'}));
  }
}

// Draw heat map
function drawHeatmap(containerId,months,types,data){
  var el=document.getElementById(containerId);
  if(!el)return;
  el.innerHTML='';
  var table=document.createElement('table');
  table.style.cssText='border-collapse:separate;border-spacing:2px;font-size:8px;font-family:Share Tech Mono,monospace;';
  // header row
  var thead=document.createElement('tr');
  var th0=document.createElement('td');
  th0.style.cssText='color:rgba(122,159,80,0.6);font-size:7px;width:72px;';
  thead.appendChild(th0);
  months.forEach(function(m){
    var th=document.createElement('td');
    th.style.cssText='color:rgba(122,159,80,0.6);font-size:7px;text-align:center;padding:0 1px;min-width:28px;';
    th.textContent=m.slice(5);
    thead.appendChild(th);
  });
  table.appendChild(thead);
  // rows
  types.forEach(function(t){
    var tr=document.createElement('tr');
    var tlabel=document.createElement('td');
    tlabel.style.cssText='color:rgba(122,159,80,0.8);font-size:7px;padding-right:4px;white-space:nowrap;';
    tlabel.textContent=t.slice(0,7);
    tr.appendChild(tlabel);
    var maxVal=0;
    months.forEach(function(m){var v=data[t]&&data[t][m]||0;if(v>maxVal)maxVal=v;});
    var typeMax=0;
    types.forEach(function(tt){months.forEach(function(mm){var v=data[tt]&&data[tt][mm]||0;if(v>typeMax)typeMax=v;});});
    months.forEach(function(m){
      var v=data[t]&&data[t][m]||0;
      var intensity=typeMax>0?v/typeMax:0;
      var td=document.createElement('td');
      td.style.cssText='width:28px;height:20px;border-radius:2px;text-align:center;font-size:7px;';
      if(v>0){
        var col=TYPE_HEX[t]||'#aaff00';
        td.style.background='rgba('+hexToRgb(col)+','+Math.max(0.08,intensity*0.85)+')';
        td.style.color=intensity>0.5?col:'rgba(122,159,80,0.6)';
        td.textContent=v>0?v:'';
        td.title=t+' / '+m+': '+v+' job(s)';
      } else {
        td.style.background='rgba(170,255,0,0.03)';
      }
      tr.appendChild(td);
    });
    table.appendChild(tr);
  });
  el.appendChild(table);
}

function hexToRgb(hex){
  var r=parseInt(hex.slice(1,3),16),g=parseInt(hex.slice(3,5),16),b=parseInt(hex.slice(5,7),16);
  return r+','+g+','+b;
}

// ══════════════════════════════════════
// RENDER FUNCTIONS
// ══════════════════════════════════════

function getMonthKeys(n){
  var keys=[];
  var now=new Date();
  for(var i=n-1;i>=0;i--){
    var d=new Date(now.getFullYear(),now.getMonth()-i,1);
    keys.push(d.toISOString().slice(0,7));
  }
  return keys;
}

function renderSysbar(){
  var total=C.reduce(function(s,c){return s+c.amountUSD;},0);
  var pending=C.filter(function(c){return['Pending','In Progress','Partial'].indexOf(c.status)>=0;}).reduce(function(s,c){return s+c.amountUSD;},0);
  document.getElementById('sb-count').textContent=String(C.length).padStart(2,'0');
  document.getElementById('sb-total').textContent=fmt(total);
  document.getElementById('sb-pending').textContent=fmt(pending);
  document.getElementById('sb-jobs').textContent=C.length;
}

function renderDashLeft(){
  var total=C.reduce(function(s,c){return s+c.amountUSD;},0);
  var paid=C.filter(function(c){return c.status==='Paid';}).reduce(function(s,c){return s+c.amountUSD;},0);
  var owed=C.filter(function(c){return['Pending','In Progress','Partial'].indexOf(c.status)>=0;}).reduce(function(s,c){return s+c.amountUSD;},0);
  document.getElementById('m-total').textContent=fmt(total);
  document.getElementById('m-total-sub').textContent=C.length+' commissions';
  document.getElementById('m-paid').textContent=fmt(paid);
  document.getElementById('m-paid-sub').textContent=C.filter(function(c){return c.status==='Paid';}).length+' invoices';
  document.getElementById('m-owed').textContent=fmt(owed);
  document.getElementById('m-owed-sub').textContent=C.filter(function(c){return['Pending','In Progress','Partial'].indexOf(c.status)>=0;}).length+' open';
  document.getElementById('m-avg').textContent=fmt(C.length?total/C.length:0);
  document.getElementById('m-count').textContent=C.length;
  document.getElementById('dash-count').textContent=C.length;

  // Status donut (dashboard left)
  var sData=[
    {label:'Paid',val:C.filter(function(c){return c.status==='Paid';}).length,color:'#55ff44'},
    {label:'In Progress',val:C.filter(function(c){return c.status==='In Progress';}).length,color:'#aaff00'},
    {label:'Pending',val:C.filter(function(c){return c.status==='Pending';}).length,color:'#ffdd00'},
    {label:'Partial',val:C.filter(function(c){return c.status==='Partial';}).length,color:'#ffcc00'},
    {label:'Cancelled',val:C.filter(function(c){return c.status==='Cancelled';}).length,color:'#ff3355'},
  ].filter(function(d){return d.val>0;});
  drawDonut('donut-svg',sData,40,40,32,10);
  document.getElementById('donut-legend').innerHTML=sData.map(function(d){
    return '<div class="dl-row"><div class="dl-dot" style="background:'+d.color+'"></div><span>'+d.label+'</span><span class="dl-val">'+d.val+'</span></div>';
  }).join('');
}

function renderDashRight(){
  // Line chart 6 months
  var mks=getMonthKeys(6);
  var mmap={};mks.forEach(function(k){mmap[k]=0;});
  C.forEach(function(c){var k=(c.date||'').slice(0,7);if(k in mmap)mmap[k]+=c.amountUSD;});
  var mvals=mks.map(function(k){return mmap[k];});
  drawLineChart('dash-linechart',mvals,'#aaff00',60,true);
  document.getElementById('dash-linelbls').innerHTML=mks.map(function(k){
    return '<span>'+new Date(k+'-02').toLocaleString('default',{month:'short'})+'</span>';
  }).join('');

  // Type breakdown bars
  var typeMap={};
  C.forEach(function(c){typeMap[c.type]=(typeMap[c.type]||0)+c.amountUSD;});
  var te=Object.entries(typeMap).sort(function(a,b){return b[1]-a[1];});
  var maxT=te[0]?te[0][1]:1;
  document.getElementById('type-breakdown').innerHTML=te.map(function(e){
    var col=TYPE_HEX[e[0]]||'#aaff00';
    return '<div class="mbar"><span class="mbl">'+e[0]+'</span><div class="mbt"><div class="mbf" style="width:'+(e[1]/maxT*100).toFixed(1)+'%;background:'+col+';box-shadow:0 0 4px '+col+'"></div></div><span class="mbv" style="color:'+col+'">'+fmt(e[1])+'</span></div>';
  }).join('')||'<div style="font-size:9px;color:var(--td);padding:4px">No data</div>';

  // Pipeline list
  var pipe=C.filter(function(c){return['In Progress','Pending','Partial'].indexOf(c.status)>=0;}).slice(0,5);
  document.getElementById('dash-pipeline').innerHTML=pipe.length?pipe.map(function(c){
    var col=TYPE_HEX[c.type]||'#aaff00';
    return '<div class="pipi"><div style="width:6px;height:6px;border-radius:50%;background:'+col+';box-shadow:0 0 5px '+col+';flex-shrink:0"></div><div style="flex:1;overflow:hidden"><div style="font-size:9px;color:var(--tb);white-space:nowrap;overflow:hidden;text-overflow:ellipsis">'+esc(c.project)+'</div><div style="font-size:8px;color:var(--td)">'+esc(c.client)+'</div></div><div style="font-size:10px;color:'+col+';font-family:Orbitron,sans-serif">'+fmt(c.amountUSD)+'</div></div>';
  }).join(''):'<div style="font-size:9px;color:var(--td);padding:6px">No active jobs</div>';
}

function renderDashTable(){
  var data=getFiltered('','','','date-desc');
  var tbody=document.getElementById('dash-tbody');
  if(!data.length){tbody.innerHTML='<tr><td colspan="9"><div class="empty"><div style="font-size:28px;opacity:0.2;margin-bottom:10px">⬡</div>NO RECORDS · ADD YOUR FIRST COMMISSION</div></td></tr>';return;}
  tbody.innerHTML=data.map(function(c,i){
    var ac=c.status==='Paid'?'paid':c.status==='Partial'?'partial':'';
    return '<tr><td style="color:var(--td);font-size:9px;opacity:0.5">'+(i+1)+'</td><td class="tid">'+esc(c.id)+'</td><td class="tcl">'+esc(c.client)+'</td><td class="tpr">'+esc(c.project)+'</td><td>'+typeChip(c.type)+'</td><td>'+statusBadge(c.status)+'</td><td class="tam '+ac+'">'+fmt(c.amountUSD)+'</td><td class="tdt">'+c.date+'</td><td style="text-align:right">'+rowOps(c.id)+'</td></tr>';
  }).join('');
}

function renderCommView(){
  var search=document.getElementById('c-search').value;
  var status=document.getElementById('c-status').value;
  var type=document.getElementById('c-type').value;
  var sort=document.getElementById('c-sort').value;
  var data=getFiltered(search,status,type,sort);
  document.getElementById('c-count').textContent=data.length;
  var tbody=document.getElementById('comm-tbody');
  if(!data.length){tbody.innerHTML='<tr><td colspan="11"><div class="empty"><div style="font-size:28px;opacity:0.2;margin-bottom:10px">⬡</div>NO RECORDS FOUND</div></td></tr>';return;}
  tbody.innerHTML=data.map(function(c,i){
    var ac=c.status==='Paid'?'paid':c.status==='Partial'?'partial':'';
    return '<tr><td style="color:var(--td);font-size:9px;opacity:0.5">'+(i+1)+'</td><td class="tid">'+esc(c.id)+'</td><td class="tcl">'+esc(c.client)+'</td><td class="tpr">'+esc(c.project)+'</td><td>'+typeChip(c.type)+'</td><td style="font-size:9px;color:var(--td)">'+esc(c.software||'—')+'</td><td>'+statusBadge(c.status)+'</td><td class="tam '+ac+'">'+fmt(c.amountUSD)+'</td><td class="tdt">'+c.date+'</td><td style="font-size:9px;color:var(--td);max-width:100px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">'+esc(c.notes||'—')+'</td><td style="text-align:right">'+rowOps(c.id)+'</td></tr>';
  }).join('');
}

function renderPipelineView(){
  var pipe=C.filter(function(c){return['In Progress','Pending','Partial'].indexOf(c.status)>=0;});
  var total=pipe.reduce(function(s,c){return s+c.amountUSD;},0);
  document.getElementById('pipe-count').textContent=pipe.length;
  document.getElementById('pipe-total').textContent=fmt(total);
  var grid=document.getElementById('pipeline-grid');
  if(!pipe.length){grid.innerHTML='<div class="empty" style="grid-column:1/-1"><div style="font-size:28px;opacity:0.2;margin-bottom:10px">⬡</div>NO ACTIVE PIPELINE</div>';return;}
  grid.innerHTML=pipe.map(function(c){
    var prog=c.status==='Partial'?50:c.status==='In Progress'?65:10;
    var col=TYPE_HEX[c.type]||'#aaff00';
    return '<div class="pcard"><div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:10px"><div><div style="font-size:11px;color:var(--tb);font-weight:600;margin-bottom:2px">'+esc(c.project)+'</div><div style="font-size:9px;color:var(--td)">'+esc(c.client)+'</div></div><div><div style="font-family:Orbitron,sans-serif;font-size:14px;color:'+col+'">'+fmt(c.amountUSD)+'</div><div style="text-align:right;margin-top:4px">'+statusBadge(c.status)+'</div></div></div><div style="display:flex;gap:8px;align-items:center">'+typeChip(c.type)+(c.software?'<span style="font-size:8px;color:var(--td)">'+esc(c.software)+'</span>':'')+'</div><div style="margin-top:10px"><div style="display:flex;justify-content:space-between;font-size:8px;color:var(--td);margin-bottom:4px"><span>PROGRESS</span><span>'+prog+'%</span></div><div class="pbar"><div class="pbarfill" style="width:'+prog+'%;background:'+col+';box-shadow:0 0 6px '+col+'"></div></div></div><div style="font-size:8px;color:var(--td);margin-top:6px">'+c.date+'</div>'+(c.notes?'<div style="font-size:8px;color:var(--td);margin-top:4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">// '+esc(c.notes)+'</div>':'')+'<div style="margin-top:10px;text-align:right">'+rowOps(c.id)+'</div></div>';
  }).join('');
}

function renderAnalyticsView(){
  var total=C.reduce(function(s,c){return s+c.amountUSD;},0);
  var paid=C.filter(function(c){return c.status==='Paid';}).reduce(function(s,c){return s+c.amountUSD;},0);
  var owed=C.filter(function(c){return['Pending','In Progress','Partial'].indexOf(c.status)>=0;}).reduce(function(s,c){return s+c.amountUSD;},0);
  var amounts=C.map(function(c){return c.amountUSD;});
  var avg=C.length?total/C.length:0;
  var maxA=amounts.length?Math.max.apply(null,amounts):0;
  var minA=amounts.length?Math.min.apply(null,amounts):0;

  document.getElementById('a-total').textContent=fmt(total);
  document.getElementById('a-total-sub').textContent=C.length+' commissions tracked';
  document.getElementById('a-avg').textContent=fmt(avg);
  document.getElementById('a-max').textContent=fmt(maxA);
  document.getElementById('a-min').textContent=fmt(minA);
  document.getElementById('a-count2').textContent=C.length;

  // Cumulative line
  var sorted=C.slice().sort(function(a,b){return new Date(a.date)-new Date(b.date);});
  var cumul=[];var run=0;
  sorted.forEach(function(c){run+=c.amountUSD;cumul.push(run);});
  drawLineChart('a-cumul',cumul,'#aaff00',40,false);

  // Paid/Pending donut
  var d2=[
    {label:'Paid',val:Math.round(paid),color:'#55ff44'},
    {label:'In Progress',val:Math.round(C.filter(function(c){return c.status==='In Progress';}).reduce(function(s,c){return s+c.amountUSD;},0)),color:'#aaff00'},
    {label:'Pending',val:Math.round(C.filter(function(c){return c.status==='Pending';}).reduce(function(s,c){return s+c.amountUSD;},0)),color:'#ffdd00'},
    {label:'Partial',val:Math.round(C.filter(function(c){return c.status==='Partial';}).reduce(function(s,c){return s+c.amountUSD;},0)),color:'#ffcc00'},
    {label:'Cancelled',val:Math.round(C.filter(function(c){return c.status==='Cancelled';}).reduce(function(s,c){return s+c.amountUSD;},0)),color:'#ff3355'},
  ].filter(function(d){return d.val>0;});
  drawDonut('a-donut2',d2,50,50,38,12);
  document.getElementById('a-donut2-legend').innerHTML=d2.map(function(d){
    return '<div class="dl-row"><div class="dl-dot" style="background:'+d.color+'"></div><span style="font-size:8px">'+d.label+'</span><span style="margin-left:auto;font-size:8px;color:'+d.color+'">'+fmt(d.val)+'</span></div>';
  }).join('');

  // Monthly bar chart 12mo
  var mks12=getMonthKeys(12);
  var mmap12={};mks12.forEach(function(k){mmap12[k]=0;});
  C.forEach(function(c){var k=(c.date||'').slice(0,7);if(k in mmap12)mmap12[k]+=c.amountUSD;});
  var mvals12=mks12.map(function(k){return mmap12[k];});
  var mlbls12=mks12.map(function(k){return new Date(k+'-02').toLocaleString('default',{month:'short'});});
  var mcols=mks12.map(function(k,i){return i===mks12.length-1?'#ffdd00':'#aaff00';});
  drawBarChart('a-monthly-bar',mlbls12,mvals12,mcols,120);
  document.getElementById('a-monthly-lbl').innerHTML=mlbls12.map(function(l){return '<span>'+l+'</span>';}).join('');

  // Line trend
  drawLineChart('a-linechart',mvals12,'#aaff00',100,true);

  // Type donut
  var typeMap={};
  C.forEach(function(c){typeMap[c.type]=(typeMap[c.type]||0)+c.amountUSD;});
  var typeData=Object.entries(typeMap).sort(function(a,b){return b[1]-a[1];}).map(function(e){return{label:e[0],val:Math.round(e[1]),color:TYPE_HEX[e[0]]||'#aaff00'};});
  drawDonut('a-type-donut',typeData,45,45,36,11);
  document.getElementById('a-type-legend').innerHTML=typeData.map(function(d){
    return '<div class="dl-row"><div class="dl-dot" style="background:'+d.color+'"></div><span style="font-size:8px">'+d.label+'</span><span class="dl-val" style="color:'+d.color+'">'+fmt(d.val)+'</span></div>';
  }).join('')||'<div style="font-size:9px;color:var(--td)">No data</div>';

  // Scatter: date vs amount
  var scatterPts=C.map(function(c){
    return{x:new Date(c.date).getTime(),y:c.amountUSD,color:TYPE_HEX[c.type]||'#aaff00'};
  });
  drawScatter('a-scatter',scatterPts,100);

  // Radar: count by type
  var typeCount=TYPES.map(function(t){return C.filter(function(c){return c.type===t;}).length;});
  drawRadar('a-radar',TYPES,typeCount,'#aaff00');

  // Heat map: months (last 8) x type
  var hmks=getMonthKeys(8);
  var hmData={};
  TYPES.forEach(function(t){
    hmData[t]={};
    hmks.forEach(function(m){
      hmData[t][m]=C.filter(function(c){return c.type===t&&(c.date||'').slice(0,7)===m;}).length;
    });
  });
  drawHeatmap('a-heatmap',hmks,TYPES,hmData);

  // Client bar chart
  var cmap={};
  C.forEach(function(c){cmap[c.client]=(cmap[c.client]||0)+c.amountUSD;});
  var ce=Object.entries(cmap).sort(function(a,b){return b[1]-a[1];}).slice(0,7);
  var clbls=ce.map(function(e){return e[0].slice(0,6);});
  var cvals=ce.map(function(e){return e[1];});
  var ccols=ce.map(function(_,i){var cols=['#aaff00','#ffdd00','#88ff44','#ffaa00','#44ff88','#ccff00','#ff9900'];return cols[i%cols.length];});
  drawBarChart('a-client-bar',clbls,cvals,ccols,130);

  // Status distribution bars
  var snames=['Paid','In Progress','Pending','Partial','Cancelled'];
  var svals=snames.map(function(s){return C.filter(function(c){return c.status===s;}).length;});
  var stotal=C.length||1;
  document.getElementById('a-status-bars').innerHTML=snames.map(function(s,i){
    var col=STATUS_COL[s];
    var pct=(svals[i]/stotal*100).toFixed(1);
    return '<div class="mbar"><span class="mbl">'+s+'</span><div class="mbt"><div class="mbf" style="width:'+pct+'%;background:'+col+'"></div></div><span style="font-size:8px;color:'+col+';width:30px;text-align:right">'+svals[i]+'</span></div>';
  }).join('');
}

function renderAll(){
  renderSysbar();
  renderDashLeft();
  renderDashRight();
  renderDashTable();
  renderCommView();
  renderPipelineView();
  renderAnalyticsView();
}

// ══ SEED DATA ══
C = [
  {id:'MRC-0001-AX7',client:'Nexus Studios',project:'City Block Viz',type:'Architecture',amountUSD:1200,status:'Paid',date:'2026-04-01',notes:'Night render 4K',software:'Blender',created:Date.now()},
  {id:'MRC-0002-BQ3',client:'PixelForge Co',project:'Hero Character Rig',type:'Character',amountUSD:850,status:'Paid',date:'2026-04-05',notes:'AAA game ready',software:'ZBrush, Maya',created:Date.now()},
  {id:'MRC-0003-CV9',client:'Luminary VFX',project:'Explosion SFX Package',type:'VFX',amountUSD:2100,status:'In Progress',date:'2026-04-10',notes:'8 shots Houdini',software:'Houdini',created:Date.now()},
  {id:'MRC-0004-DP2',client:'ArchViz Pro',project:'Interior Render Suite',type:'Architecture',amountUSD:3500,status:'Partial',date:'2026-03-20',notes:'50% deposit received',software:'3ds Max, Corona',created:Date.now()},
  {id:'MRC-0005-EW6',client:'Nexus Studios',project:'Product Turntable',type:'Product',amountUSD:600,status:'Paid',date:'2026-03-15',notes:'Watch commercial 4K',software:'Cinema 4D',created:Date.now()},
  {id:'MRC-0006-FT1',client:'SkyLine Media',project:'Forest Environment',type:'Environment',amountUSD:1800,status:'Pending',date:'2026-04-18',notes:'Open world biome',software:'Unreal Engine 5',created:Date.now()},
  {id:'MRC-0007-GR4',client:'NovaCorp',project:'Logo Animation Loop',type:'Animation',amountUSD:450,status:'Paid',date:'2026-02-28',notes:'15s seamless loop',software:'After Effects',created:Date.now()},
  {id:'MRC-0008-HK8',client:'PixelForge Co',project:'Sci-Fi Mech Unit',type:'Character',amountUSD:2200,status:'In Progress',date:'2026-04-20',notes:'High poly + LODs',software:'ZBrush, Substance',created:Date.now()},
  {id:'MRC-0009-JL2',client:'Orbit Creative',project:'Product Configurator',type:'Visualization',amountUSD:3200,status:'Paid',date:'2026-02-10',notes:'WebGL real-time',software:'Blender, Three.js',created:Date.now()},
  {id:'MRC-0010-KM5',client:'ArchViz Pro',project:'Exterior Aerial Render',type:'Architecture',amountUSD:980,status:'Cancelled',date:'2026-01-25',notes:'Client cancelled',software:'3ds Max',created:Date.now()},
  {id:'MRC-0011-LN9',client:'Titan Games',project:'Creature Concept Pack',type:'Character',amountUSD:1600,status:'Paid',date:'2026-01-10',notes:'6 creature designs',software:'ZBrush',created:Date.now()},
  {id:'MRC-0012-MP3',client:'SkyLine Media',project:'Urban Environment Kit',type:'Environment',amountUSD:2800,status:'In Progress',date:'2026-03-05',notes:'Modular city assets',software:'Blender, Substance',created:Date.now()},
  {id:'MRC-0013-NQ6',client:'NovaCorp',project:'Motion Brand Package',type:'Animation',amountUSD:750,status:'Paid',date:'2025-12-20',notes:'Full brand motion',software:'After Effects, C4D',created:Date.now()},
  {id:'MRC-0014-OR1',client:'Luminary VFX',project:'Fluid Simulation',type:'VFX',amountUSD:3100,status:'Partial',date:'2026-02-01',notes:'Ocean scene 4K',software:'Houdini, Nuke',created:Date.now()},
  {id:'MRC-0015-PS4',client:'Orbit Creative',project:'Jewellery Viz',type:'Product',amountUSD:880,status:'Paid',date:'2025-11-15',notes:'Luxury jewelry render',software:'KeyShot',created:Date.now()},
];

// Defer charts until layout is ready
setTimeout(renderAll, 100);
</script>

</body>
</html>
