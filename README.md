<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sopaan · Inverse Functions</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=IBM+Plex+Mono:wght@500;600&display=swap">
<style>
  html,body{margin:0;} img{max-width:100%;} [hidden]{display:none !important;}
  :root{
    --navy:#16264A; --navy-2:#1F3B6B; --gold:#C79A3E; --gold-soft:#F3E7C9;
    --paper:#FBF9F4; --paper-2:#F1EAD8; --card:#FFFFFF;
    --ink:#211E1A; --ink-soft:#655D4C; --rule:#E4DCC8;
    --success:#2E8B57; --success-soft:#E1F2E7;
    --danger:#BF4B45; --danger-soft:#FAE3E1;
    --locked:#C7BEA9;
    --focus:#1F3B6B;
    --accent-text:#1F3B6B; --retry-text:#8A661F;
    color-scheme:light;
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
      --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
      --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
      --success:#7BC79A; --success-soft:#1B2E22;
      --danger:#E38884; --danger-soft:#331D1B;
      --locked:#4A4436;
      --focus:#E0B75B;
      --accent-text:#E0B75B; --retry-text:#E0B75B;
      color-scheme:dark;
    }
  }
  :root[data-theme="dark"]{
    --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
    --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
    --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
    --success:#7BC79A; --success-soft:#1B2E22;
    --danger:#E38884; --danger-soft:#331D1B;
    --locked:#4A4436;
    --focus:#E0B75B;
    --accent-text:#E0B75B; --retry-text:#E0B75B;
    color-scheme:dark;
  }

  *{box-sizing:border-box;}
  body{background:var(--paper); color:var(--ink); font-family:'Source Sans 3',-apple-system,'Segoe UI',sans-serif; padding-inline:0; padding-block:0;}
  h1,h2,h3{font-family:'Fraunces',Georgia,serif; text-wrap:balance; margin:0;}
  .num{font-family:'IBM Plex Mono',ui-monospace,monospace; font-variant-numeric:tabular-nums;}

  header.brand{
    background:linear-gradient(155deg,var(--navy) 0%, var(--navy-2) 100%);
    color:#F4EFDF; padding-block:calc(20px + env(safe-area-inset-top,0px)) 18px; padding-inline:20px;
  }
  .brand-row{display:flex; align-items:center; gap:12px; max-width:900px; margin:0 auto;}
  .crest{
    width:42px; height:42px; border-radius:10px; background:var(--gold); color:var(--navy);
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-weight:700; font-size:18px; flex-shrink:0;
  }
  .brand-name{font-size:12px; letter-spacing:.08em; text-transform:uppercase; color:var(--gold); font-weight:700;}
  .series-name{font-size:19px; font-weight:700; font-family:'Fraunces',serif;}
  .chapter-eyebrow{max-width:900px; margin:14px auto 0; font-size:12px; letter-spacing:.06em; text-transform:uppercase; color:#AEB9D6;}
  .chapter-title{font-size:28px; max-width:900px; margin:2px auto 0;}
  .chapter-sub{font-size:14.5px; color:var(--gold); font-weight:700; max-width:900px; margin:3px auto 0;}

  .chapter-progress{max-width:900px; margin:14px auto 0; display:flex; align-items:center; gap:10px;}
  .cp-track{flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,.18); overflow:hidden;}
  .cp-fill{height:100%; background:var(--gold); border-radius:99px; transition:width .3s ease;}
  .cp-label{font-size:11.5px; color:#CFD7EA; white-space:nowrap;}

  .tabbar{position:sticky; top:env(safe-area-inset-top,0px); z-index:15; background:var(--paper); border-bottom:1px solid var(--rule); overflow-x:auto; white-space:nowrap;}
  .tabbar-inner{max-width:900px; margin:0 auto; display:flex; padding-inline:16px;}
  .tab-btn{font-family:inherit; font-size:14px; font-weight:600; color:var(--ink-soft); background:none; border:none; padding:13px 16px; cursor:pointer; position:relative; flex-shrink:0;}
  .tab-btn.active{color:var(--accent-text);}
  .tab-btn.active::after{content:''; position:absolute; left:12px; right:12px; bottom:0; height:3px; background:var(--gold); border-radius:3px 3px 0 0;}
  .tab-count{font-size:11px; color:var(--ink-soft); margin-left:5px;}

  .slide-progress{max-width:900px; margin:0 auto; padding:10px 16px 0; display:flex; align-items:center; gap:10px;}
  .sp-track{flex:1; height:5px; border-radius:99px; background:var(--rule); overflow:hidden;}
  .sp-fill{height:100%; background:var(--accent-text); border-radius:99px; transition:width .3s ease;}
  .sp-label{font-size:12px; color:var(--ink-soft); white-space:nowrap; font-weight:600;}

  .wrap{max-width:900px; margin:0 auto; padding:16px 16px calc(110px + env(safe-area-inset-bottom,0px));}

  .qcard{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px;}
  .qhead{display:flex; align-items:flex-start; gap:10px; margin-bottom:10px;}
  .qnum{width:32px; height:32px; border-radius:8px; background:var(--gold-soft); color:var(--accent-text); display:flex; align-items:center; justify-content:center; font-weight:700; font-family:'Fraunces',serif; flex-shrink:0; font-size:14px;}
  .qtext{font-size:16px; line-height:1.55; flex:1;}
  .qtag{font-size:10.5px; color:var(--gold); background:var(--gold-soft); padding:2px 7px; border-radius:99px; font-weight:700; margin-left:6px; white-space:nowrap;}
  .marks-pill{font-size:11px; font-weight:700; color:var(--ink-soft); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; margin-left:auto; flex-shrink:0; white-space:nowrap;}
  .step-badge{font-size:11px; font-weight:700; color:var(--accent-text); background:var(--paper-2); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; display:inline-block; margin-bottom:12px;}

  .options{display:flex; flex-direction:column; gap:8px; margin-top:10px;}
  .opt{display:flex; align-items:center; gap:10px; padding:11px 12px; border:1.5px solid var(--rule); border-radius:10px; cursor:pointer; font-size:15px; background:var(--paper);}
  .opt input{accent-color:var(--navy-2);}
  .opt.is-correct{border-color:var(--success); background:var(--success-soft);}
  .opt.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .opt.locked{cursor:not-allowed;}

  .subpart-label{font-weight:700; font-size:12.5px; color:var(--accent-text); text-transform:uppercase; letter-spacing:.03em; margin:14px 0 6px;}
  .or-divider{text-align:center; font-size:11px; font-weight:700; letter-spacing:.08em; color:var(--ink-soft); margin:8px 0;}

  .steps{display:flex; flex-direction:column; gap:10px;}
  .step-line{font-size:14.5px; line-height:1.9; background:var(--paper); border:1px dashed var(--rule); border-radius:10px; padding:9px 12px;}
  .step-line.resolved{opacity:.9;}
  .blank-input{font-family:'IBM Plex Mono',monospace; font-size:14px; border:1.5px solid var(--rule); border-radius:6px; padding:3px 8px; width:120px; background:var(--card); color:var(--ink); margin:0 2px;}
  .blank-input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .blank-input.is-correct{border-color:var(--success); background:var(--success-soft);}
  .blank-input.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .blank-input[disabled]{opacity:.85;}
  .reveal-note{font-size:12px; color:var(--danger); padding-left:2px; margin-top:-2px;}

  .feedback{font-size:13.5px; padding:10px 12px; border-radius:9px; margin-top:14px; display:none;}
  .feedback.show{display:block;}
  .feedback.ok{background:var(--success-soft); color:var(--success);}
  .feedback.retry{background:var(--gold-soft); color:var(--retry-text);}
  .feedback.reveal{background:var(--danger-soft); color:var(--danger);}
  .feedback.err{background:var(--danger-soft); color:var(--danger);}
  .attempts-dots{display:inline-flex; gap:4px; margin-left:2px;}
  .attempts-dots span{width:6px; height:6px; border-radius:50%; background:var(--ink-soft); opacity:.3; display:inline-block;}
  .attempts-dots span.used{opacity:1; background:var(--danger);}

  .ar-box{background:var(--paper-2); border-radius:10px; padding:10px 12px; margin-bottom:12px; font-size:13px; color:var(--ink-soft);}

  .navbar{
    position:fixed; left:0; right:0; bottom:0; z-index:30; background:var(--paper);
    border-top:1px solid var(--rule); padding:10px 16px calc(10px + env(safe-area-inset-bottom,0px));
  }
  .navbar-inner{max-width:900px; margin:0 auto; display:flex; gap:8px; flex-wrap:wrap; align-items:center;}
  .btn{font-family:inherit; font-size:13.5px; font-weight:700; padding:10px 14px; border-radius:9px; border:1.5px solid var(--rule); background:var(--card); color:var(--ink); cursor:pointer;}
  .btn:hover{border-color:var(--navy-2);}
  .btn:disabled{opacity:.4; cursor:not-allowed;}
  .btn-primary{background:var(--navy-2); color:#fff; border-color:var(--navy-2);}
  .navbar .spacer{flex:1;}

  .fab{position:fixed; right:16px; bottom:calc(74px + env(safe-area-inset-bottom,0px)); background:var(--gold); color:var(--navy); border:none; border-radius:999px; padding:11px 16px; font-family:inherit; font-weight:700; font-size:13px; display:flex; align-items:center; gap:7px; cursor:pointer; box-shadow:0 6px 16px rgba(0,0,0,.18); z-index:35;}
  .fab-badge{background:rgba(255,255,255,.55); border-radius:99px; padding:1px 7px; font-size:11px;}

  .overlay{position:fixed; inset:0; background:rgba(20,18,14,.45); z-index:50; display:none; align-items:flex-end; justify-content:center;}
  .overlay.show{display:flex;}
  .palette{background:var(--card); width:min(480px,100%); max-height:78vh; overflow-y:auto; border-radius:18px 18px 0 0; padding:18px 18px calc(18px + env(safe-area-inset-bottom,0px)); border:1px solid var(--rule); border-bottom:none;}
  @media (min-width:640px){ .overlay{align-items:center;} .palette{border-radius:18px; border-bottom:1px solid var(--rule); max-height:74vh;} }
  .palette-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:6px;}
  .palette-head h2{font-size:16px;}
  .palette-close{background:none; border:none; font-size:20px; color:var(--ink-soft); cursor:pointer; padding:4px;}
  .palette-legend{display:flex; gap:12px; flex-wrap:wrap; font-size:11px; color:var(--ink-soft); margin:10px 0 14px;}
  .palette-legend span{display:inline-flex; align-items:center; gap:5px;}
  .dot{width:9px; height:9px; border-radius:50%; display:inline-block;}
  .dot.correct{background:var(--success);} .dot.revealed{background:var(--danger);}
  .dot.skipped{background:var(--gold);} .dot.locked{background:var(--locked);}
  .dot.current{background:var(--navy-2);}
  .chip-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(48px,1fr)); gap:8px;}
  .chip{border:1.5px solid var(--rule); border-radius:9px; padding:8px 4px; text-align:center; font-family:'IBM Plex Mono',monospace; font-size:12.5px; font-weight:600; cursor:pointer; background:var(--paper); color:var(--ink);}
  .chip[data-status="correct"]{border-color:var(--success); background:var(--success-soft); color:var(--success);}
  .chip[data-status="revealed"]{border-color:var(--danger); background:var(--danger-soft); color:var(--danger);}
  .chip[data-status="skipped"]{border-color:var(--gold); background:var(--gold-soft); color:var(--retry-text);}
  .chip[data-status="locked"]{border-color:var(--rule); color:var(--locked); cursor:not-allowed; background:var(--paper-2);}
  .chip[data-status="current"]{outline:2px solid var(--navy-2); outline-offset:1px;}

  .toast{position:fixed; left:50%; bottom:calc(140px + env(safe-area-inset-bottom,0px)); transform:translateX(-50%); background:var(--ink); color:var(--paper); padding:9px 16px; border-radius:99px; font-size:13px; opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:60;}
  .toast.show{opacity:1;}

  .done-card{text-align:center; padding:36px 20px;}
  .done-card .big{font-size:38px; margin-bottom:6px;}
  .score-pills{display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin:16px 0;}
  .score-pill{padding:8px 16px; border-radius:99px; font-size:13px; font-weight:700;}

  footer.brandfoot{max-width:900px; margin:14px auto 0; padding:0 16px calc(110px + env(safe-area-inset-bottom,0px)); text-align:center; font-size:12px; color:var(--ink-soft);}

  .mode-pill{font-family:inherit; font-size:12.5px; font-weight:700; color:var(--navy); background:var(--gold); border:none; border-radius:99px; padding:6px 14px; cursor:pointer; margin-top:12px; display:inline-flex; align-items:center; gap:6px;}
  .mode-pick{display:flex; flex-direction:column; gap:14px; padding:8px 0 24px;}
  .mode-card{background:var(--card); border:1.5px solid var(--rule); border-radius:16px; padding:22px; cursor:pointer; text-align:left;}
  .mode-card:hover{border-color:var(--navy-2);}
  .mode-card .mode-icon{font-size:26px; margin-bottom:8px;}
  .mode-card h3{font-size:18px; margin-bottom:6px;}
  .mode-card p{font-size:13.5px; color:var(--ink-soft); line-height:1.5; margin:0;}
  .quiz-hint{font-size:12.5px; color:var(--ink-soft); background:var(--paper-2); border-radius:9px; padding:8px 12px; margin-bottom:14px;}
  .review-row{border:1px solid var(--rule); border-radius:10px; padding:11px 13px; margin-bottom:10px;}
  .review-tag{font-size:11.5px; font-weight:700; margin-bottom:4px; display:block;}
  .review-tag.ok{color:var(--success);} .review-tag.bad{color:var(--danger);} .review-tag.na{color:var(--ink-soft);}
  .review-q{font-size:13.5px; margin-bottom:6px; color:var(--ink-soft);}
  .review-ans{font-size:13px; margin-bottom:2px;}

  .who-row{max-width:900px; margin:12px auto 0; display:flex; flex-wrap:wrap; gap:8px; align-items:center;}
  .who-row .mode-pill{margin-top:0;}
  .who{display:inline-flex; flex-wrap:wrap; align-items:center; gap:6px; font-size:12.5px; color:#CFD7EA;}
  .who b{color:#F4EFDF;}
  .who button{font-family:inherit; font-size:12px; font-weight:700; color:#F4EFDF; background:rgba(255,255,255,.12); border:1px solid rgba(255,255,255,.22); border-radius:99px; padding:5px 11px; cursor:pointer;}
  .who button:hover{background:rgba(255,255,255,.2);}
  .login-card{max-width:460px; margin:8px auto 0; background:var(--card); border:1px solid var(--rule); border-radius:16px; padding:22px;}
  .login-card h2{font-size:21px; margin-bottom:4px;}
  .login-card p.lead{font-size:13.5px; color:var(--ink-soft); margin:0 0 16px; line-height:1.5;}
  .fld{display:flex; flex-direction:column; gap:5px; margin-bottom:12px;}
  .fld label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .fld input{font-family:inherit; font-size:15px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:9px; background:var(--paper); color:var(--ink);}
  .fld input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .fld-row{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
  .login-err{font-size:13px; color:var(--danger); background:var(--danger-soft); border-radius:8px; padding:8px 10px; margin-bottom:12px;}
  .login-note{font-size:12px; color:var(--ink-soft); margin-top:12px; line-height:1.5;}
  .known{margin:0 0 16px; display:flex; flex-direction:column; gap:6px;}
  .known-label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .known-btn{display:flex; justify-content:space-between; align-items:center; gap:10px; text-align:left; font-family:inherit; font-size:14.5px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:10px; background:var(--paper); color:var(--ink); cursor:pointer;}
  .known-btn:hover{border-color:var(--navy-2);}
  .known-btn small{font-size:12px; color:var(--ink-soft);}
  .rec-card{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px; margin-bottom:14px;}
  .rec-card h2{font-size:19px; margin-bottom:10px;}
  .rec-card h3{font-size:15px; margin:4px 0 8px;}
  .rec-table-wrap{overflow-x:auto;}
  .rec-table{width:100%; border-collapse:collapse; font-size:13.5px; font-variant-numeric:tabular-nums;}
  .rec-table th{text-align:left; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--ink-soft); padding:6px 8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-table td{padding:8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-bar{display:inline-block; width:70px; height:6px; border-radius:99px; background:var(--rule); overflow:hidden; vertical-align:middle; margin-right:6px;}
  .rec-bar i{display:block; height:100%; background:var(--success);}
  .rec-empty{font-size:13.5px; color:var(--ink-soft);}
  .sec-sub{max-width:900px; margin:0 auto; padding:10px 16px 0; font-size:12.5px; font-weight:700; color:var(--accent-text); letter-spacing:.02em;}
  .opt{flex-wrap:wrap;}
  .opt-l{font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--ink-soft);}
  .opt-t{flex:1; min-width:0;}
  .opt.is-chosen:not(.is-correct):not(.is-wrong){border-color:var(--navy-2); background:var(--gold-soft);}
  .opt-tag{font-size:11px; font-weight:700; padding:2px 8px; border-radius:99px; background:var(--card); border:1px solid currentColor; white-space:nowrap;}
  .opt.is-correct .opt-tag{color:var(--success);} .opt.is-wrong .opt-tag{color:var(--danger);} .opt.is-chosen:not(.is-correct):not(.is-wrong) .opt-tag{color:var(--accent-text);}
  .chosen{font-size:13.5px; margin-top:10px; padding:8px 12px; border-radius:9px;}
  .chosen.ok{background:var(--success-soft); color:var(--success);} .chosen.bad{background:var(--danger-soft); color:var(--danger);}
  .chosen + .chosen{margin-top:6px;}
  .solution{margin-top:14px; border:1px solid var(--rule); border-left:4px solid var(--gold); background:var(--paper-2); border-radius:10px; padding:12px 14px;}
  .sol-h{font-family:'Fraunces',Georgia,serif; font-weight:700; font-size:14px; color:var(--accent-text); margin-bottom:6px;}
  .sol-line{font-size:14.5px; line-height:1.7;}
  .rev-sol summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--accent-text); margin-top:6px;}
  .rev-sol .solution{margin-top:8px;}
  .chapter-credit{max-width:900px; margin:4px auto 0; font-size:12px; color:#CFD7EA;}
  footer.brandfoot a{color:inherit;}
  .blank-input.wide{width:260px; max-width:100%; font-family:'Source Sans 3',sans-serif;}
  .blank-input.expr{width:170px; max-width:100%;}
  /*fix-layout*/ .cp-fill,.sp-fill{width:0;} .fld{min-width:0;} .fld input{width:100%; min-width:0; box-sizing:border-box;}
  .fig{margin:6px 0 10px; display:flex; justify-content:center;}
  .figsvg{width:100%; max-width:340px; height:auto; overflow:visible;}
  .figsvg .ln,.figsvg .arm{stroke:var(--ink); stroke-width:1.6; fill:none;}
  .figsvg .arm{stroke:var(--accent-text); stroke-width:2;}
  .figsvg .pt{fill:var(--ink);}
  .figsvg .lb{fill:var(--ink); font:600 13px 'Source Sans 3',sans-serif;}
  .figsvg .al{fill:var(--accent-text); font:700 12px 'Source Sans 3',sans-serif;}
  .figsvg .wg{fill:var(--gold-soft); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .wg2{fill:rgba(199,154,62,.35); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .ra{fill:none; stroke:var(--ink); stroke-width:1.2;}
  .figsvg .ahd{fill:var(--ink);}
  .figsvg .pr{fill:var(--paper-2); stroke:var(--ink-soft); stroke-width:1.2;}
  .figsvg .tk{stroke:var(--ink-soft); stroke-width:.8;}
  .figsvg .po{fill:var(--ink); font:600 8.5px 'IBM Plex Mono',monospace;}
  .figsvg .pi{fill:var(--danger); font:600 7.5px 'IBM Plex Mono',monospace;}
  .figsvg .sh{fill:var(--gold-soft); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh2{fill:rgba(199,154,62,.38); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh3{fill:rgba(199,154,62,.22); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .none{fill:none;}
  .figsvg .hid{stroke-dasharray:5 4; fill:none;}
  .figsvg .tick{stroke:var(--ink); stroke-width:1.4; fill:none;}
  .figsvg .shd{fill:var(--accent-text); fill-opacity:.55;}
  .figsvg .cell{fill:var(--card); stroke:var(--ink); stroke-width:1.1;}
  .figsvg .dr{fill:var(--danger);} .figsvg .dw{fill:var(--card); stroke:var(--ink); stroke-width:1.2;}
  .figsvg .dotfill{fill:var(--danger);}
  .tt{border-collapse:collapse; font-size:13.5px; margin:4px auto; font-variant-numeric:tabular-nums;} .tt th,.tt td{border:1px solid var(--rule); padding:4px 9px; text-align:left;} .tt th{background:var(--paper-2); font-weight:700;} .ttw{overflow-x:auto; max-width:100%;}
  .fq{display:inline-flex; flex-direction:column; vertical-align:middle; text-align:center; font-size:.82em; line-height:1.12; margin:0 2px;}
  .fq>span:first-child{border-bottom:1.5px solid currentColor; padding:0 2px;}
  .fq>span:last-child{padding:0 2px;}
  .mx{white-space:nowrap;}
  .blank-input.fr{width:110px;}
  @media (prefers-reduced-motion:reduce){ *{transition:none !important;} }
.datline{display:block;margin-top:8px;padding:8px 10px;border-radius:8px;background:var(--paper-2);font:500 14px/1.7 'IBM Plex Mono',monospace;word-spacing:2px;overflow-wrap:anywhere;}

  .theory{display:flex;flex-direction:column;gap:16px;padding-bottom:40px;}
  .hub{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .hub{grid-template-columns:repeat(3,1fr);} }
  .hub-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:16px;display:flex;flex-direction:column;gap:8px;}
  .hub-card h3{font-family:'Fraunces',serif;font-size:18px;margin:0;color:var(--accent-text);}
  .hub-card p{margin:0;font-size:14px;color:var(--ink-soft);line-height:1.5;}
  .hub-btns{display:flex;flex-wrap:wrap;gap:8px;margin-top:auto;}
  .hub-btn{min-height:40px;border:1.5px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:10px;padding:8px 12px;font:600 14px 'Source Sans 3',sans-serif;cursor:pointer;text-align:left;}
  .hub-btn:hover{border-color:var(--gold);}
  .hub-btn.primary{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .note{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:18px;scroll-margin-top:120px;}
  .note h2{font-family:'Fraunces',serif;font-size:22px;margin:0 0 4px;color:var(--ink);}
  .note .lt{font-size:13.5px;color:var(--ink-soft);margin:0 0 12px;}
  .note .lt b{color:var(--accent-text);}
  .note h4{font:700 15px 'Source Sans 3',sans-serif;margin:16px 0 6px;color:var(--accent-text);}
  .note p,.note li{font-size:15.5px;line-height:1.6;}
  .note ul{padding-left:20px;margin:6px 0;}
  .keybox{background:var(--gold-soft);border-left:4px solid var(--gold);border-radius:8px;padding:10px 12px;margin:10px 0;font-size:15px;line-height:1.6;}
  .keybox b{color:var(--ink);}
  .ex{background:var(--paper-2);border-radius:10px;padding:12px;margin:10px 0;}
  .ex .exh{font-family:'Fraunces',serif;font-weight:700;color:var(--accent-text);margin-bottom:4px;}
  .ex .exl{font-size:15px;line-height:1.7;}
  .ttab{width:100%;border-collapse:collapse;font-size:14.5px;margin:8px 0;}
  .ttab th,.ttab td{border:1px solid var(--rule);padding:7px 8px;text-align:left;vertical-align:top;}
  .ttab th{background:var(--paper-2);}
  .tscroll{overflow-x:auto;}
  .mono{font-family:'IBM Plex Mono',monospace;font-size:.92em;}
  @media (max-width:480px){ .ttab{font-size:13.5px;} .ttab th,.ttab td{padding:6px;} }
  .note .figsvg{max-width:100%;height:auto;display:block;margin:8px auto;}


  .rep-top{display:flex;flex-wrap:wrap;gap:18px;align-items:center;justify-content:center;margin-top:8px;}
  .rep-legend{flex:1;min-width:220px;display:flex;flex-direction:column;gap:8px;}
  .rep-cap{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.05em;}
  .rep-li{display:flex;align-items:center;gap:6px;font-size:15px;}
  .rep-n{margin-left:auto;white-space:nowrap;padding-left:8px;font-family:'IBM Plex Mono',monospace;font-weight:600;}
  .sw{display:inline-block;width:12px;height:12px;border-radius:3px;flex:none;}
  .rep-grid{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .rep-grid{grid-template-columns:1fr 1fr;} }
  .rep-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:14px;display:flex;flex-direction:column;gap:10px;}
  .rep-h{display:flex;align-items:center;gap:8px;font:700 16px 'Source Sans 3',sans-serif;}
  .crit{display:inline-grid;place-items:center;width:28px;height:28px;border-radius:50%;color:var(--card);font:700 15px Fraunces,serif;flex:none;}
  .rep-row{display:flex;gap:14px;align-items:center;}
  .rep-stats{display:flex;flex-direction:column;gap:5px;font-size:14.5px;}
  .rep-stats div{display:flex;align-items:center;gap:6px;}
  .rep-lvl{margin-top:4px;color:var(--accent-text);} .rep-lvl span{color:var(--ink-soft);font-size:13px;}
  .rep-note{font-size:13px;color:var(--ink-soft);}


  .skip-chips{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin:12px 0;}
  .skip-chips .chip{min-width:48px;min-height:40px;cursor:pointer;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--retry-text);border-radius:10px;font:600 14px 'IBM Plex Mono',monospace;}
  .skip-btns{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px;}


  .kb-toggle{border:none;background:transparent;font-size:15px;cursor:pointer;padding:0 2px;vertical-align:middle;opacity:.7;}
  .vkb{position:fixed;left:0;right:0;bottom:0;z-index:80;background:var(--paper-2);border-top:1px solid var(--rule);box-shadow:0 -6px 20px rgba(0,0,0,.12);padding:6px 6px 8px;display:none;}
  .vkb.show{display:block;}
  .vkb-top{display:flex;justify-content:space-between;align-items:center;max-width:640px;margin:0 auto 4px;font:600 12px 'Source Sans 3',sans-serif;color:var(--ink-soft);}
  .vkb-link{border:none;background:none;color:var(--accent-text);font:600 12px 'Source Sans 3',sans-serif;cursor:pointer;text-decoration:underline;}
  .vkb-row{display:flex;gap:5px;max-width:640px;margin:0 auto 5px;}
  .vkb-k{flex:1;min-height:42px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 17px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .vkb-k.fn{font:600 13px 'Source Sans 3',sans-serif;background:var(--gold-soft);}
  .vkb-k.done{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .vkb-k:active{transform:scale(.96);}
  body.kb-open .wrap{padding-bottom:360px;}
  body.kb-open .fab{display:none;}
  .tool-bar{display:flex;gap:8px;flex-wrap:wrap;margin:-4px 0 10px;}
  .tool-btn{min-height:36px;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--ink);border-radius:18px;padding:4px 12px;font:600 13.5px 'Source Sans 3',sans-serif;cursor:pointer;}
  .tool-panel{position:fixed;z-index:85;background:var(--card);border:1px solid var(--rule);border-radius:14px;box-shadow:0 10px 30px rgba(0,0,0,.25);display:none;}
  .tool-panel.show{display:block;}
  .tp-head{display:flex;align-items:center;gap:8px;padding:8px 10px;border-bottom:1px solid var(--rule);font:600 14px 'Source Sans 3',sans-serif;}
  .tp-note{font-size:12px;color:var(--ink-soft);font-weight:500;}
  .tp-x{margin-left:auto;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:8px;min-height:32px;padding:2px 10px;cursor:pointer;font:600 13px 'Source Sans 3',sans-serif;}
  .tp-x + .tp-x{margin-left:0;}
  .calc{right:12px;bottom:84px;width:min(330px,calc(100vw - 24px));}
  body.calc-open .wrap{padding-bottom:440px;}
  body.calc-open .fab{display:none;}
  @media (max-width:640px){ .calc{left:6px;right:6px;width:auto;} .calc-keys button{min-height:36px;} }
  .calc-disp{padding:8px 12px;text-align:right;background:var(--paper-2);}
  .calc-expr{font:500 13px 'IBM Plex Mono',monospace;color:var(--ink-soft);min-height:18px;word-break:break-all;}
  .calc-res{font:600 24px 'IBM Plex Mono',monospace;color:var(--ink);word-break:break-all;}
  .calc-keys{display:grid;grid-template-columns:repeat(6,1fr);gap:5px;padding:8px;}
  .calc-keys button{min-height:40px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 14px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .calc-keys button.fn{background:var(--gold-soft);font-family:'Source Sans 3',sans-serif;font-size:13px;}
  .calc-keys button.eq{grid-column:span 2;background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .desmos{left:50%;top:50%;transform:translate(-50%,-50%);width:min(760px,calc(100vw - 16px));height:min(560px,calc(100vh - 90px));flex-direction:column;}
  .desmos.show{display:flex;}
  #desmosBox{flex:1;min-height:0;border-radius:0 0 14px 14px;overflow:hidden;}
  .desmos-msg{padding:24px;text-align:center;color:var(--ink-soft);}
  .chip[data-status="skipped"]{cursor:pointer;}
  .chip[data-status="answered"]{border-color:var(--accent-text);color:var(--accent-text);}


  button.crest-home{border:none;padding:0;position:relative;cursor:pointer;transition:transform .15s ease;}
  button.crest-home:hover,button.crest-home:focus-visible{transform:scale(1.06);outline:2px solid var(--gold);outline-offset:2px;}
  .crest-h{position:absolute;right:-7px;bottom:-7px;width:18px;height:18px;border-radius:50%;background:#F4EFDF;color:var(--navy);font:700 12px/18px 'Source Sans 3',sans-serif;text-align:center;box-shadow:0 1px 3px rgba(0,0,0,.3);}
  .brand .brand-row{position:relative;}
  .bmasw{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);display:flex;flex-shrink:0;white-space:nowrap;align-items:center;gap:6px;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.25);border-radius:99px;padding:5px 14px;color:#F4EFDF;}
  .bmasw-ic{font-size:16px;} .bmasw-t{font:600 20px 'IBM Plex Mono',monospace;letter-spacing:.02em;min-width:62px;text-align:center;}
  .bmasw-b{border:none;background:rgba(255,255,255,.18);color:#F4EFDF;border-radius:50%;width:30px;height:30px;cursor:pointer;font-size:13px;}
  .bmasw.off{display:none;}
  @media (max-width:560px){ .bmasw{position:static;transform:none;margin-left:auto;padding:4px 5px 4px 8px;gap:4px;} .bmasw-ic{display:none;} .bmasw-t{font-size:16px;min-width:48px;} .bmasw-b{width:26px;height:26px;} .brand .series-name{font-size:15px;} .brand .brand-name{font-size:10.5px;} .brand .brand-row>div:not(.bmasw){min-width:0;} }
  .bmasw-done{font:600 15px 'IBM Plex Mono',monospace;color:var(--accent-text);margin:4px 0 8px;}
  .sp-fab{position:fixed;left:14px;bottom:84px;z-index:60;border:1.5px solid var(--navy-2);background:var(--card);color:var(--ink);border-radius:99px;padding:9px 14px;font:700 14px 'Source Sans 3',sans-serif;box-shadow:0 4px 14px rgba(0,0,0,.15);cursor:pointer;}
  .sp-fab.on{background:var(--navy);color:#F4EFDF;}
  body.kb-open .sp-fab{display:none;}
  .sp-canvas{position:absolute;z-index:55;display:none;touch-action:none;cursor:crosshair;}
  .sp-canvas.passive{pointer-events:none;cursor:default;}
  .sp-bar{position:fixed;top:8px;left:8px;right:8px;margin:0 auto;width:max-content;z-index:90;display:none;align-items:center;gap:6px;background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:6px 8px;box-shadow:0 6px 20px rgba(0,0,0,.2);max-width:calc(100vw - 16px);flex-wrap:wrap;justify-content:center;}
  .sp-lbl{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);margin-right:2px;}
  .sp-pen,.sp-tool{width:38px;height:38px;border-radius:10px;border:1.5px solid var(--rule);background:var(--paper);cursor:pointer;display:inline-flex;align-items:center;justify-content:center;font-size:17px;padding:0;color:var(--ink);}
  .sp-pen i{width:20px;height:20px;border-radius:50%;display:block;}
  .sp-pen.on,.sp-tool.on{border-color:var(--navy-2);box-shadow:0 0 0 3px var(--gold-soft);}
  @media (max-width:560px){ .sp-lbl{display:none;} .sp-pen,.sp-tool{width:34px;height:34px;} .sp-fab span{display:none;} }

  /* larger reading sizes */
  .chapter-eyebrow{font-size:13.5px;}
  .chapter-title{font-size:36px;line-height:1.15;}
  .chapter-sub{font-size:16.5px;}
  .tab-btn{font-size:15.5px;}
  .sec-sub{font-size:15px;}
  .qtext{font-size:19px;line-height:1.55;}
  .qnum{width:36px;height:36px;font-size:16px;}
  .opt{font-size:17.5px;padding:12px 14px;}
  .step-line{font-size:17.5px;line-height:2;}
  .blank-input{font-size:16px;}
  .sol-line{font-size:16.5px;}
  .feedback{font-size:15px;}
  .note h2{font-size:28px;}
  .note h4{font-size:19px;}
  .note p,.note li{font-size:17.5px;line-height:1.65;}
  .note .lt{font-size:15.5px;}
  .ex .exh{font-size:18px;} .ex .exl{font-size:16.5px;}
  .keybox{font-size:16.5px;}
  .ttab{font-size:15.5px;}
  .hub-card h3{font-size:21px;} .hub-card p{font-size:15.5px;} .hub-btn{font-size:15px;}
  @media (max-width:480px){ .chapter-title{font-size:30px;} .qtext{font-size:18px;} .opt,.step-line{font-size:16.5px;} .note h2{font-size:24px;} .note p,.note li{font-size:16.5px;} }

  /* v4 celebration */
  .v4conf{position:fixed;inset:0;width:100vw;height:100vh;pointer-events:none;z-index:9999;}
  .v4ban{background:linear-gradient(135deg,var(--gold-soft),var(--card));border:2px solid var(--gold);border-radius:18px;padding:18px 14px 16px;margin:-4px 0 18px;text-align:center;animation:v4pop .55s cubic-bezier(.2,1.6,.4,1);}
  @keyframes v4pop{0%{transform:scale(.6);opacity:0}100%{transform:scale(1);opacity:1}}
  .v4trophy{font-size:54px;line-height:1;animation:v4bob 1.4s ease-in-out infinite;}
  @keyframes v4bob{0%,100%{transform:translateY(0) rotate(-6deg)}50%{transform:translateY(-6px) rotate(6deg)}}
  .v4h{font-size:28px;font-weight:800;color:var(--accent-text);margin-top:6px;}
  .v4m{font-size:19px;color:var(--ink);margin-top:4px;}
  .v4pills{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-top:12px;}
  .v4p{font-size:16px;font-weight:700;border-radius:999px;padding:6px 12px;}
  .v4p.g{background:var(--success-soft);color:var(--success);} .v4p.o{background:var(--gold-soft);color:var(--retry-text);}
  .v4p.r{background:var(--danger-soft);color:var(--danger);} .v4p.s{background:var(--rule);color:var(--ink);}
  .v4next{margin-top:14px;} .v4go{font-size:18px !important;padding:13px 20px !important;}
  .v4rec td.v4g{color:var(--success);font-weight:700;} .v4rec td.v4o{color:var(--retry-text);font-weight:700;} .v4rec td.v4r{color:var(--danger);font-weight:700;}
  .v4rec tr.v4tot td{font-weight:800;border-top:2px solid var(--rule);}
  .v4rec th{font-size:12.5px;padding:6px 3px !important;white-space:nowrap;} .v4rec td{font-size:15px;padding:7px 3px !important;text-align:center;}
  .v4rec td:first-child,.v4rec th:first-child{text-align:left;white-space:normal;min-width:92px;max-width:150px;font-size:14.5px;}
  @media(max-width:460px){ .v4left{display:none;} }
  .v4leg{font-size:14.5px;color:var(--ink-soft);margin:2px 0 8px;line-height:1.5;}
  body.v4done .fab-q,body.v4done #qFab{display:none;}
  .v4sum{font-size:16px;margin-top:10px;}
  /* v4 larger reading sizes */
  body{font-size:18px;}
  .chapter-title{font-size:38px !important;line-height:1.15;}
  .chapter-sub{font-size:17px !important;}
  .tab-btn{font-size:16.5px !important;}
  .sec-sub{font-size:16.5px !important;}
  .qtext{font-size:21px !important;line-height:1.6 !important;}
  .qnum{width:38px !important;height:38px !important;font-size:17px !important;}
  .opt{font-size:19.5px !important;padding:13px 15px !important;}
  .step-line{font-size:19.5px !important;line-height:2.1 !important;}
  .blank-input{font-size:18px !important;min-height:40px;}
  .sol-line{font-size:18px !important;line-height:1.6;}
  .feedback{font-size:16.5px !important;}
  .note h2{font-size:29px !important;}
  .note h3{font-size:22px !important;}
  .note h4{font-size:20px !important;}
  .note p,.note li,.note td,.note th{font-size:18.5px !important;line-height:1.7 !important;}
  .ex .exh{font-size:19px !important;} .ex .exl{font-size:18px !important;}
  .keybox{font-size:18px !important;}
  .hub-card p{font-size:17.5px !important;} .hub-btn{font-size:16.5px !important;}
  .review-q,.review-ans{font-size:17.5px !important;}
  .rec-table td{font-size:16px;}
  .vkb-k{font-size:19px !important;}
  .fq{font-size:0.95em;}

  /* v5 plotters */
  .plotw{background:var(--card);border:1px solid var(--rule);border-radius:12px;padding:10px;margin:6px 0 4px;}
  .plotw svg{display:block;margin:0 auto;cursor:crosshair;}
  .plw-msg{font-size:15px;color:var(--ink-soft);margin:6px 2px;}
  .plw-tools{display:flex;gap:8px;flex-wrap:wrap;margin-top:6px;}
  .plw-tools button,.plw-row button{font:600 14px 'Source Sans 3',sans-serif;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:8px;padding:7px 10px;cursor:pointer;min-height:36px;}
  .plw-row{display:flex;align-items:center;gap:6px;flex-wrap:wrap;padding:6px;border-radius:8px;margin-top:6px;border:1px solid transparent;}
  .plw-row.sel{border-color:var(--gold);background:var(--gold-soft);}
  .plw-sw{width:14px;height:14px;border-radius:4px;display:inline-block;}
  .plw-eq{font:600 16px 'IBM Plex Mono',monospace;margin-right:4px;}
  .plw-sum{font-size:16px;margin-top:8px;} .plw-key{font-size:15px;margin-top:6px;color:var(--ink);}

  /* v6 accuracy meter */
  .accm{max-width:900px;margin:6px auto 0;padding:6px 16px;display:flex;align-items:center;gap:10px;}
  .accg{width:64px;height:38px;flex:0 0 auto;}
  .acct{display:flex;flex-direction:column;line-height:1.25;font-size:14.5px;color:var(--ink-soft);}
  .acct b{font-size:16px;color:var(--ink);} .accp{font:700 18px 'IBM Plex Mono',monospace;margin-left:4px;}
  .accp.g{color:var(--success);} .accp.o{color:var(--retry-text);} .accp.r{color:var(--danger);}
  /* v6 observations */
  .v6obs{text-align:left;background:var(--card);border:1px solid var(--rule);border-left:5px solid var(--accent-text);border-radius:14px;padding:14px 16px;margin:0 0 16px;}
  .v6h{font:700 21px 'Fraunces',Georgia,serif;color:var(--accent-text);margin-bottom:6px;}
  .v6lvl{font-size:17px;font-weight:700;padding:8px 10px;border-radius:10px;margin-bottom:8px;}
  .v6lvl.g{background:var(--success-soft);color:var(--success);} .v6lvl.o{background:var(--gold-soft);color:var(--retry-text);} .v6lvl.r{background:var(--danger-soft);color:var(--danger);}
  .v6sub{font-weight:800;font-size:15px;text-transform:uppercase;letter-spacing:.04em;color:var(--ink-soft);margin:10px 0 4px;}
  .v6ul{margin:0;padding-left:20px;} .v6ul li{font-size:17px;line-height:1.55;margin:3px 0;} .v6p{font-size:17px;margin:2px 0;}
  .v6q{font:700 14px 'IBM Plex Mono',monospace;border:1px solid var(--danger);color:var(--danger);background:var(--danger-soft);border-radius:8px;padding:3px 8px;cursor:pointer;margin:2px 2px;}
  .v6btns{display:flex;flex-direction:column;gap:6px;} .v6btns button{text-align:left;font:600 16px 'Source Sans 3',sans-serif;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:10px;padding:9px 12px;cursor:pointer;}
  /* v6 whiteboard */
  .wb-fab{position:fixed;left:14px;bottom:calc(140px + env(safe-area-inset-bottom,0px));z-index:40;border:1px solid var(--rule);background:var(--card);color:var(--ink);border-radius:999px;padding:9px 14px;font:700 15px 'Source Sans 3',sans-serif;box-shadow:0 2px 8px rgba(0,0,0,.15);cursor:pointer;}
  @media(max-width:520px){ .wb-fab span{display:none;} .wb-fab{padding:9px 11px;} }
  .wbov{position:fixed;inset:0;z-index:9000;background:#f3f4f6;display:none;flex-direction:column;}
  .wbov.show{display:flex;} body.wb-open{overflow:hidden;}
  .wbbar{display:flex;flex-wrap:nowrap;overflow-x:auto;-webkit-overflow-scrolling:touch;align-items:center;gap:4px;padding:6px 8px;background:#fff;border-bottom:1px solid #e5e7eb;box-shadow:0 1px 4px rgba(0,0,0,.06);}
  .wbbar button{flex:0 0 auto;min-width:38px;height:38px;border:1px solid #e5e7eb;background:#fff;border-radius:9px;font:600 17px sans-serif;color:#111;cursor:pointer;}
  .wbbar button.on{border-color:#2563eb;background:#dbeafe;} .wbc{min-width:26px!important;width:26px;height:26px!important;border-radius:50%!important;border:2px solid #d1d5db!important;}
  .wbc.on{outline:3px solid #2563eb;outline-offset:1px;} .wbsep{flex:0 0 auto;width:1px;height:26px;background:#e5e7eb;margin:0 3px;}
  .wbsz{width:90px;flex:0 0 auto;} .wbpg{font:600 14px sans-serif;color:#374151;min-width:44px;text-align:center;} .wbx{padding:0 10px;font-size:15px!important;}
  .wbcv{flex:1;width:100%;min-width:0;min-height:0;touch-action:none;cursor:crosshair;display:block;background:#fff;}
  .wbbody{flex:1;display:flex;flex-direction:column;min-height:0;}
  .wbq{background:var(--paper);color:var(--ink);border-bottom:3px solid var(--gold);max-height:40vh;overflow:auto;padding:8px 12px 10px;flex:0 0 auto;}
  .wbqh{display:flex;align-items:center;justify-content:space-between;gap:8px;font-size:15px;color:var(--accent-text);margin-bottom:6px;position:sticky;top:-8px;background:var(--paper);padding:4px 0;z-index:1;}
  .wbqt{font:600 14px 'Source Sans 3',sans-serif;border:1px solid var(--rule);background:var(--card);color:var(--ink);border-radius:8px;padding:5px 10px;cursor:pointer;}
  .wbq.min{max-height:none;} .wbq.min .wbqc{display:none;}
  .wbqc .qcard{margin:0;box-shadow:none;} .wbqc .qtext{font-size:19px !important;} .wbqc input{pointer-events:none;}
  @media(min-width:860px){ .wbbody{flex-direction:row;} .wbq{width:40%;max-width:520px;max-height:none;border-bottom:0;border-right:3px solid var(--gold);} .wbq.min{width:auto;} }
  .wbin{position:fixed;z-index:9001;font:20px 'Source Sans 3',sans-serif;border:1px dashed #2563eb;background:rgba(255,255,255,.9);padding:2px 6px;min-width:140px;}

  .scatw{background:var(--card);border:1px solid var(--rule);border-radius:12px;padding:8px;margin:6px 0 4px;}
  .scatw svg{display:block;margin:0 auto;cursor:crosshair;}
  .scw-sum{font-size:15.5px;margin-top:6px;}

  .gp-hidden{position:absolute !important;width:2px !important;height:2px !important;padding:0 !important;border:0 !important;opacity:0 !important;overflow:hidden;}
  .gp-box{margin:8px 0 4px;padding:10px;border:1px solid var(--rule);border-radius:12px;background:var(--card);}
  .gp-help{font-size:15px;color:var(--ink-soft);margin-bottom:6px;line-height:1.4;}
  .gp-svg{display:block;margin:0 auto;width:100%;max-width:380px;user-select:none;-webkit-user-select:none;cursor:crosshair;}
  .gp-tools{display:flex;flex-wrap:wrap;gap:6px;align-items:center;margin-top:8px;}
  .gp-tools.gp-n{display:block;line-height:2.6;}
  .gp-b{font:600 15px 'Source Sans 3',sans-serif;border:1.5px solid var(--rule);background:var(--paper);color:var(--ink);border-radius:999px;padding:6px 12px;cursor:pointer;margin:0 3px 0 0;}
  .gp-b.on{border-color:var(--accent-text);background:var(--gold-soft);color:var(--accent-text);}
  .gp-lab{font-weight:700;margin-right:6px;}
  .gp-in{font:16px 'IBM Plex Mono',monospace;width:90px;border:1.5px solid var(--rule);border-radius:6px;padding:4px 6px;margin-right:6px;background:var(--card);color:var(--ink);}
  .gp-stat{font-size:15px;margin-top:6px;color:var(--accent-text);font-weight:600;}
  .ineq-grapher{border:2px solid var(--gold);border-radius:14px;padding:12px;margin:14px 0;background:var(--card);}
  .gr-head{font:700 19px 'Fraunces',serif;color:var(--accent-text);margin-bottom:6px;}
  .gr-row{display:flex;gap:8px;} .gr-in{flex:1;min-width:0;font:16px 'IBM Plex Mono',monospace;border:1.5px solid var(--rule);border-radius:8px;padding:8px;background:var(--paper);color:var(--ink);}
  .gr-hint{font-size:14.5px;color:var(--ink-soft);margin:6px 0;}
  .gr-cv{width:100%;max-width:420px;display:block;margin:6px auto;border:1px solid var(--rule);border-radius:8px;}
  .gr-msg{font-size:15px;color:var(--accent-text);font-weight:600;}

  header.brand{background:linear-gradient(180deg,rgba(20,20,20,.55),rgba(20,20,20,.78)),url('data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAA0JCgsKCA0LCgsODg0PEyAVExISEyccHhcgLikxMC4pLSwzOko+MzZGNywtQFdBRkxOUlNSMj5aYVpQYEpRUk//2wBDAQ4ODhMREyYVFSZPNS01T09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT09PT0//wAARCAKQA+gDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwDneDkAjA9aYPvcikdsJgcnNLnJ3AHNUMjbkHPrTu3pQ3NIM9KAEPIzSA4p2cZ4qM8knjigCVM7/wBafkEnkZqNOByMjvinAA8jAoAjJBkyP1pX449qGQhexOM03lthzwODSAf0UEVKZFZBuOcdBUfJRhzzTJAeMnNMCQP64P17U4yk9MAjoRVdemcU7jHSkA52BHI5oY/KMGo8qSM8U7ChT15pgOTn0p3IAG7HeoC2D8tP3n7mTzySKAJB0JU8d6QED5sHOabuyQV4Ap4JHP4igB6lASGGVPY9jSKM544z0zTCx+8f/wBVBcY/iFADycnIpPm/L1pm8rknJzSh88mgByl8jcMCpDtI2g5HaoVLKRnOKdjIGDzSAVgdvI5HWm546cUvcBWp2cIGwAegx3pgIOMEjg0EjOQe9Nzyck/Sg4PagAbOKj/Cn9aP5UAJml/GkOKD2NAD84oJOevakzl6CQRQA4OoIJGe2KnVFXOCDuHymquBnpmpQMxd+OaQDgpcgM2BQ/3SCAB6d6ZncwA4pXUfwvuwOtADV4xjH0pwYn+Gm85y2OacDkbihA7GmA18hgfWkJIIp/Xr09KTqD+lADQ2OpNPXGOvHpUSj5ueacc5JxkCgB5ZQOODTf4CQOvWmj5ulIeO5FACsVOFzTs8npyaYeO4NA5oAeSN3Xp0pWwwBPXvTQB2GaXGASQc5oAT8MUYoxSjGOTzQA3GaBx3pwYqwK9QeKQglyW6n0oAXJxT88Ad6QEY24/GheGxigCaBgk8bP8AdDjNaPiONzqTXG3MUoBQ9iMCssnAyKvpq0wsxaOqPEBgbxnFICLT7U3EoXcqqOSxOMCptZu4rmWOKDd5UI2gmqQmdIyit8p6gVGeeh/CgABppNKPunNJ2pgFHNA5pxUrwRQAykp30pDQAlFIaBzQA6kFFLQAlHNFLQAClpM0v1oATPPSlzRRQAZxRmg9aKAFBoNJ0pM80AKODTgc8ZxTaBQBLjnrSFR3qPcc0u40ABpe2KAd3saM47UABNCuVIIJBHQ0hHGabQBpxaluiEN0N8YOc9xV0jR5MEyMVHIUnBzXP54pwOBSsBtxQ2M8ssETKrN/q+tZs0TRkqykDJxnvVdJHjkV0JDA5B9K30uLXVLNUlIW4Xrk4z+NAGDyGx2p/GM1ojRLhj8skOP98U/+xZUOHmh5HZ6AMkD0Gc1qadZICLm6ysY7VdtLOxtVL3MkZYjIBOaoapfpc4jhBES9BQBFqV4LmbCNiNfu8VHBeXNsuIpWC+naq+38BSFj5fFMC+2r3rgkzdfaqst1LJ9+Rj+NQAkLS4GOtAATu5Jz9ab3o6cUoHGaAAnjigHI57U3vTgKADOaaaUcUN0oAX+Goz96nZ4ppIzzQA1hjNA6Uu4c8Uwg43UALk0Ed6XcCv3aM5WgBueCKj7089aAcdqADtStynHWgn0o+bHSgCPA289aepzgHqOlMY80oPOP1oAnzuHPWomHBoU/MOelP4KGgCvTgeKa3WjPFADqKF5ooAkKkc9jTgMc5pQV3H09acy7V3KQQelAEQXcCc0ueeacRlMdMUw5HFACn71I6464HrQc5yBTWHZs4oEKPl7ECnkgY3If8aaDlVByQKkb5gWRsAcAmkAhwcKuM+maYo2hlPHORRuJwccikyR8x5z1FAEuRgZPFRkYHfn9KmC9B2HPNQAkvtzgetMY9UDKcdv1pWWM8xnp1BFNTccEcAU9HyDnAz7daAIyAAcdexpcADB5NDfKQOCvpSblbqcGgBu1SfenbQOgoUDO4UbuKAEwAc0IpJ/lRndgfnSq4BwQAOxoAVsIc9MVGXccZ96lcb+namOuTmkIYpyeakCg/wBaaEPalOB1zmmA8MBgZJNG4eoFN7ZIwO1OZdo4AzjnvQAoHy5NNC9eue1DNlQFByO9Bfna3X1oGIMjr+NLkHgZNKACeKcrYPzHaO2BQAikHg//AKqUgY60hQ8nOfQ+tNDYGDmgAK980YFJ1OcUuV7CgBcAdKB0pMijIx0oAcMZ/nTt3zZHSow3tTg2etAhwB3ZXmk2A5Kkg+9AchNueM807jbnpQMMn+KlHzxgIeQelJ94ZIO096RVIkGKAHgA7cH73TPY011wcEYpV4ZgwGDTt5VQNx5GP/rUARhNpJI6UxT05qV9zxkn72O9QqmGBBwQKQEjAH5RyOxppGF+YAD0zUyKNm5zjI445NQ4BJb+IHlaYCAcYK4PrR3wPSnhSwL8471FjBLCgB6Hjp704ybhyeppoUqDgcUhzheKAHHr8p7UmfXGaFx09aUkL059qAFGNw6CnAKVJ24I4+tRqwBBwM9QKdGwdNrMQQeR6UAOGcdsUmSKGYZwvIFKhAOT17UAO+YYPIIpG+Y9aUsSRmkJIP8AjQA0g+tKfUUbs9KSgBR0pKKDzQAop8pLHJGD/Om4oOSaAEAOOlNNOJNNxk0AIBmkP0xSgYPWigBMUoowaKAFByaUjnjpTRTqAEApaXp0ooAQdacBmjg96QGgAxTaeaQigBAfWjFJ0ozQAtKKbmloAXFGaTNHvQAHg5FOz0IphJ6UqkZxQA480mKAe1P2/LmgCLFGR604r9a0YNId4hLcTJAp6Bup/CgDNpykocjg1qHTrAqRFqAaTsCmM1RmheCTbIMGgB8d5Mv3WFNeeVzlm/KoQQDxSk47UAPyxBySeKT+EcUgJ2mk3Z60AO6gCjbhSKdgcGhiDQIiINFKTk8009aBiMOaX+GkPNGeMUAA6048U2lcENg0AIMHinOAOM1H0NOY5FACcAdaYRz1pxxTd3NADGpVGQQaGFIpKc0AOJApudp9jTs/xEcGm5DZFIBXHGaizzUg5X6VGw9sUwF60u44xmkFB60ANNAx3oP1pmfmoAlABBxThkLUYPOc5p27igBGHNMPFSds0080AKOKKQg0UCJMnuCKeGIAB6elLsAOMZJ6UcFSKAAqQM5pp9SKkBAHXNNOCOKAGq5JwOlJk4Oe1CNhsjrTpPuk9vWgBgYt7D1p7NuxwABwB6UxSQhI6VIcGMDjLdT6UhkYbH0PejOflHPvTeeT0H86VARmmIkUssbAtxQcKBkDigdOR1pHGdueAaBkmMDPekxhehOaQFhn5u+KUO3TPNAAV5A25BFJsAHAFKZCDlTk0hJzmgBhTA+WmH2qfdjGRTGPz4/KgBhOQMDApw569DSAgHBFKcY54+lIQ4qwHIPPQ1Gdx75qbzGKjOGA6ZqMj58jgGgBFLDjOKeTnqcUhHamuNwHOKYDlYHKAceppcHOD0pgGFCnIpykHgn8aBjuhGecUFA55pCenf3p4fjkUAMK7QaRfl59PWpOG4APJpdoOcAYB5NAEbdQQcZoOe/SnNgnjH4UmcHsc0hDR7njtS4xzxSPwwB7UM2famAUgyTgdaKUDn2pANGSen1p34VJvZX+QqT3IHFNAOMscAHHvTGNPtStyMUhWlC54LYoAepO3Hal3YHHIFN2n1oA2jJBoAlBwh5+92xQB1C4yBTAQDTiA3Qc96AFkO5iM4JpjKUOSeRQWwcNz2GaXgZwcjtSAbljyeSRwfSmfMGD55HWpCMA4PB6ikfAHHSmAm3qATg9qVV5II600dOKUbsj+tADl5BB+lNxg7TxmnEkt257UP2zQA0x8delCAg+vtTsE96THOQee1ACbd3bmjac5XO4daM5G4dR1qQDPI6j9aAGKedpHXvTwMnjBxSkAgEDnNK6rnI4zzQAqR732l1HGcmkbIJ4Ao5OeBuNI4J6HoOaQDBSkcUgOTTu2Q34UwGUU7qM96aDgGgB2enP4UhNN2jAOeakOAnvQAlNNKD8tC9CfSgA7ZwKKTt9aB1NACcEdMmkwaeB1HrSUAJSiikoAdRmjjvRxQADmnDpTR1px60AJyBSdetO7Uh60AJTTT6DQIj706g0UDFpDS0hAoATNAPNIRQKAJBzSjd2NMFPHWgC9p1qbmcDOdpBxjqM0l7I8lw/mEkg457UyzmeCcPGcMOhrVurexuttwlwtuW++jAnBpAYfPqc1oXERbTDLMSJEIxn0q8NOsIgJWv4SM9gaztWvI5sRQZKL1Y/xUAZobmgk0nvS0xCq2BzTwRTAMinAUALuxxRzj2p5Hy00HFACNjHvTGOal4PIprDI96BkdBpcUCgBUBZgM06blif1oUDNNYnpnpQAw9aUjilHSkbpQA3mmkE9BTs0eYVoAZknjFDDIxQG5zSkigBgzjBNIODT84NDrxkd6AEHf3plOGR1prcGgBM4NHBzQRxSCgBM03nPHSnd6SgBAMGnZpppQaAJP4aQDIpR0pyCgBhzRStxRSAmckNxye9JyT05o6igYBAOaBAR83HegE4IHFGQAePxpu4c0wGk4bPSkLnA5/DFKOTg0YCsNx4oGOC4UEHJPUUYyflBx3pFODwaeCB+PXFADNg/rQmGbDZzUm5CCCeaaRjp36UgEchSQKAQ0e04zTGGWAzjmnADactyD+dAC8lcNxt7035M5+akZmIyTwabyOpoEOz1xxTieMjrmmfQigcmgCXcxxn0ozk4JzTVbBx2p7bQwwMUwGs6qQMUgOTk0Hk56ntSqp780DEx3VvzoBPrmhxxTk6f40CA+/FOjKnr0FNPNRgHJxQMmADPgjilKDsMUgG1KbzigB2096MHuOKaM7Qe9PEjelAhOc5Gcj0oywG0dOtAY9eKdvHagCEMOT/ADp4bpnFIQrcjik20AS5U9aTaGPBAApAMU7JIoAjYUg/WnkZ6U0Lg5oGNUkKQD3pwznr260jDByO9PGOCOnegBM9qTOKUgdRzSgH0oEKHP0p2CzYHT3pgGTgClY4TPvigYn3XpzPkYHahQdufSo8c57mgB3U5I604bfX6UgxSDg4AzmgB/QEmox/EKeSTwwwKdsX14NADM7Txj6U4urDlefbpSeXk04Io759aAFPzJnPK+1MJyAfzqUABhlSB0JqNlK5AP0oAUUhBLZHanRIyx+Y5whOBTcg8g4oAMEu3rT0Vvv7frQowwz3pWOaAAJtfC9DSMMEjPAp3I4HWhgWTA9eaAIRuGefpQjlTnr7U5+MEdKYaAJOMblA2nt6Uh6ZGKaMg5HSlGD/AL3pQA5cEcmkPAozgUmaAAdKDzwKQ9CaOgBoAeAQOMEelAwx44B4xTM80uc9TQAmMtj0oAPcikPfJ60maAH/AI80meaOO9IaAA0tKuRSElj0oAKKMGg4oAXnHFGTmheaUigAHNB6Uhozxg0AO7U00A54pSvvQA3vQetIRg0UALmjrRSUABFIKWjFADh2xU0UEkjAIpOaSzjEt1EjdGYZrRl1G7SZhC+xEOAFAFICm0cls+JBtNNeZpFCk9Oa2hI2p6XcPdABoRuV9oGTWArbTQA4AkHOTSEZGKXd3FOyMUwItuBzTanxu4xTCuKAGKcU8MOpFNIpKAJC5OR2pjZoBOMUn1NABlhUg5HNRmgMRQBIy5pvSlDZFO4xz1oAb90E9zUZPNOY5PNIcYoAWmnmnZ4ph4oAQ00jIzTyRjpzTaAGDg0GnHrSECgBATnmhmwMCg0YoAYWz1oPTNKwHXNIvpQArj5QRUZqYdMGmEc0AMoPWlxzSkUAR0opTSDmgB4p6H0pg9KcoxQAsi0UrciigBzYB9u1IQemfxoyScGgfJxk4oAQgnPOaYA3XsalKkj5aZ8wz82BQAqg7c80EZXB7nvTQWztzinBmHBHPvQAzG0jngUquQ2OgND8In61EDluRxQBY2hm5IxjOaRsq2D1puDIPlyCO1BGMBhnFIAGN+T+dKjBX77c8H0oPsM0sRIGwgMD2PamIRhljnGSfzpgADdeCfypzKVJ67aaevpSATuR1HrTsYFIPypy/wCTTAaCWOAOOlO6AA/e70Bep5FJsx6/jQMUOQMUu/imAYp5AIBNAAGyRtp4BGcUzaMZzg05en3qAEOd3NA/WhuT1poyWFAEu3IFNPpT2GRjNR7SDyaAFzgClLnPSmZPSk+bpQA/d68UcdjSA9OM08YP8PPagQ3bkUYx3pcgd6bknjFACqDnin9qjyc4HAoyc0DHMR9KMn1pCxxQcYz0NAAeTk0uce1KBkUYoABz7UfN2NOUYpCoLEg/hQAgcjjuaVvu7e696TAIwBz60pJ2haAGswKAjtSAknOKXaWGD0pNrKcZoAVAzNwKd/CfY0wb89aXDKGoAVjxjOc0gYEcjmlwcetMA9eaAJEcA8jNSC4KqU42ntioRz0FG0gZoAtI5lG0enQmo2XIBGMe1Q4OKfGSp9j1pAKchCvQZpmeOR0p7DJ655ppTmmBKGLJgcnGRRkHBFM6Ebe1PXGSQOG6j0oACuD8xHPp2qQ8JhD9aZ8ucYIp45UhTyPWgCHBBxjg03GGqbJBwaY45oAZkZpSvORSU/qvFADRyfegkDrS4wc5obB+tACN92mEnFLzSYoATNLmm8UoBoAXNJmgjFJg0AOLGkBJ7UnJ60o4oAdmlzTc0ZoAduxQfamk04MoHTmgABxSg5peG6ikIxQAtJ1ozRjvQAnQ4p3QYpGGBTc560APyKaaUdMUuDjtQAzNFKQB1pKACloooAfGxjkV16jkVrtd6VNiWeOZZcYZEwATWKCRRuNIDZ1G/gubRIrWPyEU8oO/uayh19aYrVZjUEbh27UAQ8ntT1X2pWJ9MUwOR0pgT7cY4pj80LIT3oPNAER602pGB7U3BoAaaKU0lABig8UtIaAGZwalByKjIpyHA5oAccYpBil60gHNACNxTR7inuD+FMxQA00Up9qSgBDQ1LSGgBv1peo6cUEU5HHlFCOSetAEe0McCmgEH6VI3ykgGmfWgBOppelIv0pdpJ4oAbuHakzxSkEYpGBzyKAEOOtLgcGm9sU/nbQAMQHBFOBpmPWlU8UASY4opucCigABOBnj0p75dQc0bPkGDye39aG3YVRwB1oAB3yelJtwxI6H1pCoAyrU192SopAHmEE/1qZQpUNkMR19qgClcLjJp2wqxKn6jNMRLIAUwSAF596jBDnA4Udc04KzHAwRTMHJbH40hj1TBAUjmnOoXIJBJHJqM9inNJkjr09aYhxOOgyKFY9cUwpkE5oU5Ix2oGTN8y9M1ER7U7JwD1zQGXPzKeKAG4IGcAD1NGR0BJoyGbPYdqUMCDk7fQUAIMYwGxShvbIprKG24HfrTiuPSgBOvSnAEYFLH3zSn9aAEIyMYpQOOlLQOKAGMueM0iD5qkNNx3oEKwz3oCgj5jSjFIaBhuXOB2pGwaaw5460CgBeehHHY08jH3eTTgFGOcGmOwZsZwB+tAhGXPfmk+YdqdgN900gGDigAAXqTzTuB0AoA9cZ7UnKngDFAwekxyOKf33H8qOvWgBnOfl6U5WH8Q5pMsD2NLuGfnU0AOyCeDQAMUwkZ+XpQMgdaBDuaXtjtTRSigYuOOKQICc7sUvuKQ0ABUAdaUEMeKQEY5FLtUZIoAD8vHamH2FPH3eRTWHvQAKdpzing7l57VHSjJHBxQBI6+gx60gYd+neo8EZJNO7UAJIAh4+6ehpQcj+tNk+ZR9aMZIx2oAmUKyElgCOx70BTu461CeRx0oDMOh4oAsKPmxnBPalYD7zdRwcURvGWYuTkjj60roeQDSAaQOuTS5XBBXmow+D64pwYOpUj5uoNMBh68U49QOlR5wcVIwy4PtQAw+hpKew+am0AKx9KTI70oxTWAxQA8xqYs7h7AdaaMcUisV6AEGk3A+1ACkcZpuakYjPydPeoyMGgAGKcBnpSAU8DFADSKawwOtSGkIzQBGTmhTSuMdOlNzigCQHHepFYFTzUKnnpmpCgPK8UAHG0etFAIx83Slwce3rQA3JzzSMvpSgZPFKeKAAHbQG9KAM0nSgBxxjrzTSOaTPNO7e9ADaKWg0AFBoFFACVJG5HGaZSd6ALO7cvao2HNNU81IRxmgCMEg0/eaAuTTyVAwRQA0sT0NMye9BHORS5BoAbmlA5oxR0oAQ9aUc0e9KpBNADcUU9gO1MIwaADPan4yKiPWnKaAJMjGDTBgkg0EE9DRj16igBuBnBNGMA96RsZ9aXI20ARgEmlPIFLjBptACHpSDrntS9KCMjrQAS4PQ00DIoA980EY+lABwDTkZc/PkfSm5pM0AOOARg+/NK8zlCHwc9z1ppOVHtSOAeQKQDcc0vNN7cUuSRg0wA+tJnBoOabQA8MD2oqNT81FAF4gFvkOAe/pUZGADTyeqkdeQe1IDv+Q8Z5pARZJP6UuAOjCkZCjYYUrIRg+tMQgPIP40HBOR3pCWC9TxTl3EDNACde+KcMBOcnnkU0j5sDk0ws27GRj2pASM2RlQAo7UofA2sAfeogefrT1BJ4XP1pgLIMDj8KZkA5x9aMMvynn0o7YoAAQo45pGb60H1pPr+dACFs8DrUikYHHNMBHRacF/KgY6nDpTc8UmefegQ8nGfehc9zTAe5qQcgGgApMUpBNGKADOBSj6UmR7UbqBgcUn8qaWPpil6delAh23cOTio2yrfLzUgwOv6UrHBwQPrQMjDMfvAmjnvUm4AZWjOe2KBDAcfwmndqd0HPNJkZOePSgBF689aUkUuB95SDimk5oAcD3obr1pM8c0E8+lACZLdcU4A9uaQYpwJ9aAGnoeMGkH508kmkxzQAdKAaSgUDHZwaM+1NzSg8UAOzgDikLZ4NGc0FuOnFACHp6U33HalPPQ0nlnOc0APkUowVsHIzxR8u0c0KWz0+lGTjkYoAAoY4zQY279PWl+lJufpnNADTnHSmkOWFS7/UUZU846UARKrZOfxp3BHSl3Eg8detGRgcUAJjpzUpdtvU0gXJA64Gabuyu09jQAu8N1XB9RSgDP3uRUZHYmgEqaAHPtzkHOaeTmMVGMHgg561KoBQ88UARg5/ClPPFIOM5pep4oAChApvJHFScd6bxv2jmgCHJBp3XmnNH2703GKBBjHQ0m6gk03BNAxwcBhmpuAoIORVfGaeGIXFAEnofXg04jbkHqKiV8ZB6VMDvjGc5H8qAI2Uke1N2VKvI47Uwn5gaAGhcGnA0EZGaMYFADipI3EdaM4GKNxbgZwOlM70ASgcA0Fc9KaMgZoQknk0gDABxQQMUh60Z+WmA0ilAxzR3pT6elAATk0nSjIFGQRQAUGig9RQAnelpD1paAHA1KDlagoBIPFAEu75vpSs2aizzS5yKBC55pR1po5pRQMeBSMM0A4HNJmgBMfL700A5p+RS4AOT0oASkNK3DGkzQAEDYD3pBjvSs2QB6U0k0AKeO9OD7hgkZ9fWouT1pBnNAE4TceByB0pCvY00P6HmpVKBcjJbvSAgI+Y0xhg1YdVweRnFQ7cj3oAYRzzSUuCetNNMQUh6UuM0ntQMQHigGm0nQ0ASgjoaUbc8nios+tO3LQAONrDA6009aV2BximFqAHZppNFI1AAOTRSLz3ooAuqQUIbHXims+SOOR0NCtnOAPekb1KjFAh45bDHkd/Wm8jIBxnrmnJ8/Xk05jnIYEnsaQys3YD/9dKxbHDUjctnGAD0ozgdOTTAGPGcU3Hft6Urfdxik7cZzQAZ56U8H8aZsP3sU4BSPvYoAU9CaRSe9NKgH7xNKvB6/SgQ49enNRsD370rkhvXFLyeooAaOfapFAxyaQDtindRgCgBO3BpO/Xil2naOabgg8gUAAFT5+QVEKeCe3SgY7FKADTRk+1PyOwzigCMimFsHNP7Hg0wAfxdPSgAALfN+VLuJGOc0E44zxQMk/L+tADlbruGaCwUcN+HakwAOv4UmMnPFACq3JQ9O1OAwM00LnGMZ96U5HGc0AOJyKbwe1ISSKTcQORQA8YoIOMA00N7U4GgQ0B/WgA1JSdu9ABinfSmgHb+NB68UDA8Cm7qcelM79KAHA5p2M0zOKXNAAVPrRS8+tNNACqcHNOxjOO9ImD6ZpSCDQAADIzTiORg03NKTu70AKGxwaMkjPWlAyKUDHSgBmMmgqwFSfL3HNBBPORigCHHqaDjsaeRg5zmkC7jwOaAG7tox2pN3PSnMhFIE44NADsvuDBqXb696bhOmDSg/3QfxoARlz7CgdKczevNIee2KADnGKVSwzilIOaXoKAEzntimlcHNOIO3OOPWkye9ACq2OGFHG4EcGkIGODTSaAHFmU5IBpCVzgDrQGPGRnFOGGkAxwKAI8UYxQ5+Y4pAGbp2oAUL3AoNKNy475p3XHSgCPbk0/dtYdcYxRj8KcMbAAPmHegBoYoQR0p2ACMDIzmmNg9Xz7AUsWM4yaAHYBPHA9KRt2Min4wenPb0oIweD+VADQO+MGkGC3AxTjSJgt0wcfnQBGc0/kKKRsYHHencdqABuRkUnYUY6UsgAb5TxQA0fezS9CeetGOaDn0oAQfSkxil7cikz7UAL3pepyaKTpQAuM008GnfQ0Y9TQAlGaDxTaAFzS02l7UAOFPBAX3qIGlBoAkzmk4pAT2peep6UAHUYpwOYyD1FMzzxTu2aAEYZYk0uO+KF5pxbbxigBmfam5pWNMoAcB3NNc8cUuaDQA1Tjmnk5+6ajIxQHIPFAEihSeSRSlP7tMJ45qSNijKVcHHIoAicswz6fpUWfzq1OQ+HGQ5PzVA/lbRsZy3cEUANX72M9RTOQxBp2DnLCmtgnjrQAhpKkIA25ORjtUbdeKAEJpDTgMim9KABexpST6UlFABSHpRR2oATpRQPc0UAWAMjkkUH5RncaQtjqMe9OG3g4HtmgBqORkNgfhTlkIcqeB70nVs8ZNJt9uc0AGQxP1o+8wC9KjPHX1qYFQCc8mgBHUg89qQde9PbBGc/hUfGelAACc0hPNBHpTghPNABSH9adtPOaTawFACDGMfrQOoxTioHGeaQKM4bgUALk460UjY3DAwKN3J44oEO59KRyNvy5z3pQwx7mmkYAAFAxoOOoqRTxkU0gZ96F6/yoAfnJ7CnE44zzSYzTTigB3IGM008jFGQKMA96AFUkDnke9Kxx2pTgr61Gre1ABkt6ZpynI6c0h46Uw54IoAlJ4FHfNNBJFP6UCGEkGgEn6U7pimg5Oe1AC+x60c0uRSUDEzzTg2KbxmigBd2fzpQab19KOM9zQAp657Ui5JpQPQfhS9D0oAUrScilzxRQAn4UlBpKAHL19qk6jjkDvUa0/OOO1ABmkzRR2oAUZHQ04E+vFMX0p2KAHZU98GkUnNNIpVxmgBxPcikB5zSDkd6VGHOaAHY3juDSRgjK5GTxSlsrTRjHJxQA+MIFZZVYMOhFNbHtS7uMU3CZ54oAOPWjAJzzSdD1607BC0AIWJbn86ctJjim80AT87cDkehqIkdMUFipHNKcnigBhB7GkH+1T8Cmsp60AIcetLnaM/rTcA0vTv+FAAq7gTSqOeKTOBgd6cGGc0AAUmXD5AHWhME4peWY+9GPzoAXAVhzxTCfmIAJpJA2BikwwIJ4oAUK/oBTmUdh+NJye9P6IM0ARksO+fapVIaM84I7UgIxkDNNO7kmgA7cHmhSM89cUD5hnpQw6HvQAn40p9KMZNKFwaAE6U4H1xTQOaMEGgBcEDNGcikooAQ5JoApO9KOtACA4NOHNNxSjigBSMUIpbIGPpSdc0Z2txQAhbPFNxin8GgjjmgBtFFFABRS4ooAUHFSsQYQQeRUYIxzSE4A9zQA4A4zilbAxzSEsR1JpufWgB3Q0p5GaaOaQkjigAJzTaWk70AISc0oJPSkOD9aXBWgBDnNJgU5ecikK8D3oARTng0o+VuKFU7vmGKViCOlADs4hye5qPgg9qerKBhuRTvL43LyKAIWIA96i71OoRZgJQdhHOKicDcdv3e1ACKwU8jPtQV464pOlL1AoAZyDgdKGHBNHel60ANAzzSdDThkjAFBHrwaAGZ5pQaftBXOaZjjrQIQrRUn8PaigCQEscNSvk9MU3gDGeRR8h5AoGIPU07IJ4pu4D2+lHyigBxwU5/CmrkCnDH8XI9KYcjOfwoAeMEcsc9qbtAOeppRwMnrSAZJJoABzT1OB3poGe9KeBQAu7NAODmm9sYpR6UAH8dKwwOlKPoPrSOSSKAGdOTQOnNKCMc0oH5UAHRhSkHAppFP2kDGc0AMzz0oHJ4HJoOfejoCR1FAEi470hfnpUfmc8dO9LywzmkA8Z/ClyOw5+lNB4wCaRSQeCfrTAe7ZB9KZjOKdlSuCmT65pvQcfjQAEdqAvNO7UgoAAMClzwfWl7UdOcUAITxSAjvR1HqaUqPyoATqcYo74FA96XHGeaAE/Gjt1oI49aQdelAhcdzSjjp0oyD2peT+PWgYmfWgkelHZqT6UALnijNJ9KXp1oADxQKBz1xQR6YoAUGnE55pgFLQA4UUgpaAHIKWm5x3ozQA6kwOtIDS4OKAHDGMGkIxmkxxmkKvnjj3oAUgEcNShwqkHv1FJww+br60zaM5FICTj3pQCfSo8HA5p2FHBJpgObGeKdjP1pgagNntQA8Lmjb7E0inb159KkBZh8pCigCMAE0hJJwacUIJ+bmmNnv1oAQmkDGijFAC8GnAA00CgHFAClQOlIOR16U7hqeiLg8gk0ARA4NO3c01gQeRS9aAFYfKCPWj5sZ60Dng5IoPXHNAACMcjmnH/AFSjOc5JFM5B5pxwMEkZ9KAGrkjG7p2pCcnmgKGOckUuMUAMxg1KMFcGmUgO00APA/SgnFIjfN1605hQA3JzmlNJn1oycUAGaSkINKBxQAlOAobHahTzQAEZpBzTwQvPWmEYoAOgppp1IDtNACgc4p8nzKDjkcVEeuQacWzjHGKADaDmm4xSj3pQM0AJSr70OoXG3PPrTc4B9aAHHrjFNJ6UrEnBz2ph4oAkz196TGaaMkZozQA9eKVuRTAaXdQAUhoDc0vXtQA3AP1ppLD6U/FBJxigBqsQaUnI6c5poHenr70AISxOaQMRxTiPSmHjmgB4Zcc0Kcc54PamKwDjPSlXYGIfp2IoAkmm89FjfGUHynFQ7ONxPNKcc1GHxQAhGDSA7aew4zUZI70CAkZpM4NJQ3agYuTnjinnLHLH8aiB5p+QV4FADlADEVC6kGnk89Ka7ZNACKaKQEg0UCJv4silOc8UuOnFIwyRSAMEnn8qdjPX+VClQ3zdP5U/5SDgZ5pgNGBx/OlA7GmnA56im7iD6r60AP4JPWjg9OKQMOuc5peM8UAIWyh7GkUk8n8KX60Y4G3mgYDnv0pRgr3oAOPSlCgdaBBj0Jo+hpBQevSgYZ596M47Un8WDQTQA4ZzTjn+I9PSowc0rdeCc0AKDk9MCkcY7cd6UHPfn1prdDk0hABjn+YpcYAxnPrSAZIANPPBPbBoGIuSDkc0uB0B4HWnLyO30pqDA5GOaAGk4+73oFKRgZo4xTEL2pB0pvene1AxRnFIcim5I6UuaBAD3NO3U3I6YoBoGLTs560zOByaUD3oAeeB60g/Cm5PSkLcUCJAF6bqaeCSppnXtTgQBQMOueaTkc0vOaXtQIQkbfegc+9GAetAO33oGGPpS0hYE8UADFAD/WikpT0oAB1pc0zcc8DNAbJ5FACk5oApcCgUAHSnAn8KTg96UCgBVPXLCkDercU3HtRgUAPJHajtTBxS5oAeMUvyk/MOKYDTxz3/AEoAb5Y/vcUgAHHWn4IHrSbQ3IFABTv4KFK4wQM0h6UAKCc8mkLDPKk0nzKc4zSO2fagBduRlelGccGkDFRx09Keg8zpjIoAaDjr3pV+mTT2QYyVO31FIOBx370AIRnngUbfQ0HrR2oACvqaAMc00n3o5oAXPNIT8wNHOKauRu4/CgBW59aAccD9aUHnGDzThznigBo680h605fvYNI3BpAIOaUjmmjrTunWmA3gNT93GKaRSDrQA8Dgse3ShcnqMUgYbcE8U4sOw4+tACgc89DUfQmpOoyOfpTSOelADfrRSnFB6daAAHnFBxyKQHimk0AOIxzTacG+XBFIeuKAEx60d6KXFACZpwpuKWgB/bB6UwphMk1ImO/SiTAYlenpQBG6gYx6c0Hbj3pCaSgABwMUfSkpc0CCk704DNA70DAUvamg/nTs5FABn0pCM0A9jQeDmgBMUuaTPegjPegB/vUbigOV+U9KeQCODQBAeaVCoOGBNOVc5FN280AO/CmBMkjv2oYkd6evHvQIb0+V+tRhdx56VJI29iSeTSE4G09RQBFjDYoxxzT8ZGT1oIGaBkW3OB0pwyDt7U/Hy5pDwARQAxuuMdKXbleOtHU5pw+tAiKinNxRQBLnjrxQAM5NKSCOtBHFIYMOM+tIDzkcU5ueB27UigcZoEBCsfQVGV2N6ipyRkgVGetMAC4YcjB/SnsMdKYSFPap8jgYzQMYVyvSmjg46U93AOB+NREjGaAHhs0p5ODnFRjmlPT3oEOOBmkNHUe9J3OaQx23dhgOnWmN945NKCD3/WkPyg+9ACqccmlzxkc+tNB7UqkDryaYDASO1OXJBLCjAyaUnjrx3oEIODmpA2OCPxqJjtOM8UE0AP3Y5FO835SSKiz60Ac/yoAeXHUCk4PehfoKcBzk0DEx29KUKKDTee1ADiuPpQAPTNNBPc09Qc4HGaBB8vQCjA703HrRmgBdvPsKaOc08rhR6UccndxQAzrScntUmPmyKRhtNADSDnjvRgDrT+BjmkK5JIoGHy9jQr84xSdCOaB6igB2RTWL5B607gUUARgndking5IwOKQjvTgccUAOA5HXmhsgc0h6rjrSyglgSRj2oAj7gipAeORxTQAe1OJHSkIKXFJxS5pjAjjrSdqQmkoAdSUZFJnmgBSfSgGkzSgnvQIdg0ozSA04GgY7caUY7GmUmKAJCMmjgd6apPenKwGQRQAKaRtp7UHGeKQikAjc/hRHlWzn86cADnNIMA89KYCknna31FKp4qIpz8hp+W70AOOO1GPypBzS52nnqKAGlG9KM8U4tkcdT1NM5IoAXGe+KVyDwDk9z600EDqM0oI9OaAEywIJ7U9SCee9J9aQ47UAObp0/GkZcDJpu4kY9KUnIxQAmCMHtTjhqaB6mlPHQnFAAeBTfpS9BzSZzyKAEPNT28ixA/IrZGCGqIAHr0pSExxQA4HbnHFJ1pqdeaeTzgUAIRzzTRTj0po5OKAEwMUm0j6UvTqacFAVgWOQemKAGhsEHjg0pb92EKjgk7u/0pvWloASiiigBaUZ7UmRSE0ASZHbn60gNMzxTlOeKAFOMmoyMGnmmnpQAh6AUmKWigAB7U8AEYHUU1SAc0pPzUAIVOaOhwad/OmkHNAAOtOxxim0E8UAJ04NL7UhORzRnIFADjtwOKiPBp5HpSEZoEIDyTnFITzxRtOadsGOTzQMhPJqTkikKmj6mgAwvAPJpr8nHpThj8ajB+bmgQ9cMp9aRT3NKSA3FI7ALxQAjNQ/3RTQc05jlRQMjo70dKKBDjz+FFPjCMec0UAJxnIpM0o/SlZRjINACA4B9aTPqTQpGKU9OaBiY9GoHHvS7do6GjHfFACEg9c04EY43HNCjvxgUnqQKAFJ9FFIODnv60Ak+lHFAEgICnODnv3prAHtSADPNLjigBBijOcjFIKUUAORQOTTXC9+9LuwOtIctx2oAb34OadSZC9DzRnigBxx2pp5U0uelHYjHWgBGB2gigKT2p2TtAoyccfhmgBCOOB9aUfhTQTnpS/xDOaAHIuG5/KnZGQSM5OaUnAPr60hI+lIBpHPNGKXdnmhT2pgJ0604knjFIc8+hpcetACE8cCm07+dLgY70ANHvzRx6U4rzTTkdKAFyOgFKpHOaaCSaOO1ADzgnikx70wnPApQccGgAOMY60gyKUNzzTgR1oAbgZ60/H0pAMiigBDj1pTRjjrRg+ooAUAnjP40NtHA596MetIaAF69KQ+9GemKTNAC5xRyaAaKADBHU0Y9qO1KOnWgBuPejBpRnPQGncHsBQAijP0pcZGRijntTcUAOpw6U0cdacCKAHYzS7WX0pBg96XpQA08mlxS5FOQKTk9B1oAiK9waAxPWnNlWwfwox6jFAAOadz+dM707JxmgAxikOaUP2xTiM9KAIyO/ekYk9TmnGkNACZHalBx+NNI5pM0AOLYoDd6aeRSLxQBIeelOA4560jDDYppODzQA9gCM0m39KUHvmkBINACHpSA8044I4poHPSgB4+ZTzTKemQSe1G5c9KAEUkDBAwaGGOnSlyG9qaOGwehoAaTt5pwYkZoA+YqelIAUyvagCQnJo2gDOKjzg0/tg9DQA0jnNOJO3k8t1o9u1ByaAGHNJTju74pF+9QAYoIoJyaMYoAbS0Gj6UAJjmlGRRxSE5NADxzTTSZx9acDnrQAzvRmnEU0igAGScU4EKSDzTV607bxQAA0pPNM7UuaAA0lKaQ0AJS/yoU44IzR3oATjueKl2jAKcD3pqJuBJNLvI49KAGE7jgAgml2MT1/A09chwRimyE5wee9ICKRsZzUXBPepWAMfXnPSiTaxyABx0oAauB04oZMDJI5pOhpScnmmAqpuQnOCtRE5XFSk46daYFyT9KAGLx1p/VabigHigBp6UDnilIpo9aBEqkAe9FNC5opDH5yMCkwMdcGlwM+lGMj5h+NMBABnIzS9zS55FJjHWgBSwIAJ4FGcdaABjpQfegAz27Uq9eT07Cm9eKXGOgpAJzyMYoHXFKeDSDryaYDvSlA703PPFKCaBAQc0Y+Wlz60h5Bx0oGNz1zShsDnvR24pvX60ALjnNGeaB6UA/jQAdTmlPf3pSABxSUAA9OaUZpAR64NBI7UAGDnIpOfSnAUuBQIFOeppyuoIB6ZpgGM0vUjNAxWIJ4oPoaBnJxTsHNADBtzk5pd2FzQc85oYcHigADYPHSl347UzcueT1pwI67aAAP2AoPTNO3Y6YpA27IPFADM4OMUoDddtA6047sZFADMYJOODTlBeTao5pnI+h7UqnByKAFwe9PVlA5Wk2mgE+lACjGRxQeGIpN4z1pcg96AEzS8UD2pAaAFz+VKelJ3pWPNADc4xmk601jz0pQaAFxRRR170AKM0ufamgAdDTscUAJ07U4U3b3Bp1ABSUpPFID70AGR+NB7GjqOeaU9gOKAEGacHx1pPej60APBB705Tj3qHHPFODEd6AJJDuwc80mcj6UBs0HH0oAQUA8Yoz60lAAT60bsHrSGgjigBxYGlHPeo6O9AD2XNMORTixxzRwTycUAIOnFJ068U/C+tLtXGAaAF+9yKChJPFNAwOtLvdRwaAGkYp3emb8nmnKeaACgCk74pR60ADMe+cdqANzFP4h2pwPXj6UMAOcc9z60ANA9KXOeDQfUUmKAHH06+9NPSlAJ+lIe9ADaUE0HrSGgB4b3oIzTAak2tjI79qABE3Zz2pinJIPHvT03gcZpScDpkd6AIwMHgZpaXgYx0oPPTrQA3vgnApD+lOABDZ4wKaBxQAlApT096SgAxk88Uu7HBH0NHNIeaAHZwKMd6Qc05fvYoATHcUowTg0496jcY5FAA4w1JnmlLbgKT1FACdqTtS0lABmnHHFNxSigB9Axuy3SkBz1pQfl7UAKzKBlTUTHcc5pXpo7UAMbNGSOD0qTGeBTSMHB5xQAwgnoKfnI5WggjmjJ20CI2PzcdKcD6daYR1py9KBjSpFA6U9h8vNRmgApuKcabQBJE2GopinmigCYKpHzNj0pGI7E8UdBzik6ds0AGM80DIPrRkkYoXNIBTycg0EnBPWkKndkGlBB6cGmIcqrjJIFBGO9NzzjFJyT1pDFNAx6c0hPzcUdWpiHfTpSA4oY4PFIC2cUDHhcgnt6GkAPb8qOfXpSgn0oAAMAk00jHanEZ6UE4PHSgBPekAxT9uRnIpCORjoPWkA0dfekYr75p2CT9fSm4PqKYhuQegp5x6YpoBHel7fdoAdngU7IyMj/69Mz6UHnac0AOIwMikBPWlHQ5oB9qAHc5zmnfiaZQD70DH5JHI5pM4PrmkwT0ppzQAE80oYsOaUA49aQA78UAJ3peQPUU7oenPvTWoAQ57Gn5O3Bpob1GaTzD3pABP1poJ4pxxmjCnvTAdnjB5pN+T04pCO2aaFw3WgB+MHI4pwbPBApmePWg/Q0CHflQTzTMmjBPNAyXPGO5ptNByacAaAEakpxppFACijtQKXGfagBMe9O/h60wg9aTJoAeWNLmo+tOGaAHUcelFFAhM0oIoxxTe9Ax+aODTM04H1oAftycgcUY45oBx0pe1ACEDtSHijNFAC9aSj6UlAC0uTSZ5pwoAafage9KRzimk0AKfam455oz70mT65oAcCR3pwORzUYpaAH/AI0uKYODUinIoAbt4zTdpz1qXmkP1oAQkAg0rZPzHGD0xSAbs4xSD60AO/SlGMc0gJYcnkdKTI70ABHvSc9KCce5pQVK/OOfUUAKrFUKjoetAwVpD05pUOO1ACYpGFPzgihTluaAGonG79KcWB74/pTWGCRSZ56UAPZi2BuyP5UBgDxyO4qIH5vSpA2McZoAcUIIGRsbke1IBtfls4oUgnpSOKAB8bs03gil4K470mMUAFJ0paO1ACdT6Unel2k80oXJweD70ANpVOOKMUHpQA8mgjcMimjAPJzS5x0oAZ0OKKHHOcU3NACmkozSZyetAD8cZpDx0pynjFBHNAApwc0oIAwRTM4pykZG4ZoAWRcjimqtSFtzHIxxUZGKQAwwKYTTuSMdaQj0pgR8048gelIaUfdIoACvGaZT8sy47CmEcUAKfu0xvu0N8ooP3aAEwAMU0UvWk4FAB0opDzRQIlGc+vrT1yGxxigdaQ560gF4xzQflHQ80cHvSlgV6UAN3AjJpQAVzTcjAz/KnrjGDQAhHekPT2pCee9KWOOOlABgY3ZpB0wKaMdCacPlHrQMXA/GkUHOTSZyR7VIWBoAABnNGBnrSdTSimAvbimHrk08nGQBQxBHA5oAZk05WzweKF5pHz3/AApCHYGe1IUz0pACOtPVsdRQA0IQc9qUj3FP3g+tJimAzFJkDFPyB1FRswzQAqnNGMGkWhiSfu0DHA59KXgimrxyKdknr6UAKMY603PPWkGM8c04Rg85FACg46HP1pFlGeRzTW+VRg01+tICQsDSkDHNRBuOlPUg9aYh3pSEGlHLA4pSpPWkAzoaXgc0Yx1o3cgYpgByeOKTBDDNBbAxgULmgYmeTinHp1pMAfjS0AN2mjDDrTs0rHgZoAjOc8U8MO9NJ5o696QEmVz1oxnpUY4PTinBqYCgEGpOO1MDZpaBAcHimlR2zTqTrQA3FLk4oIFLQAmaXPFFGKBi8lc03BzTshV5zz0pDnHIxQAmKOaXNJQADINOB45opKBC0UhpMkUAPBpWJOMLgVGCaduI47UADCkANKCKKAAMRyeaXINNNNwaBjiB60hHNJk0GgBVHNOxzSClB5oAKcPajjGabuoAduP4U4YNMBpc44FADiMd6Oo6UgP948U4MM49aQDCDSE9zT256nkVEcigB1KDwabjmnYGOtMAJ4p6dM00qcZ7UBsDFACuabk0H1ptADic0EjFNzS5oACFAyCc+lKM0g5+lBBFAEmcDIp4weoqKNsdan64zSAhZSMmkBqUjGQaiIx0pgFHvSNxTlxjrQAnOKCd49CP1pDwaAcc0AL25ppFBPHNGc0AJxTgabQTQA8gHmmOMGnKac655oAhxRgcYpWBFJmgAIwaXNGaCKAENCmgZpSOOtAiQH0pDhsk1ECRTwDJnHYUDAtjgU00wHmnEHHNADTSU6mmgAFB60g607tmgBrcimZ5xTzTWxuyKAEIppFOLc59aMHrQAyig8UUCLHBoIzxSd84p24H60gEOQabk0ppDQMBnHBpyknrSDpSqcCmAjUD1peMjigjB5yMUgGcFqcBjkUgU5zjinEc9aYCbcnpxSkDNPUg/eJ/ChlJUZYH0pAMGM0o96Mc804EYpgIOe3NKWB7CkHUYpSuee9IBORg4oOCBSjjvmjcPSgQzPODTgOeRSMD97tQWJGM0xjmOQAKcvJ7VCxP1p8f86ALGAy8AnvVWZcZyMDtVkMEBwPbNRldxPy8d80AQAEKDSnNTFVBKkfNUTA5pAHpQSMetJyaAhPtTAUN7CjfjsKTbn8KTn1oESEHZk4IpjfN1wKVSfwoNAxu0juKcvTHFHbpSqqlT82D6UCHK3+zS7qjGe5pQexoGOzRjP1pDSqfWgBjZzxSZIqQYDgjn60MMnNAEYJp1AXFHQ0AA5INB64NAbAppOWzSAeRgDFCkZpp6CgMeOKAJd2Rzg0EDAPFMyOnSjknGaAA9QBRntQwwF+tB60wFyKCRSDrS4BoAAe1LTSMHikBNAD8c0U3PqaUUAOOCoz1FIeTS87aaPagB2PagYpu7HWnZBoAdjvTT1pwpNvNIBKCM0uKXBApgRilPIpTSY9KAE70A0c0YoAdx2oPvTOhpQfWgBQKRgMcU8AHFNZDjrQA0HtThSAUUAPzgHFNoB4NFAC5oyaSjigBygk+1Lk4wO1NAOcU/pxQA0/rSd6DRQAGnc02nqOM0AKScYqM9aefWmd6AEJ4oHTFBODyOKOvNABS/wAqBT0A3qD0NABxSH3oI+cn0pQM80gEJFSRyHIBPy1GRihaYFtlBNROnzCnwt8uCaUgYz1oAruOTikxxUjdTio8nHNADeCDQOKQdaXPagBST6U3GaCODSjGBmgAx70mMU6mNxQAoNShsDAqE/d4oBxQA9uaYRTlPPtSEc8UgExRjijrR1GKYCZpfamng0ooAQjFKpxmnMOBTBQAbec1Ky5UUgxtxTlBB68UARFcU1hVgr8vHNRYzQBCeD1pDUzR96iYYJFACLwaCO9KF3Cm4weaADOaeMbSMUzOORRz1FADWFFKfaigRKePrQenvQWznimlqBhQRR0HpQemQaAEOccGnopJ5qPNSKSADQA5hgZqM8nnJpxOabSAcGyMc4pCRxj1pvzA4A5pQPXrQA48mlBx16UhBHIHFKAWxxQApXvSYHGDmnnBXrTcL2NACDilzj0pNwz1FJnnpTACcmgZwDRnJ6UcigBSOpU/hQRjtQB68GlwccNQAwjn1pQSp46UpHtS/L2pAOL7+OhqUANypIPf3qs2e1PWTtnBxQA+V843CoyOfb1pwOSc801/lGCeKAEDUvykdcEdqYODmgjnIoAcy/3Gz7UgI/Oj2zRzmmAcUH60u3nmkIABNIBqkjPNO3AjnrTO/FL/ADpgOJwaTPfrQBuPXFLjaKAEzQM57UpGOhpAD+NADh6UvfFIOvNLQAvQc0HrwM0dRS9FFIBoUHk0oC4IxzQRSKRu5oARhwKbj3px6c0ymA4daM4PFJnmlFAC545pQR2pCKWgAOegoww4xQOtKCfrQAmSOtBNOOMfTvR1HAyaAGY4pB14p7AkcDgUg6jHagBNx70bsUpOTTSM0ALmgHFJRmgB4enbiRUXWlHPegCTJA5FG/sRTcn60maAHc0A8+1NzRmgBxNJ9KTOaSgB1IRSAmloABkU4Mc80gxRjNADiRjimkUnQ0uaAE5oAPWnDmigBM0DrTWDEgKM49Kcp4oAcD3pc5pvXil6UAIaO1IQSM9qKADPzCnE4z6CowfmqTqTQAMcjik9MmjpxSdOlACkk4BoWk780ooAXvTto9ab2pQaAHbgFx37UqjsaaB3p68AjqTQAx6VBmlkABwOtNDbeOtAEmR0zinb8MFBqAk7qUHmgCeQgEVC/X2p4YHhqHVhkADFAEVHQc0mGB5FBfdxjmgA+lLmkHFB+9QAuaRhmlNAORQA09KYeDUnFMx83PSgBQeKch60xsZyOlKOOc0AOYbajzg9amwGUdqhZcE0ALwaTJBoGB3peDQApJIpgJp4pD7CgBAxzzUgcjtmmdulAagCaNsnaeM0hXDYJpoPepDKGIYdRQBC2R8pPHaomU5yDU4ceb5jKGXuKjkeIg7eCTQBFzSc9acCDxSe1ACYyOKQEjinYpDQAYooBzRQBISM0hGeelA9e/ejhhg54oADnpQFAoOc4zTvw4pANyMUtIRk/WhiRwMUAHekPSlOAPlOacq7lx0pgNHI4p+1u4po+XmnrKScUhCZ570qsVJOcChWyTkA0rgFcY5FAxCcj2phI6CnKnGSaTBzgdKAGE9qUUc9/WlAxQAopMnNHY0mCelMBwbcRmnZAOMVGMj1pwAHJpALz6UYxk8UuR6UYU0AIrAE9aUKCPemsCOhoVsD60ALkqcVIxBTnmmg+3FJnnBoAXGV4HFR5qUsOw4pGUY96AGAcUo+lOA54pvAYnFMBwx1pW2+WMcnvTM+goB9gKAD5TTT7Uvf2pwAPPSkAw8UoIbgU4xj1zRgAf1oAQnNApP4qO/NADutKCBTTwaTPNAEnXpSGm8kUc0AGecU9RnmmEDbkdaENMBX9KYRUm7PBpu3J4NADAKdS4NA5NABk8YoJ96OhpOpoAUHPWgn0pV2ANvBPHGPWm42igB275cYoDY6daTNLjIpAODY4yfelAA5FRMCBSKSBQBKQKbgYpuaM0wEJopMGlHWgAoFHegigBcmjNIBRg5oAcBuo5HWmZIp4agBxAxnpTcU772OlIRzSAb0pQaDRTAdjiigcCkZs/WgQtJg0mTRmgYoOKXOSCKTNFAC52Nkd+KAMUnWlFACg4ozkUHpSc9qACgj5eKCMfjR1oAaMg08mkxSGgBc0UmaVec0AJS5oPFNHWgCSgU0GnfSgB69acDjBpi04GgAJy2aVlzzimlsDoM0pJ9+aAGY5o3c8UuzgkHINN6dOtAEgJ7804EN1yKi+7zS7uc0gHOCOaiYc5qUnNRmgAHPWjHNIOtOJ4pgIeKQc9KDSE46UAOIOM0h4696Fbgj1pBzkHr2oAMcUnSlzkY7imk8UATdAD2NNde4qNWO3bT95HFAEeMGnrgDtTW5poNIB5JzSBiKVuQDUYODTAduyaNw70hIHamsfagCZXp6k9PWq6nmpgQw69KQCEMhKkZBpjp8m7GDU5G5cA/MORUMTF2YOaYEQ5pPxp8gCtx0puAaAEzzRntSUY4zQAd6KUjiigB5zTckHjinHmmkDrSAcCSTmnbSO/FJxQxoELxuzSYxnHekyoHNG9e1ACqv8SnB9KdvBTBGG9RUecnOfyo4zzQMTJzgmhTzmnYFJigBynnipDyOtQcjpShmHvTAk28HmlIw2R2qPfk807cKQCkcdaUYB60wmlIY0AOZEz1NM3Y4HIxTm5H6c0gwWFACZ6ZpxPSpGCbQCMH1zUTZzjj60CHLil60wUvA70DHNg1GR0FO3fLgUnOV9xQAtB5HvR7c0HI5xxTAUHnnrQWwfmFBXnJPFNYhmPWgBwfHSkzk+/rTOhoBOaAJBwTSHmkyTS4PekAmfanqPem9O1G7b9KBD8c0E4GO1InQljTeT1oGIRSEnPJpxHNGPloANxBxxQp5OaaxBFKO9AD88UhxjjrTgAetJhccZoAZ9acMdqaTikzzzTAcw5pQDigZ7DinkFF45B70gGjBB9aQcUHnoOBR3oAQgdqBx3oPXikyc9KBCt1zQeTikz3pSwJ4GKAExTw2BTOCaXBJ4pjFPoBSY70hbK9KX264oAMUYzR2pPWgBcUnBoB5oOQcYoAMUU6jtQAlLj1ptG6gAIppyBxTwc9KQjnmgQ0Ning1GR81GSDSAk60YwaaDTic0xjh0oIFAoNADTSClIpCcUgCnDpSdaKYC96M0e9KKAFzxSDg0n0pR1oEOwDnNNxg04U00DDNNNBzRQAdaeg65poHPWnL900AI1IKCaSgBwpRSClJoAUHmgE0mCKM/rQArEmpVYMqt/dHIqDOCOKcWweBwaQDgcKcUnY0gIGR2oJzyKAEPvQOaXOeDSZxwaAHA44oI4puRShh60wG4waXvQSMc0maAFNJkUdqTpQAGmnOcinU3oeaAHdee9IelC8HBpzUANHy0hNOb7oNRnrSAdmkHtS03vTAepPQ9KZIMHijNBO5aAE6ik70mcH2oz3xQIQHBp6t70049KBjPSgZMkpVgeuOlOkZcb1AGRUORnpStIANppAI+T2pgOOKdkscUpXDDHIpgMJxTtw24pp4YnsKM8HigB2M8g0UgPpRSAeOvIpMc0vUU3GHx1oEOA9KDmg+1BpgIeetNIFKaMZGaQwVeM0u2lHApp60wFNJmngjjNKACcCgBlIc+nFSkDOCKaBz0oAbtxQQSeBUoIJxgU45Q4xSAhCtnpT1ODinA57UjA44oAGGc8gU3bk5yKU4/ipCm3t+VADcMxx6UoUj1zTjnIwME0wvzhzjtTAcS3GF/Cmmk78GgHikAo61Io+XJHA70zqRTgdoAFAB+NKCMYPT2oPByRSZHagAZeoBzTQT3p2abnK9KADAoA/EUYo5FAEq7Rz+VNLeopqmnZ4PHNAAvPBOKSQAAHBIPekY5xinclNvagAA4wDxSgUijFAPNAC4zxTTwvFPGDSYAOe1MCPsaUHnilxSgZoAA1LuAFIoxmmkUAITnvSfWkApaAHrjHFKeQMVGDinZ4pALntQOlNPWl7cUALSH2IozRkGmIaSelLSkcUnekMAM96UgetAHNOApgNwBSe9PC9eKbt/KgBKOPWlxikNACg85FByTmk6UuaAHA0ZFMBp3PpQANUeDT9ppccUCGYIpQaKO1AwNNNL3oFACU7+lJRSAeDTuPWmA0uc0wFpPwpc0maADHpS9aBRSAKKKOlACilxSUvamAnSnYz3pMUooAawxS7R60HmkzQADHPFJ0FFHU0AJ1opcUYoAUUoHFA60vSgAxxSGnN0puPakAfrQeFwaMU1iTzQA5cFcGkIINA6UH1NMBACTTzz1pEBIJHOBSMSAD60AHsKQr3FA9aGIxQAvp6091wM/pUSn5uamdscjmgCIEng0p6YoIyNwNKMfUGkAzPODQeeRQwHWjPFMBcDbSKcmjtSdDmgAZj+FJweaDyKZmgBxNB5puaWgBDQpwaDQR6UANYfNQpyacORz1puNpoACKQdaf1pnSgBw69acSFOcZpoowDQA/luVFCkKDn0pAewpCcDHbtQAzGRTQCOvapOVYUEckGgCM0UGigCcH2pO9Apc9eKAEyc8iil4OaQikAduaXgjABph6cUqnaeaYD8EjjkjrSNjrjk05WKtujODTSCW5OaAEyCOKQHDZ7Uu33AzShAcfNxQAucmkyc0MFHAY0DGaQAM5pzybiM9hQSDxmm45yKAF75zTmOBwevb0pmKcoHtTAOhAJ4oU7TycihgMUnzDA4xQBIxzt44qORFY5HenE/KOc4ppJzSAj5FKM04nNJnBxigBQSasRBDE5bl/4RUDAAj6U4EcECmAGjjtSHmjkDg0gFXrzSE8BaO9JjBoAXHSg+lL+FNNAACRT+1NGc5IyKlxwOeD7UARNTlBpJVC45pB070wJGBpoyKOvelyelIBF54pzAdqOMGmk+lABgjpQMg5FGcClBxQApPGTTTzg048delMbqKAG4p2KTNGeKYDgqnvzTdpHNA5o5FIAHvTtqnvTOtKMUwF2DPWgrS5FODUAR4NJUhPFNxQAUc0uPWlGBQA0FjQSe4p+cU4EdSM0AVyaXtT3CnpTe1ACUvWjJxQfegAwBQGI60hpBmgB+4Gl/Gmbefej5qAF5zSc0ob1p2AaAGEUKKXBH0oFACYop2OKTFACCkPFOpDQAm6lzTO9PWkA4U6m8U5aAE70tLk0lMBKcKSjNAC0ZpKKAFNIaSg0AGKVRwaQGnLQAAUdqMc8UtABSk9KSigBSNzgUh4bGeaXnHGOaTpyaAFJOKj4NOYnHWk2+/egAwaVenPNLjbz1BFCEMuB96gBexCjH0qMq2KcGw3IokUgkZ60ANUHHNGBRjjFKMUAJtHIoT+6T9KRiA1IeeVoAU5FIPlOexp4+deaTH8NADfWhelHIOMUuKQCZooNJTAXpxTHHenkcZpGO4dKAIlNP603bg0vSgBc9qbgtzTs96Q4ByKAEztPNPYBlBph+bFKMYxQA36UHmlIIooATpzSg80lGcdaAHjBOKCmTgdKRTg5qSMjd1oAY3zKOxFMZiwHHNPmBWTK9DTAefegBQBjmijrRQA5T70hPNNoxkZPFAAD2xTjwOajb0FKAcAdaAJAuV64ppGe1Lg/jTec80gH8AcUdiabyRinqMCgAwT7UuAO+RSde9J3oAU8jimgHNOXijI3UAABzTsY5z1pMj1pQKYDT1OKUA9RStjbSKKAFJA6gU3IPYgUjDDU4CgBMEn0FLg47fWnBOBgEinhAOv5UAQnjpQegOKfIg7UmP3dIB0qbGUjlSODTAMPilUZj56inOoyCGHSgBooAPpxRyenNIMjrTAkUA9BzQyfnQAu0kttb0x1o/HmkA0AbetNp6qM0jrhtoBpgLHgkjPBFSRuU6EVGRtpFOaAHMdxp2wbfemnjvQjDdg0AK6FWAyKGGDxSSvufI7UgbNIB2CR1qPBFOyM0MPSmAlOpuaUcHNIBSTu9qZ3p7EHvTMe/FAASKCQegpcHrigGmAgHNKc5xSE80E0ABFH6UmaCaAHBSaCppoY5oznvQAuDRmlBooAM0oOab3pcUAGfelGRSYpcUgG7vmIop2KaKADNFIaVc0wDbTSCvSpM9qOO9ADFNL9KXAzSYINAAVJpFJB5p2TRmgBCc0CmkU4UAOpD0pR160GgBtBp2KMUAMIpoOOtSEU0jmgBw5paaKdnPFACZpc0hFJjmgBw5paYtSCgBKQmlNNYUAGaQk0dqKABeTTwaYop46UAOFL1po4ozQAueKTNDdRSEYFAATxxQCT1pR6UdqAGtnNKgO4n8KOM0dWxnjNACNkEjvUmwJAD0bPFIEUykZ4FOcfMB2oAaiFmJYgU9jujB4yKd8qxkMATjj3qJdpzt+X2pANII600kY4pzKc4NIR8tMBuM0KKBRmgA3YpzEnFR5p6nigAJJGe4pgJzTjwfrTSMc0AOzSUdaB70ABNNH3qU0g/pQApHFMzkYp4OVFMZcGgBFPrRnFBGOaXrQAbSelIePrS/Sg4IwKAHMQyg9xTc0RnBwaG68UAJSMSRS0pGBQA0E4qWPH41EDzipE4NAEu3fnNRFME561M3y/MO9ROOQ2eDSAaMce9FAUhv5UUwE7Uhpc4o4x1pAKFx1HNBGGHJpoYds0ocGgQ7PpSdaTdzxTgDigYcDtS/Sk70pIzwaAG45zThRmkBPYUwCg53dKBk9qXJzSAQn8KMjPNKV4yaUoTgmgBCc96d70gj9O9O8p8ZXpTAjfrTlYBetIQ2QDSBeT7UgJRKSuBShzjBFRgD0p2fTNADnKkcimK2RgClKkjk0IMDOKAEYhGAND4z8oqOTmTPODTtoI4Y9OlACqck9uORTzGykZ59KjHJyetSCQqfX69qAJI9pyDjHrTXyp9vX1pVUjGwgOOaHBZM7uR1pgRZ+alZvxpMZyQeaQEjgY5pAGaVTzTcn2oVsHmgB+aQnvSGlAoAb160tO28Zo2ZoABjtQcjGaQoRSA+tAC5GeKDkigEE+lLzjA4pgIOevWgLmkIOOtAJFIB+No5NNzijdmkIz3pgBOaD7U05HelXOeKAFxS4qRF3DBprIVNAEZXFApx96AKQB2pM0oyKD05piAHNLxTM4NLmkMdS96aOtO6c0wDtTR1pwoNADTQCc8U4j1pMUAOIPem0uT3NJ70AKDk07bkcGm0ZpAKRgU3HNODA9aXjHFMCMjmlAGelLRQAHHakzS0hoAAcUvWm4pe1AAabTqaaAAmjNIelA5oAeM44pe+cVHyD1pwNADsUClHTmlAIpAIRnFITinYxzSECgBoxml4oIxSGgAqQD5ajqQdKYDTSGlPWhh8woAM8/ShhRSHNACg0hPNHakNABQaDxQPpQBJEwXDYyRTwScngUxQCflOCB0NODEtgjGaQCngFgKaFBXIpzABuPu9xQRhsDoaAI1+Y89aMhQy+9LKu35hgUicnhQTQBHSGpGA6j8qjINMBpFPHTNGN1NU4JFAEnBjyKQcrzQnA2g8GkwR+FADM4OKcx70kg700E9DQA488ikGaVeCaKAE704oOmaZ3pxPA9RQAw8gim/Wn9ycUw9aAF96cCCKZ0pQcUAI3FPjYBuaQ8rn0pu7DigCSQDfkU0mhs00fexQAUqnmkPSkU8mgCyrDbg0m4OpU49qhBI70vagB6r8vzNzRTSO+OtFABkk8ikwT2p2D1PSlFIQzGKbz2p5oHpQA0e4pRmn4B5oxxxQMAfQUc5zwaOtGKYBtz1oA2ml5PFOxxzQA3txRnv3pTgcZFN+lIB45wKcBximgdM5p27BJJ+lACgf/WqZI3kIEYJPoKYkijBwM59aV5As5XkemKAIWB3gMMYqQxgMcc96VFT7SqSuQp6tTQTvKhsgHG72oAb83pQKUj94FDD603oxGc470wHMSQBikQ7HBYdDnI7U0kE4BqUBQOWzQAy5DGVmYYzzjGKj7U6V8gA5pisKQC42gN3pcbSM8+tIScgGlJPoDQA9mw2I/TmhSmM87u9NPqpBphJLelAEgUB8ryPSmOAG6cUhYqwPpT2wwDDpQBHxn0oHWhgc0owOtACrTsevFNGc8U7H40CAZY4pRkGgCl6imAFs8UnFGMnApCrCgYbfpSfj+FL8wpB15oAXtTSOakcY6UwA0gExxSEHNPwccUg3DqKYDT0NCj86U9cmlApADEg8mlD45pDknmk4oAcXU9qQEHpTOOtAoAkA5pcLUe5gaUEE9aYAV9KOnanYHrQQM0AH4UZ4xTgKXbxQAwUFjilIpD0oAXcaKbmloAWjHFJml3c0AGOaTn0pwPPFHNIBo4pQ3qKKSmA7vRnmm80mT3pASU09aVWHSlYCmAyiijGaADrTcGnGk70AJ9RSqPwpSeKMUAGMim7fSndKWkIaD2qTPyjimYz9aXkAe9Ax+aaetHYUmaYC4pCKCfSjOaADHelBxR2ox60AKDzS0w5oBNAC+uKO1KKQ0AA6UYzxS9qO1ADGPGKeBkDikC5bJ9alGw8gkUgGBMsAaeW2AAcmh8bhs60ksbIQDjOM8UAPiYOxDd/Wl2/L0IwcVByy8dqeZdyjqMcUAST/ONqr261V5UZJwRVtCSCzHgVBdR5QMPWgBjncevNN/nTFYipgARmgCMjjg0nsacQV69KMBhlTTAQHgGlLGmEGkGcUASfWmNwadnig4IpAN7ZoNGPeimAg60Dg0UmaAH4yOKQsuzGOaUdOKZjJoATjFHWkb5WpSCAD69KAFU8EetMYc/SnYGaUDdnNACA5FITyOaTOOKDgigBzcnim4pymkNAAOtOPamindRQA/k9KKIyaKAF5xzSEZ9BQCMZzSHGfWgQAUhGKcBnmg5zQMAOKO+KAaMHrQAoFL9KF6Uue2KQDaX2pwHFKcHjPNMCJs5zjigGnN6mk2kjpSAAx/D0pxOenSmYPcUqnsR2oAekjR7uBhhg5FIUDKMde1DNuxgDjilViF60AOjKn74JIpxXLDHH1qJztkyCacJc54z9aYClee3XrSbcscEdKNzn6UMXUEbeaABYyOcZp2MDGKYC/G7IpSecEmgBrjKjHaowM8mpWzg1CRz1oAewyM+nagHG0rxSFsOCKfjDcYoAXCsMjjnpUZyCTipnH7v3qHJBBIyBSATk8mnglUwRn0HpSFjnI454pd2W3Nyc80AMZTnrzTcYPNPb3701uuKAHc4yKcp560wcD3pVIzTAmUcGnRpuyKajVNCQj8kj3oAiIC0md1TMuSc9M01ogO9AEYGaNmTT8ACjeqqaAIMEE88UofnpSO4PFIOtIB5OfaimHr0pc9qYARSAUHnqaMkdKQD93GKaRzSA5pc0AJjml20o60cZpgMIxSYqXjGKaV9KAEHHWl3gUntSEUAPDDtTwwxioQKUMRQBJuBNNNAxS0gGY5p2KcBnil6dKYDADQUNSqeMEU1sHoaAG4KnmnlhgYBFNB4608KMetAEZ56Uzv1qTjkEUzvQAfjSHNGPUUo9+aAGk0oJp+AOcUwigBwNLtJ6VHThmgB1N6mnZptAC4ozS9abyKAHHpTQe1FLjNACkEDPalL8AHtSFj0NIwoAcQaQUA8DPSnDAFACYxzRQ33aRTxQAoFOGGpM8GhcAUAAHNBHNL1opAFIaUd6U4xTAZ2p2KAKO4FAABT0Qu4VBlj2o29iaOhHPToRQAu0rgt17ChyTyxyab1BLEkimlvWgBVUhuOhppBGFPelB5wGI+tIcYwW6GgCWAHzVDHA9D3pZMFXX0PNNeRZBvLYlXpjuKTcHLHue1AFbb82KlU4XnpRKuxsimq3PsaAEY9qaBg07jPB4prHJpAJ65oAypPpSM2QPalB+WgB5GzB60hxn2NNz2p6LkHPagCIAg4NKafLjYCPxqMH5setMBc0h4NHtQFJFAAGxR1UmkwRTo+Dg9DQAw4am7mPGelOOFOKa3rQAA04HmmUooAQ8NR1p2M02gAB7U800jIpw+6MigBRSjrikHWl6GgCVRg0UitRQAwAEUpIA461GDinHkUgHRtg809gm8YYkYqLPtihj84xz70wHAjPPTNSHBztHAqMdadvIUrgetADhwKCRnpS4IVWPem59uKAHHPTpQMYIOAfWjae386RsAc9e1IBpzjrTlzggGmk/Jx+dKMgDvigA5JOKUo4A3A7T0p3AJPPNHzDJySKYDBuUgg8elPVgc7UAOep7VF9On8qcuF5PIPUUgHyqByp/Go16+tSfIy4FIiqYyS+GBxg+lAAuM47CkZyW9KHI3dOPX1prDnimBJscrnORTXySMihHPSkZjk4zQA/5SOuKhK4frUowVyPxFRt1oAGxge1OV/nLetREZ5xTlGeKQEpY9jUZJAqRHK8AdKdKVAKoPqTQBAUZSD2PIpdzYHpTMnOCTxS4H96gBTnjNNPBpR0ozzQAnGeTSgr1pSRgcUADHvTAlTBqUDmo4lJOFFSpzwMmgBzOzKFOMLwOKj24GSae/A561XkY9qAFZiBgVHgmlXce1SEYHTmgBgT1op3SkJoATOBSZ44pcZGKdswKAIipoFSHPrSUAIM+lBznmjHvSEEd80AKOtO3DuKYDS8UAP4pKTNLnigApMCmlsdqUGgB2KRRk80op3FIBMUucUYoxxQAZzk0gYdqCMCmj60wHk0winUhoATmpA/FR0oxQApOTTehpxxRigBN3NOB5puMUvWgBTg0wjincijrQAylHFOOKbSAUnNJ1pDxSqaAFAp2O1KMU4CmBHtpVGKk/CmEgGgBMUMKdRQAwjNIcipMUxuBSAXjbTcelAPFO7UwEBHSlGM89Kb6Up7UAPAPakFODEdqAOaQCe9IacxHSm+9MBw6UKfmpAC3Tmh1ZQG7etAEh6cjmm7UYZyQaYGJxmn8AUALkEquBtHf1o2jJ9KZu7gYFKGb0oAXaD2pCg6U4HFHGOtAETRnPB6UyUFAGB61MTznNRthsikAilmXLHIFNOF7UjKVwM8VKoQqu5setADNq7MmmGppfLL4i5FNIA4IoAhopW4NFMAUZ609WwOtMPFJmgCdihtyuPn3Zz7VVOQ9TLzTXXvQA3PNOUlehoVOM5FKBxQANzTM806mnigBHweab1FPA3Zph4OKAExSgcUvalU8YoATdxik75oI5pRyKAEzxQTkD2obIpSOM0APPIB70Gk42+9JnIoAUPg0U09aKAFYU3J6VNszkDrTHXbx1pAID604rg5ByKb5Zxk0YI7GgBwznrS5x15pAhOPerEcQIIY4P8PvQIhB3DHNPVGPGcUpiKtzVloQigq+c8gUDK5RuucighMZB5qXaai24bNADQvyU0nHBNT5U9aawGMgUANRhnnPFSeZ86sqg4OcU3a3liTHynjNPyIz9R3pgMmVvOO4L83PHSkjKKGDqTkcYPQ0v3mye9SqN7goNoFAFfGRxxQCUHIzmp2BK+YMcHBFRhlYnigBuSe30pOrDNP4xyKN6jHFIBhXHIoyPL56+tPaTONo470MQUwAKYEW7pQDx0zUoUIMtSDayFhxSAhbtzSp1A6Gkb71KCDjjmgCRT8xyce9RsR0BOc1ITgeophXA3UwGfhzRx34p20MMjigrt6kUgG0vftSZ4oNADutApQMAUnGaALCOB2p6uVOMVXUE9KniJxg9qACQk9etQ8ntU8lRd6YABinHpzTQaGyVoAjd+1CqevalWM5yamLoiY7mgCM8AGmls96RmLAAdKAPWgAzS5pKCaAEOKCaDSHpjNAADS96aBiloAcKdTM05eaBCUnFONJSAAce1KHPekxnpRgjtQA7J9KM0nNGaBj+opuKAeKdjimAmKDQDzTu9ADRQadtpuM0ANpcmlK4ppFACg0uRTATS5pAOz70cU3NGaYC0YpKcDQA0im09qSgAFS7to4qKlXNAEok9RSOA3K000nSgBwBxige9ANB6UgFpp96cB8uTTaYDOc0qn1pSKaR83FIB3XtTgBTc0A0ASHNGelNBPagkgUAKxBIpU5BpgPNPUgUwBMoQVPNSTSbwARUeQaHxnigBu3J4pSeOaIyRmmkEg4oAewKQgdcnNK0nIAximYbHP4U3axOaAJC+elITSNE+OKYEkP3jgUgFPuaAOetJjBpyoS1ACFN547Ux+G46VMBjgnBpkihRzQAhK53IKQknr3qNxg5B4qVOV5oAiIJoqXbmkK9fYUwGU0nNKp3DIoNACo2DUqshDbu/Sq5qVF3LxSAjzg+1OQ5alePA3dqYpwaYC+tNPSn9RTWpAN6Uh9aXvRQA2jOKUDNJjimApPFCdetJ2pCCBmgAapIjlSKjxkUD5TxQA/HNG0inFcAHPWkB4oACmO9FOFFAEjYPTg0gUKdzHNN3nrSZJ6ikBNuBXPrTSMDNMU45HbtSnJ+Y96BDhJjGQKkMoZANuMdDUKgk4PFO2jrnigYu9twqUMx4GT6VGFBOC3WlyI85JPoRTEKckgU3nnJoyCaVlU8jIHvQMQnHWlBynJNMIA780An86QDxKQnljlc5FB+ZyW6npSAbeMDkUpbd15xQAOGU7DjNKG/eDnFRkpnkUFl3ZoAfIwGdpOD1qFXwT6UpB7UEgHpQA/zSTjHakJyOlKCA3BHSkyelACJ1JHWkBbJz1pQ/PyjDYpiMQ5HUmmBKBk/NS5UMcdMUxjgHHWkUkDJGM0gGsQeKU9sUwjJ5p+RkAdKYDl4+9zTpGDdBimn0pDmgAx2p2Ywp3KWbtzxSKM9aP71ICP3NLzmlPSk+tAB35pcGkH3s9hSljmgB/Sn+aAPeoMk9KdtAwTTAlLs3ShR60vQ/L0oDqTz8p9aAHbQeKeqhW5NNHQnqaTcCGJNACXDgN8tQZyOaM5Y0uKAEp1IaXJ7UAA60jGkORSZJ5NAC80hpcj1pRz3pAJSdTTiPekHWmIO/SlJxScZoJoAdnNJ0puaN1AxxOBQSaaTSZoAeKXGaYM08UAOAHekOfWlyKTigBBTsmkooAduo3Ckpp6UASZU0nFMBxSlqQCMKaQacGFLkGmA360fWgihaAF7UtKRxxTaAFpKKTOKAHYpQKQGnUAFNNOzSHmkAA04GmdKVTTAeDikOM0GjFADTRQ3tQKBBQKUUh4NAx4OKRuTQDxRjikAgqQY7im4pw6UwF2g0win9qYetACA08MAKYaQmkA8yc0iycnPSmZHfrTQQAR60AStIcZJ4pgy43A0gwQOM0ZEbEigAHUN2p6y4bdTYnGCD3oK+goAXzO9RyPvGKV84xTCGpgSZUoFIpiHaxFJg0Y5pASFhTQ3zH6UzBFPQUANCBRilPFK/zHigjgUAR9KfExU8cU1hxQOlADySciohwamAz0FRyDDZoAAe1IaZnBp1MBO9FBGDQelACD71KRQKDQAmOaePuEUw04Hg0AAWmsKfmmNQA9TlMelIBTEzmn9DQA4DNFKuaKAJFQEHA6UhUZ9KjXd6gUMevNIBwUDkUO2ABigNlcUjxSrGkrJ8jcBqABTuzg4OOlG4r161GODx3pxOTz+dAEgYt04pwIIwxyahB2jrTs89OtADlwMknBz0pdw7DimMwxTd3HAoAkD/ACnjmkJxTFbtinBuelAC5JXFBztAp3y8kpTdwOcLwKAEBpAcNyKUsvpTkI5IGcUAN3etPAXgnNNO09sZp4K4A7d6AGlQGBHFI5wevOKcxXA60jBd3HNMBgBKjB61Kgwrbl5HemA+gqQudpy2c0gIic5Gcmht20BqcoBk5GBSs3BGKAISecetOAI+lNf7vvmlTJBApgS9RmmdvalA+XGfwpOtADgeKDRxjrQSexpANHShuDilX7vNBA4oARRkY7UoHzn0xQOuKU9SRQAIBjtmnqB1IpFWloAkU5P3c0zvyOKUMVJ5x9KZjcflYGmBICBwKdKqqACpyRmoQT3pzOWIB9MUAM4z0o6Up6009KADv0o70oIxxSZxQAw9aUjik70ZOPWgBQuTipPL2gYIpi5HOKcGPpSAGGBTRk0rmmg4pgL36UE0vWggYoAjNFOKnFN5FAC4pQvpQpJFJuNAAODTwajY5OaUZoAkzQDzTabSAmyM0bj0xUOTTwaYEuRjmmnFNppJFIB1GKQNkU760wG7aaQRUnFNNADQTS5oxzSN7UAODe9O3ZFQ96kGaAHGmnrT6aaAFFKKQUZoAcelNPFKelJQAuc0o603NKDQA7NLmm0dqADvS0AUu3jIoATvQeaM0g5NAC7TTxjZ70hfgg96MYoAKUU0c04ZoAd6/Sox1zT84HWkABFIBMAmgqDQR0xSYIyKAGFRmmlakJxTc0wAUbATyTQzY7U3J70ATKq5qXauVwRmqwP5UrMM5zSAndUOMd6rsQhK4zSI/PWkLfNmgBDyeTSDGaG5OaFFADw2TjHFPITPGaaBUtrF51yqHp1P0pgQsAOhpKmvYRBcsq/dPIqEcikA0imE4qYr2FRyrtUGmARs2cDvTpF4PqKiXrUxGQaQFcj5eaVeRSsKbnBFADyMj6U2ndCOOtNzzTAd1OAKQjFGe+aGOaAGn7tANG3Pekxg0gHgc0SADpSA8UMQVx3oAZnFPB3Lkdajp0R5IPegBwc9KKUCimAZHHFL2NJg8U7PzYIpAJnApm9ugJx6VLsBHNMwB1/CgBoBPSgD1p2T1GBigZJoAbyBzSsxBp+flxxmmkDmgBM8UoJPNB6DNIpoAcooOc0Z5pSpNMBDnA9KMdqdg+tAVs5pAMxTt2DxwDSHIPHTvSE4+lACnkdaAwHSmg9e1KSM/hTAVmJxj1pMMW46mkH1pccdaAFV9venAk5xTBx2py9CaABmIyO5puSTz3pxGWxik8tsbuoFADX4GOuadG/yY70FaTHPFIB7AjBpCP0p5wUFNAoAcuMGkPXGOaeuAMGm7QWxigBqjjp1pcHpinKNvNKxOPemAwfep4x+VM70o5NAEvWmnINKv6UPgYoAbmjgc0H8qY1AAX54pQcd6ZT8fLmgBCaQH2oxml28DJoAF568ChiKCfemk+1ABSbsdKOaBz2oAcWNN3H1p20GnbOgoAYTQBk1IY8EUnegAwTRsPrT1FO6UARspHFN2E08nFOyGA4oAaqrtpmOTUhFNNADdoNKBR7UHigAIpnenE03HNABjmlBpOlJmgCUHNIRSAjHXFOwMdaAGEelKGYUh60p6UAKxHWkJpMU4AUAIKKXFGKAGgc1JQBS9qADFNIp2cdKCTQA0UtN69+aMe9ADiaSijFACZpwNIVz0oC8UAPopAO1LQAo4pWOBTRQ3SgA3HGKUetMp60AP25B9RSMQaaSaM+opAKMDmnCmkjtSqcCmA7bmkC9fak384ppyTwaAHsDgEUgzik+Y8U6M5JHpQAYyKaRS5K/Q0jEkUAIwFRHipGJqPrQAbuOtNOD0NTLsxhlpCFZgFGKAIgDmlwc08cORR0zSAPLbuaNoBpNxJqcIvlE5+YUAM6CtTTbfZH5rDl+n0qtZWZkIklGEB4B71sAYHFAGfqdv5kO9R8yfyrH6CumJBrJ1CzKEyxDKHqPSgDP8zkYpXw8dNYjpijgrimAxRzU69Kjxinr0oAY45qJl5qZzUTNQA1mORSHk0h5oFIBaWkpaYC00gY96cKaxwc0gEB9aU8mm5zQDQA4jJpoOHFLmmnpQBOetFNjO4Y9KKYEgGOmaCAOTSgg9aR844oAMnGB0qMjnpUg6Y6GncdG4PrSAg+tKCdpbjNSOg6Nx71GBjgHNADiuSDSkYYjHNAPHAwaXIOGoENYU3FSYx05pvemMRTning4NM6c0AEjNAEilT1IGP1pWJ4IP0qHB9qeMfxGkAH7tIFDdDikLY4HSkBGeRQBJtAXII5ppUg9qUHgYFGaYABTimQcGmjHQmjBzw1ACAEE5Ham5+XHvT8HuaRl/KgBVP7w4pSx249etN2HOVNPx1oATknnFSGMcleQB1qMEjg9KXPBxn3pAPG3FJInRlxn0pOAeQfwpyhSPvH8aAF24UMeM0j4VuKU9AWbikbDcckigBu7nJFAIpcADIGaa3QYoAPp3pfp1oHTmnggYIFACqDgmlbkA5oB+UipJI1WJSGByM4HamBAATSEYOaUcU48igCJxk+lOAwvWkb7vBpFPHIoAO/SnlQ3agDmnA7elAEZGO1Iy46ipkUyyBF5ZuBSTBi+w43LwRQBCBSkAUvSmtQA4Y604MMCo1+7ilFAEwcdKjYgmnKPlORSKvc0AC5AyBTsk9aEB7YxStx94GgBp2jHOaaTTtqsDg8jtSBR3NAAGNG7PakOF96UFeuKAG5weBSNzTyQaa3AoAbSGncGk60AJ9aQjNOxSHigAAHelLcUnB4oIoAbu5p4OaiINKDigCSigHIpwFACAGgA55p9IetACj60UlKKAFx70Gig0AN2d80vTrSE4FG7PFAC5GaUEGmZxxS5AFAC5qRcEdahp4oAk288UrKfSmB8GnGQkdeKQDQDTCcmns5AOBzTSOhNACYp44FNxijigBcil3DFRMRmlzxQA4HmlFMHFOzTAUgmlJ24o3U0tmgBxkxQmPvA8mmEimKcHg0ATZx1pN1RFjTd5oAnJz1oDADoKg3mjcaQFjevpSfLu3ZqEHigmgCQsobIoLAjmoRSlqYFuC2kmwyIdp7npWjBYwxgmQ729O1Y8N5NANqOdvoelaNtqUcpCzDY3r2pAX91KGJ4zScde1A60APH1pWx60w8U3NAFO506OUlojsb07VnzWs8AJZDtHcdKvXGpRRErH87foKoTXk8wKu+FPYdKAIc08HioqUE0AOc1GRUmA4J6EUYBWgCHHNKBSvgDigHigAooNJTAXNMfkUppMkDNIBo4FAoPJo7UwFA9aCPSl/hpF5NADowV+bIHtRTVOG5ooAlVsnFOZ+ajAOadg4pAGcml5PWkwKCR0oEOG48HpTSoQEnrSq3r0pHwV5oGAPQ0/GAHAyKjTCsM8inBgGO37p7UCFJwcqcikJ5FAHPsaRlKnFAwPfFNzQeelLjA5piFUcU/BK54xUXHrTlbB+U9KQxccjAoKkemKcGyeT1phHPWgBKOc07bnoaUxkYzQIaMnpSgn2pQlBj5wc0DHLz1pSpA6UwKBnBPFODEdaAEBwaXcM03OetLhTzQIXcOKC3OB0NJgYNAQ9RQMcp5PFMLdRTqTAzk0wHoULBecY5zSoO4PJpigbgRSDgkZpATNwMZwBUXDEgnHvR+FNzzhaAADHGafubaFB79KRc96eAT0oAkUAjmnfKN3XpxSIRg7jyKV1ChT/eGaYEOfmxTs/LSMo60zOKAE69aUY9OaVTjHpmpQqswH60AR96GNKU5OOlIVOelIBYjiRTnHvTXYh2IBIPelETMeKcXcLtNAEWR3pCBmpCoweaQLwe9ADRgcinBaRuFAxzQpJFAEgyAelGeOe9NyTRzigBN3pSlz1zQAPSjA7UCBWG7OOaGxSEAdKY2aYyQ+lITTA1LSAcTtHTrSZzSfWhjzxTAQj0ozzS59aDigBM0mKM0ooAQikyelP7UmPWgBvWkxSkc0UgAZBp4NNFLQIkBHekPtTM04GmMcKUD0popwbigB23imkcU4Nmm0ANIpAB2pxNJmgApNp9KdkEUhYgcGgBKUHigsaZzmgB5NAb3ptFAEq4brS4B4qEHFKHwaAJSvGRTGOBTjJ8tQsSSaAFxnmlwcUwHFP3HFIANAPNNLU3PPWmBITRmmcmgZ6UAOzSUgNKaADNJRRSAM0UUhzQAnSjOaTn0owaAHdutNOPWgUEc0wDiikxS470AX7G+MREUxyh6H0rYHrXLk1taXcebCY2PzJ0+lIC9x3rIv7/AHsYoeFHU+tWdTnMUQjU4Z+v0rG70CAUvFNopgP4pOMU0UUDHVJEM9ahFSr92kIZKuDTVFSMcgUwjAoGD/WmE4p3UUwjigB45HNIwG3rTd200uRTAQYI5pKU8GjGKQABRja9LnvR1oAQjnrRRg0UASGTLjtSkmoue9OzleetAhwJ60ZPNNH1oBz1oAUZz1pSoLZzmk6nk0KOaAHBcY9KUAZxSE8Z9aXBI4pjFyRx2pDnGaUZA+YcUEDOc8GgBpOOtBalcDGOtMPSgBp7UtGM0hU9KQhckHg0uSRTRwelSA8YNACAtSGUk4NDAmkYcCgB4kI561IsgYZINQAHI3dKU4B+XOPegCYHilOAccVEpIHNLuOOlMY7qSBTQOOtJ0PB5NBOBQAEkHrTkfBxTCTmgcUATYXOc0OO9MJpQ3BpAKAaeVGB6nvUYbn6VIMMOD0oAayMMZ6UgxuO3JUetSc7cn9aZtGD60wHAgkelOQ5bHIpI8KhG3J7+1OIO4FTSAcigNl+R6Uj57dKRn24PXFBYnkUAJ60w5z0p/JBNAIx70AMI7inhsL70MBj5cU0DHWgB4HPFSKUxhxz61CGxTwaYDygU5RqiwwPNOOQe/NJkZGaAGsDjpTQSDkVK2AMg5pgUMMjg0AGQc7hzTcACmklTg0blpABJ9aFJz1pwxnGM0hKjtTEO3E0E5pgGelGDjNIBT3pOoppyKUNleaYw2HGc0vIPJo6L1puaAHZzSUD5cE9DSZJPSgBSOKQ0Z5o70ABBxkCkyaXcwFJzSAcDQaYeKN1MQ8gk0hozRQMQUuaTFHegB3Wim5p1AC5pc000maAJQ1LUQPNODUgFYUzPOKcW5pmeaYEoHy0g5OKExt5NJwrcHNIAx2o6UFgG5prOM8CgB/GOlJ0NBkBUDFNLc0AKTSHmkzSUwHYNLikB4pDnNAD+MU3I9KQEik6mkAHk8UYwc0nSlzQAqnGc0A0zNKpoAdmjNN3ZFJnvQA7NGabmkLUxEn0pM0wGjNIY/PFNooxTAVRzS0g4PNJnNIB31oJG2m4pMDFADgQOoqxZTLFcoxOF6H6VW6Uo4oAsXsonumdTleg+lVz1ozSZoAOBR+FFGaADFB+lKOTS5GORTAbT16U07fSgHjrQA6mtmkLGlGTQA1c4NIc7ant7S5u32W0LyN/sjpXSaZ4LuLkg3cm0d0j5/M9KEhHJBS7BVUsx6ADJNacXh7VXh80WjY64JAP5V6ZpfhnT9OAKQrv7nqfzrRlsoZFwFCHsVp2XUdmeIzI6OUkUq6nBBGCKaxyBivQfFXhw3UZljUC6QfKR0kHp9a88IKsVYEEcEHtQ1YQZozijOKBzUjFzRSHg0UASYyaXHFL2o60wG4xzRxT+MUhFIBi4J5qToeKcqqUxxnNSYAGODTAiLYyeOae3GCO4pjY3YGKUSDGMcikA6RGABzwwqIEL9DTi5I2mmgfNQA7Bxx900wjHBp4JQEc4NMZT1HNMQgxilyB0PNIMjrT1ZAORzQMZ0o5p7bSaYRigQuaO9J9acBQMdjpR7djRkelITk0ALRnAx2ptOxnOOaAAbeCOtO69qjPH4UokPr0oAUr3oXpkU1XY8GhW57UASfKRyCDTQCwOKUsfajp0NACAHPSnrwpx1qMEk981IvHU9aQDQSe/FP3enNKoGSMZFI3H3QQDQAof5uBgDrUgZXz2PYVAOO1PXJccY9KAJHG7CtxjrQy+WSucgdDQ7HnI5NN3ZoADz160hweAOnWgn2pATzimAvQ4FBJFIOtIetAD85pQeRjpSH2FHQUAP3dzTc47ZpM+tJuI70gHNgDjj2oRsjGaTcC3NMYgHg5pgPdS3OKj2Ej6UFyRxQh5oAcqsCMUMDjmnEk9KcBxyKQCKg2Bs8ntRg54/KmquehoGVzTAGHOCKYwApS2c5NNyc+tAC7cilKGNXDJk+vpTUfDA4p5YuW+Y5NAELtnGOgpUPrUihdpGKNgxx1pAMYUmPelYMvUZFOCh+nHtQAmBjrSYpcY60DHrTAYxpuakYA1GVwaAHA0ZpozS0AOzRTOtKDg0AOozSEg0UAKDzQeKaTRmgBaAaM0p6UgAmkzR3ozQAobjpS5yabRnFADzTSaAc0NjPFMAHSgjFGcDFBPFADaXmgUE0ALmjf60n8NJSAfuBBpM45pBjPSl7cCmAhbnpSZp2KaetIApOnalzxRzQAmaQnilpCaACiijNAAPpS0maM0ALS0maKAFx70Yx3pvel6UwFpDQelJzSAfxQDg1ESehp7cgHNAC45oFJkDvRv56UAOBHekI70m6gNTAXmjBxRnmrFrZ3N4222geQ+oHH50AVmJHFMJxXUWPhC4mYfapduf4IxuP511Om+ErW1wwgRW/vSfM1Pl7iuefWOj6hfYMUBVP77/KK6nSvByZDXBadvQfKg/xrtYdPgiwSu8ju3+FWwABgcU7pD5X1M2y0iC2QLtUKP4EGBWkqqi7VAAHYUUVLbZSVhaSiloAjmiWaMo44P6V5b430g2d39siXCu22QDs3r+NerVzviizW8t54GH+si49iOlUtdCZdzyLOacp5pApAOR0oHWoAc/Wil6iimBIKX8KOM8Uu3NACqoYZ9KQgA1IoIG31pjLzQAKQDSggg0mBjimnjtQAD79KU+f0oH3hihuGOe1Ah4i4LA5FKQCKbG5wQ34UuRj3oGNzjI/nUZyDwakbrimEAdKAAH1NBwT0pOKXNADDxzTgadjj1FNxg0ALjIoFKM444o7cUABA4IpwUkZqIk5qRHxQAqplgCcZpzRiNiobJB7UZBNOH3iw5oAiyM5xyKTap+tTGMEjBxTShU+1ICPYQeKTaRTiSDwKTnPNMANOUALknmjPWmtx9KBDxkE/nQGGOaTIXkHPsaYp5GOtIZOrZJBO3jFG75NpGcGowd2d2c09B8wBNAC7elSIMjIOCKjzhuO1PWVNuMHdnrQA6TAcYzgdc0wYP3TgntUhwyhzzzTUQMx9OxoAQ5HUUgOQTkU9mdU28EGoeR2pgSfLj3pNmehpuTnkUu9R2pALyBg0nNIZT2p6SAjDDBpgJjHNIcd6k2jsabs5560AN9MUmPanYbd0oyR1pARlRngUDrTi2R6UwEUwH/jTucc00DilAz/FzQAqnmpDjGKg6E81OgUryeaQCGMNzmonjIPHNSHGeM5pN2OQelAEW0jginKMdaeZNz896ULmgBgAIyKOh+UU8qVBGeKZz1zQAAnuePSk7lhxikY+3NBGF96AHEgjNMPQY60oUladsyuR9KAGEZHNNdTkYqTZ/eNJI6buMigCIBgeRQQc9KkP1yKGVQoINAEQzQcmnkEdaRuO1ADBmlFLRQAGjFLTSeaAF6UUmaBQAUtNNISaAHUvGKjzS54oAfkYoBGOajzS5oAeOTTjzUYNLmgBTRn2pDSbjQBJ9KYTRnikJyKAHDGaXoKYDS54oAcDmk70gYc00mgBxNIWpM0lADiTSGkzRQAo5FFIePpRkUALRTc0ZHpQA7mlAz3xSbwMcc0rNmgBGGD1paaeaXd2oAVj6GkPPejGaUKcZoAaR7009cU4ikK9u9ABmkLGtGy0HUbzBSAxof45PlFdHp3guIsDcvJcN/dQbV/OqUWxXOOiSSVwkSM7HoFGTWzZeGNQucNMFt0P9/k/lXodhoENqgWOOOBfRBz+dakNnBDyqAn1PJp2SCzZyGmeDraPDPE07f3peF/Kunt9JhiUK2MDoqDArQoo5uw+UbHEkYxGgUewp1FFSUFFFLQAlISAMkgD3qtPPOXMdtCSRwXbpUYsZZjuu5i3+ytNLuK5I99GG2RBpX9FqaEylcyqqk9FHOKWOGOFcRqFFUb/AFe2s42ZnTC9WY4UUb7BtuaJIAySAPU1yni3WraygZlcNKyFY19T6/SsPWPG4fclmDM3Zm4QfQd6464up7y5aa5kLyN3P8qNhPUhViSeevWl6UcbumKDUgOBopoooAuBBjtQpweMUw4HFJmmBITikJPemdaQnDYzxQBJxSbc98YogCyPhmxxQrLyvNAhVXaw5zTW/wBYTjjNKW2tTd244/WkAE9+KTdzSjBpcY5pjFwcU04p2ccmm9aAGHNJk96kKnB9aaVG0Hv3oAaWIHBpxbKA8Zo2g/SkUAHk8UASBieTSAcn0pFwBTyMCkIYRTcGnnJ6Ck9aAGjcKk3Y5zTD+dPB3ADoaAHCT3pQcrkE5qNVHc1PFGSPlIPtQMjJxSjDHFStEoUlshuwpmDuU8GmBEY+etBDAcHNPb72aX/ln75pAQ/UUq4D+lKMd6lkhXaHRwxPUUARjOeME0pL9MYqLa2e9PLsVwcAjv60ASR853HFKQgTjO41GeqjIJx2qRjgKO4oAAwKnOcdqIW2gkcsD09qWL/WZ68HrTY0keUbRhjyM96AJVIbvyeo9KBt5Bz7U7KOvmE7Zc4ZajcAc0ABU9aaQaAT13UoY5GeaAG7fUUZ/CnkhulJtx3oAVTxwe9OweuajGc+1KCAaYDjuzmmkMeetJvJ6Uu6gBjcHmm/Snk560ALjrQAD60mOcg04DHPUUZz2pAH1605GOORTD0pY2PQ0APPPbFMYY+tO4PelYZHIpgRDO6pVbFNVV3d6cV5pAPEgYnmmHHUUxhjpSK2RjNAD9o79e1Hf5+KQAkDnmlds/eHIoAXeDJnHy4xRgAdTimbhgdqUNnjrQAbM8hgajKgjnrTnwp4phJAoAQAZODijcejD8qbjOTSqcCgBx4UE0MQcUEjbTQeehoEHfmk4obBPAxQfvfSgYUdaAKCMGgBOO9KTxxSFeaTHFADjTTQaC2FxxQAgpccUi8il5BoATFFOANIetABigUdqQ0CHZpDSgZBOelNyKAF7UdqTNL14oGHNB6UEGkNACZwaN1FIfagBd1KpG7npTRxRigBxIxSbqb3pRwQaAFJphNPbDNkDilwu3pzQAzNOoIGaMUAITmjORzSGkyRQA/PrSE0ih5GCopZj0AGTWzY+GdRusNKgt0PeTr+VNJsRjg+9WLSzu7x9trA8h9QOB+Ndtpng+1Qhnje5b1fhR+FdVa6QkaBWIVR0SMYFVy23DV7HAWHhCaQhr2YJ/sR8n866vTfDEFsAYrZIz/fk+Zq6SKCKEfu0C+/epKOZLYfL3KcOnQR8vmRvfpVoKFGFAA9BTqSpbbKSsFFFFABRRS0gEooopgLRSVXmvoIuN29vReaErivYs0ySWOJcyMFHvXOap4rtbMFWmVW/uJ8zf8A1q4rV/FN7eErb5gjP8Wcufx7U7W3FzdjrvEfiu3skaKM75D0jU8n6+grznUdRutSmMlzISB91Bwq/QVXcMx3Ek55JNM6UmwGkEGlH1p3Wm45pADZzmlPanHpimgjA9qAEFFK2M8UUATk80uDjNOxk5NDcmgQmOOKTC9Gp3U+1IyDsaYBtGPl60gAUCmnK8A0rAgjnOaQCsC3NIBg8U8k7fSm5NMBNwB6GnAg+1Nzz70E5GaBjic0g60zPNG40ASY75ppPy4pRSEUCG8gcUuVHJ60oFNKhu+DSGOUA807BB5ohHUHr2pp+9QICSOaO+M0hHakGc8CgBwJHIpUk2SKxXcFOSD3oVST0pwACneKYx0wdJSXjMe/5gD6U6NcHJbAI61E7O+C7FiOBk9qCW24YfSkBNHMVcE4YDjmgOM54qAA4xTlXjk0APYqegxQFO0mo+aer4GKAE43dKOiEik35OcDinK3zknB4oAaHZlx6Up+YCm7ee9Ie/BoEP8ALGzJbGBx70oVTtAY7j60sce5VywA5powCSecUDLIjCqzZB2ccd6h85iq7mPy/d9qCgUbo23DGSKYw35ccBj0FAhzkuS5POefekD4IFKEO0YICkcZprf6zpwKBgcE5pmcGnEelMJINAEgJ70oPNRBhS55yOlAEpJFKMdaaMk+1OKjFACEDrQI3foDTc4NS+fIQCGxjjigCFgRQG7VKGD5LCmOoGDnrQA9WAHPegHtTNuDkUoJ4zTAftpAvNKPyp2PekA3HORR5mBinMh9aYUxQACQ57U4MCc1CyGgZHSgCxsDDNQmMg0CUgkHpSb8nHrTADuA+lOYnaD60EfL1pjk4ApAISaQMRzTSWzRk4oAczZNIaQ+tIeepoEPGMdaQHBxSDGKTOKAJMjFAbYcim5GKQ0ABPel6nNNpc0DHYpVA5B9KZml3HFAC8HrScUY4pCpIzQAYFBAIpAuVzmgD3oEKqCk2+9OXpTT160DFwQcUEEHmkHXrTuc5zmgBMUhFOYkvRQIaFFIRjpUhFBxjpQMhPFKpFKR14pAwA6UAPJBpmOaUtx92kzntQAmKXbS8Ud6AG4xRTqbigQlApcUAcUAKDRnrTfSjkAmgAyBRnimA+tW9NtWv7+G1Q43tyfQdzQAy1tbi7lEVtE8j+ijpXTab4OZyrX8hyf+WUXJ/E12Wl6ElvZqluqRJjjjlvc1dsT9luWgmUBm6NWiSQtShpvh2K1QCGCOAeuMsa1Usra3G58E+rmrNwszJiF1Q9yRVUaerNuuJWkPpnilzFWsOW8hLiOPc5/2F4FWaRIkiXbGgUe1OqWUgooqKa6hg4lkAJ7dTQNK5LRVP+1LT++3/fJpw1G0P/LYD6g0h8suxaoqFby2b7s6fnUgkQjIdcDvmgVmOpapzajBHwmZD7dPzrE1PxLBagie6ji/2EOW/wAapRZLkdFLPFCMyOF9u9Z11rMcSMyAKo6vIcAVwV/4xLEixgyf+ekp/pXN3uoXl+xa6nZ/QdAPwp6Im7Z2mq+NoVJSBmun9vlQf41y194g1K9yGmMcZ/gj+Uf41ldKUHmk5MLEgbJpQ1Rg4p+akYobBwaaxB5py4zmkPegA7UmKUHNB60AHBGc03AzSdDS0AIaKKKALJI4zSZFI3BpDwOlMB+4UZHpUXOaXB7GgQ5yOOKWR+mOwpmKUrQMfuJ6UE57UzaQOtHzZ60gFbAHWgYFGM8mjAB9qYCH2oXNBwD1oxSAdjIyOtGPzoGaMHrmmAdvekPTpQT60o5HFAgUkEEmnNjPBzTSMjmhdoAzzzSGGaADn5TilIGeDxRjnIoAaGdW3VJk4HIpNvrSHDHvQA8BScnrikyxPzHpTeFHFIW70ASggnBpfL3A4bH1qEbicipMswwBk0AKkfYt1pGTbzTl3Y4bBJ6USkF+vQUwGhVI680oTA96jzjoacJOOlIBQ5UnIB/pQXZjkkUzOaTJPAoAlGGPWnpGgYs3Ix2qBQ4I96kyVXLHjNADjhM/LgsMAVG7SYEPTaaUStuDnnaeKkllMpVnVVYdwOtAE32YlvnfagIHNVpCUYjPA4HvUuWIO98kHP1pkmGQEHIz09KAIztOOaYy+9SBBtJHUVE24HpQAFcdaQEilB5p+OtACK3XPSnhhjAqML1IpNpwT6UAT7QRntTTtBO3OKjSQjg9Kl3KRnFADCxAxinqQcBweKULGCS+TkfLimbhk4596AJBgZxS7Qcc0zj8aVCcj0oAkKEcCkXNKWAb2pwUE5BoAQkjvSbhjmkcHPNNHFMCZdpbnpSlEG4L0zwahBOeKcG+TFIBrIM571CwO7pU+c8GkIA96AIOacrnvzSsBmmEehoAf8tG0HpTGGAKTcV70APK89KafWk3tSMTQAhNGaBg8Ghlx70ALuFKD3pg6UtACkinbhtxjmo6AKAJPM9hSHce1N4zTi2TxxQA1XPQ0pY4OaDGRggjmmYOcZoEKoJHFKART4/9Wys2KZn5sZoAcDjrTT1p1BQ8UDGinZOM032pwoEL2pRmgUpPAoGHak/CnAjHNIxFADeKaRTjSGgBrjGDmlGc5pCM9aUH5cUAIVFH0oozQAvbimknNKOho4oATmkHpSmigQ3vQeRinUnegYwg1s+EWVdejDd0YD64rHbpU2n3Js76C5H/ACzcE/TvTWjEz3K3cPBGy9CoqDUYvNty4Hzx8j6VX0a5SWDYrZGNyH1BrSOCMHvVPRlLVEVjcfaLYMfvDhqnrK04mG+lgPQ5x+FatKSswWwUlLRUjI5ZBFE0jdFGayLWL7Uz3E/zFjwKuau+2yKj+NgKZarsto19s1FR2N6asrmeIUW/MTjKnpVv7DAexH41DP8A8hRMe1XWcIpYg4HoM1m2zVtlU6dEejMKYdNP8Mv5ipvt0GeSw+q04Xluf+WgH1FF5Cuym+nSspUsjKeCM1lTeE7KQktYJk90Yj+tdKJ4W6SL+dPDA9CD9DRzyF8jipfBdmfupcx/Rs1Sl8GKP9XdyL/vx16HRT9oyeWPY8vl8HXg/wBXcwP9QRVSXwvqsfSKN/8Adcf1r1kojdUU/hTDbQHrEtP2gvZxPH5dH1OLPmWU2PULn+VVHjkj4lR0PoykV7QbKA9FI+hqGXTInGN2R6MoNP2iF7JdzxwH3pC2DXqdx4Zs5s7rW3b3C7T+lZlx4JsnyVimjP8AsSZ/nVc6JdJ9DgEb5qfnmupn8EupzBdOPaSP+oqhL4U1RG+QRSD1D4/nTuiHTkjC/ioNa7+GtXUZ+y5+jis65tbi0fbcwvG3bcMZp3JcWiGijqBRQIlc8jHNPGCORTD1561LE2COOlADWRONuc96ZgK1Pkz5hxTCfzpgOzznHFKXB7UnAXmgUABpvWhjz1oByaQDu3HSmluwFKM5pO1MBOM809clcYpoU9TTkBwcGgAAyaccbcd6VcsCMjNIQcYNADMZNKqk9O1B4oyM8cUADDB60lGc5zQenWgBueetPBI5xUWeal3kjaO1IB5ftUeSOhpuCadgcDvQAFuOlA60fLSjAORQA4nHI4prE7Qw49aTJY7RRn5cNQA+JjnPfFDElN/cmkiUtkL+FBUhcd80ARmlRiDk04oQ2CMYFNxyKAHkn0xUbBkkIPBFOLkptOaaSP4u1ADtzevNOJ3KB/FTBgjNOXYM5zQAhByB1pTkDr0603PNDfe74NAD95A61JHIMDeRtJ5I6ioCBjHfNKMLEyMBk9D6UAWbcxmVgeVxwPWmSKyuVX16UwKI1jfcDu6gdRQzFXz2PegA53YIpcHcSKXeMndTcgd6AHgZXpikCY+lId2O9IHI4NADtinjpTGXnANSnj5hyKQkE+9AEYJHBFNOB3qyYx1IqIqp9qAGbh1zTlck8UwxY+lCEg+1AEzNzShjnrUPmAmlDLnrQBKSSeaF+Y4pvBPWnDcBxQA7G3vRn5RTMkrzSBh0oAk3CmE5pCRnAFOVckZoAb3xQ2FYAU8px8tNx2oAaVyaQp3p3GaDQBEwo7UpBNMPy9aAEYUoJxim5zS9OTQAc07FJ1paADpzTkdedwpKAvzUAKAvXmkx6VIG+TGKbQA05pFHWnH3pgODg0APmIOCB2qIHmnOcikHSgB/SlL5HFNXk0pNACAU4CkFOoELS0lGaBinmkKn1pQaTOOKAG80hOKDxQOaAE3EjgUoUmpFwtOBUnnigCIRkc0FalbaBwaYcZoAaFxRtpRSimA3FIRTzxTaAG4pKcaSgBpApMcYpxFJgdqQHZeDNYOxbOR8TQ8xZ/iX0r0OCZLiMOh+o9K8Njdo5Vkjcq6nIYHkGun07xjJBhbxGJHHmRHBP1FXdPcWx3zLjWhjuM/pV95Uj5d1X6muCl8Y6eD5oe4eT2TB/Osa98ZXczH7LCsY/vyHc3+FN2BM9PfUbdfukuf9kVn3uvxW6kySwwD1dhmvKp9a1K4yJb2XHop2j9KpM247mYk+pOam6DU9Nt9bg1eaSOCZ5fKwSxGBz6V0QGFA9q8x8Fzql/PCTgyRgr74P/169GF3H9m37huAxjvmsal2zqp/Ciun7zVGI6LWhiqenRkI0rdX6VdxWctzRsaURvvKp+opht4T/wAsk/KpaKkVyH7NB/zyX8qUQQqcrGoNS0UXC4UUUlABRRRQAtFFFABRRRQIKOPSiigYcelZ2r6ZbX1o6yxKwxyMfqPetGjqMHvTTsI8Y1OyfTr+S2c5CnKt6qehorf8eQCO4tpAOfmQ/geP50V0p3OecbSsc6BkinBXCljwKaSRShmPBJxTIFY/Lk9TUZ61JjJqM96AFK5+tIY2HOaTn3oO4/SkAFfypTjOBTsYUDHJpsgOelMAJNIGyMUhBxzQFwKQD85GDRnimYNOGcc0wHAmjfz1puM9KCOelACk560EYH1pD0zSMWIGaAAnFN3kinAE5pVQlS2OBQAxR82T0p59qH6CjHFAhBwM5pxyhGKYQaQk5pDF5JJpwOTg9abzilXPmDNADunt70jMT1NSxQ+ZIwJwACc0zyzkk9BQAsMoRs457U6RizZJ5PeomUt04B7Uik/dPSgBxDls5zmg57Uu4g0gLE57CgBOc8cUhXnk0pOTSbSc0ANLbWwvIpysN43HApgXaDnkmjaSKAAkA5Bpxbdt57UwqaXaQKAHry3BHpk09tsc4VyHRTzjvUGDjNP8sAAZ5PWgBzsru7KNqk8D0pQ2V2k9DxTOApXqc0uO4oAlmAVFI5OOahBOaVmLjFIpIODQBKspUAUvmAnLKKiwc0djxQBKrfN7VIWU9uarKTmn7iDzQBKX5wCaZuAPShcBSSOT0oIOAT0oAepDZ5pxiBXimFFI+QmhWZTjNAEbRMpOKiIINXN4NRMA2TjmgCJWIGM1KrnHBqMxntQGZRjFAEhY4ppODxSKSeKCOaAHrJgZxSiXnmouhoAy1AE4mPal3gnIquevGacCaAJWI3gGjbnODUXIbrUmcLn1oAQqR3qMjNSZzTHGPegCMfexilcEH2oJNABI60AMzg04GlKBqTbQA5SKkBBqHHNSUALntQaaOTzT9uKAGsDTSKmlUgL7ioDkmgAK4FA6UoyRzS4oAF4NIaXbRigBOtOPAFAzSEHGaADPFKDxTMmlGTTAdnFJmlC5pvSkANQvWmsaFPNAEwoPFNBxSE5pgOJPWmHNOBNJk56UANGc07fxSkZFGz1oAXP5UwtzTiDSFctSAN1Gc0c9MUFTimAp4HNRnBOaeQSKaFNIBKjIOanC5FJtAbpQBBznFLtqTHzZoNAEZHtTW68U803bQBJbTy208c8LbZIzkGunj8ZJhfNsmz/EVf8AlxXK7aTaaLFRm47HpFl4ysJVVDN5R6YlTH6jitmDV45lzGY5B6o4NePgZ60DchyhKn1BxUuCNFV7o9oW/jP3kZakW6gbpIB9eK8eh1XUYP8AVXs4HoXJH61fh8VarF994pR/tp/hUumUqkT1ZXRvusp+hp1eaReM5B/rrJD7o5H86uxeNrYffhuY/wDdIP8AWp9myuaPc76iuRt/GWnvjN26f9dIzWlB4itZv9Xd20n/AAMA0uRlaPZm5RVBNSVhnYCPVWzUq6hCeoYUuVhZlqioBe25/jx9RT1uYG6Sr+dKzCwz7XBnBfH4U9Z4W6SL+dLthk6iNvypptLc/wDLMfhT0DQkDBuhB+hparmxh/h3L9Gp8cBjORLIR6E5pWQaEtKKTFVr+5W3gOWAJGSfQdzQlcR5/wCP7hXv4IVOdoZz+JwP5UVz+rXp1DVJrkZ2scJ/ujgUV0LRHPN3kf/Z') center/cover no-repeat, #2b2b2b !important;}
  .crest,button.crest-home{width:58px !important;height:54px !important;background:transparent !important;border-radius:12px !important;}
  .crest img{width:58px;height:53px;display:block;filter:drop-shadow(0 1px 2px rgba(0,0,0,.5));}
  button.crest-home .crest-h{right:-4px;bottom:-4px;}
  .brand-name{color:#F4EFDF !important;font-family:'Fraunces',Georgia,serif;font-size:13px !important;letter-spacing:.06em;}
  .series-name{color:#E8D9A8;}
  .chapter-eyebrow{color:#D9D4C7 !important;}
  .chapter-sub{color:#F1D58A !important;}

  .gnav{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin:4px 0 14px;}
  .gnav a{display:inline-flex;align-items:center;gap:6px;padding:9px 14px;border-radius:999px;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--accent-text);font-weight:700;font-size:15.5px;text-decoration:none;}
  .gnav a.home{background:var(--navy);color:#fff;border-color:var(--navy);}
</style>
</head>
<body>
<header class="brand">
  <div class="brand-row">
    <div class="crest"><img src="data:image/png;base64,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" alt="Brain and Mind"></div>
    <div>
      <div class="brand-name">Brain &amp; Mind Academy</div>
      <div class="series-name">Sopaan <span style="font-weight:400;font-size:14px;color:#CFD7EA;">Practice Series</span></div>
    </div>
  </div>
  <div class="chapter-eyebrow">Calculus I · Review</div>
  <div class="chapter-title">Inverse Functions</div>
  <div class="chapter-sub">Theory Notes · Step-by-step Practice · Assessment</div><div class="chapter-credit">Follows Paul's Online Notes, Calculus I §1.2 Inverse Functions, including its Practice and Assignment Problems</div>
  <div class="chapter-progress">
    <div class="cp-track"><div class="cp-fill" id="cpFill"></div></div>
    <div class="cp-label" id="cpLabel">0% complete</div>
  </div>
  <div class="who-row"><button class="mode-pill" id="modePill" hidden>Choose a mode</button><span class="who" id="whoBar" hidden></span></div>
</header>

<nav class="tabbar"><div class="tabbar-inner" id="tabbar"></div></nav>
<div class="sec-sub" id="secSub"></div><div class="slide-progress"><div class="sp-track"><div class="sp-fill" id="spFill"></div></div><div class="sp-label" id="spLabel">Question 1 of 49</div></div>
<div class="wrap" id="wrap"></div>
<footer class="brandfoot">Brain &amp; Mind Academy · Sopaan Practice Series · Calculus I<br>Topics, practice problems and assignment problems from <i>Paul's Online Notes</i> (Paul Dawkins, Lamar University), Calculus I §1.2 Inverse Functions; these problems are tagged. Notes, other questions and all solutions are written by Brain &amp; Mind Academy.</footer>

<div class="navbar"><div class="navbar-inner" id="navbarInner"></div></div>
<button class="fab" id="paletteFab"><span>Questions</span><span class="fab-badge" id="fabBadge">0/49</span></button>

<div class="overlay" id="overlay">
  <div class="palette" role="dialog" aria-label="Question palette">
    <div class="palette-head"><h2 id="paletteTitle">Question palette</h2><button class="palette-close" id="paletteClose">&times;</button></div>
    <div class="palette-legend">
      <span><i class="dot current"></i>Current</span><span><i class="dot correct"></i>Correct</span>
      <span><i class="dot revealed"></i>Revealed</span><span><i class="dot skipped"></i>Skipped</span>
      <span><i class="dot locked"></i>Locked</span>
    </div>
    <div class="chip-grid" id="paletteBody"></div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
(function(){
"use strict";

/* ================= audio ================= */
var audioCtx=null;
function ensureAudio(){ if(!audioCtx){ try{ audioCtx=new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} } return audioCtx; }
function playTone(freqs,dur,type){
  var ctx=ensureAudio(); if(!ctx) return;
  try{
    var t0=ctx.currentTime;
    freqs.forEach(function(f,i){
      var o=ctx.createOscillator(), g=ctx.createGain();
      o.type=type||'sine'; o.frequency.value=f;
      var start=t0+i*dur;
      g.gain.setValueAtTime(0.0001,start);
      g.gain.exponentialRampToValueAtTime(0.16,start+0.02);
      g.gain.exponentialRampToValueAtTime(0.0001,start+dur);
      o.connect(g); g.connect(ctx.destination);
      o.start(start); o.stop(start+dur+0.02);
    });
  }catch(e){}
}
function playSuccess(){ playTone([523.25,659.25,783.99],0.11,'sine'); }
function playWrong(){ playTone([220,185],0.14,'square'); }
function playReveal(){ playTone([300,220],0.16,'triangle'); }

/* ================= helpers ================= */
function norm(s){
  return String(s===undefined||s===null?'':s).trim().toLowerCase().replace(/\s+/g,'')
    .replace(/[×∗*·]/g,'x').replace(/÷/g,'/').replace(/–|—|−/g,'-')
    .replace(/[²]/g,'^2').replace(/[³]/g,'^3').replace(/[⁴]/g,'^4').replace(/[⁵]/g,'^5')
    .replace(/[⁶]/g,'^6').replace(/[⁷]/g,'^7').replace(/[⁸]/g,'^8').replace(/[⁹]/g,'^9')
    .replace(/\^/g,'');
}
function parseNum(s){
  if(s===undefined||s===null) return null;
  var t=String(s).trim().replace(/,/g,'').replace(/[−–—]/g,'-').replace(/\s+/g,''); if(t==='') return null;
  var neg=false; if(t[0]==='-'){neg=true;t=t.slice(1);}
  var m=t.match(/^(\d+)\/(\d+)$/);
  if(m){ var v=parseInt(m[1],10)/parseInt(m[2],10); return neg?-v:v; }
  if(/^\d+(\.\d+)?$/.test(t)){ var v2=parseFloat(t); return neg?-v2:v2; }
  return null;
}
/* ---- expression checker: compares answers like (P-2w)/2 and P/2-w at random values ---- */
function exprPrep(s){
  return String(s).toLowerCase().replace(/\s+/g,'').replace(/^[a-z]\(x\)=/i,'').replace(/^[a-z]=/i,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/⁴/g,'^4').replace(/⁵/g,'^5').replace(/⁶/g,'^6').replace(/⁷/g,'^7').replace(/⁸/g,'^8').replace(/⁹/g,'^9').replace(/π/g,'#').replace(/pi/gi,'#').replace(/½/g,'(1/2)');
}
function exprCompile(src){
  var s=exprPrep(src), i=0, toks=[], absDepth=0;
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length && /[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(/[a-zA-Z#]/.test(ch)){ toks.push({k:'v',v:ch}); i++; continue; }
    if(ch==='|'){ var pv=toks[toks.length-1]; var opn=(absDepth===0)||!pv||('+-*/^(['.indexOf(pv.k)>=0); if(opn){ absDepth++; toks.push({k:'['}); } else { absDepth--; toks.push({k:']'}); } i++; continue; }
    if('+-*/^()'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  var out=[];
  for(var t=0;t<toks.length;t++){
    var a=toks[t], b=out[out.length-1];
    if(b && (b.k==='n'||b.k==='v'||b.k===')'||b.k===']') && (a.k==='n'||a.k==='v'||a.k==='('||a.k==='[')) out.push({k:'&'});
    out.push(a);
  }
  var p=0;
  function peek(){ return out[p]; }
  function parseE(){ var n=parseT(); while(peek() && (peek().k==='+'||peek().k==='-')){ var o=out[p++].k, r=parseT(); n=(function(l,r,o){return function(e){ return o==='+'?l(e)+r(e):l(e)-r(e); };})(n,r,o); } return n; }
  function parseI(){ var n=parseU(); while(peek() && peek().k==='&'){ p++; var r=parseP(); n=(function(l,r){return function(e){ return l(e)*r(e); };})(n,r); } return n; }
  function parseT(){ var n=parseI(); while(peek() && (peek().k==='*'||peek().k==='/')){ var o=out[p++].k, r=parseI(); n=(function(l,r,o){return function(e){ return o==='*'?l(e)*r(e):l(e)/r(e); };})(n,r,o); } return n; }
  function parseU(){ if(peek() && peek().k==='-'){ p++; var u=parseU(); return function(e){ return -u(e); }; } if(peek() && peek().k==='+'){ p++; return parseU(); } return parseP(); }
  function parseP(){ var b=parseA(); if(peek() && peek().k==='^'){ p++; var x=parseU(); return function(e){ return Math.pow(b(e),x(e)); }; } return b; }
  function parseA(){
    var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){ return t.v; };
    if(t.k==='v') return t.v==='#' ? function(){ return Math.PI; } : function(e){ return e[t.v]; };
    if(t.k==='('){ var n=parseE(); if(!peek()||peek().k!==')') throw 0; p++; return n; }
    if(t.k==='['){ var m=parseE(); if(!peek()||peek().k!==']') throw 0; p++; return function(e){ return Math.abs(m(e)); }; }
    throw 0;
  }
  try{ var f=parseE(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function exprEqual(input,answer){
  var f=exprCompile(input), g=exprCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<8;trial++){
    var env={}; 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=1.3+Math.random()*4.1; });
    var x=f(env), y=g(env);
    if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-7*Math.max(1,Math.abs(x),Math.abs(y))) return false;
    hits++;
  }
  return hits>=3;
}
function wordsNorm(s){ return String(s||'').toLowerCase().replace(/\band\b/g,' ').replace(/[^a-z]/g,''); }
function listNorm(s){ return (String(s||'').replace(/[−–—]/g,'-').replace(/(\d) (?=\d{3}\b)/g,'$1').match(/-?\d+(\.\d+)?/g)||[]).join(','); }
function powNorm(s){ return String(s||'').toLowerCase().replace(/\s+/g,'').replace(/[×∗*·.]/g,'x').replace(/[⁰¹²³⁴⁵⁶⁷⁸⁹]+/g,function(m){ return '^'+m.split('').map(function(c){ return '⁰¹²³⁴⁵⁶⁷⁸⁹'.indexOf(c); }).join(''); }).replace(/\^1(?!\d)/g,''); }
function fr(s){ return String(s).replace(/\{(\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>').replace(/\{(\d+)\/(\d+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); }
function gcdI(a,b){ a=Math.abs(a); b=Math.abs(b); while(b){ var t=a%b; a=b; b=t; } return a; }
function fracParse(s){ s=String(s===undefined||s===null?'':s).trim().replace(/[\u2044\u2215\u00f7]/g,'/').replace(/\s+/g,' ').replace(/\s*\/\s*/g,'/'); var m;
  if((m=s.match(/^(-?\d+)$/))) return {v:+m[1],form:'int',n:+m[1],d:1};
  if((m=s.match(/^(-?\d+)\/(\d+)$/))){ if(+m[2]===0) return null; return {v:m[1]/m[2],form:'frac',n:+m[1],d:+m[2]}; }
  if((m=s.match(/^(-?)(\d+)(?: |\+)(\d+)\/(\d+)$/))){ if(+m[4]===0) return null; var sg=m[1]?-1:1; return {v:sg*(+m[2]+m[3]/m[4]),form:'mixed',w:sg*m[2],n:+m[3],d:+m[4]}; }
  if((m=s.match(/^-?\d*\.\d+$/))) return {v:parseFloat(s),form:'dec'};
  return null; }
function fracOK(mode,input,answer){
  if(mode==='flist'){ var A=String(input).split(/[,;]/).map(function(x){return x.trim();}).filter(Boolean), K=String(answer).split(/[,;]/).map(function(x){return x.trim();});
    if(A.length!==K.length) return false; return A.every(function(x,i){ var a=fracParse(x), k=fracParse(K[i]); return a&&k&&Math.abs(a.v-k.v)<1e-9; }); }
  var a=fracParse(input), k=fracParse(answer); if(!a||!k) return false;
  var same=Math.abs(a.v-k.v)<1e-9; if(!same) return false;
  if(mode==='fv') return true;
  if(mode==='dec') return a.form==='dec'||a.form==='int';
  if(mode==='fe') return (a.form==='frac'&&k.form==='frac'&&a.n===k.n&&a.d===k.d)||(a.form==='int'&&k.form==='int');
  if(mode==='fi') return a.form==='frac'||(a.form==='int'&&k.form==='int');
  if(mode==='fl') return a.form==='int'||(a.form==='frac'&&gcdI(a.n,a.d)===1)||(a.form==='mixed'&&a.n<a.d&&gcdI(a.n,a.d)===1);
  if(mode==='fm') return a.form==='int'||(a.form==='mixed'&&a.n>0&&a.n<a.d&&gcdI(a.n,a.d)===1);
  return false; }
function answerMatches(input,answer,accept,expr){
  if(expr==='dec'||expr==='fv'||expr==='fe'||expr==='fl'||expr==='fm'||expr==='fi'||expr==='flist'){ if(input===undefined||input===null||String(input).trim()==='') return false; return fracOK(expr,input,answer); }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  if(expr==='words'){ return [answer].concat(accept||[]).some(function(a){ if(/\d/.test(a)) return norm(a)===norm(input); var w=wordsNorm(a); return w!=='' && w===wordsNorm(input); }); }
  if(expr==='list'){ return [answer].concat(accept||[]).some(function(a){ return listNorm(a)===listNorm(input); }); }
  if(expr==='pow'){ return [answer].concat(accept||[]).some(function(a){ return powNorm(a)===powNorm(input); }); }
  if(expr==='time'){ var tn=function(x){ var t=String(x).toLowerCase().replace(/[\s.]/g,'').replace(/[:h]/g,''); if(/^\d{3}(am|pm)?$/.test(t)) t='0'+t; return t; }; return [answer].concat(accept||[]).some(function(a){ return tn(a)===tn(input); }); }
  if(expr==='glist'){ var gn=function(x){ return String(x).toUpperCase().split(/[\s,;]+/).filter(Boolean).sort().join(','); }; return [answer].concat(accept||[]).some(function(a){ return gn(a)===gn(input); }); }
  if(expr==='coord'){ var cn=function(x){ return String(x).replace(/[\u2212\u2013\u2014]/g,'-').replace(/[\s()\[\]]/g,''); }; return [answer].concat(accept||[]).some(function(a){ return cn(a)===cn(input); }); }
  if(expr==='dlist'){ var dn=function(x){ return (String(x).replace(/[−–—]/g,'-').match(/-?\d*\.?\d+/g)||[]).map(Number).join(','); }; return [answer].concat(accept||[]).some(function(a){ return dn(a)===dn(input); }); }
  if(expr==='set'){ var sn=function(x){ return (String(x).match(/-?\d+/g)||[]).map(Number).sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return sn(a)===sn(input); }); }
  if(expr==='primes'){ var pn=function(x){ var t=powNorm(x).replace(/[^0-9x^]/g,''); var out=[]; t.split('x').forEach(function(tok){ if(!tok) return; var m=tok.split('^'); var b=+m[0], e=m[1]?+m[1]:1; for(var i=0;i<e;i++) out.push(b); }); return out.sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return pn(a)===pn(input); }); }
  if(expr==='angle'){ var an=function(x){ return String(x).toUpperCase().replace(/[^A-Z]/g,''); }; var k=an(answer), v=an(input); return v===k || v===k.split('').reverse().join(''); }
  if(expr==='trans'){ var tv=function(x){ var s=String(x).toLowerCase().replace(/[−–—]/g,'-').replace(/\b(units?|squares?|and|then|steps?|to|the|a)\b/g,' ').replace(/[,;.]/g,' '); var re=/(\d+)\s*(right|left|up|down|r|l|u|d)\b/g, m, dx=0, dy=0, n=0; while((m=re.exec(s))){ var v=+m[1], d=m[2][0]; if(d==='r')dx+=v; else if(d==='l')dx-=v; else if(d==='u')dy+=v; else dy-=v; n++; } if(!n||s.replace(re,'').replace(/\s+/g,'')!=='') return null; return dx+','+dy; }; var ti=tv(input); return ti!==null && [answer].concat(accept||[]).some(function(a){ return tv(a)===ti; }); }
  if(expr==='rot'){ var rv=function(x){ var s=String(x).toLowerCase().replace(/quarter[\s-]*turn/g,'90').replace(/half[\s-]*turn/g,'180').replace(/three[\s-]*quarter[\s-]*turn/g,'270'); var m=s.match(/\b(90|180|270)\b/); if(!m) return null; var a=+m[1]; if(a===180) return '180'; var dir=/anti|counter|acw|ccw/.test(s)?-1:(/clockwise|\bcw\b/.test(s)?1:0); if(!dir) return null; return String(((a*dir)%360+360)%360); }; var ri=rv(input); return ri!==null && ri===rv(answer); }
  if(expr==='expanded'){ var f=function(x){ return String(x).replace(/\s+/g,'').replace(/,/g,''); }; return [answer].concat(accept||[]).some(function(a){ return f(a)===f(input); }); }
  if(expr===true && input!==undefined && input!==null && String(input).trim()!==''){
    if(exprEqual(input,answer)) return true;
    var alt=String(input).replace(/\/\s*(\d+(?:\.\d+)?)\s*([a-zA-Z(])/g,'/$1*$2'); if(alt!==String(input) && exprEqual(alt,answer)) return true;
    return (accept||[]).some(function(a){ return exprEqual(input,a); });
  }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  var n1=parseNum(input), n2=parseNum(answer);
  if(n1!==null && n2!==null){ if(Math.abs(n1-n2)<1e-3) return true; return (accept||[]).some(function(a){ var n3=parseNum(a); return n3!==null && Math.abs(n1-n3)<1e-3; }); }
  var cands=[answer].concat(accept||[]); var ni=norm(input);
  for(var i=0;i<cands.length;i++){ if(norm(cands[i])===ni) return true; }
  return false;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;'); }

/* ================= DATA ================= */
var AR_OPTIONS = ["Both A and R are true, and R is the correct explanation of A","Both A and R are true, but R is NOT the correct explanation of A","A is true but R is false","A is false but R is true"];
var THEORY = "<div class=\"hub\"><div class=\"hub-card\"><h3>📖 Notes</h3><p>Start with the introduction, then read one note per practice sheet. Each note has the idea, worked examples, graphs where they help and a common-mistakes box.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-jump=\"nintro\">Introduction</button><button class=\"hub-btn\" data-jump=\"n1\">1 · One-to-one & notation</button><button class=\"hub-btn\" data-jump=\"n2\">2 · Linear inverses</button><button class=\"hub-btn\" data-jump=\"n3\">3 · Powers & roots</button><button class=\"hub-btn\" data-jump=\"n4\">4 · Rational inverses</button><button class=\"hub-btn\" data-jump=\"n5\">5 · Verifying by composition</button><button class=\"hub-btn\" data-jump=\"n6\">6 · Graphs, domain & range</button><button class=\"hub-btn\" data-jump=\"nsum\">Checklist</button></div></div><div class=\"hub-card\"><h3>🎯 Practice</h3><p>Six sheets of multiple-choice and step-by-step questions, including all 16 Practice and Assignment Problems from Paul's Online Notes §1.2 (tagged <b>Paul</b>).</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s1\">1 · One-to-one & notation</button><button class=\"hub-btn\" data-go=\"s2\">2 · Linear inverses</button><button class=\"hub-btn\" data-go=\"s3\">3 · Powers & roots</button><button class=\"hub-btn\" data-go=\"s4\">4 · Rational inverses</button><button class=\"hub-btn\" data-go=\"s5\">5 · Verifying by composition</button><button class=\"hub-btn\" data-go=\"s6\">6 · Graphs, domain & range</button></div></div><div class=\"hub-card\"><h3>📝 Assessment</h3><p>Four short assessments with new problems, one for each skill area. Take them in Quiz mode, then open your report.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s7\">A · Knowing and understanding</button><button class=\"hub-btn\" data-go=\"s8\">B · Investigating patterns</button><button class=\"hub-btn\" data-go=\"s9\">C · Communicating</button><button class=\"hub-btn\" data-go=\"s10\">D · Applying mathematics in real-life contexts</button><button class=\"hub-btn primary\" data-go=\"report\">📊 View my report</button></div></div></div><section class=\"note\" id=\"nintro\"><h2>Inverse functions: introduction</h2><p>A function is a rule that turns an input into an output. An <b>inverse function</b> runs the rule backwards: it takes the output and gives back the input. If f turns 2 into 7, then f⁻¹ turns 7 back into 2.</p><p><b>Undoing.</b> Take f(x) = 3x − 2 and g(x) = x/3 + 2/3. Then f(4) = 10 and g(10) = 10/3 + 2/3 = 4: g brings us back. In general g(f(x)) = (3x − 2)/3 + 2/3 = x and f(g(x)) = 3(x/3 + 2/3) − 2 = x. Whichever order we use, we get x back. Two functions that undo each other like this are <b>inverses</b>.</p><p><b>Why it matters.</b> Converting °C to °F and back, finding the distance from a taxi fare, decoding a message, and later in calculus the logarithm (the inverse of the exponential) and the inverse trig functions all rely on the same idea.</p><div class=\"keybox\"><b>Finding the inverse of a one-to-one function f</b><br>1. Replace f(x) with y.<br>2. Swap x and y.<br>3. Solve the new equation for y. <i>This is the step where most errors happen.</i><br>4. Replace y with f⁻¹(x).<br>5. Verify by composition: (f∘f⁻¹)(x) = x and (f⁻¹∘f)(x) = x. In this course one of the two is usually enough.</div><h4>Topic map</h4><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Topic</th><th>Subtopics</th><th>Learning objectives</th></tr><tr><td>1 · One-to-one &amp; notation</td><td>tables, mappings, formulas, graphs; horizontal line test; restricting a domain; f⁻¹ vs 1/f</td><td>I can decide whether a function is one-to-one from a table, a mapping, a formula or a graph (horizontal line test), restrict a domain to make it one-to-one, and read f⁻¹ values, knowing that f⁻¹(x) is not 1/f(x).</td></tr><tr><td>2 · Linear inverses</td><td>the five-step procedure; undoing in reverse order; checking</td><td>I can find the inverse of a linear function with the five-step procedure and check it.</td></tr><tr><td>3 · Powers &amp; roots</td><td>cubes, fifth and seventh powers and roots; reverse order of operations</td><td>I can invert functions built from powers and odd roots by undoing the operations in reverse order.</td></tr><tr><td>4 · Rational inverses</td><td>clear the fraction, collect y terms, factor; excluded values</td><td>I can invert a rational function by clearing the fraction, collecting the y terms on one side and factoring out y.</td></tr><tr><td>5 · Verifying by composition</td><td>f(g(x)) and g(f(x)); one composition is usually enough; spotting errors</td><td>I can compute f(g(x)) and g(f(x)) to decide whether two functions are inverses, and spot errors in a verification.</td></tr><tr><td>6 · Graphs, domain &amp; range</td><td>reflection in y = x; (a, b) ↦ (b, a); domain of f⁻¹ = range of f; restricted domains</td><td>I can sketch f⁻¹ by reflecting f in y = x, swap points, and state the domain and range of f⁻¹, including on a restricted domain.</td></tr></table></div><h4>Typing answers</h4><ul><li>Type just the expression for f⁻¹(x), e.g. <span class=\"mono\">(x-15)/6</span>. Any equivalent form is accepted.</li><li>Bracket whole numerators and denominators: <span class=\"mono\">(4x-1)/(x+9)</span>, not 4x-1/x+9.</li><li>For roots the sheet prints the root sign; you type only what goes inside it.</li><li>Values such as f⁻¹(7) may be typed as fractions like <span class=\"mono\">5/3</span>; points as <span class=\"mono\">(4, 1)</span>.</li></ul></section><section class=\"note\" id=\"n1\"><h2>1 · One-to-one & notation</h2><p class=\"lt\"><b>Learning target:</b> I can decide whether a function is one-to-one from a table, a mapping, a formula or a graph (horizontal line test), restrict a domain to make it one-to-one, and read f⁻¹ values, knowing that f⁻¹(x) is not 1/f(x).</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Decide whether a function is one-to-one from a table, a mapping diagram, a formula or a graph.</li><li>✔ Use the horizontal line test.</li><li>✔ Restrict a domain so a function becomes one-to-one.</li><li>✔ Read values of f⁻¹ and explain why f⁻¹(x) ≠ 1/f(x).</li></ul><p>A function is <b>one-to-one</b> if different inputs always give different outputs: whenever x₁ ≠ x₂, f(x₁) ≠ f(x₂). Only one-to-one functions have inverses, because the inverse has to send each output back to <i>one</i> input.</p><h4>Four ways to check</h4><ul><li><b>Table or mapping:</b> look for a repeated output. If two inputs share an output, f is not one-to-one.</li><li><b>Formula:</b> find two inputs with the same output (for x², f(−3) = f(3) = 9), or show that f(a) = f(b) forces a = b.</li><li><b>Graph: the horizontal line test.</b> f is one-to-one exactly when no horizontal line cuts its graph more than once. (The vertical line test checks that a graph is a function at all; the horizontal line test checks one-to-one.)</li><li><b>Always increasing or always decreasing</b> functions, such as 5x − 1, x³ and ⁷√x, pass the test.</li></ul><div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"The parabola y = x squared cut twice by the horizontal line y = 4\"><line class=\"tk\" x1=\"25.8\" y1=\"264.0\" x2=\"25.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"64.9\" y1=\"264.0\" x2=\"64.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"103.9\" y1=\"264.0\" x2=\"103.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"182.1\" y1=\"264.0\" x2=\"182.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"221.1\" y1=\"264.0\" x2=\"221.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"260.2\" y1=\"264.0\" x2=\"260.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"256.2\" x2=\"268.0\" y2=\"256.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"178.1\" x2=\"268.0\" y2=\"178.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"99.9\" x2=\"268.0\" y2=\"99.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"60.9\" x2=\"268.0\" y2=\"60.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"21.8\" x2=\"268.0\" y2=\"21.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\"/><line class=\"ln\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"212.1\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"149.0\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"64.9\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"221.1\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"139.0\" y=\"143.0\" text-anchor=\"end\" style=\"font-size:10px\">2</text><line class=\"arm hid\" x1=\"18.0\" y1=\"60.9\" x2=\"268.0\" y2=\"60.9\"/><text class=\"al\" x=\"266.0\" y=\"75.9\" text-anchor=\"end\" style=\"font-size:11px\">y = 4</text><polyline class=\"arm\" points=\"54.1,14.9 54.8,18.0 55.5,21.1 56.2,24.2 56.9,27.3 57.6,30.3 58.3,33.4 59.0,36.4 59.7,39.3 60.4,42.3 61.1,45.2 61.8,48.1 62.4,51.0 63.1,53.9 63.8,56.7 64.5,59.5 65.2,62.3 65.9,65.0 66.6,67.7 67.3,70.4 68.0,73.1 68.7,75.8 69.4,78.4 70.1,81.0 70.8,83.6 71.5,86.1 72.2,88.7 72.9,91.2 73.6,93.7 74.2,96.1 74.9,98.6 75.6,101.0 76.3,103.3 77.0,105.7 77.7,108.0 78.4,110.3 79.1,112.6 79.8,114.9 80.5,117.1 81.2,119.3 81.9,121.5 82.6,123.7 83.3,125.8 84.0,127.9 84.7,130.0 85.4,132.1 86.1,134.1 86.8,136.1 87.4,138.1 88.1,140.1 88.8,142.0 89.5,143.9 90.2,145.8 90.9,147.7 91.6,149.5 92.3,151.3 93.0,153.1 93.7,154.9 94.4,156.6 95.1,158.3 95.8,160.0 96.5,161.7 97.2,163.3 97.9,165.0 98.6,166.6 99.2,168.1 99.9,169.7 100.6,171.2 101.3,172.7 102.0,174.1 102.7,175.6 103.4,177.0 104.1,178.4 104.8,179.8 105.5,181.1 106.2,182.4 106.9,183.7 107.6,185.0 108.3,186.3 109.0,187.5 109.7,188.7 110.4,189.9 111.1,191.0 111.8,192.1 112.4,193.2 113.1,194.3 113.8,195.3 114.5,196.4 115.2,197.4 115.9,198.3 116.6,199.3 117.3,200.2 118.0,201.1 118.7,202.0 119.4,202.9 120.1,203.7 120.8,204.5 121.5,205.3 122.2,206.0 122.9,206.7 123.6,207.4 124.3,208.1 124.9,208.8 125.6,209.4 126.3,210.0 127.0,210.6 127.7,211.1 128.4,211.7 129.1,212.2 129.8,212.7 130.5,213.1 131.2,213.6 131.9,214.0 132.6,214.3 133.3,214.7 134.0,215.0 134.7,215.3 135.4,215.6 136.1,215.9 136.8,216.1 137.4,216.3 138.1,216.5 138.8,216.7 139.5,216.8 140.2,216.9 140.9,217.0 141.6,217.1 142.3,217.1 143.0,217.1 143.7,217.1 144.4,217.1 145.1,217.0 145.8,216.9 146.5,216.8 147.2,216.7 147.9,216.5 148.6,216.3 149.2,216.1 149.9,215.9 150.6,215.6 151.3,215.3 152.0,215.0 152.7,214.7 153.4,214.3 154.1,214.0 154.8,213.6 155.5,213.1 156.2,212.7 156.9,212.2 157.6,211.7 158.3,211.1 159.0,210.6 159.7,210.0 160.4,209.4 161.1,208.8 161.8,208.1 162.4,207.4 163.1,206.7 163.8,206.0 164.5,205.3 165.2,204.5 165.9,203.7 166.6,202.9 167.3,202.0 168.0,201.1 168.7,200.2 169.4,199.3 170.1,198.3 170.8,197.4 171.5,196.4 172.2,195.3 172.9,194.3 173.6,193.2 174.2,192.1 174.9,191.0 175.6,189.9 176.3,188.7 177.0,187.5 177.7,186.3 178.4,185.0 179.1,183.7 179.8,182.4 180.5,181.1 181.2,179.8 181.9,178.4 182.6,177.0 183.3,175.6 184.0,174.1 184.7,172.7 185.4,171.2 186.1,169.7 186.8,168.1 187.4,166.6 188.1,165.0 188.8,163.3 189.5,161.7 190.2,160.0 190.9,158.3 191.6,156.6 192.3,154.9 193.0,153.1 193.7,151.3 194.4,149.5 195.1,147.7 195.8,145.8 196.5,143.9 197.2,142.0 197.9,140.1 198.6,138.1 199.3,136.1 199.9,134.1 200.6,132.1 201.3,130.0 202.0,127.9 202.7,125.8 203.4,123.7 204.1,121.5 204.8,119.3 205.5,117.1 206.2,114.9 206.9,112.6 207.6,110.3 208.3,108.0 209.0,105.7 209.7,103.3 210.4,101.0 211.1,98.6 211.8,96.1 212.4,93.7 213.1,91.2 213.8,88.7 214.5,86.1 215.2,83.6 215.9,81.0 216.6,78.4 217.3,75.8 218.0,73.1 218.7,70.4 219.4,67.7 220.1,65.0 220.8,62.3 221.5,59.5 222.2,56.7 222.9,53.9 223.6,51.0 224.2,48.1 224.9,45.2 225.6,42.3 226.3,39.3 227.0,36.4 227.7,33.4 228.4,30.3 229.1,27.3 229.8,24.2 230.5,21.1 231.2,18.0 231.9,14.9\"/><text class=\"al\" x=\"202.7\" y=\"134.6\" text-anchor=\"start\" style=\"font-size:12px\">y = x²</text><circle class=\"pt\" cx=\"64.9\" cy=\"60.9\" r=\"3.2\"/><text class=\"lb\" x=\"58.9\" y=\"54.9\" text-anchor=\"end\" style=\"font-size:11px\">(−2, 4)</text><circle class=\"pt\" cx=\"221.1\" cy=\"60.9\" r=\"3.2\"/><text class=\"lb\" x=\"227.1\" y=\"54.9\" text-anchor=\"start\" style=\"font-size:11px\">(2, 4)</text></svg></div><p><b>Restricting the domain.</b> y = x² fails the test (y = 4 cuts it at x = −2 and x = 2). If we keep only x ≥ 0, every horizontal line cuts it at most once, and the restricted function has the inverse √x.</p><div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"Half parabola for x at least 0 and its reflection, the square root graph, in y = x\"><line class=\"tk\" x1=\"25.8\" y1=\"264.0\" x2=\"25.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"64.9\" y1=\"264.0\" x2=\"64.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"103.9\" y1=\"264.0\" x2=\"103.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"182.1\" y1=\"264.0\" x2=\"182.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"221.1\" y1=\"264.0\" x2=\"221.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"260.2\" y1=\"264.0\" x2=\"260.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"256.2\" x2=\"268.0\" y2=\"256.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"178.1\" x2=\"268.0\" y2=\"178.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"99.9\" x2=\"268.0\" y2=\"99.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"60.9\" x2=\"268.0\" y2=\"60.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"21.8\" x2=\"268.0\" y2=\"21.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\"/><line class=\"ln\" x1=\"64.9\" y1=\"264.0\" x2=\"64.9\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"212.1\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"70.9\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"143.0\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"221.1\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"60.9\" y=\"143.0\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"60.9\" y=\"64.9\" text-anchor=\"end\" style=\"font-size:10px\">4</text><line class=\"ln hid\" x1=\"18.0\" y1=\"264.0\" x2=\"268.0\" y2=\"14.0\"/><text class=\"lb\" x=\"248.0\" y=\"26.0\" text-anchor=\"end\" style=\"font-size:11px\">y = x</text><polyline class=\"arm\" points=\"65.2,217.1 65.9,217.1 66.6,217.0 67.3,217.0 68.0,216.9 68.7,216.8 69.4,216.6 70.1,216.4 70.8,216.2 71.5,216.0 72.2,215.8 72.9,215.5 73.6,215.2 74.2,214.9 74.9,214.5 75.6,214.2 76.3,213.8 77.0,213.3 77.7,212.9 78.4,212.4 79.1,211.9 79.8,211.4 80.5,210.9 81.2,210.3 81.9,209.7 82.6,209.1 83.3,208.5 84.0,207.8 84.7,207.1 85.4,206.4 86.1,205.6 86.8,204.9 87.4,204.1 88.1,203.3 88.8,202.4 89.5,201.6 90.2,200.7 90.9,199.8 91.6,198.8 92.3,197.9 93.0,196.9 93.7,195.9 94.4,194.8 95.1,193.8 95.8,192.7 96.5,191.6 97.2,190.4 97.9,189.3 98.6,188.1 99.2,186.9 99.9,185.6 100.6,184.4 101.3,183.1 102.0,181.8 102.7,180.5 103.4,179.1 104.1,177.7 104.8,176.3 105.5,174.9 106.2,173.4 106.9,171.9 107.6,170.4 108.3,168.9 109.0,167.3 109.7,165.8 110.4,164.2 111.1,162.5 111.8,160.9 112.4,159.2 113.1,157.5 113.8,155.8 114.5,154.0 115.2,152.2 115.9,150.4 116.6,148.6 117.3,146.8 118.0,144.9 118.7,143.0 119.4,141.0 120.1,139.1 120.8,137.1 121.5,135.1 122.2,133.1 122.9,131.0 123.6,129.0 124.3,126.9 124.9,124.8 125.6,122.6 126.3,120.4 127.0,118.2 127.7,116.0 128.4,113.8 129.1,111.5 129.8,109.2 130.5,106.9 131.2,104.5 131.9,102.2 132.6,99.8 133.3,97.3 134.0,94.9 134.7,92.4 135.4,89.9 136.1,87.4 136.8,84.9 137.4,82.3 138.1,79.7 138.8,77.1 139.5,74.5 140.2,71.8 140.9,69.1 141.6,66.4 142.3,63.6 143.0,60.9 143.7,58.1 144.4,55.3 145.1,52.4 145.8,49.6 146.5,46.7 147.2,43.8 147.9,40.8 148.6,37.9 149.2,34.9 149.9,31.9 150.6,28.8 151.3,25.8 152.0,22.7 152.7,19.6 153.4,16.4\"/><text class=\"al\" x=\"141.0\" y=\"31.6\" text-anchor=\"end\" style=\"font-size:12px\">x², x ≥ 0</text><polyline class=\"ln\" points=\"65.2,213.4 65.9,210.7 66.6,208.9 67.3,207.4 68.0,206.1 68.7,204.9 69.4,203.8 70.1,202.9 70.8,201.9 71.5,201.1 72.2,200.2 72.9,199.5 73.6,198.7 74.2,198.0 74.9,197.3 75.6,196.6 76.3,196.0 77.0,195.3 77.7,194.7 78.4,194.1 79.1,193.5 79.8,193.0 80.5,192.4 81.2,191.9 81.9,191.3 82.6,190.8 83.3,190.3 84.0,189.8 84.7,189.3 85.4,188.8 86.1,188.4 86.8,187.9 87.4,187.4 88.1,187.0 88.8,186.5 89.5,186.1 90.2,185.7 90.9,185.2 91.6,184.8 92.3,184.4 93.0,184.0 93.7,183.6 94.4,183.2 95.1,182.8 95.8,182.4 96.5,182.0 97.2,181.6 97.9,181.2 98.6,180.9 99.2,180.5 99.9,180.1 100.6,179.7 101.3,179.4 102.0,179.0 102.7,178.7 103.4,178.3 104.1,178.0 104.8,177.6 105.5,177.3 106.2,176.9 106.9,176.6 107.6,176.3 108.3,175.9 109.0,175.6 109.7,175.3 110.4,175.0 111.1,174.7 111.8,174.3 112.4,174.0 113.1,173.7 113.8,173.4 114.5,173.1 115.2,172.8 115.9,172.5 116.6,172.2 117.3,171.9 118.0,171.6 118.7,171.3 119.4,171.0 120.1,170.7 120.8,170.4 121.5,170.1 122.2,169.8 122.9,169.5 123.6,169.2 124.3,169.0 124.9,168.7 125.6,168.4 126.3,168.1 127.0,167.9 127.7,167.6 128.4,167.3 129.1,167.0 129.8,166.8 130.5,166.5 131.2,166.2 131.9,166.0 132.6,165.7 133.3,165.4 134.0,165.2 134.7,164.9 135.4,164.7 136.1,164.4 136.8,164.1 137.4,163.9 138.1,163.6 138.8,163.4 139.5,163.1 140.2,162.9 140.9,162.6 141.6,162.4 142.3,162.1 143.0,161.9 143.7,161.6 144.4,161.4 145.1,161.2 145.8,160.9 146.5,160.7 147.2,160.4 147.9,160.2 148.6,160.0 149.2,159.7 149.9,159.5 150.6,159.2 151.3,159.0 152.0,158.8 152.7,158.5 153.4,158.3 154.1,158.1 154.8,157.9 155.5,157.6 156.2,157.4 156.9,157.2 157.6,156.9 158.3,156.7 159.0,156.5 159.7,156.3 160.4,156.1 161.1,155.8 161.8,155.6 162.4,155.4 163.1,155.2 163.8,155.0 164.5,154.7 165.2,154.5 165.9,154.3 166.6,154.1 167.3,153.9 168.0,153.7 168.7,153.4 169.4,153.2 170.1,153.0 170.8,152.8 171.5,152.6 172.2,152.4 172.9,152.2 173.6,152.0 174.2,151.8 174.9,151.6 175.6,151.3 176.3,151.1 177.0,150.9 177.7,150.7 178.4,150.5 179.1,150.3 179.8,150.1 180.5,149.9 181.2,149.7 181.9,149.5 182.6,149.3 183.3,149.1 184.0,148.9 184.7,148.7 185.4,148.5 186.1,148.3 186.8,148.1 187.4,147.9 188.1,147.7 188.8,147.5 189.5,147.3 190.2,147.2 190.9,147.0 191.6,146.8 192.3,146.6 193.0,146.4 193.7,146.2 194.4,146.0 195.1,145.8 195.8,145.6 196.5,145.4 197.2,145.2 197.9,145.1 198.6,144.9 199.3,144.7 199.9,144.5 200.6,144.3 201.3,144.1 202.0,143.9 202.7,143.7 203.4,143.6 204.1,143.4 204.8,143.2 205.5,143.0 206.2,142.8 206.9,142.6 207.6,142.5 208.3,142.3 209.0,142.1 209.7,141.9 210.4,141.7 211.1,141.6 211.8,141.4 212.4,141.2 213.1,141.0 213.8,140.8 214.5,140.7 215.2,140.5 215.9,140.3 216.6,140.1 217.3,140.0 218.0,139.8 218.7,139.6 219.4,139.4 220.1,139.3 220.8,139.1 221.5,138.9 222.2,138.7 222.9,138.6 223.6,138.4 224.2,138.2 224.9,138.1 225.6,137.9 226.3,137.7 227.0,137.5 227.7,137.4 228.4,137.2 229.1,137.0 229.8,136.9 230.5,136.7 231.2,136.5 231.9,136.4 232.6,136.2 233.3,136.0 234.0,135.9 234.7,135.7 235.4,135.5 236.1,135.4 236.8,135.2 237.4,135.0 238.1,134.9 238.8,134.7 239.5,134.5 240.2,134.4 240.9,134.2 241.6,134.0 242.3,133.9 243.0,133.7 243.7,133.5 244.4,133.4 245.1,133.2 245.8,133.1 246.5,132.9 247.2,132.7 247.9,132.6 248.6,132.4 249.3,132.3 249.9,132.1 250.6,131.9 251.3,131.8 252.0,131.6 252.7,131.5 253.4,131.3 254.1,131.1 254.8,131.0 255.5,130.8 256.2,130.7 256.9,130.5 257.6,130.4 258.3,130.2 259.0,130.1 259.7,129.9 260.4,129.7 261.1,129.6 261.8,129.4 262.4,129.3 263.1,129.1 263.8,129.0 264.5,128.8 265.2,128.7 265.9,128.5 266.6,128.4 267.3,128.2 268.0,128.0\"/><text class=\"lb\" x=\"264.1\" y=\"113.6\" text-anchor=\"end\" style=\"font-size:12px\">y = √x</text><circle class=\"pt\" cx=\"143.0\" cy=\"60.9\" r=\"3.2\"/><text class=\"lb\" x=\"149.0\" y=\"64.9\" text-anchor=\"start\" style=\"font-size:11px\">(2, 4)</text><circle class=\"pt\" cx=\"221.1\" cy=\"139.0\" r=\"3.2\"/><text class=\"lb\" x=\"225.1\" y=\"153.0\" text-anchor=\"start\" style=\"font-size:11px\">(4, 2)</text></svg></div><h4>Notation</h4><p>For one-to-one f and g, g is the inverse of f when (f∘g)(x) = x and (g∘f)(x) = x. We write g = f⁻¹, read \"f inverse\". If f(a) = b then f⁻¹(b) = a: the inverse swaps the roles of input and output.</p><div class=\"keybox\"><b>f⁻¹(x) ≠ 1/f(x).</b> The −1 is a label, not an exponent. For f(x) = 2x + 6, f⁻¹(x) = (x − 6)/2, so f⁻¹(2) = −2, while 1/f(2) = 1/10. If you want the reciprocal, write [f(x)]⁻¹ or 1/f(x).</div><div class=\"ex\"><div class=\"exh\">Worked example 1 · Reading f⁻¹ from a table</div><div class=\"exl\">x: 0, 1, 2, 3 and k(x): 4, 7, 12, 19. All outputs are different, so k is one-to-one.<br>k(2) = 12, so <b>k⁻¹(12) = 2</b>.  k(0) = 4, so <b>k⁻¹(4) = 0</b>.<br>k⁻¹(k(3)) = k⁻¹(19) = 3: the inverse undoes k.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Restricting a domain</div><div class=\"exl\">f(x) = (x + 1)² is not one-to-one: f(−3) = f(1) = 4.<br>The vertex is at x = −1. Keeping <b>x ≥ −1</b> (the right half of the parabola) makes f one-to-one, and the largest such domain containing x = 0 is x ≥ −1.</div></div><div class=\"keybox\"><b>Common mistakes.</b> Using the vertical line test to decide one-to-one. Saying \"f(0) ≠ f(1), so f is one-to-one\": two values prove nothing; you need <i>every</i> pair. Restricting (x − 2)² to x ≥ 0 instead of x ≥ 2 (it still repeats: f(1) = f(3)). Reading f⁻¹(5) as f(5).</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s1\">Practise 1 →</button></div></section><section class=\"note\" id=\"n2\"><h2>2 · Linear inverses</h2><p class=\"lt\"><b>Learning target:</b> I can find the inverse of a linear function with the five-step procedure and check it.</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Use the five-step procedure on linear functions.</li><li>✔ Undo the operations of f in reverse order.</li><li>✔ Verify an inverse with one composition or a numerical check.</li></ul><p>A linear function f(x) = mx + b (m ≠ 0) is always one-to-one, so it always has an inverse. The procedure finds it in five steps.</p><div class=\"keybox\"><b>Finding the inverse of a one-to-one function f</b><br>1. Replace f(x) with y.<br>2. Swap x and y.<br>3. Solve the new equation for y. <i>This is the step where most errors happen.</i><br>4. Replace y with f⁻¹(x).<br>5. Verify by composition: (f∘f⁻¹)(x) = x and (f⁻¹∘f)(x) = x. In this course one of the two is usually enough.</div><p><b>Why swap x and y?</b> The inverse sends outputs to inputs. Swapping x and y writes exactly that: the old output becomes the new input. Solving for y then gives the rule of f⁻¹.</p><div class=\"keybox\"><b>Where students go wrong in step 3</b><br><b>Roots and powers: undo in reverse order.</b> f(x) = 2(x − 1)³ + 5 is built as: subtract 1, cube, multiply by 2, add 5. To undo it, go backwards: subtract 5, divide by 2, take the cube root, add 1. So f⁻¹(x) = 1 + ∛((x − 5)/2), not ∛(x/2 − 5) + 1.<br><b>Rational functions: collect the y terms and factor.</b> After swapping, x = (2y + 3)/(y − 4). Multiply out: xy − 4x = 2y + 3. Put every y term on one side and everything else on the other: xy − 2y = 4x + 3. Factor: y(x − 2) = 4x + 3, so y = (4x + 3)/(x − 2). You cannot \"cancel\" the y in the top and bottom, and taking reciprocals gives 1/f, not f⁻¹.<br><b>Signs.</b> When a term crosses the equals sign its sign changes: from xy − 4x = 2y + 3 you get xy − 2y = 4x + 3, not 3 − 4x.</div><div class=\"ex\"><div class=\"exh\">Worked example 1 · f(x) = 4x − 7</div><div class=\"exl\">1. y = 4x − 7.<br>2. Swap: x = 4y − 7.<br>3. Solve: x + 7 = 4y, so y = (x + 7)/4.<br>4. <b>f⁻¹(x) = (x + 7)/4</b>.<br>5. Verify: f(f⁻¹(x)) = 4 · (x + 7)/4 − 7 = x + 7 − 7 = x. ✔</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · g(x) = 9 − 2x</div><div class=\"exl\">Swap: x = 9 − 2y.  Then 2y = 9 − x, so <b>g⁻¹(x) = (9 − x)/2</b>.<br>Verify: g⁻¹(g(x)) = (9 − (9 − 2x))/2 = 2x/2 = x. ✔<br>Check with a number: g(1) = 7 and g⁻¹(7) = 1.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · The general line</div><div class=\"exl\">f(x) = mx + b: swap x = my + b, so y = (x − b)/m.<br>f⁻¹(x) = (x − b)/m = (1/m)x − b/m: a line with slope <b>1/m</b>, the reciprocal of the slope of f.</div></div><div class=\"keybox\"><b>Common mistakes.</b> Undoing in the wrong order: the inverse of 4x − 7 is (x + 7)/4, not x/4 + 7. Sign slips: from x = 9 − 2y, 2y = 9 − x, not x − 9. Forgetting to swap, so the answer is just f rewritten. Writing 1/(4x − 7).</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s2\">Practise 2 →</button></div></section><section class=\"note\" id=\"n3\"><h2>3 · Powers & roots</h2><p class=\"lt\"><b>Learning target:</b> I can invert functions built from powers and odd roots by undoing the operations in reverse order.</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Invert functions built from odd powers and odd roots.</li><li>✔ List the operations of f and undo them in reverse order.</li><li>✔ Recognise that the inverse of a root function is a power function and vice versa.</li></ul><p>Odd powers (x³, x⁵, x⁷) and odd roots (∛x, ⁵√x, ⁷√x) are one-to-one on all real numbers, so functions built from them can be inverted with no restriction. Odd roots of negative numbers are fine: ∛(−8) = −2 and ⁵√(−32) = −2.</p><h4>Undo in reverse order</h4><p>Write down how f is built from x, step by step, then undo the steps from last to first.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>f(x)</th><th>Built as</th><th>Undo (reverse order)</th><th>f⁻¹(x)</th></tr><tr><td>2(x + 1)³ − 5</td><td>+1, cube, ×2, −5</td><td>+5, ÷2, cube root, −1</td><td>∛((x + 5)/2) − 1</td></tr><tr><td>∛(4x − 1)</td><td>×4, −1, cube root</td><td>cube, +1, ÷4</td><td>(x³ + 1)/4</td></tr><tr><td>3x⁵ + 2</td><td>fifth power, ×3, +2</td><td>−2, ÷3, fifth root</td><td>⁵√((x − 2)/3)</td></tr></table></div><p><b>Roots and powers swap.</b> The inverse of a root function is a power (polynomial) function, and the inverse of a power function is a root function.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · g(x) = 2(x + 1)³ − 5</div><div class=\"exl\">Swap: x = 2(y + 1)³ − 5.<br>Add 5: x + 5 = 2(y + 1)³.  Divide by 2: (y + 1)³ = (x + 5)/2.<br>Cube root: y + 1 = ∛((x + 5)/2).  Subtract 1: <b>g⁻¹(x) = ∛((x + 5)/2) − 1</b>.<br>Check: g(1) = 2 · 8 − 5 = 11 and g⁻¹(11) = ∛8 − 1 = 1. ✔</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · h(x) = ⁵√(3 − 2x)</div><div class=\"exl\">Swap: x = ⁵√(3 − 2y).  Raise both sides to the 5th power: x⁵ = 3 − 2y.<br>So 2y = 3 − x⁵ and <b>h⁻¹(x) = (3 − x⁵)/2</b>, a polynomial.<br>Check: h(−14.5) = ⁵√32 = 2, and h⁻¹(2) = (3 − 32)/2 = −14.5. ✔</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · An even root needs care</div><div class=\"exl\">f(x) = √(x + 2) has domain x ≥ −2 and range y ≥ 0.<br>Swap: x = √(y + 2), so x² = y + 2 and f⁻¹(x) = x² − 2, <b>but only for x ≥ 0</b> (the range of f).<br>Without the restriction, x² − 2 is not one-to-one and is not the inverse.</div></div><div class=\"keybox\"><b>Common mistakes.</b> Taking the root too early: from x = 2(y + 1)³ − 5 you cannot take the cube root before removing −5 and ×2. Writing ∛x − 6 for the inverse of x³ + 6 (the answer is ∛(x − 6)). Using the wrong root (a square root to undo a cube). Forgetting the restriction x ≥ 0 when inverting an even root.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s3\">Practise 3 →</button></div></section><section class=\"note\" id=\"n4\"><h2>4 · Rational inverses</h2><p class=\"lt\"><b>Learning target:</b> I can invert a rational function by clearing the fraction, collecting the y terms on one side and factoring out y.</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Clear the denominator after swapping.</li><li>✔ Collect the y terms on one side and factor out y.</li><li>✔ State the value excluded from the domain of f⁻¹.</li><li>✔ Recognise a self-inverse rational function.</li></ul><p>For a rational function such as f(x) = (ax + b)/(cx + d) the unknown y appears in both the numerator and the denominator after swapping. The plan is always the same.</p><div class=\"keybox\"><b>Solving x = (ay + b)/(cy + d) for y</b><br>1. Multiply both sides by the denominator: x(cy + d) = ay + b.<br>2. Expand: cxy + dx = ay + b.<br>3. Collect every y term on one side: cxy − ay = b − dx.<br>4. Factor out y: y(cx − a) = b − dx.<br>5. Divide: y = (b − dx)/(cx − a).</div><div class=\"ex\"><div class=\"exh\">Worked example 1 · f(x) = (2x + 3)/(x − 4)</div><div class=\"exl\">Swap: x = (2y + 3)/(y − 4).  Multiply: x(y − 4) = 2y + 3, so xy − 4x = 2y + 3.<br>Collect: xy − 2y = 4x + 3.  Factor: y(x − 2) = 4x + 3.<br><b>f⁻¹(x) = (4x + 3)/(x − 2)</b>.<br>Check with a number: f(5) = 13/1 = 13 and f⁻¹(13) = 55/11 = 5. ✔</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · g(x) = 3x/(x + 2)</div><div class=\"exl\">Swap: x = 3y/(y + 2).  Multiply: xy + 2x = 3y.<br>Collect: 2x = 3y − xy = y(3 − x).<br><b>g⁻¹(x) = 2x/(3 − x)</b>, with x ≠ 3.<br>The excluded value 3 is the horizontal asymptote of g: g never takes the value 3, so 3 is not in the domain of g⁻¹.</div></div><div class=\"keybox\"><b>Where students go wrong in step 3.</b> Trying to cancel y from the top and bottom. Taking reciprocals of both sides (that gives 1/f). Losing a sign when a term crosses the equals sign. Forgetting to bracket: (4x + 3)/(x − 2) typed as 4x+3/x-2 means 4x + (3/x) − 2.</div><div class=\"keybox\"><b>Self-inverse functions.</b> When a = −d, as in (2x + 5)/(3x − 2), the formula gives back f itself: f is its own inverse, and its graph is symmetric about y = x.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s4\">Practise 4 →</button></div></section><section class=\"note\" id=\"n5\"><h2>5 · Verifying by composition</h2><p class=\"lt\"><b>Learning target:</b> I can compute f(g(x)) and g(f(x)) to decide whether two functions are inverses, and spot errors in a verification.</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Compute f(g(x)) and g(f(x)).</li><li>✔ Decide whether two functions are inverses, and explain why one composition is usually enough.</li><li>✔ Find and correct errors in a verification.</li></ul><p>To prove that f and g are inverses, show both compositions give x: <b>(f∘g)(x) = f(g(x)) = x</b> and <b>(g∘f)(x) = g(f(x)) = x</b>. If either composition gives something other than x, they are not inverses.</p><p><b>One composition is usually enough here.</b> When you found f⁻¹ by the procedure and both functions are one-to-one, one composition confirms the algebra. When someone hands you two arbitrary functions, check both, and keep an eye on domains.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · f(x) = 5x + 2 and g(x) = (x − 2)/5</div><div class=\"exl\">f(g(x)) = 5 · (x − 2)/5 + 2 = x − 2 + 2 = x.<br>g(f(x)) = ((5x + 2) − 2)/5 = 5x/5 = x.<br>Both give x: <b>f and g are inverses</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Not inverses</div><div class=\"exl\">f(x) = 2x + 4 and g(x) = x/2 − 4.<br>f(g(x)) = 2(x/2 − 4) + 4 = x − 8 + 4 = x − 4 ≠ x.<br>So they are <b>not</b> inverses. (The inverse of f is x/2 − 2.) A quick number check shows it too: g(0) = −4, f(−4) = −4, not 0.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Domains matter</div><div class=\"exl\">f(x) = x² − 1 for x ≥ 0 and g(x) = √(x + 1).<br>f(g(x)) = (√(x + 1))² − 1 = x for x ≥ −1.<br>g(f(x)) = √(x²) = |x|, which equals x only because x ≥ 0. Without the restriction, g(f(−3)) = 3, not −3.</div></div><div class=\"keybox\"><b>Common mistakes.</b> Checking one number and concluding \"inverses\" (f(g(0)) = 0 can happen by luck). Not distributing: 3(x/3 − 6) = x − 18, not x − 6. Simplifying √(x²) to x without the restriction x ≥ 0. Multiplying f(x) · g(x) instead of composing.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s5\">Practise 5 →</button></div></section><section class=\"note\" id=\"n6\"><h2>6 · Graphs, domain & range</h2><p class=\"lt\"><b>Learning target:</b> I can sketch f⁻¹ by reflecting f in y = x, swap points, and state the domain and range of f⁻¹, including on a restricted domain.</p><h4>Learning objectives</h4><ul style=\"list-style:none;padding-left:2px\"><li>✔ Sketch f⁻¹ by reflecting the graph of f in y = x.</li><li>✔ Turn a point (a, b) on f into (b, a) on f⁻¹.</li><li>✔ State the domain and range of f⁻¹ from the range and domain of f.</li><li>✔ Find inverses on a restricted domain, choosing the correct sign.</li></ul><p>If (a, b) is on the graph of f, then f(a) = b, so f⁻¹(b) = a and <b>(b, a) is on the graph of f⁻¹</b>. Swapping the coordinates of every point is a reflection in the line <b>y = x</b>.</p><div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"f(x) = x cubed over 8 plus 1 and its inverse, mirror images in the line y = x\"><line class=\"tk\" x1=\"24.0\" y1=\"264.0\" x2=\"24.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"53.7\" y1=\"264.0\" x2=\"53.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"83.5\" y1=\"264.0\" x2=\"83.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"113.2\" y1=\"264.0\" x2=\"113.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"172.8\" y1=\"264.0\" x2=\"172.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"202.5\" y1=\"264.0\" x2=\"202.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"232.3\" y1=\"264.0\" x2=\"232.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"262.0\" y1=\"264.0\" x2=\"262.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"258.0\" x2=\"268.0\" y2=\"258.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"228.3\" x2=\"268.0\" y2=\"228.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"198.5\" x2=\"268.0\" y2=\"198.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"168.8\" x2=\"268.0\" y2=\"168.8\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"109.2\" x2=\"268.0\" y2=\"109.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"79.5\" x2=\"268.0\" y2=\"79.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"49.7\" x2=\"268.0\" y2=\"49.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"20.0\" x2=\"268.0\" y2=\"20.0\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\"/><line class=\"ln\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"134.0\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"149.0\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"24.0\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"262.0\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"139.0\" y=\"262.0\" text-anchor=\"end\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"139.0\" y=\"83.5\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"139.0\" y=\"24.0\" text-anchor=\"end\" style=\"font-size:10px\">4</text><line class=\"ln hid\" x1=\"18.0\" y1=\"264.0\" x2=\"268.0\" y2=\"14.0\"/><text class=\"lb\" x=\"248.0\" y=\"26.0\" text-anchor=\"end\" style=\"font-size:11px\">y = x</text><polyline class=\"arm\" points=\"40.2,262.4 40.9,259.4 41.6,256.3 42.3,253.3 43.0,250.4 43.7,247.4 44.4,244.6 45.1,241.7 45.8,238.9 46.5,236.2 47.2,233.4 47.9,230.8 48.6,228.1 49.2,225.5 49.9,223.0 50.6,220.4 51.3,217.9 52.0,215.5 52.7,213.1 53.4,210.7 54.1,208.4 54.8,206.0 55.5,203.8 56.2,201.5 56.9,199.3 57.6,197.2 58.3,195.1 59.0,193.0 59.7,190.9 60.4,188.9 61.1,186.9 61.8,184.9 62.4,183.0 63.1,181.1 63.8,179.3 64.5,177.4 65.2,175.6 65.9,173.9 66.6,172.1 67.3,170.4 68.0,168.8 68.7,167.1 69.4,165.5 70.1,163.9 70.8,162.4 71.5,160.9 72.2,159.4 72.9,157.9 73.6,156.5 74.2,155.1 74.9,153.7 75.6,152.4 76.3,151.1 77.0,149.8 77.7,148.5 78.4,147.3 79.1,146.0 79.8,144.9 80.5,143.7 81.2,142.6 81.9,141.4 82.6,140.4 83.3,139.3 84.0,138.3 84.7,137.2 85.4,136.3 86.1,135.3 86.8,134.4 87.4,133.4 88.1,132.5 88.8,131.7 89.5,130.8 90.2,130.0 90.9,129.2 91.6,128.4 92.3,127.6 93.0,126.9 93.7,126.2 94.4,125.4 95.1,124.8 95.8,124.1 96.5,123.5 97.2,122.8 97.9,122.2 98.6,121.6 99.2,121.1 99.9,120.5 100.6,120.0 101.3,119.4 102.0,118.9 102.7,118.5 103.4,118.0 104.1,117.5 104.8,117.1 105.5,116.7 106.2,116.3 106.9,115.9 107.6,115.5 108.3,115.1 109.0,114.8 109.7,114.5 110.4,114.1 111.1,113.8 111.7,113.5 112.4,113.3 113.1,113.0 113.8,112.7 114.5,112.5 115.2,112.3 115.9,112.0 116.6,111.8 117.3,111.6 118.0,111.4 118.7,111.3 119.4,111.1 120.1,110.9 120.8,110.8 121.5,110.6 122.2,110.5 122.9,110.4 123.6,110.3 124.2,110.2 124.9,110.1 125.6,110.0 126.3,109.9 127.0,109.8 127.7,109.7 128.4,109.7 129.1,109.6 129.8,109.6 130.5,109.5 131.2,109.5 131.9,109.4 132.6,109.4 133.3,109.4 134.0,109.3 134.7,109.3 135.4,109.3 136.1,109.3 136.8,109.3 137.4,109.3 138.1,109.3 138.8,109.2 139.5,109.2 140.2,109.2 140.9,109.2 141.6,109.2 142.3,109.2 143.0,109.2 143.7,109.2 144.4,109.2 145.1,109.2 145.8,109.2 146.5,109.2 147.2,109.2 147.9,109.2 148.6,109.2 149.2,109.2 149.9,109.2 150.6,109.2 151.3,109.2 152.0,109.1 152.7,109.1 153.4,109.1 154.1,109.0 154.8,109.0 155.5,109.0 156.2,108.9 156.9,108.9 157.6,108.8 158.3,108.7 159.0,108.7 159.7,108.6 160.4,108.5 161.1,108.4 161.8,108.3 162.4,108.2 163.1,108.1 163.8,108.0 164.5,107.8 165.2,107.7 165.9,107.5 166.6,107.4 167.3,107.2 168.0,107.0 168.7,106.8 169.4,106.6 170.1,106.4 170.8,106.2 171.5,106.0 172.2,105.7 172.9,105.5 173.6,105.2 174.2,104.9 174.9,104.6 175.6,104.3 176.3,104.0 177.0,103.7 177.7,103.3 178.4,103.0 179.1,102.6 179.8,102.2 180.5,101.8 181.2,101.4 181.9,100.9 182.6,100.5 183.3,100.0 184.0,99.5 184.7,99.0 185.4,98.5 186.1,98.0 186.7,97.4 187.4,96.8 188.1,96.3 188.8,95.7 189.5,95.0 190.2,94.4 190.9,93.7 191.6,93.0 192.3,92.3 193.0,91.6 193.7,90.9 194.4,90.1 195.1,89.3 195.8,88.5 196.5,87.7 197.2,86.8 197.9,85.9 198.6,85.0 199.2,84.1 199.9,83.2 200.6,82.2 201.3,81.2 202.0,80.2 202.7,79.2 203.4,78.1 204.1,77.0 204.8,75.9 205.5,74.8 206.2,73.6 206.9,72.4 207.6,71.2 208.3,70.0 209.0,68.7 209.7,67.4 210.4,66.1 211.1,64.8 211.7,63.4 212.4,62.0 213.1,60.5 213.8,59.1 214.5,57.6 215.2,56.1 215.9,54.5 216.6,52.9 217.3,51.3 218.0,49.7 218.7,48.0 219.4,46.3 220.1,44.6 220.8,42.8 221.5,41.0 222.2,39.2 222.9,37.4 223.6,35.5 224.2,33.5 224.9,31.6 225.6,29.6 226.3,27.6 227.0,25.5 227.7,23.4 228.4,21.3 229.1,19.1 229.8,16.9 230.5,14.7\"/><text class=\"al\" x=\"212.9\" y=\"34.8\" text-anchor=\"end\" style=\"font-size:12px\">f</text><polyline class=\"ln\" points=\"18.0,242.1 18.7,242.0 19.4,241.8 20.1,241.7 20.8,241.5 21.5,241.3 22.2,241.2 22.9,241.0 23.6,240.9 24.2,240.7 24.9,240.6 25.6,240.4 26.3,240.2 27.0,240.1 27.7,239.9 28.4,239.8 29.1,239.6 29.8,239.4 30.5,239.3 31.2,239.1 31.9,238.9 32.6,238.8 33.3,238.6 34.0,238.4 34.7,238.3 35.4,238.1 36.1,237.9 36.8,237.8 37.4,237.6 38.1,237.4 38.8,237.3 39.5,237.1 40.2,236.9 40.9,236.8 41.6,236.6 42.3,236.4 43.0,236.2 43.7,236.1 44.4,235.9 45.1,235.7 45.8,235.5 46.5,235.4 47.2,235.2 47.9,235.0 48.6,234.8 49.2,234.7 49.9,234.5 50.6,234.3 51.3,234.1 52.0,233.9 52.7,233.7 53.4,233.6 54.1,233.4 54.8,233.2 55.5,233.0 56.2,232.8 56.9,232.6 57.6,232.5 58.3,232.3 59.0,232.1 59.7,231.9 60.4,231.7 61.1,231.5 61.8,231.3 62.4,231.1 63.1,230.9 63.8,230.7 64.5,230.5 65.2,230.3 65.9,230.1 66.6,229.9 67.3,229.7 68.0,229.5 68.7,229.3 69.4,229.1 70.1,228.9 70.8,228.7 71.5,228.5 72.2,228.3 72.9,228.1 73.6,227.9 74.2,227.7 74.9,227.5 75.6,227.3 76.3,227.1 77.0,226.9 77.7,226.7 78.4,226.4 79.1,226.2 79.8,226.0 80.5,225.8 81.2,225.6 81.9,225.4 82.6,225.1 83.3,224.9 84.0,224.7 84.7,224.5 85.4,224.2 86.1,224.0 86.8,223.8 87.4,223.6 88.1,223.3 88.8,223.1 89.5,222.9 90.2,222.6 90.9,222.4 91.6,222.2 92.3,221.9 93.0,221.7 93.7,221.4 94.4,221.2 95.1,221.0 95.8,220.7 96.5,220.5 97.2,220.2 97.9,220.0 98.6,219.7 99.2,219.5 99.9,219.2 100.6,219.0 101.3,218.7 102.0,218.4 102.7,218.2 103.4,217.9 104.1,217.6 104.8,217.4 105.5,217.1 106.2,216.8 106.9,216.6 107.6,216.3 108.3,216.0 109.0,215.7 109.7,215.5 110.4,215.2 111.1,214.9 111.7,214.6 112.4,214.3 113.1,214.0 113.8,213.7 114.5,213.4 115.2,213.2 115.9,212.9 116.6,212.6 117.3,212.2 118.0,211.9 118.7,211.6 119.4,211.3 120.1,211.0 120.8,210.7 121.5,210.4 122.2,210.0 122.9,209.7 123.6,209.4 124.2,209.1 124.9,208.7 125.6,208.4 126.3,208.0 127.0,207.7 127.7,207.3 128.4,207.0 129.1,206.6 129.8,206.3 130.5,205.9 131.2,205.5 131.9,205.2 132.6,204.8 133.3,204.4 134.0,204.0 134.7,203.6 135.4,203.2 136.1,202.8 136.8,202.4 137.4,202.0 138.1,201.6 138.8,201.2 139.5,200.8 140.2,200.3 140.9,199.9 141.6,199.4 142.3,199.0 143.0,198.5 143.7,198.1 144.4,197.6 145.1,197.1 145.8,196.6 146.5,196.1 147.2,195.6 147.9,195.1 148.6,194.6 149.2,194.0 149.9,193.5 150.6,192.9 151.3,192.4 152.0,191.8 152.7,191.2 153.4,190.6 154.1,189.9 154.8,189.3 155.5,188.6 156.2,188.0 156.9,187.3 157.6,186.6 158.3,185.8 159.0,185.1 159.7,184.3 160.4,183.5 161.1,182.6 161.8,181.7 162.4,180.8 163.1,179.9 163.8,178.8 164.5,177.8 165.2,176.7 165.9,175.5 166.6,174.2 167.3,172.8 168.0,171.3 168.7,169.7 169.4,167.8 170.1,165.7 170.8,163.1 171.5,159.9 172.2,155.2 172.9,130.1 173.6,121.2 174.2,117.1 174.9,114.1 175.6,111.7 176.3,109.6 177.0,107.8 177.7,106.2 178.4,104.8 179.1,103.4 179.8,102.2 180.5,101.0 181.2,99.9 181.9,98.9 182.6,97.9 183.3,96.9 184.0,96.0 184.7,95.1 185.4,94.3 186.1,93.5 186.7,92.7 187.4,92.0 188.1,91.2 188.8,90.5 189.5,89.8 190.2,89.2 190.9,88.5 191.6,87.9 192.3,87.3 193.0,86.7 193.7,86.1 194.4,85.5 195.1,84.9 195.8,84.4 196.5,83.8 197.2,83.3 197.9,82.8 198.6,82.2 199.2,81.7 199.9,81.2 200.6,80.8 201.3,80.3 202.0,79.8 202.7,79.3 203.4,78.9 204.1,78.4 204.8,78.0 205.5,77.6 206.2,77.1 206.9,76.7 207.6,76.3 208.3,75.9 209.0,75.5 209.7,75.1 210.4,74.7 211.1,74.3 211.7,73.9 212.4,73.5 213.1,73.1 213.8,72.7 214.5,72.4 215.2,72.0 215.9,71.6 216.6,71.3 217.3,70.9 218.0,70.6 218.7,70.2 219.4,69.9 220.1,69.5 220.8,69.2 221.5,68.9 222.2,68.5 222.9,68.2 223.6,67.9 224.2,67.5 224.9,67.2 225.6,66.9 226.3,66.6 227.0,66.3 227.7,66.0 228.4,65.7 229.1,65.4 229.8,65.1 230.5,64.8 231.2,64.5 231.9,64.2 232.6,63.9 233.3,63.6 234.0,63.3 234.7,63.0 235.4,62.7 236.1,62.5 236.7,62.2 237.4,61.9 238.1,61.6 238.8,61.3 239.5,61.1 240.2,60.8 240.9,60.5 241.6,60.3 242.3,60.0 243.0,59.8 243.7,59.5 244.4,59.2 245.1,59.0 245.8,58.7 246.5,58.5 247.2,58.2 247.9,58.0 248.6,57.7 249.2,57.5 249.9,57.2 250.6,57.0 251.3,56.7 252.0,56.5 252.7,56.3 253.4,56.0 254.1,55.8 254.8,55.5 255.5,55.3 256.2,55.1 256.9,54.8 257.6,54.6 258.3,54.4 259.0,54.1 259.7,53.9 260.4,53.7 261.1,53.5 261.8,53.2 262.4,53.0 263.1,52.8 263.8,52.6 264.5,52.4 265.2,52.1 265.9,51.9 266.6,51.7 267.3,51.5 268.0,51.3\"/><text class=\"lb\" x=\"244.2\" y=\"78.0\" text-anchor=\"middle\" style=\"font-size:12px\">f⁻¹</text><circle class=\"pt\" cx=\"202.5\" cy=\"79.5\" r=\"3.2\"/><text class=\"lb\" x=\"208.5\" y=\"93.5\" text-anchor=\"start\" style=\"font-size:11px\">(2, 2)</text><circle class=\"pt\" cx=\"83.5\" cy=\"139.0\" r=\"3.2\"/><text class=\"lb\" x=\"77.5\" y=\"132.0\" text-anchor=\"end\" style=\"font-size:11px\">(−2, 0)</text><circle class=\"pt\" cx=\"143.0\" cy=\"198.5\" r=\"3.2\"/><text class=\"lb\" x=\"149.0\" y=\"202.5\" text-anchor=\"start\" style=\"font-size:11px\">(0, −2)</text><circle class=\"pt\" cx=\"143.0\" cy=\"109.2\" r=\"3.2\"/><text class=\"lb\" x=\"137.0\" y=\"102.2\" text-anchor=\"end\" style=\"font-size:11px\">(0, 1)</text><circle class=\"pt\" cx=\"172.8\" cy=\"139.0\" r=\"3.2\"/><text class=\"lb\" x=\"177.8\" y=\"153.0\" text-anchor=\"start\" style=\"font-size:11px\">(1, 0)</text></svg></div><p>Here f(x) = x³/8 + 1. Its points (−2, 0), (0, 1) and (2, 2) become (0, −2), (1, 0) and (2, 2) on f⁻¹. A point on y = x, such as (2, 2), stays where it is, so f and f⁻¹ meet there.</p><h4>Domain and range swap</h4><p>Because inputs and outputs trade places: <b>domain of f⁻¹ = range of f</b> and <b>range of f⁻¹ = domain of f</b>.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>f</th><th>Domain of f</th><th>Range of f</th><th>f⁻¹</th><th>Domain of f⁻¹</th></tr><tr><td>√(x − 2) + 1</td><td>x ≥ 2</td><td>y ≥ 1</td><td>(x − 1)² + 2</td><td>x ≥ 1</td></tr><tr><td>x² (x ≥ 0)</td><td>x ≥ 0</td><td>y ≥ 0</td><td>√x</td><td>x ≥ 0</td></tr><tr><td>(2x + 3)/(x − 4)</td><td>x ≠ 4</td><td>y ≠ 2</td><td>(4x + 3)/(x − 2)</td><td>x ≠ 2</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Worked example 1 · f(x) = √(x − 2) + 1</div><div class=\"exl\"><div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"f(x) = square root of (x − 2) plus 1 and its inverse, reflected in y = x\"><line class=\"tk\" x1=\"24.8\" y1=\"264.0\" x2=\"24.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"58.5\" y1=\"264.0\" x2=\"58.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"92.3\" y1=\"264.0\" x2=\"92.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"126.1\" y1=\"264.0\" x2=\"126.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"159.9\" y1=\"264.0\" x2=\"159.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"193.7\" y1=\"264.0\" x2=\"193.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"227.5\" y1=\"264.0\" x2=\"227.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"261.2\" y1=\"264.0\" x2=\"261.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"257.2\" x2=\"268.0\" y2=\"257.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"223.5\" x2=\"268.0\" y2=\"223.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"189.7\" x2=\"268.0\" y2=\"189.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"155.9\" x2=\"268.0\" y2=\"155.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"122.1\" x2=\"268.0\" y2=\"122.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"88.3\" x2=\"268.0\" y2=\"88.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"54.5\" x2=\"268.0\" y2=\"54.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"20.8\" x2=\"268.0\" y2=\"20.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"223.5\" x2=\"268.0\" y2=\"223.5\"/><line class=\"ln\" x1=\"58.5\" y1=\"264.0\" x2=\"58.5\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"218.5\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"64.5\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"126.1\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"193.7\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"261.2\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">6</text><text class=\"lb\" x=\"54.5\" y=\"159.9\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"54.5\" y=\"92.3\" text-anchor=\"end\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"54.5\" y=\"24.8\" text-anchor=\"end\" style=\"font-size:10px\">6</text><line class=\"ln hid\" x1=\"18.0\" y1=\"264.0\" x2=\"268.0\" y2=\"14.0\"/><text class=\"lb\" x=\"248.0\" y=\"26.0\" text-anchor=\"end\" style=\"font-size:11px\">y = x</text><polyline class=\"arm\" points=\"126.3,186.9 127.0,184.1 127.7,182.3 128.4,180.8 129.1,179.6 129.8,178.5 130.5,177.5 131.2,176.6 131.9,175.7 132.6,174.9 133.3,174.1 134.0,173.4 134.7,172.7 135.4,172.0 136.1,171.3 136.8,170.7 137.4,170.1 138.1,169.5 138.8,168.9 139.5,168.4 140.2,167.8 140.9,167.3 141.6,166.8 142.3,166.3 143.0,165.8 143.7,165.3 144.4,164.8 145.1,164.4 145.8,163.9 146.5,163.4 147.2,163.0 147.9,162.6 148.6,162.1 149.3,161.7 149.9,161.3 150.6,160.9 151.3,160.5 152.0,160.1 152.7,159.7 153.4,159.3 154.1,158.9 154.8,158.5 155.5,158.2 156.2,157.8 156.9,157.4 157.6,157.1 158.3,156.7 159.0,156.4 159.7,156.0 160.4,155.7 161.1,155.3 161.8,155.0 162.4,154.6 163.1,154.3 163.8,154.0 164.5,153.6 165.2,153.3 165.9,153.0 166.6,152.7 167.3,152.4 168.0,152.1 168.7,151.7 169.4,151.4 170.1,151.1 170.8,150.8 171.5,150.5 172.2,150.2 172.9,149.9 173.6,149.6 174.2,149.3 174.9,149.1 175.6,148.8 176.3,148.5 177.0,148.2 177.7,147.9 178.4,147.6 179.1,147.4 179.8,147.1 180.5,146.8 181.2,146.5 181.9,146.3 182.6,146.0 183.3,145.7 184.0,145.5 184.7,145.2 185.4,144.9 186.1,144.7 186.8,144.4 187.4,144.2 188.1,143.9 188.8,143.6 189.5,143.4 190.2,143.1 190.9,142.9 191.6,142.6 192.3,142.4 193.0,142.1 193.7,141.9 194.4,141.6 195.1,141.4 195.8,141.2 196.5,140.9 197.2,140.7 197.9,140.4 198.6,140.2 199.2,140.0 199.9,139.7 200.6,139.5 201.3,139.3 202.0,139.0 202.7,138.8 203.4,138.6 204.1,138.3 204.8,138.1 205.5,137.9 206.2,137.7 206.9,137.4 207.6,137.2 208.3,137.0 209.0,136.8 209.7,136.5 210.4,136.3 211.1,136.1 211.7,135.9 212.4,135.7 213.1,135.5 213.8,135.2 214.5,135.0 215.2,134.8 215.9,134.6 216.6,134.4 217.3,134.2 218.0,134.0 218.7,133.7 219.4,133.5 220.1,133.3 220.8,133.1 221.5,132.9 222.2,132.7 222.9,132.5 223.6,132.3 224.2,132.1 224.9,131.9 225.6,131.7 226.3,131.5 227.0,131.3 227.7,131.1 228.4,130.9 229.1,130.7 229.8,130.5 230.5,130.3 231.2,130.1 231.9,129.9 232.6,129.7 233.3,129.5 234.0,129.3 234.7,129.1 235.4,128.9 236.1,128.7 236.7,128.5 237.4,128.3 238.1,128.2 238.8,128.0 239.5,127.8 240.2,127.6 240.9,127.4 241.6,127.2 242.3,127.0 243.0,126.8 243.7,126.6 244.4,126.5 245.1,126.3 245.8,126.1 246.5,125.9 247.2,125.7 247.9,125.5 248.6,125.4 249.2,125.2 249.9,125.0 250.6,124.8 251.3,124.6 252.0,124.5 252.7,124.3 253.4,124.1 254.1,123.9 254.8,123.7 255.5,123.6 256.2,123.4 256.9,123.2 257.6,123.0 258.3,122.9 259.0,122.7 259.7,122.5 260.4,122.3 261.1,122.2 261.8,122.0 262.4,121.8 263.1,121.6 263.8,121.5 264.5,121.3 265.2,121.1 265.9,120.9 266.6,120.8 267.3,120.6 268.0,120.4\"/><text class=\"al\" x=\"218.9\" y=\"129.2\" text-anchor=\"start\" style=\"font-size:12px\">f</text><polyline class=\"ln\" points=\"93.0,155.9 93.7,155.8 94.4,155.8 95.1,155.7 95.8,155.5 96.5,155.4 97.2,155.2 97.9,155.0 98.6,154.7 99.2,154.5 99.9,154.2 100.6,153.8 101.3,153.5 102.0,153.1 102.7,152.7 103.4,152.2 104.1,151.8 104.8,151.3 105.5,150.8 106.2,150.2 106.9,149.6 107.6,149.0 108.3,148.4 109.0,147.7 109.7,147.0 110.4,146.3 111.1,145.5 111.8,144.7 112.4,143.9 113.1,143.1 113.8,142.2 114.5,141.3 115.2,140.4 115.9,139.4 116.6,138.4 117.3,137.4 118.0,136.4 118.7,135.3 119.4,134.2 120.1,133.1 120.8,131.9 121.5,130.7 122.2,129.5 122.9,128.3 123.6,127.0 124.2,125.7 124.9,124.4 125.6,123.0 126.3,121.7 127.0,120.2 127.7,118.8 128.4,117.3 129.1,115.8 129.8,114.3 130.5,112.8 131.2,111.2 131.9,109.6 132.6,107.9 133.3,106.2 134.0,104.5 134.7,102.8 135.4,101.1 136.1,99.3 136.8,97.5 137.4,95.6 138.1,93.8 138.8,91.9 139.5,89.9 140.2,88.0 140.9,86.0 141.6,84.0 142.3,81.9 143.0,79.9 143.7,77.8 144.4,75.7 145.1,73.5 145.8,71.3 146.5,69.1 147.2,66.9 147.9,64.6 148.6,62.3 149.3,60.0 149.9,57.6 150.6,55.2 151.3,52.8 152.0,50.4 152.7,47.9 153.4,45.4 154.1,42.9 154.8,40.3 155.5,37.8 156.2,35.1 156.9,32.5 157.6,29.8 158.3,27.1 159.0,24.4 159.7,21.7 160.4,18.9 161.1,16.1\"/><text class=\"lb\" x=\"134.6\" y=\"68.1\" text-anchor=\"end\" style=\"font-size:12px\">f⁻¹</text><circle class=\"pt\" cx=\"126.1\" cy=\"189.7\" r=\"3.2\"/><text class=\"lb\" x=\"132.1\" y=\"201.7\" text-anchor=\"start\" style=\"font-size:11px\">(2, 1)</text><circle class=\"pt\" cx=\"92.3\" cy=\"155.9\" r=\"3.2\"/><text class=\"lb\" x=\"86.3\" y=\"149.9\" text-anchor=\"end\" style=\"font-size:11px\">(1, 2)</text></svg></div><br>Domain x ≥ 2, range y ≥ 1 (the graph starts at (2, 1)).<br>Swap: x = √(y − 2) + 1, so x − 1 = √(y − 2) and y = (x − 1)² + 2.<br><b>f⁻¹(x) = (x − 1)² + 2 for x ≥ 1</b>: the right half of a parabola starting at (1, 2).</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Inverse on a restricted domain</div><div class=\"exl\">f(x) = (x − 3)² for x ≥ 3 has range y ≥ 0.<br>Swap: x = (y − 3)², so y − 3 = ±√x. The range of f⁻¹ must be y ≥ 3, so we take the + sign.<br><b>f⁻¹(x) = 3 + √x, x ≥ 0</b>.</div></div><div class=\"keybox\"><b>Common mistakes.</b> Reflecting in the x-axis or y-axis instead of y = x. Swapping a point to (−a, −b) or (a, 1/b). Giving the domain of f⁻¹ as the domain of f. Choosing the wrong sign of the square root on a restricted domain.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s6\">Practise 6 →</button></div></section><section class=\"note\" id=\"nsum\"><h2>Summary checklist</h2><ul style=\"list-style:none;padding-left:2px\"><li>✔ I can decide whether a function is one-to-one from a table, a mapping, a formula or a graph (horizontal line test), restrict a domain to make it one-to-one, and read f⁻¹ values, knowing that f⁻¹(x) is not 1/f(x).</li><li>✔ I can find the inverse of a linear function with the five-step procedure and check it.</li><li>✔ I can invert functions built from powers and odd roots by undoing the operations in reverse order.</li><li>✔ I can invert a rational function by clearing the fraction, collecting the y terms on one side and factoring out y.</li><li>✔ I can compute f(g(x)) and g(f(x)) to decide whether two functions are inverses, and spot errors in a verification.</li><li>✔ I can sketch f⁻¹ by reflecting f in y = x, swap points, and state the domain and range of f⁻¹, including on a restricted domain.</li><li>✔ I always verify my inverse with a composition or a number check.</li></ul><div class=\"keybox\"><b>Finding the inverse of a one-to-one function f</b><br>1. Replace f(x) with y.<br>2. Swap x and y.<br>3. Solve the new equation for y. <i>This is the step where most errors happen.</i><br>4. Replace y with f⁻¹(x).<br>5. Verify by composition: (f∘f⁻¹)(x) = x and (f⁻¹∘f)(x) = x. In this course one of the two is usually enough.</div><div class=\"hub-btns\" style=\"margin-top:10px\"><button class=\"hub-btn\" data-go=\"s7\">Assessment A</button><button class=\"hub-btn\" data-go=\"s8\">Assessment B</button><button class=\"hub-btn\" data-go=\"s9\">Assessment C</button><button class=\"hub-btn\" data-go=\"s10\">Assessment D</button><button class=\"hub-btn primary\" data-go=\"report\">📊 Report</button></div></section>";
var REPORT = [["s7", "A", "Knowing and understanding"], ["s8", "B", "Investigating patterns"], ["s9", "C", "Communicating"], ["s10", "D", "Applying mathematics in real-life contexts"]];
var SECTIONS = [{"id": "s1", "label": "1 · One-to-one & notation", "sub": "One-to-one from tables, mappings, formulas and graphs; restricting a domain; f⁻¹ vs 1/f", "slides": [{"kind": "mcq", "text": "A function f is given by the table.\nx: 1, 2, 3, 4\nf(x): 5, 8, 5, 2\nIs f one-to-one?", "opts": ["No: the output 2 is smaller than its input 4", "No: f(1) = f(3) = 5, so two inputs share an output", "Yes: all the outputs are whole numbers", "Yes: every input has exactly one output"], "correct": 1, "tag": "", "sol": "One-to-one means different inputs give different outputs. Here 1 and 3 both give 5, so f is not one-to-one and has no inverse (f⁻¹(5) would have to be both 1 and 3). 'Every input has one output' only says f is a function."}, {"kind": "blank", "p": "The function g is given by the table.\nx: −2, −1, 0, 1, 2\ng(x): 7, 4, 1, −2, −5", "tag": "", "marks": "", "flat": [{"t": "All five outputs are different, so g is __B1__", "a": {"B1": "one-to-one"}, "expr": "words", "accept": ["one to one", "injective", "1-1", "1 to 1"]}, {"t": "g⁻¹(4) = __B1__", "a": {"B1": "-1"}}, {"t": "g⁻¹(−5) = __B1__", "a": {"B1": "2"}}, {"t": "g(g⁻¹(1)) = __B1__", "a": {"B1": "1"}}], "sol": "Different inputs give different outputs: one-to-one.\ng(−1) = 4, so g⁻¹(4) = −1.\ng(2) = −5, so g⁻¹(−5) = 2.\ng⁻¹(1) = 0 and g(0) = 1: g undoes g⁻¹."}, {"kind": "mcq", "text": "Which of these functions is NOT one-to-one?", "opts": ["f(x) = 2x − 7", "f(x) = √x", "f(x) = x² + 1", "f(x) = x³"], "correct": 2, "tag": "", "sol": "x² + 1 gives the same output for x and −x: f(−2) = f(2) = 5. A non-vertical line, x³ and √x (on its domain x ≥ 0) are always increasing, so they are one-to-one."}, {"kind": "blank", "p": "f(x) = x² for all real x. The figure shows the horizontal line y = 4 meeting the graph at (−2, 4) and (2, 4).", "tag": "", "marks": "", "flat": [{"t": "f(−3) = __B1__, the same as f(3)", "a": {"B1": "9"}}, {"t": "So the horizontal line y = 9 cuts the graph __B1__ (how many times?)", "a": {"B1": "twice"}, "expr": "words", "accept": ["two", "2", "two times", "2 times"]}, {"t": "Keeping only x ≥ __B1__ (the right half) makes f one-to-one", "a": {"B1": "0"}}, {"t": "On that domain f⁻¹(x) = √x, so f⁻¹(25) = __B1__", "a": {"B1": "5"}}], "sol": "(−3)² = 9 = 3².\nIt meets y = 9 at x = −3 and x = 3: two points, so f fails the horizontal line test.\nFor x ≥ 0 each output comes from one input only.\n√25 = 5 (and 5 ≥ 0).", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"The parabola y = x squared cut twice by the horizontal line y = 4\"><line class=\"tk\" x1=\"25.8\" y1=\"264.0\" x2=\"25.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"64.9\" y1=\"264.0\" x2=\"64.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"103.9\" y1=\"264.0\" x2=\"103.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"182.1\" y1=\"264.0\" x2=\"182.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"221.1\" y1=\"264.0\" x2=\"221.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"260.2\" y1=\"264.0\" x2=\"260.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"256.2\" x2=\"268.0\" y2=\"256.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"178.1\" x2=\"268.0\" y2=\"178.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"99.9\" x2=\"268.0\" y2=\"99.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"60.9\" x2=\"268.0\" y2=\"60.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"21.8\" x2=\"268.0\" y2=\"21.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"217.1\" x2=\"268.0\" y2=\"217.1\"/><line class=\"ln\" x1=\"143.0\" y1=\"264.0\" x2=\"143.0\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"212.1\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"149.0\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"64.9\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"221.1\" y=\"230.1\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"139.0\" y=\"143.0\" text-anchor=\"end\" style=\"font-size:10px\">2</text><line class=\"arm hid\" x1=\"18.0\" y1=\"60.9\" x2=\"268.0\" y2=\"60.9\"/><text class=\"al\" x=\"266.0\" y=\"75.9\" text-anchor=\"end\" style=\"font-size:11px\">y = 4</text><polyline class=\"arm\" points=\"54.1,14.9 54.8,18.0 55.5,21.1 56.2,24.2 56.9,27.3 57.6,30.3 58.3,33.4 59.0,36.4 59.7,39.3 60.4,42.3 61.1,45.2 61.8,48.1 62.4,51.0 63.1,53.9 63.8,56.7 64.5,59.5 65.2,62.3 65.9,65.0 66.6,67.7 67.3,70.4 68.0,73.1 68.7,75.8 69.4,78.4 70.1,81.0 70.8,83.6 71.5,86.1 72.2,88.7 72.9,91.2 73.6,93.7 74.2,96.1 74.9,98.6 75.6,101.0 76.3,103.3 77.0,105.7 77.7,108.0 78.4,110.3 79.1,112.6 79.8,114.9 80.5,117.1 81.2,119.3 81.9,121.5 82.6,123.7 83.3,125.8 84.0,127.9 84.7,130.0 85.4,132.1 86.1,134.1 86.8,136.1 87.4,138.1 88.1,140.1 88.8,142.0 89.5,143.9 90.2,145.8 90.9,147.7 91.6,149.5 92.3,151.3 93.0,153.1 93.7,154.9 94.4,156.6 95.1,158.3 95.8,160.0 96.5,161.7 97.2,163.3 97.9,165.0 98.6,166.6 99.2,168.1 99.9,169.7 100.6,171.2 101.3,172.7 102.0,174.1 102.7,175.6 103.4,177.0 104.1,178.4 104.8,179.8 105.5,181.1 106.2,182.4 106.9,183.7 107.6,185.0 108.3,186.3 109.0,187.5 109.7,188.7 110.4,189.9 111.1,191.0 111.8,192.1 112.4,193.2 113.1,194.3 113.8,195.3 114.5,196.4 115.2,197.4 115.9,198.3 116.6,199.3 117.3,200.2 118.0,201.1 118.7,202.0 119.4,202.9 120.1,203.7 120.8,204.5 121.5,205.3 122.2,206.0 122.9,206.7 123.6,207.4 124.3,208.1 124.9,208.8 125.6,209.4 126.3,210.0 127.0,210.6 127.7,211.1 128.4,211.7 129.1,212.2 129.8,212.7 130.5,213.1 131.2,213.6 131.9,214.0 132.6,214.3 133.3,214.7 134.0,215.0 134.7,215.3 135.4,215.6 136.1,215.9 136.8,216.1 137.4,216.3 138.1,216.5 138.8,216.7 139.5,216.8 140.2,216.9 140.9,217.0 141.6,217.1 142.3,217.1 143.0,217.1 143.7,217.1 144.4,217.1 145.1,217.0 145.8,216.9 146.5,216.8 147.2,216.7 147.9,216.5 148.6,216.3 149.2,216.1 149.9,215.9 150.6,215.6 151.3,215.3 152.0,215.0 152.7,214.7 153.4,214.3 154.1,214.0 154.8,213.6 155.5,213.1 156.2,212.7 156.9,212.2 157.6,211.7 158.3,211.1 159.0,210.6 159.7,210.0 160.4,209.4 161.1,208.8 161.8,208.1 162.4,207.4 163.1,206.7 163.8,206.0 164.5,205.3 165.2,204.5 165.9,203.7 166.6,202.9 167.3,202.0 168.0,201.1 168.7,200.2 169.4,199.3 170.1,198.3 170.8,197.4 171.5,196.4 172.2,195.3 172.9,194.3 173.6,193.2 174.2,192.1 174.9,191.0 175.6,189.9 176.3,188.7 177.0,187.5 177.7,186.3 178.4,185.0 179.1,183.7 179.8,182.4 180.5,181.1 181.2,179.8 181.9,178.4 182.6,177.0 183.3,175.6 184.0,174.1 184.7,172.7 185.4,171.2 186.1,169.7 186.8,168.1 187.4,166.6 188.1,165.0 188.8,163.3 189.5,161.7 190.2,160.0 190.9,158.3 191.6,156.6 192.3,154.9 193.0,153.1 193.7,151.3 194.4,149.5 195.1,147.7 195.8,145.8 196.5,143.9 197.2,142.0 197.9,140.1 198.6,138.1 199.3,136.1 199.9,134.1 200.6,132.1 201.3,130.0 202.0,127.9 202.7,125.8 203.4,123.7 204.1,121.5 204.8,119.3 205.5,117.1 206.2,114.9 206.9,112.6 207.6,110.3 208.3,108.0 209.0,105.7 209.7,103.3 210.4,101.0 211.1,98.6 211.8,96.1 212.4,93.7 213.1,91.2 213.8,88.7 214.5,86.1 215.2,83.6 215.9,81.0 216.6,78.4 217.3,75.8 218.0,73.1 218.7,70.4 219.4,67.7 220.1,65.0 220.8,62.3 221.5,59.5 222.2,56.7 222.9,53.9 223.6,51.0 224.2,48.1 224.9,45.2 225.6,42.3 226.3,39.3 227.0,36.4 227.7,33.4 228.4,30.3 229.1,27.3 229.8,24.2 230.5,21.1 231.2,18.0 231.9,14.9\"/><text class=\"al\" x=\"202.7\" y=\"134.6\" text-anchor=\"start\" style=\"font-size:12px\">y = x²</text><circle class=\"pt\" cx=\"64.9\" cy=\"60.9\" r=\"3.2\"/><text class=\"lb\" x=\"58.9\" y=\"54.9\" text-anchor=\"end\" style=\"font-size:11px\">(−2, 4)</text><circle class=\"pt\" cx=\"221.1\" cy=\"60.9\" r=\"3.2\"/><text class=\"lb\" x=\"227.1\" y=\"54.9\" text-anchor=\"start\" style=\"font-size:11px\">(2, 4)</text></svg></div>"}, {"kind": "mcq", "text": "The graph of f(x) = x³ − 3x is shown with the line y = 1. Does f have an inverse on all real numbers?", "opts": ["Yes: the graph rises at both ends", "No: the graph passes through the origin", "No: the horizontal line y = 1 cuts the graph three times", "Yes: every vertical line cuts the graph once"], "correct": 2, "tag": "", "sol": "Horizontal line test: y = 1 meets the graph at three points, so three inputs share the output 1 and f is not one-to-one. The vertical line test only shows f is a function.", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 233 284\" role=\"img\" aria-label=\"A cubic graph with a turning point on each side of the origin, and a horizontal line\"><line class=\"tk\" x1=\"41.4\" y1=\"264.0\" x2=\"41.4\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"80.5\" y1=\"264.0\" x2=\"80.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"119.6\" y1=\"264.0\" x2=\"119.6\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"158.6\" y1=\"264.0\" x2=\"158.6\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"197.7\" y1=\"264.0\" x2=\"197.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"256.2\" x2=\"221.1\" y2=\"256.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"217.1\" x2=\"221.1\" y2=\"217.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"178.1\" x2=\"221.1\" y2=\"178.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"221.1\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"99.9\" x2=\"221.1\" y2=\"99.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"60.9\" x2=\"221.1\" y2=\"60.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"21.8\" x2=\"221.1\" y2=\"21.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"139.0\" x2=\"221.1\" y2=\"139.0\"/><line class=\"ln\" x1=\"119.6\" y1=\"264.0\" x2=\"119.6\" y2=\"14.0\"/><text class=\"lb\" x=\"219.1\" y=\"134.0\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"125.6\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"41.4\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"197.7\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"115.6\" y=\"221.1\" text-anchor=\"end\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"115.6\" y=\"64.9\" text-anchor=\"end\" style=\"font-size:10px\">2</text><line class=\"arm hid\" x1=\"18.0\" y1=\"99.9\" x2=\"221.1\" y2=\"99.9\"/><text class=\"al\" x=\"219.1\" y=\"114.9\" text-anchor=\"end\" style=\"font-size:11px\">y = 1</text><polyline class=\"arm\" points=\"37.2,258.2 37.7,252.5 38.3,246.8 38.9,241.2 39.4,235.7 40.0,230.3 40.6,225.1 41.1,219.9 41.7,214.8 42.3,209.8 42.8,204.9 43.4,200.1 44.0,195.4 44.5,190.8 45.1,186.3 45.6,181.9 46.2,177.6 46.8,173.4 47.3,169.2 47.9,165.2 48.5,161.2 49.0,157.3 49.6,153.6 50.2,149.9 50.7,146.3 51.3,142.7 51.9,139.3 52.4,136.0 53.0,132.7 53.5,129.5 54.1,126.4 54.7,123.4 55.2,120.4 55.8,117.6 56.4,114.8 56.9,112.1 57.5,109.5 58.1,106.9 58.6,104.5 59.2,102.1 59.8,99.8 60.3,97.5 60.9,95.4 61.4,93.3 62.0,91.3 62.6,89.3 63.1,87.5 63.7,85.6 64.3,83.9 64.8,82.3 65.4,80.7 66.0,79.1 66.5,77.7 67.1,76.3 67.7,74.9 68.2,73.7 68.8,72.5 69.3,71.3 69.9,70.3 70.5,69.3 71.0,68.3 71.6,67.4 72.2,66.6 72.7,65.8 73.3,65.1 73.9,64.5 74.4,63.9 75.0,63.3 75.6,62.8 76.1,62.4 76.7,62.0 77.2,61.7 77.8,61.4 78.4,61.2 78.9,61.1 79.5,61.0 80.1,60.9 80.6,60.9 81.2,60.9 81.8,61.0 82.3,61.1 82.9,61.3 83.5,61.5 84.0,61.8 84.6,62.1 85.1,62.5 85.7,62.9 86.3,63.3 86.8,63.8 87.4,64.3 88.0,64.9 88.5,65.5 89.1,66.1 89.7,66.8 90.2,67.5 90.8,68.3 91.4,69.1 91.9,69.9 92.5,70.8 93.0,71.7 93.6,72.6 94.2,73.6 94.7,74.5 95.3,75.6 95.9,76.6 96.4,77.7 97.0,78.8 97.6,80.0 98.1,81.1 98.7,82.3 99.2,83.6 99.8,84.8 100.4,86.1 100.9,87.4 101.5,88.7 102.1,90.0 102.6,91.4 103.2,92.8 103.8,94.2 104.3,95.6 104.9,97.1 105.5,98.5 106.0,100.0 106.6,101.5 107.1,103.0 107.7,104.5 108.3,106.1 108.8,107.6 109.4,109.2 110.0,110.8 110.5,112.4 111.1,114.0 111.7,115.6 112.2,117.3 112.8,118.9 113.4,120.5 113.9,122.2 114.5,123.9 115.0,125.5 115.6,127.2 116.2,128.9 116.7,130.6 117.3,132.2 117.9,133.9 118.4,135.6 119.0,137.3 119.6,139.0 120.1,140.7 120.7,142.4 121.3,144.1 121.8,145.8 122.4,147.4 122.9,149.1 123.5,150.8 124.1,152.5 124.6,154.1 125.2,155.8 125.8,157.5 126.3,159.1 126.9,160.7 127.5,162.4 128.0,164.0 128.6,165.6 129.2,167.2 129.7,168.8 130.3,170.4 130.8,171.9 131.4,173.5 132.0,175.0 132.5,176.5 133.1,178.0 133.7,179.5 134.2,180.9 134.8,182.4 135.4,183.8 135.9,185.2 136.5,186.6 137.1,188.0 137.6,189.3 138.2,190.6 138.7,191.9 139.3,193.2 139.9,194.4 140.4,195.7 141.0,196.9 141.6,198.0 142.1,199.2 142.7,200.3 143.3,201.4 143.8,202.4 144.4,203.5 145.0,204.4 145.5,205.4 146.1,206.3 146.6,207.2 147.2,208.1 147.8,208.9 148.3,209.7 148.9,210.5 149.5,211.2 150.0,211.9 150.6,212.5 151.2,213.1 151.7,213.7 152.3,214.2 152.9,214.7 153.4,215.1 154.0,215.5 154.5,215.9 155.1,216.2 155.7,216.5 156.2,216.7 156.8,216.9 157.4,217.0 157.9,217.1 158.5,217.1 159.1,217.1 159.6,217.0 160.2,216.9 160.8,216.8 161.3,216.6 161.9,216.3 162.4,216.0 163.0,215.6 163.6,215.2 164.1,214.7 164.7,214.1 165.3,213.5 165.8,212.9 166.4,212.2 167.0,211.4 167.5,210.6 168.1,209.7 168.7,208.7 169.2,207.7 169.8,206.7 170.3,205.5 170.9,204.3 171.5,203.1 172.0,201.7 172.6,200.3 173.2,198.9 173.7,197.3 174.3,195.7 174.9,194.1 175.4,192.4 176.0,190.5 176.6,188.7 177.1,186.7 177.7,184.7 178.2,182.6 178.8,180.5 179.4,178.2 179.9,175.9 180.5,173.5 181.1,171.1 181.6,168.5 182.2,165.9 182.8,163.2 183.3,160.4 183.9,157.6 184.4,154.6 185.0,151.6 185.6,148.5 186.1,145.3 186.7,142.0 187.3,138.7 187.8,135.3 188.4,131.7 189.0,128.1 189.5,124.4 190.1,120.7 190.7,116.8 191.2,112.8 191.8,108.8 192.3,104.6 192.9,100.4 193.5,96.1 194.0,91.7 194.6,87.2 195.2,82.6 195.7,77.9 196.3,73.1 196.9,68.2 197.4,63.2 198.0,58.1 198.6,52.9 199.1,47.7 199.7,42.3 200.2,36.8 200.8,31.2 201.4,25.5 201.9,19.8\"/><text class=\"al\" x=\"204.6\" y=\"36.7\" text-anchor=\"start\" style=\"font-size:12px\">f</text></svg></div>"}, {"kind": "blank", "p": "f(x) = 2x + 6. Compare f⁻¹(2) with 1/f(2).", "tag": "", "marks": "", "flat": [{"t": "f(2) = __B1__", "a": {"B1": "10"}}, {"t": "1/f(2) = __B1__", "a": {"B1": "1/10"}}, {"t": "Swap and solve: f⁻¹(x) = __B1__", "a": {"B1": "(x-6)/2"}, "expr": true}, {"t": "f⁻¹(2) = __B1__", "a": {"B1": "-2"}}], "sol": "2 · 2 + 6 = 10.\n1/10 = 0.1.\nx = 2y + 6, so y = (x − 6)/2.\n(2 − 6)/2 = −2, which is not 1/10: f⁻¹(x) and 1/f(x) are different things."}, {"kind": "mcq", "text": "What does f⁻¹(x) mean?", "opts": ["−f(x), the negative of f(x)", "1/f(x), the reciprocal of f(x)", "The function that undoes f: if f(a) = b then f⁻¹(b) = a", "f(−x), f with the input negated"], "correct": 2, "tag": "", "sol": "The −1 in f⁻¹ is notation, not an exponent. f⁻¹ sends each output of f back to its input. The reciprocal is written 1/f(x) or [f(x)]⁻¹."}, {"kind": "blank", "p": "The mapping diagram shows a function f.", "tag": "", "marks": "", "flat": [{"t": "Each output comes from exactly one input, so f is __B1__", "a": {"B1": "one-to-one"}, "expr": "words", "accept": ["one to one", "injective", "1-1", "1 to 1"]}, {"t": "f⁻¹(9) = __B1__", "a": {"B1": "2"}}, {"t": "f⁻¹(f(3)) = __B1__", "a": {"B1": "3"}}, {"t": "The point (4, 7) on f becomes the point __B1__ on f⁻¹", "a": {"B1": "(7, 4)"}, "expr": "coord"}], "sol": "No two arrows end at the same output.\nThe arrow into 9 starts at 2.\nf(3) = 4 and f⁻¹(4) = 3: f⁻¹ undoes f.\nSwap the coordinates: (7, 4).", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 300 180\" role=\"img\" aria-label=\"Mapping diagram from inputs to outputs\"><ellipse class=\"wg\" cx=\"70\" cy=\"95\" rx=\"38\" ry=\"70\"/><ellipse class=\"wg\" cx=\"230\" cy=\"95\" rx=\"38\" ry=\"70\"/><text class=\"lb\" x=\"70.0\" y=\"16.0\" text-anchor=\"middle\">x</text><text class=\"lb\" x=\"230.0\" y=\"16.0\" text-anchor=\"middle\">f(x)</text><text class=\"al\" x=\"150.0\" y=\"16.0\" text-anchor=\"middle\">f</text><text class=\"lb\" x=\"70.0\" y=\"50.0\" text-anchor=\"middle\">1</text><text class=\"lb\" x=\"70.0\" y=\"83.3\" text-anchor=\"middle\">2</text><text class=\"lb\" x=\"70.0\" y=\"116.7\" text-anchor=\"middle\">3</text><text class=\"lb\" x=\"70.0\" y=\"150.0\" text-anchor=\"middle\">4</text><text class=\"lb\" x=\"230.0\" y=\"50.0\" text-anchor=\"middle\">4</text><text class=\"lb\" x=\"230.0\" y=\"83.3\" text-anchor=\"middle\">6</text><text class=\"lb\" x=\"230.0\" y=\"116.7\" text-anchor=\"middle\">7</text><text class=\"lb\" x=\"230.0\" y=\"150.0\" text-anchor=\"middle\">9</text><line class=\"arm\" x1=\"84.0\" y1=\"45.0\" x2=\"208.0\" y2=\"78.3\"/><polygon class=\"pt\" points=\"208.0,78.3 200.1,79.4 201.7,73.4\"/><line class=\"arm\" x1=\"84.0\" y1=\"78.3\" x2=\"208.0\" y2=\"145.0\"/><polygon class=\"pt\" points=\"208.0,145.0 200.0,144.3 203.0,138.8\"/><line class=\"arm\" x1=\"84.0\" y1=\"111.7\" x2=\"208.0\" y2=\"45.0\"/><polygon class=\"pt\" points=\"208.0,45.0 203.0,51.2 200.0,45.7\"/><line class=\"arm\" x1=\"84.0\" y1=\"145.0\" x2=\"208.0\" y2=\"111.7\"/><polygon class=\"pt\" points=\"208.0,111.7 201.7,116.6 200.1,110.6\"/></svg></div>"}, {"kind": "mcq", "text": "f(x) = (x − 2)² is not one-to-one. Which restriction makes it one-to-one and still includes x = 5?", "opts": ["x ≥ 0", "x ≤ 2", "x ≥ 2", "x ≥ −2"], "correct": 2, "tag": "", "sol": "The vertex is at x = 2, so each half of the parabola, x ≥ 2 or x ≤ 2, is one-to-one. Only x ≥ 2 contains 5. On x ≥ 0, f(1) = f(3) = 1, so it still repeats; x ≥ −2 is worse."}, {"kind": "blank", "p": "The table gives some values of a one-to-one function h.\nx: 0, 1, 2, 3, 4\nh(x): 3, 5, 9, 17, 33", "tag": "", "marks": "", "flat": [{"t": "h⁻¹(17) = __B1__ and h⁻¹(5) = __B2__", "a": {"B1": "3", "B2": "1"}}, {"t": "h(h⁻¹(9)) = __B1__", "a": {"B1": "9"}}, {"t": "h⁻¹(h(4)) = __B1__", "a": {"B1": "4"}}], "sol": "Find the output in the bottom row and read its input: h(3) = 17, h(1) = 5.\nh⁻¹(9) = 2 and h(2) = 9: composing gives back 9.\nh(4) = 33 and h⁻¹(33) = 4."}]}, {"id": "s2", "label": "2 · Linear inverses", "sub": "The five-step procedure on linear functions (Paul's Practice 1–2, Assignment 1–2)", "slides": [{"kind": "blank", "p": "Find the inverse of f(x) = 6x + 15.", "tag": "Paul · Practice 1", "marks": "", "flat": [{"t": "Write y = 6x + 15, then swap x and y: x = __B1__", "a": {"B1": "6y+15"}, "expr": true}, {"t": "Solve for y: f⁻¹(x) = __B1__", "a": {"B1": "(x-15)/6"}, "expr": true}, {"t": "Check: f(2) = 27, so f⁻¹(27) should be __B1__", "a": {"B1": "2"}}], "sol": "Swapping gives x = 6y + 15.\nx − 15 = 6y, so y = (x − 15)/6: f⁻¹(x) = (x − 15)/6.\n(27 − 15)/6 = 2 ✔. Composition: f(f⁻¹(x)) = 6 · (x − 15)/6 + 15 = x."}, {"kind": "mcq", "text": "What is the inverse of f(x) = 5x − 4?", "opts": ["f⁻¹(x) = (x + 4)/5", "f⁻¹(x) = x/5 + 4", "f⁻¹(x) = (x − 4)/5", "f⁻¹(x) = 1/(5x − 4)"], "correct": 0, "tag": "", "sol": "Swap: x = 5y − 4, so x + 4 = 5y and y = (x + 4)/5. Undo in reverse order: add 4 first, then divide by 5. x/5 + 4 divides first; 1/(5x − 4) is the reciprocal."}, {"kind": "blank", "p": "Find the inverse of f(x) = 3 − 29x.", "tag": "Paul · Practice 2", "marks": "", "flat": [{"t": "Swap: x = 3 − 29y.  Subtract 3: x − 3 = __B1__", "a": {"B1": "-29y"}, "expr": true}, {"t": "Solve: f⁻¹(x) = __B1__", "a": {"B1": "(3-x)/29"}, "expr": true}, {"t": "f⁻¹(3) = __B1__", "a": {"B1": "0"}}], "sol": "x − 3 = −29y.\ny = (x − 3)/(−29) = (3 − x)/29.\n(3 − 3)/29 = 0. Check: f(0) = 3 ✔."}, {"kind": "mcq", "text": "Asha found the inverse of g(x) = 4x + 12 as g⁻¹(x) = x/4 + 12. What went wrong?", "opts": ["She should have written 1/(4x + 12)", "She forgot the sign: g⁻¹(x) = −x/4 − 12", "She undid the steps in the wrong order; subtract 12 first, then divide by 4: g⁻¹(x) = (x − 12)/4", "Nothing: x/4 + 12 is correct"], "correct": 2, "tag": "", "sol": "Check: g(1) = 16, but 16/4 + 12 = 16, not 1. From x = 4y + 12: x − 12 = 4y, so y = (x − 12)/4, which gives (16 − 12)/4 = 1 ✔."}, {"kind": "blank", "p": "Find the inverse of f(x) = 11x − 8.", "tag": "Paul · Assignment 1", "marks": "", "flat": [{"t": "Swap: x = __B1__", "a": {"B1": "11y-8"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(x+8)/11"}, "expr": true}, {"t": "Verify: f⁻¹(f(x)) = ((11x − 8) + 8)/11 = __B1__", "a": {"B1": "x"}, "expr": true}], "sol": "Replace f(x) with y and swap: x = 11y − 8.\nx + 8 = 11y, so f⁻¹(x) = (x + 8)/11.\n(11x)/11 = x ✔, so the inverse is right."}, {"kind": "mcq", "text": "Which function g undoes f(x) = 3x − 2, so that f(g(x)) = x and g(f(x)) = x?", "opts": ["g(x) = x/3 + 2/3", "g(x) = 3x + 2", "g(x) = 1/(3x − 2)", "g(x) = x/3 − 2/3"], "correct": 0, "tag": "", "sol": "f(g(x)) = 3(x/3 + 2/3) − 2 = x + 2 − 2 = x, and g(f(x)) = (3x − 2)/3 + 2/3 = x. With x/3 − 2/3 we get f(g(x)) = x − 4."}, {"kind": "blank", "p": "Find the inverse of f(x) = 4 − 10x.", "tag": "Paul · Assignment 2", "marks": "", "flat": [{"t": "Swap: x = 4 − 10y, so 10y = __B1__", "a": {"B1": "4-x"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(4-x)/10"}, "expr": true}, {"t": "f⁻¹(−6) = __B1__", "a": {"B1": "1"}}], "sol": "Add 10y and subtract x: 10y = 4 − x.\ny = (4 − x)/10.\n(4 + 6)/10 = 1. Check: f(1) = 4 − 10 = −6 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = (x − 7)/2?", "opts": ["f⁻¹(x) = 2x + 7", "f⁻¹(x) = 2/(x − 7)", "f⁻¹(x) = (x + 7)/2", "f⁻¹(x) = 2x − 7"], "correct": 0, "tag": "", "sol": "f subtracts 7, then halves. Undo in reverse: double, then add 7. Swap: x = (y − 7)/2, so 2x = y − 7 and y = 2x + 7."}, {"kind": "blank", "p": "Find the inverse of f(x) = (2/3)x + 5.", "tag": "", "marks": "", "flat": [{"t": "Swap: x = (2/3)y + 5, so (2/3)y = __B1__", "a": {"B1": "x-5"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "3(x-5)/2"}, "expr": true}, {"t": "f⁻¹(9) = __B1__", "a": {"B1": "6"}}], "sol": "Subtract 5: (2/3)y = x − 5.\nMultiply by 3/2: y = 3(x − 5)/2 = (3x − 15)/2.\n3 · 4/2 = 6. Check: f(6) = 4 + 5 = 9 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = 4 − x?", "opts": ["f⁻¹(x) = 1/(4 − x)", "f⁻¹(x) = x − 4", "f⁻¹(x) = 4 − x: f is its own inverse", "f⁻¹(x) = x + 4"], "correct": 2, "tag": "", "sol": "Swap: x = 4 − y, so y = 4 − x, the same rule. Check: f(f(x)) = 4 − (4 − x) = x. Its graph is symmetric about y = x."}, {"kind": "blank", "p": "The general linear function f(x) = ax + b, with a ≠ 0.", "tag": "", "marks": "", "flat": [{"t": "Swap and solve: f⁻¹(x) = __B1__", "a": {"B1": "(x-b)/a"}, "expr": true}, {"t": "The slope of f⁻¹ is __B1__", "a": {"B1": "1/a"}, "expr": true}, {"t": "For a = 4, b = 1: the slope of f⁻¹ is __B1__", "a": {"B1": "1/4"}}], "sol": "x = ay + b gives y = (x − b)/a.\n(x − b)/a = (1/a)x − b/a: slope 1/a.\n1/4: the slopes of f and f⁻¹ are reciprocals."}]}, {"id": "s3", "label": "3 · Powers & roots", "sub": "Cubes, fifth and seventh powers and roots, undone in reverse order (Paul's Practice 3–6, Assignment 3–6)", "slides": [{"kind": "blank", "p": "Find the inverse of R(x) = x³ + 6.", "tag": "Paul · Practice 3", "marks": "", "flat": [{"t": "Replace R(x) with y and swap: x = __B1__", "a": {"B1": "y^3+6"}, "expr": true}, {"t": "Solve: R⁻¹(x) = ∛( __B1__ )", "a": {"B1": "x-6"}, "expr": true}, {"t": "R⁻¹(−2) = __B1__", "a": {"B1": "-2"}}, {"t": "Check: R(R⁻¹(x)) = (∛(x − 6))³ + 6 = __B1__", "a": {"B1": "x"}, "expr": true}], "sol": "x = y³ + 6.\ny³ = x − 6, so R⁻¹(x) = ∛(x − 6).\n∛(−2 − 6) = ∛(−8) = −2.\n(x − 6) + 6 = x ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = x³ − 8?", "opts": ["f⁻¹(x) = ∛(x − 8)", "f⁻¹(x) = ∛x + 8", "f⁻¹(x) = 1/(x³ − 8)", "f⁻¹(x) = ∛(x + 8)"], "correct": 3, "tag": "", "sol": "Swap: x = y³ − 8, so y³ = x + 8 and y = ∛(x + 8). The 8 must be undone before the cube root. Check: f(2) = 0 and ∛(0 + 8) = 2."}, {"kind": "blank", "p": "Find the inverse of g(x) = 4(x − 3)⁵ + 21.", "tag": "Paul · Practice 4", "marks": "", "flat": [{"t": "Swap: x = 4(y − 3)⁵ + 21.  Subtract 21: 4(y − 3)⁵ = __B1__", "a": {"B1": "x-21"}, "expr": true}, {"t": "Divide by 4 and take the fifth root: g⁻¹(x) = 3 + ⁵√( __B1__ )", "a": {"B1": "(x-21)/4"}, "expr": true}, {"t": "g⁻¹(25) = __B1__", "a": {"B1": "4"}}, {"t": "g⁻¹(17) = __B1__", "a": {"B1": "2"}}], "sol": "4(y − 3)⁵ = x − 21.\n(y − 3)⁵ = (x − 21)/4, so y − 3 = ⁵√((x − 21)/4) and g⁻¹(x) = 3 + ⁵√((x − 21)/4).\n3 + ⁵√(4/4) = 3 + 1 = 4. Check: g(4) = 4 + 21 = 25 ✔.\n3 + ⁵√(−4/4) = 3 + (−1) = 2. Check: g(2) = 4(−1) + 21 = 17 ✔."}, {"kind": "mcq", "text": "What is the inverse of g(x) = 2(x + 1)³?", "opts": ["g⁻¹(x) = ∛(x/2 − 1)", "g⁻¹(x) = ∛(x/2) + 1", "g⁻¹(x) = ∛(2x) − 1", "g⁻¹(x) = ∛(x/2) − 1"], "correct": 3, "tag": "", "sol": "g adds 1, cubes, then doubles. Undo in reverse: halve, cube root, subtract 1. Check: g(1) = 16 and ∛8 − 1 = 1."}, {"kind": "blank", "p": "Find the inverse of W(x) = ⁵√(9 − 11x).", "tag": "Paul · Practice 5", "marks": "", "flat": [{"t": "Swap: x = ⁵√(9 − 11y).  Raise both sides to the 5th power: x⁵ = __B1__", "a": {"B1": "9-11y"}, "expr": true}, {"t": "W⁻¹(x) = __B1__", "a": {"B1": "(9-x^5)/11"}, "expr": true}, {"t": "W⁻¹(1) = __B1__", "a": {"B1": "8/11"}}], "sol": "(⁵√(9 − 11y))⁵ = 9 − 11y.\n11y = 9 − x⁵, so W⁻¹(x) = (9 − x⁵)/11, a polynomial.\n(9 − 1)/11 = 8/11. Check: W(8/11) = ⁵√(9 − 8) = 1 ✔."}, {"kind": "mcq", "text": "Why does f(x) = x⁵ have an inverse on all real numbers while f(x) = x⁴ does not?", "opts": ["x⁴ grows faster than x⁵", "x⁴ is not a function", "x⁵ is one-to-one (always increasing), but x⁴ gives the same output for x and −x", "Fifth roots of negative numbers do not exist"], "correct": 2, "tag": "", "sol": "(−2)⁴ = 2⁴ = 16, so x⁴ fails the horizontal line test. Odd powers keep the sign, are always increasing and pass it. Fifth roots of negatives do exist: ⁵√(−32) = −2."}, {"kind": "blank", "p": "Find the inverse of f(x) = ⁷√(5x + 8).", "tag": "Paul · Practice 6", "marks": "", "flat": [{"t": "Swap: x = ⁷√(5y + 8).  Raise to the 7th power and subtract 8: x⁷ − 8 = __B1__", "a": {"B1": "5y"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(x^7-8)/5"}, "expr": true}, {"t": "f⁻¹(1) = __B1__", "a": {"B1": "-7/5"}}], "sol": "x⁷ = 5y + 8, so x⁷ − 8 = 5y.\ny = (x⁷ − 8)/5.\n(1 − 8)/5 = −7/5. Check: f(−7/5) = ⁷√(−7 + 8) = 1 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = √(x − 3)?", "opts": ["f⁻¹(x) = x² + 3, for all real x", "f⁻¹(x) = (x + 3)², for x ≥ 0", "f⁻¹(x) = x² − 3, for x ≥ 0", "f⁻¹(x) = x² + 3, for x ≥ 0"], "correct": 3, "tag": "", "sol": "Swap: x = √(y − 3), so x² = y − 3 and y = x² + 3. The range of f is y ≥ 0, so the domain of f⁻¹ is x ≥ 0; without it x² + 3 is not one-to-one."}, {"kind": "blank", "p": "Find the inverse of Z(x) = 2x⁷ − 9.", "tag": "Paul · Assignment 3", "marks": "", "flat": [{"t": "Swap: x = 2y⁷ − 9.  Add 9: x + 9 = __B1__", "a": {"B1": "2y^7"}, "expr": true}, {"t": "Z⁻¹(x) = ⁷√( __B1__ )", "a": {"B1": "(x+9)/2"}, "expr": true}, {"t": "Z⁻¹(−11) = __B1__", "a": {"B1": "-1"}}], "sol": "x + 9 = 2y⁷.\ny⁷ = (x + 9)/2, so Z⁻¹(x) = ⁷√((x + 9)/2).\n⁷√(−2/2) = ⁷√(−1) = −1. Check: Z(−1) = −2 − 9 = −11 ✔."}, {"kind": "mcq", "text": "In which order must you undo f(x) = 3x⁵ − 2 to find f⁻¹?", "opts": ["Add 2, divide by 3, take the fifth root", "Divide by 3, add 2, take the fifth root", "Add 2, take the fifth root, divide by 3", "Take the fifth root, divide by 3, add 2"], "correct": 0, "tag": "", "sol": "f takes the fifth power, multiplies by 3, then subtracts 2. Undo from last to first: add 2, divide by 3, fifth root. So f⁻¹(x) = ⁵√((x + 2)/3)."}, {"kind": "blank", "p": "Find the inverse of h(x) = 7 + (2x + 1)³.", "tag": "Paul · Assignment 4", "marks": "", "flat": [{"t": "Swap: x = 7 + (2y + 1)³, so (2y + 1)³ = __B1__", "a": {"B1": "x-7"}, "expr": true}, {"t": "2y + 1 = ∛(x − 7), so h⁻¹(x) = (∛(x − 7) − __B1__)/__B2__", "a": {"B1": "1", "B2": "2"}}, {"t": "h⁻¹(15) = __B1__", "a": {"B1": "1/2"}}, {"t": "h⁻¹(−1) = __B1__", "a": {"B1": "-3/2"}}], "sol": "Subtract 7: (2y + 1)³ = x − 7.\nCube root, subtract 1, divide by 2: h⁻¹(x) = (∛(x − 7) − 1)/2.\n(∛8 − 1)/2 = 1/2. Check: h(1/2) = 7 + 2³ = 15 ✔.\n(∛(−8) − 1)/2 = (−2 − 1)/2 = −3/2. Check: h(−3/2) = 7 + (−2)³ = −1 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = ∛(x + 1)?", "opts": ["f⁻¹(x) = x³ − 1", "f⁻¹(x) = (x − 1)³", "f⁻¹(x) = x³ + 1", "f⁻¹(x) = ∛(x − 1)"], "correct": 0, "tag": "", "sol": "Swap: x = ∛(y + 1). Cube both sides: x³ = y + 1, so y = x³ − 1. A cube undoes a cube root; another cube root does not. Check: f(7) = 2 and 2³ − 1 = 7."}, {"kind": "blank", "p": "Find the inverse of W(x) = ⁷√(15x + 2).", "tag": "Paul · Assignment 5", "marks": "", "flat": [{"t": "Swap and raise to the 7th power: x⁷ = __B1__", "a": {"B1": "15y+2"}, "expr": true}, {"t": "W⁻¹(x) = __B1__", "a": {"B1": "(x^7-2)/15"}, "expr": true}, {"t": "W⁻¹(1) = __B1__", "a": {"B1": "-1/15"}}], "sol": "x = ⁷√(15y + 2), so x⁷ = 15y + 2.\n15y = x⁷ − 2, so W⁻¹(x) = (x⁷ − 2)/15.\n(1 − 2)/15 = −1/15. Check: W(−1/15) = ⁷√(−1 + 2) = 1 ✔."}, {"kind": "blank", "p": "Find the inverse of f(x) = ∛(6 − 18x).", "tag": "Paul · Assignment 6", "marks": "", "flat": [{"t": "Swap and cube both sides: x³ = __B1__", "a": {"B1": "6-18y"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(6-x^3)/18"}, "expr": true}, {"t": "f⁻¹(−3) = __B1__", "a": {"B1": "11/6"}}], "sol": "x = ∛(6 − 18y), so x³ = 6 − 18y.\n18y = 6 − x³, so f⁻¹(x) = (6 − x³)/18.\n(6 + 27)/18 = 33/18 = 11/6. Check: f(11/6) = ∛(6 − 33) = ∛(−27) = −3 ✔."}]}, {"id": "s4", "label": "4 · Rational inverses", "sub": "Clear the fraction, collect the y terms and factor (Paul's Practice 7–8, Assignment 7–8)", "slides": [{"kind": "blank", "p": "Find the inverse of h(x) = (1 + 9x)/(4 − x).", "tag": "Paul · Practice 7", "marks": "", "flat": [{"t": "Swap: x = (1 + 9y)/(4 − y).  Multiply out: 4x − xy = __B1__", "a": {"B1": "1+9y"}, "expr": true}, {"t": "Collect the y terms: 4x − 1 = __B1__", "a": {"B1": "9y+xy"}, "expr": true}, {"t": "h⁻¹(x) = __B1__", "a": {"B1": "(4x-1)/(x+9)"}, "expr": true}, {"t": "h⁻¹(2) = __B1__", "a": {"B1": "7/11"}}], "sol": "x(4 − y) = 1 + 9y gives 4x − xy = 1 + 9y.\nMove −xy right and 1 left: 4x − 1 = 9y + xy = y(9 + x).\ny = (4x − 1)/(x + 9).\n(8 − 1)/(2 + 9) = 7/11. Check: h(7/11) = (1 + 63/11)/(4 − 7/11) = (74/11)/(37/11) = 2 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = (x + 2)/(x − 3)?", "opts": ["f⁻¹(x) = (x − 3)/(x + 2)", "f⁻¹(x) = (3x − 2)/(x − 1)", "f⁻¹(x) = (x − 2)/(x + 3)", "f⁻¹(x) = (3x + 2)/(x − 1)"], "correct": 3, "tag": "", "sol": "Swap: x = (y + 2)/(y − 3). Then xy − 3x = y + 2, so xy − y = 3x + 2, y(x − 1) = 3x + 2 and y = (3x + 2)/(x − 1). (x − 3)/(x + 2) is 1/f(x)."}, {"kind": "blank", "p": "Find the inverse of f(x) = (6 − 10x)/(8x + 7).", "tag": "Paul · Practice 8", "marks": "", "flat": [{"t": "Swap: x = (6 − 10y)/(8y + 7).  Multiply out: 8xy + 7x = __B1__", "a": {"B1": "6-10y"}, "expr": true}, {"t": "Collect the y terms: y(8x + 10) = __B1__", "a": {"B1": "6-7x"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(6-7x)/(8x+10)"}, "expr": true}, {"t": "f⁻¹(0) = __B1__", "a": {"B1": "3/5"}}], "sol": "x(8y + 7) = 6 − 10y.\n8xy + 10y = 6 − 7x, so y(8x + 10) = 6 − 7x.\ny = (6 − 7x)/(8x + 10).\n6/10 = 3/5. Check: f(3/5) = (6 − 6)/(…) = 0 ✔."}, {"kind": "mcq", "text": "Kiran is solving x = (2y + 1)/(y − 4) for y. He writes: x(y − 4) = 2y + 1, so xy − 4x = 2y + 1, so xy − 2y = 1 − 4x. Which statement is correct?", "opts": ["The first step should be x = (y − 4)/(2y + 1)", "Every step is correct", "He should cancel y from the top and bottom first", "The last step has a sign error: moving −4x across gives xy − 2y = 4x + 1"], "correct": 3, "tag": "", "sol": "From xy − 4x = 2y + 1, subtract 2y and add 4x: xy − 2y = 4x + 1. Then y(x − 2) = 4x + 1 and y = (4x + 1)/(x − 2)."}, {"kind": "blank", "p": "Find the inverse of R(x) = (2x + 14)/(6x + 1).", "tag": "Paul · Assignment 7", "marks": "", "flat": [{"t": "Swap: x = (2y + 14)/(6y + 1).  Multiply out: 6xy + x = __B1__", "a": {"B1": "2y+14"}, "expr": true}, {"t": "Collect: 6xy − 2y = 14 − x, so y(6x − 2) = __B1__", "a": {"B1": "14-x"}, "expr": true}, {"t": "R⁻¹(x) = __B1__", "a": {"B1": "(14-x)/(6x-2)"}, "expr": true}, {"t": "R⁻¹(2) = __B1__", "a": {"B1": "6/5"}}], "sol": "x(6y + 1) = 2y + 14.\n6xy − 2y = 14 − x; factor out y.\ny = (14 − x)/(6x − 2).\n12/10 = 6/5. Check: R(6/5) = (12/5 + 14)/(36/5 + 1) = (82/5)/(41/5) = 2 ✔."}, {"kind": "mcq", "text": "After swapping, you have x = (ay + b)/(cy + d). What is the key move once the fraction is cleared?", "opts": ["Cancel the y in the numerator with the y in the denominator", "Collect every y term on one side, then factor out y", "Divide both sides by y", "Take reciprocals of both sides"], "correct": 1, "tag": "", "sol": "x(cy + d) = ay + b gives cxy − ay = b − dx, so y(cx − a) = b − dx. Reciprocals give 1/f, and y cannot be cancelled across a sum."}, {"kind": "blank", "p": "Find the inverse of g(x) = (1 − x)/(9 − 12x).", "tag": "Paul · Assignment 8", "marks": "", "flat": [{"t": "Swap: x = (1 − y)/(9 − 12y).  Multiply out: 9x − 12xy = __B1__", "a": {"B1": "1-y"}, "expr": true}, {"t": "Collect: 9x − 1 = 12xy − y = y(__B1__)", "a": {"B1": "12x-1"}, "expr": true}, {"t": "g⁻¹(x) = __B1__", "a": {"B1": "(9x-1)/(12x-1)"}, "expr": true}, {"t": "g⁻¹(1) = __B1__", "a": {"B1": "8/11"}}], "sol": "x(9 − 12y) = 1 − y.\nMove −12xy right and 1 left: 9x − 1 = 12xy − y = y(12x − 1).\ny = (9x − 1)/(12x − 1).\n8/11. Check: g(8/11) = (3/11)/(3/11) = 1 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = 3/(x − 2)?", "opts": ["f⁻¹(x) = 3/(x + 2)", "f⁻¹(x) = (2x + 3)/x", "f⁻¹(x) = (x − 2)/3", "f⁻¹(x) = 3/x − 2"], "correct": 1, "tag": "", "sol": "Swap: x = 3/(y − 2). Then y − 2 = 3/x, so y = 3/x + 2 = (2x + 3)/x. (x − 2)/3 is 1/f(x); 3/x − 2 has a sign error."}, {"kind": "blank", "p": "Find the inverse of f(x) = (2x − 1)/(x + 3).", "tag": "", "marks": "", "flat": [{"t": "Swap and multiply out: xy + 3x = 2y − 1, so y(x − 2) = __B1__", "a": {"B1": "-1-3x"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(3x+1)/(2-x)"}, "expr": true}, {"t": "The value x = __B1__ is not in the domain of f⁻¹", "a": {"B1": "2"}}, {"t": "f⁻¹(1) = __B1__", "a": {"B1": "4"}}], "sol": "xy − 2y = −1 − 3x.\ny = (−1 − 3x)/(x − 2) = (3x + 1)/(2 − x).\nThe denominator 2 − x is 0 at x = 2 (f never takes the value 2: its horizontal asymptote).\n(3 + 1)/(2 − 1) = 4. Check: f(4) = 7/7 = 1 ✔."}, {"kind": "mcq", "text": "What is the inverse of f(x) = (2x + 5)/(3x − 2)?", "opts": ["f⁻¹(x) = (2x − 5)/(3x + 2)", "f⁻¹(x) = (2x + 5)/(3x + 2)", "f⁻¹(x) = (3x − 2)/(2x + 5)", "f itself: f⁻¹(x) = (2x + 5)/(3x − 2)"], "correct": 3, "tag": "", "sol": "Swap: x(3y − 2) = 2y + 5, so 3xy − 2y = 2x + 5 and y = (2x + 5)/(3x − 2), the same rule: f is its own inverse. (3x − 2)/(2x + 5) is 1/f."}, {"kind": "blank", "p": "Find the inverse of f(x) = 5x/(x + 4).", "tag": "", "marks": "", "flat": [{"t": "Swap: x(y + 4) = 5y, so xy + 4x = 5y.  Collect: 4x = __B1__", "a": {"B1": "5y-xy"}, "expr": true}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "4x/(5-x)"}, "expr": true}, {"t": "f⁻¹(1) = __B1__", "a": {"B1": "1"}}], "sol": "4x = 5y − xy = y(5 − x).\ny = 4x/(5 − x).\n4/4 = 1. Check: f(1) = 5/5 = 1 ✔ (1 is a point where f and f⁻¹ meet on y = x)."}]}, {"id": "s5", "label": "5 · Verifying by composition", "sub": "f(g(x)) and g(f(x)); one composition is usually enough; spot the error", "slides": [{"kind": "blank", "p": "Decide whether f(x) = 2x + 1 and g(x) = (x − 1)/2 are inverses.", "tag": "", "marks": "", "flat": [{"t": "f(g(x)) = 2 · (x − 1)/2 + 1 = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "g(f(x)) = ((2x + 1) − 1)/2 = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "Both compositions give x, so f and g are __B1__", "a": {"B1": "inverses"}, "expr": "words", "accept": ["inverse", "inverse functions", "inverses of each other"]}], "sol": "(x − 1) + 1 = x.\n2x/2 = x.\nf and g undo each other: they are inverses."}, {"kind": "mcq", "text": "f(x) = x³ − 1 and g(x) = ∛x + 1. Are they inverses?", "opts": ["No: f is not one-to-one", "No: f(g(8)) = 26, not 8", "Yes: f(g(0)) = 0", "Yes: one cubes and the other takes a cube root"], "correct": 1, "tag": "", "sol": "g(8) = 2 + 1 = 3 and f(3) = 26 ≠ 8. f(g(0)) = f(1) = 0 works by luck: one number cannot prove inverses. The inverse of f is ∛(x + 1). f = x³ − 1 is one-to-one."}, {"kind": "blank", "p": "Check whether f(x) = 1/(x − 2) and g(x) = 1/x + 2 are inverses.", "tag": "", "marks": "", "flat": [{"t": "g(x) − 2 = __B1__", "a": {"B1": "1/x"}, "expr": true}, {"t": "f(g(x)) = 1/(g(x) − 2) = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "Number check: g(4) = 9/4 and f(9/4) = __B1__", "a": {"B1": "4"}}], "sol": "(1/x + 2) − 2 = 1/x.\n1/(1/x) = x, so f(g(x)) = x (one composition is enough here).\n9/4 − 2 = 1/4 and 1/(1/4) = 4 ✔."}, {"kind": "mcq", "text": "You found f⁻¹ with the five-step procedure. In this course, how much checking is usually enough?", "opts": ["Both compositions, a graph and a table", "None: the procedure never goes wrong", "Checking f⁻¹(0) only", "One composition, such as f(f⁻¹(x)) = x"], "correct": 3, "tag": "", "sol": "One composition confirms the algebra of a procedure answer. Checking a single number can be passed by luck, and errors in step 3 are common, so some check is needed."}, {"kind": "blank", "p": "f(x) = x² + 3 for x ≥ 0, and g(x) = √(x − 3).", "tag": "", "marks": "", "flat": [{"t": "f(g(x)) = (√(x − 3))² + 3 = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "g(f(x)) = √(x²) = |x|, which equals x because x is __B1__", "a": {"B1": "non-negative"}, "expr": "words", "accept": ["nonnegative", "not negative", "zero or positive", "positive or zero", "greater than or equal to zero", "at least zero"]}, {"t": "Without the restriction, g(f(−2)) would be __B1__", "a": {"B1": "2"}}], "sol": "(x − 3) + 3 = x.\nOn the domain x ≥ 0, |x| = x, so g(f(x)) = x and they are inverses.\nf(−2) = 7 and g(7) = 2, not −2: that is why the domain is restricted."}, {"kind": "mcq", "text": "Ravi checks f(x) = 3x + 6 and g(x) = x/3 − 6. He writes f(g(x)) = 3(x/3 − 6) + 6 = x − 6 + 6 = x and says they are inverses. What is wrong?", "opts": ["His algebra is right, but he must also check g(f(x))", "He should have computed 1/f(x)", "He did not distribute the 3: f(g(x)) = x − 18 + 6 = x − 12, so they are not inverses", "Nothing: they are inverses"], "correct": 2, "tag": "", "sol": "3 · (−6) = −18. So f(g(x)) = x − 12 ≠ x. The inverse of f is (x − 6)/3 = x/3 − 2."}, {"kind": "blank", "p": "f(x) = (x + 1)/(x − 1).", "tag": "", "marks": "", "flat": [{"t": "f(3) = 2, and f(2) = __B1__", "a": {"B1": "3"}}, {"t": "f(f(x)) = ((x + 1)/(x − 1) + 1)/((x + 1)/(x − 1) − 1) = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "So f is its own __B1__", "a": {"B1": "inverse"}, "expr": "words", "accept": ["inverses", "inverse function"]}], "sol": "(2 + 1)/(2 − 1) = 3: f sends 3 to 2 and 2 back to 3.\nMultiply top and bottom by (x − 1): (2x)/(2) = x.\nf(f(x)) = x, so f⁻¹ = f."}, {"kind": "mcq", "text": "Which pair of functions are NOT inverses of each other?", "opts": ["f(x) = 5 − x and g(x) = 5 − x", "f(x) = 2x + 3 and g(x) = x/2 − 3", "f(x) = x³ + 2 and g(x) = ∛(x − 2)", "f(x) = 1/x and g(x) = 1/x"], "correct": 1, "tag": "", "sol": "For f(x) = 2x + 3 and g(x) = x/2 − 3, f(g(x)) = 2(x/2 − 3) + 3 = x − 3 ≠ x (the inverse of 2x + 3 is (x − 3)/2). The cube pair undo each other, and 5 − x and 1/x are each their own inverse."}, {"kind": "blank", "p": "h(x) = 7x − 2.", "tag": "", "marks": "", "flat": [{"t": "h⁻¹(x) = __B1__", "a": {"B1": "(x+2)/7"}, "expr": true}, {"t": "h(h⁻¹(x)) = 7 · h⁻¹(x) − 2 = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "h⁻¹(h(10)) = __B1__", "a": {"B1": "10"}}], "sol": "x = 7y − 2, so y = (x + 2)/7.\n(x + 2) − 2 = x ✔.\nh(10) = 68 and h⁻¹(68) = 70/7 = 10."}, {"kind": "mcq", "text": "f(x) = x² and g(x) = √x satisfy f(g(x)) = x for every x ≥ 0. Are they inverses on all real numbers?", "opts": ["No, because f(g(x)) is never equal to x", "No: g(f(−3)) = 3, so g does not undo f for negative x; they are inverses only on x ≥ 0", "Yes, because f(g(x)) = x", "Yes, squares and square roots always cancel"], "correct": 1, "tag": "", "sol": "Both compositions must give x. g(f(x)) = √(x²) = |x|, which is −x for negative x. Restricting f to x ≥ 0 fixes it."}]}, {"id": "s6", "label": "6 · Graphs, domain & range", "sub": "Reflection in y = x; swapping points; domain and range of f⁻¹; restricted domains", "slides": [{"kind": "mcq", "text": "The point (2, 7) lies on the graph of a one-to-one function f. Which point must lie on the graph of f⁻¹?", "opts": ["(7, 2)", "(2, 1/7)", "(−7, −2)", "(−2, −7)"], "correct": 0, "tag": "", "sol": "f(2) = 7 means f⁻¹(7) = 2, so (7, 2) is on f⁻¹: swap the coordinates (reflect in y = x)."}, {"kind": "blank", "p": "The line f(x) = 3x − 1 passes through (−1, −4), (0, −1) and (2, 5).", "tag": "", "marks": "", "flat": [{"t": "(2, 5) on f becomes __B1__ on f⁻¹", "a": {"B1": "(5, 2)"}, "expr": "coord"}, {"t": "(−1, −4) on f becomes __B1__ on f⁻¹", "a": {"B1": "(-4, -1)"}, "expr": "coord"}, {"t": "f⁻¹(x) = __B1__", "a": {"B1": "(x+1)/3"}, "expr": true}, {"t": "The graphs of f and f⁻¹ are mirror images in the line __B1__", "a": {"B1": "y = x"}, "expr": "words", "accept": ["y=x", "the line y = x", "x = y", "line y = x"]}], "sol": "Swap: (5, 2).\nSwap: (−4, −1).\nx = 3y − 1 gives y = (x + 1)/3. Check: (5 + 1)/3 = 2 ✔.\nSwapping coordinates reflects in y = x."}, {"kind": "mcq", "text": "The graph shows f(x) = x² for 0 ≤ x ≤ 2 and three other curves A, B and C. Which curve is the graph of f⁻¹?", "opts": ["Curve C", "None of them: f has no inverse", "Curve A", "Curve B"], "correct": 3, "tag": "", "sol": "f⁻¹ is the reflection of f in y = x: (2, 4) becomes (4, 2), giving √x, curve B. A is the reflection in the x-axis and C the reflection in the y-axis. On 0 ≤ x ≤ 2, f is one-to-one, so it has an inverse.", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 252 284\" role=\"img\" aria-label=\"Graph of f(x) = x squared for x from 0 to 2, and three other curves labelled A, B and C\"><line class=\"tk\" x1=\"23.7\" y1=\"264.0\" x2=\"23.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"52.1\" y1=\"264.0\" x2=\"52.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"80.5\" y1=\"264.0\" x2=\"80.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"108.9\" y1=\"264.0\" x2=\"108.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"137.3\" y1=\"264.0\" x2=\"137.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"165.7\" y1=\"264.0\" x2=\"165.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"194.1\" y1=\"264.0\" x2=\"194.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"222.5\" y1=\"264.0\" x2=\"222.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"258.3\" x2=\"239.6\" y2=\"258.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"229.9\" x2=\"239.6\" y2=\"229.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"201.5\" x2=\"239.6\" y2=\"201.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"173.1\" x2=\"239.6\" y2=\"173.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"144.7\" x2=\"239.6\" y2=\"144.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"116.3\" x2=\"239.6\" y2=\"116.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"87.9\" x2=\"239.6\" y2=\"87.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"59.5\" x2=\"239.6\" y2=\"59.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"31.0\" x2=\"239.6\" y2=\"31.0\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"144.7\" x2=\"239.6\" y2=\"144.7\"/><line class=\"ln\" x1=\"108.9\" y1=\"264.0\" x2=\"108.9\" y2=\"14.0\"/><text class=\"lb\" x=\"237.6\" y=\"139.7\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"114.9\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"52.1\" y=\"157.7\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"165.7\" y=\"157.7\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"222.5\" y=\"157.7\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"104.9\" y=\"262.3\" text-anchor=\"end\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"104.9\" y=\"205.5\" text-anchor=\"end\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"104.9\" y=\"91.9\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"104.9\" y=\"35.0\" text-anchor=\"end\" style=\"font-size:10px\">4</text><line class=\"ln hid\" x1=\"18.0\" y1=\"235.6\" x2=\"239.6\" y2=\"14.0\"/><text class=\"lb\" x=\"219.6\" y=\"26.0\" text-anchor=\"end\" style=\"font-size:11px\">y = x</text><polyline class=\"arm\" points=\"109.1,144.7 109.7,144.7 110.3,144.6 110.9,144.5 111.6,144.4 112.2,144.3 112.8,144.2 113.4,144.0 114.0,143.8 114.6,143.5 115.3,143.3 115.9,143.0 116.5,142.7 117.1,142.3 117.7,142.0 118.3,141.6 118.9,141.1 119.6,140.7 120.2,140.2 120.8,139.7 121.4,139.2 122.0,138.6 122.6,138.0 123.3,137.4 123.9,136.8 124.5,136.1 125.1,135.5 125.7,134.7 126.3,134.0 126.9,133.2 127.6,132.4 128.2,131.6 128.8,130.8 129.4,129.9 130.0,129.0 130.6,128.1 131.3,127.1 131.9,126.1 132.5,125.1 133.1,124.1 133.7,123.0 134.3,121.9 135.0,120.8 135.6,119.7 136.2,118.5 136.8,117.3 137.4,116.1 138.0,114.8 138.6,113.6 139.3,112.3 139.9,110.9 140.5,109.6 141.1,108.2 141.7,106.8 142.3,105.3 143.0,103.9 143.6,102.4 144.2,100.9 144.8,99.3 145.4,97.8 146.0,96.2 146.6,94.6 147.3,92.9 147.9,91.2 148.5,89.5 149.1,87.8 149.7,86.0 150.3,84.3 151.0,82.5 151.6,80.6 152.2,78.8 152.8,76.9 153.4,75.0 154.0,73.0 154.6,71.0 155.3,69.0 155.9,67.0 156.5,65.0 157.1,62.9 157.7,60.8 158.3,58.7 159.0,56.5 159.6,54.3 160.2,52.1 160.8,49.9 161.4,47.6 162.0,45.3 162.6,43.0 163.3,40.7 163.9,38.3 164.5,35.9 165.1,33.5 165.7,31.0 166.3,28.6 167.0,26.1 167.6,23.5 168.2,21.0\"/><text class=\"al\" x=\"154.4\" y=\"50.9\" text-anchor=\"end\" style=\"font-size:12px\">f</text><polyline class=\"ln\" points=\"109.1,144.7 109.7,144.7 110.3,144.8 110.9,144.8 111.6,144.9 112.2,145.1 112.8,145.2 113.4,145.4 114.0,145.6 114.6,145.8 115.3,146.1 115.9,146.4 116.5,146.7 117.1,147.0 117.7,147.4 118.3,147.8 118.9,148.2 119.6,148.7 120.2,149.2 120.8,149.7 121.4,150.2 122.0,150.7 122.6,151.3 123.3,151.9 123.9,152.6 124.5,153.2 125.1,153.9 125.7,154.6 126.3,155.4 126.9,156.1 127.6,156.9 128.2,157.8 128.8,158.6 129.4,159.5 130.0,160.4 130.6,161.3 131.3,162.3 131.9,163.2 132.5,164.3 133.1,165.3 133.7,166.3 134.3,167.4 135.0,168.6 135.6,169.7 136.2,170.9 136.8,172.1 137.4,173.3 138.0,174.5 138.6,175.8 139.3,177.1 139.9,178.4 140.5,179.8 141.1,181.2 141.7,182.6 142.3,184.0 143.0,185.5 143.6,187.0 144.2,188.5 144.8,190.0 145.4,191.6 146.0,193.2 146.6,194.8 147.3,196.5 147.9,198.1 148.5,199.8 149.1,201.6 149.7,203.3 150.3,205.1 151.0,206.9 151.6,208.7 152.2,210.6 152.8,212.5 153.4,214.4 154.0,216.4 154.6,218.3 155.3,220.3 155.9,222.3 156.5,224.4 157.1,226.5 157.7,228.6 158.3,230.7 159.0,232.8 159.6,235.0 160.2,237.2 160.8,239.5 161.4,241.7 162.0,244.0 162.6,246.3 163.3,248.7 163.9,251.1 164.5,253.4 165.1,255.9 165.7,258.3 166.3,260.8 167.0,263.3\"/><polyline class=\"ln\" points=\"109.1,142.4 109.7,139.9 110.3,138.3 110.9,137.1 111.6,136.0 112.2,135.0 112.8,134.2 113.4,133.4 114.0,132.6 114.6,131.9 115.3,131.3 115.9,130.6 116.5,130.0 117.1,129.4 117.7,128.9 118.3,128.3 118.9,127.8 119.6,127.3 120.2,126.8 120.8,126.3 121.4,125.8 122.0,125.4 122.6,124.9 123.3,124.5 123.9,124.1 124.5,123.6 125.1,123.2 125.7,122.8 126.3,122.4 126.9,122.0 127.6,121.7 128.2,121.3 128.8,120.9 129.4,120.5 130.0,120.2 130.6,119.8 131.3,119.5 131.9,119.1 132.5,118.8 133.1,118.5 133.7,118.1 134.3,117.8 135.0,117.5 135.6,117.2 136.2,116.8 136.8,116.5 137.4,116.2 138.0,115.9 138.6,115.6 139.3,115.3 139.9,115.0 140.5,114.7 141.1,114.4 141.7,114.2 142.3,113.9 143.0,113.6 143.6,113.3 144.2,113.0 144.8,112.8 145.4,112.5 146.0,112.2 146.6,111.9 147.3,111.7 147.9,111.4 148.5,111.1 149.1,110.9 149.7,110.6 150.3,110.4 151.0,110.1 151.6,109.9 152.2,109.6 152.8,109.4 153.4,109.1 154.0,108.9 154.6,108.6 155.3,108.4 155.9,108.2 156.5,107.9 157.1,107.7 157.7,107.4 158.3,107.2 159.0,107.0 159.6,106.7 160.2,106.5 160.8,106.3 161.4,106.1 162.0,105.8 162.6,105.6 163.3,105.4 163.9,105.2 164.5,104.9 165.1,104.7 165.7,104.5 166.3,104.3 167.0,104.1 167.6,103.9 168.2,103.6 168.8,103.4 169.4,103.2 170.0,103.0 170.7,102.8 171.3,102.6 171.9,102.4 172.5,102.2 173.1,102.0 173.7,101.8 174.3,101.6 175.0,101.4 175.6,101.2 176.2,101.0 176.8,100.8 177.4,100.6 178.0,100.4 178.7,100.2 179.3,100.0 179.9,99.8 180.5,99.6 181.1,99.4 181.7,99.2 182.3,99.0 183.0,98.8 183.6,98.6 184.2,98.4 184.8,98.2 185.4,98.1 186.0,97.9 186.7,97.7 187.3,97.5 187.9,97.3 188.5,97.1 189.1,96.9 189.7,96.8 190.3,96.6 191.0,96.4 191.6,96.2 192.2,96.0 192.8,95.9 193.4,95.7 194.0,95.5 194.7,95.3 195.3,95.1 195.9,95.0 196.5,94.8 197.1,94.6 197.7,94.4 198.4,94.3 199.0,94.1 199.6,93.9 200.2,93.8 200.8,93.6 201.4,93.4 202.0,93.2 202.7,93.1 203.3,92.9 203.9,92.7 204.5,92.6 205.1,92.4 205.7,92.2 206.4,92.1 207.0,91.9 207.6,91.7 208.2,91.6 208.8,91.4 209.4,91.2 210.0,91.1 210.7,90.9 211.3,90.8 211.9,90.6 212.5,90.4 213.1,90.3 213.7,90.1 214.4,89.9 215.0,89.8 215.6,89.6 216.2,89.5 216.8,89.3 217.4,89.2 218.0,89.0 218.7,88.8 219.3,88.7 219.9,88.5 220.5,88.4 221.1,88.2 221.7,88.1 222.4,87.9 223.0,87.8 223.6,87.6 224.2,87.5 224.8,87.3 225.4,87.1 226.0,87.0 226.7,86.8 227.3,86.7 227.9,86.5 228.5,86.4 229.1,86.2 229.7,86.1 230.4,85.9 231.0,85.8 231.6,85.6 232.2,85.5 232.8,85.4 233.4,85.2\"/><polyline class=\"ln\" points=\"51.2,27.6 51.9,30.1 52.5,32.6 53.1,35.0 53.7,37.4 54.3,39.8 54.9,42.1 55.5,44.5 56.2,46.7 56.8,49.0 57.4,51.3 58.0,53.5 58.6,55.7 59.2,57.8 59.9,60.0 60.5,62.1 61.1,64.2 61.7,66.2 62.3,68.3 62.9,70.3 63.5,72.3 64.2,74.2 64.8,76.1 65.4,78.0 66.0,79.9 66.6,81.8 67.2,83.6 67.9,85.4 68.5,87.1 69.1,88.9 69.7,90.6 70.3,92.3 70.9,93.9 71.6,95.6 72.2,97.2 72.8,98.7 73.4,100.3 74.0,101.8 74.6,103.3 75.2,104.8 75.9,106.2 76.5,107.7 77.1,109.0 77.7,110.4 78.3,111.7 78.9,113.1 79.6,114.3 80.2,115.6 80.8,116.8 81.4,118.0 82.0,119.2 82.6,120.4 83.2,121.5 83.9,122.6 84.5,123.7 85.1,124.7 85.7,125.7 86.3,126.7 86.9,127.7 87.6,128.6 88.2,129.5 88.8,130.4 89.4,131.3 90.0,132.1 90.6,132.9 91.2,133.7 91.9,134.5 92.5,135.2 93.1,135.9 93.7,136.6 94.3,137.2 94.9,137.8 95.6,138.4 96.2,139.0 96.8,139.5 97.4,140.0 98.0,140.5 98.6,141.0 99.2,141.4 99.9,141.8 100.5,142.2 101.1,142.5 101.7,142.9 102.3,143.2 102.9,143.4 103.6,143.7 104.2,143.9 104.8,144.1 105.4,144.2 106.0,144.4 106.6,144.5 107.3,144.6 107.9,144.6 108.5,144.7\"/><circle class=\"none\" cx=\"162.9\" cy=\"247.2\" r=\"3.2\"/><text class=\"lb\" x=\"169.9\" y=\"251.2\" text-anchor=\"start\" style=\"font-size:11px\">A</text><circle class=\"none\" cx=\"211.2\" cy=\"90.8\" r=\"3.2\"/><text class=\"lb\" x=\"213.2\" y=\"106.8\" text-anchor=\"start\" style=\"font-size:11px\">B</text><circle class=\"none\" cx=\"54.9\" cy=\"42.1\" r=\"3.2\"/><text class=\"lb\" x=\"47.9\" y=\"46.1\" text-anchor=\"end\" style=\"font-size:11px\">C</text></svg></div>"}, {"kind": "blank", "p": "f(x) = √(x − 1) + 3, shown in the graph.", "tag": "", "marks": "", "flat": [{"t": "The range of f is y ≥ __B1__", "a": {"B1": "3"}}, {"t": "So the domain of f⁻¹ is x ≥ __B1__", "a": {"B1": "3"}}, {"t": "f⁻¹(x) = __B1__ (for x ≥ 3)", "a": {"B1": "(x-3)^2+1"}, "expr": true}, {"t": "The range of f⁻¹ is y ≥ __B1__", "a": {"B1": "1"}}], "sol": "√(x − 1) ≥ 0, so f(x) ≥ 3: the graph starts at (1, 3).\nDomain of f⁻¹ = range of f.\nx − 3 = √(y − 1), so y = (x − 3)² + 1.\nRange of f⁻¹ = domain of f: y ≥ 1.", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"Graph of f(x) = square root of (x − 1) plus 3\"><line class=\"tk\" x1=\"24.8\" y1=\"264.0\" x2=\"24.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"58.5\" y1=\"264.0\" x2=\"58.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"92.3\" y1=\"264.0\" x2=\"92.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"126.1\" y1=\"264.0\" x2=\"126.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"159.9\" y1=\"264.0\" x2=\"159.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"193.7\" y1=\"264.0\" x2=\"193.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"227.5\" y1=\"264.0\" x2=\"227.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"261.2\" y1=\"264.0\" x2=\"261.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"257.2\" x2=\"268.0\" y2=\"257.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"223.5\" x2=\"268.0\" y2=\"223.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"189.7\" x2=\"268.0\" y2=\"189.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"155.9\" x2=\"268.0\" y2=\"155.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"122.1\" x2=\"268.0\" y2=\"122.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"88.3\" x2=\"268.0\" y2=\"88.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"54.5\" x2=\"268.0\" y2=\"54.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"20.8\" x2=\"268.0\" y2=\"20.8\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"223.5\" x2=\"268.0\" y2=\"223.5\"/><line class=\"ln\" x1=\"58.5\" y1=\"264.0\" x2=\"58.5\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"218.5\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"64.5\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"126.1\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"193.7\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"261.2\" y=\"236.5\" text-anchor=\"middle\" style=\"font-size:10px\">6</text><text class=\"lb\" x=\"54.5\" y=\"159.9\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"54.5\" y=\"92.3\" text-anchor=\"end\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"54.5\" y=\"24.8\" text-anchor=\"end\" style=\"font-size:10px\">6</text><polyline class=\"arm\" points=\"93.0,117.3 93.7,115.3 94.4,113.8 95.1,112.5 95.8,111.3 96.5,110.3 97.2,109.3 97.9,108.4 98.6,107.6 99.2,106.8 99.9,106.1 100.6,105.3 101.3,104.7 102.0,104.0 102.7,103.4 103.4,102.7 104.1,102.2 104.8,101.6 105.5,101.0 106.2,100.5 106.9,99.9 107.6,99.4 108.3,98.9 109.0,98.4 109.7,97.9 110.4,97.4 111.1,97.0 111.8,96.5 112.4,96.0 113.1,95.6 113.8,95.2 114.5,94.7 115.2,94.3 115.9,93.9 116.6,93.5 117.3,93.1 118.0,92.7 118.7,92.3 119.4,91.9 120.1,91.5 120.8,91.1 121.5,90.7 122.2,90.4 122.9,90.0 123.6,89.6 124.2,89.3 124.9,88.9 125.6,88.6 126.3,88.2 127.0,87.9 127.7,87.5 128.4,87.2 129.1,86.9 129.8,86.5 130.5,86.2 131.2,85.9 131.9,85.5 132.6,85.2 133.3,84.9 134.0,84.6 134.7,84.3 135.4,84.0 136.1,83.7 136.8,83.4 137.4,83.1 138.1,82.8 138.8,82.5 139.5,82.2 140.2,81.9 140.9,81.6 141.6,81.3 142.3,81.0 143.0,80.7 143.7,80.4 144.4,80.2 145.1,79.9 145.8,79.6 146.5,79.3 147.2,79.1 147.9,78.8 148.6,78.5 149.3,78.3 149.9,78.0 150.6,77.7 151.3,77.5 152.0,77.2 152.7,76.9 153.4,76.7 154.1,76.4 154.8,76.2 155.5,75.9 156.2,75.7 156.9,75.4 157.6,75.2 158.3,74.9 159.0,74.7 159.7,74.4 160.4,74.2 161.1,73.9 161.8,73.7 162.4,73.4 163.1,73.2 163.8,73.0 164.5,72.7 165.2,72.5 165.9,72.2 166.6,72.0 167.3,71.8 168.0,71.5 168.7,71.3 169.4,71.1 170.1,70.9 170.8,70.6 171.5,70.4 172.2,70.2 172.9,69.9 173.6,69.7 174.2,69.5 174.9,69.3 175.6,69.1 176.3,68.8 177.0,68.6 177.7,68.4 178.4,68.2 179.1,68.0 179.8,67.7 180.5,67.5 181.2,67.3 181.9,67.1 182.6,66.9 183.3,66.7 184.0,66.5 184.7,66.3 185.4,66.0 186.1,65.8 186.8,65.6 187.4,65.4 188.1,65.2 188.8,65.0 189.5,64.8 190.2,64.6 190.9,64.4 191.6,64.2 192.3,64.0 193.0,63.8 193.7,63.6 194.4,63.4 195.1,63.2 195.8,63.0 196.5,62.8 197.2,62.6 197.9,62.4 198.6,62.2 199.2,62.0 199.9,61.8 200.6,61.6 201.3,61.4 202.0,61.2 202.7,61.0 203.4,60.8 204.1,60.7 204.8,60.5 205.5,60.3 206.2,60.1 206.9,59.9 207.6,59.7 208.3,59.5 209.0,59.3 209.7,59.1 210.4,59.0 211.1,58.8 211.7,58.6 212.4,58.4 213.1,58.2 213.8,58.0 214.5,57.9 215.2,57.7 215.9,57.5 216.6,57.3 217.3,57.1 218.0,56.9 218.7,56.8 219.4,56.6 220.1,56.4 220.8,56.2 221.5,56.1 222.2,55.9 222.9,55.7 223.6,55.5 224.2,55.3 224.9,55.2 225.6,55.0 226.3,54.8 227.0,54.6 227.7,54.5 228.4,54.3 229.1,54.1 229.8,54.0 230.5,53.8 231.2,53.6 231.9,53.4 232.6,53.3 233.3,53.1 234.0,52.9 234.7,52.8 235.4,52.6 236.1,52.4 236.7,52.3 237.4,52.1 238.1,51.9 238.8,51.8 239.5,51.6 240.2,51.4 240.9,51.3 241.6,51.1 242.3,50.9 243.0,50.8 243.7,50.6 244.4,50.4 245.1,50.3 245.8,50.1 246.5,49.9 247.2,49.8 247.9,49.6 248.6,49.5 249.2,49.3 249.9,49.1 250.6,49.0 251.3,48.8 252.0,48.7 252.7,48.5 253.4,48.3 254.1,48.2 254.8,48.0 255.5,47.9 256.2,47.7 256.9,47.5 257.6,47.4 258.3,47.2 259.0,47.1 259.7,46.9 260.4,46.8 261.1,46.6 261.8,46.5 262.4,46.3 263.1,46.1 263.8,46.0 264.5,45.8 265.2,45.7 265.9,45.5 266.6,45.4 267.3,45.2 268.0,45.1\"/><text class=\"al\" x=\"205.4\" y=\"55.7\" text-anchor=\"start\" style=\"font-size:12px\">f</text></svg></div>"}, {"kind": "mcq", "text": "f(x) = (2x + 1)/(x − 3). What is the domain of f⁻¹?", "opts": ["All real x except x = −1/2", "All real x except x = 2", "All real x except x = 3", "All real numbers"], "correct": 1, "tag": "", "sol": "f⁻¹(x) = (3x + 1)/(x − 2), so x ≠ 2. This matches the range of f: f never takes the value 2 (its horizontal asymptote). x ≠ 3 is the domain of f."}, {"kind": "blank", "p": "f(x) = (x + 1)² for x ≥ −1.", "tag": "", "marks": "", "flat": [{"t": "The range of f is y ≥ __B1__", "a": {"B1": "0"}}, {"t": "Swap: x = (y + 1)², and since y ≥ −1, f⁻¹(x) = √x − __B1__", "a": {"B1": "1"}}, {"t": "f⁻¹(9) = __B1__", "a": {"B1": "2"}}, {"t": "We take the __B1__ square root because f⁻¹ must have range y ≥ −1", "a": {"B1": "positive"}, "expr": "words", "accept": ["principal", "non-negative", "nonnegative", "plus"]}], "sol": "(x + 1)² ≥ 0.\ny + 1 = √x (not −√x), so y = √x − 1.\n3 − 1 = 2. Check: f(2) = 9 ✔.\ny + 1 ≥ 0, so y + 1 = +√x."}, {"kind": "mcq", "text": "The graph shows f(x) = 2x − 3, its inverse and the line y = x. At which point do f and f⁻¹ meet?", "opts": ["(0, −3)", "(1.5, 0)", "(−3, 0)", "(3, 3)"], "correct": 3, "tag": "", "sol": "An increasing f meets its inverse on y = x: 2x − 3 = x gives x = 3, so (3, 3). (0, −3) is on f but (−3, 0) is on f⁻¹: these are mirror points, not a meeting point.", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 284\" role=\"img\" aria-label=\"The line f(x) = 2x − 3, its inverse and the mirror line y = x\"><line class=\"tk\" x1=\"23.3\" y1=\"264.0\" x2=\"23.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"49.9\" y1=\"264.0\" x2=\"49.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"76.5\" y1=\"264.0\" x2=\"76.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"103.1\" y1=\"264.0\" x2=\"103.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"129.7\" y1=\"264.0\" x2=\"129.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"156.3\" y1=\"264.0\" x2=\"156.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"182.9\" y1=\"264.0\" x2=\"182.9\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"209.5\" y1=\"264.0\" x2=\"209.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"236.1\" y1=\"264.0\" x2=\"236.1\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"262.7\" y1=\"264.0\" x2=\"262.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"258.7\" x2=\"268.0\" y2=\"258.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"232.1\" x2=\"268.0\" y2=\"232.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"205.5\" x2=\"268.0\" y2=\"205.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"178.9\" x2=\"268.0\" y2=\"178.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"152.3\" x2=\"268.0\" y2=\"152.3\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"125.7\" x2=\"268.0\" y2=\"125.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"99.1\" x2=\"268.0\" y2=\"99.1\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"72.5\" x2=\"268.0\" y2=\"72.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"45.9\" x2=\"268.0\" y2=\"45.9\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"19.3\" x2=\"268.0\" y2=\"19.3\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"152.3\" x2=\"268.0\" y2=\"152.3\"/><line class=\"ln\" x1=\"129.7\" y1=\"264.0\" x2=\"129.7\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"147.3\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"135.7\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"23.3\" y=\"165.3\" text-anchor=\"middle\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"76.5\" y=\"165.3\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"182.9\" y=\"165.3\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"236.1\" y=\"165.3\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"125.7\" y=\"262.7\" text-anchor=\"end\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"125.7\" y=\"209.5\" text-anchor=\"end\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"125.7\" y=\"103.1\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"125.7\" y=\"49.9\" text-anchor=\"end\" style=\"font-size:10px\">4</text><line class=\"ln hid\" x1=\"18.0\" y1=\"264.0\" x2=\"268.0\" y2=\"14.0\"/><text class=\"lb\" x=\"248.0\" y=\"26.0\" text-anchor=\"end\" style=\"font-size:11px\">y = x</text><polyline class=\"arm\" points=\"113.8,263.8 114.5,262.4 115.2,261.0 115.9,259.7 116.6,258.3 117.3,256.9 118.0,255.5 118.7,254.1 119.4,252.7 120.1,251.3 120.8,249.9 121.5,248.5 122.2,247.2 122.9,245.8 123.6,244.4 124.2,243.0 124.9,241.6 125.6,240.2 126.3,238.8 127.0,237.4 127.7,236.0 128.4,234.7 129.1,233.3 129.8,231.9 130.5,230.5 131.2,229.1 131.9,227.7 132.6,226.3 133.3,224.9 134.0,223.5 134.7,222.2 135.4,220.8 136.1,219.4 136.8,218.0 137.4,216.6 138.1,215.2 138.8,213.8 139.5,212.4 140.2,211.0 140.9,209.7 141.6,208.3 142.3,206.9 143.0,205.5 143.7,204.1 144.4,202.7 145.1,201.3 145.8,199.9 146.5,198.5 147.2,197.2 147.9,195.8 148.6,194.4 149.2,193.0 149.9,191.6 150.6,190.2 151.3,188.8 152.0,187.4 152.7,186.0 153.4,184.7 154.1,183.3 154.8,181.9 155.5,180.5 156.2,179.1 156.9,177.7 157.6,176.3 158.3,174.9 159.0,173.5 159.7,172.2 160.4,170.8 161.1,169.4 161.8,168.0 162.4,166.6 163.1,165.2 163.8,163.8 164.5,162.4 165.2,161.0 165.9,159.7 166.6,158.3 167.3,156.9 168.0,155.5 168.7,154.1 169.4,152.7 170.1,151.3 170.8,149.9 171.5,148.5 172.2,147.2 172.9,145.8 173.6,144.4 174.2,143.0 174.9,141.6 175.6,140.2 176.3,138.8 177.0,137.4 177.7,136.0 178.4,134.7 179.1,133.3 179.8,131.9 180.5,130.5 181.2,129.1 181.9,127.7 182.6,126.3 183.3,124.9 184.0,123.5 184.7,122.2 185.4,120.8 186.1,119.4 186.8,118.0 187.4,116.6 188.1,115.2 188.8,113.8 189.5,112.4 190.2,111.0 190.9,109.7 191.6,108.3 192.3,106.9 193.0,105.5 193.7,104.1 194.4,102.7 195.1,101.3 195.8,99.9 196.5,98.5 197.2,97.2 197.9,95.8 198.6,94.4 199.2,93.0 199.9,91.6 200.6,90.2 201.3,88.8 202.0,87.4 202.7,86.0 203.4,84.7 204.1,83.3 204.8,81.9 205.5,80.5 206.2,79.1 206.9,77.7 207.6,76.3 208.3,74.9 209.0,73.5 209.7,72.2 210.4,70.8 211.1,69.4 211.8,68.0 212.4,66.6 213.1,65.2 213.8,63.8 214.5,62.4 215.2,61.0 215.9,59.7 216.6,58.3 217.3,56.9 218.0,55.5 218.7,54.1 219.4,52.7 220.1,51.3 220.8,49.9 221.5,48.5 222.2,47.2 222.9,45.8 223.6,44.4 224.2,43.0 224.9,41.6 225.6,40.2 226.3,38.8 227.0,37.4 227.7,36.0 228.4,34.7 229.1,33.3 229.8,31.9 230.5,30.5 231.2,29.1 231.9,27.7 232.6,26.3 233.3,24.9 234.0,23.5 234.7,22.2 235.4,20.8 236.1,19.4 236.7,18.0 237.4,16.6 238.1,15.2\"/><text class=\"al\" x=\"217.5\" y=\"30.0\" text-anchor=\"end\" style=\"font-size:12px\">f</text><polyline class=\"ln\" points=\"18.0,168.3 18.7,167.9 19.4,167.6 20.1,167.2 20.8,166.9 21.5,166.5 22.2,166.2 22.9,165.8 23.6,165.5 24.2,165.1 24.9,164.8 25.6,164.4 26.3,164.1 27.0,163.7 27.7,163.4 28.4,163.0 29.1,162.7 29.8,162.4 30.5,162.0 31.2,161.7 31.9,161.3 32.6,161.0 33.3,160.6 34.0,160.3 34.7,159.9 35.4,159.6 36.1,159.2 36.8,158.9 37.4,158.5 38.1,158.2 38.8,157.8 39.5,157.5 40.2,157.1 40.9,156.8 41.6,156.4 42.3,156.1 43.0,155.8 43.7,155.4 44.4,155.1 45.1,154.7 45.8,154.4 46.5,154.0 47.2,153.7 47.9,153.3 48.6,153.0 49.2,152.6 49.9,152.3 50.6,151.9 51.3,151.6 52.0,151.2 52.7,150.9 53.4,150.5 54.1,150.2 54.8,149.9 55.5,149.5 56.2,149.2 56.9,148.8 57.6,148.5 58.3,148.1 59.0,147.8 59.7,147.4 60.4,147.1 61.1,146.7 61.8,146.4 62.4,146.0 63.1,145.7 63.8,145.3 64.5,145.0 65.2,144.6 65.9,144.3 66.6,143.9 67.3,143.6 68.0,143.3 68.7,142.9 69.4,142.6 70.1,142.2 70.8,141.9 71.5,141.5 72.2,141.2 72.9,140.8 73.6,140.5 74.2,140.1 74.9,139.8 75.6,139.4 76.3,139.1 77.0,138.7 77.7,138.4 78.4,138.0 79.1,137.7 79.8,137.4 80.5,137.0 81.2,136.7 81.9,136.3 82.6,136.0 83.3,135.6 84.0,135.3 84.7,134.9 85.4,134.6 86.1,134.2 86.8,133.9 87.4,133.5 88.1,133.2 88.8,132.8 89.5,132.5 90.2,132.1 90.9,131.8 91.6,131.4 92.3,131.1 93.0,130.8 93.7,130.4 94.4,130.1 95.1,129.7 95.8,129.4 96.5,129.0 97.2,128.7 97.9,128.3 98.6,128.0 99.2,127.6 99.9,127.3 100.6,126.9 101.3,126.6 102.0,126.2 102.7,125.9 103.4,125.5 104.1,125.2 104.8,124.9 105.5,124.5 106.2,124.2 106.9,123.8 107.6,123.5 108.3,123.1 109.0,122.8 109.7,122.4 110.4,122.1 111.1,121.7 111.7,121.4 112.4,121.0 113.1,120.7 113.8,120.3 114.5,120.0 115.2,119.6 115.9,119.3 116.6,118.9 117.3,118.6 118.0,118.3 118.7,117.9 119.4,117.6 120.1,117.2 120.8,116.9 121.5,116.5 122.2,116.2 122.9,115.8 123.6,115.5 124.2,115.1 124.9,114.8 125.6,114.4 126.3,114.1 127.0,113.7 127.7,113.4 128.4,113.0 129.1,112.7 129.8,112.4 130.5,112.0 131.2,111.7 131.9,111.3 132.6,111.0 133.3,110.6 134.0,110.3 134.7,109.9 135.4,109.6 136.1,109.2 136.8,108.9 137.4,108.5 138.1,108.2 138.8,107.8 139.5,107.5 140.2,107.1 140.9,106.8 141.6,106.4 142.3,106.1 143.0,105.8 143.7,105.4 144.4,105.1 145.1,104.7 145.8,104.4 146.5,104.0 147.2,103.7 147.9,103.3 148.6,103.0 149.2,102.6 149.9,102.3 150.6,101.9 151.3,101.6 152.0,101.2 152.7,100.9 153.4,100.5 154.1,100.2 154.8,99.9 155.5,99.5 156.2,99.2 156.9,98.8 157.6,98.5 158.3,98.1 159.0,97.8 159.7,97.4 160.4,97.1 161.1,96.7 161.8,96.4 162.4,96.0 163.1,95.7 163.8,95.3 164.5,95.0 165.2,94.6 165.9,94.3 166.6,93.9 167.3,93.6 168.0,93.3 168.7,92.9 169.4,92.6 170.1,92.2 170.8,91.9 171.5,91.5 172.2,91.2 172.9,90.8 173.6,90.5 174.2,90.1 174.9,89.8 175.6,89.4 176.3,89.1 177.0,88.7 177.7,88.4 178.4,88.0 179.1,87.7 179.8,87.4 180.5,87.0 181.2,86.7 181.9,86.3 182.6,86.0 183.3,85.6 184.0,85.3 184.7,84.9 185.4,84.6 186.1,84.2 186.8,83.9 187.4,83.5 188.1,83.2 188.8,82.8 189.5,82.5 190.2,82.1 190.9,81.8 191.6,81.4 192.3,81.1 193.0,80.8 193.7,80.4 194.4,80.1 195.1,79.7 195.8,79.4 196.5,79.0 197.2,78.7 197.9,78.3 198.6,78.0 199.2,77.6 199.9,77.3 200.6,76.9 201.3,76.6 202.0,76.2 202.7,75.9 203.4,75.5 204.1,75.2 204.8,74.9 205.5,74.5 206.2,74.2 206.9,73.8 207.6,73.5 208.3,73.1 209.0,72.8 209.7,72.4 210.4,72.1 211.1,71.7 211.8,71.4 212.4,71.0 213.1,70.7 213.8,70.3 214.5,70.0 215.2,69.6 215.9,69.3 216.6,68.9 217.3,68.6 218.0,68.3 218.7,67.9 219.4,67.6 220.1,67.2 220.8,66.9 221.5,66.5 222.2,66.2 222.9,65.8 223.6,65.5 224.2,65.1 224.9,64.8 225.6,64.4 226.3,64.1 227.0,63.7 227.7,63.4 228.4,63.0 229.1,62.7 229.8,62.4 230.5,62.0 231.2,61.7 231.9,61.3 232.6,61.0 233.3,60.6 234.0,60.3 234.7,59.9 235.4,59.6 236.1,59.2 236.7,58.9 237.4,58.5 238.1,58.2 238.8,57.8 239.5,57.5 240.2,57.1 240.9,56.8 241.6,56.4 242.3,56.1 243.0,55.8 243.7,55.4 244.4,55.1 245.1,54.7 245.8,54.4 246.5,54.0 247.2,53.7 247.9,53.3 248.6,53.0 249.2,52.6 249.9,52.3 250.6,51.9 251.3,51.6 252.0,51.2 252.7,50.9 253.4,50.5 254.1,50.2 254.8,49.9 255.5,49.5 256.2,49.2 256.9,48.8 257.6,48.5 258.3,48.1 259.0,47.8 259.7,47.4 260.4,47.1 261.1,46.7 261.8,46.4 262.4,46.0 263.1,45.7 263.8,45.3 264.5,45.0 265.2,44.6 265.9,44.3 266.6,43.9 267.3,43.6 268.0,43.3\"/><text class=\"lb\" x=\"26.0\" y=\"131.0\" text-anchor=\"start\" style=\"font-size:12px\">f⁻¹</text></svg></div>"}, {"kind": "blank", "p": "f(x) = √(4 − x) for x ≤ 4.", "tag": "", "marks": "", "flat": [{"t": "Swap and square: f⁻¹(x) = __B1__", "a": {"B1": "4-x^2"}, "expr": true}, {"t": "Domain of f⁻¹: x ≥ __B1__", "a": {"B1": "0"}}, {"t": "Range of f⁻¹: y ≤ __B1__", "a": {"B1": "4"}}, {"t": "(3, 1) is on f, so __B1__ is on f⁻¹", "a": {"B1": "(1, 3)"}, "expr": "coord"}], "sol": "x = √(4 − y), so x² = 4 − y and y = 4 − x².\nThe range of f is y ≥ 0.\nThe domain of f is x ≤ 4.\nSwap: (1, 3). Check: 4 − 1² = 3 ✔."}, {"kind": "mcq", "text": "f(x) = x³ + 1 has y-intercept (0, 1). Which point is the x-intercept of f⁻¹?", "opts": ["(0, 1)", "(0, −1)", "(−1, 0)", "(1, 0)"], "correct": 3, "tag": "", "sol": "(0, 1) on f becomes (1, 0) on f⁻¹, which lies on the x-axis. Check: f⁻¹(x) = ∛(x − 1), and ∛0 = 0."}, {"kind": "blank", "p": "The graph shows the line f.", "tag": "", "marks": "", "flat": [{"t": "Read f⁻¹(2) = __B1__ and f⁻¹(0) = __B2__", "a": {"B1": "2", "B2": "-2"}}, {"t": "f(x) = x/2 + 1, so f⁻¹(x) = __B1__", "a": {"B1": "2x-2"}, "expr": true}, {"t": "The slope of f⁻¹ is __B1__", "a": {"B1": "2"}}], "sol": "f(2) = 2 and f(−2) = 0: read across from the y-value to the x-value.\nx = y/2 + 1, so y = 2(x − 1) = 2x − 2.\n2 = 1/(1/2): the reciprocal of the slope of f.", "fig": "<div style=\"width:100%;max-width:320px;margin:0 auto\"><svg class=\"figsvg\" viewBox=\"0 0 280 224\" role=\"img\" aria-label=\"Graph of a straight line f through the grid points (−2, 0), (0, 1), (2, 2) and (4, 3)\"><line class=\"tk\" x1=\"24.0\" y1=\"204.5\" x2=\"24.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"53.7\" y1=\"204.5\" x2=\"53.7\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"83.5\" y1=\"204.5\" x2=\"83.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"113.2\" y1=\"204.5\" x2=\"113.2\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"143.0\" y1=\"204.5\" x2=\"143.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"172.8\" y1=\"204.5\" x2=\"172.8\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"202.5\" y1=\"204.5\" x2=\"202.5\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"232.3\" y1=\"204.5\" x2=\"232.3\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"262.0\" y1=\"204.5\" x2=\"262.0\" y2=\"14.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"198.5\" x2=\"268.0\" y2=\"198.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"168.8\" x2=\"268.0\" y2=\"168.8\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"109.2\" x2=\"268.0\" y2=\"109.2\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"79.5\" x2=\"268.0\" y2=\"79.5\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"49.7\" x2=\"268.0\" y2=\"49.7\" stroke-opacity=\".35\"/><line class=\"tk\" x1=\"18.0\" y1=\"20.0\" x2=\"268.0\" y2=\"20.0\" stroke-opacity=\".35\"/><line class=\"ln\" x1=\"18.0\" y1=\"139.0\" x2=\"268.0\" y2=\"139.0\"/><line class=\"ln\" x1=\"143.0\" y1=\"204.5\" x2=\"143.0\" y2=\"14.0\"/><text class=\"lb\" x=\"266.0\" y=\"134.0\" text-anchor=\"end\">x</text><text class=\"lb\" x=\"149.0\" y=\"25.0\" text-anchor=\"start\">y</text><text class=\"lb\" x=\"24.0\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">−4</text><text class=\"lb\" x=\"83.5\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"202.5\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"262.0\" y=\"152.0\" text-anchor=\"middle\" style=\"font-size:10px\">4</text><text class=\"lb\" x=\"139.0\" y=\"202.5\" text-anchor=\"end\" style=\"font-size:10px\">−2</text><text class=\"lb\" x=\"139.0\" y=\"83.5\" text-anchor=\"end\" style=\"font-size:10px\">2</text><text class=\"lb\" x=\"139.0\" y=\"24.0\" text-anchor=\"end\" style=\"font-size:10px\">4</text><polyline class=\"arm\" points=\"18.0,171.7 18.7,171.4 19.4,171.0 20.1,170.7 20.8,170.3 21.5,170.0 22.2,169.7 22.9,169.3 23.6,169.0 24.2,168.6 24.9,168.3 25.6,167.9 26.3,167.6 27.0,167.2 27.7,166.9 28.4,166.5 29.1,166.2 29.8,165.8 30.5,165.5 31.2,165.1 31.9,164.8 32.6,164.4 33.3,164.1 34.0,163.8 34.7,163.4 35.4,163.1 36.1,162.7 36.8,162.4 37.4,162.0 38.1,161.7 38.8,161.3 39.5,161.0 40.2,160.6 40.9,160.3 41.6,159.9 42.3,159.6 43.0,159.2 43.7,158.9 44.4,158.5 45.1,158.2 45.8,157.8 46.5,157.5 47.2,157.2 47.9,156.8 48.6,156.5 49.2,156.1 49.9,155.8 50.6,155.4 51.3,155.1 52.0,154.7 52.7,154.4 53.4,154.0 54.1,153.7 54.8,153.3 55.5,153.0 56.2,152.6 56.9,152.3 57.6,151.9 58.3,151.6 59.0,151.3 59.7,150.9 60.4,150.6 61.1,150.2 61.8,149.9 62.4,149.5 63.1,149.2 63.8,148.8 64.5,148.5 65.2,148.1 65.9,147.8 66.6,147.4 67.3,147.1 68.0,146.7 68.7,146.4 69.4,146.0 70.1,145.7 70.8,145.3 71.5,145.0 72.2,144.7 72.9,144.3 73.6,144.0 74.2,143.6 74.9,143.3 75.6,142.9 76.3,142.6 77.0,142.2 77.7,141.9 78.4,141.5 79.1,141.2 79.8,140.8 80.5,140.5 81.2,140.1 81.9,139.8 82.6,139.4 83.3,139.1 84.0,138.8 84.7,138.4 85.4,138.1 86.1,137.7 86.8,137.4 87.4,137.0 88.1,136.7 88.8,136.3 89.5,136.0 90.2,135.6 90.9,135.3 91.6,134.9 92.3,134.6 93.0,134.2 93.7,133.9 94.4,133.5 95.1,133.2 95.8,132.8 96.5,132.5 97.2,132.2 97.9,131.8 98.6,131.5 99.2,131.1 99.9,130.8 100.6,130.4 101.3,130.1 102.0,129.7 102.7,129.4 103.4,129.0 104.1,128.7 104.8,128.3 105.5,128.0 106.2,127.6 106.9,127.3 107.6,126.9 108.3,126.6 109.0,126.3 109.7,125.9 110.4,125.6 111.1,125.2 111.7,124.9 112.4,124.5 113.1,124.2 113.8,123.8 114.5,123.5 115.2,123.1 115.9,122.8 116.6,122.4 117.3,122.1 118.0,121.7 118.7,121.4 119.4,121.0 120.1,120.7 120.8,120.3 121.5,120.0 122.2,119.7 122.9,119.3 123.6,119.0 124.2,118.6 124.9,118.3 125.6,117.9 126.3,117.6 127.0,117.2 127.7,116.9 128.4,116.5 129.1,116.2 129.8,115.8 130.5,115.5 131.2,115.1 131.9,114.8 132.6,114.4 133.3,114.1 134.0,113.8 134.7,113.4 135.4,113.1 136.1,112.7 136.8,112.4 137.4,112.0 138.1,111.7 138.8,111.3 139.5,111.0 140.2,110.6 140.9,110.3 141.6,109.9 142.3,109.6 143.0,109.2 143.7,108.9 144.4,108.5 145.1,108.2 145.8,107.8 146.5,107.5 147.2,107.2 147.9,106.8 148.6,106.5 149.2,106.1 149.9,105.8 150.6,105.4 151.3,105.1 152.0,104.7 152.7,104.4 153.4,104.0 154.1,103.7 154.8,103.3 155.5,103.0 156.2,102.6 156.9,102.3 157.6,101.9 158.3,101.6 159.0,101.3 159.7,100.9 160.4,100.6 161.1,100.2 161.8,99.9 162.4,99.5 163.1,99.2 163.8,98.8 164.5,98.5 165.2,98.1 165.9,97.8 166.6,97.4 167.3,97.1 168.0,96.7 168.7,96.4 169.4,96.0 170.1,95.7 170.8,95.3 171.5,95.0 172.2,94.7 172.9,94.3 173.6,94.0 174.2,93.6 174.9,93.3 175.6,92.9 176.3,92.6 177.0,92.2 177.7,91.9 178.4,91.5 179.1,91.2 179.8,90.8 180.5,90.5 181.2,90.1 181.9,89.8 182.6,89.4 183.3,89.1 184.0,88.8 184.7,88.4 185.4,88.1 186.1,87.7 186.7,87.4 187.4,87.0 188.1,86.7 188.8,86.3 189.5,86.0 190.2,85.6 190.9,85.3 191.6,84.9 192.3,84.6 193.0,84.2 193.7,83.9 194.4,83.5 195.1,83.2 195.8,82.8 196.5,82.5 197.2,82.2 197.9,81.8 198.6,81.5 199.2,81.1 199.9,80.8 200.6,80.4 201.3,80.1 202.0,79.7 202.7,79.4 203.4,79.0 204.1,78.7 204.8,78.3 205.5,78.0 206.2,77.6 206.9,77.3 207.6,76.9 208.3,76.6 209.0,76.3 209.7,75.9 210.4,75.6 211.1,75.2 211.7,74.9 212.4,74.5 213.1,74.2 213.8,73.8 214.5,73.5 215.2,73.1 215.9,72.8 216.6,72.4 217.3,72.1 218.0,71.7 218.7,71.4 219.4,71.0 220.1,70.7 220.8,70.3 221.5,70.0 222.2,69.7 222.9,69.3 223.6,69.0 224.2,68.6 224.9,68.3 225.6,67.9 226.3,67.6 227.0,67.2 227.7,66.9 228.4,66.5 229.1,66.2 229.8,65.8 230.5,65.5 231.2,65.1 231.9,64.8 232.6,64.4 233.3,64.1 234.0,63.8 234.7,63.4 235.4,63.1 236.1,62.7 236.7,62.4 237.4,62.0 238.1,61.7 238.8,61.3 239.5,61.0 240.2,60.6 240.9,60.3 241.6,59.9 242.3,59.6 243.0,59.2 243.7,58.9 244.4,58.5 245.1,58.2 245.8,57.8 246.5,57.5 247.2,57.2 247.9,56.8 248.6,56.5 249.2,56.1 249.9,55.8 250.6,55.4 251.3,55.1 252.0,54.7 252.7,54.4 253.4,54.0 254.1,53.7 254.8,53.3 255.5,53.0 256.2,52.6 256.9,52.3 257.6,51.9 258.3,51.6 259.0,51.3 259.7,50.9 260.4,50.6 261.1,50.2 261.8,49.9 262.4,49.5 263.1,49.2 263.8,48.8 264.5,48.5 265.2,48.1 265.9,47.8 266.6,47.4 267.3,47.1 268.0,46.7\"/><text class=\"al\" x=\"225.4\" y=\"64.5\" text-anchor=\"start\" style=\"font-size:12px\">f</text><circle class=\"pt\" cx=\"83.5\" cy=\"139.0\" r=\"3.2\"/><circle class=\"pt\" cx=\"143.0\" cy=\"109.2\" r=\"3.2\"/><circle class=\"pt\" cx=\"202.5\" cy=\"79.5\" r=\"3.2\"/><circle class=\"pt\" cx=\"262.0\" cy=\"49.7\" r=\"3.2\"/></svg></div>"}]}, {"id": "s7", "label": "Assessment A", "sub": "Knowing and understanding", "slides": [{"kind": "mcq", "text": "Two one-to-one functions f and g are inverses exactly when:", "opts": ["f(g(x)) = g(f(x))", "f(g(x)) = x and g(f(x)) = x", "f(x) · g(x) = 1", "f(x) + g(x) = x"], "correct": 1, "tag": "", "sol": "Inverses undo each other in both orders. f(x)·g(x) = 1 describes reciprocals. f(g(x)) = g(f(x)) holds for many pairs that are not inverses, e.g. f = g = 2x."}, {"kind": "blank", "p": "f(x) = 9x − 4.", "tag": "", "marks": "", "flat": [{"t": "f⁻¹(x) = __B1__", "a": {"B1": "(x+4)/9"}, "expr": true}, {"t": "f⁻¹(5) = __B1__", "a": {"B1": "1"}}, {"t": "1/f(5) = __B1__", "a": {"B1": "1/41"}}], "sol": "x = 9y − 4, so y = (x + 4)/9.\n9/9 = 1.\nf(5) = 41, so 1/f(5) = 1/41, not the same as f⁻¹(5)."}, {"kind": "mcq", "text": "What is the inverse of g(x) = ∛x − 5?", "opts": ["g⁻¹(x) = x³ + 5", "g⁻¹(x) = (x − 5)³", "g⁻¹(x) = 1/(∛x − 5)", "g⁻¹(x) = (x + 5)³"], "correct": 3, "tag": "", "sol": "g takes the cube root, then subtracts 5. Undo in reverse: add 5, then cube. Check: g(8) = −3 and (−3 + 5)³ = 8."}, {"kind": "blank", "p": "Complete the facts about the procedure.", "tag": "", "marks": "", "flat": [{"t": "Step 2: __B1__ x and y", "a": {"B1": "swap"}, "expr": "words", "accept": ["interchange", "switch", "exchange", "swap them"]}, {"t": "Step 5: verify by __B1__", "a": {"B1": "composition"}, "expr": "words", "accept": ["composing", "compositions", "composition of functions", "composing the functions"]}, {"t": "f(x) = x² is not __B1__, so it has no inverse unless the domain is restricted", "a": {"B1": "one-to-one"}, "expr": "words", "accept": ["one to one", "injective", "1-1", "1 to 1"]}], "sol": "After writing y = f(x), swap x and y.\nCheck that f(f⁻¹(x)) = x (one composition is usually enough).\nf(−1) = f(1), so x² fails the horizontal line test."}, {"kind": "mcq", "text": "What is the inverse of f(x) = (x − 1)/(x + 2)?", "opts": ["f⁻¹(x) = (2x + 1)/(1 − x)", "f⁻¹(x) = (2x + 1)/(x − 1)", "f⁻¹(x) = (x + 2)/(x − 1)", "f⁻¹(x) = (2x − 1)/(1 − x)"], "correct": 0, "tag": "", "sol": "Swap: x(y + 2) = y − 1, so xy − y = −1 − 2x, y(x − 1) = −(2x + 1), and y = (2x + 1)/(1 − x). (x + 2)/(x − 1) is 1/f."}, {"kind": "blank", "p": "f is given by the table.\nx: 1, 2, 3, 4, 5\nf(x): 4, 6, −1, 0, 2", "tag": "", "marks": "", "flat": [{"t": "f⁻¹(0) = __B1__ and f⁻¹(6) = __B2__", "a": {"B1": "4", "B2": "2"}}, {"t": "f(f⁻¹(−1)) = __B1__", "a": {"B1": "-1"}}, {"t": "f⁻¹(f(5)) = __B1__", "a": {"B1": "5"}}], "sol": "f(4) = 0 and f(2) = 6.\nf⁻¹(−1) = 3 and f(3) = −1.\nf(5) = 2 and f⁻¹(2) = 5."}, {"kind": "mcq", "text": "f(x) = √x + 3. What is the domain of f⁻¹?", "opts": ["All real x", "x ≥ 3", "x ≥ −3", "x ≥ 0"], "correct": 1, "tag": "", "sol": "The domain of f⁻¹ is the range of f. √x ≥ 0, so f(x) ≥ 3. Indeed f⁻¹(x) = (x − 3)², for x ≥ 3."}, {"kind": "blank", "p": "h(x) = 2x⁵ + 1.", "tag": "", "marks": "", "flat": [{"t": "h⁻¹(x) = ⁵√( __B1__ )", "a": {"B1": "(x-1)/2"}, "expr": true}, {"t": "h⁻¹(−63) = __B1__", "a": {"B1": "-2"}}, {"t": "h⁻¹(1) = __B1__", "a": {"B1": "0"}}], "sol": "x = 2y⁵ + 1, so y⁵ = (x − 1)/2.\n⁵√(−64/2) = ⁵√(−32) = −2. Check: h(−2) = −64 + 1 = −63 ✔.\n⁵√0 = 0."}]}, {"id": "s8", "label": "Assessment B", "sub": "Investigating patterns", "slides": [{"kind": "blank", "p": "Investigate the slopes of linear functions and their inverses.", "tag": "", "marks": "", "flat": [{"t": "f(x) = 4x + 1: the slope of f⁻¹ is __B1__", "a": {"B1": "1/4"}}, {"t": "g(x) = 7 − 2x: g⁻¹(x) = __B1__", "a": {"B1": "(7-x)/2"}, "expr": true}, {"t": "The slope of g⁻¹ is __B1__", "a": {"B1": "-1/2"}}, {"t": "In general, if f has slope m, then f⁻¹ has slope __B1__", "a": {"B1": "1/m"}, "expr": true}], "sol": "f⁻¹(x) = (x − 1)/4: slope 1/4.\nx = 7 − 2y gives y = (7 − x)/2.\n(7 − x)/2 = −x/2 + 7/2: slope −1/2 = 1/(−2).\nf⁻¹(x) = (x − b)/m: slope 1/m. Reflecting in y = x swaps rise and run."}, {"kind": "mcq", "text": "For which values of b is f(x) = b − x its own inverse?", "opts": ["Every value of b", "Only b = 0", "No value of b", "Only b = 1"], "correct": 0, "tag": "", "sol": "f(f(x)) = b − (b − x) = x for every b. Each such line has slope −1, so it is perpendicular to y = x and symmetric about it."}, {"kind": "blank", "p": "Investigate f(x) = (3x + 1)/(2x − 3).", "tag": "", "marks": "", "flat": [{"t": "f(1) = __B1__", "a": {"B1": "-4"}}, {"t": "f(−4) = __B1__", "a": {"B1": "1"}}, {"t": "Swap and solve: f⁻¹(x) = __B1__", "a": {"B1": "(3x+1)/(2x-3)"}, "expr": true}, {"t": "So f is its own __B1__", "a": {"B1": "inverse"}, "expr": "words", "accept": ["inverses", "inverse function"]}], "sol": "4/(−1) = −4.\n(−11)/(−11) = 1: f sends 1 to −4 and −4 back to 1.\nx(2y − 3) = 3y + 1 gives y(2x − 3) = 3x + 1.\nf⁻¹ = f. This happens whenever the coefficient of x on top is minus the constant on the bottom."}, {"kind": "mcq", "text": "Look at the pattern: x³ + 6 → ∛(x − 6), 2x⁷ − 9 → ⁷√((x + 9)/2). For n odd and any k, what is the inverse of f(x) = xⁿ + k?", "opts": ["(x − k)ⁿ", "ⁿ√x − k", "ⁿ√(x − k)", "ⁿ√(x + k)"], "correct": 2, "tag": "", "sol": "Swap: x = yⁿ + k, so yⁿ = x − k and y = ⁿ√(x − k). Subtract k first, then take the root."}, {"kind": "blank", "p": "f(x) = 2x and g(x) = x + 3. Investigate the inverse of the composition f∘g.", "tag": "", "marks": "", "flat": [{"t": "(f∘g)(x) = f(g(x)) = __B1__", "a": {"B1": "2x+6"}, "expr": true}, {"t": "(f∘g)⁻¹(x) = __B1__", "a": {"B1": "(x-6)/2"}, "expr": true}, {"t": "f⁻¹(x) = __B1__, and g⁻¹(f⁻¹(x)) = x/2 − 3", "a": {"B1": "x/2"}, "expr": true}, {"t": "(f∘g)⁻¹ = g⁻¹∘f⁻¹: the inverses are applied in the __B1__ order", "a": {"B1": "reverse"}, "expr": "words", "accept": ["opposite", "backwards", "backward", "reverse order"]}], "sol": "2(x + 3) = 2x + 6.\nx = 2y + 6 gives y = (x − 6)/2.\nf⁻¹(x) = x/2; then g⁻¹ subtracts 3: x/2 − 3 = (x − 6)/2, the same.\nLike taking off socks and shoes: the last thing done is undone first."}, {"kind": "mcq", "text": "Where do the graphs of f(x) = x³ and f⁻¹(x) = ∛x meet?", "opts": ["Only at (0, 0)", "At (−1, −1), (0, 0) and (1, 1)", "Only at (0, 0) and (1, 1)", "They never meet"], "correct": 1, "tag": "", "sol": "f is increasing, so it meets f⁻¹ on y = x: x³ = x gives x(x − 1)(x + 1) = 0, so x = −1, 0, 1."}, {"kind": "blank", "p": "Inverses of restricted quadratics.", "tag": "", "marks": "", "flat": [{"t": "f(x) = x² + 5, x ≥ 0: f⁻¹(x) = √(x − __B1__)", "a": {"B1": "5"}}, {"t": "f⁻¹(21) = __B1__", "a": {"B1": "4"}}, {"t": "f(x) = (x − h)² with x ≥ h: f⁻¹(x) = √x + __B1__", "a": {"B1": "h"}, "expr": true}], "sol": "x = y² + 5 gives y = √(x − 5) (positive root since y ≥ 0).\n√16 = 4.\nx = (y − h)², y − h = √x (since y ≥ h), so f⁻¹(x) = √x + h."}, {"kind": "mcq", "text": "Which of these functions is NOT its own inverse?", "opts": ["f(x) = 6 − x", "f(x) = (x + 4)/(x − 1)", "f(x) = x + 1", "f(x) = 1/x"], "correct": 2, "tag": "", "sol": "f(f(x)) = x + 2 for x + 1. The others satisfy f(f(x)) = x: 1/(1/x) = x, 6 − (6 − x) = x, and (x + 4)/(x − 1) has top coefficient 1 = −(−1)."}]}, {"id": "s9", "label": "Assessment C", "sub": "Communicating", "slides": [{"kind": "mcq", "text": "Meera writes: \"For f(x) = 2x + 3, f⁻¹(x) = 1/(2x + 3).\" Which reply explains her mistake best?", "opts": ["Her answer is right, but she forgot to verify it", "She should write 1/(2x) + 3", "The −1 is not an exponent: f⁻¹ undoes f, and here f⁻¹(x) = (x − 3)/2", "She is right: f⁻¹ means 1/f"], "correct": 2, "tag": "", "sol": "1/(2x + 3) is the reciprocal of f. Check: f(1) = 5, and the inverse must send 5 back to 1: (5 − 3)/2 = 1, but 1/(2·5 + 3) = 1/13."}, {"kind": "blank", "p": "Kabir found the inverse of f(x) = 5x − 2. He swapped to get x = 5y − 2, solved y = (x + 2)/5, then wrote \"f⁻¹(x) = (y + 2)/5\".", "tag": "", "marks": "", "flat": [{"t": "The correct inverse is f⁻¹(x) = __B1__", "a": {"B1": "(x+2)/5"}, "expr": true}, {"t": "Check: f(3) = 13, so f⁻¹(13) = __B1__", "a": {"B1": "3"}}, {"t": "Kabir went wrong in step 4: after solving, replace __B1__ with f⁻¹(x)", "a": {"B1": "y"}, "expr": "words", "accept": ["y only"]}], "sol": "After solving, the answer is in x: (x + 2)/5.\n(13 + 2)/5 = 3 ✔.\nStep 4 replaces y by f⁻¹(x); the rule must be written in terms of x."}, {"kind": "mcq", "text": "Which is a complete argument that f(x) = 7 − 3x is one-to-one?", "opts": ["Its graph goes through (0, 7)", "Its graph passes the vertical line test", "f(0) = 7 and f(1) = 4 are different", "If 7 − 3a = 7 − 3b then −3a = −3b, so a = b: equal outputs force equal inputs"], "correct": 3, "tag": "", "sol": "One-to-one needs every pair of inputs, so a general argument is required. Two values prove nothing, and the vertical line test only shows f is a function."}, {"kind": "blank", "p": "Priya inverted f(x) = (3x − 1)/(x + 2). She wrote xy + 2x = 3y − 1, then got f⁻¹(x) = (2x + 1)/(x − 3).", "tag": "", "marks": "", "flat": [{"t": "Collect the y terms correctly: xy − 3y = __B1__", "a": {"B1": "-1-2x"}, "expr": true}, {"t": "The correct inverse is f⁻¹(x) = __B1__", "a": {"B1": "(2x+1)/(3-x)"}, "expr": true}, {"t": "Check with f(1) = 2/3: f⁻¹(2/3) = __B1__", "a": {"B1": "1"}}], "sol": "Move 3y left and 2x right: xy − 3y = −1 − 2x.\ny(x − 3) = −(2x + 1), so y = (2x + 1)/(3 − x). Priya lost the minus sign.\n(4/3 + 1)/(3 − 2/3) = (7/3)/(7/3) = 1 ✔. Priya's formula gives −1."}, {"kind": "mcq", "text": "Which sentence best explains why f(x) = x² (all real x) has no inverse?", "opts": ["x² is not continuous", "f(−2) = f(2) = 4, so f⁻¹(4) would have to be both −2 and 2", "Squares cannot be undone", "The graph of x² fails the vertical line test"], "correct": 1, "tag": "", "sol": "An inverse must send 4 to one input, but two inputs give 4. On x ≥ 0 the square can be undone by √x, so 'squares cannot be undone' is false."}, {"kind": "blank", "p": "Show that f(x) = ∛x + 2 and g(x) = (x − 2)³ are inverses.", "tag": "", "marks": "", "flat": [{"t": "f(g(x)) = ∛((x − 2)³) + 2 = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "g(f(x)) = ((∛x + 2) − 2)³ = __B1__", "a": {"B1": "x"}, "expr": true}, {"t": "Conclusion: f and g are __B1__", "a": {"B1": "inverses"}, "expr": "words", "accept": ["inverse", "inverse functions", "inverses of each other"]}], "sol": "∛((x − 2)³) = x − 2 (a cube root undoes a cube for every real number), so x − 2 + 2 = x.\n(∛x)³ = x.\nBoth compositions give x for every real x."}, {"kind": "mcq", "text": "Arjun says: \"To graph f⁻¹, reflect the graph of f in the x-axis.\" Which response is correct?", "opts": ["Wrong mirror: f⁻¹ is the reflection in y = x, so (a, b) goes to (b, a)", "Nearly: reflect in the y-axis instead", "Correct only for linear functions", "Correct: reflecting in the x-axis gives the inverse"], "correct": 0, "tag": "", "sol": "Reflecting in the x-axis gives −f(x), sending (a, b) to (a, −b). The inverse swaps inputs and outputs, which is the reflection in y = x."}, {"kind": "blank", "p": "f(x) = x² − 4 for x ≥ 0. Explain how to choose f⁻¹.", "tag": "", "marks": "", "flat": [{"t": "The range of f is y ≥ __B1__", "a": {"B1": "-4"}}, {"t": "Swap: x = y² − 4, so f⁻¹(x) = √( __B1__ )", "a": {"B1": "x+4"}, "expr": true}, {"t": "We choose the positive root because the range of f⁻¹ must equal the __B1__ of f", "a": {"B1": "domain"}, "expr": "words"}], "sol": "x² ≥ 0, so x² − 4 ≥ −4.\ny² = x + 4 and y ≥ 0, so y = √(x + 4), for x ≥ −4.\nThe domain of f is x ≥ 0, so f⁻¹ must give y ≥ 0."}]}, {"id": "s10", "label": "Assessment D", "sub": "Applying mathematics in real-life contexts", "slides": [{"kind": "blank", "p": "A thermometer converts °C to °F with f(x) = 9x/5 + 32, where x is in °C.", "tag": "", "marks": "", "flat": [{"t": "The inverse, which turns °F into °C, is f⁻¹(x) = __B1__", "a": {"B1": "5(x-32)/9"}, "expr": true}, {"t": "Body temperature 98.6 °F is __B1__ °C", "a": {"B1": "37"}}, {"t": "f⁻¹(f(25)) = __B1__", "a": {"B1": "25"}}], "sol": "x = 9y/5 + 32, so 9y/5 = x − 32 and y = 5(x − 32)/9.\n5 × 66.6/9 = 37 °C.\nf(25) = 77 °F and f⁻¹(77) = 25: the conversions undo each other."}, {"kind": "mcq", "text": "A travel desk charges c(d) = 84d + 100 rupees to buy d US dollars (₹84 per dollar plus a ₹100 fee). How many dollars do you get for ₹2620?", "opts": ["$220 180", "$31.19", "$30", "$32.38"], "correct": 2, "tag": "", "sol": "Use the inverse d = (c − 100)/84: (2620 − 100)/84 = 2520/84 = 30. Forgetting the fee gives 2620/84 ≈ 31.19; adding it gives 32.38; 84 × 2620 + 100 applies c instead of its inverse."}, {"kind": "blank", "p": "A taxi fare is F(x) = 50 + 18x rupees for a ride of x km.", "tag": "", "marks": "", "flat": [{"t": "F⁻¹(x) = __B1__", "a": {"B1": "(x-50)/18"}, "expr": true}, {"t": "A fare of ₹500 means a ride of __B1__ km", "a": {"B1": "25"}}, {"t": "F⁻¹ takes a fare and gives the __B1__", "a": {"B1": "distance"}, "expr": "words", "accept": ["distance travelled", "kilometres", "km", "number of kilometres", "distance in km"]}], "sol": "x = 50 + 18y, so y = (x − 50)/18.\n(500 − 50)/18 = 25 km.\nF turns distance into fare, so F⁻¹ turns fare into distance."}, {"kind": "mcq", "text": "A secret code turns a letter number n (A = 1, …, Z = 26) into E(n) = 3n + 5. Which function decodes a received number m?", "opts": ["D(m) = 3m − 5", "D(m) = (m − 5)/3", "D(m) = (m + 5)/3", "D(m) = m/3 − 5"], "correct": 1, "tag": "", "sol": "D must undo E: subtract 5, then divide by 3. For example 32 decodes to (32 − 5)/3 = 9, the letter I. Check: E(9) = 32."}, {"kind": "blank", "p": "A bakery's daily cost for q loaves is C(q) = 2000 + 15q rupees.", "tag": "", "marks": "", "flat": [{"t": "Quantity as a function of cost: C⁻¹(x) = __B1__", "a": {"B1": "(x-2000)/15"}, "expr": true}, {"t": "A cost of ₹5000 means __B1__ loaves", "a": {"B1": "200"}}, {"t": "With a budget of ₹8000 the bakery can make __B1__ loaves", "a": {"B1": "400"}}], "sol": "x = 2000 + 15q, so q = (x − 2000)/15.\n3000/15 = 200.\n6000/15 = 400."}, {"kind": "mcq", "text": "The volume of a cube of side s cm is V(s) = s³. A cube holds 343 cm³. Use the inverse to find its side.", "opts": ["18.52 cm", "7 cm", "114.3 cm", "49 cm"], "correct": 1, "tag": "", "sol": "V⁻¹(x) = ∛x, and ∛343 = 7, since 7³ = 343. 343/3 ≈ 114.3 divides by 3, √343 ≈ 18.52 uses the wrong root, and 49 = 7²."}, {"kind": "blank", "p": "A stone dropped from a cliff falls d(t) = 4.9t² metres in t seconds (t ≥ 0).", "tag": "", "marks": "", "flat": [{"t": "The time to fall x metres is t(x) = √( __B1__ )", "a": {"B1": "x/4.9"}, "expr": true}, {"t": "It takes __B1__ s to fall 122.5 m", "a": {"B1": "5"}}, {"t": "We use only t ≥ 0 because time cannot be __B1__", "a": {"B1": "negative"}, "expr": "words", "accept": ["less than zero", "below zero"]}], "sol": "x = 4.9t², so t² = x/4.9 and t = √(x/4.9) (positive root).\n122.5/4.9 = 25 and √25 = 5 s.\nRestricting to t ≥ 0 makes d one-to-one, so the inverse exists."}, {"kind": "mcq", "text": "A plumber charges P(h) = 300 + 450h rupees for h hours of work. A bill is ₹2550. How long did the job take?", "opts": ["5 hours", "5.67 hours", "6.33 hours", "1 147 800 hours"], "correct": 0, "tag": "", "sol": "P⁻¹(x) = (x − 300)/450, so (2550 − 300)/450 = 5 hours. Adding the call-out fee gives 6.33; ignoring it gives 5.67; 300 + 450 × 2550 = 1 147 800 applies P to 2550 instead of its inverse."}]}];
/* ================= build slide lists ================= */
var SLIDES = {}; SECTIONS.forEach(function(sec){ SLIDES[sec.id]=sec.slides; });
var TAB_DEFS = SECTIONS.map(function(sec){ return {id:sec.id, label:sec.label, sub:sec.sub}; });

/* ================= state ================= */
function blankItem(slide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    return {status:'unanswered', attempts:0, choice:undefined};
  }
  return {status:'unanswered', curStep:0, stepStates: slide.flat.map(function(){ return {status:'unanswered', attempts:0, inputs:{}}; })};
}
function defaultState(){
  var s={tabs:{}};
  TAB_DEFS.forEach(function(td){
    s.tabs[td.id] = { idx:0, maxReached:0, items: SLIDES[td.id].map(function(sl){ return blankItem(sl); }) };
  });
  return s;
}
var appState = {mode:null, learning:null, quiz:null};
var state = null;      // alias for appState[appState.mode]
var MODE = null;
var activeTab=TAB_DEFS[0].id;

function setMode(m){
  appState.mode = m;
  if(!appState[m]) appState[m] = defaultState();
  state = appState[m];
  MODE = m;
}
/* ================= student accounts (saved on this device) ================= */
var SHEET_KEY='sopaan-calc-inverse-functions';
var ACC_KEY='sopaan-students-v1';
var storageOK=true;
var MEM={};
function lsGet(k){ var r=null; try{ r=localStorage.getItem(k); }catch(e){ storageOK=false; }
  if(r===null||r===undefined) r=MEM[k]||null; try{ return r?JSON.parse(r):null; }catch(e){ return null; } }
function lsSet(k,v){ var j=JSON.stringify(v); MEM[k]=j; try{ localStorage.setItem(k,j); return true; }catch(e){ storageOK=false; return false; } }
try{ localStorage.setItem('sopaan-probe','1'); localStorage.removeItem('sopaan-probe'); }catch(e){ storageOK=false; }
function hashPin(pin,salt){ var h=2166136261, str=salt+'|'+pin; for(var i=0;i<str.length;i++){ h^=str.charCodeAt(i); h=Math.imul(h,16777619)>>>0; } return h.toString(36); }
function accKey(name,roll){ return (name.trim().toLowerCase().replace(/\s+/g,' ')+'#'+roll.trim().toLowerCase()); }
function accounts(){ return lsGet(ACC_KEY)||{students:{}}; }
var student=null; // {key,name,roll}
var records=[];   // finished-tab history for this student on this sheet
function progKey(){ return SHEET_KEY+'::'+student.key; }

function loadState(){
  appState = {mode:null, learning:null, quiz:null}; records=[]; activeTab=TAB_DEFS[0].id;
  var saved=lsGet(progKey());
  if(!saved) return;
  try{
    ['learning','quiz'].forEach(function(m){
      if(saved[m] && saved[m].tabs){
        var fresh = defaultState();
        TAB_DEFS.forEach(function(td){
          if(saved[m].tabs[td.id] && saved[m].tabs[td.id].items && saved[m].tabs[td.id].items.length===SLIDES[td.id].length){
            fresh.tabs[td.id] = saved[m].tabs[td.id];
          }
        });
        appState[m] = fresh;
      }
    });
    if(saved.mode==='learning' || saved.mode==='quiz') appState.mode = saved.mode;
    if(saved.activeTab && TAB_DEFS.some(function(t){ return t.id===saved.activeTab; })) activeTab = saved.activeTab;
    if(Array.isArray(saved.records)) records = saved.records;
  }catch(e){}
}
function saveState(){
  if(!student) return;
  lsSet(progKey(), {mode:appState.mode, learning:appState.learning, quiz:appState.quiz, activeTab:activeTab, records:records, updated:Date.now()});
  var acc=accounts(); if(acc.students[student.key]){ acc.students[student.key].last=Date.now(); lsSet(ACC_KEY,acc); }
}
function addRecord(mode, tabId, correct, revealed, skipped, total){
  records.unshift({at:Date.now(), mode:mode, tab:tabId, correct:correct, revealed:revealed, skipped:skipped, total:total});
  if(records.length>60) records.length=60;
  saveState();
}
function fmtDate(ms){ try{ return new Date(ms).toLocaleString(undefined,{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function renderWho(){
  var el=document.getElementById('whoBar');
  if(!student){ el.hidden=true; el.innerHTML=''; return; }
  el.hidden=false;
  el.innerHTML='Signed in as <b>'+esc(student.name)+'</b> · Roll '+esc(student.roll)+
    ' <button id="btnRecord">My record</button> <button id="btnSignOut">Sign out</button>';
  document.getElementById('btnRecord').addEventListener('click', renderRecord);
  document.getElementById('btnSignOut').addEventListener('click', signOut);
}
function signOut(){
  saveState(); student=null; state=null; MODE=null;
  var acc=accounts(); delete acc.current; lsSet(ACC_KEY,acc);
  document.getElementById('modePill').hidden=true;
  renderWho(); renderLogin();
}
function signIn(key){
  var acc=accounts(); var st=acc.students[key]; if(!st) return;
  student={key:key, name:st.name, roll:st.roll};
  acc.current=key; st.last=Date.now(); lsSet(ACC_KEY,acc);
  loadState(); renderWho();
  if(appState.mode==='learning' || appState.mode==='quiz'){
    setMode(appState.mode); document.getElementById('modePill').hidden=false; updateModePill();
    showChrome(true); buildTabbar(); renderSlide();
    showToast('Welcome back, '+st.name.split(' ')[0]+'. Picking up where you left off.');
  } else {
    renderModePicker();
  }
}
function renderLogin(msg){
  showChrome(false);
  var acc=accounts(); var keys=Object.keys(acc.students).sort(function(a,b){ return (acc.students[b].last||0)-(acc.students[a].last||0); });
  var h='<div class="login-card"><h2>Student sign-in</h2>'+
    '<p class="lead">Sign in to save your answers, see your record and continue where you left off next time.</p>';
  if(!storageOK) h+='<div class="login-err">This browser is blocking saved data (for example, a private window). You can still practise, but progress will not be kept after you close the page.</div>';
  if(msg) h+='<div class="login-err">'+esc(msg)+'</div>';
  if(keys.length){
    h+='<div class="known"><span class="known-label">Continue as</span>';
    keys.slice(0,6).forEach(function(k){ var st=acc.students[k];
      h+='<button class="known-btn" data-k="'+esc(k)+'"><span>'+esc(st.name)+' <small>· Roll '+esc(st.roll)+'</small></span><small>'+(st.last?'Last active '+fmtDate(st.last):'')+'</small></button>'; });
    h+='</div>';
  }
  h+='<form id="loginForm" novalidate>'+
    '<div class="fld"><label for="lgName">Full name</label><input id="lgName" autocomplete="name" required></div>'+
    '<div class="fld-row"><div class="fld"><label for="lgRoll">Roll no.</label><input id="lgRoll" required></div>'+
    '<div class="fld"><label for="lgPin">4-digit PIN</label><input id="lgPin" type="password" inputmode="numeric" maxlength="4" autocomplete="off" required></div></div>'+
    '<button class="btn btn-primary" type="submit" style="width:100%;">Sign in</button>'+
    '<p class="login-note">New here? Enter your name, roll no. and a PIN you will remember, and your profile is created. Progress is saved on this device, so use the same device and browser to continue.</p>'+
    '</form></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  wrap.querySelectorAll('.known-btn').forEach(function(b){
    b.addEventListener('click', function(){
      var st=accounts().students[b.dataset.k];
      document.getElementById('lgName').value=st.name; document.getElementById('lgRoll').value=st.roll;
      document.getElementById('lgPin').focus();
    });
  });
  document.getElementById('loginForm').addEventListener('submit', function(e){
    e.preventDefault();
    var name=document.getElementById('lgName').value.trim(), roll=document.getElementById('lgRoll').value.trim(), pin=document.getElementById('lgPin').value.trim();
    if(!name||!roll){ renderLoginErr('Enter your name and roll no.'); return; }
    if(!/^\d{4}$/.test(pin)){ renderLoginErr('Your PIN must be exactly 4 digits.'); return; }
    var k=accKey(name,roll); var acc=accounts();
    if(acc.students[k]){
      if(acc.students[k].pin!==hashPin(pin,k)){ renderLoginErr('That PIN does not match this name and roll no. Try again.'); return; }
    } else {
      acc.students[k]={name:name.replace(/\s+/g,' '), roll:roll, pin:hashPin(pin,k), created:Date.now()};
      lsSet(ACC_KEY,acc);
    }
    signIn(k);
  });
}
function renderLoginErr(m){
  var n=document.getElementById('lgName').value, r=document.getElementById('lgRoll').value;
  renderLogin(m); document.getElementById('lgName').value=n; document.getElementById('lgRoll').value=r; document.getElementById('lgPin').focus();
}
function tabSummary(m){
  var st=appState[m]; if(!st) return null;
  return TAB_DEFS.map(function(td){
    var items=st.tabs[td.id].items, n=items.length;
    var c=items.filter(function(i){return i.status==='correct';}).length;
    var done=items.filter(function(i){return i.status!=='unanswered';}).length;
    return {label:td.label, n:n, done:done, correct:c};
  });
}
function renderRecord(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+' · Right Triangles and Trigonometry</p>';
  ['learning','quiz'].forEach(function(m){
    var sum=tabSummary(m);
    h+='<h3>'+(m==='learning'?'📘 Learning Sheet':'📝 Quiz Mode')+'</h3>';
    if(!sum){ h+='<p class="rec-empty">Not started yet.</p>'; return; }
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>Section</th><th>Progress</th><th>Correct first time</th></tr></thead><tbody>';
    sum.forEach(function(r){ var pct=Math.round(r.done/r.n*100);
      h+='<tr><td>'+r.label+'</td><td><span class="rec-bar"><i style="width:'+pct+'%"></i></span>'+r.done+' / '+r.n+'</td><td>'+(m==='quiz'?'—':r.correct+' / '+r.n)+'</td></tr>'; });
    h+='</tbody></table></div>';
  });
  h+='</div><div class="rec-card"><h3>Finished sections</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sections finished yet. Each time you finish a tab, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>When</th><th>Mode</th><th>Section</th><th>Score</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+(r.mode==='learning'?' <span class="rec-empty">('+r.revealed+' revealed, '+r.skipped+' skipped)</span>':'')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){
    if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker();
  });
  window.scrollTo({top:0});
}

/* ================= tab bar ================= */
function buildTabbar(){
  var el=document.getElementById('tabbar');
  el.innerHTML = '<button class="tab-btn'+(activeTab==='theory'?' active':'')+'" data-tab="theory">Theory<span class="tab-count">notes</span></button>' + TAB_DEFS.map(function(t){
    return '<button class="tab-btn'+(t.id===activeTab?' active':'')+'" data-tab="'+t.id+'">'+t.label+'<span class="tab-count">'+SLIDES[t.id].length+'</span></button>';
  }).join('') + '<button class="tab-btn'+(activeTab==='report'?' active':'')+'" data-tab="report">📊 Report<span class="tab-count">pie</span></button>';
  el.querySelectorAll('.tab-btn').forEach(function(btn){
    btn.addEventListener('click', function(){ activeTab=btn.dataset.tab; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  });
}

/* ================= rendering ================= */
function canProceed(item){ return item.status==='correct'||item.status==='revealed'||item.status==='skipped'; }

function renderSlide(){
  if(!state.tabs[activeTab]){ activeTab=TAB_DEFS[0].id; }
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  if(ts.idx>=slides.length||ts.idx<0) ts.idx=0;
  var idx = ts.idx;
  var slide = slides[idx];
  var item = ts.items[idx];

  var tdef=TAB_DEFS.find(function(t){return t.id===activeTab;});
  document.getElementById('spLabel').textContent = tdef.label+' · Question '+(idx+1)+' of '+slides.length;
  document.getElementById('secSub').textContent = tdef.label+' — '+tdef.sub;
  document.getElementById('spFill').style.width = Math.round(((idx)/(Math.max(slides.length-1,1)))*100)+'%';

  var h='<div class="qcard">';
  if(slide.kind==='mcq' || slide.kind==='ar'){
    h += renderChoiceBody(slide, item, idx);
  } else {
    h += renderBlankBody(slide, item, idx);
  }
  h += '<div class="feedback" id="feedbackBox"></div>';
  if(MODE==='learning' && (item.status==='correct'||item.status==='revealed')) h += solutionHTML(slide);
  h += '</div>';

  document.getElementById('wrap').innerHTML = h;
  wireSlideEvents(slide, item, idx);
  restoreFeedback(item);
  renderNavbar(item);
  updateFab();
  saveState();
}

function solutionHTML(slide){
  if(!slide.sol) return '';
  return '<div class="solution"><div class="sol-h">Solution</div>'+slide.sol.split('\n').map(function(l){ return '<div class="sol-line">'+fr(esc(l))+'</div>'; }).join('')+'</div>';
}
var LETTERS=['a','b','c','d','e','f'];
function chosenHTML(slide,item){
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(item.choice===undefined) return '';
  var ok=item.choice===slide.correct;
  var h='<div class="chosen '+(ok?'ok':'bad')+'"><b>Your answer:</b> ('+LETTERS[item.choice]+') '+fr(esc(opts[item.choice]))+(ok?' ✓':' ✗')+'</div>';
  if(!ok) h+='<div class="chosen ok"><b>Correct answer:</b> ('+LETTERS[slide.correct]+') '+fr(esc(opts[slide.correct]))+'</div>';
  return h;
}
function renderChoiceBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div>';
  if(slide.kind==='mcq'){
    h += '<div class="qtext">'+fr(esc(slide.text))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  } else {
    h += '<div class="qtext"><span class="qtag" style="margin-left:0;margin-right:6px;">A / R</span>Assertion (A): '+fr(esc(slide.a))+'<br>Reason (R): '+fr(esc(slide.r))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  }
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(MODE==='quiz') h += '<div class="quiz-hint">Quiz mode — pick an option. The correct answer is revealed once you finish this tab.</div>';
  var locked = MODE==='learning' && (item.status==='correct' || item.status==='revealed');
  h += '<div class="options">';
  opts.forEach(function(opt,i){
    var cls='opt';
    if(locked){
      if(i===slide.correct) cls+=' is-correct';
      else if(item.choice===i) cls+=' is-wrong';
      cls+=' locked';
    }
    if(item.choice===i) cls+=' is-chosen';
    h += '<label class="'+cls+'"><input type="radio" name="choice" value="'+i+'" '+(item.choice===i?'checked':'')+' '+(locked?'disabled':'')+'> <span class="opt-l">('+LETTERS[i]+')</span> <span class="opt-t">'+fr(esc(opt))+'</span>'+(item.choice===i?'<span class="opt-tag">'+(locked?(i===slide.correct?'Your answer ✓':'Your answer ✗'):'Selected')+'</span>':'')+'</label>';
  });
  h += '</div>';
  if(locked) h += chosenHTML(slide,item);
  return h;
}

function renderBlankBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div><div class="qtext">';
  if(slide.kind==='case'){ h += '<b>'+esc(slide.title)+'.</b> '+esc(slide.body); }
  else { var pp=fr(esc(slide.p)).split('\n'); h += pp[0]+pp.slice(1).map(function(x){return '<span class="datline">'+x+'</span>';}).join(''); }
  h += (slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  if(slide.marks) h += '<div class="marks-pill">'+slide.marks+'</div>';
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';

  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  var blankCount=0; slide.flat.forEach(function(s){ blankCount+=Object.keys(s.a).length; });

  if(MODE==='quiz'){
    h += '<div class="step-badge">'+blankCount+' blank'+(blankCount===1?'':'s')+' in this question</div>';
    h += '<div class="quiz-hint">Quiz mode — fill in what you can. Correct answers are revealed once you finish this tab.</div>';
    if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
    if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
    h += '<div class="steps">';
    for(var qi=0; qi<total; qi++){
      var qstep = slide.flat[qi];
      var qss = item.stepStates[qi];
      if(qstep.partLabel) h += '<div class="subpart-label">'+esc(qstep.partLabel)+'</div>';
      if(qstep.orDivider) h += '<div class="or-divider">OR</div>';
      var qline = fr(qstep.t);
      Object.keys(qstep.a).forEach(function(bkey){
        var val = qss.inputs[bkey]||'';
        var inp='<input class="blank-input'+(['fv','fe','fl','fm','fi','dec'].indexOf(qstep.expr)>=0?' fr':(qstep.expr==='flist'||qstep.expr==='dlist'||qstep.expr==='glist')?' wide':qstep.expr===true?' expr':(qstep.expr==='words'||qstep.expr==='list'||qstep.expr==='expanded'||qstep.expr==='set'||qstep.expr==='primes'||qstep.expr==='trans'||qstep.expr==='rot'?' wide':''))+'" data-step="'+qi+'" data-bkey="'+bkey+'" value="'+esc(val)+'">';
        qline = qline.replace('__'+bkey+'__', inp);
      });
      if(qstep.fig) h += '<div class="fig">'+qstep.fig+'</div>';
      h += '<div class="step-line">'+qline+'</div>';
    }
    h += '</div>';
    return h;
  }

  if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
  if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
  var locked = item.status==='correct' || item.status==='revealed';
  var upto = locked ? total-1 : item.curStep;
  h += '<div class="step-badge">Step '+(Math.min(item.curStep,total-1)+1)+' of '+total+'</div>';
  h += '<div class="steps">';
  for(var i=0;i<=upto;i++){
    var step = slide.flat[i];
    var ss = item.stepStates[i];
    if(step.partLabel) h += '<div class="subpart-label">'+esc(step.partLabel)+'</div>';
    if(step.orDivider) h += '<div class="or-divider">OR</div>';
    var resolved = ss.status==='correct' || ss.status==='revealed';
    var line = fr(step.t);
    Object.keys(step.a).forEach(function(bkey){
      var fs = ss.inputs['fs_'+bkey];
      var cls = fs==='correct'?'is-correct':(fs==='wrong'?'is-wrong':'');
      var val = ss.inputs[bkey]||'';
      var dis = resolved ? 'disabled':'';
      var inp='<input class="blank-input '+cls+(['fv','fe','fl','fm','fi','dec'].indexOf(step.expr)>=0?' fr':(step.expr==='flist'||step.expr==='dlist'||step.expr==='glist')?' wide':step.expr===true?' expr':(step.expr==='words'||step.expr==='list'||step.expr==='expanded'||step.expr==='set'||step.expr==='primes'||step.expr==='trans'||step.expr==='rot'?' wide':''))+'" data-step="'+i+'" data-bkey="'+bkey+'" value="'+esc(val)+'" '+dis+'>';
      line = line.replace('__'+bkey+'__', inp);
    });
    if(step.fig) h += '<div class="fig">'+step.fig+'</div>';
    h += '<div class="step-line'+(resolved?' resolved':'')+'">'+line+'</div>';
    if(ss.status==='revealed'){
      var reveals=[];
      Object.keys(step.a).forEach(function(bkey){ reveals.push(bkey+' = '+esc(step.a[bkey])); });
      h += '<div class="reveal-note">correct: '+reveals.join(', ')+'</div>';
    }
  }
  h += '</div>';
  return h;
}

var __flash=null;
function restoreFeedback(item){
  var fb=document.getElementById('feedbackBox'); if(!fb) return;
  if(__flash){ fb.className='feedback show '+__flash.c; fb.innerHTML=__flash.h; __flash=null; return; }
  if(MODE==='quiz'){ fb.className='feedback'; fb.innerHTML=''; return; }
  if(item.status==='correct'){ fb.className='feedback show ok'; fb.innerHTML='<b>All done — correct!</b>'; }
  else if(item.status==='revealed'){ fb.className='feedback show reveal'; fb.innerHTML='<b>Answer revealed above.</b> Move on whenever you’re ready.'; }
  else if(item.status==='skipped'){ fb.className='feedback show retry'; fb.innerHTML='Skipped — you can answer it now and press <b>Check</b>, or come back later from the Question Palette.'; }
  else { fb.className='feedback'; fb.innerHTML=''; }
}

function slideIsAnswered(slide,item){
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return item.stepStates.some(function(ss){ return Object.keys(ss.inputs).some(function(k){ return k.indexOf('fs_')!==0 && ss.inputs[k] && String(ss.inputs[k]).trim()!==''; }); });
}
function renderNavbar(item){
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  var slide = slides[ts.idx];
  var isLast = ts.idx === slides.length-1;
  var h='';
  h += '<button class="btn" id="btnPrev" '+(ts.idx===0?'disabled':'')+'>&larr; Previous</button>';

  if(MODE==='quiz'){
    h += '<button class="btn" id="btnSkip">Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnNext">'+(isLast?'Finish':'Next →')+'</button>';
  } else {
    h += '<button class="btn" id="btnSkip" '+(item.status!=='unanswered'?'disabled':'')+'>Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnCheck" '+((item.status!=='unanswered'&&item.status!=='skipped')?'disabled':'')+'>Check</button>';
    h += '<button class="btn btn-primary" id="btnNext" '+(canProceed(item)?'':'disabled')+'>'+(isLast?'Finish':'Next →')+'</button>';
  }
  document.getElementById('navbarInner').innerHTML = h;

  document.getElementById('btnPrev').addEventListener('click', function(){ if(ts.idx>0){ ts.idx--; renderSlide(); } });

  if(MODE==='quiz'){
    document.getElementById('btnSkip').addEventListener('click', function(){
      item.status='skipped';
      advanceQuiz(ts, slides);
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      item.status = slideIsAnswered(slide,item) ? 'answered' : 'unanswered';
      advanceQuiz(ts, slides);
    });
  } else {
    document.getElementById('btnSkip').addEventListener('click', function(){
      if(item.status==='unanswered'){ item.status='skipped'; renderSlide(); }
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      if(!canProceed(item)) return;
      if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
      else { renderFinished(); }
    });
    document.getElementById('btnCheck').addEventListener('click', function(){ handleCheck(); });
  }
}
function advanceQuiz(ts, slides){
  if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
  else { renderFinished(); }
}

function wireSlideEvents(slide, item, idx){
  document.querySelectorAll('input[type="radio"][name="choice"]').forEach(function(r){
    r.addEventListener('change', function(){ item.choice=parseInt(r.value,10); saveState();
      document.querySelectorAll('.opt').forEach(function(l){ l.classList.remove('is-chosen'); var t=l.querySelector('.opt-tag'); if(t) t.remove(); });
      var lab=r.closest('.opt'); lab.classList.add('is-chosen'); var tg=document.createElement('span'); tg.className='opt-tag'; tg.textContent='Selected'; lab.appendChild(tg); });
  });
  document.querySelectorAll('.blank-input').forEach(function(inp){
    inp.addEventListener('input', function(){
      var si=parseInt(inp.dataset.step,10), bk=inp.dataset.bkey;
      item.stepStates[si].inputs[bk]=inp.value;
      saveState();
    });
  });
}

function handleCheck(){
  var ts = state.tabs[activeTab];
  var slide = SLIDES[activeTab][ts.idx];
  var item = ts.items[ts.idx];
  if(item.status==='skipped') item.status='unanswered';
  var fb = document.getElementById('feedbackBox');

  if(slide.kind==='mcq' || slide.kind==='ar'){
    if(item.choice===undefined){ fb.className='feedback show err'; fb.innerHTML='Please choose an option first.'; return; }
    var ok = item.choice===slide.correct;
    if(ok){
      item.status='correct'; playSuccess();
      fb.className='feedback show ok'; fb.innerHTML='<b>Correct!</b>';
    } else {
      item.attempts=(item.attempts||0)+1;
      if(item.attempts>=2){ item.status='revealed'; playReveal(); }
      else { playWrong(); fb.className='feedback show retry'; fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'}; }
    }
    renderSlide();
    return;
  }

  // blank / case
  var step = slide.flat[item.curStep];
  var ss = item.stepStates[item.curStep];
  var blanks = Object.keys(step.a);
  var missing = blanks.some(function(k){ return !ss.inputs[k] || String(ss.inputs[k]).trim()===''; });
  if(missing){ fb.className='feedback show err'; fb.innerHTML='Fill in every blank in this step before checking.'; return; }

  var allGood=true;
  blanks.forEach(function(k){
    var good=answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr);
    ss.inputs['fs_'+k]=good?'correct':'wrong';
    if(!good) allGood=false;
  });

  if(allGood){
    ss.status='correct'; playSuccess();
    advanceStepOrFinish(item, slide);
  } else {
    ss.attempts=(ss.attempts||0)+1;
    if(ss.attempts>=2){
      ss.status='revealed'; playReveal();
      advanceStepOrFinish(item, slide);
    } else {
      playWrong();
      fb.className='feedback show retry';
      fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'};
      renderSlide();
      return;
    }
  }
  renderSlide();
}

function advanceStepOrFinish(item, slide){
  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  if(item.curStep < total-1){
    item.curStep++;
  } else {
    var anyRevealed = item.stepStates.some(function(ss){ return ss.status==='revealed'; });
    item.status = anyRevealed ? 'revealed' : 'correct';
  }
}

/* ================= palette ================= */
var overlay=document.getElementById('overlay');
function statusOf(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  return ts.items[i].status==='unanswered' ? 'locked' : ts.items[i].status;
}
function buildPalette(){
  var slides=SLIDES[activeTab];
  document.getElementById('paletteTitle').textContent = TAB_DEFS.find(function(t){return t.id===activeTab;}).label+' · Question palette';
  var body=document.getElementById('paletteBody');
  var html='';
  for(var i=0;i<slides.length;i++){
    html += '<div class="chip" data-status="'+statusOf(activeTab,i)+'" data-idx="'+i+'">'+(i+1)+'</div>';
  }
  body.innerHTML = html;
  body.querySelectorAll('.chip').forEach(function(chip){
    chip.addEventListener('click', function(){
      var i=parseInt(chip.dataset.idx,10);
      var ts=state.tabs[activeTab];
      if(i>ts.maxReached){ showToast('Finish the earlier questions to unlock this one.'); return; }
      ts.idx=i; closePalette(); renderSlide();
    });
  });
}
function openPalette(){ buildPalette(); overlay.classList.add('show'); }
function closePalette(){ overlay.classList.remove('show'); }
var toastTimer;
function showToast(msg){
  var t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer); toastTimer=setTimeout(function(){ t.classList.remove('show'); },2200);
}
document.getElementById('paletteFab').addEventListener('click', openPalette);
document.getElementById('paletteClose').addEventListener('click', closePalette);
overlay.addEventListener('click', function(e){ if(e.target===overlay) closePalette(); });

function updateFab(){
  var slides=SLIDES[activeTab];
  var done=state.tabs[activeTab].items.filter(function(it){ return it.status==='correct'||it.status==='revealed'||it.status==='skipped'; }).length;
  document.getElementById('fabBadge').textContent = done+'/'+slides.length;
}

/* ================= overall progress + finish ================= */
function updateChapterProgress(){
  var total=0, done=0;
  TAB_DEFS.forEach(function(td){
    state.tabs[td.id].items.forEach(function(it){
      total++;
      if(it.status==='correct'||it.status==='revealed'||it.status==='skipped') done++;
    });
  });
  var pct = total>0 ? Math.round((done/total)*100) : 0;
  document.getElementById('cpFill').style.width=pct+'%';
  document.getElementById('cpLabel').textContent=pct+'% complete';
}
function isSlideCorrect(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice===slide.correct;
  return slide.flat.every(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).every(function(k){ return answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr); });
  });
}
function isSlideAttempted(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return slide.flat.some(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).some(function(k){ return ss.inputs[k] && String(ss.inputs[k]).trim()!==''; });
  });
}
function slideLabel(slide){
  var t = slide.kind==='case' ? slide.title : (slide.kind==='ar' ? slide.a : (slide.p||slide.text||''));
  t = String(t);
  return t.length>90 ? t.slice(0,90)+'…' : t;
}
function slideAnswerText(slide, item, correctSide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
    if(correctSide) return '('+LETTERS[slide.correct]+') '+opts[slide.correct];
    return item.choice!==undefined ? '('+LETTERS[item.choice]+') '+opts[item.choice] : '— not attempted —';
  }
  return slide.flat.map(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).map(function(k){
      return correctSide ? step.a[k] : (ss.inputs[k] || '—');
    }).join(', ');
  }).join('  |  ');
}

function renderFinished(){
  if(MODE==='quiz'){ renderQuizResults(); return; }
  var ts=state.tabs[activeTab];
  var correct=ts.items.filter(function(i){return i.status==='correct';}).length;
  var revealed=ts.items.filter(function(i){return i.status==='revealed';}).length;
  var skipped=ts.items.filter(function(i){return i.status==='skipped';}).length;
  var h='<div class="qcard done-card"><div class="big">✨</div><h2>Tab complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">You worked through all '+ts.items.length+' questions in this tab.</p>';
  if(!ts.recorded){ ts.recorded=true; addRecord('learning', activeTab, correct, revealed, skipped, ts.items.length); }
  h+='<div class="score-pills">'+
     '<span class="score-pill" style="background:var(--success-soft);color:var(--success);">'+correct+' correct</span>'+
     '<span class="score-pill" style="background:var(--danger-soft);color:var(--danger);">'+revealed+' revealed</span>'+
     '<span class="score-pill" style="background:var(--gold-soft);color:var(--retry-text);">'+skipped+' skipped</span></div>'+
     '<button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; ts.recorded=false; renderSlide(); });
  updateChapterProgress(); saveState();
}

function renderQuizResults(){
  var ts=state.tabs[activeTab];
  var slides=SLIDES[activeTab];
  var correctCount=0, attemptedCount=0;
  var rowsHtml = slides.map(function(slide,i){
    var item=ts.items[i];
    var ok=isSlideCorrect(activeTab,i);
    var att=isSlideAttempted(activeTab,i);
    if(ok) correctCount++;
    if(att) attemptedCount++;
    var tagCls = ok?'ok':(att?'bad':'na');
    var tagText = ok?'Correct':(att?'Incorrect':'Not attempted');
    var row='<div class="review-row">';
    row+='<span class="review-tag '+tagCls+'">Q'+(i+1)+' · '+tagText+'</span>';
    row+='<div class="review-q">'+fr(esc(slideLabel(slide)))+'</div>';
    row+='<div class="review-ans"><b>Your answer:</b> '+fr(esc(slideAnswerText(slide,item,false)))+'</div>';
    if(!ok) row+='<div class="review-ans" style="color:var(--success);"><b>Correct answer:</b> '+fr(esc(slideAnswerText(slide,item,true)))+'</div>';
    if(slide.sol) row+='<details class="rev-sol"><summary>Show solution</summary>'+solutionHTML(slide)+'</details>';
    row+='</div>';
    return row;
  }).join('');

  addRecord('quiz', activeTab, correctCount, 0, 0, slides.length);
  var h='<div class="qcard done-card" style="text-align:left;">';
  h+='<div style="text-align:center;"><div class="big">🏁</div><h2>Quiz complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">'+correctCount+' / '+slides.length+' correct · '+attemptedCount+' attempted</p></div>';
  h+='<div style="margin-top:16px;">'+rowsHtml+'</div>';
  h+='<div style="text-align:center;margin-top:6px;"><button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  h+='</div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; renderSlide(); });
  playSuccess();
  updateChapterProgress(); saveState();
}

/* ================= mode picker ================= */
function updateModePill(){
  var btn=document.getElementById('modePill');
  if(!btn) return;
  btn.textContent = MODE==='quiz' ? '📝 Quiz Mode · switch' : '📘 Learning Sheet · switch';
}
function showChrome(show){
  document.querySelector('.tabbar').style.display = show?'':'none';
  document.querySelector('.slide-progress').style.display = show?'':'none';
  document.querySelector('.navbar').style.display = show?'':'none';
  document.getElementById('paletteFab').style.display = show?'':'none';
}
function renderModePicker(){
  showChrome(false);
  var wrap=document.getElementById('wrap');
  wrap.innerHTML =
    '<div class="mode-pick">'+
      '<div class="mode-card" data-pick="learning"><div class="mode-icon">📘</div><h3>Learning Sheet</h3>'+
      '<p>Work through each question step by step with instant feedback — two tries, then the correct value is revealed right there so you can keep moving.</p></div>'+
      '<div class="mode-card" data-pick="quiz"><div class="mode-icon">📝</div><h3>Quiz Mode</h3>'+
      '<p>Attempt every question with no hints along the way. Your score and the full answer key are shown together once you finish the tab — just like the real exam.</p></div>'+
    '</div>';
  wrap.querySelectorAll('[data-pick]').forEach(function(card){
    card.addEventListener('click', function(){
      setMode(card.dataset.pick); activeTab='theory';
      document.getElementById('modePill').hidden=false;
      updateModePill();
      showChrome(true);
      buildTabbar();
      renderSlide();
    });
  });
}
document.getElementById('modePill').addEventListener('click', function(){
  if(!appState.mode){ return; }
  setMode(appState.mode==='quiz' ? 'learning' : 'quiz');
  updateModePill();
  showChrome(true);
  buildTabbar();
  renderSlide();
});

/* ================= boot ================= */
var _origRenderSlide = renderSlide;
renderSlide = function(){ _origRenderSlide(); updateChapterProgress(); updateModePill(); };


/* ================= theory tab ================= */
function renderTheory(){
  var wrap=document.getElementById('wrap');
  wrap.innerHTML='<div class="theory">'+fr(THEORY)+'</div>';
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Theory — notes, key ideas and worked examples';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
  wrap.querySelectorAll('[data-jump]').forEach(function(b){ b.addEventListener('click',function(){ var t=document.getElementById(b.dataset.jump); if(t) t.scrollIntoView({behavior:'smooth',block:'start'}); }); });
}
var _rsTheory = renderSlide;
renderSlide = function(){
  if(activeTab==='theory'){ renderTheory(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  document.querySelector('.slide-progress').style.display='';
  document.querySelector('.navbar').style.display='';
  document.getElementById('paletteFab').style.display='';
  _rsTheory();
};


/* ================= MYP criterion report ================= */
var CRIT_COL={A:'var(--accent-text)',B:'var(--gold)',C:'#8A6FC4',D:'#2F9AA0'};
function critStats(){
  return REPORT.map(function(r){
    var tabId=r[0], slides=SLIDES[tabId], ts=state&&state.tabs[tabId];
    var c=0,w=0,n=0;
    slides.forEach(function(sl,i){
      if(!ts||!ts.items[i]){ n++; return; }
      var it=ts.items[i];
      if(MODE==='learning'){
        if(it.status==='correct') c++; else if(it.status==='revealed') w++; else n++;
      } else {
        if(isSlideCorrect(tabId,i)) c++; else if(isSlideAttempted(tabId,i)) w++; else n++;
      }
    });
    var tot=slides.length, pct=tot?Math.round(c/tot*100):0;
    var lvl=Math.round(c/Math.max(tot,1)*8);
    return {tab:tabId,letter:r[1],name:r[2],c:c,w:w,n:n,tot:tot,pct:pct,lvl:lvl};
  });
}
function arcPath(cx,cy,r,a0,a1){
  if(a1-a0>=Math.PI*2-1e-6){ return 'M'+(cx-r)+','+cy+' a'+r+','+r+' 0 1,0 '+(2*r)+',0 a'+r+','+r+' 0 1,0 '+(-2*r)+',0 Z'; }
  var x0=cx+r*Math.sin(a0), y0=cy-r*Math.cos(a0), x1=cx+r*Math.sin(a1), y1=cy-r*Math.cos(a1);
  return 'M'+cx+','+cy+' L'+x0.toFixed(2)+','+y0.toFixed(2)+' A'+r+','+r+' 0 '+((a1-a0)>Math.PI?1:0)+',1 '+x1.toFixed(2)+','+y1.toFixed(2)+' Z';
}
function pieSVG(parts,size,hole,center,sub){
  var tot=parts.reduce(function(s,p){return s+p.v;},0), cx=size/2, cy=size/2, r=size/2-4, a=0, h='';
  if(!tot){ h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+r+'" style="fill:var(--paper-2);stroke:var(--rule)"/>'; }
  parts.forEach(function(p){ if(!p.v) return; var b=a+p.v/tot*Math.PI*2; h+='<path d="'+arcPath(cx,cy,r,a,b)+'" style="fill:'+p.col+';stroke:var(--card);stroke-width:2"><title>'+esc(p.label)+': '+p.v+'</title></path>'; a=b; });
  if(hole) h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+(r*hole)+'" style="fill:var(--card)"/>';
  if(center) h+='<text x="'+cx+'" y="'+(cy-(sub?4:0))+'" text-anchor="middle" dominant-baseline="middle" style="fill:var(--ink);font:700 '+(size>150?22:15)+'px Fraunces,serif">'+center+'</text>';
  if(sub) h+='<text x="'+cx+'" y="'+(cy+16)+'" text-anchor="middle" style="fill:var(--ink-soft);font:600 11px \'Source Sans 3\',sans-serif">'+sub+'</text>';
  return '<svg viewBox="0 0 '+size+' '+size+'" width="'+size+'" height="'+size+'" role="img">'+h+'</svg>';
}
function band(l){ return l===0?'0':(l<=2?'1–2':(l<=4?'3–4':(l<=6?'5–6':'7–8'))); }
function renderReport(){
  var st=critStats(), totC=0, totQ=0;
  st.forEach(function(s){ totC+=s.c; totQ+=s.tot; });
  var h='<div class="theory">';
  h+='<section class="note"><h2>Chapter test report</h2><p class="lt">'+(MODE==='quiz'?'<b>Quiz mode</b> results: answers are marked when you finish each test tab.':'<b>Learning mode</b> results: a question counts as correct only if you got it without the answer being revealed. Switch to Quiz mode for an exam-style score.')+'</p>';
  h+='<div class="rep-top"><div class="rep-pie">'+pieSVG(st.map(function(s){return {v:s.c,col:CRIT_COL[s.letter],label:'Criterion '+s.letter};}),200,0.55,totC+'/'+totQ,'correct')+'</div>';
  h+='<div class="rep-legend"><div class="rep-cap">Marks earned, by criterion</div>'+st.map(function(s){ return '<div class="rep-li"><span class="sw" style="background:'+CRIT_COL[s.letter]+'"></span><b>'+s.letter+'</b>&nbsp;'+esc(s.name)+'<span class="rep-n">'+s.c+' / '+s.tot+'</span></div>'; }).join('')+'</div></div></section>';
  h+='<div class="rep-grid">'+st.map(function(s){
    return '<div class="rep-card"><div class="rep-h"><span class="crit" style="background:'+CRIT_COL[s.letter]+'">'+s.letter+'</span>'+esc(s.name)+'</div>'+
      '<div class="rep-row">'+pieSVG([{v:s.c,col:'var(--success)',label:'Correct'},{v:s.w,col:'var(--danger)',label:'Incorrect'},{v:s.n,col:'var(--locked)',label:'Not attempted'}],120,0.5,s.pct+'%')+
      '<div class="rep-stats"><div><span class="sw" style="background:var(--success)"></span>Correct <b>'+s.c+'</b></div><div><span class="sw" style="background:var(--danger)"></span>Incorrect <b>'+s.w+'</b></div><div><span class="sw" style="background:var(--locked)"></span>Not attempted <b>'+s.n+'</b></div>'+
      '<div class="rep-lvl">Indicative level <b>'+s.lvl+'</b> / 8 <span>(band '+band(s.lvl)+')</span></div></div></div>'+
      '<button class="hub-btn" data-go="'+s.tab+'">Open Test '+s.letter+' →</button></div>';
  }).join('')+'</div>';
  h+='<p class="rep-note">Indicative level = fraction of questions correct × 8, rounded. It is a practice guide only; your teacher awards the real MYP criterion levels.</p></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Report — chapter test results by MYP criterion';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
}
var _rsReport = renderSlide;
renderSlide = function(){
  if(activeTab==='report'){ renderReport(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  _rsReport();
};


/* ================= skipped-question return ================= */
function firstSkippedIdx(ts){
  for(var i=0;i<ts.items.length;i++){
    var it=ts.items[i];
    if(MODE==='quiz'){ if(!isSlideAttempted(activeTab,i)) return i; }
    else if(it.status==='skipped'||it.status==='unanswered') return i;
  }
  return -1;
}
function skippedList(ts){
  var out=[]; for(var i=0;i<ts.items.length;i++){ var it=ts.items[i];
    if(MODE==='quiz' ? !isSlideAttempted(activeTab,i) : (it.status==='skipped'||it.status==='unanswered')) out.push(i); }
  return out;
}
function renderSkipGate(ts){
  var list=skippedList(ts);
  var h='<div class="qcard done-card skip-gate"><div class="big">⏭️</div><h2>You skipped '+list.length+' question'+(list.length>1?'s':'')+'</h2>'+
    '<p style="color:var(--ink-soft);font-size:14px;">Answer them now, or submit the tab as it is. Answers are marked only when you submit.</p>'+
    '<div class="skip-chips">'+list.map(function(i){ return '<button class="chip skip-go" data-i="'+i+'">Q'+(i+1)+'</button>'; }).join('')+'</div>'+
    '<div class="skip-btns"><button class="btn btn-primary" id="btnGoSkipped">Answer skipped questions</button><button class="btn" id="btnSubmitAnyway">Submit anyway</button></div></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  var go=function(i){ ts.idx=i; ts.maxReached=Math.max(ts.maxReached,i); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); };
  document.getElementById('btnGoSkipped').addEventListener('click',function(){ go(list[0]); });
  document.querySelectorAll('.skip-go').forEach(function(b){ b.addEventListener('click',function(){ go(parseInt(b.dataset.i,10)); }); });
  document.getElementById('btnSubmitAnyway').addEventListener('click',function(){ ts.submitOK=true; renderFinished(); ts.submitOK=false; });
  saveState();
}
var _rfSkip = renderFinished;
renderFinished = function(){
  var ts=state.tabs[activeTab];
  if(MODE==='quiz' && !ts.submitOK && skippedList(ts).length){ renderSkipGate(ts); return; }
  _rfSkip();
  if(MODE==='learning'){
    var list=skippedList(ts);
    if(list.length){
      var card=document.querySelector('.done-card');
      if(card){ var d=document.createElement('div'); d.className='skip-btns';
        d.innerHTML='<button class="btn btn-primary" id="btnGoSkipped">Attempt skipped questions ('+list.length+')</button>';
        card.appendChild(d);
        document.getElementById('btnGoSkipped').addEventListener('click',function(){ ts.idx=list[0]; ts.recorded=false; renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); }
    }
  }
};


/* ================= approx answers (physics: within 1%) ================= */
var _amTools = answerMatches;
answerMatches = function(input,answer,accept,expr){
  if(expr==='approx'){
    var n1=parseNum(input); if(n1===null) return false;
    return [answer].concat(accept||[]).some(function(a){ var n2=parseNum(a); if(n2===null) return false; return Math.abs(n1-n2) <= Math.max(0.011*Math.abs(n2), 1e-9); });
  }
  return _amTools(input,answer,accept,expr);
};

/* ================= palette: every question already reached can be opened ================= */
statusOf = function(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  var s=ts.items[i].status;
  if(s==='unanswered') return 'skipped';
  return s;
};

/* ================= on-screen keyboard ================= */
var KB={on:true, page:'num', target:null};
try{ var kbp=localStorage.getItem('sopaan-kb-pref'); if(kbp==='off') KB.on=false; }catch(e){}
function kbSave(){ try{ localStorage.setItem('sopaan-kb-pref', KB.on?'on':'off'); }catch(e){} }
var KEYS_NUM=[['7','8','9','(',')'],['4','5','6','−','/'],['1','2','3','.',','],['0',':','%','°','⌫'],['abc','←','→','Clear','Done']];
var KEYS_FRAC=[['7','8','9','/'],['4','5','6','−'],['1','2','3','space'],['0',',','⌫','Clear'],['abc','←','→','Done']];
var KEYS_ALG=[['7','8','9','x','y','n'],['4','5','6','+','−','a'],['1','2','3','×','÷','b'],['0','.','(',')','^','²'],['/','π','|','t','⌫','Clear'],['abc','←','→','Done']];
function kbLayoutFor(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx], stp=sl.flat[parseInt(inp.dataset.step,10)]; var m=stp.expr, key=String(stp.a[inp.dataset.bkey]||'');
  if(m==='words'||m==='glist'||m==='angle') return 'abc'; if(m===true||m==='pow'||m==='primes') return 'alg';
  if(['fv','fe','fl','fm','fi','flist'].indexOf(m)>=0) return 'frac'; if(m==='dec'||m==='approx'||m==='dlist'||m==='set'||m==='coord'||m==='list'||m==='time') return 'num';
  if(/^[\-−]?\d+ \d+\/\d+$/.test(key)||/^[\-−]?\d+\/\d+$/.test(key)) return 'frac'; if(/[a-df-z]/i.test(key.replace(/pi/gi,''))) return /\d/.test(key)?'alg':'abc'; return 'num'; }catch(e){ return 'num'; } }
var KEYS_CALC=[['7','8','9','x','(',')'],['4','5','6','+','−','^'],['1','2','3','×','/','²'],['0','.','e','eˣ','√','ln'],['sin','cos','tan','t','⌫','Clear'],['sec','csc','cot','π','θ','∛'],['abc','←','→','Done']];
var KEYS_ABC=[['q','w','e','r','t','y','u','i','o','p'],['a','s','d','f','g','h','j','k','l','-'],['z','x','c','v','b','n','m',',',':','/'],['123','space','←','→','⌫','Done']];
function kbBuild(){
  var el=document.getElementById('vkb'); if(!el){ el=document.createElement('div'); el.id='vkb'; el.className='vkb'; document.body.appendChild(el);
    el.addEventListener('pointerdown',function(e){ var b=e.target.closest('button[data-k]'); e.preventDefault(); if(b) kbPress(b.dataset.k); });
    el.addEventListener('mousedown',function(e){ e.preventDefault(); }); }
  var rows={num:KEYS_NUM,frac:KEYS_FRAC,alg:KEYS_ALG,abc:KEYS_ABC,calc:KEYS_CALC}[KB.page]||KEYS_NUM;
  el.innerHTML='<div class="vkb-top"><span>⌨️ Keyboard</span><button data-k="device" class="vkb-link">Use device keyboard</button></div>'+
    rows.map(function(r){ return '<div class="vkb-row">'+r.map(function(k){
      var cls='vkb-k'+(/^(abc|123|Done|Clear|⌫|←|→|space)$/.test(k)?' fn':'')+(k==='Done'?' done':'');
      return '<button type="button" class="'+cls+'" data-k="'+k+'">'+(k==='space'?'space':k)+'</button>'; }).join('')+'</div>'; }).join('');
  return el;
}
function kbShow(inp){ KB.target=inp; KB.home=kbLayoutFor(inp); KB.page=KB.home; if(!KB.on) return; var cp=document.getElementById('calcPanel'); if(cp&&cp.classList.contains('show')) return; var el=kbBuild(); var nb=document.querySelector('.navbar'); el.style.bottom=(nb?nb.getBoundingClientRect().height:0)+'px'; el.classList.add('show'); document.body.classList.add('kb-open'); setTimeout(function(){ var r=inp.getBoundingClientRect(), top=el.getBoundingClientRect().top; if(r.bottom>top-12) window.scrollBy({top:r.bottom-top+60,behavior:'smooth'}); else if(r.top<60) window.scrollBy({top:r.top-80,behavior:'smooth'}); },30); }
function kbHide(){ var el=document.getElementById('vkb'); if(el) el.classList.remove('show'); document.body.classList.remove('kb-open'); }
function kbInsert(s){
  var t=KB.target; if(!t||t.disabled) return;
  var a=t.selectionStart==null?t.value.length:t.selectionStart, b=t.selectionEnd==null?a:t.selectionEnd;
  t.value=t.value.slice(0,a)+s+t.value.slice(b); var p=a+s.length; try{ t.setSelectionRange(p,p); }catch(e){}
  t.dispatchEvent(new Event('input',{bubbles:true}));
}
function kbPress(k){
  var t=KB.target; if(k==='device'){ KB.on=false; kbSave(); kbHide(); document.querySelectorAll('.blank-input').forEach(function(i){ i.removeAttribute('inputmode'); }); if(t){ t.blur(); setTimeout(function(){ t.focus(); },50); } showToast('Device keyboard on. Tap ⌨️ on any blank to bring the on-screen keyboard back.'); return; }
  if(k==='Done'){ kbHide(); if(t) t.blur(); return; }
  if(k==='abc'||k==='123'){ KB.page=(k==='abc')?'abc':(KB.home&&KB.home!=='abc'?KB.home:'num'); kbBuild(); return; }
  if(!t) return;
  if(k==='⌫'){ var a=t.selectionStart, b=t.selectionEnd; if(a===b&&a>0){ t.value=t.value.slice(0,a-1)+t.value.slice(b); try{t.setSelectionRange(a-1,a-1);}catch(e){} } else { t.value=t.value.slice(0,a)+t.value.slice(b); try{t.setSelectionRange(a,a);}catch(e){} } t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='Clear'){ t.value=''; t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='←'||k==='→'){ var p=(t.selectionStart||0)+(k==='←'?-1:1); p=Math.max(0,Math.min(t.value.length,p)); try{t.setSelectionRange(p,p);}catch(e){} return; }
  var map={'−':'-','space':' '}; kbInsert(map[k]!==undefined?map[k]:k);
}
function kbWire(){
  document.querySelectorAll('.blank-input').forEach(function(inp){
    if(inp.dataset.kb) return; inp.dataset.kb='1';
    if(KB.on) inp.setAttribute('inputmode','none');
    inp.addEventListener('focus',function(){ kbShow(inp); });
    var btn=document.createElement('button'); btn.type='button'; btn.className='kb-toggle'; btn.title='On-screen keyboard'; btn.textContent='⌨️'; btn.tabIndex=-1;
    btn.addEventListener('mousedown',function(e){ e.preventDefault(); });
    btn.addEventListener('click',function(){ KB.on=true; kbSave(); document.querySelectorAll('.blank-input').forEach(function(i){ i.setAttribute('inputmode','none'); }); inp.focus(); kbShow(inp); });
    if(!inp.disabled) inp.insertAdjacentElement('afterend',btn);
  });
}
document.addEventListener('focusout',function(e){ setTimeout(function(){ var a=document.activeElement; if(!a||!a.classList||!a.classList.contains('blank-input')){ if(!document.querySelector('#vkb:hover')) kbHide(); } },120); });

/* ================= calculator ================= */
var CALC={expr:'', ans:0};
function calcEval(src){
  var s=String(src).replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-').replace(/π/g,'(PI)').replace(/Ans/g,'('+CALC.ans+')').replace(/\^/g,'**').replace(/√\(/g,'sqrt(').replace(/²/g,'**2').replace(/E/g,'*10**');
  s=s.replace(/(^|[(*\/+\-,])-/g,'$1(-1)*');
  if(/[^0-9+\-*/().,a-z A-Z]/.test(s)) throw 0;
  var ok=s.replace(/sin|cos|tan|asin|acos|atan|sqrt|log|ln|PI|abs/g,''); if(/[a-zA-Z]/.test(ok)) throw 0;
  var f=new Function('sin','cos','tan','asin','acos','atan','sqrt','log','ln','PI','abs','return ('+s+');');
  var d=Math.PI/180;
  var v=f(function(x){return Math.sin(x*d);},function(x){return Math.cos(x*d);},function(x){return Math.tan(x*d);},
    function(x){return Math.asin(x)/d;},function(x){return Math.acos(x)/d;},function(x){return Math.atan(x)/d;},Math.sqrt,Math.log10,Math.log,Math.PI,Math.abs);
  if(typeof v!=='number'||!isFinite(v)) throw 0; return v;
}
function fmtNum(v){ if(Math.abs(v)>=1e10||(Math.abs(v)<1e-6&&v!==0)) return v.toExponential(6).replace(/\.?0+e/,'e'); return String(parseFloat(v.toPrecision(10))); }
var CKEYS=[['sin(','cos(','tan(','√(','^','²'],['asin(','acos(','atan(','(',')','π'],['7','8','9','÷','⌫','AC'],['4','5','6','×','E','Ans'],['1','2','3','−','(−)','Insert'],['0','.','=','+']];
function openCalc(){
  var p=document.getElementById('calcPanel');
  if(!p){ p=document.createElement('div'); p.id='calcPanel'; p.className='tool-panel calc';
    p.innerHTML='<div class="tp-head"><b>🧮 Calculator</b><span class="tp-note">degrees · tap a blank, then Insert</span><button class="tp-x" data-c="close">✕</button></div>'+
      '<div class="calc-disp"><div class="calc-expr" id="calcExpr"></div><div class="calc-res" id="calcRes">0</div></div>'+
      '<div class="calc-keys">'+CKEYS.map(function(r){ return r.map(function(k){ return '<button type="button" data-c="'+k+'" class="'+(k==='='?'eq':(/^(AC|⌫|Insert)$/.test(k)?'fn':''))+'">'+({'sin(':'sin','cos(':'cos','tan(':'tan','asin(':'sin⁻¹','acos(':'cos⁻¹','atan(':'tan⁻¹','√(':'√'}[k]||k)+'</button>'; }).join(''); }).join('')+'</div>';
    document.body.appendChild(p);
    p.addEventListener('mousedown',function(e){ if(e.target.closest('button')) e.preventDefault(); });
    p.addEventListener('click',function(e){ var b=e.target.closest('button[data-c]'); if(!b) return; calcKey(b.dataset.c); });
  }
  kbHide(); var nb=document.querySelector('.navbar'); p.style.bottom=((nb?nb.getBoundingClientRect().height:0)+8)+'px'; p.classList.add('show'); document.body.classList.add('calc-open'); calcShow();
}
function calcShow(res){ document.getElementById('calcExpr').textContent=CALC.expr||' '; if(res!==undefined) document.getElementById('calcRes').textContent=res; }
function calcKey(k){
  if(k==='close'){ document.getElementById('calcPanel').classList.remove('show'); document.body.classList.remove('calc-open'); return; }
  if(k==='AC'){ CALC.expr=''; calcShow('0'); return; }
  if(k==='⌫'){ CALC.expr=CALC.expr.replace(/(asin\(|acos\(|atan\(|sin\(|cos\(|tan\(|√\(|Ans|.)$/,''); calcShow(); return; }
  if(k==='='){ try{ var v=calcEval(CALC.expr); CALC.ans=v; calcShow(fmtNum(v)); }catch(e){ calcShow('Error'); } return; }
  if(k==='(−)'){ CALC.expr+='−'; calcShow(); return; }
  if(k==='Insert'){ var r=document.getElementById('calcRes').textContent; if(KB.target && !KB.target.disabled && r!=='Error'){ KB.target.value=r; KB.target.dispatchEvent(new Event('input',{bubbles:true})); showToast('Inserted '+r+' into the blank.'); } else showToast('Tap a blank first, then press Insert.'); return; }
  CALC.expr+=k; calcShow();
}

/* ================= Desmos ================= */
var DESMOS_KEY='dcb31709b452b1cf9dc26972add0fda6', desmosCalc=null, desmosLoading=false;
function openDesmos(exprs){
  var p=document.getElementById('desmosPanel');
  if(!p){ p=document.createElement('div'); p.id='desmosPanel'; p.className='tool-panel desmos';
    p.innerHTML='<div class="tp-head"><b>📈 Desmos graphing calculator</b><button class="tp-x" id="desmosReset">Reset graph</button><button class="tp-x" id="desmosClose">✕</button></div><div id="desmosBox"><div class="desmos-msg">Loading Desmos…</div></div>';
    document.body.appendChild(p);
    document.getElementById('desmosClose').addEventListener('click',function(){ p.classList.remove('show'); });
    document.getElementById('desmosReset').addEventListener('click',function(){ if(desmosCalc) desmosSet(p._exprs||[]); });
  }
  p._exprs=exprs||[]; p.classList.add('show');
  if(window.Desmos){ desmosInit(); desmosSet(p._exprs); return; }
  if(desmosLoading) return; desmosLoading=true;
  var sc=document.createElement('script'); sc.src='https://www.desmos.com/api/v1.9/calculator.js?apiKey='+DESMOS_KEY;
  sc.onload=function(){ desmosInit(); desmosSet(p._exprs); };
  sc.onerror=function(){ desmosLoading=false; document.getElementById('desmosBox').innerHTML='<div class="desmos-msg">Desmos needs an internet connection. <a href="https://www.desmos.com/calculator" target="_blank" rel="noopener">Open Desmos in a new tab</a>.</div>'; };
  document.head.appendChild(sc);
}
function desmosInit(){ if(desmosCalc) return; var box=document.getElementById('desmosBox'); box.innerHTML=''; desmosCalc=Desmos.GraphingCalculator(box,{expressionsCollapsed:false,settingsMenu:false,border:false,degreeMode:true}); }
function desmosSet(exprs){ if(!desmosCalc) return; desmosCalc.setBlank(); (exprs||[]).forEach(function(e,i){ if(typeof e==='string') desmosCalc.setExpression({id:'e'+i,latex:e}); else desmosCalc.setExpression(Object.assign({id:'e'+i},e)); }); }

/* ================= toolbar on each question ================= */
var _rsTools = renderSlide;
renderSlide = function(){
  _rsTools();
  kbHide();
  if(activeTab==='theory'||activeTab==='report') return;
  var ts=state.tabs[activeTab]; if(!ts) return;
  var slide=SLIDES[activeTab][ts.idx], card=document.querySelector('#wrap .qcard');
  if(card && slide && slide.tools && slide.tools.length && !card.querySelector('.tool-bar')){
    var bar=document.createElement('div'); bar.className='tool-bar';
    bar.innerHTML=(slide.tools.indexOf('calc')>=0?'<button type="button" class="tool-btn" data-t="calc">🧮 Calculator</button>':'')+
                  (slide.tools.indexOf('desmos')>=0?'<button type="button" class="tool-btn" data-t="desmos">📈 Desmos graph</button>':'');
    card.insertBefore(bar, card.firstChild);
    bar.addEventListener('click',function(e){ var b=e.target.closest('[data-t]'); if(!b) return; if(b.dataset.t==='calc') openCalc(); else openDesmos(slide.desmos||[]); });
  }
  kbWire();
};



/* ================= signed fractions in text: {−3/4}, {3/−4}, {−2 1/3}, {p/q} ================= */
fr = function(s){ return String(s).replace(/&lt;(\/?)(b|sup|sub|i)>/g,'<$1$2>')
  .replace(/\{([−-]?\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>')
  .replace(/\{([−-]?[A-Za-z0-9]+)\/([−-]?[A-Za-z0-9]+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); };
/* ================= BMA badge → main page of this sheet (theory hub) ================= */
(function(){
  var c=document.querySelector('.brand .crest'); if(!c) return;
  var a=document.createElement('button'); a.type='button'; a.className='crest crest-home'; a.title='Back to the main page (theory notes)'; a.setAttribute('aria-label','Main page');
  a.innerHTML='<img src="data:image/png;base64,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" alt="Brain and Mind"><span class="crest-h">⌂</span>'; c.parentNode.replaceChild(a,c);
  a.addEventListener('click',function(){
    if(!student||!MODE){ window.scrollTo({top:0,behavior:'smooth'}); return; }
    if(typeof kbHide==='function') kbHide(); if(typeof SP!=='undefined'&&SP.on) spToggle(false);
    var cp=document.getElementById('calcPanel'); if(cp) cp.classList.remove('show'); document.body.classList.remove('calc-open');
    activeTab = (typeof THEORY!=='undefined') ? 'theory' : TAB_DEFS[0].id;
    buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'});
  });
})();

/* ================= session clock: starts at sign-in and keeps running ================= */
var CLK={t0:null};
(function(){
  var row=document.querySelector('.brand .brand-row'); if(!row) return;
  var d=document.createElement('div'); d.className='bmasw off'; d.id='swBox'; d.title='Time since you signed in';
  d.innerHTML='<span class="bmasw-ic">⏱</span><span class="bmasw-t" id="swT">00:00</span>';
  row.appendChild(d); setInterval(swTick,1000);
})();
function swFmt(s){ s=Math.floor(s||0); var h=Math.floor(s/3600), m=Math.floor(s%3600/60), x=s%60; return (h?h+':'+String(m).padStart(2,'0'):String(m).padStart(2,'0'))+':'+String(x).padStart(2,'0'); }
function swTick(){
  var box=document.getElementById('swBox'); if(!box) return;
  if(student && !CLK.t0) CLK.t0=Date.now();
  if(!student) CLK.t0=null;
  box.classList.toggle('off',!CLK.t0);
  document.getElementById('swT').textContent = CLK.t0 ? swFmt((Date.now()-CLK.t0)/1000) : '00:00';
}
function swTab(){ try{ if(!state||!state.tabs||activeTab==='theory'||activeTab==='report') return null; return state.tabs[activeTab]||null; }catch(e){ return null; } }
var _rsSW = renderSlide;
renderSlide = function(){ _rsSW(); swTick(); };
var _rfSW = renderFinished;
renderFinished = function(){ _rfSW(); var done=document.querySelector('#wrap .done-card'); if(CLK.t0 && done && !done.querySelector('.bmasw-done')){ var p=document.createElement('p'); p.className='bmasw-done'; p.textContent='⏱ Time since sign-in: '+swFmt((Date.now()-CLK.t0)/1000); var h2=done.querySelector('h2'); if(h2) h2.insertAdjacentElement('afterend',p); else done.appendChild(p); } };

/* ================= scratchpad (Khan-style, 4 pens) ================= */
var SP={on:false, draw:true, color:'ink', size:3, erase:false, store:{}, key:null, cv:null, ctx:null, down:false, last:null};
var SP_COL={ink:null, blue:'#2563EB', red:'#DC2626', green:'#16A34A'};
function spInk(){ return getComputedStyle(document.documentElement).getPropertyValue('--ink').trim()||'#211E1A'; }
function spKey(){ var ts=swTab(); return ts ? (MODE+'|'+activeTab+'|'+ts.idx) : null; }
function spBuild(){
  if(SP.cv) return;
  var cv=document.createElement('canvas'); cv.id='spCanvas'; cv.className='sp-canvas'; document.body.appendChild(cv);
  var bar=document.createElement('div'); bar.id='spBar'; bar.className='sp-bar';
  bar.innerHTML='<span class="sp-lbl">✏️ Scratchpad</span>'+
    ['ink','blue','red','green'].map(function(c){ return '<button type="button" class="sp-pen" data-c="'+c+'" title="'+(c==='ink'?'black':c)+' pen"><i style="background:'+(c==='ink'?'var(--ink)':SP_COL[c])+'"></i></button>'; }).join('')+
    '<button type="button" class="sp-tool" data-t="erase" title="Eraser">🧽</button><button type="button" class="sp-tool" data-t="size" title="Pen size">●</button><button type="button" class="sp-tool" data-t="scroll" title="Pause drawing to scroll or answer">✋</button>'+
    '<button type="button" class="sp-tool" data-t="clear" title="Clear page">🗑</button><button type="button" class="sp-tool" data-t="close" title="Close scratchpad">✕</button>';
  document.body.appendChild(bar);
  bar.addEventListener('click',function(e){ var b=e.target.closest('button'); if(!b) return;
    if(b.dataset.c){ SP.color=b.dataset.c; SP.erase=false; SP.draw=true; }
    else if(b.dataset.t==='erase'){ SP.erase=true; SP.draw=true; }
    else if(b.dataset.t==='size'){ SP.size = SP.size===3?6:(SP.size===6?1.5:3); b.textContent = SP.size===6?'⬤':(SP.size===1.5?'·':'●'); }
    else if(b.dataset.t==='scroll'){ SP.draw=!SP.draw; }
    else if(b.dataset.t==='clear'){ spClear(); }
    else if(b.dataset.t==='close'){ spToggle(false); return; }
    spUI(); });
  SP.cv=cv; SP.ctx=cv.getContext('2d');
  cv.addEventListener('pointerdown',function(e){ if(!SP.draw) return; e.preventDefault(); cv.setPointerCapture(e.pointerId); SP.down=true; SP.last=spPt(e); spDot(SP.last); });
  cv.addEventListener('pointermove',function(e){ if(!SP.down) return; e.preventDefault(); var p=spPt(e); spLine(SP.last,p); SP.last=p; });
  var up=function(){ if(SP.down){ SP.down=false; spSave(); } };
  cv.addEventListener('pointerup',up); cv.addEventListener('pointercancel',up); cv.addEventListener('pointerleave',up);
  window.addEventListener('resize',function(){ if(SP.on) spFit(true); });
}
function spPt(e){ var r=SP.cv.getBoundingClientRect(); return {x:e.clientX-r.left, y:e.clientY-r.top}; }
function spStyle(){ var c=SP.ctx; c.lineCap='round'; c.lineJoin='round'; c.globalCompositeOperation=SP.erase?'destination-out':'source-over'; c.strokeStyle=c.fillStyle=(SP.color==='ink'?spInk():SP_COL[SP.color]); c.lineWidth=SP.erase?22:SP.size; }
function spDot(p){ spStyle(); var c=SP.ctx; c.beginPath(); c.arc(p.x,p.y,(SP.erase?11:SP.size/2),0,Math.PI*2); c.fill(); }
function spLine(a,b){ spStyle(); var c=SP.ctx; c.beginPath(); c.moveTo(a.x,a.y); c.lineTo(b.x,b.y); c.stroke(); }
function spSave(){ if(SP.key&&SP.cv){ try{ SP.store[SP.key]=SP.cv.toDataURL(); }catch(e){} } }
function spClear(){ if(!SP.ctx) return; SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.clearRect(0,0,SP.cv.width,SP.cv.height); SP.ctx.restore(); if(SP.key) delete SP.store[SP.key]; }
function spFit(keep){
  var wrap=document.getElementById('wrap'); if(!wrap||!SP.cv) return;
  var r=wrap.getBoundingClientRect(), top=r.top+window.scrollY, h=Math.max(wrap.scrollHeight, window.innerHeight-r.top)+40, w=document.documentElement.clientWidth;
  var old=keep&&SP.key?SP.store[SP.key]:null, dpr=window.devicePixelRatio||1;
  SP.cv.style.top=top+'px'; SP.cv.style.left='0px'; SP.cv.style.width=w+'px'; SP.cv.style.height=h+'px';
  SP.cv.width=Math.round(w*dpr); SP.cv.height=Math.round(h*dpr); SP.ctx.setTransform(dpr,0,0,dpr,0,0);
  if(old){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=old; }
}
function spLoad(){ spSave(); SP.key=spKey(); spFit(false); var d=SP.key&&SP.store[SP.key]; if(d){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=d; } }
function spUI(){
  var bar=document.getElementById('spBar'); if(!bar) return;
  bar.querySelectorAll('.sp-pen').forEach(function(b){ b.classList.toggle('on', !SP.erase && SP.draw && b.dataset.c===SP.color); });
  bar.querySelector('[data-t=erase]').classList.toggle('on', SP.erase && SP.draw);
  bar.querySelector('[data-t=scroll]').classList.toggle('on', !SP.draw);
  SP.cv.classList.toggle('passive', !SP.draw);
  var fb=document.getElementById('spFab'); if(fb) fb.classList.toggle('on',SP.on);
}
function spToggle(on){
  spBuild(); SP.on=(on===undefined)?!SP.on:on;
  document.body.classList.toggle('sp-open',SP.on); SP.cv.style.display=SP.on?'block':'none'; document.getElementById('spBar').style.display=SP.on?'flex':'none';
  if(SP.on){ SP.draw=true; SP.erase=false; spLoad(); if(typeof kbHide==='function') kbHide(); } else { spSave(); }
  spUI();
}
(function(){ var f=document.createElement('button'); f.type='button'; f.id='spFab'; f.className='sp-fab'; f.innerHTML='✏️ <span>Scratchpad</span>'; f.title='Open a scratchpad to write your working'; f.addEventListener('click',function(){ spToggle(); }); document.body.appendChild(f); })();
var _rsSP = renderSlide;
renderSlide = function(){ _rsSP(); var fab=document.getElementById('spFab'); var q=!!swTab(); if(fab) fab.style.display=q?'':'none'; if(!q && SP.on) spToggle(false); if(SP.on) setTimeout(spLoad,30); };


/* ================= v4: attempt classification ================= */
function v4Class(item){
  if(!item) return 'un';
  if(item.status==='skipped') return 'sk';
  if(item.status==='unanswered') return 'un';
  if(item.stepStates){ // step question
    if(item.status!=='correct' && item.status!=='revealed') return 'un';
    if(item.status==='revealed' || item.stepStates.some(function(s){return s.status==='revealed';})) return 'w';
    return item.stepStates.some(function(s){return (s.attempts||0)>0;}) ? 'c2' : 'c1';
  }
  if(item.status==='revealed') return 'w';
  if(item.status==='correct') return (item.attempts||0)>0 ? 'c2' : 'c1';
  if(item.status==='wrong'||item.status==='incorrect') return 'w';
  return 'un';
}
function v4Counts(items){ var c={n:items.length,c1:0,c2:0,w:0,sk:0,un:0}; items.forEach(function(it){ c[v4Class(it)]++; }); return c; }

/* ================= v4: My record with attempt columns ================= */
renderRecord = function(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var title=(document.querySelector('.chapter-title')||{}).textContent||'';
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+(title?' · '+esc(title):'')+'</p>';
  var st=appState.learning;
  h+='<h3>📘 Learning Sheet — attempts</h3><p class="v4leg"><b>1st ✓</b> correct on the first attempt · <b>2nd ✓</b> correct on the second attempt · <b>Wrong</b> still wrong after two attempts (answer revealed) · <b>Skip</b> skipped<span class="v4left"> · <b>Left</b> not done yet</span></p>';
  if(!st){ h+='<p class="rec-empty">Not started yet.</p>'; }
  else {
    var T={n:0,c1:0,c2:0,w:0,sk:0,un:0};
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>Sheet</th><th>Qs</th><th>1st ✓</th><th>2nd ✓</th><th>Wrong</th><th>Skip</th><th class="v4left">Left</th></tr></thead><tbody>';
    TAB_DEFS.forEach(function(td){ var tt=st.tabs[td.id]; if(!tt||!tt.items||!tt.items.length) return; var c=v4Counts(tt.items);
      ['n','c1','c2','w','sk','un'].forEach(function(k){ T[k]+=c[k]; });
      h+='<tr><td>'+td.label+'</td><td>'+c.n+'</td><td class="v4g">'+c.c1+'</td><td class="v4o">'+c.c2+'</td><td class="v4r">'+c.w+'</td><td>'+c.sk+'</td><td class="v4left">'+c.un+'</td></tr>'; });
    h+='<tr class="v4tot"><td>Total</td><td>'+T.n+'</td><td class="v4g">'+T.c1+'</td><td class="v4o">'+T.c2+'</td><td class="v4r">'+T.w+'</td><td>'+T.sk+'</td><td class="v4left">'+T.un+'</td></tr>';
    h+='</tbody></table></div>';
    var doneN=T.c1+T.c2+T.w; if(doneN){ h+='<p class="v4sum">Of '+doneN+' questions answered: <b>'+Math.round(T.c1/doneN*100)+'%</b> right first time, <b>'+Math.round(T.c2/doneN*100)+'%</b> right on the second try, <b>'+Math.round(T.w/doneN*100)+'%</b> still wrong after two tries.</p>'; }
  }
  var q=appState.quiz;
  h+='<h3>📝 Quiz Mode</h3>';
  if(!q){ h+='<p class="rec-empty">Not started yet.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>Sheet</th><th>Qs</th><th>Status</th><th>Correct</th><th>Wrong</th></tr></thead><tbody>';
    TAB_DEFS.forEach(function(td){ var tt=q.tabs[td.id]; if(!tt||!tt.items||!tt.items.length) return; var n=tt.items.length, cor=0, att=0;
      tt.items.forEach(function(it){ if(it.status!=='unanswered'||it.choice!==undefined) att++; });
      var rec=records.filter(function(r){ return r.mode==='quiz'&&r.tab===td.id; })[0];
      if(rec){ cor=rec.correct; att=Math.max(att,rec.total); }
      h+='<tr><td>'+td.label+'</td><td>'+n+'</td><td>'+(rec?'Finished':att+' / '+n)+'</td><td class="v4g">'+(rec?cor:'—')+'</td><td class="v4r">'+(rec?(rec.total-cor):'—')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><div class="rec-card"><h3>Finished sheets (latest first)</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sheets finished yet. Each time you finish a sheet, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>When</th><th>Mode</th><th>Sheet</th><th>Score</th><th>1st ✓</th><th>2nd ✓</th><th>Wrong</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+'</td><td>'+(r.c1!=null?r.c1:'—')+'</td><td>'+(r.c2!=null?r.c2:'—')+'</td><td>'+(r.w!=null?r.w:(r.mode==='quiz'?r.total-r.correct:'—'))+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){ if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker(); });
  window.scrollTo({top:0});
};
var _v4add = addRecord;
addRecord = function(mode, tabId, correct, revealed, skipped, total){
  _v4add(mode, tabId, correct, revealed, skipped, total);
  try{ if(mode==='learning'&&records[0]){ var c=v4Counts(state.tabs[tabId].items); records[0].c1=c.c1; records[0].c2=c.c2; records[0].w=c.w; saveState(); } }catch(e){}
};

/* ================= v4: celebration ================= */
function v4Cracker(){
  var ctx=ensureAudio(); if(!ctx) return; try{ if(ctx.state==='suspended') ctx.resume(); }catch(e){}
  var now=ctx.currentTime;
  function pop(t, vol, dur, hp){
    var len=Math.floor(ctx.sampleRate*dur), buf=ctx.createBuffer(1,len,ctx.sampleRate), d=buf.getChannelData(0);
    for(var i=0;i<len;i++){ d[i]=(Math.random()*2-1)*Math.pow(1-i/len,3); }
    var src=ctx.createBufferSource(); src.buffer=buf;
    var f=ctx.createBiquadFilter(); f.type='highpass'; f.frequency.value=hp;
    var g=ctx.createGain(); g.gain.setValueAtTime(vol,t); g.gain.exponentialRampToValueAtTime(0.001,t+dur);
    src.connect(f); f.connect(g); g.connect(ctx.destination); src.start(t); src.stop(t+dur+0.02);
  }
  pop(now,0.9,0.35,300);                                   // big bang
  for(var k=0;k<14;k++){ pop(now+0.35+Math.random()*1.3, 0.25+Math.random()*0.35, 0.05+Math.random()*0.08, 1500+Math.random()*2500); } // crackles
  [523.25,659.25,783.99,1046.5].forEach(function(fq,i){ var o=ctx.createOscillator(), g=ctx.createGain(); o.type='triangle'; o.frequency.value=fq;
    var t=now+0.15+i*0.12; g.gain.setValueAtTime(0.0001,t); g.gain.exponentialRampToValueAtTime(0.18,t+0.03); g.gain.exponentialRampToValueAtTime(0.001,t+0.5);
    o.connect(g); g.connect(ctx.destination); o.start(t); o.stop(t+0.55); });
}
function v4Confetti(){
  var cv=document.createElement('canvas'); cv.className='v4conf'; document.body.appendChild(cv);
  var W=cv.width=window.innerWidth*(window.devicePixelRatio||1), H=cv.height=window.innerHeight*(window.devicePixelRatio||1), s=(window.devicePixelRatio||1);
  var ctx=cv.getContext('2d'), cols=['#e8b13a','#d9534f','#2e86de','#27ae60','#9b59b6','#f39c12','#1abc9c','#ff6b9a'], P=[];
  function burst(x,y,n){ for(var i=0;i<n;i++){ var a=Math.random()*Math.PI*2, v=(4+Math.random()*9)*s;
    P.push({x:x,y:y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-6*s,w:(6+Math.random()*7)*s,h:(4+Math.random()*5)*s,r:Math.random()*6,vr:(Math.random()-.5)*.4,c:cols[i%cols.length],life:0,flyer:Math.random()<.25}); } }
  burst(W*0.2,H*0.35,90); burst(W*0.8,H*0.35,90); setTimeout(function(){ burst(W*0.5,H*0.25,120); },380); setTimeout(function(){ burst(W*0.35,H*0.3,70); burst(W*0.65,H*0.3,70); },800);
  var t0=performance.now();
  (function frame(t){
    ctx.clearRect(0,0,W,H);
    P.forEach(function(p){ p.vy+=0.22*s; p.vx*=0.985; p.vy*=0.985; p.x+=p.vx; p.y+=p.vy; p.r+=p.vr; p.life++;
      ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.r); ctx.fillStyle=p.c;
      if(p.flyer){ ctx.fillRect(-p.w*1.4,-1.5*s,p.w*2.8,3*s); } else { ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h*Math.abs(Math.cos(p.life/6))); }
      ctx.restore(); });
    if(t-t0<4200) requestAnimationFrame(frame); else cv.remove();
  })(t0);
}
function v4NextTab(){
  var i=TAB_DEFS.findIndex(function(t){return t.id===activeTab;});
  for(var j=i+1;j<TAB_DEFS.length;j++){ var id=TAB_DEFS[j].id; if(id!=='theory' && SLIDES[id] && SLIDES[id].length) return TAB_DEFS[j]; }
  return null;
}
function v4Celebrate(){
  var done=document.querySelector('#wrap .done-card'); if(!done || done.dataset.v4 || done.classList.contains('skip-gate')) return; done.dataset.v4='1';
  var ts=state.tabs[activeTab], c=v4Counts(ts.items), n=ts.items.length;
  var first=(student&&student.name)?String(student.name).split(' ')[0]:'';
  var pct=MODE==='quiz'?null:Math.round((c.c1+c.c2)/Math.max(n,1)*100);
  var msg = pct===null ? 'You finished this sheet!' : (pct>=90?'Outstanding work!':pct>=75?'Excellent effort!':pct>=50?'Well done — keep going!':'Great persistence — every try makes you stronger!');
  var banner=document.createElement('div'); banner.className='v4ban';
  banner.innerHTML='<div class="v4trophy">🏆</div><div class="v4h">Congratulations'+(first?', '+esc(first):'')+'!</div><div class="v4m">'+msg+'</div>'+
    (MODE==='quiz'?'':'<div class="v4pills"><span class="v4p g">✅ '+c.c1+' first attempt</span><span class="v4p o">🔁 '+c.c2+' second attempt</span><span class="v4p r">❌ '+c.w+' finally wrong</span>'+(c.sk?'<span class="v4p s">⏭ '+c.sk+' skipped</span>':'')+'</div>');
  done.insertBefore(banner, done.firstChild);
  var nx=v4NextTab(), wrapB=document.createElement('div'); wrapB.className='v4next';
  if(nx){ wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">Next sheet: '+nx.label+' →</button>'; }
  else if(SLIDES.report!==undefined || TAB_DEFS.some(function(t){return t.id==='report';})){ wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">📊 View my report →</button>'; }
  else { wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">⌂ Back to the home page</button>'; }
  banner.appendChild(wrapB);
  document.getElementById('v4Next').addEventListener('click',function(){
    var t=nx?nx.id:(TAB_DEFS.some(function(x){return x.id==='report';})?'report':(TAB_DEFS[0]&&TAB_DEFS[0].id));
    activeTab=t; showChrome(true); buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  setTimeout(function(){ var r=banner.getBoundingClientRect(); window.scrollBy({top:r.top-110,behavior:'smooth'}); },60);
  v4Confetti(); v4Cracker();
}
var _v4rf = renderFinished;
renderFinished = function(){ _v4rf.apply(this,arguments); try{ v4Celebrate(); }catch(e){ console.log('v4',e); } };


/* ================= v5: inequality plotters ================= */
var PLT={};
function pFrac(s){ s=String(s).trim().replace(/−/g,'-'); if(/^[-+]?∞$|^[-+]?inf$/i.test(s)) return s.charAt(0)==='-'?-Infinity:Infinity;
  var m=s.match(/^([-+]?\d*\.?\d+)\s*\/\s*(\d*\.?\d+)$/); if(m) return parseFloat(m[1])/parseFloat(m[2]); var v=parseFloat(s); return isNaN(v)?null:v; }
function fmtN(v){ if(v===Infinity) return '∞'; if(v===-Infinity) return '−∞'; var r=Math.round(v*1000)/1000; var s=String(r); for(var d=2;d<=12;d++){ var n=Math.round(v*d); if(Math.abs(n/d-v)<1e-9 && Math.abs(n)%d!==0){ s=n+'/'+d; break; } } return s.replace('-','−'); }
/* ---- intervals ---- */
function ivParse(s){ s=String(s||'').trim(); if(!s) return null; if(/^(∅|\{\s*\}|none|empty)$/i.test(s)) return [];
  if(/^(ℝ|R|all real( numbers)?)$/i.test(s)) return [{a:-Infinity,ai:false,b:Infinity,bi:false}];
  var parts=s.split(/\s*(?:∪|U|u|or)\s*/), out=[];
  for(var i=0;i<parts.length;i++){ var m=parts[i].match(/^([\[(])\s*([^,]+?)\s*,\s*([^\])]+?)\s*([\])])$/); if(!m) return null;
    var a=pFrac(m[2]), b=pFrac(m[3]); if(a===null||b===null) return null; out.push({a:a,ai:m[1]==='['&&isFinite(a),b:b,bi:m[4]===']'&&isFinite(b)}); }
  return ivNorm(out); }
function ivNorm(L){ L=L.filter(function(t){ return t.a<t.b||(t.a===t.b&&t.ai&&t.bi); }).sort(function(p,q){ return p.a-q.a||((q.ai?1:0)-(p.ai?1:0)); });
  var o=[]; L.forEach(function(t){ var l=o[o.length-1];
    if(l && (t.a<l.b || (Math.abs(t.a-l.b)<1e-9 && (l.bi||t.ai)))){ if(t.b>l.b||(Math.abs(t.b-l.b)<1e-9&&t.bi)){ l.b=t.b; l.bi=t.bi; } }
    else o.push({a:t.a,ai:t.ai,b:t.b,bi:t.bi}); }); return o; }
function ivEq(x,y){ var A=ivParse(x),B=ivParse(y); if(!A||!B||A.length!==B.length) return false;
  for(var i=0;i<A.length;i++){ var p=A[i],q=B[i]; if(Math.abs(p.a-q.a)>1e-6&&!(p.a===q.a)) return false; if(Math.abs(p.b-q.b)>1e-6&&!(p.b===q.b)) return false; if(p.ai!==q.ai||p.bi!==q.bi) return false; } return true; }
function ivFmt(L){ if(!L.length) return '∅'; return L.map(function(t){ return (t.ai?'[':'(')+fmtN(t.a)+', '+fmtN(t.b)+(t.bi?']':')'); }).join(' ∪ '); }
/* ---- half-planes ---- */
function linParse(side){ side=String(side).replace(/\s+/g,'').replace(/−/g,'-').replace(/\*/g,''); if(!side) side='0';
  if(!/^[-+]/.test(side)) side='+'+side; var re=/([-+])(\(?\d*\.?\d*(?:\/\d*\.?\d+)?\)?)([xy]?)/g, m, r={x:0,y:0,c:0}, used=0;
  while((m=re.exec(side))!==null){ if(m[0]==='') { re.lastIndex++; continue; } used+=m[0].length; var co=m[2].replace(/[()]/g,''); var v=co===''?1:pFrac(co); if(v===null) return null; if(m[1]==='-') v=-v; if(m[3]) r[m[3]]+=v; else { if(co==='') return null; r.c+=v; } }
  if(used!==side.length) return null; return r; }
function hpParse(s){ s=String(s).replace(/<=/g,'≤').replace(/>=/g,'≥'); var m=s.match(/^(.*?)(≤|≥|<|>)(.*)$/); if(!m) return null;
  var L=linParse(m[1]), R=linParse(m[3]); if(!L||!R) return null; var a=L.x-R.x, b=L.y-R.y, c=R.c-L.c, op=m[2];
  if(Math.abs(a)<1e-12&&Math.abs(b)<1e-12) return null; var n=Math.sqrt(a*a+b*b), sg=(Math.abs(a)>1e-12? (a>0?1:-1):(b>0?1:-1));
  a=a/n*sg; b=b/n*sg; c=c/n*sg; if(sg<0) op={'≤':'≥','≥':'≤','<':'>','>':'<'}[op]; return {a:a,b:b,c:c,op:op}; }
function hpList(s){ s=String(s||'').trim(); if(!s) return null; var parts=s.split(/\s*(?:;|,|\band\b)\s*/).filter(Boolean), o=[]; for(var i=0;i<parts.length;i++){ var h=hpParse(parts[i]); if(!h) return null; o.push(h);} return o; }
function hpEq(x,y){ var A=hpList(x),B=hpList(y); if(!A||!B||A.length!==B.length) return false; var used=B.map(function(){return false;});
  return A.every(function(p){ for(var j=0;j<B.length;j++){ var q=B[j]; if(!used[j]&&p.op===q.op&&Math.abs(p.a-q.a)<1e-6&&Math.abs(p.b-q.b)<1e-6&&Math.abs(p.c-q.c)<1e-6){ used[j]=true; return true; } } return false; }); }
function gcd(a,b){ a=Math.abs(a);b=Math.abs(b); while(b){ var t=a%b;a=b;b=t;} return a; }
function hpFmtInt(a,b,c,op){ var g=gcd(gcd(a,b),c)||1; a/=g;b/=g;c/=g; if(a<0||(a===0&&b<0)){ a=-a;b=-b;c=-c; op=({'≤':'≥','≥':'≤','<':'>','>':'<'}[op]||op); }
  function term(k,v,first){ if(!k) return ''; var s=(k<0?(first?'−':' − '):(first?'':' + ')); var m=Math.abs(k); return s+(m===1?'':m)+v; }
  var lhs=term(a,'x',true); lhs+=term(b,'y',lhs===''); return lhs+' '+op+' '+String(c).replace('-','−'); }
/* ---- answer checking ---- */
(function(){ var _am=answerMatches; answerMatches=function(input,answer,accept,expr){
  if(expr==='plot1'||expr==='plot2'){ if(input===undefined||input===null||String(input).trim()==='') return false; var f=expr==='plot1'?ivEq:hpEq;
    return [answer].concat(accept||[]).some(function(a){ return f(input,a); }); }
  return _am.apply(this,arguments); }; })();
/* ---- SVG helpers ---- */
function sv(tag,attrs){ return '<'+tag+' '+Object.keys(attrs).map(function(k){return k+'="'+attrs[k]+'"';}).join(' ')+'/>'; }
/* ---- number-line widget ---- */
function nlEncode(st){ var P=st.pts.slice().sort(function(p,q){return p.v-q.v;}), n=P.length, R=[];
  for(var i=0;i<=n;i++){ R.push({a:i===0?-Infinity:P[i-1].v, b:i===n?Infinity:P[i].v, on:!!st.sh[i]}); }
  var L=[]; R.forEach(function(r,i){ if(r.on) L.push({a:r.a,ai:i>0&&P[i-1].closed,b:r.b,bi:i<n&&P[i].closed}); });
  P.forEach(function(p,i){ if(p.closed && !st.sh[i] && !st.sh[i+1]) L.push({a:p.v,ai:true,b:p.v,bi:true}); });
  var out=[]; L.forEach(function(t){ out.push(t); }); return ivFmt(ivNorm(out)); }
function nlDraw(w){ var st=w._st, lo=st.lo, hi=st.hi, W=340, H=78, x0=22, x1=W-22, y=40, X=function(v){ return x0+(v-lo)/(hi-lo)*(x1-x0); };
  var P=st.pts.slice().sort(function(p,q){return p.v-q.v;}), n=P.length, h='';
  var col='var(--accent-text)';
  for(var i=0;i<=n;i++){ if(!st.sh[i]) continue; var a=i===0?x0-14:X(P[i-1].v), b=i===n?x1+14:X(P[i].v);
    h+=sv('line',{x1:a,y1:y,x2:b,y2:y,style:'stroke:'+col+';stroke-width:7;stroke-linecap:round;opacity:.85'});
    if(i===0) h+='<polygon points="'+(x0-18)+','+y+' '+(x0-6)+','+(y-8)+' '+(x0-6)+','+(y+8)+'" style="fill:'+col+'"/>';
    if(i===n) h+='<polygon points="'+(x1+18)+','+y+' '+(x1+6)+','+(y-8)+' '+(x1+6)+','+(y+8)+'" style="fill:'+col+'"/>'; }
  h=sv('line',{x1:x0-16,y1:y,x2:x1+16,y2:y,style:'stroke:var(--ink);stroke-width:1.6'})+h;
  var every=Math.max(1,Math.ceil((hi-lo)/14));
  for(var v=Math.ceil(lo/st.step)*st.step; v<=hi+1e-9; v+=st.step){ var big=Math.abs(v-Math.round(v))<1e-9; var xx=X(v);
    h+=sv('line',{x1:xx,y1:y-(big?8:4),x2:xx,y2:y+(big?8:4),style:'stroke:var(--ink);stroke-width:'+(big?1.4:1)});
    if(big && Math.round(v)%every===0) h+='<text x="'+xx+'" y="'+(y+24)+'" text-anchor="middle" style="font:13px sans-serif;fill:var(--ink)">'+String(Math.round(v)).replace('-','−')+'</text>'; }
  P.forEach(function(p){ h+=sv('circle',{cx:X(p.v),cy:y,r:7,style:'stroke:'+col+';stroke-width:2.5;fill:'+(p.closed?col:'var(--card)')}); });
  if(st.key){ var K=ivParse(st.key)||[]; K.forEach(function(t){ var a=isFinite(t.a)?X(t.a):x0-14, b=isFinite(t.b)?X(t.b):x1+14;
      h+=sv('line',{x1:a,y1:y-17,x2:b,y2:y-17,style:'stroke:var(--success);stroke-width:5;stroke-linecap:round'});
      if(isFinite(t.a)) h+=sv('circle',{cx:a,cy:y-17,r:5,style:'stroke:var(--success);stroke-width:2;fill:'+(t.ai?'var(--success)':'var(--card)')});
      if(isFinite(t.b)) h+=sv('circle',{cx:b,cy:y-17,r:5,style:'stroke:var(--success);stroke-width:2;fill:'+(t.bi?'var(--success)':'var(--card)')}); }); }
  w.querySelector('.plw-svg').innerHTML='<svg viewBox="0 0 '+W+' '+H+'" style="width:100%;max-width:520px;touch-action:manipulation">'+h+'</svg>';
  w._X=X; w._x0=x0; w._x1=x1; w._W=W; }
function nlTap(w,ev){ var st=w._st; if(st.ro) return; var svg=w.querySelector('svg'), r=svg.getBoundingClientRect(), px=(ev.clientX-r.left)*w._W/r.width;
  var v=st.lo+(px-w._x0)/(w._x1-w._x0)*(st.hi-st.lo), sv_=Math.round(v/st.step)*st.step;
  var near=Math.abs(sv_-v)<st.step*0.28 && sv_>=st.lo-1e-9 && sv_<=st.hi+1e-9;
  if(near){ var idx=-1; st.pts.forEach(function(p,i){ if(Math.abs(p.v-sv_)<1e-9) idx=i; });
    if(idx<0){ st.pts.push({v:Math.round(sv_*1e6)/1e6,closed:true}); st.sh={}; } else if(st.pts[idx].closed){ st.pts[idx].closed=false; } else { st.pts.splice(idx,1); st.sh={}; } }
  else { var P=st.pts.slice().sort(function(p,q){return p.v-q.v;}), i=0; while(i<P.length && P[i].v<v) i++; st.sh[i]=!st.sh[i]; }
  plwSave(w); }
/* ---- grid widget ---- */
function clipPoly(poly,a,b,c,ge){ var out=[], f=function(p){ var s=a*p[0]+b*p[1]-c; return ge? s>=-1e-9 : s<=1e-9; };
  for(var i=0;i<poly.length;i++){ var P=poly[i], Q=poly[(i+1)%poly.length], fp=f(P), fq=f(Q);
    if(fp) out.push(P); if(fp!==fq){ var sp=a*P[0]+b*P[1]-c, sq=a*Q[0]+b*Q[1]-c, t=sp/(sp-sq); out.push([P[0]+t*(Q[0]-P[0]),P[1]+t*(Q[1]-P[1])]); } } return out; }
function grLines(st){ return st.lines.map(function(L){ var a=L.p2[1]-L.p1[1], b=L.p1[0]-L.p2[0], c=a*L.p1[0]+b*L.p1[1]; return {a:a,b:b,c:c,L:L}; }); }
function grEncode(st){ var o=[]; var bad=false; grLines(st).forEach(function(q){ if(!q.L.side){ bad=true; return; } var s=q.a*q.L.side[0]+q.b*q.L.side[1]-q.c; if(Math.abs(s)<1e-9){ bad=true; return; }
    var op=s<0?(q.L.solid?'≤':'<'):(q.L.solid?'≥':'>'); o.push(hpFmtInt(q.a,q.b,q.c,op)); }); return (bad||!o.length)?'':o.join('; '); }
function grDraw(w){ var st=w._st, lo=st.lo, hi=st.hi, W=340, pad=18, S=(W-2*pad)/(hi-lo), X=function(x){return pad+(x-lo)*S;}, Y=function(y){return W-pad-(y-lo)*S;}, h='';
  var box=[[lo,lo],[hi,lo],[hi,hi],[lo,hi]], every=Math.max(1,Math.ceil((hi-lo)/12));
  for(var g=lo; g<=hi; g++){ var ax=(g===0); h+=sv('line',{x1:X(g),y1:Y(lo),x2:X(g),y2:Y(hi),style:'stroke:'+(ax?'var(--ink)':'var(--rule)')+';stroke-width:'+(ax?1.6:1)});
    h+=sv('line',{x1:X(lo),y1:Y(g),x2:X(hi),y2:Y(g),style:'stroke:'+(ax?'var(--ink)':'var(--rule)')+';stroke-width:'+(ax?1.6:1)});
    if(g!==0 && g%every===0 && lo<=0 && hi>=0){ h+='<text x="'+X(g)+'" y="'+(Y(0)+13)+'" text-anchor="middle" style="font:10px sans-serif;fill:var(--ink-soft)">'+String(g).replace('-','−')+'</text>';
      h+='<text x="'+(X(0)-4)+'" y="'+(Y(g)+3)+'" text-anchor="end" style="font:10px sans-serif;fill:var(--ink-soft)">'+String(g).replace('-','−')+'</text>'; } }
  if(lo<=0&&hi>=0){ h+='<text x="'+(X(hi)-2)+'" y="'+(Y(0)-5)+'" text-anchor="end" style="font:italic 13px serif;fill:var(--ink)">x</text><text x="'+(X(0)+6)+'" y="'+(Y(hi)+12)+'" style="font:italic 13px serif;fill:var(--ink)">y</text>'; }
  var Ls=grLines(st), inter=box.slice(), anySide=false, cols=['#2e86de','#e67e22','#8e44ad','#16a085','#c0392b'];
  Ls.forEach(function(q,i){ if(!q.L.side) return; anySide=true; var s=q.a*q.L.side[0]+q.b*q.L.side[1]-q.c, ge=s>0; var pl=clipPoly(box,q.a,q.b,q.c,ge); inter=clipPoly(inter,q.a,q.b,q.c,ge);
    if(pl.length>2) h+='<polygon points="'+pl.map(function(p){return X(p[0])+','+Y(p[1]);}).join(' ')+'" style="fill:'+cols[i%5]+';opacity:.13"/>'; });
  if(anySide && Ls.length>1 && inter.length>2) h+='<polygon points="'+inter.map(function(p){return X(p[0])+','+Y(p[1]);}).join(' ')+'" style="fill:var(--accent-text);opacity:.28"/>';
  if(st.key){ var K=hpList(st.key)||[], kin=box.slice(); K.forEach(function(k){ var ge=(k.op==='≥'||k.op==='>'); kin=clipPoly(kin,k.a,k.b,k.c,ge); });
    if(kin.length>2) h+='<polygon points="'+kin.map(function(p){return X(p[0])+','+Y(p[1]);}).join(' ')+'" style="fill:none;stroke:var(--success);stroke-width:3;stroke-dasharray:2 3"/>'; }
  Ls.forEach(function(q,i){ var seg=clipLine(q.a,q.b,q.c,lo,hi); if(!seg) return;
    h+=sv('line',{x1:X(seg[0][0]),y1:Y(seg[0][1]),x2:X(seg[1][0]),y2:Y(seg[1][1]),style:'stroke:'+cols[i%5]+';stroke-width:'+(i===st.sel?3.4:2.6)+(q.L.solid?'':';stroke-dasharray:8 6')});
    [q.L.p1,q.L.p2].forEach(function(p){ h+=sv('circle',{cx:X(p[0]),cy:Y(p[1]),r:4.5,style:'fill:'+cols[i%5]}); });
    if(q.L.side) h+='<text x="'+X(q.L.side[0])+'" y="'+(Y(q.L.side[1])+5)+'" text-anchor="middle" style="font:bold 15px sans-serif;fill:'+cols[i%5]+'">✓</text>'; });
  if(st.pend) h+=sv('circle',{cx:X(st.pend[0]),cy:Y(st.pend[1]),r:6,style:'fill:none;stroke:var(--danger);stroke-width:2.5'});
  w.querySelector('.plw-svg').innerHTML='<svg viewBox="0 0 '+W+' '+W+'" style="width:100%;max-width:460px;touch-action:manipulation">'+h+'</svg>';
  w._inv=function(px,py){ return [lo+(px-pad)/S, lo+(W-pad-py)/S]; }; w._W=W;
  var list=w.querySelector('.plw-list'); list.innerHTML=st.lines.map(function(L,i){ var q=Ls[i]; var eq=hpFmtInt(q.a,q.b,q.c,'=').replace(' = ',' = ');
    return '<div class="plw-row'+(i===st.sel?' sel':'')+'" data-i="'+i+'"><span class="plw-sw" style="background:'+cols[i%5]+'"></span><span class="plw-eq">'+eq+'</span>'+
      (st.ro?'':'<button type="button" data-a="style">'+(L.solid?'━ solid (≤, ≥)':'┅ dashed (<, >)')+'</button><button type="button" data-a="side">'+(L.side?'🎨 change side':'🎨 shade a side')+'</button><button type="button" data-a="del" aria-label="Delete line">✕</button>')+'</div>'; }).join('');
  var msg=w.querySelector('.plw-msg'); msg.textContent= st.ro?'':(st.pend?'Tap a second grid point on the line.':(st.mode==='side'?'Tap a point in the region you want to keep (not on the line).':(st.lines.length?'Tap two grid points to draw another boundary line, or adjust a line below.':'Tap two grid points to draw the boundary line.'))); }
function clipLine(a,b,c,lo,hi){ var P=[]; if(Math.abs(b)>1e-12){ [lo,hi].forEach(function(x){ var y=(c-a*x)/b; if(y>=lo-1e-9&&y<=hi+1e-9) P.push([x,y]); }); }
  if(Math.abs(a)>1e-12){ [lo,hi].forEach(function(y){ var x=(c-b*y)/a; if(x>=lo-1e-9&&x<=hi+1e-9) P.push([x,y]); }); }
  if(P.length<2) return null; var best=[P[0],P[1]], d=0; for(var i=0;i<P.length;i++) for(var j=i+1;j<P.length;j++){ var dd=Math.hypot(P[i][0]-P[j][0],P[i][1]-P[j][1]); if(dd>d){ d=dd; best=[P[i],P[j]]; } } return best; }
function grTap(w,ev){ var st=w._st; if(st.ro) return; var svg=w.querySelector('svg'), r=svg.getBoundingClientRect(); var p=w._inv((ev.clientX-r.left)*w._W/r.width,(ev.clientY-r.top)*w._W/r.width);
  if(st.mode==='side' && st.sel>=0 && st.lines[st.sel]){ var L=st.lines[st.sel]; var a=L.p2[1]-L.p1[1], b=L.p1[0]-L.p2[0], c=a*L.p1[0]+b*L.p1[1]; if(Math.abs(a*p[0]+b*p[1]-c)/Math.hypot(a,b)<0.15){ return; } L.side=[Math.round(p[0]*100)/100,Math.round(p[1]*100)/100]; st.mode='draw'; plwSave(w); return; }
  var g=[Math.round(p[0]),Math.round(p[1])]; if(g[0]<st.lo||g[0]>st.hi||g[1]<st.lo||g[1]>st.hi) return;
  if(!st.pend){ st.pend=g; grDraw(w); return; } if(g[0]===st.pend[0]&&g[1]===st.pend[1]){ st.pend=null; grDraw(w); return; }
  st.lines.push({p1:st.pend,p2:g,solid:true,side:null}); st.pend=null; st.sel=st.lines.length-1; st.mode='side'; plwSave(w); }
/* ---- wiring ---- */
function plwSave(w){ var st=w._st, enc; if(st.kind==='1d'){ enc=nlEncode(st); nlDraw(w); } else { enc=grEncode(st); grDraw(w); }
  var inp=w._inp; if(inp && !inp.disabled){ inp.value=enc; inp.dispatchEvent(new Event('input',{bubbles:true})); }
  try{ PLT[w._key]=JSON.stringify({pts:st.pts,sh:st.sh,lines:st.lines}); }catch(e){}
  var sm=w.querySelector('.plw-sum'); if(sm) sm.innerHTML= enc? 'Your graph shows: <b>'+esc(enc)+'</b>' : (st.kind==='2d'&&st.lines.length?'Shade a side for every line to finish.':''); }
function plwInit(){ document.querySelectorAll('.plotw').forEach(function(w){ if(w._st) return;
  var figd=w.closest('.fig'), line=figd&&figd.nextElementSibling, inp=line&&line.querySelector('.blank-input'); w._inp=inp||null;
  if(inp){ inp.setAttribute('tabindex','-1'); inp.setAttribute('inputmode','none'); inp.style.cssText='position:absolute;opacity:0;width:1px;height:1px;padding:0;border:0;pointer-events:none;'; }
  var kind=w.dataset.kind, st={kind:kind,lo:parseFloat(w.dataset.lo),hi:parseFloat(w.dataset.hi),step:parseFloat(w.dataset.step||'1'),pts:[],sh:{},lines:[],pend:null,sel:-1,mode:'draw',ro:!!(inp&&inp.disabled),key:null};
  w._st=st; w._key=MODE+'|'+activeTab+'|'+state.tabs[activeTab].idx+'|'+(inp?inp.dataset.step:'')+'|'+(w.dataset.id||'');
  var saved=PLT[w._key]; if(saved){ try{ var o=JSON.parse(saved); st.pts=o.pts||[]; st.sh=o.sh||{}; st.lines=o.lines||[]; }catch(e){} }
  else if(inp && inp.value){ if(kind==='1d'){ (ivParse(inp.value)||[]).forEach(function(t){ /* rebuild from value */ var i0=st.pts.length;
        if(isFinite(t.a)) st.pts.push({v:t.a,closed:t.ai}); if(isFinite(t.b)&&t.b!==t.a) st.pts.push({v:t.b,closed:t.bi}); });
      var P=st.pts.slice().sort(function(p,q){return p.v-q.v;}); st.pts=P; var L=ivParse(inp.value)||[]; for(var i=0;i<=P.length;i++){ var m=(i===0?(P.length?P[0].v-1:0):(i===P.length?P[i-1].v+1:(P[i-1].v+P[i].v)/2)); st.sh[i]=L.some(function(t){ return m>t.a&&m<t.b; }); } } }
  if(st.ro && inp && w.dataset.key){ var ok=(kind==='1d'?ivEq:hpEq)(inp.value,w.dataset.key); if(!ok) st.key=w.dataset.key; }
  if(MODE==='quiz') st.key=null;
  w.innerHTML='<div class="plw-svg"></div>'+(kind==='2d'?'<div class="plw-list"></div><div class="plw-msg"></div>':'<div class="plw-msg">'+(st.ro?'':'Tap a number to place an endpoint (tap again: ● closed → ○ open → remove). Tap a part of the line to shade it.')+'</div>')+
    (st.ro?'':'<div class="plw-tools"><button type="button" data-a="undo">↩ Undo</button><button type="button" data-a="clear">🗑 Clear</button></div>')+'<div class="plw-sum"></div>'+(st.key?'<div class="plw-key">Correct graph shown in <b style="color:var(--success)">green</b>: '+esc(w.dataset.key)+'</div>':'');
  w._hist=[];
  w.addEventListener('click',function(ev){ var b=ev.target.closest('button[data-a]'); if(!b) return; ev.preventDefault(); var a=b.dataset.a;
    if(a==='clear'){ st.pts=[]; st.sh={}; st.lines=[]; st.pend=null; st.sel=-1; st.mode='draw'; plwSave(w); return; }
    if(a==='undo'){ if(kind==='1d'){ st.pts.pop(); st.sh={}; } else { if(st.pend) st.pend=null; else st.lines.pop(); st.sel=st.lines.length-1; st.mode='draw'; } plwSave(w); return; }
    var row=b.closest('.plw-row'); if(!row) return; var i=parseInt(row.dataset.i,10); st.sel=i;
    if(a==='style'){ st.lines[i].solid=!st.lines[i].solid; plwSave(w); }
    if(a==='side'){ st.mode='side'; grDraw(w); }
    if(a==='del'){ st.lines.splice(i,1); st.sel=st.lines.length-1; st.mode='draw'; plwSave(w); } });
  w.querySelector('.plw-svg').addEventListener('click',function(ev){ if(kind==='1d') nlTap(w,ev); else grTap(w,ev); });
  if(kind==='1d') nlDraw(w); else grDraw(w); plwSave0(w); }); }
function plwSave0(w){ var st=w._st, enc=st.kind==='1d'?nlEncode(st):grEncode(st); var sm=w.querySelector('.plw-sum'); if(sm&&enc&&(st.pts.length||st.lines.length)) sm.innerHTML='Your graph shows: <b>'+esc(enc)+'</b>'; }
(function(){ var _rs=renderSlide; renderSlide=function(){ _rs.apply(this,arguments); try{ if(document.querySelector('#wrap .plotw')){ plwInit();
  var sl=SLIDES[activeTab][state.tabs[activeTab].idx]; if(sl&&sl.flat&&sl.flat.every(function(s){ return !s.expr||s.expr==='plot1'||s.expr==='plot2'; })) document.querySelectorAll('#wrap .quiz-hint').forEach(function(q){ if(/Type expressions/.test(q.textContent)) q.remove(); }); } }catch(e){ console.log('plot',e); } }; })();


/* ================= v6: helpers ================= */
function v6Correct(tab,i){ var it=state.tabs[tab].items[i]; if(MODE==='quiz'){ try{ return isSlideCorrect(tab,i); }catch(e){ return false; } } var c=v4Class(it); return c==='c1'||c==='c2'; }
function v6Stats(tab){ var ts=state.tabs[tab]; if(!ts||!ts.items) return null; var sl=SLIDES[tab]||[], o={n:ts.items.length,ans:0,ok:0,c1:0,c2:0,w:0,sk:0,wrong:[],byKind:{mcq:[0,0],step:[0,0],plot:[0,0]},stepFail:{first:0,mid:0,last:0}};
  ts.items.forEach(function(it,i){ var s=sl[i]||{}, kind=s.kind==='mcq'||s.kind==='ar'?'mcq':((s.flat||[]).some(function(f){return f.expr==='plot1'||f.expr==='plot2';})?'plot':'step');
    if(MODE==='quiz'){ var att=false; try{ att=isSlideAttempted(tab,i); }catch(e){} if(!att) return; o.ans++; var ok=v6Correct(tab,i); if(ok) o.ok++; else o.wrong.push(i); o.byKind[kind][0]++; if(ok) o.byKind[kind][1]++; return; }
    var c=v4Class(it); if(c==='un') return; if(c==='sk'){ o.sk++; return; } o.ans++; o.byKind[kind][0]++;
    if(c==='c1'){ o.c1++; o.ok++; o.byKind[kind][1]++; } else if(c==='c2'){ o.c2++; o.ok++; o.byKind[kind][1]++; } else { o.w++; o.wrong.push(i); }
    if(it.stepStates&&it.stepStates.length>1){ var L=it.stepStates.length; it.stepStates.forEach(function(ss,k){ if(ss.status==='revealed'||(ss.attempts||0)>0){ if(k===0) o.stepFail.first++; else if(k===L-1) o.stepFail.last++; else o.stepFail.mid++; } }); } });
  o.acc=o.ans?Math.round(o.ok/o.ans*100):null; o.first=o.ans?Math.round(o.c1/o.ans*100):null; return o; }
function v6Qtabs(){ return TAB_DEFS.filter(function(t){ return SLIDES[t.id]&&SLIDES[t.id].length; }); }

/* ================= v6: accuracy meter ================= */
(function(){ var sp=document.querySelector('.slide-progress'); if(!sp) return; var m=document.createElement('div'); m.id='accMeter'; m.className='accm'; sp.parentNode.insertBefore(m, sp.nextSibling); })();
function v6Gauge(p){ var r=26, cx=32, cy=32, a=Math.PI*(1-(p||0)/100), x=cx+r*Math.cos(a), y=cy-r*Math.sin(a), col=p===null?'var(--rule)':(p>=75?'var(--success)':p>=50?'var(--gold)':'var(--danger)');
  return '<svg viewBox="0 0 64 38" class="accg"><path d="M6 32 A26 26 0 0 1 58 32" style="fill:none;stroke:var(--rule);stroke-width:7;stroke-linecap:round"/>'+(p?'<path d="M6 32 A26 26 0 0 1 '+x.toFixed(1)+' '+y.toFixed(1)+'" style="fill:none;stroke:'+col+';stroke-width:7;stroke-linecap:round"/>':'')+
    '<line x1="32" y1="32" x2="'+(cx+20*Math.cos(a)).toFixed(1)+'" y2="'+(cy-20*Math.sin(a)).toFixed(1)+'" style="stroke:var(--ink);stroke-width:2.5;stroke-linecap:round"/><circle cx="32" cy="32" r="3.5" style="fill:var(--ink)"/></svg>'; }
function v6Meter(){ var m=document.getElementById('accMeter'); if(!m) return; var tab=activeTab, sl=SLIDES[tab];
  if(!MODE||!sl||!sl.length||!state.tabs[tab]){ m.style.display='none'; return; } m.style.display='';
  var o=v6Stats(tab); var all={ans:0,ok:0}; v6Qtabs().forEach(function(t){ var s=v6Stats(t.id); if(s){ all.ans+=s.ans; all.ok+=s.ok; } });
  var chap=all.ans?Math.round(all.ok/all.ans*100):null;
  if(MODE==='quiz'){ m.innerHTML=v6Gauge(null)+'<div class="acct"><b>🎯 Accuracy</b><span>Quiz mode: answered '+o.ans+' of '+o.n+' — your accuracy appears when you finish this sheet.</span></div>'; return; }
  var p=o.acc, lab=p===null?'—':p+'%', col=p===null?'':(p>=75?'g':p>=50?'o':'r');
  m.innerHTML=v6Gauge(p)+'<div class="acct"><b>🎯 Accuracy <span class="accp '+col+'">'+lab+'</span></b><span>'+(o.ans?o.ok+' of '+o.ans+' right · '+o.c1+' on the first try':'Answer a question to start the meter')+(chap!==null?' · Chapter '+chap+'%':'')+'</span></div>'; }
(function(){ var _rs=renderSlide; renderSlide=function(){ _rs.apply(this,arguments); try{ v6Meter(); }catch(e){} }; })();
(function(){ var _sc=showChrome; showChrome=function(show){ _sc(show); var m=document.getElementById('accMeter'); if(m&&!show) m.style.display='none'; }; })();

/* ================= v6: observations on the finished card ================= */
function v6NoteFor(tab){ var b=null, sec=null; try{ var tmp=document.createElement('div'); tmp.innerHTML=(typeof THEORY!=='undefined'?THEORY:''); b=tmp.querySelector('section [data-go="'+tab+'"]'); }catch(e){}
  if(b) sec=b.closest('section'); return sec&&sec.id?sec.id:null; }
function v6Observe(){ var done=document.querySelector('#wrap .done-card'); if(!done||done.dataset.v6||done.classList.contains('skip-gate')) return; done.dataset.v6='1';
  var tab=activeTab, o=v6Stats(tab); if(!o||!o.ans) return; var first=(student&&student.name)?String(student.name).split(' ')[0]:'You';
  var tdef=TAB_DEFS.find(function(t){return t.id===tab;})||{label:''}, acc=o.acc, lvl, lvlc;
  if(acc>=90){ lvl='Excellent understanding — this topic is mastered'; lvlc='g'; } else if(acc>=75){ lvl='Strong understanding — just a few points to polish'; lvlc='g'; } else if(acc>=50){ lvl='Developing understanding — the basics are in place'; lvlc='o'; } else { lvl='Building understanding — a little more practice will make it click'; lvlc='r'; }
  var pos=[], grow=[], rev=[];
  // positive diagnostic remarks
  if(MODE!=='quiz' && o.first>=70) pos.push('Your first-try accuracy of <b>'+o.first+'%</b> shows you understood the method before checking.');
  if(MODE!=='quiz' && o.c2>0) pos.push('You corrected <b>'+o.c2+'</b> answer'+(o.c2>1?'s':'')+' on the second try — spotting and fixing your own mistakes is a great habit.');
  var K={mcq:'multiple-choice reasoning',step:'step-by-step working',plot:'plotting graphs'}, best=null, worst=null;
  Object.keys(o.byKind).forEach(function(k){ var v=o.byKind[k]; if(v[0]<2) return; var r=v[1]/v[0]; if(!best||r>best.r) best={k:k,r:r}; if(!worst||r<worst.r) worst={k:k,r:r}; });
  if(best && best.r>=0.6) pos.push('A real strength: <b>'+K[best.k]+'</b> ('+Math.round(best.r*100)+'% correct).');
  if(o.sk===0 && o.ans===o.n) pos.push('You attempted every question in the sheet — excellent persistence.');
  if(acc>=90) pos.push('You are ready to move on to the next sheet with confidence.');
  if(!pos.length) pos.push('You finished the whole sheet, '+esc(first)+' — finishing is the first step to mastering it. Every question you worked through added to your understanding.');
  // growth areas
  if(worst && best && worst.k!==best.k && worst.r<0.6) grow.push('Practise more <b>'+K[worst.k]+'</b> ('+Math.round(worst.r*100)+'% correct so far).');
  var sf=o.stepFail, tot=sf.first+sf.mid+sf.last; if(MODE!=='quiz' && tot>=2){ var mx=Math.max(sf.first,sf.mid,sf.last);
    if(mx===sf.first) grow.push('Most slips happened in the <b>first step</b> — re-read the question and set up the method carefully before calculating.');
    else if(mx===sf.last) grow.push('Most slips happened in the <b>final step</b> — the method was right; check the last simplification or rounding.');
    else grow.push('Most slips happened in the <b>middle steps</b> — write each line of working fully and check signs and arithmetic.'); }
  if(o.wrong.length) grow.push('Have another look at '+(o.wrong.length>1?'these questions':'this question')+': '+o.wrong.slice(0,10).map(function(i){ return '<button type="button" class="v6q" data-q="'+i+'">Q'+(i+1)+'</button>'; }).join(' ')+(o.wrong.length>10?' …':''));
  if(o.sk) grow.push('Come back to the <b>'+o.sk+'</b> skipped question'+(o.sk>1?'s':'')+' when you are ready.');
  // review suggestions
  var nid=v6NoteFor(tab); if(acc<75 && nid) rev.push('<button type="button" class="v6r" data-n="'+nid+'">📖 Re-read the notes for '+esc(tdef.label)+'</button>');
  var tabs=v6Qtabs(), ci=tabs.findIndex(function(t){return t.id===tab;}), weakPrev=[];
  for(var j=0;j<ci;j++){ var t=tabs[j]; if(/^Assessment|Test|Report/i.test(t.label)) continue; var s=v6Stats(t.id); if(s&&s.ans&&s.acc<60) weakPrev.push({t:t,a:s.acc}); else if(acc<60 && j===ci-1 && (!s||!s.ans)) weakPrev.push({t:t,a:null}); }
  weakPrev.slice(-3).forEach(function(w){ rev.push('<button type="button" class="v6t" data-t="'+w.t.id+'">🔁 Review '+esc(w.t.label)+(w.a!==null?' (you scored '+w.a+'%)':' (not attempted yet)')+'</button>'); });
  var revTxt = rev.length? '<div class="v6sub">Suggested review</div><div class="v6btns">'+rev.join('')+'</div>' : '<div class="v6sub">Suggested review</div><p class="v6p">'+(acc>=75?'No earlier topics need review — you are ready for the next sheet.':'Re-try the questions above, then move on.')+'</p>';
  var box=document.createElement('div'); box.className='v6obs';
  box.innerHTML='<div class="v6h">📝 Teacher’s observations</div><div class="v6lvl '+lvlc+'">'+lvl+' · <b>'+acc+'%</b> accuracy</div>'+
    '<div class="v6sub">What went well</div><ul class="v6ul">'+pos.map(function(x){return '<li>'+x+'</li>';}).join('')+'</ul>'+
    (grow.length?'<div class="v6sub">Next steps</div><ul class="v6ul">'+grow.map(function(x){return '<li>'+x+'</li>';}).join('')+'</ul>':'')+revTxt;
  var ban=done.querySelector('.v4ban'); if(ban&&ban.nextSibling) done.insertBefore(box, ban.nextSibling); else done.appendChild(box);
  box.addEventListener('click',function(ev){ var b=ev.target.closest('button'); if(!b) return;
    if(b.dataset.q!==undefined){ var ts=state.tabs[tab]; ts.idx=parseInt(b.dataset.q,10); ts.recorded=false; showChrome(true); buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }
    else if(b.dataset.t){ activeTab=b.dataset.t; showChrome(true); buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }
    else if(b.dataset.n){ var th=TAB_DEFS.find(function(t){return t.id==='theory';}); if(th){ activeTab='theory'; showChrome(true); buildTabbar(); renderSlide(); setTimeout(function(){ var el=document.getElementById(b.dataset.n); if(el) el.scrollIntoView({behavior:'smooth',block:'start'}); },80); } } });
  try{ if(records[0]&&records[0].tab===tab){ records[0].obs=lvl.split(' — ')[0]; saveState(); } }catch(e){}
}
(function(){ var _rf=renderFinished; renderFinished=function(){ _rf.apply(this,arguments); try{ v6Observe(); }catch(e){ console.log('v6',e); } }; })();

/* ================= v6: whiteboard ================= */
var WB={on:false,pages:[[]],pg:0,tool:'pen',color:'#1f2937',size:4,bg:'grid',redo:[],cur:null,cv:null,ctx:null,w0:0};
var WB_COLS=['#1f2937','#2563eb','#dc2626','#16a34a','#ea580c','#9333ea','#db2777','#ffffff'];
function wbKey(){ try{ return 'sopaan-wb::'+document.title+'::'+(student?student.name+'#'+student.roll:'')+'::'+MODE+'|'+activeTab+'|'+((state.tabs[activeTab]||{}).idx||0); }catch(e){ return 'sopaan-wb'; } }
function wbLoad(){ WB.pages=[[]]; WB.pg=0; WB.redo=[]; WB.w0=0; try{ var s=localStorage.getItem(wbKey()); if(s){ var o=JSON.parse(s); if(o&&o.pages){ WB.pages=o.pages; WB.pg=Math.min(o.pg||0,WB.pages.length-1); WB.bg=o.bg||'grid'; WB.w0=o.w0||0; } } }catch(e){} }
function wbStore(){ try{ localStorage.setItem(wbKey(), JSON.stringify({pages:WB.pages,pg:WB.pg,bg:WB.bg,w0:WB.w0})); }catch(e){} }
function wbBuild(){ if(document.getElementById('wbOv')) return; var d=document.createElement('div'); d.id='wbOv'; d.className='wbov';
  var tools=[['pen','✏️','Pen'],['hl','🖍️','Highlighter'],['er','🧽','Eraser'],['line','／','Line'],['arrow','➚','Arrow'],['rect','▭','Rectangle'],['ell','◯','Circle'],['text','T','Text']];
  d.innerHTML='<div class="wbbar"><button type="button" data-a="close" class="wbx" title="Close">✕ Close</button><span class="wbsep"></span>'+tools.map(function(t){ return '<button type="button" class="wbt" data-tool="'+t[0]+'" title="'+t[2]+'">'+t[1]+'</button>'; }).join('')+
    '<span class="wbsep"></span>'+WB_COLS.map(function(c){ return '<button type="button" class="wbc" data-col="'+c+'" style="background:'+c+'" title="Colour"></button>'; }).join('')+
    '<span class="wbsep"></span><input type="range" min="1" max="24" value="4" class="wbsz" title="Size"><span class="wbsep"></span>'+
    '<button type="button" data-a="undo" title="Undo">↶</button><button type="button" data-a="redo" title="Redo">↷</button><button type="button" data-a="bg" title="Background">▦</button><button type="button" data-a="clear" title="Clear page">🗑</button>'+
    '<span class="wbsep"></span><button type="button" data-a="prev" title="Previous page">◀</button><span class="wbpg"></span><button type="button" data-a="next" title="Next / new page">▶</button>'+
    '<span class="wbsep"></span><button type="button" data-a="save" title="Save as picture">💾</button></div><div class="wbbody"><div class="wbq"><div class="wbqh"><b>📌 Question</b><button type="button" class="wbqt">Hide question</button></div><div class="wbqc"></div></div><canvas class="wbcv"></canvas></div>';
  document.body.appendChild(d); d.querySelector('.wbqt').addEventListener('click',function(){ var q=d.querySelector('.wbq'); q.classList.toggle('min'); this.textContent=q.classList.contains('min')?'Show question':'Hide question'; setTimeout(function(){ wbSize(); wbDraw(); },20); });
  WB.cv=d.querySelector('canvas.wbcv'); WB.ctx=WB.cv.getContext('2d');
  d.querySelector('.wbbar').addEventListener('click',function(ev){ var b=ev.target.closest('button'); if(!b) return;
    if(b.dataset.tool){ WB.tool=b.dataset.tool; wbUI(); return; } if(b.dataset.col){ WB.color=b.dataset.col; wbUI(); return; }
    var a=b.dataset.a, P=WB.pages[WB.pg];
    if(a==='undo'&&P.length){ WB.redo.push(P.pop()); } else if(a==='redo'&&WB.redo.length){ P.push(WB.redo.pop()); } else if(a==='clear'&&P.length){ WB.pages[WB.pg]=[]; WB.redo=[]; }
    else if(a==='bg'){ WB.bg={grid:'lines',lines:'plain',plain:'grid'}[WB.bg]; } else if(a==='prev'&&WB.pg>0){ WB.pg--; WB.redo=[]; } else if(a==='next'){ WB.pg++; if(WB.pg>=WB.pages.length) WB.pages.push([]); WB.redo=[]; }
    else if(a==='save'){ try{ var l=document.createElement('a'); l.download='whiteboard-page-'+(WB.pg+1)+'.png'; l.href=wbExport(); l.click(); }catch(e){} }
    else if(a==='close'){ wbToggle(false); return; }
    wbStore(); wbDraw(); wbUI(); });
  d.querySelector('.wbsz').addEventListener('input',function(){ WB.size=parseInt(this.value,10); });
  var cv=WB.cv; cv.addEventListener('pointerdown',wbDown); cv.addEventListener('pointermove',wbMove); cv.addEventListener('pointerup',wbUp); cv.addEventListener('pointercancel',wbUp);
  window.addEventListener('resize',function(){ if(WB.on){ wbSize(); wbDraw(); } }); }
function wbUI(){ var d=document.getElementById('wbOv'); if(!d) return; d.querySelectorAll('.wbt').forEach(function(b){ b.classList.toggle('on',b.dataset.tool===WB.tool); }); d.querySelectorAll('.wbc').forEach(function(b){ b.classList.toggle('on',b.dataset.col===WB.color); }); d.querySelector('.wbpg').textContent=(WB.pg+1)+' / '+WB.pages.length; }
function wbSize(){ var cv=WB.cv, r=cv.getBoundingClientRect(), dpr=window.devicePixelRatio||1; cv.width=Math.round(r.width*dpr); cv.height=Math.round(r.height*dpr); WB.ctx.setTransform(dpr,0,0,dpr,0,0); if(!WB.w0) WB.w0=r.width; WB.sc=r.width/WB.w0; }
function wbP(e){ var r=WB.cv.getBoundingClientRect(); return [(e.clientX-r.left)/WB.sc,(e.clientY-r.top)/WB.sc]; }
function wbDown(e){ e.preventDefault(); var p=wbP(e);
  if(WB.tool==='text'){ wbText(p); return; } WB.cv.setPointerCapture(e.pointerId);
  WB.cur={t:WB.tool,c:WB.color,s:WB.tool==='hl'?Math.max(12,WB.size*3):(WB.tool==='er'?Math.max(18,WB.size*4):WB.size),pts:[p],a:p,b:p}; }
function wbMove(e){ if(!WB.cur) return; var p=wbP(e); if(WB.cur.t==='pen'||WB.cur.t==='hl'||WB.cur.t==='er') WB.cur.pts.push(p); else WB.cur.b=p; wbDraw(); }
function wbUp(){ if(!WB.cur) return; WB.pages[WB.pg].push(WB.cur); WB.cur=null; WB.redo=[]; wbStore(); wbDraw(); }
function wbText(p){ var d=document.getElementById('wbOv'), r=WB.cv.getBoundingClientRect(); var inp=document.createElement('input'); inp.className='wbin'; inp.placeholder='Type, then Enter';
  inp.style.left=(r.left+p[0]*WB.sc)+'px'; inp.style.top=(r.top+p[1]*WB.sc-14)+'px'; inp.style.color=WB.color; d.appendChild(inp); inp.focus(); setTimeout(function(){ inp.focus(); },60);
  var fin=function(){ if(inp._d) return; inp._d=1; var v=inp.value.trim(); inp.remove(); if(v){ WB.pages[WB.pg].push({t:'text',c:WB.color,s:Math.max(24,WB.size*5),a:p,str:v}); WB.redo=[]; wbStore(); wbDraw(); } };
  inp.addEventListener('keydown',function(ev){ if(ev.key==='Enter') fin(); if(ev.key==='Escape'){ inp.value=''; fin(); } }); setTimeout(function(){ inp.addEventListener('blur',fin); },300); }
function wbShape(c,o){ var k=WB.sc; c.save(); c.lineCap='round'; c.lineJoin='round'; c.strokeStyle=c.fillStyle=o.c; c.lineWidth=o.s*k; c.globalAlpha=o.t==='hl'?0.35:1; c.globalCompositeOperation=o.t==='er'?'destination-out':'source-over';
  if(o.t==='pen'||o.t==='hl'||o.t==='er'){ c.beginPath(); o.pts.forEach(function(p,i){ if(i) c.lineTo(p[0]*k,p[1]*k); else c.moveTo(p[0]*k,p[1]*k); }); if(o.pts.length===1) c.lineTo(o.pts[0][0]*k+0.1,o.pts[0][1]*k); c.stroke(); }
  else if(o.t==='line'||o.t==='arrow'){ c.beginPath(); c.moveTo(o.a[0]*k,o.a[1]*k); c.lineTo(o.b[0]*k,o.b[1]*k); c.stroke(); if(o.t==='arrow'){ var an=Math.atan2(o.b[1]-o.a[1],o.b[0]-o.a[0]), h=(10+o.s*2)*k; c.beginPath(); c.moveTo(o.b[0]*k,o.b[1]*k); c.lineTo(o.b[0]*k-h*Math.cos(an-0.45),o.b[1]*k-h*Math.sin(an-0.45)); c.lineTo(o.b[0]*k-h*Math.cos(an+0.45),o.b[1]*k-h*Math.sin(an+0.45)); c.closePath(); c.fill(); } }
  else if(o.t==='rect'){ c.strokeRect(o.a[0]*k,o.a[1]*k,(o.b[0]-o.a[0])*k,(o.b[1]-o.a[1])*k); }
  else if(o.t==='ell'){ c.beginPath(); c.ellipse((o.a[0]+o.b[0])/2*k,(o.a[1]+o.b[1])/2*k,Math.abs(o.b[0]-o.a[0])/2*k,Math.abs(o.b[1]-o.a[1])/2*k,0,0,Math.PI*2); c.stroke(); }
  else if(o.t==='text'){ c.font=(o.s*k)+'px "Source Sans 3",sans-serif'; c.textBaseline='middle'; c.fillText(o.str,o.a[0]*k,o.a[1]*k); }
  c.restore(); }
function wbBg(c,W,H,bg){ c.fillStyle='#ffffff'; c.fillRect(0,0,W,H); if(bg==='plain') return; c.strokeStyle=bg==='grid'?'#e5e7eb':'#dbeafe'; c.lineWidth=1; var g=28*WB.sc; c.beginPath(); for(var y=g;y<H;y+=g){ c.moveTo(0,y); c.lineTo(W,y); } if(bg==='grid') for(var x=g;x<W;x+=g){ c.moveTo(x,0); c.lineTo(x,H); } c.stroke(); }
function wbDraw(){ var c=WB.ctx, r=WB.cv.getBoundingClientRect(), W=r.width, H=r.height; c.clearRect(0,0,W,H);
  var ink=document.createElement('canvas'), dpr=window.devicePixelRatio||1; ink.width=WB.cv.width; ink.height=WB.cv.height; var ic=ink.getContext('2d'); ic.setTransform(dpr,0,0,dpr,0,0);
  WB.pages[WB.pg].concat(WB.cur?[WB.cur]:[]).forEach(function(o){ wbShape(ic,o); });
  wbBg(c,W,H,WB.bg); c.save(); c.setTransform(1,0,0,1,0,0); c.drawImage(ink,0,0); c.restore(); }
function wbExport(){ return WB.cv.toDataURL('image/png'); }
function wbFillQ(){ var d=document.getElementById('wbOv'); if(!d) return; var box=d.querySelector('.wbq'), c=d.querySelector('.wbqc'), q=document.querySelector('#wrap .qcard');
  if(!q){ box.style.display='none'; return; } box.style.display='';
  var cl=q.cloneNode(true); cl.removeAttribute('id'); cl.querySelectorAll('[id]').forEach(function(e){ e.removeAttribute('id'); });
  cl.querySelectorAll('input,button,select,textarea').forEach(function(e){ e.setAttribute('tabindex','-1'); e.disabled=true; });
  cl.querySelectorAll('.feedback,.step-badge,.quiz-hint,.plw-tools,.plw-msg').forEach(function(e){ e.remove(); });
  cl.querySelectorAll('canvas').forEach(function(e){ e.remove(); });
  c.innerHTML=''; c.appendChild(cl); var tdef=(TAB_DEFS.find(function(t){return t.id===activeTab;})||{}).label||''; var h=d.querySelector('.wbqh b'); if(h) h.textContent='📌 '+tdef+' · Question '+(((state.tabs[activeTab]||{}).idx||0)+1); }
function wbToggle(on){ WB.on=(on===undefined)?!WB.on:on; wbBuild(); var d=document.getElementById('wbOv'); d.classList.toggle('show',WB.on); document.body.classList.toggle('wb-open',WB.on);
  if(WB.on){ wbLoad(); wbFillQ(); setTimeout(function(){ wbSize(); wbDraw(); wbUI(); },30); } }
(function(){ var f=document.createElement('button'); f.type='button'; f.id='wbFab'; f.className='wb-fab'; f.innerHTML='🧑‍🏫 <span>Whiteboard</span>'; f.title='Open the whiteboard'; f.addEventListener('click',function(){ wbToggle(true); }); document.body.appendChild(f); })();
(function(){ var _rs=renderSlide; renderSlide=function(){ _rs.apply(this,arguments); var f=document.getElementById('wbFab'); if(f) f.style.display=MODE?'':'none'; }; })();


/* ================= v7: scatter-graph plotter ================= */
var SCT={};
function scPts(s){ s=String(s||'').trim(); if(!s) return []; return s.split(/\s*;\s*/).filter(Boolean).map(function(p){ var a=p.replace(/[()]/g,'').split(/\s*,\s*/); return [parseFloat(a[0]),parseFloat(a[1])]; }).filter(function(p){ return isFinite(p[0])&&isFinite(p[1]); }); }
function scEqPts(inp,key,tolx,toly){ var A=scPts(inp),B=scPts(key); if(!A.length||A.length!==B.length) return false; var used=B.map(function(){return false;});
  return A.every(function(p){ for(var j=0;j<B.length;j++){ if(!used[j]&&Math.abs(p[0]-B[j][0])<=tolx+1e-9&&Math.abs(p[1]-B[j][1])<=toly+1e-9){ used[j]=true; return true; } } return false; }); }
function scLine(s){ var m=String(s||'').match(/^line:\(([^,]+),([^)]+)\)-\(([^,]+),([^)]+)\)/); if(!m) return null; var x1=+m[1],y1=+m[2],x2=+m[3],y2=+m[4]; if(Math.abs(x2-x1)<1e-9) return null; var k=(y2-y1)/(x2-x1); return {m:k,c:y1-k*x1}; }
(function(){ var _am=answerMatches; answerMatches=function(input,answer,accept,expr){
  if(expr==='spts'||expr==='slbf'){ if(input===undefined||input===null||String(input).trim()==='') return false;
    var meta=String((accept&&accept[0])||''); var mm=meta.match(/tol:([\d.]+),([\d.]+)/), tx=mm?+mm[1]:0.5, ty=mm?+mm[2]:0.5;
    if(expr==='spts') return scEqPts(input,answer,tx,ty);
    if(String(input).trim()===String(answer).trim()) return true;
    var L=scLine(input), k=String(answer).split(','), m=+k[0], c=+k[1], tol=+k[2], xa=+k[3], xb=+k[4]; if(!L) return false;
    return [xa,xb].every(function(x){ return Math.abs((L.m*x+L.c)-(m*x+c))<=tol; }); }
  return _am.apply(this,arguments); }; })();
function scDraw(w){ var st=w._st, W=360, H=300, L=52, R=14, T=14, B=44, X=function(x){ return L+(x-st.xlo)/(st.xhi-st.xlo)*(W-L-R); }, Y=function(y){ return H-B-(y-st.ylo)/(st.yhi-st.ylo)*(H-T-B); }, h='';
  function line(x1,y1,x2,y2,sty){ return '<line x1="'+x1.toFixed(1)+'" y1="'+y1.toFixed(1)+'" x2="'+x2.toFixed(1)+'" y2="'+y2.toFixed(1)+'" style="'+sty+'"/>'; }
  var fmt=function(v){ var a=Math.abs(v); return (a>=10000? (v/1000)+'k' : String(Math.round(v*100)/100)).replace('-','−'); };
  if(st.xminor) for(var x=st.xlo;x<=st.xhi+1e-9;x+=st.xminor) h+=line(X(x),Y(st.ylo),X(x),Y(st.yhi),'stroke:var(--rule);stroke-width:.6');
  if(st.yminor) for(var y=st.ylo;y<=st.yhi+1e-9;y+=st.yminor) h+=line(X(st.xlo),Y(y),X(st.xhi),Y(y),'stroke:var(--rule);stroke-width:.6');
  for(var x2=st.xlo;x2<=st.xhi+1e-9;x2+=st.xstep){ h+=line(X(x2),Y(st.ylo),X(x2),Y(st.yhi),'stroke:var(--rule);stroke-width:1.2'); h+='<text x="'+X(x2).toFixed(1)+'" y="'+(H-B+15)+'" text-anchor="middle" style="font:11px sans-serif;fill:var(--ink-soft)">'+fmt(x2)+'</text>'; }
  for(var y2=st.ylo;y2<=st.yhi+1e-9;y2+=st.ystep){ h+=line(X(st.xlo),Y(y2),X(st.xhi),Y(y2),'stroke:var(--rule);stroke-width:1.2'); h+='<text x="'+(L-5)+'" y="'+(Y(y2)+4).toFixed(1)+'" text-anchor="end" style="font:11px sans-serif;fill:var(--ink-soft)">'+fmt(y2)+'</text>'; }
  h+=line(X(st.xlo),Y(st.ylo),X(st.xhi),Y(st.ylo),'stroke:var(--ink);stroke-width:1.6')+line(X(st.xlo),Y(st.ylo),X(st.xlo),Y(st.yhi),'stroke:var(--ink);stroke-width:1.6');
  h+='<text x="'+((L+W-R)/2)+'" y="'+(H-6)+'" text-anchor="middle" style="font:600 12.5px sans-serif;fill:var(--ink)">'+esc(st.xlab)+'</text>';
  h+='<text transform="translate(13,'+((T+H-B)/2)+') rotate(-90)" text-anchor="middle" style="font:600 12.5px sans-serif;fill:var(--ink)">'+esc(st.ylab)+'</text>';
  if(st.line){ var a=st.line, xs=[st.xlo,st.xhi].map(function(x){ return [x,a[0]*x+a[1]]; }); h+='<g clip-path="url(#scclip'+w._n+')">'+line(X(xs[0][0]),Y(xs[0][1]),X(xs[1][0]),Y(xs[1][1]),'stroke:var(--accent-text);stroke-width:2')+'</g>'; }
  function cross(px,py,col,sz){ return line(px-sz,py-sz,px+sz,py+sz,'stroke:'+col+';stroke-width:2.4')+line(px-sz,py+sz,px+sz,py-sz,'stroke:'+col+';stroke-width:2.4'); }
  st.fixed.forEach(function(p){ h+=cross(X(p[0]),Y(p[1]),'var(--ink)',4.5); });
  if(st.key){ if(st.mode==='spts') scPts(st.key).forEach(function(p){ h+='<circle cx="'+X(p[0]).toFixed(1)+'" cy="'+Y(p[1]).toFixed(1)+'" r="8" style="fill:none;stroke:var(--success);stroke-width:2.5"/>'; });
    else { var k=st.key.split(',').map(Number); h+='<g clip-path="url(#scclip'+w._n+')">'+line(X(k[3]),Y(k[0]*k[3]+k[1]),X(k[4]),Y(k[0]*k[4]+k[1]),'stroke:var(--success);stroke-width:3;stroke-dasharray:6 5')+'</g>'; } }
  st.pts.forEach(function(p){ h+=cross(X(p[0]),Y(p[1]),'var(--danger)',6); });
  if(st.mode==='slbf'){ if(st.lp.length===2){ var P=st.lp, k2=(P[1][1]-P[0][1])/(P[1][0]-P[0][0]||1e-9), c2=P[0][1]-k2*P[0][0];
      var ya=k2*st.xlo+c2, yb=k2*st.xhi+c2; h+='<g clip-path="url(#scclip'+w._n+')">'+line(X(st.xlo),Y(ya),X(st.xhi),Y(yb),'stroke:var(--danger);stroke-width:2.6')+'</g>'; }
    st.lp.forEach(function(p){ h+='<circle cx="'+X(p[0]).toFixed(1)+'" cy="'+Y(p[1]).toFixed(1)+'" r="5" style="fill:var(--danger)"/>'; }); }
  w.querySelector('.scw-svg').innerHTML='<svg viewBox="0 0 '+W+' '+H+'" style="width:100%;max-width:520px;touch-action:manipulation;overflow:hidden"><clipPath id="scclip'+w._n+'"><rect x="'+L+'" y="'+T+'" width="'+(W-L-R)+'" height="'+(H-T-B)+'"/></clipPath>'+h+'</svg>';
  w._inv=function(px,py){ return [st.xlo+(px-L)/(W-L-R)*(st.xhi-st.xlo), st.ylo+(H-B-py)/(H-T-B)*(st.yhi-st.ylo)]; }; w._W=W; w._H=H; }
function scEnc(st){ if(st.mode==='spts') return st.pts.map(function(p){ return p[0]+','+p[1]; }).join('; ');
  if(st.lp.length<2) return ''; return 'line:('+st.lp[0][0]+','+st.lp[0][1]+')-('+st.lp[1][0]+','+st.lp[1][1]+')'; }
function scSave(w){ var st=w._st, enc=scEnc(st); scDraw(w); var inp=w._inp; if(inp&&!inp.disabled){ inp.value=enc; inp.dispatchEvent(new Event('input',{bubbles:true})); }
  try{ SCT[w._key]=JSON.stringify({pts:st.pts,lp:st.lp}); }catch(e){}
  var sm=w.querySelector('.scw-sum'); if(sm) sm.innerHTML= st.mode==='spts' ? (st.pts.length?'Points plotted: <b>'+st.pts.length+'</b>':'') : (st.lp.length===2?'Line drawn — tap ↩ Undo to move it.':(st.lp.length?'Tap a second point on your line.':'')); }
function scTap(w,ev){ var st=w._st; if(st.ro) return; var svg=w.querySelector('svg'), r=svg.getBoundingClientRect(), p=w._inv((ev.clientX-r.left)*w._W/r.width,(ev.clientY-r.top)*w._H/r.height);
  if(p[0]<st.xlo||p[0]>st.xhi||p[1]<st.ylo||p[1]>st.yhi) return;
  var q=[Math.round(p[0]/st.xsnap)*st.xsnap, Math.round(p[1]/st.ysnap)*st.ysnap]; q=[+q[0].toFixed(6),+q[1].toFixed(6)];
  if(st.mode==='spts'){ var i=st.pts.findIndex(function(a){ return Math.abs(a[0]-q[0])<1e-9&&Math.abs(a[1]-q[1])<1e-9; }); if(i>=0) st.pts.splice(i,1); else st.pts.push(q); }
  else { if(st.lp.length>=2) st.lp=[]; if(!(st.lp.length===1&&Math.abs(st.lp[0][0]-q[0])<1e-9)) st.lp.push(q); }
  scSave(w); }
var SCN=0;
function scInit(){ document.querySelectorAll('.scatw').forEach(function(w){ if(w._st) return; w._n=++SCN;
  var figd=w.closest('.fig'), line=figd&&figd.nextElementSibling, inp=(w.dataset.mode&&line)?line.querySelector('.blank-input'):null; w._inp=inp||null;
  if(inp){ inp.setAttribute('tabindex','-1'); inp.setAttribute('inputmode','none'); inp.style.cssText='position:absolute;opacity:0;width:1px;height:1px;padding:0;border:0;pointer-events:none;'; }
  var D=w.dataset, num=function(k,d){ var v=parseFloat(D[k]); return isFinite(v)?v:d; };
  var st={mode:D.mode||'',xlo:num('xlo',0),xhi:num('xhi',10),xstep:num('xstep',1),xminor:num('xminor',0),ylo:num('ylo',0),yhi:num('yhi',10),ystep:num('ystep',1),yminor:num('yminor',0),
    xsnap:num('xsnap',num('xminor',0)||num('xstep',1)),ysnap:num('ysnap',num('yminor',0)||num('ystep',1)),xlab:D.xlab||'',ylab:D.ylab||'',fixed:scPts(D.pts),line:D.line?D.line.split(',').map(Number):null,pts:[],lp:[],ro:!!(inp&&inp.disabled),key:null};
  w._st=st; w._key=MODE+'|'+activeTab+'|'+state.tabs[activeTab].idx+'|'+(inp?inp.dataset.step:'')+'|'+(D.id||'');
  var sv=SCT[w._key]; if(sv){ try{ var o=JSON.parse(sv); st.pts=o.pts||[]; st.lp=o.lp||[]; }catch(e){} }
  else if(inp&&inp.value){ if(st.mode==='spts') st.pts=scPts(inp.value); else { var m=inp.value.match(/^line:\(([^,]+),([^)]+)\)-\(([^,]+),([^)]+)\)/); if(m) st.lp=[[+m[1],+m[2]],[+m[3],+m[4]]]; } }
  if(st.ro && inp && D.key && MODE!=='quiz'){ if(!answerMatches(inp.value,D.key,D.meta?[D.meta]:[],st.mode)) st.key=D.key; }
  var tip=st.mode==='spts'?'Tap the grid to plot each point (tap a point again to remove it).':(st.mode==='slbf'?'Tap two points to draw your line of best fit (tap again to start over).':'');
  w.innerHTML='<div class="scw-svg"></div>'+(st.mode&&!st.ro?'<div class="plw-msg">'+tip+'</div><div class="plw-tools"><button type="button" data-a="undo">↩ Undo</button><button type="button" data-a="clear">🗑 Clear</button></div>':'')+'<div class="scw-sum"></div>'+(st.key?'<div class="plw-key">Correct answer shown in <b style="color:var(--success)">green</b>.</div>':'');
  w.addEventListener('click',function(ev){ var b=ev.target.closest('button[data-a]'); if(!b) return; ev.preventDefault(); if(b.dataset.a==='clear'){ st.pts=[]; st.lp=[]; } else { if(st.mode==='spts') st.pts.pop(); else st.lp.pop(); } scSave(w); });
  if(st.mode) w.querySelector('.scw-svg').addEventListener('click',function(ev){ scTap(w,ev); });
  scDraw(w); var sm=w.querySelector('.scw-sum'); if(sm&&st.mode==='spts'&&st.pts.length) sm.innerHTML='Points plotted: <b>'+st.pts.length+'</b>'; }); }
(function(){ var _rs=renderSlide; renderSlide=function(){ _rs.apply(this,arguments); try{ if(document.querySelector('#wrap .scatw')){ scInit();
  var sl=SLIDES[activeTab][state.tabs[activeTab].idx]; if(sl&&sl.flat&&sl.flat.every(function(s){ return !s.expr||s.expr==='spts'||s.expr==='slbf'||s.expr==='plot1'||s.expr==='plot2'; })) document.querySelectorAll('#wrap .quiz-hint').forEach(function(q){ if(/Type expressions/.test(q.textContent)) q.remove(); }); } }catch(e){ console.log('scat',e); } }; })();


/* ================= calculus answer mode ================= */
function calcCompile(src){
  var s=String(src).replace(/\s+/g,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^(2)').replace(/³/g,'^(3)').replace(/π/g,'#').replace(/θ/g,'q').replace(/eˣ/g,'e^x');
  if(s.indexOf('=')>=0) s=s.slice(s.lastIndexOf('=')+1);
  var FN=['sqrt','cbrt','abs','ln','log','exp','sin','cos','tan','sec','csc','cot','pi'];
  var i=0,toks=[];
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length&&/[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(ch==='√'){ toks.push({k:'f',v:'sqrt'}); i++; continue; }
    if(ch==='∛'){ toks.push({k:'f',v:'cbrt'}); i++; continue; }
    if(/[a-zA-Z#]/.test(ch)){
      var hit=null; for(var q=0;q<FN.length;q++){ if(s.substr(i,FN[q].length).toLowerCase()===FN[q]){ hit=FN[q]; break; } }
      if(hit==='pi'){ toks.push({k:'v',v:'#'}); i+=2; continue; }
      if(hit){ toks.push({k:'f',v:hit}); i+=hit.length; continue; }
      toks.push({k:'v',v:ch}); i++; continue; }
    if('+-*/^()|'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  // absolute value bars -> abs( )
  var t2=[],open=false; for(var a=0;a<toks.length;a++){ var tk=toks[a]; if(tk.k==='|'){ if(!open){ t2.push({k:'f',v:'abs'}); t2.push({k:'('}); open=true; } else { t2.push({k:')'}); open=false; } } else t2.push(tk); }
  toks=t2;
  var out=[];
  for(var t=0;t<toks.length;t++){ var A=toks[t], B=out[out.length-1];
    if(B&&(B.k==='n'||B.k==='v'||B.k===')')&&(A.k==='n'||A.k==='v'||A.k==='('||A.k==='f')) out.push({k:'&'});
    out.push(A); }
  var p=0; function pk(){ return out[p]; }
  var F={sqrt:Math.sqrt,cbrt:Math.cbrt,ln:Math.log,log:function(x){return Math.log(x)/Math.LN10;},exp:Math.exp,sin:Math.sin,cos:Math.cos,tan:Math.tan,
    sec:function(x){return 1/Math.cos(x);},csc:function(x){return 1/Math.sin(x);},cot:function(x){return 1/Math.tan(x);},abs:Math.abs};
  function E(){ var n=T(); while(pk()&&(pk().k==='+'||pk().k==='-')){ var o=out[p++].k,r=T(); n=(function(l,r,o){return function(e){return o==='+'?l(e)+r(e):l(e)-r(e);};})(n,r,o);} return n; }
  function T(){ var n=I(); while(pk()&&(pk().k==='*'||pk().k==='/')){ var o=out[p++].k,r=I(); n=(function(l,r,o){return function(e){return o==='*'?l(e)*r(e):l(e)/r(e);};})(n,r,o);} return n; }
  function I(){ var n=U(); while(pk()&&pk().k==='&'){ p++; var r=P(); n=(function(l,r){return function(e){return l(e)*r(e);};})(n,r);} return n; }
  function U(){ if(pk()&&pk().k==='-'){ p++; var u=U(); return function(e){return -u(e);}; } if(pk()&&pk().k==='+'){ p++; return U(); } return P(); }
  function P(){ var b=Aa(); if(pk()&&pk().k==='^'){ p++; var x=U(); return function(e){return Math.pow(b(e),x(e));}; } return b; }
  function Aa(){ var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){return t.v;};
    if(t.k==='v'){ if(t.v==='#') return function(){return Math.PI;}; if(t.v==='e') return function(){return Math.E;}; return function(e){return e[t.v];}; }
    if(t.k==='('){ var n=E(); if(!pk()||pk().k!==')') throw 0; p++; return n; }
    if(t.k==='f'){ var fn=F[t.v]; var ex=null;
      if(pk()&&pk().k==='^'){ p++; ex=Aa(); if(pk()&&pk().k==='&') p++; }            // sin^2(x)
      var arg; if(pk()&&pk().k==='('){ p++; arg=E(); if(!pk()||pk().k!==')') throw 0; p++; } else { arg=P(); while(pk()&&pk().k==='&'&&out[p+1]&&(out[p+1].k==='n'||(out[p+1].k==='v'&&out[p+1].v!=='e'))){ p++; var nx=P(); arg=(function(l,r){return function(e){return l(e)*r(e);};})(arg,nx); } }
      return ex? function(e){ return Math.pow(fn(arg(e)),ex(e)); } : function(e){ return fn(arg(e)); }; }
    throw 0; }
  try{ var f=E(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function calcEqual(input,answer){
  var f=calcCompile(input), g=calcCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<14;trial++){
    var env={}; 'abcdfghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=0.35+Math.random()*2.3; });
    var x=f(env), y=g(env); if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-6*Math.max(1,Math.abs(x),Math.abs(y))) return false; hits++;
  }
  return hits>=4;
}
(function(){
  var _am=answerMatches;
  answerMatches=function(input,answer,accept,expr){
    if(expr==='expanded'){ if(input===undefined||input===null||String(input).trim()==='') return false; if(/[()\[\]]/.test(String(input))) return false; return _am.call(this,input,answer,accept,true); }
    if(expr==='calc'){ if(input===undefined||input===null||String(input).trim()==='') return false;
      if(calcEqual(input,answer)) return true; return (accept||[]).some(function(a){ return calcEqual(input,a); }); }
    return _am.apply(this,arguments); };
  var _kl=kbLayoutFor;
  kbLayoutFor=function(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx], stp=sl.flat[parseInt(inp.dataset.step,10)]; if(stp.expr==='calc') return 'calc'; }catch(e){} return _kl(inp); };
  var _kp=kbPress;
  kbPress=function(k){ var m={'eˣ':'e^(','√':'√(','ln':'ln(','sin':'sin(','cos':'cos(','tan':'tan(','sec':'sec(','csc':'csc(','cot':'cot(','∛':'∛('}; if(KB.page==='calc'&&m[k]){ kbInsert(m[k]); return; } return _kp(k); };
})();


/* ================= v5: interactive plotting ================= */
var GP={};
function gpNum(s){ s=String(s).trim().replace(/[−–]/g,'-'); var m=s.match(/^(-?\d+(?:\.\d+)?)\/(\d+(?:\.\d+)?)$/); if(m) return parseFloat(m[1])/parseFloat(m[2]); var m2=s.match(/^(-?)(\d+) (\d+)\/(\d+)$/); if(m2) return (m2[1]?-1:1)*(+m2[2]+m2[3]/m2[4]); var v=parseFloat(s); return isFinite(v)&&/^-?\d*\.?\d+$/.test(s)?v:NaN; }
function gpIneq(src){ // -> {f:function(x,y), op:'<'|'<='|'>'|'>=', a,b,c} with f = lhs-rhs
  var s=String(src).replace(/≤/g,'<=').replace(/≥/g,'>=').replace(/\s+/g,'').replace(/−/g,'-');
  var m=s.match(/^(.*?)(<=|>=|<|>)(.*)$/); if(!m) return null;
  var L=calcCompile(m[1]), R=calcCompile(m[3]); if(!L||!R) return null;
  var f=function(x,y){ return L({x:x,y:y})-R({x:x,y:y}); };
  var d=f(0,0), a=f(1,0)-d, b=f(0,1)-d; return {f:f,op:m[2],a:a,b:b,c:-d,src:src};
}
function gpOpTxt(op){ return {'<':'<','<=':'≤','>':'>','>=':'≥'}[op]; }
function gpSat(I,x,y){ var v=I.f(x,y); if(I.op==='<') return v<-1e-9; if(I.op==='<=') return v<=1e-9; if(I.op==='>') return v>1e-9; return v>=-1e-9; }
function gpParseG(v){ var m=String(v||'').match(/^G:(-?[\d.]+),(-?[\d.]+);(-?[\d.]+),(-?[\d.]+);([sd]);(-?[\d.]+),(-?[\d.]+)$/); if(!m) return null;
  return {p:[[+m[1],+m[2]],[+m[3],+m[4]]], solid:m[5]==='s', sh:[+m[6],+m[7]]}; }
function gpParseN(v){ var m=String(v||'').match(/^N:([^;]+);([^;]+);([LRBO])$/); if(!m) return null;
  var vs=m[1].split(',').map(gpNum), cs=m[2].split(','); if(vs.some(isNaN)) return null; return {v:vs, c:cs.map(function(c){return c==='c';}), mode:m[3]}; }
function gpOpt(accept,pre){ var r=null; (accept||[]).forEach(function(a){ if(String(a).indexOf(pre)===0) r=String(a).slice(pre.length); }); return r; }
function gpCheckG(input,answer,accept){
  var I=gpIneq(gpOpt(accept,'INEQ:')||''), S=gpParseG(input); if(!I||!S) return false;
  var p=S.p; if(Math.abs(p[0][0]-p[1][0])<1e-9&&Math.abs(p[0][1]-p[1][1])<1e-9) return false;
  var tol=1e-7*Math.max(1,Math.abs(I.a),Math.abs(I.b),Math.abs(I.c));
  if(Math.abs(I.f(p[0][0],p[0][1]))>tol||Math.abs(I.f(p[1][0],p[1][1]))>tol) return false;
  var strict=(I.op==='<'||I.op==='>'); if(S.solid===strict) return false;
  if(Math.abs(I.f(S.sh[0],S.sh[1]))<tol) return false;
  return gpSat(I,S.sh[0],S.sh[1]);
}
function gpCheckN(input,answer){
  var S=gpParseN(input), K=gpParseN(answer); if(!S||!K) return false;
  if(S.mode!==K.mode||S.v.length!==K.v.length) return false;
  var sv=S.v.slice(), sc=S.c.slice(); if(sv.length===2&&sv[0]>sv[1]){ sv.reverse(); sc.reverse(); }
  for(var i=0;i<sv.length;i++){ if(Math.abs(sv[i]-K.v[i])>1e-6||sc[i]!==K.c[i]) return false; }
  return true;
}
function gpHumanG(v){ var S=gpParseG(v); if(!S) return v||'—'; return 'boundary through ('+S.p[0]+') and ('+S.p[1]+'), '+(S.solid?'solid':'dashed')+', shaded on the side of ('+S.sh+')'; }
function gpHumanN(v){ var S=gpParseN(v); if(!S) return v||'—'; var d=function(i){ return (S.c[i]?'closed':'open')+' dot at '+S.v[i]; };
  if(S.mode==='L') return d(0)+', shaded to the left'; if(S.mode==='R') return d(0)+', shaded to the right';
  return d(0)+' and '+d(1)+', shaded '+(S.mode==='B'?'between them':'outside them'); }
(function(){
  var _am=answerMatches;
  answerMatches=function(input,answer,accept,expr){
    if(expr==='gplot') return gpCheckG(input,answer,accept);
    if(expr==='nplot') return gpCheckN(input,answer);
    return _am.apply(this,arguments); };
  var _sat=slideAnswerText;
  slideAnswerText=function(slide,item,correctSide){
    if(slide.kind!=='blank'||!slide.flat.some(function(s){return s.expr==='gplot'||s.expr==='nplot';})) return _sat.apply(this,arguments);
    return slide.flat.map(function(step,si){ var ss=item.stepStates[si];
      return Object.keys(step.a).map(function(k){
        if(step.expr==='gplot') return correctSide ? 'the graph of '+(gpOpt(step.accept,'INEQ:')||'').replace(/<=/g,'≤').replace(/>=/g,'≥') : gpHumanG(ss.inputs[k]);
        if(step.expr==='nplot') return correctSide ? gpHumanN(step.a[k])+((gpOpt(step.accept,'INEQ:'))?' ('+gpOpt(step.accept,'INEQ:').replace(/<=/g,'≤').replace(/>=/g,'≥')+')':'') : gpHumanN(ss.inputs[k]);
        return correctSide ? step.a[k] : (ss.inputs[k] || '—'); }).join(', '); }).join('  |  ');
  };
  var _rs=renderSlide;
  renderSlide=function(){ _rs.apply(this,arguments); try{ gpEnhance(); grInitAll(); }catch(e){ console.log('gp',e); } };
})();
function gpStep(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx]; return sl.flat[parseInt(inp.dataset.step,10)]; }catch(e){ return null; } }
function gpEnhance(){
  document.querySelectorAll('.blank-input').forEach(function(inp){
    var st=gpStep(inp); if(!st||(st.expr!=='gplot'&&st.expr!=='nplot')||inp.dataset.gp) return; inp.dataset.gp='1';
    inp.classList.add('gp-hidden'); inp.setAttribute('tabindex','-1'); inp.setAttribute('aria-hidden','true');
    var box=document.createElement('div'); box.className='gp-box';
    var line=inp.closest('.step-line'); (line||inp.parentNode).appendChild(box);
    var ts=state.tabs[activeTab], item=ts.items[ts.idx], ss=item.stepStates?item.stepStates[parseInt(inp.dataset.step,10)]:null;
    var done=inp.disabled, revealed=ss&&ss.status==='revealed';
    if(st.expr==='gplot') gpBuildG(box,inp,st,done,revealed); else gpBuildN(box,inp,st,done,revealed);
    var rn=line&&line.nextElementSibling; if(rn&&rn.classList.contains('reveal-note')){ var iq=gpOpt(st.accept,'INEQ:'); rn.textContent='Correct graph'+(iq?' of '+iq.replace(/<=/g,'≤').replace(/>=/g,'≥'):'')+' shown in green.'; }
  });
}
function gpKey(inp){ return (MODE||'')+'|'+activeTab+'|'+state.tabs[activeTab].idx+'|'+inp.dataset.step; }
function gpSet(inp,v){ inp.value=v; inp.dispatchEvent(new Event('input',{bubbles:true})); }
/* ---------- coordinate-plane widget ---------- */
function gpRange(st,def){ var r=gpOpt(st.accept,'R:'); if(!r) return def; var a=r.split(',').map(Number); return a.length>=2&&a.every(isFinite)?a:def; }
function gpClipHalf(poly,a,b,c,keepPos){ // keep points with s*(a x + b y - c) >= 0
  var s=keepPos?1:-1, out=[]; for(var i=0;i<poly.length;i++){ var P=poly[i], Q=poly[(i+1)%poly.length];
    var fp=s*(a*P[0]+b*P[1]-c), fq=s*(a*Q[0]+b*Q[1]-c);
    if(fp>=0) out.push(P); if((fp>=0)!==(fq>=0)){ var t=fp/(fp-fq); out.push([P[0]+t*(Q[0]-P[0]),P[1]+t*(Q[1]-P[1])]); } } return out; }
function gpBuildG(box,inp,st,done,revealed){
  var R=gpRange(st,[-8,8,-8,8]), x0=R[0],x1=R[1],y0=R[2],y1=R[3], W=320, H=Math.round(320*(y1-y0)/(x1-x0)), pad=0;
  var X=function(x){ return (x-x0)/(x1-x0)*W; }, Y=function(y){ return H-(y-y0)/(y1-y0)*H; };
  var S=gpParseG(inp.value)||{p:[],solid:true,sh:null}; if(!gpParseG(inp.value)){ if(GP[gpKey(inp)]) S=JSON.parse(JSON.stringify(GP[gpKey(inp)])); }
  var I=gpIneq(gpOpt(st.accept,'INEQ:')||'');
  box.innerHTML='<div class="gp-help">'+(done?'Your graph':'① Tap two grid points on the boundary line · ② choose Solid or Dashed · ③ tap the side to shade')+'</div>'+
    '<svg class="gp-svg" viewBox="-14 -14 '+(W+28)+' '+(H+28)+'" style="max-width:100%;touch-action:manipulation"></svg>'+
    (done?'':'<div class="gp-tools"><button type="button" data-k="s" class="gp-b">━ Solid (≤, ≥)</button><button type="button" data-k="d" class="gp-b">┅ Dashed (&lt;, &gt;)</button><button type="button" data-k="u" class="gp-b">↶ Undo</button><button type="button" data-k="c" class="gp-b">Clear</button></div>')+
    '<div class="gp-stat"></div>';
  var svg=box.querySelector('svg'), stat=box.querySelector('.gp-stat');
  function lineSeg(a,b,c){ // endpoints of a x + b y = c inside box
    var pts=[], add=function(x,y){ if(x>=x0-1e-9&&x<=x1+1e-9&&y>=y0-1e-9&&y<=y1+1e-9&&!pts.some(function(p){return Math.abs(p[0]-x)<1e-9&&Math.abs(p[1]-y)<1e-9;})) pts.push([x,y]); };
    if(Math.abs(b)>1e-12){ add(x0,(c-a*x0)/b); add(x1,(c-a*x1)/b); } if(Math.abs(a)>1e-12){ add((c-b*y0)/a,y0); add((c-b*y1)/a,y1); } return pts.slice(0,2); }
  function region(a,b,c,keepPos,fill){ var poly=gpClipHalf([[x0,y0],[x1,y0],[x1,y1],[x0,y1]],a,b,c,keepPos); if(poly.length<3) return '';
    return '<polygon points="'+poly.map(function(p){return X(p[0]).toFixed(1)+','+Y(p[1]).toFixed(1);}).join(' ')+'" style="fill:'+fill+';opacity:.28"/>'; }
  function draw(){
    var h='', i;
    for(i=Math.ceil(x0);i<=x1;i++) h+='<line x1="'+X(i)+'" y1="0" x2="'+X(i)+'" y2="'+H+'" style="stroke:var(--rule);stroke-width:'+(i===0?0:1)+'"/>';
    for(i=Math.ceil(y0);i<=y1;i++) h+='<line x1="0" y1="'+Y(i)+'" x2="'+W+'" y2="'+Y(i)+'" style="stroke:var(--rule);stroke-width:'+(i===0?0:1)+'"/>';
    if(x0<0&&x1>0) h+='<line x1="'+X(0)+'" y1="0" x2="'+X(0)+'" y2="'+H+'" style="stroke:var(--ink);stroke-width:1.6"/>';
    if(y0<0&&y1>0) h+='<line x1="0" y1="'+Y(0)+'" x2="'+W+'" y2="'+Y(0)+'" style="stroke:var(--ink);stroke-width:1.6"/>';
    var step=(x1-x0)>12?2:1; for(i=Math.ceil(x0);i<=x1;i++) if(i!==0&&i%step===0) h+='<text x="'+X(i)+'" y="'+(Y(0)+13)+'" text-anchor="middle" style="font:10px sans-serif;fill:var(--ink-soft)">'+String(i).replace('-','−')+'</text>';
    for(i=Math.ceil(y0);i<=y1;i++) if(i!==0&&i%step===0) h+='<text x="'+(X(0)-5)+'" y="'+(Y(i)+3.5)+'" text-anchor="end" style="font:10px sans-serif;fill:var(--ink-soft)">'+String(i).replace('-','−')+'</text>';
    h+='<text x="'+(W+4)+'" y="'+(Y(0)-4)+'" style="font:italic 12px serif;fill:var(--ink)">x</text><text x="'+(X(0)+5)+'" y="-3" style="font:italic 12px serif;fill:var(--ink)">y</text>';
    if(S.p.length===2){ var P=S.p, a=P[1][1]-P[0][1], b=P[0][0]-P[1][0], c=a*P[0][0]+b*P[0][1];
      if(Math.abs(a)>1e-12||Math.abs(b)>1e-12){
        if(S.sh){ var keep=(a*S.sh[0]+b*S.sh[1]-c)>0; h+=region(a,b,c,keep,'var(--accent-text)'); }
        var sg2=lineSeg(a,b,c); if(sg2.length===2) h+='<line x1="'+X(sg2[0][0])+'" y1="'+Y(sg2[0][1])+'" x2="'+X(sg2[1][0])+'" y2="'+Y(sg2[1][1])+'" style="stroke:var(--accent-text);stroke-width:2.6;'+(S.solid?'':'stroke-dasharray:8 6')+'"/>'; } }
    if((done||revealed)&&revealed&&I){ // correct answer in green
      var keepPos=I.op==='>'||I.op==='>='; h+=region(I.a,I.b,I.c,keepPos,'var(--success)'); var sg=lineSeg(I.a,I.b,I.c);
      if(sg.length===2) h+='<line x1="'+X(sg[0][0])+'" y1="'+Y(sg[0][1])+'" x2="'+X(sg[1][0])+'" y2="'+Y(sg[1][1])+'" style="stroke:var(--success);stroke-width:3;'+((I.op==='<'||I.op==='>')?'stroke-dasharray:8 6':'')+'"/>'; }
    S.p.forEach(function(p){ h+='<circle cx="'+X(p[0])+'" cy="'+Y(p[1])+'" r="5.5" style="fill:var(--danger)"/>'; });
    if(S.sh) h+='<text x="'+X(S.sh[0])+'" y="'+(Y(S.sh[1])+5)+'" text-anchor="middle" style="font:700 15px sans-serif;fill:var(--accent-text)">✚</text>';
    h+='<rect x="0" y="0" width="'+W+'" height="'+H+'" style="fill:transparent;stroke:var(--ink-soft);stroke-width:1" class="gp-hit"/>';
    svg.innerHTML=h;
    var msg = S.p.length<2 ? 'Point '+(S.p.length+1)+' of 2: tap a grid point on the boundary line.' : (!S.sh ? 'Line: '+(S.solid?'solid':'dashed')+'. Now tap a point on the side to shade.' : 'Boundary through ('+S.p[0]+') and ('+S.p[1]+'), '+(S.solid?'solid':'dashed')+', shaded side marked ✚. Press Check.');
    if(!done) stat.textContent=msg; else stat.textContent=S.p.length===2&&S.sh?gpHumanG(inp.value):'';
  }
  function save(){ GP[gpKey(inp)]=JSON.parse(JSON.stringify(S)); if(S.p.length===2&&S.sh) gpSet(inp,'G:'+S.p[0]+';'+S.p[1]+';'+(S.solid?'s':'d')+';'+S.sh); else gpSet(inp,''); }
  if(!done){
    svg.addEventListener('click',function(e){ var r=svg.getBoundingClientRect(), vb=svg.viewBox.baseVal, sx=(e.clientX-r.left)/r.width*vb.width+vb.x, sy=(e.clientY-r.top)/r.height*vb.height+vb.y;
      var x=x0+sx/W*(x1-x0), y=y0+(H-sy)/H*(y1-y0); if(x<x0-0.3||x>x1+0.3||y<y0-0.3||y>y1+0.3) return;
      if(S.p.length<2){ var gx=Math.round(x), gy=Math.round(y); if(S.p.length===1&&S.p[0][0]===gx&&S.p[0][1]===gy) return; S.p.push([gx,gy]); S.sh=null; }
      else { S.sh=[Math.round(x*2)/2,Math.round(y*2)/2]; var a=S.p[1][1]-S.p[0][1], b=S.p[0][0]-S.p[1][0], c=a*S.p[0][0]+b*S.p[0][1]; if(Math.abs(a*S.sh[0]+b*S.sh[1]-c)<1e-9){ S.sh=[Math.round(x*4)/4,Math.round(y*4)/4]; if(Math.abs(a*S.sh[0]+b*S.sh[1]-c)<1e-9) S.sh=null; } }
      save(); draw(); });
    box.querySelectorAll('.gp-b').forEach(function(b){ b.addEventListener('click',function(){ var k=b.dataset.k;
      if(k==='s') S.solid=true; else if(k==='d') S.solid=false; else if(k==='c'){ S={p:[],solid:S.solid,sh:null}; } else if(k==='u'){ if(S.sh) S.sh=null; else S.p.pop(); }
      box.querySelectorAll('.gp-b[data-k=s],.gp-b[data-k=d]').forEach(function(x){ x.classList.toggle('on',(x.dataset.k==='s')===S.solid); });
      save(); draw(); }); });
    box.querySelectorAll('.gp-b[data-k=s],.gp-b[data-k=d]').forEach(function(x){ x.classList.toggle('on',(x.dataset.k==='s')===S.solid); });
  }
  draw();
}
/* ---------- number-line widget ---------- */
function gpBuildN(box,inp,st,done,revealed){
  var R=gpRange(st,[-8,8]), lo=R[0], hi=R[1], W=320, H=70, X=function(v){ return 14+(v-lo)/(hi-lo)*(W-28); };
  var S=gpParseN(inp.value)||{v:[],c:[],mode:''}; var draft={v:['',''],c:['c','c'],n:1,mode:''};
  if(gpParseN(inp.value)){ var T=gpParseN(inp.value); draft.n=T.v.length; draft.v=[String(T.v[0]),T.v[1]!==undefined?String(T.v[1]):'']; draft.c=[T.c[0]?'c':'o',T.c[1]?'c':'o']; draft.mode=T.mode; }
  else { if(GP[gpKey(inp)]) draft=JSON.parse(JSON.stringify(GP[gpKey(inp)])); }
  var K=gpParseN(st.a[Object.keys(st.a)[0]]);
  box.innerHTML='<div class="gp-help">'+(done?'Your number line':'Choose 1 or 2 endpoints, type each value, pick open ○ / closed ● dots and the shading')+'</div>'+
    '<svg class="gp-svg" viewBox="0 0 '+W+' '+H+'" style="max-width:100%"></svg>'+
    (done?'':'<div class="gp-tools gp-n">'+
      '<span class="gp-lab">Endpoints:</span><button type="button" class="gp-b" data-n="1">1</button><button type="button" class="gp-b" data-n="2">2</button><br>'+
      '<span class="gp-lab">A =</span><input class="gp-in" data-i="0" inputmode="decimal" placeholder="value"><button type="button" class="gp-b" data-ci="0" data-c="o">○ open</button><button type="button" class="gp-b" data-ci="0" data-c="c">● closed</button><br>'+
      '<span class="gp-row2"><span class="gp-lab">B =</span><input class="gp-in" data-i="1" inputmode="decimal" placeholder="value"><button type="button" class="gp-b" data-ci="1" data-c="o">○ open</button><button type="button" class="gp-b" data-ci="1" data-c="c">● closed</button><br></span>'+
      '<span class="gp-lab">Shade:</span><span class="gp-sh1"><button type="button" class="gp-b" data-m="L">← left</button><button type="button" class="gp-b" data-m="R">right →</button></span><span class="gp-sh2"><button type="button" class="gp-b" data-m="B">between</button><button type="button" class="gp-b" data-m="O">outside</button></span></div>')+
    '<div class="gp-stat"></div>';
  var svg=box.querySelector('svg'), stat=box.querySelector('.gp-stat');
  function seg(a,b,col,y){ return '<line x1="'+X(a)+'" y1="'+y+'" x2="'+X(b)+'" y2="'+y+'" style="stroke:'+col+';stroke-width:5;stroke-linecap:round;opacity:.85"/>'; }
  function arrowTo(v,dir,col,y){ var e=dir<0?lo:hi; return seg(v,e,col,y)+'<path d="M'+X(e)+' '+y+' l'+(dir<0?8:-8)+' -6 v12 z" style="fill:'+col+'"/>'; }
  function dot(v,closed,col,y){ return '<circle cx="'+X(v)+'" cy="'+y+'" r="6" style="fill:'+(closed?col:'var(--card)')+';stroke:'+col+';stroke-width:2.4"/>'; }
  function paint(T,col,y){ if(!T) return ''; var h='', v=T.v.slice(), c=T.c.slice(); if(v.length===2&&v[0]>v[1]){ v.reverse(); c.reverse(); }
    if(T.mode==='L') h+=arrowTo(v[0],-1,col,y); else if(T.mode==='R') h+=arrowTo(v[0],1,col,y); else if(T.mode==='B') h+=seg(v[0],v[1],col,y); else if(T.mode==='O') h+=arrowTo(v[0],-1,col,y)+arrowTo(v[1],1,col,y);
    v.forEach(function(x,i){ h+=dot(x,c[i],col,y); }); return h; }
  function cur(){ var vs=draft.v.slice(0,draft.n).map(gpNum); if(vs.some(isNaN)||!draft.mode) return null; if(draft.n===1&&'LR'.indexOf(draft.mode)<0) return null; if(draft.n===2&&'BO'.indexOf(draft.mode)<0) return null;
    return {v:vs,c:draft.c.slice(0,draft.n).map(function(x){return x==='c';}),mode:draft.mode}; }
  function draw(){
    var h='<line x1="6" y1="40" x2="'+(W-6)+'" y2="40" style="stroke:var(--ink);stroke-width:1.6"/><path d="M'+(W-6)+' 40 l-8 -5 v10z M6 40 l8 -5 v10z" style="fill:var(--ink)"/>';
    var step=(hi-lo)>16?2:1; for(var i=Math.ceil(lo);i<=hi;i++){ h+='<line x1="'+X(i)+'" y1="35" x2="'+X(i)+'" y2="45" style="stroke:var(--ink);stroke-width:1"/>'; if(i%step===0) h+='<text x="'+X(i)+'" y="60" text-anchor="middle" style="font:11px sans-serif;fill:var(--ink-soft)">'+String(i).replace('-','−')+'</text>'; }
    if(revealed&&K) h+=paint(K,'var(--success)',22);
    var T=done?gpParseN(inp.value):cur(); h+=paint(T,'var(--accent-text)',40); svg.innerHTML=h;
    if(!done){ box.querySelectorAll('.gp-b[data-n]').forEach(function(b){ b.classList.toggle('on',+b.dataset.n===draft.n); });
      box.querySelector('.gp-row2').style.display=draft.n===2?'':'none'; box.querySelector('.gp-sh1').style.display=draft.n===1?'':'none'; box.querySelector('.gp-sh2').style.display=draft.n===2?'':'none';
      box.querySelectorAll('.gp-b[data-ci]').forEach(function(b){ b.classList.toggle('on',draft.c[+b.dataset.ci]===b.dataset.c); });
      box.querySelectorAll('.gp-b[data-m]').forEach(function(b){ b.classList.toggle('on',draft.mode===b.dataset.m); });
      stat.textContent = T ? gpHumanN('N:'+T.v.join(',')+';'+T.c.map(function(x){return x?'c':'o';}).join(',')+';'+T.mode)+'. Press Check.' : 'Fill in the endpoint value(s) and choose the shading.'; }
    else stat.textContent = T?gpHumanN(inp.value):'';
  }
  function save(){ GP[gpKey(inp)]=JSON.parse(JSON.stringify(draft)); var T=cur(); gpSet(inp, T? 'N:'+draft.v.slice(0,draft.n).map(function(s){return String(s).trim().replace(/[−–]/g,'-');}).join(',')+';'+draft.c.slice(0,draft.n).join(',')+';'+draft.mode : ''); }
  if(!done){
    box.querySelectorAll('.gp-in').forEach(function(f){ f.value=draft.v[+f.dataset.i]||''; f.addEventListener('input',function(){ draft.v[+f.dataset.i]=f.value; save(); draw(); }); });
    box.querySelectorAll('.gp-b').forEach(function(b){ b.addEventListener('click',function(){
      if(b.dataset.n){ draft.n=+b.dataset.n; draft.mode=''; } if(b.dataset.ci) draft.c[+b.dataset.ci]=b.dataset.c; if(b.dataset.m) draft.mode=b.dataset.m; save(); draw(); }); });
  }
  draw();
}
/* ---------- inequality grapher (explore tool) ---------- */
function grInitAll(root){ (root||document).querySelectorAll('.ineq-grapher:not([data-ok])').forEach(grInit); }
function grInit(el){
  el.dataset.ok='1'; var init=el.dataset.init||'y >= 2x - 1; x + y < 6';
  el.innerHTML='<div class="gr-head">📈 Inequality grapher</div><div class="gr-row"><input class="gr-in" value="'+esc(init)+'" aria-label="inequalities"><button type="button" class="gp-b gr-go">Plot</button></div>'+
    '<div class="gr-hint">Type one or more inequalities in x and y, separated by ; (e.g. 2x + 3y ≤ 6; x ≥ 0; y ≥ 0). The region that satisfies all of them is shaded; solid lines for ≤ ≥, dashed for &lt; &gt;.</div>'+
    '<canvas class="gr-cv" width="640" height="640"></canvas><div class="gr-msg"></div>';
  var cv=el.querySelector('canvas'), inp=el.querySelector('.gr-in'), msg=el.querySelector('.gr-msg');
  function plot(){
    var ctx=cv.getContext('2d'), W=cv.width, H=cv.height, x0=-10,x1=10,y0=-10,y1=10, cs=getComputedStyle(document.documentElement);
    var ink=cs.getPropertyValue('--ink').trim()||'#222', rule=cs.getPropertyValue('--rule').trim()||'#ddd', acc=cs.getPropertyValue('--accent-text').trim()||'#1F3B6B', card=cs.getPropertyValue('--card').trim()||'#fff';
    var parts=inp.value.split(/[;,]/).map(function(s){return s.trim();}).filter(Boolean), Is=[];
    for(var i=0;i<parts.length;i++){ var I=gpIneq(parts[i]); if(!I){ msg.textContent='Could not read “'+parts[i]+'”. Use x, y, numbers, + − × /, ^ and one of < > ≤ ≥ (or <= >=).'; return; } Is.push(I); }
    msg.textContent=Is.length?'Shaded: points satisfying '+parts.map(function(p){return p.replace(/<=/g,'≤').replace(/>=/g,'≥');}).join(' and ')+'.':'';
    var X=function(x){return (x-x0)/(x1-x0)*W;}, Y=function(y){return H-(y-y0)/(y1-y0)*H;};
    ctx.fillStyle=card; ctx.fillRect(0,0,W,H);
    var cell=4; ctx.fillStyle=acc; ctx.globalAlpha=0.28;
    for(var px=0;px<W;px+=cell) for(var py=0;py<H;py+=cell){ var x=x0+(px+cell/2)/W*(x1-x0), y=y1-(py+cell/2)/H*(y1-y0); if(Is.length&&Is.every(function(I){return gpSat(I,x,y);})) ctx.fillRect(px,py,cell,cell); }
    ctx.globalAlpha=1; ctx.strokeStyle=rule; ctx.lineWidth=1;
    for(var g=x0;g<=x1;g++){ ctx.beginPath(); ctx.moveTo(X(g),0); ctx.lineTo(X(g),H); ctx.stroke(); ctx.beginPath(); ctx.moveTo(0,Y(g)); ctx.lineTo(W,Y(g)); ctx.stroke(); }
    ctx.strokeStyle=ink; ctx.lineWidth=2; ctx.beginPath(); ctx.moveTo(X(0),0); ctx.lineTo(X(0),H); ctx.moveTo(0,Y(0)); ctx.lineTo(W,Y(0)); ctx.stroke();
    ctx.fillStyle=ink; ctx.font='20px sans-serif'; ctx.textAlign='center'; for(g=x0+2;g<=x1-1;g+=2){ if(g) { ctx.fillText(String(g),X(g),Y(0)+22); ctx.fillText(String(g),X(0)-16,Y(g)+7); } }
    Is.forEach(function(I){ // boundary f = 0 by sampling sign changes
      var strict=(I.op==='<'||I.op==='>'), n=320; ctx.fillStyle=acc;
      for(var i=0;i<n;i++) for(var j=0;j<n;j++){ var xa=x0+i/n*(x1-x0), ya=y0+j/n*(y1-y0), d=(x1-x0)/n;
        var f00=I.f(xa,ya), f10=I.f(xa+d,ya), f01=I.f(xa,ya+d);
        if((f00>0)!==(f10>0)||(f00>0)!==(f01>0)||Math.abs(f00)<1e-12){ if(strict&&((i+j)%14>6)) continue; ctx.fillRect(X(xa)-1.6,Y(ya)-1.6,3.2,3.2); } } });
  }
  el.querySelector('.gr-go').addEventListener('click',plot); inp.addEventListener('keydown',function(e){ if(e.key==='Enter') plot(); });
  plot();
}




window.__chk=function(i,k,a,m){ return answerMatches(i,k,a,m); };
renderLogin();
})();
</script>
</body>
</html>
