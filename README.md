<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AgentPlan</title>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0a0a0f;
  --bg2: #0f0f18;
  --bg3: #14141f;
  --card: #17172a;
  --card2: #1c1c32;
  --border: rgba(160,120,255,0.10);
  --border2: rgba(160,120,255,0.22);
  --text: #ede8ff;
  --text2: #9b92c0;
  --text3: #5a5280;
  --accent: #a855f7;
  --accent2: #7c3aed;
  --accent3: #c084fc;
  --accent-dim: rgba(168,85,247,0.13);
  --accent-glow: rgba(168,85,247,0.25);
  --red: #f87171;
  --red-dim: rgba(248,113,113,0.13);
  --yellow: #fbbf24;
  --yellow-dim: rgba(251,191,36,0.13);
  --green: #34d399;
  --green-dim: rgba(52,211,153,0.13);
  --blue: #60a5fa;
  --blue-dim: rgba(96,165,250,0.13);
  --orange: #fb923c;
  --orange-dim: rgba(251,146,60,0.13);
  --r: 10px;
  --r-sm: 7px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:'Outfit',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}
::-webkit-scrollbar{width:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

/* ── Auth screen ── */
.auth-wrap{display:flex;align-items:center;justify-content:center;min-height:100vh;position:relative;overflow:hidden}
.auth-bg{position:absolute;inset:0;background:radial-gradient(ellipse 60% 50% at 50% 30%,rgba(168,85,247,0.18) 0%,transparent 70%);pointer-events:none}
.auth-card{background:var(--card);border:1px solid var(--border2);border-radius:20px;padding:40px;width:100%;max-width:420px;position:relative;z-index:1;box-shadow:0 0 60px rgba(168,85,247,0.1)}
.auth-logo{font-size:28px;font-weight:900;color:var(--accent);letter-spacing:-1px;margin-bottom:4px}
.auth-logo span{color:var(--text3);font-weight:300}
.auth-tagline{font-size:13px;color:var(--text3);margin-bottom:28px}
.auth-tabs{display:flex;background:var(--bg3);border-radius:var(--r-sm);padding:3px;margin-bottom:24px;gap:3px}
.auth-tab{flex:1;text-align:center;padding:8px;border-radius:5px;font-size:13px;font-weight:500;cursor:pointer;color:var(--text3);transition:all .2s}
.auth-tab.active{background:var(--accent);color:#fff}

/* ── Shell ── */
.shell{display:flex;min-height:100vh}
.sidebar{width:220px;flex-shrink:0;background:var(--bg2);border-right:1px solid var(--border);padding:24px 0;display:flex;flex-direction:column;position:fixed;top:0;left:0;height:100vh;z-index:50;overflow-y:auto}
.logo-wrap{padding:0 18px 20px;border-bottom:1px solid var(--border);margin-bottom:12px}
.logo-name{font-size:20px;font-weight:900;color:var(--accent);letter-spacing:-0.5px}
.logo-user{font-size:11px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-top:2px}
.nav{flex:1;padding:0 10px}
.nav-sec{font-size:10px;text-transform:uppercase;letter-spacing:.1em;color:var(--text3);padding:14px 10px 6px}
.nav-item{display:flex;align-items:center;gap:9px;padding:9px 10px;border-radius:var(--r-sm);font-size:13.5px;color:var(--text2);cursor:pointer;transition:all .15s;margin-bottom:2px;font-weight:400}
.nav-item:hover{background:var(--accent-dim);color:var(--text)}
.nav-item.active{background:var(--accent-dim);color:var(--accent);font-weight:600}
.nav-item .ico{width:18px;text-align:center;font-size:15px}
.logout-btn{margin:12px 10px 0;padding:9px 10px;border-radius:var(--r-sm);font-size:13px;color:var(--text3);cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:9px;border:1px solid var(--border)}
.logout-btn:hover{color:var(--red);border-color:var(--red-dim)}

.main{margin-left:220px;padding:36px 40px;flex:1}
.page{display:none}.page.active{display:block}

/* ── Headers ── */
.page-hdr{margin-bottom:28px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px}
.page-hdr-left .page-title{font-size:26px;font-weight:800;letter-spacing:-0.5px}
.page-hdr-left .page-sub{font-size:13px;color:var(--text2);margin-top:3px}

/* ── Stats ── */
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:24px}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:16px 18px}
.stat-lbl{font-size:11px;text-transform:uppercase;letter-spacing:.08em;color:var(--text3);margin-bottom:6px}
.stat-num{font-size:28px;font-weight:800;line-height:1}
.stat-num.ac{color:var(--accent)}
.stat-num.rd{color:var(--red)}
.stat-num.yl{color:var(--yellow)}

/* ── Card ── */
.card{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:20px;margin-bottom:16px}
.card-title{font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:.08em;color:var(--text2);margin-bottom:16px}

/* ── Tasks ── */
.task-item{display:flex;align-items:flex-start;gap:12px;padding:14px 16px;background:var(--card);border:1px solid var(--border);border-radius:var(--r-sm);margin-bottom:8px;transition:border-color .15s}
.task-item:hover{border-color:var(--border2)}
.task-check{width:20px;height:20px;border-radius:50%;border:1.5px solid var(--border2);cursor:pointer;flex-shrink:0;margin-top:2px;display:flex;align-items:center;justify-content:center;transition:all .15s}
.task-check:hover{border-color:var(--accent)}
.task-check.done{background:var(--accent);border-color:var(--accent)}
.task-check.done::after{content:'✓';font-size:11px;color:#fff;font-weight:700}
.task-info{flex:1;min-width:0}
.task-name{font-size:14px;font-weight:600;color:var(--text);margin-bottom:2px}
.task-name.done{text-decoration:line-through;color:var(--text3)}
.task-meta{font-size:12px;color:var(--text2)}
.task-right{display:flex;align-items:center;gap:8px;flex-shrink:0}
.prog-bar{height:3px;background:var(--bg3);border-radius:2px;overflow:hidden;margin-top:6px}
.prog-fill{height:100%;background:var(--accent);border-radius:2px;transition:width .3s}
.diff-dots{display:flex;gap:3px}
.diff-dot{width:7px;height:7px;border-radius:50%;background:var(--border2)}
.diff-dot.lit{background:var(--accent)}
.diff-dot.lit.global{background:var(--red)}
.task-acts{display:flex;gap:5px}
.btn-ico{background:transparent;border:1px solid var(--border);color:var(--text3);width:28px;height:28px;border-radius:var(--r-sm);cursor:pointer;font-size:13px;display:flex;align-items:center;justify-content:center;transition:all .15s}
.btn-ico:hover{border-color:var(--border2);color:var(--text)}

/* ── Badges ── */
.badge{font-size:11px;padding:2px 9px;border-radius:20px;font-weight:500;white-space:nowrap}
.b-red{background:var(--red-dim);color:var(--red)}
.b-yellow{background:var(--yellow-dim);color:var(--yellow)}
.b-green{background:var(--green-dim);color:var(--green)}
.b-accent{background:var(--accent-dim);color:var(--accent)}
.b-blue{background:var(--blue-dim);color:var(--blue)}
.b-orange{background:var(--orange-dim);color:var(--orange)}

/* ── Buttons ── */
.btn{display:inline-flex;align-items:center;gap:7px;padding:9px 18px;border-radius:var(--r-sm);font-size:13.5px;font-weight:600;cursor:pointer;transition:all .15s;border:none;font-family:'Outfit',sans-serif}
.btn-primary{background:var(--accent);color:#fff}
.btn-primary:hover{background:var(--accent2)}
.btn-ghost{background:transparent;border:1px solid var(--border2);color:var(--text2)}
.btn-ghost:hover{color:var(--text);background:var(--accent-dim)}

/* ── Forms ── */
.form-group{margin-bottom:14px}
.form-label{font-size:12px;font-weight:600;color:var(--text2);text-transform:uppercase;letter-spacing:.07em;display:block;margin-bottom:6px}
.form-input,.form-select,.form-textarea{width:100%;background:var(--bg3);border:1px solid var(--border2);border-radius:var(--r-sm);color:var(--text);font-family:'Outfit',sans-serif;font-size:14px;padding:9px 12px;outline:none;transition:border-color .15s}
.form-input:focus,.form-select:focus,.form-textarea:focus{border-color:var(--accent)}
.form-select option{background:var(--card2)}
.form-textarea{resize:vertical;min-height:70px}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.form-actions{display:flex;gap:10px;justify-content:flex-end;margin-top:20px}
.stars{display:flex;gap:5px;align-items:center;flex-wrap:wrap}
.star{font-size:22px;cursor:pointer;color:var(--text3);transition:color .1s}
.star.lit{color:var(--yellow)}
.star.global-star{font-size:18px;padding:3px 10px;border-radius:20px;background:var(--red-dim);color:var(--red);border:1px solid rgba(248,113,113,0.3);font-family:'Outfit',sans-serif;font-weight:700;letter-spacing:.03em;cursor:pointer;transition:all .15s}
.star.global-star.lit{background:var(--red);color:#fff}

/* ── Hours estimate bubble ── */
.hrs-estimate{background:var(--accent-dim);border:1px solid var(--border2);border-radius:var(--r-sm);padding:10px 14px;font-size:13px;color:var(--accent);margin-top:8px;display:none}
.hrs-estimate strong{font-weight:700}
.hrs-estimate.global-est{background:var(--red-dim);border-color:rgba(248,113,113,0.3);color:var(--red)}

/* ── Modal ── */
.modal-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:100;align-items:center;justify-content:center}
.modal-overlay.open{display:flex}
.modal{background:var(--card2);border:1px solid var(--border2);border-radius:16px;padding:28px;width:100%;max-width:500px;max-height:90vh;overflow-y:auto}
.modal-title{font-size:18px;font-weight:800;margin-bottom:20px}

/* ── Plan ── */
.plan-day{margin-bottom:10px}
.plan-day-hdr{display:flex;align-items:center;gap:10px;padding:10px 14px;background:var(--card);border:1px solid var(--border);border-radius:var(--r-sm) var(--r-sm) 0 0;font-size:13px;font-weight:600}
.plan-day-date{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--text3)}
.plan-day-hrs{margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--accent)}
.plan-session{padding:8px 14px 8px 26px;background:var(--card2);border:1px solid var(--border);border-top:none;font-size:13px;display:flex;gap:8px;align-items:center}
.plan-session:last-child{border-radius:0 0 var(--r-sm) var(--r-sm)}
.plan-dot{width:6px;height:6px;border-radius:50%;background:var(--accent);flex-shrink:0}
.plan-mat{color:var(--text2);font-size:12px}
.plan-hrs{margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--text2)}

/* ── Apuntes ── */
.apunte-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r-sm);padding:14px 16px;margin-bottom:8px}
.apunte-hdr{display:flex;align-items:flex-start;gap:8px;margin-bottom:6px;flex-wrap:wrap}
.apunte-titulo{font-size:14px;font-weight:600;flex:1}

/* ── Apunte type selector ── */
.type-grid{display:flex;flex-direction:column;gap:8px}
.type-btn{display:flex;align-items:center;gap:14px;padding:14px 16px;border-radius:var(--r-sm);border:1px solid var(--border2);background:transparent;cursor:pointer;text-align:left;font-family:'Outfit',sans-serif;transition:all .15s;color:var(--text)}
.type-btn:hover{border-color:var(--accent);background:var(--accent-dim)}
.type-btn .type-ico{font-size:24px;width:32px;text-align:center;flex-shrink:0}
.type-btn .type-lbl{font-size:14px;font-weight:600;color:var(--text)}
.type-btn .type-sub{font-size:12px;color:var(--text3);margin-top:2px}

/* ── File dropzone ── */
.dropzone{border:1.5px dashed var(--border2);border-radius:var(--r-sm);padding:28px;text-align:center;cursor:pointer;transition:border-color .15s}
.dropzone:hover,.dropzone.over{border-color:var(--accent);background:var(--accent-dim)}

/* ── Horas modal ── */
.horas-range{width:100%;accent-color:var(--accent);cursor:pointer}
.horas-display{font-size:36px;font-weight:800;color:var(--accent);text-align:center;margin:10px 0;font-family:'Outfit',sans-serif}

/* ── Onboarding horas grid ── */
.horas-dia-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.horas-dia-row{display:flex;align-items:center;gap:8px}
.horas-dia-lbl{font-size:13px;color:var(--text2);width:36px;flex-shrink:0}

/* ── Perfil ── */
.perfil-section{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:20px;margin-bottom:16px;max-width:560px}
.perfil-sec-title{font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:.08em;color:var(--text2);margin-bottom:16px}

/* ── Empty ── */
.empty{text-align:center;padding:48px 0;color:var(--text3);font-size:14px}
.empty-ico{font-size:32px;margin-bottom:10px}

/* ══ CALENDARIO ══ */
.cal-wrap{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:20px;margin-bottom:16px}
.cal-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.cal-title{font-size:16px;font-weight:700}
.cal-nav{display:flex;gap:8px}
.cal-nav button{background:var(--bg3);border:1px solid var(--border2);color:var(--text2);width:30px;height:30px;border-radius:var(--r-sm);cursor:pointer;font-size:14px;transition:all .15s}
.cal-nav button:hover{color:var(--text);background:var(--accent-dim)}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px}
.cal-dow{font-size:11px;text-transform:uppercase;letter-spacing:.06em;color:var(--text3);text-align:center;padding:4px 0 8px;font-weight:600}
.cal-cell{min-height:64px;background:var(--bg3);border:1px solid var(--border);border-radius:6px;padding:4px 5px;cursor:pointer;transition:border-color .15s;position:relative}
.cal-cell:hover{border-color:var(--border2)}
.cal-cell.today{border-color:var(--accent);background:var(--accent-dim)}
.cal-cell.other-month{opacity:.35}
.cal-cell.has-tasks{border-color:rgba(168,85,247,0.4)}
.cal-day-num{font-size:11px;font-weight:700;color:var(--text2);margin-bottom:3px}
.cal-cell.today .cal-day-num{color:var(--accent)}
.cal-dot-row{display:flex;flex-wrap:wrap;gap:2px;margin-top:2px}
.cal-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0}
.cal-task-pill{font-size:9px;font-weight:600;border-radius:3px;padding:1px 4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:100%;display:block;margin-bottom:1px}
.cal-tooltip{position:fixed;background:var(--card2);border:1px solid var(--border2);border-radius:var(--r-sm);padding:10px 12px;font-size:12px;z-index:200;pointer-events:none;min-width:160px;max-width:220px;box-shadow:0 8px 24px rgba(0,0,0,.5)}
.cal-tooltip-item{padding:3px 0;border-bottom:1px solid var(--border);color:var(--text2)}
.cal-tooltip-item:last-child{border-bottom:none}
.cal-tooltip-item strong{color:var(--text);display:block}

/* ══ GRÁFICAS ══ */
.stats-charts-row{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:16px}
.chart-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:20px}
.chart-title{font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:.08em;color:var(--text2);margin-bottom:16px}
.bar-chart{display:flex;align-items:flex-end;gap:6px;height:100px}
.bar-wrap{display:flex;flex-direction:column;align-items:center;gap:4px;flex:1}
.bar{width:100%;border-radius:3px 3px 0 0;transition:height .3s;position:relative;min-height:2px}
.bar-lbl{font-size:9px;color:var(--text3);font-family:'JetBrains Mono',monospace;white-space:nowrap}
.bar-val{font-size:9px;color:var(--text2);font-family:'JetBrains Mono',monospace}
.streak-row{display:flex;gap:8px;flex-wrap:wrap}
.streak-day{width:28px;height:28px;border-radius:5px;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;font-family:'JetBrains Mono',monospace;transition:transform .15s}
.streak-day:hover{transform:scale(1.15)}
.sd-none{background:var(--bg3);color:var(--text3)}
.sd-ok{background:var(--green-dim);color:var(--green);border:1px solid rgba(52,211,153,.3)}
.sd-crush{background:var(--accent);color:#fff;box-shadow:0 0 8px rgba(168,85,247,.5)}
.sd-miss{background:var(--red-dim);color:var(--red);border:1px solid rgba(248,113,113,.2)}
.legend-row{display:flex;gap:12px;flex-wrap:wrap;margin-top:12px}
.legend-item{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--text3)}
.legend-dot{width:10px;height:10px;border-radius:3px;flex-shrink:0}

/* ── log sesion (registrar horas y si fue dia de estudio) ── */
.log-form{display:flex;flex-direction:column;gap:10px;margin-top:12px;padding:14px;background:var(--bg3);border-radius:var(--r-sm);border:1px solid var(--border)}
.log-form-title{font-size:12px;font-weight:700;text-transform:uppercase;letter-spacing:.06em;color:var(--text2)}
</style>
</head>
<body>

<!-- ══════════════ AUTH ══════════════ -->
<div id="auth-screen">
  <div class="auth-wrap">
    <div class="auth-bg"></div>
    <div class="auth-card">
      <div class="auth-logo">Agent<span>Plan</span></div>
      <div class="auth-tagline">Tu planificador de estudios inteligente</div>
      <div class="auth-tabs">
        <div class="auth-tab active" onclick="switchTab('login')">Iniciar sesión</div>
        <div class="auth-tab" onclick="switchTab('registro')">Registrarse</div>
      </div>
      <div id="tab-login">
        <div class="form-group">
          <label class="form-label">Usuario</label>
          <input class="form-input" id="l-user" placeholder="Tu usuario" />
        </div>
        <div class="form-group">
          <label class="form-label">Contraseña</label>
          <input class="form-input" id="l-pass" type="password" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()" />
        </div>
        <div id="l-error" style="color:var(--red);font-size:13px;margin-bottom:10px;display:none"></div>
        <button class="btn btn-primary" style="width:100%;justify-content:center" onclick="doLogin()">Entrar →</button>
      </div>
      <div id="tab-registro" style="display:none">
        <div class="form-group">
          <label class="form-label">¿Cómo te llamas?</label>
          <input class="form-input" id="r-nombre" placeholder="Tu nombre" />
        </div>
        <div class="form-group">
          <label class="form-label">Elige un usuario</label>
          <input class="form-input" id="r-user" placeholder="Ej: maria92" />
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Contraseña</label>
            <input class="form-input" id="r-pass" type="password" placeholder="••••••••" />
          </div>
          <div class="form-group">
            <label class="form-label">Confirmar</label>
            <input class="form-input" id="r-pass2" type="password" placeholder="••••••••" />
          </div>
        </div>
        <div id="r-error" style="color:var(--red);font-size:13px;margin-bottom:10px;display:none"></div>
        <button class="btn btn-primary" style="width:100%;justify-content:center" onclick="doRegistro()">Crear cuenta →</button>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════ ONBOARDING ══════════════ -->
<div id="onboarding-screen" style="display:none">
  <div class="auth-wrap">
    <div class="auth-bg"></div>
    <div class="auth-card" style="max-width:500px">
      <div id="ob-step1">
        <div class="auth-logo" style="margin-bottom:4px">Agent<span style="color:var(--text3);font-weight:300">Plan</span></div>
        <div style="font-size:15px;color:var(--text2);margin-bottom:24px">Un par de preguntas para personalizar tu plan 🎓</div>
        <div class="form-group">
          <label class="form-label">¿Cómo prefieres distribuir el estudio?</label>
          <select class="form-select" id="ob-estilo">
            <option value="uniforme">Distribuido uniformemente</option>
            <option value="intensivo">Intensivo al principio</option>
            <option value="ultima_hora">Más al final (última hora)</option>
          </select>
        </div>
        <button class="btn btn-primary" style="width:100%;justify-content:center;margin-top:4px" onclick="obNext()">Siguiente →</button>
      </div>
      <div id="ob-step2" style="display:none">
        <div style="font-size:18px;font-weight:800;margin-bottom:6px">¿Cuántas horas puedes estudiar cada día?</div>
        <div style="font-size:13px;color:var(--text2);margin-bottom:20px">Pon <strong>0</strong> en los días que no puedes estudiar.</div>
        <div class="horas-dia-grid" id="ob-horas-grid">
          <div class="horas-dia-row"><span class="horas-dia-lbl">Lunes</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="4" data-dia="0"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Martes</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="4" data-dia="1"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Miérc.</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="4" data-dia="2"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Jueves</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="4" data-dia="3"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Viernes</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="4" data-dia="4"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Sábado</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="0" data-dia="5"/></div>
          <div class="horas-dia-row"><span class="horas-dia-lbl">Domingo</span><input class="form-input" type="number" min="0" max="16" step="0.5" value="0" data-dia="6"/></div>
        </div>
        <div style="display:flex;gap:10px;margin-top:24px">
          <button class="btn btn-ghost" onclick="obBack()">← Atrás</button>
          <button class="btn btn-primary" style="flex:1;justify-content:center" onclick="obFinish()">¡Empezar! 🚀</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════ APP ══════════════ -->
<div class="shell" id="app" style="display:none">
  <nav class="sidebar">
    <div class="logo-wrap">
      <div class="logo-name">AgentPlan</div>
      <div class="logo-user" id="sb-user">—</div>
    </div>
    <div class="nav">
      <div class="nav-sec">Principal</div>
      <div class="nav-item active" onclick="showPage('dashboard',this)"><span class="ico">⬛</span>Dashboard</div>
      <div class="nav-item" onclick="showPage('tareas',this)"><span class="ico">✓</span>Tareas</div>
      <div class="nav-item" onclick="showPage('plan',this)"><span class="ico">📅</span>Plan de estudio</div>
      <div class="nav-item" onclick="showPage('calendario',this)"><span class="ico">🗓</span>Calendario</div>
      <div class="nav-sec">Estadísticas</div>
      <div class="nav-item" onclick="showPage('estadisticas',this)"><span class="ico">📊</span>Mis estadísticas</div>
      <div class="nav-sec">Contenido</div>
      <div class="nav-item" onclick="showPage('apuntes',this)"><span class="ico">📝</span>Apuntes</div>
      <div class="nav-sec">Cuenta</div>
      <div class="nav-item" onclick="showPage('perfil',this)"><span class="ico">⚙</span>Perfil</div>
    </div>
    <div class="logout-btn" onclick="doLogout()"><span>🚪</span>Cerrar sesión</div>
  </nav>
  <main class="main">

    <!-- DASHBOARD -->
    <div class="page active" id="page-dashboard">
      <div class="page-hdr"><div class="page-hdr-left"><div class="page-title" id="dash-saludo"></div><div class="page-sub" id="dash-fecha"></div></div></div>
      <div class="stats-row">
        <div class="stat-card"><div class="stat-lbl">Pendientes</div><div class="stat-num" id="s-pend">0</div></div>
        <div class="stat-card"><div class="stat-lbl">Urgentes ≤2d</div><div class="stat-num rd" id="s-urg">0</div></div>
        <div class="stat-card"><div class="stat-lbl">Próxima entrega</div><div class="stat-num yl" id="s-prox" style="font-size:15px;padding-top:7px">—</div></div>
        <div class="stat-card"><div class="stat-lbl">Completadas</div><div class="stat-num ac" id="s-comp">0</div></div>
      </div>
      <div class="card"><div class="card-title">Tareas más urgentes</div><div id="dash-tareas"></div></div>
      <div class="card"><div class="card-title">Hoy en tu plan</div><div id="dash-hoy"></div></div>
    </div>

    <!-- TAREAS -->
    <div class="page" id="page-tareas">
      <div class="page-hdr">
        <div class="page-hdr-left"><div class="page-title">Tareas</div><div class="page-sub">Gestiona entregas y proyectos</div></div>
        <button class="btn btn-primary" onclick="openModal('modal-tarea')">+ Nueva tarea</button>
      </div>
      <div id="lista-tareas"></div>
    </div>

    <!-- PLAN -->
    <div class="page" id="page-plan">
      <div class="page-hdr"><div class="page-hdr-left"><div class="page-title">Plan de estudio</div><div class="page-sub">Próximos 14 días según tu disponibilidad</div></div></div>
      <div id="plan-cont"></div>
    </div>

    <!-- CALENDARIO -->
    <div class="page" id="page-calendario">
      <div class="page-hdr"><div class="page-hdr-left"><div class="page-title">Calendario</div><div class="page-sub">Visualiza tus entregas y sesiones de estudio</div></div></div>
      <div class="cal-wrap">
        <div class="cal-header">
          <div class="cal-title" id="cal-month-title">—</div>
          <div class="cal-nav">
            <button onclick="calPrev()">‹</button>
            <button onclick="calToday()">Hoy</button>
            <button onclick="calNext()">›</button>
          </div>
        </div>
        <div class="cal-grid" id="cal-grid"></div>
      </div>
      <div id="cal-tooltip" class="cal-tooltip" style="display:none"></div>
    </div>

    <!-- ESTADÍSTICAS -->
    <div class="page" id="page-estadisticas">
      <div class="page-hdr">
        <div class="page-hdr-left"><div class="page-title">Mis estadísticas</div><div class="page-sub">Seguimiento de tus horas de estudio</div></div>
        <button class="btn btn-primary" onclick="openModal('modal-log-dia')">+ Registrar día</button>
      </div>
      <div class="stats-charts-row">
        <div class="chart-card">
          <div class="chart-title">Horas estudiadas — últimas 2 semanas</div>
          <div class="bar-chart" id="bar-chart"></div>
        </div>
        <div class="chart-card">
          <div class="chart-title">Racha de días — últimas 4 semanas</div>
          <div class="streak-row" id="streak-row"></div>
          <div class="legend-row">
            <div class="legend-item"><div class="legend-dot" style="background:var(--bg3)"></div>Sin datos</div>
            <div class="legend-item"><div class="legend-dot sd-ok"></div>Objetivo ✓</div>
            <div class="legend-item"><div class="legend-dot" style="background:var(--accent)"></div>¡Arrasaste! 🔥</div>
            <div class="legend-item"><div class="legend-dot sd-miss"></div>Por debajo</div>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">Resumen</div>
        <div id="stats-resumen" style="display:grid;grid-template-columns:repeat(3,1fr);gap:12px"></div>
      </div>
      <div class="card">
        <div class="card-title">Historial de días registrados</div>
        <div id="stats-historial"></div>
      </div>
    </div>

    <!-- APUNTES -->
    <div class="page" id="page-apuntes">
      <div class="page-hdr">
        <div class="page-hdr-left"><div class="page-title">Apuntes</div><div class="page-sub">Notas, imágenes y documentos</div></div>
        <button class="btn btn-primary" onclick="abrirModalApunte()">+ Nuevo apunte</button>
      </div>
      <div id="lista-apuntes"></div>
    </div>

    <!-- PERFIL -->
    <div class="page" id="page-perfil">
      <div class="page-hdr"><div class="page-hdr-left"><div class="page-title">Perfil</div><div class="page-sub">Tus preferencias de estudio</div></div></div>
      <div class="perfil-section">
        <div class="perfil-sec-title">Datos personales</div>
        <div class="form-group"><label class="form-label">Nombre</label><input class="form-input" id="p-nombre"/></div>
        <div class="form-group"><label class="form-label">Contraseña actual</label><input class="form-input" id="p-pass-actual" type="password" placeholder="Dejar vacío si no cambias"/></div>
        <div class="form-row">
          <div class="form-group"><label class="form-label">Nueva contraseña</label><input class="form-input" id="p-pass-nueva" type="password" placeholder="••••••••"/></div>
          <div class="form-group"><label class="form-label">Confirmar</label><input class="form-input" id="p-pass-conf" type="password" placeholder="••••••••"/></div>
        </div>
      </div>
      <div class="perfil-section">
        <div class="perfil-sec-title">Horario de estudio</div>
        <div class="form-group"><label class="form-label">¿Cuántas horas puedes estudiar cada día? (0 = no disponible)</label>
          <div class="horas-dia-grid" id="p-horas-grid">
            <div class="horas-dia-row"><span class="horas-dia-lbl">Lunes</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="0"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Martes</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="1"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Miérc.</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="2"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Jueves</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="3"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Viernes</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="4"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Sábado</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="5"/></div>
            <div class="horas-dia-row"><span class="horas-dia-lbl">Domingo</span><input class="form-input" type="number" min="0" max="16" step="0.5" data-dia="6"/></div>
          </div>
        </div>
        <div class="form-group"><label class="form-label">Estilo de estudio</label>
          <select class="form-select" id="p-estilo">
            <option value="uniforme">Distribuido uniformemente</option>
            <option value="intensivo">Intensivo al principio</option>
            <option value="ultima_hora">Última hora</option>
          </select>
        </div>
        <button class="btn btn-primary" onclick="guardarPerfil()">Guardar cambios</button>
      </div>
    </div>

  </main>
</div>

<!-- ═══ MODAL: Nueva tarea ═══ -->
<div class="modal-overlay" id="modal-tarea">
  <div class="modal">
    <div class="modal-title">Nueva tarea</div>
    <div class="form-row">
      <div class="form-group"><label class="form-label">Nombre</label><input class="form-input" id="t-nombre" placeholder="Ej: Parcial de Química"/></div>
      <div class="form-group"><label class="form-label">Materia</label><input class="form-input" id="t-materia" placeholder="Ej: Química"/></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label class="form-label">Tipo</label>
        <select class="form-select" id="t-tipo" onchange="recalcEstimate()">
          <option value="Examen">Examen</option>
          <option value="Proyecto">Proyecto</option>
          <option value="Lectura">Lectura/Libro</option>
          <option value="Trabajo">Trabajo escrito</option>
          <option value="Tarea">Tarea puntual</option>
          <option value="Otro">Otro</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Fecha de entrega</label><input class="form-input" id="t-fecha" type="date" onchange="recalcEstimate()"/></div>
    </div>
    <div class="form-group" id="grp-paginas" style="display:none">
      <label class="form-label">Número de páginas</label>
      <input class="form-input" id="t-paginas" type="number" min="1" placeholder="Ej: 250" oninput="recalcEstimate()"/>
    </div>
    <div class="form-group">
      <label class="form-label">Dificultad</label>
      <div class="stars" id="t-stars">
        <span class="star" data-v="1" onclick="setDiff(1)">★</span>
        <span class="star" data-v="2" onclick="setDiff(2)">★</span>
        <span class="star" data-v="3" onclick="setDiff(3)">★</span>
        <span class="star" data-v="4" onclick="setDiff(4)">★</span>
        <span class="star" data-v="5" onclick="setDiff(5)">★</span>
        <span class="star global-star" data-v="6" id="star-global" onclick="setDiff(6)" title="Examen global: muchísimo contenido">🌍 Global</span>
      </div>
      <div style="font-size:11px;color:var(--text3);margin-top:5px" id="diff-hint">Dificultad normal</div>
    </div>
    <div class="hrs-estimate" id="hrs-estimate">
      🧠 Estimación: <strong id="est-horas">—</strong> horas totales · <strong id="est-desc">—</strong>
    </div>
    <div class="form-group" style="margin-top:14px">
      <label class="form-label">Notas (opcional)</label>
      <textarea class="form-textarea" id="t-notas" placeholder="Temas, recursos..."></textarea>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-tarea')">Cancelar</button>
      <button class="btn btn-primary" onclick="guardarTarea()">Guardar tarea</button>
    </div>
  </div>
</div>

<!-- ═══ MODAL: Registrar horas ═══ -->
<div class="modal-overlay" id="modal-horas">
  <div class="modal" style="max-width:380px">
    <div class="modal-title">Registrar horas estudiadas</div>
    <div style="font-size:14px;color:var(--text2);margin-bottom:14px" id="h-tarea-nombre"></div>
    <div class="horas-display" id="h-display">2h</div>
    <input type="range" class="horas-range" id="h-slider" min="0.5" max="12" step="0.5" value="2" oninput="document.getElementById('h-display').textContent=this.value+'h'"/>
    <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--text3);margin-top:4px"><span>0.5h</span><span>12h</span></div>
    <div class="form-actions"><button class="btn btn-ghost" onclick="closeModal('modal-horas')">Cancelar</button><button class="btn btn-primary" onclick="guardarHoras()">Registrar</button></div>
  </div>
</div>

<!-- ═══ MODAL: Registrar día de estudio ═══ -->
<div class="modal-overlay" id="modal-log-dia">
  <div class="modal" style="max-width:400px">
    <div class="modal-title">Registrar día de estudio</div>
    <div class="form-group">
      <label class="form-label">Fecha</label>
      <input class="form-input" id="ld-fecha" type="date"/>
    </div>
    <div class="form-group">
      <label class="form-label">Horas estudiadas ese día</label>
      <div class="horas-display" id="ld-display">2h</div>
      <input type="range" class="horas-range" id="ld-slider" min="0" max="16" step="0.5" value="2" oninput="document.getElementById('ld-display').textContent=this.value+'h'"/>
      <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--text3);margin-top:4px"><span>0h</span><span>16h</span></div>
    </div>
    <div class="form-actions">
      <button class="btn btn-ghost" onclick="closeModal('modal-log-dia')">Cancelar</button>
      <button class="btn btn-primary" onclick="guardarLogDia()">Guardar</button>
    </div>
  </div>
</div>

<!-- ═══ MODAL: Apunte ═══ -->
<div class="modal-overlay" id="modal-apunte">
  <div class="modal">
    <div id="ap-step1">
      <div class="modal-title">Nuevo apunte</div>
      <div style="font-size:13px;color:var(--text2);margin-bottom:18px">¿Qué tipo de apunte quieres añadir?</div>
      <div class="type-grid">
        <button class="type-btn" onclick="elegirTipoAp('texto')">
          <span class="type-ico">✍️</span>
          <div><div class="type-lbl">Texto</div><div class="type-sub">Escribe notas directamente</div></div>
        </button>
        <button class="type-btn" onclick="elegirTipoAp('imagen')">
          <span class="type-ico">🖼️</span>
          <div><div class="type-lbl">Imagen o foto</div><div class="type-sub">Sube una captura, foto o imagen</div></div>
        </button>
        <button class="type-btn" onclick="elegirTipoAp('documento')">
          <span class="type-ico">📄</span>
          <div><div class="type-lbl">Documento o archivo</div><div class="type-sub">PDF, Word, PowerPoint, etc.</div></div>
        </button>
      </div>
      <div class="form-actions"><button class="btn btn-ghost" onclick="closeModal('modal-apunte')">Cancelar</button></div>
    </div>
    <div id="ap-step2" style="display:none">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:20px">
        <button onclick="apBack()" style="background:none;border:none;color:var(--text2);cursor:pointer;font-size:20px;line-height:1">←</button>
        <div class="modal-title" style="margin-bottom:0" id="ap-title">Nuevo apunte</div>
        <span id="ap-badge" class="badge b-accent" style="margin-left:auto"></span>
      </div>
      <div class="form-row">
        <div class="form-group"><label class="form-label">Materia</label><input class="form-input" id="a-materia" placeholder="Ej: Física"/></div>
        <div class="form-group"><label class="form-label">Título</label><input class="form-input" id="a-titulo" placeholder="Ej: Leyes de Newton"/></div>
      </div>
      <div class="form-group">
        <label class="form-label">Asociar a una tarea (opcional)</label>
        <select class="form-select" id="a-tarea-id"><option value="">Sin asociar</option></select>
      </div>
      <div id="ap-campo-texto">
        <div class="form-group"><label class="form-label">Contenido</label><textarea class="form-textarea" id="a-contenido" style="min-height:120px" placeholder="Escribe tus notas..."></textarea></div>
      </div>
      <div id="ap-campo-imagen" style="display:none">
        <div class="form-group">
          <label class="form-label">Imagen o foto</label>
          <div class="dropzone" id="img-dz" onclick="document.getElementById('a-img-inp').click()" ondragover="dzOver(event,'img-dz')" ondragleave="dzLeave('img-dz')" ondrop="handleImgDrop(event)">
            <div style="font-size:28px;margin-bottom:8px">🖼️</div>
            <div style="font-size:13px;color:var(--text2)">Haz clic o arrastra aquí</div>
            <div style="font-size:11px;color:var(--text3);margin-top:3px">JPG, PNG, GIF, WebP</div>
          </div>
          <input type="file" id="a-img-inp" accept="image/*" style="display:none" onchange="previewImg(this)"/>
          <div id="img-preview" style="display:none;margin-top:10px;position:relative">
            <img id="img-prev-img" style="max-width:100%;max-height:200px;border-radius:var(--r-sm);border:1px solid var(--border)"/>
            <button onclick="clearImg()" style="position:absolute;top:6px;right:6px;background:rgba(0,0,0,.6);border:none;color:#fff;width:22px;height:22px;border-radius:50%;cursor:pointer;font-size:13px">✕</button>
          </div>
        </div>
      </div>
      <div id="ap-campo-doc" style="display:none">
        <div class="form-group">
          <label class="form-label">Documento o archivo</label>
          <div class="dropzone" id="doc-dz" onclick="document.getElementById('a-doc-inp').click()" ondragover="dzOver(event,'doc-dz')" ondragleave="dzLeave('doc-dz')" ondrop="handleDocDrop(event)">
            <div style="font-size:28px;margin-bottom:8px">📄</div>
            <div style="font-size:13px;color:var(--text2)">Haz clic o arrastra aquí</div>
            <div style="font-size:11px;color:var(--text3);margin-top:3px">PDF, DOC, DOCX, PPTX, XLS…</div>
          </div>
          <input type="file" id="a-doc-inp" style="display:none" onchange="previewDoc(this)"/>
          <div id="doc-preview" style="display:none;margin-top:10px;align-items:center;gap:10px;background:var(--bg3);border-radius:var(--r-sm);padding:10px 14px">
            <span style="font-size:22px" id="doc-ico">📄</span>
            <div style="flex:1;min-width:0"><div style="font-size:13px;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap" id="doc-name"></div><div style="font-size:11px;color:var(--text3)" id="doc-size"></div></div>
            <button onclick="clearDoc()" style="background:none;border:none;color:var(--text3);cursor:pointer;font-size:16px">✕</button>
          </div>
          <div class="form-group" style="margin-top:10px;margin-bottom:0"><label class="form-label">Descripción (opcional)</label><textarea class="form-textarea" id="a-doc-desc" style="min-height:55px" placeholder="¿De qué trata este documento?"></textarea></div>
        </div>
      </div>
      <div class="form-actions">
        <button class="btn btn-ghost" onclick="closeModal('modal-apunte')">Cancelar</button>
        <button class="btn btn-primary" onclick="guardarApunte()">Guardar apunte</button>
      </div>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════════════════
// STORAGE — FIX: clave por usuario, sin sessionStorage para el login
// ══════════════════════════════════════════════
const STORE_KEY = 'agentplan_db';
const SESSION_KEY = 'agentplan_session';
let db = {};
let currentUser = null;
let D = null;

function loadDB(){ try{ const r=localStorage.getItem(STORE_KEY); if(r) db=JSON.parse(r); }catch(e){ db={}; } }
function saveDB(){ localStorage.setItem(STORE_KEY,JSON.stringify(db)); }
function saveD(){ saveDB(); }

loadDB();

// FIX: usar localStorage para la sesión (sessionStorage se borra al cerrar la pestaña pero también en algunos contextos de recarga)
const sessionUser = localStorage.getItem(SESSION_KEY);
if(sessionUser && db[sessionUser]){
  currentUser=sessionUser; D=db[currentUser];
  if(!D.perfil){ showOnboarding(); } else { showApp(); }
} else {
  document.getElementById('auth-screen').style.display='block';
}

// ══════════════ AUTH ══════════════
function switchTab(tab){
  ['login','registro'].forEach(t=>{
    document.getElementById('tab-'+t).style.display=t===tab?'block':'none';
  });
  document.querySelectorAll('.auth-tab').forEach((el,i)=>{
    el.classList.toggle('active',(i===0&&tab==='login')||(i===1&&tab==='registro'));
  });
}
function showErr(id,msg){ const el=document.getElementById(id); el.textContent=msg; el.style.display=msg?'block':'none'; }

function doLogin(){
  const u=document.getElementById('l-user').value.trim();
  const p=document.getElementById('l-pass').value;
  if(!u||!p){ showErr('l-error','Completa todos los campos'); return; }
  if(!db[u]){ showErr('l-error','Usuario no encontrado'); return; }
  if(db[u].pass!==btoa(p)){ showErr('l-error','Contraseña incorrecta'); return; }
  currentUser=u; D=db[u];
  localStorage.setItem(SESSION_KEY,u); // FIX: localStorage en vez de sessionStorage
  showErr('l-error','');
  document.getElementById('auth-screen').style.display='none';
  if(!D.perfil){ showOnboarding(); } else { showApp(); }
}

function doRegistro(){
  const nombre=document.getElementById('r-nombre').value.trim();
  const u=document.getElementById('r-user').value.trim().toLowerCase().replace(/\s+/g,'');
  const p=document.getElementById('r-pass').value;
  const p2=document.getElementById('r-pass2').value;
  if(!nombre||!u||!p){ showErr('r-error','Completa todos los campos'); return; }
  if(p.length<4){ showErr('r-error','La contraseña debe tener al menos 4 caracteres'); return; }
  if(p!==p2){ showErr('r-error','Las contraseñas no coinciden'); return; }
  if(db[u]){ showErr('r-error','Ese usuario ya existe'); return; }
  db[u]={ pass:btoa(p), nombre, perfil:null, tareas:[], apuntes:[], logsEstudio:[] };
  saveDB();
  currentUser=u; D=db[u];
  localStorage.setItem(SESSION_KEY,u);
  showErr('r-error','');
  document.getElementById('auth-screen').style.display='none';
  showOnboarding();
}

function doLogout(){
  localStorage.removeItem(SESSION_KEY);
  currentUser=null; D=null;
  location.reload();
}

// ══════════════ ONBOARDING ══════════════
function showOnboarding(){ document.getElementById('onboarding-screen').style.display='flex'; }
function obNext(){ document.getElementById('ob-step1').style.display='none'; document.getElementById('ob-step2').style.display='block'; }
function obBack(){ document.getElementById('ob-step2').style.display='none'; document.getElementById('ob-step1').style.display='block'; }
function getHorasDiaGrid(gridId){
  const arr=[0,0,0,0,0,0,0];
  document.querySelectorAll('#'+gridId+' input[data-dia]').forEach(inp=>{ arr[parseInt(inp.dataset.dia)]=parseFloat(inp.value)||0; });
  return arr;
}
function obFinish(){
  D.perfil={ estilo:document.getElementById('ob-estilo').value, horas_dia:getHorasDiaGrid('ob-horas-grid') };
  if(!D.logsEstudio) D.logsEstudio=[];
  saveD();
  document.getElementById('onboarding-screen').style.display='none';
  showApp();
}

// ══════════════ APP ══════════════
function showApp(){
  document.getElementById('app').style.display='flex';
  document.getElementById('sb-user').textContent=D.nombre;
  if(!D.logsEstudio) D.logsEstudio=[];
  const h=new Date().getHours();
  document.getElementById('dash-saludo').textContent=(h<13?'Buenos días, ':h<20?'Buenas tardes, ':'Buenas noches, ')+D.nombre+' 👋';
  document.getElementById('dash-fecha').textContent=new Date().toLocaleDateString('es-ES',{weekday:'long',year:'numeric',month:'long',day:'numeric'});
  renderDashboard();
}

// ══════════════ NAV ══════════════
function showPage(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  if(el) el.classList.add('active');
  if(id==='dashboard') renderDashboard();
  if(id==='tareas') renderTareas();
  if(id==='plan') renderPlan();
  if(id==='calendario') renderCalendario();
  if(id==='estadisticas') renderEstadisticas();
  if(id==='apuntes') renderApuntes();
  if(id==='perfil') renderPerfil();
}

// ══════════════ MODAL ══════════════
function openModal(id){ document.getElementById(id).classList.add('open'); }
function closeModal(id){
  document.getElementById(id).classList.remove('open');
  if(id==='modal-apunte') resetApModal();
}
document.querySelectorAll('.modal-overlay').forEach(m=>m.addEventListener('click',e=>{ if(e.target===m){ m.classList.remove('open'); if(m.id==='modal-apunte') resetApModal(); }}));

// ══════════════ UTILS ══════════════
const DIAS_FULL=['Lunes','Martes','Miércoles','Jueves','Viernes','Sábado','Domingo'];
const DIAS_SHORT=['Lu','Ma','Mi','Ju','Vi','Sá','Do'];
function today(){ return new Date(); }
function todayStr(){ return today().toISOString().slice(0,10); }
function parseDate(s){ return new Date(s+'T12:00:00'); }
function fmtDate(s){ return parseDate(s).toLocaleDateString('es-ES',{day:'numeric',month:'short'}); }
function daysUntil(s){ return Math.ceil((parseDate(s)-today())/86400000); }
function urgBadge(d){
  if(d<=0) return '<span class="badge b-red">Vencida</span>';
  if(d<=2) return '<span class="badge b-red">'+d+'d</span>';
  if(d<=7) return '<span class="badge b-yellow">'+d+'d</span>';
  return '<span class="badge b-green">'+d+'d</span>';
}
function diffDots(n){
  // n=6 means "Global"
  if(n===6){
    return '<div class="diff-dots">'+Array(5).fill(0).map((_,i)=>`<div class="diff-dot lit global"></div>`).join('')+'</div>';
  }
  let h='<div class="diff-dots">';
  for(let i=1;i<=5;i++) h+=`<div class="diff-dot${i<=n?' lit':''}"></div>`;
  return h+'</div>';
}
function pct(t){ return t.h_total?Math.round((t.h_done||0)/t.h_total*100):0; }
function fmtSize(b){ if(b<1024)return b+'B'; if(b<1048576)return(b/1024).toFixed(1)+'KB'; return(b/1048576).toFixed(1)+'MB'; }
function docIco(type){
  if(type.includes('pdf')) return '📕';
  if(type.includes('word')||type.includes('doc')) return '📘';
  if(type.includes('sheet')||type.includes('excel')||type.includes('csv')) return '📗';
  if(type.includes('presentation')||type.includes('ppt')) return '📙';
  if(type.includes('image')) return '🖼️';
  return '📄';
}
function getHorasDia(){ return Array.isArray(D.perfil.horas_dia)?D.perfil.horas_dia:[4,4,4,4,4,0,0]; }
function dowOf(date){ const d=date.getDay(); return d===0?6:d-1; } // 0=Mon..6=Sun

// ══════════════ HOUR ESTIMATION ENGINE ══════════════
// diff 1-5 normal, diff 6 = GLOBAL (examen con MUCHO contenido, ×2.5 de diff5)
const H_BASE = {
  Examen:   [4,6,10,15,22,55],   // [d1,d2,d3,d4,d5,dGlobal]
  Proyecto: [3,5,8,14,20,40],
  Trabajo:  [2,4,7,11,16,35],
  Tarea:    [0.5,1,2,3,5,10],
  Lectura:  [0,0,0,0,0,0],
  Otro:     [4,6,10,15,22,55],
};

function getCadencia(tipo,diff,hTotal,daysLeft){
  if(tipo==='Tarea'&&diff<6){ return {sesiones:1,desc:'Se puede hacer en una sola sesión'}; }
  if(tipo==='Proyecto'){
    const s=diff<=2?1:diff<=4?2:diff===5?3:5;
    return {sesiones:s,desc:`Concentrado en ${s} sesión${s>1?'es':''} intensiva${s>1?'s':''}`};
  }
  if(tipo==='Lectura'){
    const n=diff<=2?Math.ceil(hTotal/1.5):diff<=4?Math.ceil(hTotal/1.2):Math.ceil(hTotal);
    return {sesiones:n,desc:`Distribuido en ~${n} noches de lectura`};
  }
  if(tipo==='Trabajo'&&diff<6){ const s=diff<=2?2:diff<=3?3:4; return {sesiones:s,desc:`Planificado en ${s} sesiones de redacción`}; }
  if(diff===6){ return {sesiones:Math.min(21,daysLeft||21),desc:'Examen global: máxima distribución de sesiones, empieza ya 🚨'}; }
  const minDays=diff<=1?2:diff<=2?3:diff<=3?5:diff<=4?7:10;
  const d=Math.min(minDays,daysLeft||minDays);
  return {sesiones:d,desc:`Repartido en ~${d} días para consolidar memoria`};
}

let currentDiff=3;
let estimatedHours=0;
const DIFF_HINTS=['','Muy fácil — repaso rápido','Fácil — algo de trabajo','Normal — dedicación media','Difícil — requiere esfuerzo','Muy difícil — materia densa','🌍 GLOBAL — examen con todo el temario'];

function setDiff(v){
  currentDiff=v;
  document.querySelectorAll('#t-stars .star:not(.global-star)').forEach(s=>s.classList.toggle('lit',parseInt(s.dataset.v)<=v&&v<6));
  const gs=document.getElementById('star-global');
  if(gs) gs.classList.toggle('lit',v===6);
  const hint=document.getElementById('diff-hint');
  if(hint){ hint.textContent=DIFF_HINTS[v]||''; hint.style.color=v===6?'var(--red)':'var(--text3)'; }
  recalcEstimate();
}
setDiff(3);

function recalcEstimate(){
  const tipo=document.getElementById('t-tipo').value;
  const fecha=document.getElementById('t-fecha').value;
  const paginas=parseInt(document.getElementById('t-paginas').value)||0;
  document.getElementById('grp-paginas').style.display=(tipo==='Lectura'?'block':'none');
  const est=document.getElementById('hrs-estimate');
  if(!fecha){ est.style.display='none'; return; }
  const daysLeft=daysUntil(fecha);
  let hTotal;
  if(tipo==='Lectura'){
    if(!paginas){ est.style.display='none'; return; }
    const pgPerHr=[50,40,30,22,15,10][currentDiff-1];
    hTotal=Math.ceil(paginas/pgPerHr);
  } else {
    hTotal=H_BASE[tipo]?.[currentDiff-1]??H_BASE['Otro'][currentDiff-1];
  }
  const {desc}=getCadencia(tipo,currentDiff,hTotal,daysLeft);
  estimatedHours=hTotal;
  document.getElementById('est-horas').textContent=hTotal+'h';
  document.getElementById('est-desc').textContent=desc;
  est.style.display='block';
  est.className='hrs-estimate'+(currentDiff===6?' global-est':'');
}

// ══════════════ DASHBOARD ══════════════
function renderDashboard(){
  const pend=D.tareas.filter(t=>!t.done);
  const urg=pend.filter(t=>daysUntil(t.fecha)<=2);
  const comp=D.tareas.filter(t=>t.done);
  document.getElementById('s-pend').textContent=pend.length;
  document.getElementById('s-urg').textContent=urg.length;
  document.getElementById('s-comp').textContent=comp.length;
  const srt=[...pend].sort((a,b)=>new Date(a.fecha)-new Date(b.fecha));
  document.getElementById('s-prox').textContent=srt.length?fmtDate(srt[0].fecha):'—';
  const dt=document.getElementById('dash-tareas');
  const top3=srt.slice(0,3);
  dt.innerHTML=top3.length?top3.map(t=>taskHTML(t,true)).join(''):'<div class="empty"><div class="empty-ico">🎉</div>Sin tareas pendientes</div>';
  const plan=calcPlan();
  const hoyKey=todayStr();
  const ses=plan[hoyKey]||[];
  const el=document.getElementById('dash-hoy');
  if(!ses.length){ el.innerHTML='<div class="empty"><div>Sin sesiones planificadas hoy</div></div>'; return; }
  el.innerHTML=ses.map(s=>`<div style="display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--border)"><div class="plan-dot"></div><span style="font-size:14px;font-weight:500">${s.nombre}</span><span style="font-size:12px;color:var(--text2)">${s.materia}</span><span style="margin-left:auto;font-family:'JetBrains Mono',monospace;font-size:13px;color:var(--accent)">${s.horas}h</span></div>`).join('');
}

// ══════════════ TAREAS ══════════════
function taskHTML(t,mini=false){
  const d=daysUntil(t.fecha); const p=pct(t);
  const nAp=D.apuntes.filter(a=>a.tareaId===t.id).length;
  const isGlobal=t.diff===6;
  return `<div class="task-item">
    <div class="task-check${t.done?' done':''}" onclick="toggleTask(${t.id})"></div>
    <div class="task-info">
      <div class="task-name${t.done?' done':''}">
        ${isGlobal?'<span style="font-size:11px;background:var(--red-dim);color:var(--red);border-radius:3px;padding:1px 5px;margin-right:5px;font-weight:700">GLOBAL</span>':''}${t.nombre}
      </div>
      <div class="task-meta">${t.materia} · ${t.tipo} · ${fmtDate(t.fecha)}${nAp?' · 📝 '+nAp:''}</div>
      <div class="prog-bar"><div class="prog-fill" style="width:${p}%;${isGlobal?'background:var(--red)':''}"></div></div>
      <div style="font-size:11px;color:var(--text3);margin-top:3px">${t.h_done||0}h / ${t.h_total}h (${p}%)</div>
    </div>
    <div class="task-right">
      ${diffDots(t.diff)}
      ${urgBadge(d)}
      ${!mini?`<div class="task-acts">
        <button class="btn-ico" onclick="openHoras(${t.id})" title="Registrar horas">⏱</button>
        <button class="btn-ico" onclick="eliminarTarea(${t.id})" title="Eliminar">✕</button>
      </div>`:''}
    </div>
  </div>`;
}
function renderTareas(){
  const pend=D.tareas.filter(t=>!t.done).sort((a,b)=>new Date(a.fecha)-new Date(b.fecha));
  const comp=D.tareas.filter(t=>t.done);
  let h='';
  if(!pend.length&&!comp.length){ h='<div class="empty"><div class="empty-ico">📚</div>Agrega tu primera tarea</div>'; }
  else {
    h+=pend.map(t=>taskHTML(t)).join('');
    if(comp.length){ h+=`<div style="font-size:12px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;padding:16px 0 8px">Completadas (${comp.length})</div>`+comp.map(t=>taskHTML(t)).join(''); }
  }
  document.getElementById('lista-tareas').innerHTML=h;
}
function guardarTarea(){
  const nombre=document.getElementById('t-nombre').value.trim();
  const materia=document.getElementById('t-materia').value.trim();
  const fecha=document.getElementById('t-fecha').value;
  const tipo=document.getElementById('t-tipo').value;
  if(!nombre||!materia||!fecha){ alert('Rellena nombre, materia y fecha'); return; }
  const paginas=parseInt(document.getElementById('t-paginas').value)||0;
  let hTotal=estimatedHours;
  if(!hTotal){
    if(tipo==='Lectura'&&paginas){ const pgPerHr=[50,40,30,22,15,10][currentDiff-1]; hTotal=Math.ceil(paginas/pgPerHr); }
    else { hTotal=H_BASE[tipo]?.[currentDiff-1]??H_BASE['Otro'][currentDiff-1]; }
  }
  D.tareas.push({
    id:Date.now(), nombre, materia, fecha, tipo,
    diff:currentDiff, paginas, h_total:hTotal, h_done:0,
    notas:document.getElementById('t-notas').value.trim(),
    done:false, creada:todayStr()
  });
  saveD();
  closeModal('modal-tarea');
  ['t-nombre','t-materia','t-notas','t-paginas'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  document.getElementById('t-fecha').value='';
  document.getElementById('hrs-estimate').style.display='none';
  document.getElementById('grp-paginas').style.display='none';
  estimatedHours=0;
  setDiff(3);
  renderTareas();
}
function toggleTask(id){
  const t=D.tareas.find(x=>x.id===id); if(t){ t.done=!t.done; saveD(); renderTareas(); renderDashboard(); }
}
function eliminarTarea(id){
  if(!confirm('¿Eliminar esta tarea?')) return;
  D.tareas=D.tareas.filter(t=>t.id!==id); saveD(); renderTareas(); renderDashboard();
}

// ══════════════ HORAS (por tarea) ══════════════
let horasTargetId=null;
function openHoras(id){
  horasTargetId=id;
  const t=D.tareas.find(x=>x.id===id);
  document.getElementById('h-tarea-nombre').textContent=t.nombre+' — '+t.materia;
  document.getElementById('h-slider').value=2;
  document.getElementById('h-display').textContent='2h';
  openModal('modal-horas');
}
function guardarHoras(){
  const t=D.tareas.find(x=>x.id===horasTargetId); if(!t) return;
  const h=parseFloat(document.getElementById('h-slider').value);
  t.h_done=Math.min((t.h_done||0)+h,t.h_total);
  if(t.h_done>=t.h_total) t.done=true;
  saveD(); closeModal('modal-horas'); renderTareas(); renderDashboard();
}

// ══════════════ PLAN — FIX: respetar límite de horas por día ══════════════
function calcPlan(){
  const hd=getHorasDia();
  const estilo=D.perfil.estilo;
  const pend=D.tareas.filter(t=>!t.done&&t.fecha);
  const agenda={};    // key -> [{nombre,materia,horas}]
  const horasUsadas={}; // key -> horas ya asignadas ese día

  // Ordenar por fecha de entrega (más urgentes primero) y diff (global primero dentro de misma fecha)
  const sorted=[...pend].sort((a,b)=>{
    const df=new Date(a.fecha)-new Date(b.fecha);
    if(df!==0) return df;
    return (b.diff===6?1:0)-(a.diff===6?1:0);
  });

  sorted.forEach(t=>{
    const hRest=(t.h_total||0)-(t.h_done||0);
    if(hRest<=0) return;
    const entrega=parseDate(t.fecha);
    const days=[];
    for(let i=0;i<30;i++){
      const d=new Date(today()); d.setDate(d.getDate()+i);
      const dow=dowOf(d);
      if((hd[dow]||0)>0&&d<entrega){
        const key=d.toISOString().slice(0,10);
        days.push({key,dow,hd:hd[dow]});
      }
    }
    if(!days.length) return;

    let {sesiones}=getCadencia(t.tipo,t.diff,hRest,days.length);
    sesiones=Math.min(sesiones,days.length);

    let chosenDays;
    if((t.tipo==='Proyecto'||t.tipo==='Tarea')&&t.diff<6){
      chosenDays=days.slice(Math.max(0,days.length-sesiones));
    } else if(estilo==='intensivo'){
      chosenDays=days.slice(0,sesiones);
    } else if(estilo==='ultima_hora'){
      chosenDays=days.slice(Math.max(0,days.length-sesiones));
    } else {
      const step=Math.max(1,Math.floor(days.length/sesiones));
      chosenDays=[];
      for(let i=0;i<sesiones&&i*step<days.length;i++) chosenDays.push(days[i*step]);
    }

    // FIX: distribuir horas respetando el límite diario (hd) y lo ya asignado ese día
    let restante=hRest;
    const hPorSesion=restante/chosenDays.length;
    chosenDays.forEach(({key,hd:maxHd})=>{
      if(restante<=0) return;
      const yaUsado=horasUsadas[key]||0;
      const disponible=Math.max(0,maxHd-yaUsado); // FIX: calcular espacio real disponible
      if(disponible<=0) return;
      const h=Math.min(Math.round(hPorSesion*10)/10, restante, disponible);
      if(h>0){
        if(!agenda[key]) agenda[key]=[];
        agenda[key].push({nombre:t.nombre,materia:t.materia,horas:Math.round(h*10)/10});
        horasUsadas[key]=(horasUsadas[key]||0)+h;
        restante-=h;
      }
    });
  });
  return agenda;
}

function renderPlan(){
  const plan=calcPlan();
  const hd=getHorasDia();
  let html='';
  for(let i=0;i<14;i++){
    const d=new Date(today()); d.setDate(d.getDate()+i);
    const dow=dowOf(d);
    if((hd[dow]||0)===0) continue;
    const key=d.toISOString().slice(0,10);
    const ses=plan[key]||[];
    const totalH=ses.reduce((a,s)=>a+s.horas,0);
    const limiteH=hd[dow];
    const pctBar=Math.min(100,Math.round(totalH/limiteH*100));
    html+=`<div class="plan-day"><div class="plan-day-hdr"><span>${DIAS_FULL[dow]}</span><span class="plan-day-date">${d.toLocaleDateString('es-ES',{day:'numeric',month:'short'})}</span>${ses.length?`<span class="plan-day-hrs">${Math.round(totalH*10)/10}h / ${limiteH}h</span>`:'<span class="plan-day-hrs" style="color:var(--text3)">libre</span>'}</div>${ses.map(s=>`<div class="plan-session"><div class="plan-dot"></div><span>${s.nombre}</span><span class="plan-mat">${s.materia}</span><span class="plan-hrs">${s.horas}h</span></div>`).join('')}${!ses.length?'<div class="plan-session" style="color:var(--text3)">Sin sesiones</div>':''}<div style="height:3px;background:var(--bg3);border-radius:0 0 var(--r-sm) var(--r-sm)"><div style="height:100%;width:${pctBar}%;background:${pctBar>90?'var(--red)':'var(--accent)'};transition:width .3s;border-radius:0 0 var(--r-sm) var(--r-sm)"></div></div></div>`;
  }
  if(!D.tareas.filter(t=>!t.done).length) html='<div class="empty"><div class="empty-ico">🎉</div>No hay tareas para planificar</div>';
  document.getElementById('plan-cont').innerHTML=html;
}

// ══════════════ CALENDARIO ══════════════
let calYear=today().getFullYear();
let calMonth=today().getMonth();

const TASK_COLORS=['#a855f7','#60a5fa','#34d399','#fbbf24','#f87171','#fb923c','#c084fc'];
function getTaskColor(idx){ return TASK_COLORS[idx%TASK_COLORS.length]; }

function renderCalendario(){
  const meses=['Enero','Febrero','Marzo','Abril','Mayo','Junio','Julio','Agosto','Septiembre','Octubre','Noviembre','Diciembre'];
  document.getElementById('cal-month-title').textContent=meses[calMonth]+' '+calYear;
  const grid=document.getElementById('cal-grid');
  let html='';
  DIAS_SHORT.forEach(d=>{ html+=`<div class="cal-dow">${d}</div>`; });

  const first=new Date(calYear,calMonth,1);
  const last=new Date(calYear,calMonth+1,0);
  const startDow=first.getDay()===0?6:first.getDay()-1;

  // Build task color map
  const taskColorMap={};
  D.tareas.forEach((t,i)=>{ taskColorMap[t.id]=getTaskColor(i); });

  // Plan for this month
  const plan=calcPlan();

  // Prev month filler
  for(let i=0;i<startDow;i++){
    const d=new Date(calYear,calMonth,1-startDow+i);
    html+=`<div class="cal-cell other-month"><div class="cal-day-num">${d.getDate()}</div></div>`;
  }

  for(let day=1;day<=last.getDate();day++){
    const d=new Date(calYear,calMonth,day);
    const key=d.toISOString().slice(0,10);
    const isToday=key===todayStr();
    const deliveries=D.tareas.filter(t=>t.fecha===key);
    const sessions=plan[key]||[];
    const hasSomething=deliveries.length||sessions.length;

    // Build pill content for deliveries
    let pills='';
    deliveries.slice(0,2).forEach(t=>{
      const color=taskColorMap[t.id];
      pills+=`<span class="cal-task-pill" style="background:${color}22;color:${color}">${t.nombre}</span>`;
    });
    if(deliveries.length>2) pills+=`<span class="cal-task-pill" style="background:var(--bg3);color:var(--text3)">+${deliveries.length-2}</span>`;

    // Session dots
    let dots='';
    if(sessions.length){
      dots='<div class="cal-dot-row">'+sessions.slice(0,4).map(s=>`<div class="cal-dot" style="background:var(--accent);opacity:.6"></div>`).join('')+'</div>';
    }

    const calData=encodeURIComponent(JSON.stringify({key,deliveries:deliveries.map(t=>({nombre:t.nombre,materia:t.materia,done:t.done})),sessions}));
    html+=`<div class="cal-cell${isToday?' today':''}${hasSomething?' has-tasks':''}" onmouseenter="showCalTooltip(event,'${calData}')" onmouseleave="hideCalTooltip()">
      <div class="cal-day-num">${day}</div>
      ${pills}
      ${dots}
    </div>`;
  }

  // Next month filler
  const cells=startDow+last.getDate();
  const remain=cells%7===0?0:7-(cells%7);
  for(let i=1;i<=remain;i++){
    html+=`<div class="cal-cell other-month"><div class="cal-day-num">${i}</div></div>`;
  }
  grid.innerHTML=html;
}

function calPrev(){ calMonth--; if(calMonth<0){calMonth=11;calYear--;} renderCalendario(); }
function calNext(){ calMonth++; if(calMonth>11){calMonth=0;calYear++;} renderCalendario(); }
function calToday(){ calYear=today().getFullYear(); calMonth=today().getMonth(); renderCalendario(); }

function showCalTooltip(e,dataStr){
  const data=JSON.parse(decodeURIComponent(dataStr));
  if(!data.deliveries.length&&!data.sessions.length) return;
  const tip=document.getElementById('cal-tooltip');
  let html=`<div style="font-size:11px;font-weight:700;color:var(--text3);margin-bottom:6px;text-transform:uppercase;letter-spacing:.06em">${data.key}</div>`;
  if(data.deliveries.length){
    html+=`<div style="font-size:11px;color:var(--text3);margin-bottom:4px">Entregas</div>`;
    data.deliveries.forEach(t=>{
      html+=`<div class="cal-tooltip-item"><strong>${t.nombre}</strong>${t.materia}</div>`;
    });
  }
  if(data.sessions.length){
    html+=`<div style="font-size:11px;color:var(--text3);margin:6px 0 4px">Sesiones planificadas</div>`;
    data.sessions.forEach(s=>{
      html+=`<div class="cal-tooltip-item"><strong>${s.nombre}</strong>${s.horas}h · ${s.materia}</div>`;
    });
  }
  tip.innerHTML=html;
  tip.style.display='block';
  // Position
  const rect=e.target.getBoundingClientRect();
  let top=rect.bottom+6; let left=rect.left;
  if(top+200>window.innerHeight) top=rect.top-200-6;
  if(left+240>window.innerWidth) left=window.innerWidth-250;
  tip.style.top=top+'px'; tip.style.left=left+'px';
}
function hideCalTooltip(){ document.getElementById('cal-tooltip').style.display='none'; }

// ══════════════ ESTADÍSTICAS ══════════════
function guardarLogDia(){
  const fecha=document.getElementById('ld-fecha').value;
  const horas=parseFloat(document.getElementById('ld-slider').value);
  if(!fecha){ alert('Selecciona una fecha'); return; }
  if(!D.logsEstudio) D.logsEstudio=[];
  // Si ya existe ese día, actualizar
  const existing=D.logsEstudio.find(l=>l.fecha===fecha);
  if(existing){ existing.horas=horas; } else { D.logsEstudio.push({fecha,horas}); }
  saveD();
  closeModal('modal-log-dia');
  renderEstadisticas();
}

// Abrir modal con fecha de hoy por defecto
document.getElementById('modal-log-dia').addEventListener('click',function(){});
function abrirLogDia(){
  document.getElementById('ld-fecha').value=todayStr();
  document.getElementById('ld-slider').value=2;
  document.getElementById('ld-display').textContent='2h';
  openModal('modal-log-dia');
}
// Override btn en estadísticas para poner fecha de hoy
document.querySelector('[onclick="openModal(\'modal-log-dia\')"]')&&
  document.querySelector('[onclick="openModal(\'modal-log-dia\')"]').setAttribute('onclick',"abrirLogDia()");

function renderEstadisticas(){
  if(!D.logsEstudio) D.logsEstudio=[];
  const hd=getHorasDia();

  // ── Bar chart: últimas 2 semanas ──
  const dias14=[];
  for(let i=13;i>=0;i--){
    const d=new Date(today()); d.setDate(d.getDate()-i);
    const key=d.toISOString().slice(0,10);
    const dow=dowOf(d);
    const objetivo=hd[dow]||0;
    const log=D.logsEstudio.find(l=>l.fecha===key);
    dias14.push({key,dow,objetivo,horas:log?log.horas:null,
      lbl:d.toLocaleDateString('es-ES',{weekday:'short'}).slice(0,2)});
  }
  const maxH=Math.max(...dias14.map(d=>Math.max(d.objetivo,d.horas||0)),1);
  let barHtml='';
  dias14.forEach(d=>{
    const horas=d.horas;
    const obHPct=Math.round(d.objetivo/maxH*100);
    const actPct=horas!=null?Math.round(horas/maxH*100):0;
    const isToday=d.key===todayStr();
    const color=horas==null?'var(--border2)':horas>=d.objetivo*1.3?'var(--accent)':horas>=d.objetivo?'var(--green)':'var(--red)';
    barHtml+=`<div class="bar-wrap" title="${d.key}: ${horas!=null?horas+'h':'sin dato'} / objetivo ${d.objetivo}h">
      <div class="bar-val">${horas!=null?horas+'':''}</div>
      <div style="position:relative;width:100%;display:flex;align-items:flex-end;height:80px">
        <div style="position:absolute;bottom:0;width:100%;height:${obHPct}%;background:var(--border);border-radius:3px 3px 0 0;border:1px dashed var(--border2)"></div>
        <div class="bar" style="background:${color};height:${actPct}%;${isToday?'box-shadow:0 0 8px '+color:''}"></div>
      </div>
      <div class="bar-lbl" style="color:${isToday?'var(--accent)':'var(--text3)'}">${d.lbl}</div>
    </div>`;
  });
  document.getElementById('bar-chart').innerHTML=barHtml||'<div class="empty">Sin datos aún</div>';

  // ── Streak: últimas 4 semanas ──
  const dias28=[];
  for(let i=27;i>=0;i--){
    const d=new Date(today()); d.setDate(d.getDate()-i);
    const key=d.toISOString().slice(0,10);
    const dow=dowOf(d);
    const objetivo=hd[dow]||0;
    const log=D.logsEstudio.find(l=>l.fecha===key);
    dias28.push({key,dow,objetivo,horas:log?log.horas:null});
  }
  let streakHtml='';
  dias28.forEach(d=>{
    let cls='sd-none', title='Sin dato';
    if(d.horas!=null){
      if(d.horas>=d.objetivo*1.3){ cls='sd-crush'; title='¡Arrasaste! 🔥 '+d.horas+'h'; }
      else if(d.horas>=d.objetivo){ cls='sd-ok'; title='Objetivo conseguido ✓ '+d.horas+'h'; }
      else { cls='sd-miss'; title='Por debajo '+d.horas+'h / '+d.objetivo+'h objetivo'; }
    }
    const lbl=new Date(d.key+'T12:00:00').getDate();
    streakHtml+=`<div class="streak-day ${cls}" title="${title}">${lbl}</div>`;
  });
  document.getElementById('streak-row').innerHTML=streakHtml;

  // ── Resumen ──
  const logsConDatos=D.logsEstudio.filter(l=>l.horas>0);
  const totalHoras=logsConDatos.reduce((a,l)=>a+l.horas,0);
  const diasCrush=dias28.filter(d=>d.horas!=null&&d.objetivo>0&&d.horas>=d.objetivo*1.3).length;
  const diasOk=dias28.filter(d=>d.horas!=null&&d.objetivo>0&&d.horas>=d.objetivo).length;
  document.getElementById('stats-resumen').innerHTML=`
    <div class="stat-card"><div class="stat-lbl">Total horas registradas</div><div class="stat-num ac">${Math.round(totalHoras*10)/10}h</div></div>
    <div class="stat-card"><div class="stat-lbl">Días objetivo ✓ (4 sem.)</div><div class="stat-num" style="color:var(--green)">${diasOk}</div></div>
    <div class="stat-card"><div class="stat-lbl">Días que arrasaste 🔥 (4 sem.)</div><div class="stat-num ac">${diasCrush}</div></div>
  `;

  // ── Historial ──
  const sorted=[...D.logsEstudio].sort((a,b)=>b.fecha.localeCompare(a.fecha));
  const hist=document.getElementById('stats-historial');
  if(!sorted.length){ hist.innerHTML='<div class="empty">Aún no has registrado ningún día</div>'; return; }
  hist.innerHTML=sorted.slice(0,20).map(l=>{
    const dow=dowOf(new Date(l.fecha+'T12:00:00'));
    const obj=hd[dow]||0;
    const ratio=obj>0?l.horas/obj:1;
    let badge='',color='var(--text2)';
    if(ratio>=1.3){ badge='🔥'; color='var(--accent)'; }
    else if(ratio>=1){ badge='✓'; color='var(--green)'; }
    else { badge='↓'; color='var(--red)'; }
    return `<div style="display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--border)">
      <span style="font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--text3);min-width:80px">${l.fecha}</span>
      <span style="font-size:13px;font-weight:700;color:${color}">${l.horas}h</span>
      ${obj?`<span style="font-size:11px;color:var(--text3)">/ ${obj}h objetivo</span>`:''}
      <span style="margin-left:auto;font-size:16px">${badge}</span>
      <button class="btn-ico" onclick="eliminarLog('${l.fecha}')" title="Eliminar">✕</button>
    </div>`;
  }).join('');
}

function eliminarLog(fecha){
  D.logsEstudio=D.logsEstudio.filter(l=>l.fecha!==fecha); saveD(); renderEstadisticas();
}

// ══════════════ APUNTES ══════════════
let apTipo='texto';
let apImgData=null;
let apDocData=null;

function abrirModalApunte(){ resetApModal(); openModal('modal-apunte'); }
function resetApModal(){
  document.getElementById('ap-step1').style.display='block';
  document.getElementById('ap-step2').style.display='none';
  ['a-materia','a-titulo','a-contenido','a-doc-desc'].forEach(id=>{ const el=document.getElementById(id); if(el) el.value=''; });
  clearImg(); clearDoc();
  apImgData=null; apDocData=null;
}
function apBack(){ document.getElementById('ap-step1').style.display='block'; document.getElementById('ap-step2').style.display='none'; }
function elegirTipoAp(tipo){
  apTipo=tipo;
  document.getElementById('ap-step1').style.display='none';
  document.getElementById('ap-step2').style.display='block';
  const labels={texto:'Texto',imagen:'Imagen',documento:'Documento'};
  document.getElementById('ap-badge').textContent=labels[tipo];
  document.getElementById('ap-campo-texto').style.display=tipo==='texto'?'block':'none';
  document.getElementById('ap-campo-imagen').style.display=tipo==='imagen'?'block':'none';
  document.getElementById('ap-campo-doc').style.display=tipo==='documento'?'block':'none';
  const sel=document.getElementById('a-tarea-id');
  sel.innerHTML='<option value="">Sin asociar</option>';
  D.tareas.filter(t=>!t.done).forEach(t=>{ sel.innerHTML+=`<option value="${t.id}">${t.nombre} (${t.materia})</option>`; });
}
function fileToB64(file){ return new Promise(res=>{ const r=new FileReader(); r.onload=e=>res(e.target.result); r.readAsDataURL(file); }); }
async function previewImg(inp){
  const file=inp.files[0]; if(!file) return;
  apImgData=await fileToB64(file);
  document.getElementById('img-prev-img').src=apImgData;
  document.getElementById('img-preview').style.display='block';
  document.getElementById('img-dz').style.display='none';
}
function clearImg(){ apImgData=null; const i=document.getElementById('a-img-inp'); if(i) i.value=''; const p=document.getElementById('img-preview'); const d=document.getElementById('img-dz'); if(p) p.style.display='none'; if(d) d.style.display='block'; }
function handleImgDrop(e){ e.preventDefault(); dzLeave('img-dz'); const f=e.dataTransfer.files[0]; if(f&&f.type.startsWith('image/')){ const dt=new DataTransfer(); dt.items.add(f); document.getElementById('a-img-inp').files=dt.files; previewImg(document.getElementById('a-img-inp')); }}
async function previewDoc(inp){
  const file=inp.files[0]; if(!file) return;
  apDocData={name:file.name,size:file.size,type:file.type,data:await fileToB64(file)};
  document.getElementById('doc-ico').textContent=docIco(file.type);
  document.getElementById('doc-name').textContent=file.name;
  document.getElementById('doc-size').textContent=fmtSize(file.size);
  document.getElementById('doc-preview').style.display='flex';
  document.getElementById('doc-dz').style.display='none';
}
function clearDoc(){ apDocData=null; const i=document.getElementById('a-doc-inp'); if(i) i.value=''; const p=document.getElementById('doc-preview'); const d=document.getElementById('doc-dz'); if(p) p.style.display='none'; if(d) d.style.display='block'; }
function handleDocDrop(e){ e.preventDefault(); dzLeave('doc-dz'); const f=e.dataTransfer.files[0]; if(f){ const dt=new DataTransfer(); dt.items.add(f); document.getElementById('a-doc-inp').files=dt.files; previewDoc(document.getElementById('a-doc-inp')); }}
function dzOver(e,id){ e.preventDefault(); document.getElementById(id).classList.add('over'); }
function dzLeave(id){ document.getElementById(id).classList.remove('over'); }

function guardarApunte(){
  const materia=document.getElementById('a-materia').value.trim();
  const titulo=document.getElementById('a-titulo').value.trim();
  const tareaId=document.getElementById('a-tarea-id').value?parseInt(document.getElementById('a-tarea-id').value):null;
  if(!materia||!titulo){ alert('Rellena materia y título'); return; }
  const ap={materia,titulo,fecha:todayStr(),tipo:apTipo,tareaId};
  if(apTipo==='texto'){ const c=document.getElementById('a-contenido').value.trim(); if(!c){alert('Escribe el contenido');return;} ap.contenido=c; }
  else if(apTipo==='imagen'){ if(!apImgData){alert('Selecciona una imagen');return;} ap.imgData=apImgData; }
  else { if(!apDocData){alert('Selecciona un documento');return;} ap.docData=apDocData; ap.descripcion=document.getElementById('a-doc-desc').value.trim(); }
  D.apuntes.push(ap);
  saveD(); closeModal('modal-apunte'); renderApuntes();
}
function renderApuntes(){
  const el=document.getElementById('lista-apuntes');
  if(!D.apuntes.length){ el.innerHTML='<div class="empty"><div class="empty-ico">📝</div>Agrega tu primer apunte</div>'; return; }
  el.innerHTML=[...D.apuntes].reverse().map((a,i)=>{
    const realIdx=D.apuntes.length-1-i;
    const tarea=a.tareaId?D.tareas.find(t=>t.id===a.tareaId):null;
    let contenido='';
    if(a.tipo==='texto') contenido=`<div style="font-size:13px;color:var(--text2);line-height:1.6;margin-top:8px">${(a.contenido||'').replace(/\n/g,'<br>')}</div>`;
    else if(a.tipo==='imagen') contenido=`<div style="margin-top:8px"><img src="${a.imgData}" style="max-width:100%;max-height:240px;border-radius:var(--r-sm);border:1px solid var(--border)"/></div>`;
    else {
      const ico=a.docData?docIco(a.docData.type):'📄';
      const nm=a.docData?a.docData.name:'Documento';
      const sz=a.docData?fmtSize(a.docData.size):'';
      contenido=`<div style="margin-top:8px;display:flex;align-items:center;gap:10px;background:var(--bg3);border-radius:var(--r-sm);padding:10px 14px"><span style="font-size:22px">${ico}</span><div style="flex:1;min-width:0"><div style="font-size:13px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${nm}</div><div style="font-size:11px;color:var(--text3)">${sz}</div></div>${a.docData?`<a href="${a.docData.data}" download="${a.docData.name}" style="font-size:11px;color:var(--accent);text-decoration:none;border:1px solid var(--accent);padding:3px 9px;border-radius:20px;white-space:nowrap">Descargar</a>`:''}</div>${a.descripcion?`<div style="font-size:13px;color:var(--text2);margin-top:6px">${a.descripcion}</div>`:''}`;
    }
    const tIco=a.tipo==='imagen'?'🖼️':a.tipo==='documento'?'📄':'✍️';
    return `<div class="apunte-card">
      <div class="apunte-hdr">
        <div class="apunte-titulo">${tIco} ${a.titulo}</div>
        <span class="badge b-blue">${a.materia}</span>
        <button class="btn-ico" onclick="eliminarApunte(${realIdx})" style="margin-left:4px">✕</button>
      </div>
      <div style="display:flex;align-items:center;gap:8px;margin-top:2px">
        <span style="font-size:11px;color:var(--text3);font-family:'JetBrains Mono',monospace">${a.fecha}</span>
        ${tarea?`<span class="badge b-accent">📌 ${tarea.nombre}</span>`:''}
      </div>
      ${contenido}
    </div>`;
  }).join('');
}
function eliminarApunte(idx){ if(!confirm('¿Eliminar este apunte?'))return; D.apuntes.splice(idx,1); saveD(); renderApuntes(); }

// ══════════════ PERFIL ══════════════
function renderPerfil(){
  document.getElementById('p-nombre').value=D.nombre;
  document.getElementById('p-estilo').value=D.perfil.estilo;
  const hd=getHorasDia();
  document.querySelectorAll('#p-horas-grid input[data-dia]').forEach(inp=>{ inp.value=hd[parseInt(inp.dataset.dia)]||0; });
}
function guardarPerfil(){
  const nombre=document.getElementById('p-nombre').value.trim()||D.nombre;
  const pAct=document.getElementById('p-pass-actual').value;
  const pNva=document.getElementById('p-pass-nueva').value;
  const pConf=document.getElementById('p-pass-conf').value;
  if(pNva){
    if(btoa(pAct)!==db[currentUser].pass){ alert('La contraseña actual es incorrecta'); return; }
    if(pNva!==pConf){ alert('Las contraseñas nuevas no coinciden'); return; }
    if(pNva.length<4){ alert('La contraseña debe tener al menos 4 caracteres'); return; }
    db[currentUser].pass=btoa(pNva);
  }
  D.nombre=nombre;
  document.getElementById('sb-user').textContent=nombre;
  const hd=[0,0,0,0,0,0,0];
  document.querySelectorAll('#p-horas-grid input[data-dia]').forEach(inp=>{ hd[parseInt(inp.dataset.dia)]=parseFloat(inp.value)||0; });
  D.perfil.horas_dia=hd;
  D.perfil.estilo=document.getElementById('p-estilo').value;
  saveD();
  ['p-pass-actual','p-pass-nueva','p-pass-conf'].forEach(id=>document.getElementById(id).value='');
  alert('✅ Perfil guardado');
}
</script>
</body>
</html>
