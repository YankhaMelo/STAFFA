<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>5.7CF · Leads</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --black:#0A0A0A;--gold:#C9A84C;--gold-dim:#8A6F2E;--gold-glow:rgba(201,168,76,0.15);
    --white:#F5F5F0;--surface:#141414;--s2:#1C1C1C;--s3:#242424;
    --muted:#666;--muted2:#444;--red:#E05252;--orange:#D4803A;
    --green:#4CAF7D;--blue:#5B8DEF;--purple:#9B6EE8;
    --r:8px;--rs:5px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:var(--black);color:var(--white);font-family:'Inter',sans-serif;font-size:14px;min-height:100vh}
  /* TOPBAR */
  .topbar{display:flex;align-items:center;justify-content:space-between;padding:0 24px;height:56px;background:var(--surface);border-bottom:1px solid #222;position:sticky;top:0;z-index:100}
  .logo{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;color:var(--gold)}
  .logo span{color:var(--white)}
  .nav-tabs{display:flex;gap:4px}
  .nav-tab{padding:6px 16px;border-radius:var(--rs);font-size:13px;font-weight:600;cursor:pointer;border:none;background:transparent;color:var(--muted);transition:all .15s}
  .nav-tab.active{background:var(--s3);color:var(--white)}
  .nav-tab:hover:not(.active){color:var(--white)}
  .topbar-right{display:flex;gap:8px;align-items:center}
  /* BUTTONS */
  .btn{padding:8px 16px;border-radius:var(--rs);border:none;font-family:'Inter',sans-serif;font-size:13px;font-weight:600;cursor:pointer;transition:all .15s;display:inline-flex;align-items:center;gap:6px}
  .btn-gold{background:var(--gold);color:#000}.btn-gold:hover{background:#dbb95a}
  .btn-ghost{background:transparent;color:var(--muted);border:1px solid #333}.btn-ghost:hover{border-color:var(--gold);color:var(--gold)}
  .btn-sm{padding:5px 10px;font-size:12px}
  .btn-red{background:transparent;color:var(--red);border:1px solid #3a2020}.btn-red:hover{background:rgba(224,82,82,.1)}
  /* VIEWS */
  .view{display:none}.view.active{display:block}
  /* STATS */
  .statsbar{display:flex;gap:1px;background:#222;border-bottom:1px solid #222}
  .stat-item{flex:1;padding:14px 20px;background:var(--surface);display:flex;flex-direction:column;gap:3px}
  .stat-val{font-family:'Bebas Neue',sans-serif;font-size:28px;color:var(--white);line-height:1}
  .stat-val.gold{color:var(--gold)}.stat-val.green{color:var(--green)}.stat-val.red{color:var(--red)}
  .stat-label{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.8px}
  /* TOOLBAR */
  .toolbar{padding:12px 24px;display:flex;gap:8px;align-items:center;flex-wrap:wrap;border-bottom:1px solid #1a1a1a;background:var(--surface)}
  .toolbar-sep{width:1px;height:20px;background:#333;margin:0 4px}
  /* KANBAN */
  .kanban-wrap{padding:20px 24px;overflow-x:auto}
  .kanban{display:flex;gap:16px;min-width:max-content}
  .column{width:280px;background:var(--surface);border-radius:var(--r);border:1px solid #222;display:flex;flex-direction:column}
  .col-hdr{padding:14px 16px;border-bottom:1px solid #222;display:flex;align-items:center;justify-content:space-between}
  .col-title{font-weight:600;font-size:13px;display:flex;align-items:center;gap:8px}
  .col-dot{width:8px;height:8px;border-radius:50%}
  .col-novo .col-dot{background:var(--muted)}.col-contactado .col-dot{background:var(--gold)}
  .col-aula .col-dot{background:var(--orange)}.col-convertido .col-dot{background:var(--green)}.col-perdido .col-dot{background:var(--red)}
  .col-cnt{font-size:11px;color:var(--muted);background:#222;padding:2px 7px;border-radius:99px}
  .col-body{padding:12px;display:flex;flex-direction:column;gap:10px;min-height:200px;flex:1}
  /* CARD */
  .card{background:var(--s2);border-radius:var(--rs);border:1px solid #2a2a2a;padding:12px;cursor:pointer;transition:border-color .15s,box-shadow .15s;position:relative}
  .card:hover{border-color:#3a3a3a}
  .card.hot{border-left:3px solid var(--gold);animation:pulse 3s ease-in-out infinite}
  .card.warm{border-left:3px solid var(--orange)}
  .card.cold{border-left:3px solid var(--muted2)}
  @keyframes pulse{0%,100%{box-shadow:0 0 0 0 var(--gold-glow)}50%{box-shadow:0 0 12px 2px var(--gold-glow)}}
  .card-name{font-weight:600;font-size:14px;margin-bottom:3px}
  .card-phone{font-size:12px;color:var(--muted);margin-bottom:7px}
  .card-meta{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:7px}
  .tag{font-size:10px;font-weight:600;padding:2px 7px;border-radius:99px;text-transform:uppercase;letter-spacing:.5px}
  .tag-obj{background:#1a1a2e;color:#7b8cde}
  .tag-exp{background:#1a2a1a;color:#6bcf7f}
  .tag-mod{background:#1a1a1a;color:#aaa;border:1px solid #333}
  .tag-hot{background:rgba(201,168,76,.15);color:var(--gold);border:1px solid rgba(201,168,76,.3)}
  .tag-warm{background:rgba(212,128,58,.12);color:var(--orange);border:1px solid rgba(212,128,58,.3)}
  .tag-cold{background:rgba(100,100,100,.12);color:var(--muted);border:1px solid #333}
  .tag-canal{background:#1a1a2a;color:#8ab4f8;border:1px solid #2a3a5a}
  .ai-badge{font-size:10px;color:var(--gold);background:rgba(201,168,76,.1);border:1px solid rgba(201,168,76,.2);padding:1px 6px;border-radius:99px;font-weight:600}
  .card-foot{display:flex;justify-content:space-between;align-items:center;margin-top:4px}
  .card-days{font-size:11px;color:var(--muted)}.card-days.urgent{color:var(--red);font-weight:600}
  .card-acts{display:flex;gap:4px}
  .icon-btn{width:26px;height:26px;border-radius:4px;background:#2a2a2a;border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;color:var(--muted);font-size:13px;transition:all .15s}
  .icon-btn:hover{background:#333;color:var(--white)}
  .icon-btn.wa:hover{background:rgba(37,211,102,.15);color:#25d366}
  .empty-col{text-align:center;padding:24px 12px;color:var(--muted2);font-size:12px;line-height:1.6}
  /* MODAL */
  .overlay{position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:200;display:flex;align-items:center;justify-content:center;backdrop-filter:blur(4px)}
  .overlay.hidden{display:none}
  .modal{background:var(--s2);border-radius:12px;border:1px solid #2a2a2a;width:520px;max-width:95vw;max-height:90vh;overflow-y:auto}
  .modal-hdr{padding:20px 24px 16px;border-bottom:1px solid #2a2a2a;display:flex;align-items:center;justify-content:space-between}
  .modal-title{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:1px}
  .modal-body{padding:20px 24px;display:flex;flex-direction:column;gap:14px}
  .modal-foot{padding:16px 24px;border-top:1px solid #2a2a2a;display:flex;gap:10px;justify-content:flex-end}
  .xbtn{background:none;border:none;color:var(--muted);font-size:20px;cursor:pointer;padding:4px}.xbtn:hover{color:var(--white)}
  /* FORM */
  .field{display:flex;flex-direction:column;gap:6px}
  .field label{font-size:12px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.7px}
  .field input,.field select,.field textarea{background:var(--s3);border:1px solid #2a2a2a;border-radius:var(--rs);color:var(--white);font-family:'Inter',sans-serif;font-size:14px;padding:10px 12px;outline:none;transition:border-color .15s;width:100%}
  .field input:focus,.field select:focus,.field textarea:focus{border-color:var(--gold)}
  .field textarea{resize:vertical;min-height:60px}
  .field select option{background:var(--s3)}
  .form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
  /* CHECKBOX PILLS */
  .pill-group{display:flex;gap:8px;flex-wrap:wrap}
  .chk-inp{display:none}
  .chk-lbl{padding:7px 14px;border-radius:99px;border:1px solid #333;font-size:12px;font-weight:600;cursor:pointer;color:var(--muted);transition:all .15s;user-select:none}
  .chk-inp:checked+.chk-lbl{border-color:var(--gold);color:var(--gold);background:rgba(201,168,76,.1)}
  .chk-lbl:hover{border-color:#555;color:var(--white)}
  /* EXP PILLS */
  .exp-pills{display:flex;gap:8px}
  .exp-pill{padding:7px 14px;border-radius:99px;border:1px solid #333;font-size:12px;font-weight:600;cursor:pointer;color:var(--muted);transition:all .15s;background:transparent}
  .exp-pill.sel{border-color:var(--green);color:var(--green);background:rgba(76,175,125,.1)}
  /* STAGE PILLS */
  .stage-row{display:flex;gap:8px;flex-wrap:wrap}
  .stage-pill{padding:6px 14px;border-radius:99px;border:1px solid #333;font-size:12px;font-weight:600;cursor:pointer;background:transparent;color:var(--muted);transition:all .15s}
  .stage-pill.a-novo{background:#333;color:var(--white);border-color:#555}
  .stage-pill.a-contactado{background:rgba(201,168,76,.15);color:var(--gold);border-color:var(--gold-dim)}
  .stage-pill.a-aula{background:rgba(212,128,58,.12);color:var(--orange);border-color:var(--orange)}
  .stage-pill.a-convertido{background:rgba(76,175,125,.12);color:var(--green);border-color:var(--green)}
  .stage-pill.a-perdido{background:rgba(224,82,82,.12);color:var(--red);border-color:var(--red)}
  .stage-pill:hover{border-color:#555;color:var(--white)}
  /* AI */
  .ai-panel{background:var(--s3);border-radius:var(--rs);border:1px solid rgba(201,168,76,.2);padding:14px;display:flex;flex-direction:column;gap:10px}
  .ai-hdr{display:flex;align-items:center;gap:8px;font-size:12px;color:var(--gold);font-weight:600}
  .sec-lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.7px;margin-bottom:4px}
  .ai-msg{background:var(--s2);border:1px solid #333;border-radius:var(--rs);padding:12px 12px 12px 12px;font-size:13px;line-height:1.6;color:var(--white);white-space:pre-wrap;position:relative;padding-top:36px}
  .copy-btn{position:absolute;top:8px;right:8px;background:#333;border:none;border-radius:4px;color:var(--muted);font-size:11px;font-weight:600;padding:4px 8px;cursor:pointer;transition:all .15s}
  .copy-btn:hover{background:var(--gold);color:#000}
  .dots{display:flex;gap:4px;align-items:center}
  .dots span{width:6px;height:6px;background:var(--gold);border-radius:50%;animation:bop 1.2s infinite}
  .dots span:nth-child(2){animation-delay:.2s}.dots span:nth-child(3){animation-delay:.4s}
  @keyframes bop{0%,80%,100%{transform:scale(.7);opacity:.5}40%{transform:scale(1);opacity:1}}
  .divider{height:1px;background:#2a2a2a}
  /* EXP CIRCLES */
  .exp-circles{display:flex;align-items:center;gap:4px}
  .exp-circ{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;transition:all .2s}
  .exp-line{flex:1;height:2px;background:#222}
  /* FOLLOW-UP TAB */
  .fu-list{display:flex;flex-direction:column;gap:10px}
  .fu-item{background:var(--s3);border-radius:var(--rs);border:1px solid #2a2a2a;padding:12px;display:flex;flex-direction:column;gap:6px}
  .fu-item-hdr{display:flex;justify-content:space-between;align-items:center}
  .fu-date{font-size:12px;color:var(--muted)}
  .fu-feedback{font-size:13px;line-height:1.5}
  .fu-tags{display:flex;gap:6px;flex-wrap:wrap}
  .tag-resp{background:rgba(76,175,125,.12);color:var(--green);border:1px solid rgba(76,175,125,.3)}
  .tag-noresp{background:rgba(224,82,82,.12);color:var(--red);border:1px solid rgba(224,82,82,.3)}
  .tag-later{background:rgba(212,128,58,.12);color:var(--orange);border:1px solid rgba(212,128,58,.3)}
  .tag-inscrito{background:rgba(201,168,76,.15);color:var(--gold);border:1px solid rgba(201,168,76,.3)}
  /* REPORTS */
  .rep-wrap{padding:24px;display:flex;flex-direction:column;gap:20px}
  .rep-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px}
  .rep-card{background:var(--surface);border:1px solid #222;border-radius:var(--r);padding:20px}
  .rep-title{font-family:'Bebas Neue',sans-serif;font-size:16px;letter-spacing:1px;color:var(--gold);margin-bottom:16px;display:flex;justify-content:space-between;align-items:center}
  .rep-full{grid-column:1/-1}
  .week-nav{display:flex;gap:8px;align-items:center}
  .wnbtn{background:#222;border:1px solid #333;border-radius:4px;color:var(--muted);padding:3px 10px;cursor:pointer;font-size:13px}
  .wnbtn:hover{color:var(--white);border-color:#555}
  .wlbl{font-size:12px;color:var(--muted);font-family:Inter;font-weight:400;letter-spacing:0}
  .bar-chart{display:flex;align-items:flex-end;gap:6px;height:120px;padding-top:8px}
  .bar-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;height:100%;justify-content:flex-end}
  .bar{width:100%;border-radius:3px 3px 0 0;transition:height .3s;min-height:2px}
  .bar-v{font-size:11px;font-weight:600;color:var(--white)}
  .bar-l{font-size:10px;color:var(--muted);text-align:center}
  .rank-item{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid #222}
  .rank-item:last-child{border-bottom:none}
  .rank-bg{flex:1;height:6px;background:#222;border-radius:3px;overflow:hidden}
  .rank-fill{height:100%;border-radius:3px;transition:width .3s}
  .rank-lbl{font-size:13px;font-weight:600;width:110px}
  .rank-v{font-size:13px;font-weight:700;color:var(--gold);min-width:24px;text-align:right}
  .week-stats{display:grid;grid-template-columns:repeat(5,1fr);gap:10px;margin-bottom:16px}
  .ws{background:var(--s2);border-radius:var(--rs);padding:12px;text-align:center}
  .ws-v{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--gold)}
  .ws-l{font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:.7px;margin-top:2px}
  /* SEARCH */
  .srch{background:var(--s2);border:1px solid #2a2a2a;border-radius:var(--rs);color:var(--white);font-family:'Inter',sans-serif;font-size:13px;padding:7px 14px;outline:none;width:200px;transition:border-color .15s,width .2s}
  .srch:focus{border-color:var(--gold);width:240px}
  /* TOAST */
  .toast{position:fixed;bottom:24px;right:24px;z-index:999;background:var(--s2);border:1px solid var(--gold);color:var(--white);padding:12px 18px;border-radius:var(--r);font-size:13px;font-weight:500;opacity:0;transition:opacity .2s;pointer-events:none}
  .toast.show{opacity:1}
  /* IMPORT BTN */
  .import-bar{padding:10px 24px;background:rgba(201,168,76,.05);border-bottom:1px solid rgba(201,168,76,.15);display:flex;align-items:center;gap:12px;font-size:13px;color:var(--muted)}
  /* SCROLLBAR */
  ::-webkit-scrollbar{width:6px;height:6px}::-webkit-scrollbar-track{background:transparent}::-webkit-scrollbar-thumb{background:#333;border-radius:3px}
  /* PRINT */
  @media print{
    body{background:white;color:#111}
    .topbar,.toolbar,.statsbar,.btn,.icon-btn,.ai-badge,.import-bar{display:none!important}
    .rep-wrap{padding:0}
    .rep-card{border:1px solid #ddd;background:white;page-break-inside:avoid}
    .rep-title{color:#C9A84C}.ws{background:#f5f5f5}.rank-bg{background:#eee}
    .bar-l,.ws-l,.rank-lbl{color:#555}.bar-v,.ws-v{color:#111}
  }
  /* AULA BADGE */
  .aula-badge{display:inline-flex;align-items:center;gap:6px;padding:8px 14px;border-radius:var(--rs);background:rgba(212,128,58,.1);border:1px solid rgba(212,128,58,.3);color:var(--orange);font-size:13px;font-weight:600}
  /* OBJETIVO FILTER */
  .obj-badge{font-size:11px;padding:3px 8px;border-radius:99px;font-weight:600}
  .obj-peso{background:#1a2a1a;color:#6bcf7f}
  .obj-musculo{background:#1a1a2e;color:#8ab4f8}
  .obj-condicao{background:#2a1a1a;color:#e08080}
  .obj-comp{background:#2a1a2a;color:#c080e0}
  .obj-bem{background:#1a2a2a;color:#80c0c0}
  .obj-reab{background:#2a2a1a;color:#c0c060}

  /* ══════════════════════════════════════════
     RESPONSIVE — TABLET (≤ 900px)
  ══════════════════════════════════════════ */
  @media (max-width:900px){
    .topbar{padding:0 16px;height:52px;gap:12px}
    .nav-tabs .nav-tab{padding:5px 10px;font-size:12px}
    .topbar-right .srch{width:140px}
    .statsbar{flex-wrap:wrap}
    .stat-item{min-width:calc(33.3% - 1px);padding:12px 14px}
    .stat-val{font-size:22px}
    .toolbar{padding:10px 16px;gap:6px}
    .kanban-wrap{padding:14px 16px}
    .column{width:240px}
    .rep-grid{grid-template-columns:1fr}
    .rep-wrap{padding:16px}
    .week-stats{grid-template-columns:repeat(3,1fr)}
    .form-row{grid-template-columns:1fr}
    .modal{width:95vw!important}
  }

  /* ══════════════════════════════════════════
     RESPONSIVE — MOBILE (≤ 600px)
  ══════════════════════════════════════════ */
  @media (max-width:600px){
    /* TOPBAR — logo only on mobile */
    .topbar{padding:0 14px;height:50px;justify-content:space-between}
    .desktop-nav{display:none!important}
    .topbar-right{gap:6px}
    .topbar-right .srch{display:none}
    .topbar-right .btn-ghost{display:none}
    .topbar-right .btn-gold{padding:6px 12px;font-size:12px}

    /* BOTTOM NAV */
    .bottom-nav{
      display:flex;position:fixed;bottom:0;left:0;right:0;
      background:var(--surface);border-top:1px solid #222;
      z-index:150;height:58px;
    }
    .bnav-item{
      flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;
      gap:3px;cursor:pointer;border:none;background:transparent;
      color:var(--muted);font-size:10px;font-weight:600;
      text-transform:uppercase;letter-spacing:.5px;transition:color .15s;
      padding-bottom:env(safe-area-inset-bottom,0);
    }
    .bnav-item.active{color:var(--gold)}
    .bnav-icon{font-size:20px;line-height:1}

    /* Add FAB */
    .mobile-fab{
      display:flex;position:fixed;bottom:70px;right:16px;z-index:160;
      width:52px;height:52px;border-radius:50%;background:var(--gold);
      color:#000;font-size:24px;font-weight:700;border:none;cursor:pointer;
      align-items:center;justify-content:center;
      box-shadow:0 4px 16px rgba(201,168,76,.4);
    }
    .mobile-search-bar{
      padding:10px 14px;background:var(--surface);border-bottom:1px solid #222;
      display:flex;gap:8px;
    }
    .mobile-search-bar input{
      flex:1;background:var(--s2);border:1px solid #2a2a2a;border-radius:var(--rs);
      color:var(--white);font-family:'Inter',sans-serif;font-size:14px;
      padding:9px 12px;outline:none;
    }
    .mobile-search-bar input:focus{border-color:var(--gold)}

    /* STATS — 2 col grid */
    .statsbar{display:grid;grid-template-columns:1fr 1fr;gap:1px}
    .stat-item{padding:10px 12px}
    .stat-val{font-size:24px}
    .stat-label{font-size:10px}

    /* TOOLBAR — scrollable horizontal */
    .toolbar{
      overflow-x:auto;flex-wrap:nowrap;padding:10px 14px;gap:6px;
      scrollbar-width:none;
    }
    .toolbar::-webkit-scrollbar{display:none}
    .toolbar-sep{display:none}
    .toolbar span{white-space:nowrap;flex-shrink:0}
    .toolbar .btn{flex-shrink:0}
    .toolbar select{flex-shrink:0;min-width:120px}

    /* KANBAN → VERTICAL LIST */
    .kanban-wrap{padding:0 0 80px 0}
    .kanban{
      display:flex;flex-direction:column;gap:0;min-width:unset;
      border-top:1px solid #222;
    }
    .column{
      width:100%;border-radius:0;border:none;
      border-bottom:1px solid #1a1a1a;
    }
    .col-hdr{
      padding:12px 14px;cursor:pointer;
      user-select:none;
    }
    .col-body{padding:0 14px 14px;min-height:unset}
    .col-body.collapsed{display:none}
    .col-hdr::after{content:'▾';margin-left:auto;color:var(--muted);font-size:12px}
    .col-hdr.collapsed::after{content:'▸'}

    /* CARDS in list mode */
    .card{border-radius:var(--rs);margin-bottom:8px}
    .card:last-child{margin-bottom:0}

    /* MODAL — full screen on mobile */
    .overlay{align-items:flex-end}
    .modal{
      width:100vw!important;max-width:100vw!important;
      border-radius:16px 16px 0 0;max-height:92vh;
    }
    .modal-hdr{padding:16px 18px 14px}
    .modal-body{padding:16px 18px}
    .modal-foot{padding:14px 18px}
    .form-row{grid-template-columns:1fr}

    /* FOLLOW-UP view */
    #view-followup .fu-header{flex-direction:column;gap:10px;align-items:flex-start}
    #view-followup .fu-filters{width:100%;display:flex;flex-direction:column;gap:8px}
    #view-followup .fu-filters select,
    #view-followup .fu-filters input{width:100%}
    #view-followup>div{padding:14px 14px 80px}

    /* REPORTS */
    .rep-wrap{padding:14px 14px 80px}
    .rep-grid{grid-template-columns:1fr}
    .week-stats{grid-template-columns:repeat(2,1fr);gap:8px}
    .rep-card{padding:14px}
    .week-nav{flex-wrap:wrap;gap:6px}
    .bar-chart{height:90px}
    .bar-l{font-size:9px}
    .rank-lbl{width:80px;font-size:12px}

    /* IMPORT BAR */
    .import-bar{flex-direction:column;align-items:flex-start;gap:8px;padding:12px 14px}

    /* DETAIL modal adjustments */
    .stage-row{gap:6px}
    .stage-pill{padding:5px 10px;font-size:11px}
    .exp-circles{gap:2px}
    .exp-circ{width:30px;height:30px;font-size:12px}
  }

  /* Hide bottom nav on desktop */
  .bottom-nav{display:none}
  .mobile-fab{display:none}
  .mobile-search-bar{display:none}

  /* Safe area for iPhone notch */
  @supports(padding-bottom: env(safe-area-inset-bottom)){
    .bottom-nav{padding-bottom:env(safe-area-inset-bottom)}
    .mobile-fab{bottom:calc(70px + env(safe-area-inset-bottom))}
  }

</style>
</head>
<body>


<!-- MOBILE BOTTOM NAV -->
<nav class="bottom-nav" id="bottomNav">
  <button class="bnav-item active" id="bn-pipeline" onclick="switchView('pipeline')">
    <span class="bnav-icon">📋</span>Pipeline
  </button>
  <button class="bnav-item" id="bn-followup" onclick="switchView('followup')">
    <span class="bnav-icon">📞</span>Follow-up
  </button>
  <button class="bnav-item" id="bn-relatorios" onclick="switchView('relatorios')">
    <span class="bnav-icon">📊</span>Relatórios
  </button>
</nav>
<!-- MOBILE FAB -->
<button class="mobile-fab" onclick="openAddModal()" id="mobileFab">+</button>

<div class="topbar">
  <div class="logo">5.7<span>CF</span> · LEADS</div>
  <div class="nav-tabs desktop-nav">
    <button class="nav-tab active" onclick="switchView('pipeline')">Pipeline</button>
    <button class="nav-tab" onclick="switchView('followup')">Follow-up</button>
    <button class="nav-tab" onclick="switchView('relatorios')">Relatórios</button>
  </div>
  <div class="topbar-right" id="topbarRight">
    <input class="srch" type="text" placeholder="🔍  Pesquisar..." id="searchInput" oninput="renderAll()">
    <button class="btn btn-ghost btn-sm" onclick="exportPDF()">↓ PDF</button>
    <button class="btn btn-gold" onclick="openAddModal()">+ Novo Lead</button>
  </div>
</div>

<!-- PIPELINE -->
<div class="view active" id="view-pipeline">
  <div class="mobile-search-bar" id="mobileSearchBar">
    <input type="text" placeholder="🔍  Pesquisar lead..." id="mobileSearchInput" oninput="syncSearch(this.value)">
  </div>
  <div class="statsbar" id="statsBar"></div>
  <!-- SETUP GUIDE (shown when no data) -->
  <div id="setupGuide" style="display:none;flex-direction:column;align-items:center;justify-content:center;padding:48px 24px;gap:16px;text-align:center;min-height:300px">
    <div style="font-size:48px">⚙️</div>
    <div style="font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:1px;color:var(--gold)">CONFIGURAÇÃO NECESSÁRIA</div>
    <div style="font-size:14px;color:var(--muted);max-width:320px;line-height:1.7">
      Para usar a app, precisas de criar as tabelas no Supabase.<br>
      Faz isto <strong style="color:var(--white)">uma vez no computador</strong>:
    </div>
    <div style="background:var(--surface);border:1px solid #333;border-radius:var(--r);padding:20px;max-width:360px;text-align:left;display:flex;flex-direction:column;gap:10px">
      <div style="font-size:13px;display:flex;gap:10px;align-items:flex-start"><span style="color:var(--gold);font-weight:700;min-width:20px">1.</span><span>Vai a <strong>supabase.com</strong> e abre o teu projeto</span></div>
      <div style="font-size:13px;display:flex;gap:10px;align-items:flex-start"><span style="color:var(--gold);font-weight:700;min-width:20px">2.</span><span>Clica em <strong>SQL Editor</strong> no menu da esquerda</span></div>
      <div style="font-size:13px;display:flex;gap:10px;align-items:flex-start"><span style="color:var(--gold);font-weight:700;min-width:20px">3.</span><span>Cola o conteúdo do ficheiro <strong>supabase_v3.sql</strong> e clica <strong>Run</strong></span></div>
      <div style="font-size:13px;display:flex;gap:10px;align-items:flex-start"><span style="color:var(--gold);font-weight:700;min-width:20px">4.</span><span>Volta aqui e clica <strong>"Importar agora"</strong></span></div>
    </div>
    <button class="btn btn-gold" onclick="loadAll()">↺ Tentar novamente</button>
  </div>
  <div id="importBar" class="import-bar" style="display:none">
    ✦ <strong style="color:var(--gold)" id="importCount">136</strong> leads do teu CRM prontos para importar &nbsp;
    <button class="btn btn-gold btn-sm" onclick="importCSVLeads()">Importar agora</button>
    <button class="btn btn-ghost btn-sm" onclick="document.getElementById('importBar').style.display='none'">Ignorar</button>
  </div>
  <div class="toolbar">
    <span style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.7px">Modalidade:</span>
    <button class="btn btn-gold btn-sm" id="fAll" onclick="setMF('')">Todas</button>
    <button class="btn btn-ghost btn-sm" id="fCF" onclick="setMF('CrossFit')">CrossFit</button>
    <button class="btn btn-ghost btn-sm" id="fCal" onclick="setMF('Calistenia')">Calistenia</button>
    <button class="btn btn-ghost btn-sm" id="fWL" onclick="setMF('Weightlifting')">Weightlifting</button>
    <button class="btn btn-ghost btn-sm" id="fHY" onclick="setMF('Hyrox')">Hyrox</button>
    <div class="toolbar-sep"></div>
    <span style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.7px">Objetivo:</span>
    <select id="objFilter" onchange="renderAll()" style="background:var(--s2);border:1px solid #333;border-radius:var(--rs);color:var(--white);font-size:12px;padding:5px 10px;outline:none">
      <option value="">Todos</option>
      <option value="Perder peso">Perder peso</option>
      <option value="Ganhar músculo">Ganhar músculo</option>
      <option value="Melhorar condição física">Melhorar condição</option>
      <option value="Competição / performance">Competição</option>
      <option value="Bem-estar geral">Bem-estar</option>
      <option value="Reabilitação">Reabilitação</option>
    </select>
  </div>
  <div class="kanban-wrap"><div class="kanban" id="kanban"></div></div>
</div>

<!-- FOLLOW-UP -->
<div class="view" id="view-followup">
  <div style="padding:20px 24px">
    <div class="fu-header" style="display:flex;justify-content:space-between;align-items:center;margin-bottom:16px;flex-wrap:wrap;gap:10px">
      <div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:1px">REGISTO DE CONTACTOS</div>
        <div style="font-size:13px;color:var(--muted);margin-top:2px">Histórico de follow-ups com todos os leads</div>
      </div>
      <div class="fu-filters" style="display:flex;gap:8px;flex-wrap:wrap">
        <select id="fuFilter" onchange="renderFollowUp()" style="background:var(--s2);border:1px solid #333;border-radius:var(--rs);color:var(--white);font-size:12px;padding:5px 10px;outline:none">
          <option value="">Todos os leads</option>
          <option value="respondeu">Responderam</option>
          <option value="nao_respondeu">Não responderam</option>
          <option value="mais_tarde">Pediram para voltar</option>
          <option value="inscrito">Passaram a inscritos</option>
        </select>
        <input class="srch" type="text" placeholder="🔍  Pesquisar..." id="fuSearch" oninput="renderFollowUp()" style="width:160px">
      </div>
    </div>
    <div id="fuList" class="fu-list"></div>
  </div>
</div>

<!-- RELATÓRIOS -->
<div class="view" id="view-relatorios">
  <div class="rep-wrap" id="repContent"></div>
</div>

<!-- ADD/EDIT MODAL -->
<div class="overlay hidden" id="addOverlay">
  <div class="modal">
    <div class="modal-hdr">
      <div class="modal-title" id="modalTitle">NOVO LEAD</div>
      <button class="xbtn" onclick="closeAdd()">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-row">
        <div class="field"><label>Nome *</label><input type="text" id="f_nome" placeholder="Nome completo"></div>
        <div class="field"><label>Telefone</label><input type="text" id="f_tel" placeholder="9xx xxx xxx"></div>
      </div>
      <div class="field">
        <label>Objetivo</label>
        <select id="f_obj">
          <option value="">Seleccionar...</option>
          <option>Perder peso</option><option>Ganhar músculo</option>
          <option>Melhorar condição física</option><option>Competição / performance</option>
          <option>Bem-estar geral</option><option>Reabilitação</option>
        </select>
      </div>
      <div class="field">
        <label>Modalidade de interesse</label>
        <div class="pill-group">
          <input type="checkbox" class="chk-inp" id="mc_cf" value="CrossFit"><label class="chk-lbl" for="mc_cf">CrossFit</label>
          <input type="checkbox" class="chk-inp" id="mc_cal" value="Calistenia"><label class="chk-lbl" for="mc_cal">Calistenia</label>
          <input type="checkbox" class="chk-inp" id="mc_wl" value="Weightlifting"><label class="chk-lbl" for="mc_wl">Weightlifting</label>
          <input type="checkbox" class="chk-inp" id="mc_hy" value="Hyrox"><label class="chk-lbl" for="mc_hy">Hyrox</label>
        </div>
      </div>
      <div class="field">
        <label>Experiências realizadas</label>
        <div class="exp-pills">
          <button type="button" class="exp-pill sel" data-exp="0" onclick="selExp(0)">Nenhuma</button>
          <button type="button" class="exp-pill" data-exp="1" onclick="selExp(1)">1ª Exp.</button>
          <button type="button" class="exp-pill" data-exp="2" onclick="selExp(2)">2ª Exp.</button>
          <button type="button" class="exp-pill" data-exp="3" onclick="selExp(3)">3ª Exp.</button>
        </div>
      </div>
      <div class="form-row">
        <div class="field"><label>Canal de origem</label>
          <select id="f_canal">
            <option value="">Desconhecido</option>
            <option value="instagram">Instagram</option>
            <option value="email">Email</option>
            <option value="site">Site</option>
            <option value="telefone">Telefone</option>
            <option value="presencial">Presencial</option>
            <option value="indicacao">Indicação</option>
          </select>
        </div>
        <div class="field"><label>Disponibilidade</label><input type="text" id="f_disp" placeholder="manhãs, 18h..."></div>
      </div>
      <div class="field"><label>Notas</label><textarea id="f_notas" placeholder="Contexto adicional..."></textarea></div>
      <div class="field"><label>Fase</label>
        <select id="f_fase">
          <option value="novo">Novo</option><option value="contactado">Contactado</option>
          <option value="aula">Aula experimental</option><option value="convertido">Convertido</option><option value="perdido">Perdido</option>
        </select>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeAdd()">Cancelar</button>
      <button class="btn btn-gold" onclick="saveLead()">Guardar</button>
    </div>
  </div>
</div>

<!-- AULA MODAL -->
<div class="overlay hidden" id="aulaOverlay">
  <div class="modal" style="width:420px">
    <div class="modal-hdr">
      <div class="modal-title" id="aulaTit">REGISTAR AULA</div>
      <button class="xbtn" onclick="document.getElementById('aulaOverlay').classList.add('hidden')">✕</button>
    </div>
    <div class="modal-body">
      <div class="aula-badge" id="aulaBadge">→ Avança para 2ª Experiência</div>
      <div class="field"><label>Modalidade desta aula</label>
        <div class="pill-group">
          <input type="checkbox" class="chk-inp" id="am_cf" value="CrossFit"><label class="chk-lbl" for="am_cf">CrossFit</label>
          <input type="checkbox" class="chk-inp" id="am_cal" value="Calistenia"><label class="chk-lbl" for="am_cal">Calistenia</label>
          <input type="checkbox" class="chk-inp" id="am_wl" value="Weightlifting"><label class="chk-lbl" for="am_wl">Weightlifting</label>
          <input type="checkbox" class="chk-inp" id="am_hy" value="Hyrox"><label class="chk-lbl" for="am_hy">Hyrox</label>
        </div>
      </div>
      <div class="field"><label>Notas da aula</label><textarea id="aulaNotas" placeholder="Como correu, interesse demonstrado..."></textarea></div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="document.getElementById('aulaOverlay').classList.add('hidden')">Cancelar</button>
      <button class="btn btn-gold" onclick="confirmAula()">Confirmar</button>
    </div>
  </div>
</div>

<!-- FOLLOW-UP MODAL -->
<div class="overlay hidden" id="fuOverlay">
  <div class="modal" style="width:460px">
    <div class="modal-hdr">
      <div>
        <div class="modal-title">REGISTAR CONTACTO</div>
        <div style="font-size:12px;color:var(--muted);margin-top:2px" id="fu_leadname"></div>
      </div>
      <button class="xbtn" onclick="document.getElementById('fuOverlay').classList.add('hidden')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-row">
        <div class="field"><label>Data do contacto</label><input type="date" id="fu_data"></div>
        <div class="field"><label>Canal</label>
          <select id="fu_canal">
            <option value="instagram">Instagram</option>
            <option value="email">Email</option>
            <option value="site">Site</option>
            <option value="telefone">Telefone</option>
            <option value="whatsapp">WhatsApp</option>
            <option value="presencial">Presencial</option>
          </select>
        </div>
      </div>
      <div class="field"><label>Feedback</label>
        <select id="fu_feedback">
          <option value="respondeu">Respondeu</option>
          <option value="nao_respondeu">Não respondeu</option>
          <option value="mais_tarde">Pediu para contactar mais tarde</option>
          <option value="sem_interesse">Sem interesse</option>
          <option value="agendou">Agendou aula</option>
        </select>
      </div>
      <div class="field">
        <label>Passou a inscrito?</label>
        <div class="pill-group">
          <input type="radio" name="fu_inscrito" id="fi_nao" value="nao" style="display:none" checked>
          <label class="chk-lbl" for="fi_nao" id="fi_nao_lbl">Não</label>
          <input type="radio" name="fu_inscrito" id="fi_sim" value="sim" style="display:none">
          <label class="chk-lbl" for="fi_sim" id="fi_sim_lbl">Sim — passou a membro!</label>
        </div>
      </div>
      <div class="field"><label>Observações</label><textarea id="fu_obs" placeholder="O que disse, próximo passo..."></textarea></div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="document.getElementById('fuOverlay').classList.add('hidden')">Cancelar</button>
      <button class="btn btn-gold" onclick="saveFU()">Guardar contacto</button>
    </div>
  </div>
</div>

<!-- DETAIL MODAL -->
<div class="overlay hidden" id="detailOverlay">
  <div class="modal" style="width:580px">
    <div class="modal-hdr">
      <div>
        <div class="modal-title" id="d_nome"></div>
        <div style="font-size:12px;color:var(--muted);margin-top:2px" id="d_phone"></div>
      </div>
      <div style="display:flex;gap:8px;align-items:center">
        <button class="btn btn-ghost btn-sm" onclick="openFUModal()">+ Contacto</button>
        <button class="btn btn-ghost btn-sm" onclick="editLead()">✏ Editar</button>
        <button class="xbtn" onclick="closeDetail()">✕</button>
      </div>
    </div>
    <div class="modal-body">
      <div style="display:flex;gap:8px;flex-wrap:wrap" id="d_tags"></div>
      <div class="divider"></div>
      <div>
        <div class="sec-lbl" style="margin-bottom:8px">Fase</div>
        <div class="stage-row" id="stageRow"></div>
      </div>
      <div>
        <div style="display:flex;gap:8px;align-items:center;margin-bottom:8px">
          <div class="sec-lbl">Experiências</div>
          <button class="btn btn-ghost btn-sm" id="aulaBtn" onclick="openAulaModal()">+ Registar aula</button>
        </div>
        <div class="exp-circles" id="expCircles"></div>
      </div>
      <div class="divider"></div>
      <div id="fuSection">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
          <div class="sec-lbl">Histórico de contactos</div>
        </div>
        <div id="d_fu_list"></div>
      </div>
      <div class="divider"></div>
      <div>
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
          <div class="sec-lbl">Análise IA</div>
          <button class="btn btn-ghost btn-sm" onclick="runAI()" id="aiBtn">✦ Analisar com IA</button>
        </div>
        <div id="aiPanel" class="ai-panel" style="display:none"></div>
      </div>
      <div id="d_notas_sec" style="display:none">
        <div class="divider"></div>
        <div class="sec-lbl" style="margin-bottom:6px">Notas</div>
        <div id="d_notas" style="font-size:13px;color:#aaa;line-height:1.6"></div>
      </div>
      <div class="divider"></div>
      <div class="sec-lbl" style="margin-bottom:4px">Criado em</div>
      <div id="d_created" style="font-size:13px;color:var(--muted)"></div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-red btn-sm" onclick="deleteLead()">🗑 Eliminar</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const SB = 'https://trqwlnsnvfcmnyjsfqjd.supabase.co';
const SK = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InRycXdsbnNudmZjbW55anNmcWpkIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODA5NzAwNjgsImV4cCI6MjA5NjU0NjA2OH0.9YVXbyCiJ-bF5YJ57u-HExDfAWeK2NBpkS25vDcsSAw';
const T = 'leads_crossfit';
const TFU = 'leads_followup';
const STAGES = [
  {k:'novo',l:'Novo'},{k:'contactado',l:'Contactado'},
  {k:'aula',l:'Aula experimental'},{k:'convertido',l:'Convertido'},{k:'perdido',l:'Perdido'}
];
const MODAIS = ['CrossFit','Calistenia','Weightlifting','Hyrox'];

let leads=[], followups=[], currentLead=null, editingId=null, modalFilter='', expSel=0, weekOff=0;

// CSV IMPORT DATA
const CSV_IMPORT = [{"nome":"Maria João","data_contacto_1":"7/1/2026","notas":"1º Contacto: Não respondeu\n2º Contacto (Atendeu a chamada)\nObs: Pediu para voltar a ser contacta para iniciar no inicio do próximo mês","fase":"perdido"},{"nome":"Manu fernandes","data_contacto_1":"","notas":"1º Contacto: não respondeu","fase":"perdido"},{"nome":"Afonso Castro","data_contacto_1":"27/01/2026","notas":"1º Contacto: não respondeu","fase":"perdido"},{"nome":"Fábio Oliveira","data_contacto_1":"","notas":"1º Contacto: inativo por falta de pagamento","fase":"perdido"},{"nome":"Nuno Fernandes","data_contacto_1":"24/02/2026","notas":"1º Contacto: 961711827 inativo","fase":"perdido"},{"nome":"Manuel Pereira","data_contacto_1":"25/02/2026","notas":"1º Contacto: 918904490","fase":"novo"},{"nome":"Francisca Lima","data_contacto_1":"","notas":"1º Contacto: 918765306","fase":"novo"},{"nome":"Daniel Pereira","data_contacto_1":"","notas":"1º Contacto: 915572817","fase":"novo"},{"nome":"Pedro Manuel Brites Pereira","data_contacto_1":"","notas":"1º Contacto: 960219883","fase":"novo"},{"nome":"Ricardo Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rui Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Margarida Salgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Mauro Teixeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Pedro Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Anabela Rego","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rui Manuel Almeida Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Licínio Macário","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Diogo Manuel Batista Domingues","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Sandra Cristina Carvalho Osório","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ricardo Alexandre Sampaio Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Carlos Miguel Barros Lobão","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vânia Isabel Fernandes Teixeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Eduardo Oliveira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vitor Miguel Almeida Cardoso","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Carolina Ferreira De Oliveira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Susana Daniela Rodrigues Guimarães","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vitória Dias","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Agostinho Matos","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Bernardo Ferreira De Oliveira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Afonso João Parente Dos Reis","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"André Miguel Pinto Almeida","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"José Alberto Fernandes Leite Boído","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Gonçalo Nuno Fonseca Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Dina Rafaela Domingues E Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Anabela Sofia Almeida Barbosa Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Pedro Miguel Soares Pinto","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"José Tiago Castro Pinto","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ana Rita Pontes Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"André Luis Leitão Magalhães","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Carla Veloso Almeida","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ana Isabel Da Costa","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Manuel Oliveira Fernandes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Tiago André Salado Peixoto","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luis Filipe Beites Alpoim","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Maria Manuela Pereira Mendes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Teresa Margarida De Abreu Barros","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Kelly Cristine Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Angela Martins Lima","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Eric Lee Chambers","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Wellbert Delfino da Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ana Do Carmo Rodrigues","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"André Emanuel Pires Martins","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Jorge David Costa Da Cunha","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Neto Ventura Lança","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Joaquim César Cardoso Faria","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Fernanda Crhistina Santiago Lins E Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luís Filipe Fernandes da Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"José Diogo Fonseca Magalhães","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Carlos De Sousa Areias","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luis Miguel De Almeida Machado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"José André Leal Mendes Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Diogo Moura","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luis Carlos Fernandes Salgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Diogo Cascais","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Lucinda Delgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Inês Maria Peixoto Pontes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rui Afonso Peixoto Pontes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Angelo Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Alanna Pahl","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João António Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Jennifer Pahl","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rita Cardoso","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Teresa Fontes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Diogo Carneiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Isidro Teixeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Francisco Salgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Eurico Peixoto","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Miguel Carneiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Lara Costa Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Pedro Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Fatima Carvalho","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Albertino Macieira Coelho De Macedo","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Rebelo","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Anabela Rego","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ana Catarina Pinto","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Cesário Guimarães","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luís Lobo","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rita Coelho","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vera Lopes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Abreu","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ricardo Miguel da Silva Martins","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Sandrine Gonçalves","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Raquel Abreu","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Filipe Mendes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ismael Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vítor Batista","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Carlota Milheiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Jaime Milheiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Maria João","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ricardo Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Fernando Ribeiro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Hewerton Camargo","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Vasco Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rafaela Vieira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"José Manuel Rodrigues Caldeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Fábio Alexandre Freitas Oliveira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Eduardo Barros","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Rui MARQUES","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Natasja","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Benjamin Fernandes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Joana Torres","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Mateus Teixeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Afonso de Castro","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Daniel Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Mayur Samegy","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Manuel Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luz Moscoso","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Margarida Salgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Mariana Santos","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Ana Rita Silva Alves","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Beatriz Freitas","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Maria Francisca Oliveira Coelho Lima","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Mauro Teixeira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Jéssica De Amorim Medeiros Da Cunha","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Luiz Fernando Do Nascimento Ferreira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Hector Smith","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"André Monteiro Pinheiro Figueiredo Benta","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"João Pedro Mendes De Oliveira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Inês Bastos","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Pedro Manuel Brites Pereira","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Raquel Salgado","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Tatiane Luiza Da Silva","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Pedro Fernandes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Nuno Fernandes","data_contacto_1":"","notas":"","fase":"novo"},{"nome":"Sabryna Amorim","data_contacto_1":"","notas":"","fase":"novo"}];

// ── SUPABASE ──────────────────────────────────────────────────────────────────
async function sb(path,opts={}){
  const r=await fetch(`${SB}/rest/v1/${path}`,{...opts,headers:{'apikey':SK,'Authorization':`Bearer ${SK}`,'Content-Type':'application/json','Prefer':opts.prefer||'',...opts.headers}});
  if(!r.ok)throw new Error(await r.text());
  const t=await r.text();return t?JSON.parse(t):null;
}
async function loadAll(){
  try{
    [leads,followups]=await Promise.all([
      sb(`${T}?order=created_at.desc`),
      sb(`${TFU}?order=data_contacto.desc`)
    ]);
    leads=leads||[];followups=followups||[];
  }catch(e){
    leads=[];followups=[];
    // Show setup guide on table-not-found errors
    const sg=document.getElementById('setupGuide');
    if(sg)sg.style.display='flex';
    const sb2=document.getElementById('statsBar');
    if(sb2)sb2.style.display='none';
    return;
  }
  renderAll();
  // Show import bar if no leads yet
  if(leads.length===0){document.getElementById('importBar').style.display='flex';}
}

async function importCSVLeads(){
  const btn=document.querySelector('#importBar .btn-gold');
  btn.textContent='A importar...';btn.disabled=true;
  const now=new Date().toISOString();
  const batch=CSV_IMPORT.map(r=>({nome:r.nome,notas:r.notas||null,fase:r.fase,origem:'csv_importado',canal:null,modalidades:[],experiencia_num:0,created_at:now,updated_at:now}));
  // Insert in chunks of 50
  for(let i=0;i<batch.length;i+=50){
    try{await sb(T,{method:'POST',prefer:'return=minimal',body:JSON.stringify(batch.slice(i,i+50))});}
    catch(e){showToast('Erro na importação: '+e.message,true);return;}
  }
  document.getElementById('importBar').style.display='none';
  showToast(`${batch.length} leads importados com sucesso ✓`);
  await 
// Mobile search sync
function syncSearch(val){
  const si=document.getElementById('searchInput');
  if(si)si.value=val;
  renderAll();
}

// Collapsible columns on mobile
function toggleCol(key){
  if(window.innerWidth>600)return;
  const body=document.getElementById('colbody_'+key);
  const hdr=document.getElementById('colhdr_'+key);
  if(!body||!hdr)return;
  const collapsed=body.classList.toggle('collapsed');
  hdr.classList.toggle('collapsed',collapsed);
}

loadAll();
}

// ── VIEW ──────────────────────────────────────────────────────────────────────
function switchView(v){
  document.querySelectorAll('.view').forEach(el=>el.classList.remove('active'));
  document.getElementById('view-'+v).classList.add('active');
  document.querySelectorAll('.nav-tab').forEach((t,i)=>t.classList.toggle('active',['pipeline','followup','relatorios'][i]===v));
  // Update bottom nav
  ['pipeline','followup','relatorios'].forEach(n=>{
    const el=document.getElementById('bn-'+n);
    if(el)el.classList.toggle('active',n===v);
  });
  // Show/hide mobile elements
  const fab=document.getElementById('mobileFab');
  const msb=document.getElementById('mobileSearchBar');
  if(fab)fab.style.display=v==='pipeline'?'flex':'none';
  if(msb)msb.style.display=v==='pipeline'?'flex':'none';
  const tr=document.getElementById('topbarRight');
  if(v==='relatorios'){
    tr.innerHTML=`<button class="btn btn-ghost btn-sm" onclick="exportPDF()">↓ PDF Relatório</button>`;
    renderReports();
  }else if(v==='followup'){
    tr.innerHTML=``;
    renderFollowUp();
  }else{
    tr.innerHTML=`<input class="srch" type="text" placeholder="🔍  Pesquisar..." id="searchInput" oninput="renderAll()"><button class="btn btn-ghost btn-sm" onclick="exportPDF()">↓ PDF</button><button class="btn btn-gold" onclick="openAddModal()">+ Novo Lead</button>`;
  }
}

// ── RENDER ────────────────────────────────────────────────────────────────────
function renderAll(){renderStats();renderKanban();}
function days(d){return Math.floor((new Date()-new Date(d))/86400000);}
function getFiltered(){
  const q=(document.getElementById('searchInput')?.value||'').trim().toLowerCase();
  const obj=document.getElementById('objFilter')?.value||'';
  return leads.filter(l=>{
    const mq=!q||(l.nome||'').toLowerCase().includes(q)||(l.telefone||'').includes(q);
    const mm=!modalFilter||(l.modalidades||[]).includes(modalFilter);
    const mo=!obj||l.objetivo===obj;
    return mq&&mm&&mo;
  });
}
function setMF(m){
  modalFilter=m;
  ['fAll','fCF','fCal','fWL','fHY'].forEach(id=>{const el=document.getElementById(id);if(el){el.className='btn btn-ghost btn-sm';}});
  const map={'':'fAll','CrossFit':'fCF','Calistenia':'fCal','Weightlifting':'fWL','Hyrox':'fHY'};
  const el=document.getElementById(map[m]);if(el)el.className='btn btn-gold btn-sm';
  renderKanban();
}
function renderStats(){
  const tot=leads.length,conv=leads.filter(l=>l.fase==='convertido').length;
  const taxa=tot?Math.round(conv/tot*100):0;
  const sem=leads.filter(l=>!['convertido','perdido'].includes(l.fase)&&days(l.updated_at||l.created_at)>=3).length;
  document.getElementById('statsBar').innerHTML=`
    <div class="stat-item"><div class="stat-val">${tot}</div><div class="stat-label">Total leads</div></div>
    <div class="stat-item"><div class="stat-val gold">${leads.filter(l=>l.fase==='novo').length}</div><div class="stat-label">Novos</div></div>
    <div class="stat-item"><div class="stat-val green">${conv}</div><div class="stat-label">Convertidos</div></div>
    <div class="stat-item"><div class="stat-val">${taxa}%</div><div class="stat-label">Taxa conversão</div></div>
    <div class="stat-item"><div class="stat-val ${sem>0?'red':''}">${sem}</div><div class="stat-label">Sem follow-up +3d</div></div>`;
}
function tempTag(l){
  if(!l.ai_temp)return'';
  if(l.ai_temp==='quente')return`<span class="tag tag-hot">🔥 Quente</span>`;
  if(l.ai_temp==='morno')return`<span class="tag tag-warm">~ Morno</span>`;
  return`<span class="tag tag-cold">❄ Frio</span>`;
}
function expLbl(n){return n===0?'Nenhuma':n===1?'1ª Exp.':n===2?'2ª Exp.':'3ª Exp.';}
function canalTag(c){
  if(!c)return'';
  const icons={instagram:'📸',email:'✉',site:'🌐',telefone:'📞',whatsapp:'💬',presencial:'🤝',indicacao:'👥'};
  return`<span class="tag tag-canal">${icons[c]||''} ${c}</span>`;
}
function objClass(obj){
  const m={'Perder peso':'obj-peso','Ganhar músculo':'obj-musculo','Melhorar condição física':'obj-condicao','Competição / performance':'obj-comp','Bem-estar geral':'obj-bem','Reabilitação':'obj-reab'};
  return m[obj]||'';
}
function renderKanban(){
  const fil=getFiltered(),kb=document.getElementById('kanban');
  kb.innerHTML='';
  STAGES.forEach(s=>{
    const sl=fil.filter(l=>l.fase===s.k);
    const col=document.createElement('div');
    col.className=`column col-${s.k}`;
    col.innerHTML=`<div class="col-hdr" id="colhdr_${s.k}" onclick="toggleCol('${s.k}')"><div class="col-title"><span class="col-dot"></span>${s.l}</div><span class="col-cnt">${sl.length}</span></div>
      <div class="col-body" id="colbody_${s.k}">${sl.length===0?'<div class="empty-col">Sem leads<br>nesta fase</div>':sl.map(renderCard).join('')}</div>`;
    kb.appendChild(col);
  });
  // Show setup guide if no leads at all
  const setupEl = document.getElementById('setupGuide');
  if(setupEl) setupEl.style.display = leads.length === 0 ? 'flex' : 'none';
}
function renderCard(l){
  const d=days(l.updated_at||l.created_at);
  const urg=d>=3&&!['convertido','perdido'].includes(l.fase);
  const tc=l.ai_temp==='quente'?'hot':l.ai_temp==='morno'?'warm':l.ai_temp==='frio'?'cold':'';
  const mods=(l.modalidades||[]).slice(0,2).map(m=>`<span class="tag tag-mod">${m}</span>`).join('');
  const en=l.experiencia_num||0;
  return`<div class="card ${tc}" onclick="openDetail('${l.id}')">
    <div class="card-name">${l.nome}</div>
    <div class="card-phone">${l.telefone||'—'}</div>
    <div class="card-meta">
      ${l.objetivo?`<span class="tag obj-badge ${objClass(l.objetivo)}">${l.objetivo}</span>`:''}
      ${en>0?`<span class="tag tag-exp">${expLbl(en)}</span>`:''}
      ${mods}${tempTag(l)}${l.ai_temp?`<span class="ai-badge">IA</span>`:''}
      ${canalTag(l.canal)}
    </div>
    <div class="card-foot">
      <span class="card-days ${urg?'urgent':''}">${d===0?'hoje':`há ${d}d`}</span>
      <div class="card-acts">${l.telefone?`<button class="icon-btn wa" onclick="openWA(event,'${l.telefone}')" title="WhatsApp">💬</button>`:''}</div>
    </div>
  </div>`;
}

// ── ADD/EDIT ──────────────────────────────────────────────────────────────────
function selExp(n){expSel=n;document.querySelectorAll('.exp-pill').forEach(p=>p.classList.toggle('sel',parseInt(p.dataset.exp)===n));}
function openAddModal(){
  editingId=null;
  document.getElementById('modalTitle').textContent='NOVO LEAD';
  ['f_nome','f_tel','f_disp','f_notas'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('f_obj').value='';document.getElementById('f_canal').value='';
  document.getElementById('f_fase').value='novo';
  ['mc_cf','mc_cal','mc_wl','mc_hy'].forEach(id=>document.getElementById(id).checked=false);
  selExp(0);document.getElementById('addOverlay').classList.remove('hidden');
}
function closeAdd(){document.getElementById('addOverlay').classList.add('hidden');}
function editLead(){
  if(!currentLead)return;closeDetail();editingId=currentLead.id;
  document.getElementById('modalTitle').textContent='EDITAR LEAD';
  document.getElementById('f_nome').value=currentLead.nome||'';
  document.getElementById('f_tel').value=currentLead.telefone||'';
  document.getElementById('f_obj').value=currentLead.objetivo||'';
  document.getElementById('f_canal').value=currentLead.canal||'';
  document.getElementById('f_disp').value=currentLead.disponibilidade||'';
  document.getElementById('f_notas').value=currentLead.notas||'';
  document.getElementById('f_fase').value=currentLead.fase||'novo';
  const m=currentLead.modalidades||[];
  document.getElementById('mc_cf').checked=m.includes('CrossFit');
  document.getElementById('mc_cal').checked=m.includes('Calistenia');
  document.getElementById('mc_wl').checked=m.includes('Weightlifting');
  document.getElementById('mc_hy').checked=m.includes('Hyrox');
  selExp(currentLead.experiencia_num||0);
  document.getElementById('addOverlay').classList.remove('hidden');
}
async function saveLead(){
  const nome=document.getElementById('f_nome').value.trim();
  if(!nome){showToast('Nome obrigatório',true);return;}
  const mods=[...document.querySelectorAll('#addOverlay .chk-inp:checked')].map(c=>c.value);
  const data={nome,telefone:document.getElementById('f_tel').value.trim(),objetivo:document.getElementById('f_obj').value,
    canal:document.getElementById('f_canal').value||null,modalidades:mods,experiencia_num:expSel,
    disponibilidade:document.getElementById('f_disp').value.trim(),notas:document.getElementById('f_notas').value.trim(),
    fase:document.getElementById('f_fase').value,updated_at:new Date().toISOString()};
  try{
    if(editingId){await sb(`${T}?id=eq.${editingId}`,{method:'PATCH',prefer:'return=representation',body:JSON.stringify(data)});showToast('Lead actualizado ✓');}
    else{data.created_at=new Date().toISOString();await sb(T,{method:'POST',prefer:'return=representation',body:JSON.stringify(data)});showToast('Lead adicionado ✓');}
    closeAdd();await loadAll();
  }catch(e){showToast('Erro: '+e.message,true);}
}

// ── DETAIL ────────────────────────────────────────────────────────────────────
function openDetail(id){
  const l=leads.find(x=>x.id===id);if(!l)return;currentLead=l;
  document.getElementById('d_nome').textContent=l.nome;
  document.getElementById('d_phone').textContent=l.telefone||'—';
  document.getElementById('d_created').textContent=l.created_at?new Date(l.created_at).toLocaleDateString('pt-PT',{day:'numeric',month:'long',year:'numeric'}):'—';
  // Tags
  const mods=(l.modalidades||[]).map(m=>`<span class="tag tag-mod">${m}</span>`).join('');
  document.getElementById('d_tags').innerHTML=[
    l.objetivo?`<span class="tag obj-badge ${objClass(l.objetivo)}">${l.objetivo}</span>`:'',
    mods,tempTag(l),canalTag(l.canal)
  ].join('');
  // Stages
  document.getElementById('stageRow').innerHTML=STAGES.map(s=>`<button class="stage-pill ${l.fase===s.k?'a-'+s.k:''}" onclick="changeStage('${l.id}','${s.k}')">${s.l}</button>`).join('');
  // Exp circles
  const en=l.experiencia_num||0;
  const circles=[1,2,3].map((n,i)=>`
    ${i>0?`<div class="exp-line"></div>`:''}
    <div style="text-align:center">
      <div class="exp-circ" style="border:2px solid ${n<=en?'var(--green)':'#333'};background:${n<=en?'rgba(76,175,125,.15)':'transparent'};color:${n<=en?'var(--green)':'var(--muted)'};">${n}</div>
      <div style="font-size:10px;color:var(--muted);margin-top:4px">${n}ª Exp.</div>
    </div>`).join('');
  document.getElementById('expCircles').innerHTML=circles;
  // Aula btn
  document.getElementById('aulaBtn').style.display=(en>=3||['convertido','perdido'].includes(l.fase))?'none':'inline-flex';
  // Follow-up history for this lead
  const lfu=followups.filter(f=>f.lead_id===l.id);
  const fuEl=document.getElementById('d_fu_list');
  if(lfu.length===0){
    fuEl.innerHTML=`<div style="font-size:13px;color:var(--muted2);padding:8px 0">Sem contactos registados ainda.</div>`;
  }else{
    const icons={instagram:'📸',email:'✉',site:'🌐',telefone:'📞',whatsapp:'💬',presencial:'🤝'};
    const flbls={respondeu:'Respondeu',nao_respondeu:'Não respondeu',mais_tarde:'Mais tarde',sem_interesse:'Sem interesse',agendou:'Agendou aula'};
    const fcls={respondeu:'tag-resp',nao_respondeu:'tag-noresp',mais_tarde:'tag-later',sem_interesse:'tag-noresp',agendou:'tag-resp'};
    fuEl.innerHTML=lfu.map(f=>`
      <div class="fu-item">
        <div class="fu-item-hdr">
          <span class="fu-date">${f.data_contacto?new Date(f.data_contacto).toLocaleDateString('pt-PT',{day:'numeric',month:'short',year:'numeric'}):''}</span>
          <span style="font-size:11px;color:var(--muted)">${icons[f.canal]||''} ${f.canal||''}</span>
        </div>
        <div class="fu-tags">
          <span class="tag ${fcls[f.feedback]||''}">${flbls[f.feedback]||f.feedback}</span>
          ${f.inscrito==='sim'?`<span class="tag tag-inscrito">⭐ Passou a membro</span>`:''}
        </div>
        ${f.observacoes?`<div class="fu-feedback">${f.observacoes}</div>`:''}
      </div>`).join('');
  }
  // Notas
  const ns=document.getElementById('d_notas_sec');
  if(l.notas){ns.style.display='block';document.getElementById('d_notas').textContent=l.notas;}else{ns.style.display='none';}
  // AI
  const aip=document.getElementById('aiPanel');
  if(l.ai_temp){renderAIPanel(l);aip.style.display='flex';document.getElementById('aiBtn').textContent='✦ Re-analisar';}
  else{aip.style.display='none';document.getElementById('aiBtn').textContent='✦ Analisar com IA';}
  document.getElementById('detailOverlay').classList.remove('hidden');
}
function closeDetail(){document.getElementById('detailOverlay').classList.add('hidden');currentLead=null;}
async function changeStage(id,stage){
  try{await sb(`${T}?id=eq.${id}`,{method:'PATCH',prefer:'return=representation',body:JSON.stringify({fase:stage,updated_at:new Date().toISOString()})});
    await loadAll();const u=leads.find(l=>l.id===id);if(u){currentLead=u;openDetail(id);}
  }catch(e){showToast('Erro: '+e.message,true);}
}
async function deleteLead(){
  if(!currentLead)return;
  if(!confirm(`Eliminar "${currentLead.nome}"?`))return;
  try{await sb(`${T}?id=eq.${currentLead.id}`,{method:'DELETE'});closeDetail();showToast('Lead eliminado');await loadAll();}
  catch(e){showToast('Erro: '+e.message,true);}
}

// ── AULA PROGRESSION ──────────────────────────────────────────────────────────
function openAulaModal(){
  if(!currentLead)return;
  const next=(currentLead.experiencia_num||0)+1;
  document.getElementById('aulaTit').textContent=`REGISTAR ${next}ª EXPERIÊNCIA`;
  document.getElementById('aulaBadge').textContent=`→ Avança para ${next}ª Experiência`;
  const m=currentLead.modalidades||[];
  document.getElementById('am_cf').checked=m.includes('CrossFit');
  document.getElementById('am_cal').checked=m.includes('Calistenia');
  document.getElementById('am_wl').checked=m.includes('Weightlifting');
  document.getElementById('am_hy').checked=m.includes('Hyrox');
  document.getElementById('aulaNotas').value='';
  document.getElementById('aulaOverlay').classList.remove('hidden');
}
async function confirmAula(){
  if(!currentLead)return;
  const newExp=Math.min((currentLead.experiencia_num||0)+1,3);
  const mods=[...document.querySelectorAll('#aulaOverlay .chk-inp:checked')].map(c=>c.value);
  const nota=document.getElementById('aulaNotas').value.trim();
  const notas=nota?(currentLead.notas?currentLead.notas+`\n\n[${newExp}ª Exp] `+nota:`[${newExp}ª Exp] `+nota):currentLead.notas;
  try{
    await sb(`${T}?id=eq.${currentLead.id}`,{method:'PATCH',prefer:'return=representation',body:JSON.stringify({experiencia_num:newExp,modalidades:mods.length?mods:currentLead.modalidades||[],fase:'aula',notas:notas||currentLead.notas,updated_at:new Date().toISOString()})});
    document.getElementById('aulaOverlay').classList.add('hidden');
    await loadAll();const u=leads.find(l=>l.id===currentLead.id);
    if(u){currentLead=u;openDetail(currentLead.id);}
    if(newExp===3)showToast('3ª Experiência! Considera marcar como Convertido 🏆');
    else showToast(`${newExp}ª Experiência registada ✓`);
  }catch(e){showToast('Erro: '+e.message,true);}
}

// ── FOLLOW-UP MODAL ───────────────────────────────────────────────────────────
function openFUModal(){
  if(!currentLead)return;
  document.getElementById('fu_leadname').textContent=currentLead.nome;
  document.getElementById('fu_data').value=new Date().toISOString().slice(0,10);
  document.getElementById('fu_canal').value='whatsapp';
  document.getElementById('fu_feedback').value='respondeu';
  document.getElementById('fu_obs').value='';
  document.getElementById('fi_nao').checked=true;
  // Style radio labels
  styleRadios();
  document.getElementById('fuOverlay').classList.remove('hidden');
}
function styleRadios(){
  document.querySelectorAll('input[name="fu_inscrito"]').forEach(r=>{
    const lbl=document.getElementById(r.id+'_lbl');
    if(lbl)lbl.style.borderColor=r.checked?'var(--gold)':'#333',lbl.style.color=r.checked?'var(--gold)':'var(--muted)';
  });
}
document.querySelectorAll('input[name="fu_inscrito"]').forEach(r=>r.addEventListener('change',styleRadios));
async function saveFU(){
  if(!currentLead)return;
  const inscrito=document.querySelector('input[name="fu_inscrito"]:checked')?.value||'nao';
  const data={lead_id:currentLead.id,data_contacto:document.getElementById('fu_data').value,
    canal:document.getElementById('fu_canal').value,feedback:document.getElementById('fu_feedback').value,
    inscrito,observacoes:document.getElementById('fu_obs').value.trim()||null,created_at:new Date().toISOString()};
  try{
    await sb(TFU,{method:'POST',prefer:'return=representation',body:JSON.stringify(data)});
    // If inscrito, update lead fase
    if(inscrito==='sim')await sb(`${T}?id=eq.${currentLead.id}`,{method:'PATCH',prefer:'return=representation',body:JSON.stringify({fase:'convertido',updated_at:new Date().toISOString()})});
    document.getElementById('fuOverlay').classList.add('hidden');
    showToast('Contacto registado ✓');await loadAll();
    const u=leads.find(l=>l.id===currentLead.id);if(u){currentLead=u;openDetail(currentLead.id);}
  }catch(e){showToast('Erro: '+e.message,true);}
}
function renderFollowUp(){
  const q=(document.getElementById('fuSearch')?.value||'').trim().toLowerCase();
  const flt=document.getElementById('fuFilter')?.value||'';
  const fuEl=document.getElementById('fuList');
  // Group followups by lead
  const grouped={};
  followups.forEach(f=>{if(!grouped[f.lead_id])grouped[f.lead_id]=[];grouped[f.lead_id].push(f);});
  const icons={instagram:'📸',email:'✉',site:'🌐',telefone:'📞',whatsapp:'💬',presencial:'🤝'};
  const flbls={respondeu:'Respondeu',nao_respondeu:'Não respondeu',mais_tarde:'Mais tarde',sem_interesse:'Sem interesse',agendou:'Agendou aula'};
  const fcls={respondeu:'tag-resp',nao_respondeu:'tag-noresp',mais_tarde:'tag-later',sem_interesse:'tag-noresp',agendou:'tag-resp'};

  let items=leads.filter(l=>{
    const lfu=grouped[l.id]||[];
    if(flt==='respondeu'&&!lfu.some(f=>f.feedback==='respondeu'))return false;
    if(flt==='nao_respondeu'&&!lfu.some(f=>f.feedback==='nao_respondeu'))return false;
    if(flt==='mais_tarde'&&!lfu.some(f=>f.feedback==='mais_tarde'))return false;
    if(flt==='inscrito'&&!lfu.some(f=>f.inscrito==='sim'))return false;
    if(q&&!(l.nome||'').toLowerCase().includes(q))return false;
    return true;
  });

  if(items.length===0){fuEl.innerHTML=`<div style="text-align:center;padding:40px;color:var(--muted)">Nenhum resultado</div>`;return;}

  fuEl.innerHTML=items.map(l=>{
    const lfu=(grouped[l.id]||[]).sort((a,b)=>new Date(b.data_contacto)-new Date(a.data_contacto));
    const lastFU=lfu[0];
    return`<div class="fu-item" style="cursor:pointer" onclick="openDetail('${l.id}')">
      <div class="fu-item-hdr">
        <div>
          <div style="font-weight:600;font-size:14px">${l.nome}</div>
          <div style="font-size:12px;color:var(--muted);margin-top:2px">${l.telefone||'—'} · ${l.fase}</div>
        </div>
        <div style="display:flex;gap:6px;flex-direction:column;align-items:flex-end">
          ${lastFU?`<span class="tag ${fcls[lastFU.feedback]||''}">${flbls[lastFU.feedback]||lastFU.feedback}</span>`:`<span class="tag tag-cold">Sem contacto</span>`}
          ${lfu.some(f=>f.inscrito==='sim')?`<span class="tag tag-inscrito">⭐ Membro</span>`:''}
        </div>
      </div>
      ${lfu.length>0?`<div class="fu-tags" style="margin-top:6px">
        <span style="font-size:11px;color:var(--muted)">${lfu.length} contacto${lfu.length>1?'s':''} · Último: ${lastFU.data_contacto?new Date(lastFU.data_contacto).toLocaleDateString('pt-PT',{day:'numeric',month:'short'}):'—'} via ${icons[lastFU.canal]||''} ${lastFU.canal||''}</span>
      </div>`:`<div style="font-size:12px;color:var(--muted2);margin-top:4px">Sem contactos registados</div>`}
    </div>`;
  }).join('');
}

// ── AI ────────────────────────────────────────────────────────────────────────
async function runAI(){
  if(!currentLead)return;
  const btn=document.getElementById('aiBtn'),aip=document.getElementById('aiPanel');
  btn.disabled=true;btn.textContent='...';
  aip.style.display='flex';
  aip.innerHTML=`<div class="ai-hdr">✦ A analisar...</div><div class="dots"><span></span><span></span><span></span></div>`;
  const l=currentLead,mods=(l.modalidades||[]).join(', ')||'não especificada';
  const lfu=followups.filter(f=>f.lead_id===l.id);
  const fuContext=lfu.length?`Histórico: ${lfu.map(f=>`${f.data_contacto} via ${f.canal} — ${f.feedback}`).join('; ')}`:'Sem contactos anteriores';
  const prompt=`És especialista em vendas de ginásios CrossFit em Portugal. Analisa este lead para o 5.7CrossFit, Guimarães. Responde APENAS em JSON válido.
Lead: Nome: ${l.nome}, Objetivo: ${l.objetivo||'?'}, Modalidade: ${mods}, Experiências: ${l.experiencia_num||0}/3, Canal origem: ${l.canal||'?'}, ${fuContext}, Fase: ${l.fase}
JSON: {"temperatura":"quente|morno|frio","justificacao":"1-2 frases","mensagem_whatsapp":"mensagem PT de Portugal, informal, personalizada com nome/objetivo/modalidade, convidar para próxima experiência no 5.7CF, máx 3 parágrafos"}`;
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:prompt}]})});
    const data=await res.json();
    const parsed=JSON.parse(data.content.map(c=>c.text||'').join('').replace(/```json|```/g,'').trim());
    await sb(`${T}?id=eq.${l.id}`,{method:'PATCH',prefer:'return=representation',body:JSON.stringify({ai_temp:parsed.temperatura,ai_justificacao:parsed.justificacao,ai_mensagem:parsed.mensagem_whatsapp,updated_at:new Date().toISOString()})});
    l.ai_temp=parsed.temperatura;l.ai_justificacao=parsed.justificacao;l.ai_mensagem=parsed.mensagem_whatsapp;
    currentLead=l;renderAIPanel(l);btn.disabled=false;btn.textContent='✦ Re-analisar';await loadAll();
  }catch(e){aip.innerHTML=`<div style="color:var(--red);font-size:13px">Erro: ${e.message}</div>`;btn.disabled=false;btn.textContent='✦ Tentar novamente';}
}
function renderAIPanel(l){
  const aip=document.getElementById('aiPanel');
  const tl=l.ai_temp==='quente'?'🔥 Quente':l.ai_temp==='morno'?'~ Morno':'❄ Frio';
  const tc=l.ai_temp==='quente'?'tag-hot':l.ai_temp==='morno'?'tag-warm':'tag-cold';
  aip.style.cssText='display:flex;flex-direction:column;gap:12px';
  aip.innerHTML=`<div class="ai-hdr">✦ Análise IA</div>
    <div><div class="sec-lbl">Classificação</div><div style="display:flex;align-items:center;gap:8px;margin-top:4px"><span class="tag ${tc}">${tl}</span><span style="font-size:13px;color:#aaa">${l.ai_justificacao||''}</span></div></div>
    <div><div class="sec-lbl">Mensagem WhatsApp sugerida</div><div class="ai-msg" style="margin-top:4px">${(l.ai_mensagem||'').replace(/\n/g,'<br>')}<button class="copy-btn" onclick="copyMsg()">Copiar</button></div></div>`;
}
function copyMsg(){if(!currentLead?.ai_mensagem)return;navigator.clipboard.writeText(currentLead.ai_mensagem).then(()=>showToast('Copiado ✓'));}

// ── RELATÓRIOS ────────────────────────────────────────────────────────────────
function getWeekRange(off=0){
  const now=new Date(),day=now.getDay();
  const mon=new Date(now);mon.setDate(now.getDate()+(day===0?-6:1-day)+(off*7));mon.setHours(0,0,0,0);
  const sun=new Date(mon);sun.setDate(mon.getDate()+6);sun.setHours(23,59,59,999);
  return{mon,sun};
}
function fd(d){return d.toLocaleDateString('pt-PT',{day:'numeric',month:'short'});}
function renderReports(){
  const{mon,sun}=getWeekRange(weekOff);
  const yr=new Date().getFullYear();
  const months=['Jan','Fev','Mar','Abr','Mai','Jun','Jul','Ago','Set','Out','Nov','Dez'];
  // Week leads
  const wl=leads.filter(l=>{const d=new Date(l.created_at);return d>=mon&&d<=sun;});
  const wc=leads.filter(l=>l.fase==='convertido'&&new Date(l.updated_at||l.created_at)>=mon&&new Date(l.updated_at||l.created_at)<=sun);
  // Week exp (aulas registadas nesta semana — usando updated_at como proxy)
  const wexp=leads.filter(l=>(l.experiencia_num||0)>0&&new Date(l.updated_at||l.created_at)>=mon&&new Date(l.updated_at||l.created_at)<=sun);
  // Modal week
  const mw={CrossFit:0,Calistenia:0,Weightlifting:0,Hyrox:0};
  wl.forEach(l=>(l.modalidades||[]).forEach(m=>{if(mw[m]!==undefined)mw[m]++;}));
  const maxMW=Math.max(...Object.values(mw),1);
  // Modal all-time
  const ma={CrossFit:0,Calistenia:0,Weightlifting:0,Hyrox:0};
  leads.forEach(l=>(l.modalidades||[]).forEach(m=>{if(ma[m]!==undefined)ma[m]++;}));
  const sma=Object.entries(ma).sort((a,b)=>b[1]-a[1]);
  const maxMA=Math.max(...Object.values(ma),1);
  // Monthly leads
  const mc=months.map((_,i)=>leads.filter(l=>{const d=new Date(l.created_at);return d.getFullYear()===yr&&d.getMonth()===i;}).length);
  const maxMC=Math.max(...mc,1);
  // Monthly exp
  const me=months.map((_,i)=>leads.filter(l=>{
    const d=new Date(l.updated_at||l.created_at);
    return(l.experiencia_num||0)>0&&d.getFullYear()===yr&&d.getMonth()===i;
  }).length);
  const maxME=Math.max(...me,1);
  // Objetivo breakdown
  const objs={'Perder peso':0,'Ganhar músculo':0,'Melhorar condição física':0,'Competição / performance':0,'Bem-estar geral':0,'Reabilitação':0};
  leads.forEach(l=>{if(l.objetivo&&objs[l.objetivo]!==undefined)objs[l.objetivo]++;});
  const sobjMax=Math.max(...Object.values(objs),1);
  // Follow-up stats
  const fuResp=followups.filter(f=>f.feedback==='respondeu').length;
  const fuNR=followups.filter(f=>f.feedback==='nao_respondeu').length;
  const fuInsc=followups.filter(f=>f.inscrito==='sim').length;
  const fuCanais={instagram:0,email:0,site:0,telefone:0,whatsapp:0,presencial:0};
  followups.forEach(f=>{if(f.canal&&fuCanais[f.canal]!==undefined)fuCanais[f.canal]++;});

  document.getElementById('repContent').innerHTML=`
    <!-- Week header -->
    <div style="display:flex;align-items:center;justify-content:space-between">
      <div>
        <div style="font-family:'Bebas Neue',sans-serif;font-size:24px;letter-spacing:1px">RELATÓRIO SEMANAL</div>
        <div style="font-size:13px;color:var(--muted);margin-top:2px">${fd(mon)} — ${fd(sun)}</div>
      </div>
      <div class="week-nav">
        <button class="wnbtn" onclick="weekOff--;renderReports()">← Anterior</button>
        <span class="wlbl">${weekOff===0?'Esta semana':weekOff===-1?'Semana passada':`${Math.abs(weekOff)} semanas atrás`}</span>
        <button class="wnbtn" onclick="weekOff++;renderReports()" ${weekOff>=0?'disabled style="opacity:.4"':''}>→ Seguinte</button>
      </div>
    </div>
    <div class="week-stats">
      <div class="ws"><div class="ws-v">${wl.length}</div><div class="ws-l">Novos leads</div></div>
      <div class="ws"><div class="ws-v" style="color:var(--green)">${wc.length}</div><div class="ws-l">Convertidos</div></div>
      <div class="ws"><div class="ws-v">${wl.length?Math.round(wc.length/wl.length*100):0}%</div><div class="ws-l">Taxa conversão</div></div>
      <div class="ws"><div class="ws-v" style="color:var(--blue)">${wexp.length}</div><div class="ws-l">Aulas registadas</div></div>
      <div class="ws"><div class="ws-v" style="color:var(--purple)">${followups.filter(f=>{const d=new Date(f.data_contacto||f.created_at);return d>=mon&&d<=sun;}).length}</div><div class="ws-l">Contactos feitos</div></div>
    </div>

    <div class="rep-grid">
      <!-- Modal semana -->
      <div class="rep-card">
        <div class="rep-title">MODALIDADES — SEMANA</div>
        ${Object.entries(mw).map(([m,n])=>`<div class="rank-item"><div class="rank-lbl">${m}</div><div class="rank-bg"><div class="rank-fill" style="width:${Math.round(n/maxMW*100)}%;background:var(--gold)"></div></div><div class="rank-v">${n}</div></div>`).join('')}
      </div>
      <!-- Objetivo breakdown -->
      <div class="rep-card">
        <div class="rep-title">OBJETIVOS</div>
        ${Object.entries(objs).map(([o,n])=>`<div class="rank-item"><div class="rank-lbl" style="font-size:12px">${o}</div><div class="rank-bg"><div class="rank-fill" style="width:${Math.round(n/sobjMax*100)}%;background:var(--blue)"></div></div><div class="rank-v">${n}</div></div>`).join('')}
      </div>
      <!-- Modal all-time -->
      <div class="rep-card">
        <div class="rep-title">MODALIDADES — TOTAL</div>
        ${sma.map(([m,n],i)=>`<div class="rank-item"><div class="rank-lbl" style="${i===0?'color:var(--gold)':''}">${i===0?'🥇 ':''}${m}</div><div class="rank-bg"><div class="rank-fill" style="width:${Math.round(n/maxMA*100)}%;background:${i===0?'var(--gold)':'var(--muted2)'}"></div></div><div class="rank-v">${n}</div></div>`).join('')}
      </div>
      <!-- Follow-up stats -->
      <div class="rep-card">
        <div class="rep-title">FOLLOW-UPS</div>
        <div class="rank-item"><div class="rank-lbl">Responderam</div><div class="rank-bg"><div class="rank-fill" style="width:${followups.length?Math.round(fuResp/followups.length*100):0}%;background:var(--green)"></div></div><div class="rank-v">${fuResp}</div></div>
        <div class="rank-item"><div class="rank-lbl">Não responderam</div><div class="rank-bg"><div class="rank-fill" style="width:${followups.length?Math.round(fuNR/followups.length*100):0}%;background:var(--red)"></div></div><div class="rank-v">${fuNR}</div></div>
        <div class="rank-item"><div class="rank-lbl">⭐ Passaram a membro</div><div class="rank-bg"><div class="rank-fill" style="width:${followups.length?Math.round(fuInsc/followups.length*100):0}%;background:var(--gold)"></div></div><div class="rank-v">${fuInsc}</div></div>
      </div>
    </div>

    <!-- Annual leads -->
    <div class="rep-card rep-full">
      <div class="rep-title">NOVOS LEADS ${yr} — POR MÊS <span style="font-family:Inter;font-size:13px;font-weight:400;letter-spacing:0;color:var(--muted)">Total: <strong style="color:var(--gold)">${mc.reduce((a,b)=>a+b,0)}</strong></span></div>
      <div class="bar-chart">${mc.map((n,i)=>`<div class="bar-col"><div class="bar-v">${n||''}</div><div class="bar" style="height:${Math.round(n/maxMC*100)}%;background:${i===new Date().getMonth()?'var(--gold)':'var(--muted2)'}"></div><div class="bar-l">${months[i]}</div></div>`).join('')}</div>
    </div>

    <!-- Annual exp -->
    <div class="rep-card rep-full">
      <div class="rep-title">EXPERIÊNCIAS REALIZADAS ${yr} — POR MÊS <span style="font-family:Inter;font-size:13px;font-weight:400;letter-spacing:0;color:var(--muted)">Total: <strong style="color:var(--blue)">${me.reduce((a,b)=>a+b,0)}</strong></span></div>
      <div class="bar-chart">${me.map((n,i)=>`<div class="bar-col"><div class="bar-v">${n||''}</div><div class="bar" style="height:${Math.round(n/maxME*100)}%;background:${i===new Date().getMonth()?'var(--blue)':'#2a3a5a'}"></div><div class="bar-l">${months[i]}</div></div>`).join('')}</div>
    </div>`;
}

// ── UTILS ─────────────────────────────────────────────────────────────────────
function openWA(e,tel){e.stopPropagation();const c=tel.replace(/\D/g,'');window.open(`https://wa.me/${c.startsWith('351')?c:'351'+c}`,'_blank');}
function exportPDF(){const isR=document.getElementById('view-relatorios').classList.contains('active');if(!isR){switchView('relatorios');setTimeout(()=>window.print(),400);}else window.print();}
function showToast(msg,err=false){const t=document.getElementById('toast');t.textContent=msg;t.style.borderColor=err?'var(--red)':'var(--gold)';t.classList.add('show');setTimeout(()=>t.classList.remove('show'),2800);}
['addOverlay','detailOverlay','aulaOverlay','fuOverlay'].forEach(id=>{document.getElementById(id).addEventListener('click',e=>{if(e.target===e.currentTarget)document.getElementById(id).classList.add('hidden');});});

loadAll();
</script>
</body>
</html>
