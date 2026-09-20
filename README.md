<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
<meta name="theme-color" content="#070B18" />
<title>Aweh AI — Sovereign On-Device Intelligence for South Africa</title>
<meta name="author" content="Donovan Daniel Herbst" />
<meta name="description" content="Aweh AI — sovereign, offline, on-device AI for South Africa. Built by Donovan Daniel Herbst." />
<style>
  :root{
    --sa-blue:#002366;--sa-gold:#FFB612;--sa-green:#007749;--sa-red:#DE3831;
    --bg:#070B18;--surface:#101728;--surface-2:#1A2338;--outline:#2A3654;
    --text:#E8EDF7;--muted:#8A97B5;
    --mono:ui-monospace,"SF Mono",Menlo,Consolas,monospace;
    --sans:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  }
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
  html,body{margin:0;height:100%;background:var(--bg);color:var(--text);font-family:var(--sans);overscroll-behavior:none}
  body{display:flex;flex-direction:column;height:100dvh}
  header{display:flex;align-items:center;gap:10px;padding:12px 14px;padding-top:calc(12px + env(safe-area-inset-top,0));border-bottom:1px solid var(--outline);background:linear-gradient(180deg,rgba(0,35,102,.35),transparent)}
  .brand h1{margin:0;font-size:20px;font-weight:900;letter-spacing:2px;color:var(--sa-gold);font-family:var(--mono)}
  .brand p{margin:2px 0 0;font-size:9px;letter-spacing:1.5px;color:var(--muted);font-family:var(--mono);text-transform:uppercase}
  .spacer{flex:1}
  .chip{display:inline-flex;align-items:center;gap:6px;padding:5px 10px;border-radius:999px;font-family:var(--mono);font-size:10px;letter-spacing:1px;border:1px solid currentColor;opacity:.9}
  .chip .dot{width:6px;height:6px;border-radius:999px;background:currentColor}
  .chip.online{color:var(--sa-green);background:rgba(0,119,73,.10)}
  .chip.loading{color:var(--sa-gold);background:rgba(255,182,18,.10)}
  .chip.thinking{color:var(--sa-gold);background:rgba(255,182,18,.10);animation:gpulse 1.6s infinite}
  @keyframes gpulse{50%{opacity:.55}}
  .toolbar{display:flex;gap:6px;padding:8px 12px;border-bottom:1px solid var(--outline);background:var(--surface);overflow-x:auto;scrollbar-width:none}
  .toolbar::-webkit-scrollbar{display:none}
  .tgl{display:inline-flex;align-items:center;gap:5px;padding:6px 10px;border-radius:999px;font-family:var(--mono);font-size:10px;letter-spacing:.8px;border:1px solid var(--outline);background:transparent;color:var(--muted);cursor:pointer;white-space:nowrap;transition:all .15s}
  .tgl.active{color:var(--sa-gold);border-color:var(--sa-gold);background:rgba(255,182,18,.10)}
  main{flex:1;overflow:hidden;display:flex;flex-direction:column}
  #chat{flex:1;overflow-y:auto;padding:14px;display:flex;flex-direction:column;gap:10px;scroll-behavior:smooth}
  .msg{max-width:90%;padding:10px 13px;border-radius:14px;line-height:1.5;font-size:14.5px;white-space:pre-wrap;word-wrap:break-word;position:relative}
  .msg .who{font-family:var(--mono);font-size:9.5px;letter-spacing:1.2px;margin-bottom:5px;text-transform:uppercase;display:flex;align-items:center;gap:6px}
  .msg .who .badge{font-size:8px;padding:1px 5px;border-radius:4px;background:rgba(255,182,18,.15);color:var(--sa-gold)}
  .msg.user{align-self:flex-end;background:var(--sa-blue);border:1px solid #1a3a7a}
  .msg.user .who{color:var(--sa-gold)}
  .msg.bot{align-self:flex-start;background:var(--surface);border:1px solid var(--outline)}
  .msg.bot .who{color:var(--sa-green)}
  .msg.sys{align-self:center;background:transparent;border:1px dashed var(--outline);color:var(--muted);font-family:var(--mono);font-size:10.5px;letter-spacing:.8px;text-align:center;max-width:100%}
  .msg.trace{align-self:flex-start;background:rgba(0,35,102,.15);border:1px dashed rgba(255,182,18,.3);color:var(--muted);font-family:var(--mono);font-size:10.5px;line-height:1.5;max-width:90%}
  .msg.trace .step{color:var(--sa-gold)}
  .msg.trace .tool{color:var(--sa-green)}
  .cursor{display:inline-block;width:7px;height:15px;background:var(--sa-gold);vertical-align:text-bottom;animation:blink 1s steps(2) infinite;margin-left:2px}
  @keyframes blink{50%{opacity:0}}
  .msg-actions{display:flex;gap:6px;margin-top:8px;padding-top:6px;border-top:1px dashed var(--outline);opacity:.7}
  .msg-actions button{background:transparent;border:1px solid var(--outline);color:var(--muted);border-radius:8px;padding:3px 7px;font-family:var(--mono);font-size:9.5px;letter-spacing:.6px;cursor:pointer}
  .msg-actions button:hover{color:var(--sa-gold);border-color:var(--sa-gold)}
  #inputbar{display:flex;gap:8px;padding:10px 12px calc(10px + env(safe-area-inset-bottom,0));border-top:1px solid var(--outline);background:var(--surface);align-items:flex-end}
  #prompt{flex:1;background:var(--surface-2);border:1px solid var(--outline);color:var(--text);border-radius:12px;padding:10px 12px;font-size:15px;font-family:var(--sans);resize:none;max-height:110px;outline:none;line-height:1.4}
  #prompt:focus{border-color:var(--sa-gold)}
  .ibtn{background:var(--surface-2);color:var(--text);border:1px solid var(--outline);border-radius:12px;min-width:44px;height:44px;font-size:18px;cursor:pointer;display:flex;align-items:center;justify-content:center;padding:0}
  .ibtn.rec{background:var(--sa-red);color:#fff;border-color:var(--sa-red);animation:rpulse 1.2s infinite}
  @keyframes rpulse{50%{opacity:.6}}
  #send{background:var(--sa-gold);color:#070B18;border:0;border-radius:12px;padding:0 16px;height:44px;font-weight:800;font-family:var(--mono);letter-spacing:1px;cursor:pointer;font-size:12px;min-width:64px}
  #send:disabled{opacity:.35;cursor:not-allowed}
  #stop{display:none;background:var(--sa-red);color:#fff}
  #stop.show{display:flex}
  footer{font-family:var(--mono);font-size:9.5px;color:var(--muted);text-align:center;padding:6px 12px;letter-spacing:.7px;border-top:1px solid var(--outline);background:var(--surface)}
  footer b{color:var(--sa-gold)}
  .statbar{font-family:var(--mono);font-size:9.5px;color:var(--muted);padding:4px 12px;letter-spacing:.6px;text-align:center;background:var(--bg);border-bottom:1px solid var(--outline);display:none}
  .statbar.show{display:block}
  #firstrun{position:fixed;inset:0;z-index:30;background:rgba(7,11,24,.97);backdrop-filter:blur(8px);display:flex;flex-direction:column;justify-content:center;align-items:center;padding:20px;text-align:center;gap:14px;overflow-y:auto}
  #firstrun.hide{display:none}
  #firstrun h2{font-family:var(--mono);letter-spacing:3px;color:var(--sa-gold);margin:0;font-size:26px}
  #firstrun .tag{font-family:var(--mono);font-size:10.5px;letter-spacing:1.5px;color:var(--muted);text-transform:uppercase}
  #firstrun p{color:var(--muted);max-width:400px;font-size:12.5px;line-height:1.65;margin:0}
  .models{display:flex;flex-direction:column;gap:8px;width:100%;max-width:400px}
  .model{display:flex;justify-content:space-between;align-items:center;gap:12px;padding:11px 13px;background:var(--surface);border:1px solid var(--outline);border-radius:12px;cursor:pointer;color:var(--text);font-size:13px;text-align:left}
  .model:hover{border-color:var(--sa-gold)}
  .model .meta{font-family:var(--mono);font-size:10px;color:var(--muted);letter-spacing:1px}
  #progress{width:100%;max-width:400px}
  #progress .bar{height:6px;border-radius:3px;background:var(--surface-2);overflow:hidden}
  #progress .fill{height:100%;width:0%;background:linear-gradient(90deg,var(--sa-green),var(--sa-gold));transition:width .2s}
  #progress .txt{font-family:var(--mono);font-size:10.5px;color:var(--muted);margin-top:8px;text-align:center;letter-spacing:1px}
  .hero-badge{font-family:var(--mono);font-size:10px;letter-spacing:2px;color:var(--sa-gold);border:1px solid var(--sa-gold);border-radius:999px;padding:5px 12px;margin-bottom:6px}
  .banner{display:none;font-family:var(--mono);font-size:10.5px;letter-spacing:1px;padding:7px 12px;background:rgba(222,56,49,.1);color:var(--sa-red);border-bottom:1px solid rgba(222,56,49,.3);text-align:center}
  .banner.show{display:block}
  .drawer{position:fixed;inset:auto 0 0 0;z-index:15;background:var(--surface);border-top:1px solid var(--outline);padding:14px 14px calc(14px + env(safe-area-inset-bottom,0));transform:translateY(110%);transition:transform .25s;max-height:80dvh;overflow-y:auto}
  .drawer.show{transform:translateY(0)}
  .drawer h3{margin:0 0 10px;font-family:var(--mono);font-size:12px;letter-spacing:2px;color:var(--sa-gold)}
  .row{display:flex;gap:8px;margin-bottom:8px;align-items:center;flex-wrap:wrap}
  select,textarea.xin{background:var(--surface-2);color:var(--text);border:1px solid var(--outline);border-radius:10px;padding:9px 11px;font-size:14px;font-family:var(--sans);outline:none;width:100%}
  textarea.xin{resize:vertical;min-height:64px}
  .xbtn{background:var(--sa-gold);color:#070B18;border:0;border-radius:10px;padding:10px 14px;font-weight:800;font-family:var(--mono);letter-spacing:1px;font-size:11px;cursor:pointer}
  .xbtn.ghost{background:transparent;color:var(--text);border:1px solid var(--outline)}
  .xout{background:var(--surface-2);border:1px solid var(--outline);border-radius:10px;padding:11px;font-size:14px;line-height:1.5;min-height:64px;white-space:pre-wrap}
  .close{background:transparent;border:1px solid var(--outline);color:var(--muted);border-radius:10px;padding:9px 12px;cursor:pointer;font-family:var(--mono);font-size:11px;letter-spacing:1px}
  .memitem{background:var(--surface-2);border:1px solid var(--outline);border-radius:10px;padding:10px;font-size:12px;line-height:1.4;margin-bottom:8px;font-family:var(--mono);color:var(--muted);white-space:pre-wrap;word-break:break-word}
  #share-modal{position:fixed;inset:0;z-index:40;background:rgba(7,11,24,.95);backdrop-filter:blur(6px);display:none;flex-direction:column;align-items:center;justify-content:center;padding:20px;gap:14px}
  #share-modal.show{display:flex}
  #share-canvas{max-width:100%;max-height:60dvh;border-radius:14px;border:1px solid var(--outline)}
  #toast{position:fixed;bottom:calc(80px + env(safe-area-inset-bottom,0));left:50%;transform:translateX(-50%);background:var(--sa-gold);color:#070B18;font-family:var(--mono);font-size:11px;letter-spacing:1px;padding:10px 16px;border-radius:999px;z-index:50;opacity:0;pointer-events:none;transition:opacity .2s}
  #toast.show{opacity:1}
</style>
</head>
<body>

<header>
  <div class="brand">
    <h1>AWEH AI</h1>
    <p>Sovereign SA Intelligence · by Donovan Daniel Herbst</p>
  </div>
  <div class="spacer"></div>
  <span id="status" class="chip loading"><span class="dot"></span><span id="statusText">BOOTING</span></span>
</header>

<div class="toolbar">
  <button class="tgl" id="tglDeep">⟳ DEEP THINK</button>
  <button class="tgl" id="tglCrit">✓ CRITIQUE</button>
  <button class="tgl" id="tglCouncil">⚖ COUNCIL</button>
  <button class="tgl" id="tglAweh">🇿🇦 AWEH</button>
  <button class="tgl" id="tglMem">◆ MEMORY</button>
  <button class="tgl" id="tglXlate">⇄ TRANSLATE</button>
  <button class="tgl" id="openMemory">📚 MEMORIES</button>
</div>

<div id="statbar" class="statbar"></div>
<div id="banner" class="banner">⚠ No WebGPU — falling back to WASM. Slower, but still fully on-device.</div>

<main>
  <div id="chat"></div>
  <div id="inputbar">
    <button class="ibtn" id="mic" title="Voice input">🎙</button>
    <textarea id="prompt" rows="1" placeholder="Aweh? Vra my iets…" disabled></textarea>
    <button class="ibtn" id="stop" title="Stop">■</button>
    <button id="send" disabled>SEND</button>
  </div>
</main>

<footer>
  <b>© 2026 Donovan Daniel Herbst</b> · Aweh AI · GPLv3 · No cloud. No tracking. Your data stays yours.
</footer>

<div id="xlate" class="drawer">
  <div class="row">
    <h3 style="flex:1;margin:0">OFFLINE TRANSLATION · NLLB-200</h3>
    <button class="close" id="xclose">CLOSE</button>
  </div>
  <div class="row">
    <select id="xsrc">
      <option value="eng_Latn">English</option>
      <option value="zul_Latn">isiZulu</option>
      <option value="xho_Latn">isiXhosa</option>
      <option value="afr_Latn">Afrikaans</option>
      <option value="sot_Latn">Sesotho</option>
      <option value="tsn_Latn">Setswana</option>
      <option value="nso_Latn">Sepedi</option>
      <option value="tso_Latn">Xitsonga</option>
      <option value="ssw_Latn">siSwati</option>
      <option value="ven_Latn">Tshivenda</option>
      <option value="nbl_Latn">isiNdebele</option>
    </select>
    <button class="close" id="xswap">⇄</button>
    <select id="xtgt">
      <option value="zul_Latn">isiZulu</option>
      <option value="xho_Latn">isiXhosa</option>
      <option value="afr_Latn">Afrikaans</option>
      <option value="eng_Latn">English</option>
      <option value="sot_Latn">Sesotho</option>
      <option value="tsn_Latn">Setswana</option>
      <option value="nso_Latn">Sepedi</option>
      <option value="tso_Latn">Xitsonga</option>
      <option value="ssw_Latn">siSwati</option>
      <option value="ven_Latn">Tshivenda</option>
      <option value="nbl_Latn">isiNdebele</option>
    </select>
  </div>
  <textarea class="xin" id="xinput" placeholder="Type text to translate…"></textarea>
  <div class="row"><button class="xbtn" id="xgo">TRANSLATE</button></div>
  <div class="xout" id="xout">Translation appears here…</div>
</div>

<div id="memory" class="drawer">
  <div class="row">
    <h3 style="flex:1;margin:0">UBUNTU MEMORY</h3>
    <button class="close" id="memClose">CLOSE</button>
  </div>
  <p style="font-family:var(--mono);font-size:10.5px;color:var(--muted);letter-spacing:.6px;margin:0 0 10px">
    "I remember because we remember." Stored on-device. Never transmitted.
  </p>
  <div id="memList"></div>
  <div class="row"><button class="close" id="memClear" style="color:var(--sa-red);border-color:var(--sa-red)">CLEAR MEMORY</button></div>
</div>

<div id="share-modal">
  <canvas id="share-canvas" width="1080" height="1350"></canvas>
  <div class="row" style="justify-content:center">
    <button class="xbtn" id="shareDownload">DOWNLOAD</button>
    <button class="close" id="shareClose">CLOSE</button>
  </div>
</div>

<div id="toast"></div>

<div id="firstrun">
  <div class="hero-badge">SOVEREIGN · ON-DEVICE · GPLV3</div>
  <h2>AWEH AI</h2>
  <div class="tag">Sovereign SA Intelligence · by Donovan Daniel Herbst</div>
  <p>Runs entirely in your browser. Models download once, then cache for offline use. Nothing is sent to a server.</p>
  <p style="color:var(--sa-gold);font-family:var(--mono);font-size:11px;letter-spacing:1px">PICK YOUR ENGINE</p>
  <div class="models" id="modelList"></div>
  <div id="progress" style="display:none">
    <div class="bar"><div class="fill" id="fill"></div></div>
    <div class="txt" id="ptxt">Preparing…</div>
  </div>
  <p style="font-family:var(--mono);font-size:10px;letter-spacing:1px;color:var(--muted);margin-top:8px">
    Your device. Your model. Your data.
  </p>
</div>

<script type="module">
import { pipeline, TextStreamer, env } from "https://cdn.jsdelivr.net/npm/@huggingface/transformers@3.0.2";

env.allowLocalModels = false;
env.useBrowserCache   = true;

const CHAT_MODELS = [
  { id:"onnx-community/SmolLM2-360M-Instruct", name:"SmolLM2 360M", size:"~230 MB", note:"Fastest · best for Nova 9 SE" },
  { id:"onnx-community/Qwen2.5-0.5B-Instruct", name:"Qwen2.5 0.5B", size:"~350 MB", note:"Balanced · best tool use" },
  { id:"onnx-community/glm-edge-1.5b-chat-ONNX", name:"GLM-Edge 1.5B", size:"~1.0 GB", note:"GLM family · slow but real" },
  { id:"onnx-community/Qwen2.5-1.5B-Instruct", name:"Qwen2.5 1.5B", size:"~1.0 GB", note:"Best reasoning · slow on mobile" },
];

const AUX = {
  whisper : "onnx-community/whisper-tiny",
  embedder: "Xenova/all-MiniLM-L6-v2",
  nllb    : "Xenova/nllb-200-distilled-600M",
};

const $ = id => document.getElementById(id);
const chat = $("chat"), promptEl = $("prompt"), sendBtn = $("send"),
      stopBtn = $("stop"), micBtn = $("mic"), statusEl = $("status"),
      statusText = $("statusText"), banner = $("banner"),
      firstrun = $("firstrun"), modelList = $("modelList"),
      progressEl = $("progress"), fillEl = $("fill"), ptxtEl = $("ptxt"),
      statbar = $("statbar"), toastEl = $("toast");

const state = {
  chat:null, whisper:null, embedder:null, nllb:null,
  device:"wasm", modelName:"", busy:false, abort:false,
  deepThink:false, selfCritique:false, council:false, awehMode:true, memoryOn:true,
  sessionStats:{ tokens:0, ms:0, turns:0 },
};

const PREF_KEY = "aweh.prefs.v1";
function savePrefs(){
  try { localStorage.setItem(PREF_KEY, JSON.stringify({
    deepThink:state.deepThink, selfCritique:state.selfCritique,
    council:state.council, awehMode:state.awehMode, memoryOn:state.memoryOn,
  })); } catch {}
}
function loadPrefs(){
  try {
    const p = JSON.parse(localStorage.getItem(PREF_KEY) || "{}");
    Object.assign(state, p);
    $("tglDeep").classList.toggle("active", state.deepThink);
    $("tglCrit").classList.toggle("active", state.selfCritique);
    $("tglCouncil").classList.toggle("active", state.council);
    $("tglAweh").classList.toggle("active", state.awehMode);
    $("tglMem").classList.toggle("active", state.memoryOn);
  } catch {}
}

function setStatus(kind, text){ statusEl.className = "chip " + kind; statusText.textContent = text; }
function updateStatbar(){
  const s = state.sessionStats;
  if (!s.turns){ statbar.classList.remove("show"); return; }
  const tps = s.ms > 0 ? (s.tokens / (s.ms / 1000)).toFixed(1) : "0";
  statbar.textContent = `${s.turns} turn${s.turns===1?"":"s"} · ${s.tokens} tokens · ${tps} tok/s · ${state.modelName}`;
  statbar.classList.add("show");
}
function addMessage(role, text, opts = {}){
  const wrap = document.createElement("div");
  wrap.className = "msg " + role;
  const who = document.createElement("div");
  who.className = "who";
  const labels = { user:"You", bot:"Aweh AI", sys:"System", trace:"Reasoning Trace" };
  who.textContent = labels[role] || role;
  if (opts.badge){ const b = document.createElement("span"); b.className = "badge"; b.textContent = opts.badge; who.appendChild(b); }
  const body = document.createElement("div");
  body.className = "body";
  if (opts.html) body.innerHTML = text; else body.textContent = text;
  if (opts.streaming){ const cur = document.createElement("span"); cur.className = "cursor"; body.appendChild(cur); }
  wrap.appendChild(who); wrap.appendChild(body);

  if (role === "bot" && opts.actions !== false){
    const acts = document.createElement("div");
    acts.className = "msg-actions";
    acts.innerHTML = `<button data-act="copy">COPY</button><button data-act="share">SHARE</button><button data-act="regen">RETRY</button>`;
    acts.onclick = (e) => {
      const a = e.target.dataset.act;
      const txt = wrap.querySelector(".body").textContent;
      if (a === "copy"){ copyText(txt); toast("Copied"); }
      if (a === "share"){ openShare(txt); }
      if (a === "regen"){ regenerate(wrap); }
    };
    wrap.appendChild(acts);
  }

  chat.appendChild(wrap);
  chat.scrollTop = chat.scrollHeight;
  return { wrap, body };
}
function autoGrow(){ promptEl.style.height = "auto"; promptEl.style.height = Math.min(promptEl.scrollHeight, 110) + "px"; }
promptEl.addEventListener("input", autoGrow);

function escapeHtml(s){ return String(s).replace(/[&<>"']/g, c => ({ "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;" }[c])); }
async function copyText(t){ try { await navigator.clipboard.writeText(t); } catch { const ta = document.createElement("textarea"); ta.value = t; document.body.appendChild(ta); ta.select(); document.execCommand("copy"); ta.remove(); } }
function toast(msg){ toastEl.textContent = msg; toastEl.classList.add("show"); clearTimeout(toastEl._t); toastEl._t = setTimeout(() => toastEl.classList.remove("show"), 1800); }

function bindToggle(id, key, label){
  const el = $(id);
  el.onclick = () => {
    state[key] = !state[key];
    el.classList.toggle("active", state[key]);
    savePrefs();
    addMessage("sys", `${label} ${state[key] ? "ON" : "OFF"}`);
  };
}
bindToggle("tglDeep",   "deepThink",    "Deep Think");
bindToggle("tglCrit",   "selfCritique", "Self-Critique");
bindToggle("tglCouncil","council",      "Ubuntu Council");
bindToggle("tglAweh",   "awehMode",     "Aweh Mode");
bindToggle("tglMem",    "memoryOn",     "Ubuntu Memory");
$("tglXlate").onclick = () => $("xlate").classList.toggle("show");
$("xclose").onclick   = () => $("xlate").classList.remove("show");
$("xswap").onclick    = () => { const s = $("xsrc").value; $("xsrc").value = $("xtgt").value; $("xtgt").value = s; };
$("openMemory").onclick = () => { renderMemory(); $("memory").classList.toggle("show"); };
$("memClose").onclick = () => $("memory").classList.remove("show");
$("memClear").onclick = async () => { await wipeMemory(); renderMemory(); toast("Memory wiped"); };

function renderModels(){
  modelList.innerHTML = "";
  for (const m of CHAT_MODELS){
    const btn = document.createElement("button");
    btn.className = "model";
    btn.innerHTML = `<div><div><b>${m.name}</b></div><div class="meta">${m.note}</div></div><div class="meta">${m.size}</div>`;
    btn.onclick = () => loadChat(m);
    modelList.appendChild(btn);
  }
}

async function loadChat(model){
  modelList.style.display = "none";
  progressEl.style.display = "block";
  ptxtEl.textContent = "Loading runtime…";
  state.device = navigator.gpu ? "webgpu" : "wasm";
  if (!navigator.gpu) banner.classList.add("show");
  try {
    state.chat = await pipeline("text-generation", model.id, {
      dtype:"q4", device:state.device,
      progress_callback: p => {
        if (p.status === "progress" && p.total){
          const pct = Math.round((p.loaded / p.total) * 100);
          fillEl.style.width = pct + "%";
          ptxtEl.textContent = `Downloading ${p.file || "model"} — ${pct}%`;
        } else if (p.status === "ready"){ ptxtEl.textContent = "Initialising engine…"; }
        else if (p.status === "done"){ fillEl.style.width = "100%"; ptxtEl.textContent = "Ready."; }
      },
    });
    state.modelName = model.name;
    addMessage("sys", `Engine ready · ${model.name} · ${state.device.toUpperCase()} · on-device`);
    firstrun.classList.add("hide");
    setStatus("online", "ONLINE");
    promptEl.disabled = false; sendBtn.disabled = false; promptEl.focus();
  } catch (err){
    console.error(err);
    ptxtEl.textContent = "Load failed: " + (err.message || err);
  }
}

async function ensureWhisper(){
  if (state.whisper) return state.whisper;
  setStatus("loading", "VOICE…");
  state.whisper = await pipeline("automatic-speech-recognition", AUX.whisper, { dtype:"q8", device:state.device });
  setStatus("online", "ONLINE");
  return state.whisper;
}
async function ensureEmbedder(){
  if (state.embedder) return state.embedder;
  state.embedder = await pipeline("feature-extraction", AUX.embedder, { dtype:"q8", device:state.device });
  return state.embedder;
}
async function ensureNLLB(){
  if (state.nllb) return state.nllb;
  setStatus("loading", "NLLB…");
  toast("Downloading NLLB (~600 MB, one-time)…");
  state.nllb = await pipeline("translation", AUX.nllb, { dtype:"q4", device:state.device });
  setStatus("online", "ONLINE");
  return state.nllb;
}
async function translate(text, src, tgt){
  const t = await ensureNLLB();
  const out = await t(text, { src_lang:src, tgt_lang:tgt, max_new_tokens:400 });
  return out[0].translation_text;
}

const DB_NAME = "aweh-memory";
let dbPromise = null;
function openDB(){
  if (dbPromise) return dbPromise;
  dbPromise = new Promise((res, rej) => {
    const req = indexedDB.open(DB_NAME, 1);
    req.onupgradeneeded = () => {
      const db = req.result;
      if (!db.objectStoreNames.contains("mem")) db.createObjectStore("mem", { keyPath:"id", autoIncrement:true });
    };
    req.onsuccess = () => res(req.result);
    req.onerror   = () => rej(req.error);
  });
  return dbPromise;
}
async function memPut(text, vec){
  const db = await openDB();
  return new Promise((res, rej) => {
    const tx = db.transaction("mem", "readwrite");
    tx.objectStore("mem").add({ text, vec:Array.from(vec), t:Date.now() });
    tx.oncomplete = res; tx.onerror = () => rej(tx.error);
  });
}
async function memAll(){
  const db = await openDB();
  return new Promise((res, rej) => {
    const tx = db.transaction("mem", "readonly");
    const req = tx.objectStore("mem").getAll();
    req.onsuccess = () => res(req.result);
    req.onerror   = () => rej(req.error);
  });
}
async function wipeMemory(){
  const db = await openDB();
  return new Promise((res, rej) => {
    const tx = db.transaction("mem", "readwrite");
    tx.objectStore("mem").clear();
    tx.oncomplete = res; tx.onerror = () => rej(tx.error);
  });
}
async function embed(text){
  const e = await ensureEmbedder();
  const out = await e(text, { pooling:"mean", normalize:true });
  return out.data;
}
function cosine(a, b){ let s = 0; for (let i = 0; i < a.length; i++) s += a[i] * b[i]; return s; }
async function memorySearch(query, k = 3){
  if (!state.memoryOn) return [];
  const q = await embed(query);
  const all = await memAll();
  if (!all.length) return [];
  const scored = all.map(m => ({ text:m.text, score:cosine(q, m.vec) }));
  scored.sort((a, b) => b.score - a.score);
  return scored.slice(0, k).filter(s => s.score > 0.35);
}
async function memoryWrite(text){
  if (!state.memoryOn || !text || text.length < 12) return;
  const v = await embed(text);
  await memPut(text, v);
}
async function renderMemory(){
  const list = $("memList");
  const all = await memAll();
  if (!all.length){ list.innerHTML = `<div class="memitem">No memories yet. Turn on ◆ MEMORY and start chatting — I'll remember across sessions.</div>`; return; }
  list.innerHTML = all.slice().reverse().map(m => `<div class="memitem">${escapeHtml(m.text.slice(0, 400))}${m.text.length > 400 ? "…" : ""}</div>`).join("");
}

const tools = {
  async calc(expr){
    if (!/^[0-9+\-*/().\s%]+$/.test(expr)) return "ERR: only arithmetic allowed";
    try { return String(Function('"use strict";return(' + expr + ')')()); } catch { return "ERR: bad expression"; }
  },
  async now(){ return new Date().toLocaleString("en-ZA", { dateStyle:"full", timeStyle:"short" }); },
  async translate(args){
    const m = args.match(/^(\w+)>(\w+)::([\s\S]+)$/);
    if (!m) return "ERR: format src>tgt::text";
    return await translate(m[3].trim(), m[1], m[2]);
  },
  async recall(query){
    const hits = await memorySearch(query, 3);
    if (!hits.length) return "No relevant memories.";
    return hits.map((h, i) => `[${i+1}] (${h.score.toFixed(2)}) ${h.text}`).join("\n");
  },
  async remember(text){ await memoryWrite(text.trim()); return "Saved to Ubuntu Memory."; },
};
function parseAction(text){
  const toolMatch = text.match(/TOOL:\s*(\w+)\s*\(([\s\S]*?)\)/i);
  const ansMatch  = text.match(/ANSWER:\s*([\s\S]+)/i);
  if (toolMatch) return { kind:"tool", name:toolMatch[1].toLowerCase(), args:toolMatch[2].trim() };
  if (ansMatch)  return { kind:"answer", text:ansMatch[1].trim() };
  return { kind:"answer", text:text.trim() };
}

const AWEH_STYLE = `Speak with warm South African flavour — light use of "aweh", "ja", "lekker", "sharp" — but stay useful. Never overdo it.`;
const CRITIQUE_PROMPT = `You are a strict reviewer. Critique the answer below in one sentence: name one weakness or unstated assumption. If the answer is already excellent, say "Strong."\n\nAnswer: `;
const COUNCIL_BUILDER = `You are the BUILDER on the Ubuntu Council — you argue FOR the strongest possible answer. Be concrete and confident.`;
const COUNCIL_SKEPTIC = `You are the SKEPTIC on the Ubuntu Council — you name risks, edge cases, and unstated assumptions. Be sharp, not cynical.`;
const COUNCIL_JUDGE = `You are the JUDGE on the Ubuntu Council. You read the Builder's and Skeptic's positions, then produce a single final answer that takes the best of both.`;

function systemPrompt(){
  let base = `You are Aweh AI, a sovereign on-device assistant for South Africa. Be direct, warm, and honest. If you don't know, say so. You run entirely on the user's device — no cloud, no tracking.`;
  if (state.awehMode) base += "\n" + AWEH_STYLE;
  if (state.deepThink){
    base += `\n\nYou can reason step by step using tools. To use a tool, output exactly:\nTOOL: name(argument)\nAvailable tools: calc(expr), now(), translate(src>tgt::text), recall(query), remember(text).\nWhen you have the final answer, output:\nANSWER: your final answer\nDo not mix TOOL and ANSWER in one response. Keep reasoning short.`;
  }
  return base;
}

async function* streamOnce(messages, maxTokens = 256){
  const queue = [];
  const streamer = new TextStreamer(state.chat.tokenizer, {
    skip_prompt:true, skip_special_tokens:true,
    callback_function: tok => { queue.push(tok); },
  });
  const t0 = performance.now();
  const promise = state.chat(messages, { max_new_tokens:maxTokens, temperature:0.7, top_p:0.9, do_sample:true, streamer });
  let done = false;
  promise.finally(() => { done = true; });
  let count = 0;
  while (!done || queue.length){
    if (state.abort) throw new Error("__abort__");
    if (queue.length){ count++; yield queue.shift(); }
    else await new Promise(r => setTimeout(r, 15));
  }
  await promise;
  state.sessionStats.tokens += count;
  state.sessionStats.ms += (performance.now() - t0);
  updateStatbar();
}

async function recursiveAnswer(userText, onTrace, onToken){
  const ctx = [];
  if (state.memoryOn){
    const mem = await memorySearch(userText, 3);
    if (mem.length){
      ctx.push("Relevant memories:\n" + mem.map(m => "• " + m.text).join("\n"));
      onTrace(`recall → ${mem.length} memor${mem.length===1?"y":"ies"} found`);
    }
  }
  const messages = [
    { role:"system", content:systemPrompt() },
    ...(ctx.length ? [{ role:"system", content:ctx.join("\n") }] : []),
    { role:"user", content:userText },
  ];
  let final = "";
  const maxSteps = 4;
  for (let step = 0; step < maxSteps; step++){
    let buf = "", shown = "";
    for await (const tok of streamOnce(messages, 320)){
      buf += tok;
      if (step > 0 && /ANSWER:/i.test(buf)){
        const idx = buf.search(/ANSWER:\s*/i);
        const after = buf.slice(idx).replace(/^ANSWER:\s*/i, "");
        if (after.length > shown.length){
          const delta = after.slice(shown.length);
          shown = after; onToken(delta);
        }
      }
    }
    const action = parseAction(buf);
    if (action.kind === "answer"){
      final = action.text;
      if (shown && final.startsWith(shown)){
        const rem = final.slice(shown.length);
        if (rem) onToken(rem);
      } else onToken(final);
      break;
    }
    onTrace(`step ${step+1} → TOOL: ${action.name}(${action.args.slice(0,80)})`);
    const fn = tools[action.name];
    const result = fn ? await fn(action.args) : `ERR: unknown tool ${action.name}`;
    onTrace(`        ← ${String(result).slice(0,160)}`);
    messages.push({ role:"assistant", content:buf });
    messages.push({ role:"user", content:`TOOL RESULT:\n${result}\n\nContinue. If done, output ANSWER: ...` });
  }
  if (!final){ final = "I hit my reasoning limit without a clean answer. Try rephrasing, or turn off Deep Think."; onToken(final); }
  return final;
}

async function councilAnswer(userText, onPhase, onToken){
  onPhase("Builder drafting…");
  let builder = "";
  for await (const tok of streamOnce([{ role:"system", content:COUNCIL_BUILDER },{ role:"user", content:userText }], 220)) builder += tok;
  onPhase("Skeptic reviewing…");
  let skeptic = "";
  for await (const tok of streamOnce([{ role:"system", content:COUNCIL_SKEPTIC },{ role:"user", content:`Question: ${userText}\n\nBuilder's answer: ${builder}\n\nName the top 2 risks or gaps. Be concise.` }], 180)) skeptic += tok;
  onPhase("Judge synthesising…");
  let final = "";
  for await (const tok of streamOnce([{ role:"system", content:COUNCIL_JUDGE },{ role:"user", content:`Question: ${userText}\n\nBuilder: ${builder}\n\nSkeptic: ${skeptic}\n\nDeliver the final answer.` }], 320)){ final += tok; onToken(tok); }
  return final;
}

async function send(){
  const text = promptEl.value.trim();
  if (!text || state.busy || !state.chat) return;
  addMessage("user", text);
  promptEl.value = ""; autoGrow();
  const badge = state.council ? "COUNCIL" : state.deepThink ? "DEEP THINK" : "";
  const { body } = addMessage("bot", "", { streaming:true, badge });
  state.busy = true; state.abort = false;
  sendBtn.disabled = true; stopBtn.classList.add("show");
  setStatus("thinking", state.council ? "COUNCIL" : state.deepThink ? "REASONING" : "THINKING");
  state.sessionStats.turns++;
  let acc = "";
  const writeToken = (tok) => { acc += tok; body.textContent = acc; const cur = document.createElement("span"); cur.className = "cursor"; body.appendChild(cur); chat.scrollTop = chat.scrollHeight; };
  try {
    if (state.council){
      const { body: traceBody } = addMessage("trace", "", { html:true });
      const lines = [];
      const onPhase = (p) => { lines.push("◆ " + p); traceBody.innerHTML = lines.map(l => `<div class="step">${escapeHtml(l)}</div>`).join(""); };
      await councilAnswer(text, onPhase, writeToken);
    } else if (state.deepThink){
      const { body: traceBody } = addMessage("trace", "", { html:true });
      const lines = [];
      const onTrace = (l) => { lines.push(l); traceBody.innerHTML = lines.map(x => `<div class="${x.includes("←") ? "tool" : "step"}">${escapeHtml(x)}</div>`).join(""); };
      await recursiveAnswer(text, onTrace, writeToken);
    } else {
      for await (const tok of streamOnce([{ role:"system", content:systemPrompt() },{ role:"user", content:text }], 256)) writeToken(tok);
    }
    if (state.selfCritique && !state.abort && acc.trim()){
      let crit = "";
      for await (const tok of streamOnce([{ role:"system", content:CRITIQUE_PROMPT },{ role:"user", content:acc }], 80)) crit += tok;
      if (crit.trim() && !/^strong\.?$/i.test(crit.trim())){
        body.textContent = acc;
        const note = document.createElement("div");
        note.style.cssText = "margin-top:8px;padding-top:8px;border-top:1px dashed var(--outline);font-family:var(--mono);font-size:10.5px;color:var(--muted);letter-spacing:.6px";
        note.textContent = "SELF-CRITIQUE: " + crit.trim();
        body.appendChild(note);
      }
    }
    if (state.memoryOn) await memoryWrite(`User: ${text}\nAssistant: ${acc}`);
  } catch (e){
    if (e.message !== "__abort__") console.error(e);
  } finally {
    body.textContent = acc + (state.abort ? " [stopped]" : "");
    state.busy = false; sendBtn.disabled = false; stopBtn.classList.remove("show");
    setStatus("online", "ONLINE");
    chat.scrollTop = chat.scrollHeight;
  }
}

function regenerate(node){
  const all = Array.from(chat.querySelectorAll(".msg"));
  const idx = all.indexOf(node);
  for (let i = idx - 1; i >= 0; i--){
    if (all[i].classList.contains("user")){
      const text = all[i].querySelector(".body").textContent;
      node.remove(); promptEl.value = text; autoGrow(); send();
      return;
    }
  }
}

sendBtn.addEventListener("click", send);
stopBtn.addEventListener("click", () => { state.abort = true; });
promptEl.addEventListener("keydown", e => { if (e.key === "Enter" && !e.shiftKey){ e.preventDefault(); send(); } });

let mediaRec = null, chunks = [];
micBtn.onclick = async () => {
  if (mediaRec && mediaRec.state === "recording"){ mediaRec.stop(); return; }
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ audio:true });
    mediaRec = new MediaRecorder(stream); chunks = [];
    mediaRec.ondataavailable = e => chunks.push(e.data);
    mediaRec.onstop = async () => {
      stream.getTracks().forEach(t => t.stop());
      micBtn.classList.remove("rec"); micBtn.textContent = "🎙";
      const blob = new Blob(chunks, { type:"audio/webm" });
      const buf = await blob.arrayBuffer();
      const ac = new (window.AudioContext || window.webkitAudioContext)({ sampleRate:16000 });
      const audio = await ac.decodeAudioData(buf);
      const ch = audio.getChannelData(0);
      setStatus("loading", "TRANSCRIBING");
      const w = await ensureWhisper();
      const out = await w(ch, { language:"english", task:"transcribe" });
      setStatus("online", "ONLINE");
      const txt = (out.text || "").trim();
      if (txt){ promptEl.value = (promptEl.value ? promptEl.value + " " : "") + txt; autoGrow(); promptEl.focus(); }
    };
    mediaRec.start();
    micBtn.classList.add("rec"); micBtn.textContent = "■";
  } catch (e){ addMessage("sys", "Mic access denied: " + e.message); }
};

$("xgo").onclick = async () => {
  const text = $("xinput").value.trim();
  if (!text) return;
  $("xout").textContent = "Translating…";
  try { $("xout").textContent = await translate(text, $("xsrc").value, $("xtgt").value); }
  catch (e){ $("xout").textContent = "Error: " + e.message; }
};

function openShare(text){
  const c = $("share-canvas"), ctx = c.getContext("2d");
  const W = c.width, H = c.height;
  ctx.fillStyle = "#070B18"; ctx.fillRect(0, 0, W, H);
  ctx.fillStyle = "#0E1A33"; ctx.fillRect(40, 40, W-80, H-80);
  ctx.strokeStyle = "#2A3654"; ctx.lineWidth = 2; ctx.strokeRect(40, 40, W-80, H-80);
  ctx.fillStyle = "#FFB612"; ctx.font = "900 64px ui-monospace, monospace"; ctx.fillText("AWEH AI", 80, 160);
  ctx.fillStyle = "#8A97B5"; ctx.font = "500 26px ui-monospace, monospace";
  ctx.fillText("SOVEREIGN SA INTELLIGENCE", 80, 205);
  ctx.fillText("BUILT BY DONOVAN DANIEL HERBST", 80, 240);
  ctx.strokeStyle = "#2A3654"; ctx.beginPath(); ctx.moveTo(80, 280); ctx.lineTo(W-80, 280); ctx.stroke();
  ctx.fillStyle = "#E8EDF7"; ctx.font = "500 30px system-ui, sans-serif";
  const maxW = W - 160, lineH = 44;
  const words = text.split(/\s+/); let line = "", y = 340;
  for (const w of words){
    const test = line ? line + " " + w : w;
    if (ctx.measureText(test).width > maxW){ ctx.fillText(line, 80, y); y += lineH; line = w; if (y > H - 220) break; }
    else line = test;
  }
  if (line) ctx.fillText(line, 80, y);
  ctx.fillStyle = "#007749"; ctx.fillRect(40, H-140, W-80, 4);
  ctx.fillStyle = "#FFB612"; ctx.font = "900 30px ui-monospace, monospace"; ctx.fillText("Aweh AI", 80, H-90);
  ctx.fillStyle = "#8A97B5"; ctx.font = "500 22px ui-monospace, monospace";
  ctx.fillText("© 2026 Donovan Daniel Herbst · GPLv3 · On-device. Offline.", 80, H-55);
  $("share-modal").classList.add("show");
}
$("shareClose").onclick = () => $("share-modal").classList.remove("show");
$("shareDownload").onclick = () => {
  const c = $("share-canvas");
  const a = document.createElement("a");
  a.download = `aweh-ai-${Date.now()}.png`;
  a.href = c.toDataURL("image/png");
  a.click();
};

loadPrefs();
renderModels();
addMessage("sys", "Aweh AI · on-device · GPLv3 · © 2026 Donovan Daniel Herbst");
if (!navigator.gpu) banner.classList.add("show");
</script># Aweh AI
### Sovereign, on-device AI for South Africa

**Founder & Lead Engineer:** Donovan Daniel Herbst
**Status:** Active development
**Target:** Android 11+, Snapdragon 680 class, any modern browser
**Licence:** GNU GPL v3 — © 2026 Donovan Daniel Herbst

> "Umuntu ngumuntu ngabantu" — I am because we are.

Aweh AI runs entirely in your browser. The language model, the memory,
and your conversations never leave your device. No cloud. No tracking.

## Stack

| Layer | Choice |
|---|---|
| UI | Single HTML file, no build step |
| Inference | transformers.js (WebGPU / WASM) |
| Chat models | SmolLM2, Qwen2.5, GLM-Edge |
| Voice in | Whisper Tiny (local) |
| Translation | NLLB-200 (local) |
| Memory | MiniLM embeddings + IndexedDB |

## Features

- On-device chat with streaming tokens
- Recursive reasoning with local tools (Deep Think)
- Ubuntu Council — three-agent debate and synthesis
- Self-Critique — the model reviews its own answer
- Ubuntu Memory — vector recall across sessions
- Offline translation for 11 SA languages
- Voice input with on-device Whisper
- Share-as-image with creator watermark

## Run it

Open `index.html` in a modern browser. Pick a model. Done.

## Models

| Model | Size | Speed on Snapdragon 680 |
|---|---|---|
| SmolLM2 360M | ~230 MB | Fastest |
| Qwen2.5 0.5B | ~350 MB | Balanced, best tool use |
| GLM-Edge 1.5B | ~1.0 GB | Slow but real GLM |
| Qwen2.5 1.5B | ~1.0 GB | Best reasoning |

## What Aweh AI does not claim

No "quantum" encryption. No blockchain identity. No network scanner.
POPIA-aligned by design; not a compliance badge.

## Licence

GNU GPL v3 — see LICENSE.

© 2026 Donovan Daniel Herbst · Aweh AI

</body>
</html>
 # Aweh AI
### Sovereign, on-device AI for South Africa

**Founder & Lead Engineer:** Donovan Daniel Herbst
**Status:** Active development
**Target:** Android 11+, Snapdragon 680 class, any modern browser
**Licence:** GNU GPL v3 — © 2026 Donovan Daniel Herbst

> "Umuntu ngumuntu ngabantu" — I am because we are.

Aweh AI runs entirely in your browser. The language model, the memory,
and your conversations never leave your device. No cloud. No tracking.

## Stack

| Layer | Choice |
|---|---|
| UI | Single HTML file, no build step |
| Inference | transformers.js (WebGPU / WASM) |
| Chat models | SmolLM2, Qwen2.5, GLM-Edge |
| Voice in | Whisper Tiny (local) |
| Translation | NLLB-200 (local) |
| Memory | MiniLM embeddings + IndexedDB |

## Features

- On-device chat with streaming tokens
- Recursive reasoning with local tools (Deep Think)
- Ubuntu Council — three-agent debate and synthesis
- Self-Critique — the model reviews its own answer
- Ubuntu Memory — vector recall across sessions
- Offline translation for 11 SA languages
- Voice input with on-device Whisper
- Share-as-image with creator watermark

## Run it

Open `index.html` in a modern browser. Pick a model. Done.

## Models

| Model | Size | Speed on Snapdragon 680 |
|---|---|---|
| SmolLM2 360M | ~230 MB | Fastest |
| Qwen2.5 0.5B | ~350 MB | Balanced, best tool use |
| GLM-Edge 1.5B | ~1.0 GB | Slow but real GLM |
| Qwen2.5 1.5B | ~1.0 GB | Best reasoning |

## What Aweh AI does not claim

No "quantum" encryption. No blockchain identity. No network scanner.
POPIA-aligned by design; not a compliance badge.

## Licence

GNU GPL v3 — see LICENSE.

© 2026 Donovan Daniel Herbst · Aweh AI
