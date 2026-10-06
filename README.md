<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>⚡ FuturesBot — Binance Testnet</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{--bg:#060a0f;--bg2:#0b111c;--bg3:#0d1525;--bdr:#1a2535;--txt:#ccd6e8;--dim:#2a3a50;--g:#00e5a0;--r:#ff4060;--y:#f5c030;--b:#4a90d9}
body{background:var(--bg);color:var(--txt);font-family:'IBM Plex Mono',monospace;font-size:12px;min-height:100vh}
input{background:#0d1525;border:1px solid var(--bdr);color:var(--txt);font-family:inherit;font-size:11px;padding:8px 12px;border-radius:4px;outline:none;width:100%}
input:focus{border-color:var(--y)}
.btn{background:transparent;border:1px solid;border-radius:4px;padding:7px 16px;cursor:pointer;font-family:inherit;font-size:11px;font-weight:700;letter-spacing:1px;margin-left:6px;transition:opacity .2s}
.btn:hover{opacity:.8}
.btn-g{color:var(--g);border-color:#00e5a050}
.btn-r{color:var(--r);border-color:#ff406050}
.btn-y{color:var(--y);border-color:#f5c03050;width:100%;margin:0;padding:10px;font-size:12px}
.btn-d{color:var(--dim);border-color:var(--bdr)}
/* SETUP */
#setup{display:flex;align-items:center;justify-content:center;min-height:100vh;padding:16px}
.card{background:var(--bg2);border:1px solid var(--bdr);border-radius:8px;width:100%;max-width:520px}
.card-h{background:var(--bg3);padding:18px 22px;border-bottom:1px solid var(--bdr);border-radius:8px 8px 0 0}
.card-b{padding:22px}
.step{display:flex;gap:12px;margin-bottom:18px;padding-bottom:18px;border-bottom:1px solid var(--bdr)}
.step:last-of-type{border:0;margin:0;padding:0}
.sn{min-width:24px;height:24px;border-radius:50%;background:var(--y);color:#000;font-weight:700;font-size:10px;display:flex;align-items:center;justify-content:center;margin-top:2px}
.sl{font-size:11px;font-weight:600;color:var(--txt);margin-bottom:4px}
.sd{font-size:10px;color:var(--dim);line-height:1.7}
.fg{margin-top:8px}.fl{font-size:9px;color:var(--dim);letter-spacing:1px;margin-bottom:3px}
.fg+.fg{margin-top:8px}
#conn-err{font-size:10px;color:var(--r);margin-top:8px;min-height:14px}
.secnote{background:#050a05;border:1px solid #00e5a015;border-radius:4px;padding:8px 10px;font-size:9px;color:#1a3a1a;line-height:1.7;margin-top:16px}
a{color:var(--b);text-decoration:none}a:hover{text-decoration:underline}
/* DASHBOARD */
#main{display:none}
.hdr{background:var(--bg2);border-bottom:1px solid var(--bdr);padding:10px 18px;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:99}
.logo{font-size:14px;font-weight:700;color:var(--y);letter-spacing:3px}
.badge{display:inline-block;font-size:9px;border-radius:3px;padding:2px 6px;letter-spacing:1px;border:1px solid var(--bdr);background:var(--bg3);color:var(--dim);margin-left:5px}
/* DEBUG BAR */
.dbg{background:#080c14;border-bottom:1px solid var(--bdr);padding:5px 18px;font-size:9px;color:var(--dim);display:flex;gap:12px;flex-wrap:wrap;align-items:center;letter-spacing:.5px}
/* STATS */
.stats{display:grid;grid-template-columns:repeat(5,1fr);border-bottom:1px solid var(--bdr);background:var(--bg2)}
.sc{padding:12px 14px;border-right:1px solid var(--bdr)}
.sl2{font-size:9px;color:var(--dim);letter-spacing:1.5px;margin-bottom:4px}
.sv{font-size:18px;font-weight:700;line-height:1}
.ss{font-size:10px;color:var(--dim);margin-top:3px}
/* BODY */
.body{display:grid;grid-template-columns:1fr 270px}
.left{border-right:1px solid var(--bdr)}
.right{background:var(--bg2)}
/* TABS */
.tabs{display:flex;background:var(--bg);border-bottom:1px solid var(--bdr);overflow-x:auto}
.tab{padding:8px 12px;cursor:pointer;font-size:11px;white-space:nowrap;border-bottom:2px solid transparent;color:var(--dim);display:flex;align-items:center;gap:4px}
.tab.on{color:var(--y);border-bottom-color:var(--y)}
/* MARKET TABLE */
.mkt{background:var(--bg2);border-bottom:1px solid var(--bdr)}
.mhdr{display:grid;grid-template-columns:110px 105px 85px 50px 60px 75px;padding:5px 14px;font-size:9px;color:var(--dim);letter-spacing:1px;border-bottom:1px solid var(--bdr)}
.mrow{display:grid;grid-template-columns:110px 105px 85px 50px 60px 75px;padding:9px 14px;border-bottom:1px solid #0d1220;cursor:pointer;align-items:center;transition:background .15s}
.mrow:hover,.mrow.on{background:var(--bg3)}
/* PANEL */
.panel{background:var(--bg2);border-bottom:1px solid var(--bdr)}
.ph{padding:7px 14px;border-bottom:1px solid var(--bdr);font-size:9px;color:var(--dim);letter-spacing:1.5px;display:flex;justify-content:space-between;align-items:center}
.empty{padding:18px 14px;text-align:center;color:#1a2535}
/* LOG */
.logbody{overflow-y:auto;max-height:290px}
/* STRATEGY */
.strp{padding:10px 12px}
.strt{font-size:9px;color:var(--dim);letter-spacing:1.5px;margin-bottom:7px}
.strr{display:flex;justify-content:space-between;padding:3px 0;border-bottom:1px solid #0d1220;font-size:10px}
.strk{color:var(--dim)}.strv{color:#5a7a9a;text-align:right;max-width:60%}
.wbox{margin-top:8px;padding:7px;background:var(--bg);border-radius:4px;font-size:9px;color:#1a2a3a;line-height:1.7}
::-webkit-scrollbar{width:3px}::-webkit-scrollbar-track{background:var(--bg)}::-webkit-scrollbar-thumb{background:var(--bdr);border-radius:2px}
</style>
</head>
<body>

<!-- ═══ SETUP ═══════════════════════════════════════ -->
<div id="setup">
<div class="card">
  <div class="card-h">
    <div style="font-size:16px;font-weight:700;color:var(--y);letter-spacing:2px">⚡ FUTURESBOT — TESTNET</div>
    <div style="font-size:10px;color:var(--dim);margin-top:3px">Real Binance Futures orders · Zero real funds at risk</div>
  </div>
  <div class="card-b">
    <div class="step">
      <div class="sn">1</div>
      <div>
        <div class="sl">Get Testnet API Keys (free)</div>
        <div class="sd">
          Go to <a href="https://testnet.binancefuture.com" target="_blank">testnet.binancefuture.com</a><br>
          → Click <b style="color:var(--txt)">API Keys</b> tab<br>
          → Sign in with <b style="color:var(--txt)">GitHub</b> (free account)<br>
          → Click <b style="color:var(--txt)">"Generate HMAC_SHA256 Key"</b><br>
          → Copy <b style="color:var(--y)">API Key</b> and <b style="color:var(--y)">Secret Key</b>
        </div>
      </div>
    </div>
    <div class="step">
      <div class="sn">2</div>
      <div style="width:100%">
        <div class="sl">Enter Keys &amp; Connect</div>
        <div class="fg"><div class="fl">API KEY</div><input id="inp-key" type="text" placeholder="Paste API Key here..." autocomplete="off" spellcheck="false"></div>
        <div class="fg"><div class="fl">SECRET KEY</div><input id="inp-sec" type="password" placeholder="Paste Secret Key here..." autocomplete="off"></div>
        <div style="margin-top:12px"><button class="btn btn-y" id="conn-btn" onclick="doConnect()">🔗 CONNECT TO TESTNET</button></div>
        <div id="conn-err"></div>
      </div>
    </div>
    <div class="step">
      <div class="sn">3</div>
      <div>
        <div class="sl">Free test USDT ready instantly</div>
        <div class="sd">Testnet accounts get USDT automatically. No real funds ever involved.</div>
      </div>
    </div>
    <div class="secnote">🔒 Your keys live in browser memory only — never stored, never sent anywhere except Binance Testnet. Testnet keys cannot touch real funds even if stolen.</div>
  </div>
</div>
</div>

<!-- ═══ DASHBOARD ════════════════════════════════════ -->
<div id="main">

<div class="hdr">
  <div style="display:flex;align-items:center;flex-wrap:wrap">
    <span class="logo">⚡ FUTURESBOT</span>
    <span class="badge" style="background:#1a0f00;color:var(--y);border-color:#f5c03040">TESTNET</span>
    <span class="badge" id="badge-ws">○ WS</span>
    <span class="badge" id="badge-api">○ API</span>
    <span class="badge" id="badge-bot">● IDLE</span>
  </div>
  <div>
    <button class="btn btn-g" id="btn-start" onclick="toggleBot()">▶ START</button>
    <button class="btn btn-d" onclick="resetSession()">↺ RESET</button>
    <button class="btn btn-d" style="font-size:10px" onclick="doDisconnect()">⏏ OUT</button>
  </div>
</div>

<!-- LIVE DEBUG BAR -->
<div class="dbg">
  <span>WS: <b id="d-ws" style="color:var(--r)">--</b></span>
  <span style="color:#1a2535">|</span>
  <span id="d-pairs" style="flex:1">Loading...</span>
  <span style="color:#1a2535">|</span>
  <span>Bot: <b id="d-bot">OFF</b></span>
  <span style="color:#1a2535">|</span>
  <span>CD: <b id="d-cd">--</b></span>
</div>

<div class="stats">
  <div class="sc"><div class="sl2">TESTNET BALANCE</div><div class="sv" id="s-bal" style="color:var(--g)">--</div><div class="ss" id="s-bal2">USDT available</div></div>
  <div class="sc"><div class="sl2">SESSION PnL</div><div class="sv" id="s-pnl">$0.00</div><div class="ss" id="s-pnl2">0 trades</div></div>
  <div class="sc"><div class="sl2">WIN RATE</div><div class="sv" id="s-wr">--%</div><div class="ss" id="s-wr2">0W 0L</div></div>
  <div class="sc"><div class="sl2">OPEN POSITION</div><div class="sv" id="s-pos" style="color:var(--dim)">NONE</div><div class="ss" id="s-pos2">No active trade</div></div>
  <div class="sc"><div class="sl2">LEVERAGE / RISK</div><div class="sv" style="color:var(--y)">5×</div><div class="ss">TP +1.5% · SL -0.75%</div></div>
</div>

<div class="body">
  <div class="left">
    <div class="tabs" id="tabs"></div>
    <div class="mkt">
      <div class="mhdr"><span>PAIR</span><span>PRICE</span><span>CHART</span><span>RSI</span><span>SCORE</span><span>SIGNAL</span></div>
      <div id="mrows"></div>
    </div>
    <div class="panel" style="padding:10px 14px">
      <div id="ind-detail" style="font-size:10px;color:var(--dim);line-height:2">Loading signal detail...</div>
    </div>
    <div class="panel">
      <div class="ph"><span>OPEN POSITION (TESTNET)</span><span id="pos-id" style="color:var(--dim)">—</span></div>
      <div id="pos-body"><div class="empty">Press START — bot will place real testnet orders on confirmed signal</div></div>
    </div>
    <div class="panel">
      <div class="ph"><span>TRADE HISTORY</span><span id="h-cnt">0</span></div>
      <div id="hist"><div class="empty">No trades this session</div></div>
    </div>
  </div>
  <div class="right">
    <div class="panel">
      <div class="ph"><span>ACTIVITY LOG</span><span id="log-st" style="color:var(--dim)">IDLE</span></div>
      <div class="logbody" id="log"></div>
    </div>
    <div class="strp">
      <div class="strt">STRATEGY — BINANCE TESTNET</div>
      <div class="strr"><span class="strk">EXECUTION</span><span class="strv" style="color:var(--y)">Real testnet orders</span></div>
      <div class="strr"><span class="strk">PRICES</span><span class="strv" style="color:var(--g)">Binance Futures WS</span></div>
      <div class="strr"><span class="strk">PAIRS</span><span class="strv">BTC ETH BNB SOL XRP</span></div>
      <div class="strr"><span class="strk">SIGNAL</span><span class="strv">3/3 — EMA+MACD+RSI</span></div>
      <div class="strr"><span class="strk">LEVERAGE</span><span class="strv">5× (set via API)</span></div>
      <div class="strr"><span class="strk">TAKE PROFIT</span><span class="strv">+1.5% MARKET order</span></div>
      <div class="strr"><span class="strk">STOP LOSS</span><span class="strv">-0.75% MARKET order</span></div>
      <div class="strr"><span class="strk">POS SIZE</span><span class="strv">10% balance / trade</span></div>
      <div class="strr"><span class="strk">DAILY LIMIT</span><span class="strv">-5% → bot pauses</span></div>
      <div class="strr"><span class="strk">COOLDOWN</span><span class="strv">5 candles per pair</span></div>
      <div class="wbox">⚠ Testnet only. Real order infrastructure, zero real funds. Verify results for 2–4 weeks before considering live trading.</div>
    </div>
  </div>
</div>
</div>

<script>
'use strict';
// ══════════════════════════════════════════════════
// CONFIG
// ══════════════════════════════════════════════════
const PAIRS   = ['BTCUSDT','ETHUSDT','BNBUSDT','SOLUSDT','XRPUSDT'];
const DISP    = {BTCUSDT:'BTC/USDT',ETHUSDT:'ETH/USDT',BNBUSDT:'BNB/USDT',SOLUSDT:'SOL/USDT',XRPUSDT:'XRP/USDT'};
const LEV     = 5;
const TP_PCT  = 0.015;
const SL_PCT  = 0.0075;
const POS_PCT = 0.10;
const DAY_LIM = -0.05;
const COOLDOWN= 5;
// Per-symbol: price decimal places, quantity decimal places, min qty
const PRICE_DP= {BTCUSDT:1,ETHUSDT:2,BNBUSDT:2,SOLUSDT:2,XRPUSDT:4};
const QTY_DP  = {BTCUSDT:3,ETHUSDT:3,BNBUSDT:2,SOLUSDT:1,XRPUSDT:0};
const QTY_MIN = {BTCUSDT:0.001,ETHUSDT:0.001,BNBUSDT:0.01,SOLUSDT:0.1,XRPUSDT:1};
const TESTNET = 'https://testnet.binancefuture.com';
const WS_URL  = 'wss://fstream.binance.com/stream?streams=' + PAIRS.map(p=>`${p.toLowerCase()}@kline_1m`).join('/');

// ══════════════════════════════════════════════════
// STATE — separated clearly
// ══════════════════════════════════════════════════
let KEY='', SEC='', BAL=0, START_BAL=0, DAY_PNL=0;
let openPos=null, trades=[], logs=[];
let stats={w:0,l:0,be:0,pnl:0,n:0};
let cooldowns={}, botOn=false, paused=false, busy=false;
let activePair='BTCUSDT', ws=null, wsRecon=null;
let tickTmr=null, pollTmr=null, tryTmr=null;

// Raw price data (updated ONLY by WebSocket)
const RAW={};
PAIRS.forEach(sym=>{
  RAW[sym]={price:0,closes:[],volumes:[],hist:[],ready:false};
});

// Computed signals (updated ONLY by tick())
const SIG={};
PAIRS.forEach(sym=>{
  SIG[sym]={sig:'WAIT',rsi:50,ema20:0,ema50:0,macd:0,ls:0,ss:0,reason:'Loading...'};
});

// ══════════════════════════════════════════════════
// INDICATORS — simple & tested
// ══════════════════════════════════════════════════
function calcEMA(arr,n){
  if(!arr||arr.length<1)return 0;
  if(arr.length<=n)return arr[arr.length-1];
  const k=2/(n+1);
  let v=arr.slice(0,n).reduce((a,b)=>a+b,0)/n;
  for(let i=n;i<arr.length;i++)v=arr[i]*k+v*(1-k);
  return v;
}
function calcRSI(arr,n=14){
  if(!arr||arr.length<n+1)return 50;
  let g=0,l=0;
  for(let i=arr.length-n;i<arr.length;i++){const d=arr[i]-arr[i-1];d>0?g+=d:l-=d;}
  return 100-100/(1+g/(l||1e-9));
}
function computeSignal(sym){
  const d=RAW[sym];
  if(!d.ready||d.closes.length<52){
    return{sig:'WAIT',rsi:50,ema20:0,ema50:0,macd:0,ls:0,ss:0,reason:`Need ${d.closes.length}/52 candles`};
  }
  // Append current live price to closed candles
  const cl=d.price>0?[...d.closes,d.price]:d.closes;
  const last=cl[cl.length-1];
  const rsi  =calcRSI(cl);
  const ema20=calcEMA(cl.slice(-30),20);
  const ema50=calcEMA(cl.slice(-60),50);
  const macd =calcEMA(cl,12)-calcEMA(cl,26); // full-history MACD
  // LONG: all 3 must be true
  const L1=last>ema20;            // price above EMA20
  const L2=macd>0;                // MACD line positive
  const L3=rsi>=38&&rsi<=70;      // RSI in bull zone
  const ls=[L1,L2,L3].filter(Boolean).length;
  // SHORT: all 3 must be true
  const S1=last<ema20;
  const S2=macd<0;
  const S3=rsi>=30&&rsi<=62;
  const ss=[S1,S2,S3].filter(Boolean).length;
  const reason=`RSI:${rsi.toFixed(0)} P${last>ema20?'>':'<'}EMA MACD:${macd>0?'+':'-'} L:${ls}/3 S:${ss}/3`;
  if(ls===3&&ls>ss)return{sig:'LONG', rsi,ema20,ema50,macd,ls,ss,reason};
  if(ss===3&&ss>ls)return{sig:'SHORT',rsi,ema20,ema50,macd,ls,ss,reason};
  return{sig:'WAIT',rsi,ema20,ema50,macd,ls,ss,reason};
}

// ══════════════════════════════════════════════════
// BINANCE API
// ══════════════════════════════════════════════════
async function signQS(qs){
  const enc=new TextEncoder();
  const k=await crypto.subtle.importKey('raw',enc.encode(SEC),{name:'HMAC',hash:'SHA-256'},false,['sign']);
  const s=await crypto.subtle.sign('HMAC',k,enc.encode(qs));
  return Array.from(new Uint8Array(s)).map(b=>b.toString(16).padStart(2,'0')).join('');
}
async function api(method,path,params={}){
  params.timestamp=Date.now();
  params.recvWindow=6000;
  const qs =new URLSearchParams(params).toString();
  const sig=await signQS(qs);
  // ── ALL params go in the URL for both GET and POST ──
  // Binance accepts this for all endpoints.
  // Avoids Content-Type body + CORS preflight issues on mobile file:// origin.
  const url=`${TESTNET}${path}?${qs}&signature=${sig}`;
  let res;
  try{
    res=await fetch(url,{
      method,
      headers:{'X-MBX-APIKEY':KEY},
      // No body, no Content-Type — Binance reads params from URL
    });
  }catch(fetchErr){
    // TypeError: Failed to fetch = CORS or network block
    // Most common cause: opening HTML from local file (file:// origin)
    // Fix: serve the file via HTTPS (see instructions below)
    throw new Error(`NETWORK BLOCKED — open the file via HTTPS, not from Downloads. Error: ${fetchErr.message}`);
  }
  if(!res.ok)throw new Error(`HTTP ${res.status}: ${res.statusText}`);
  let data;
  try{data=await res.json();}catch(e){throw new Error(`Bad response (not JSON) from ${path}`);}
  if(data.code&&data.code<0)throw new Error(`Binance [${data.code}]: ${data.msg}`);
  return data;
}
async function getBalance(){
  const data=await api('GET','/fapi/v2/balance');
  const u=data.find(x=>x.asset==='USDT');
  return parseFloat(u?.availableBalance||0);
}
async function getOpenPositions(){
  const data=await api('GET','/fapi/v2/positionRisk');
  return data.filter(x=>Math.abs(parseFloat(x.positionAmt||0))>0.00001);
}
function calcQty(sym,price){
  const notional=BAL*POS_PCT*LEV;
  const dp=QTY_DP[sym]??2;
  const q=parseFloat((notional/price).toFixed(dp));
  return Math.max(QTY_MIN[sym]||0.001,q);
}
function roundPrice(sym,price){
  return parseFloat(price.toFixed(PRICE_DP[sym]??2));
}

// ══════════════════════════════════════════════════
// ORDER EXECUTION — step by step, verbose logging
// ══════════════════════════════════════════════════
async function openTrade(sym,dir,price){
  // Step 1: Set leverage
  try{
    await api('POST','/fapi/v1/leverage',{symbol:sym,leverage:LEV});
    addLog(`⚙ Leverage: ${LEV}× set on ${DISP[sym]}`,'info');
  }catch(e){addLog(`⚠ Leverage warning (non-fatal): ${e.message}`,'info');}

  // Step 2: Calculate quantity
  const q=calcQty(sym,price);
  addLog(`📐 Qty: ${q} ${sym.replace('USDT','')} (${POS_PCT*100}% of $${BAL.toFixed(0)} × ${LEV}×)`,'info');

  // Step 3: Market entry order
  addLog(`📤 Placing ${dir} MARKET order...`,'open');
  const entryOrd=await api('POST','/fapi/v1/order',{
    symbol:sym, side:dir==='LONG'?'BUY':'SELL', type:'MARKET', quantity:q
  });
  // Safe fill price: parseFloat first so "0" string doesn't block fallback
  const fill=parseFloat(entryOrd.avgPrice)||parseFloat(entryOrd.price)||price;
  addLog(`✅ Entry filled @ $${fp(fill)} (orderId:${entryOrd.orderId})`,'win');

  // Step 4: SL order — correct price precision per symbol
  const slP=roundPrice(sym, dir==='LONG'?fill*(1-SL_PCT):fill*(1+SL_PCT));
  addLog(`📤 Placing SL order @ $${fp(slP)}...`,'info');
  const slOrd=await api('POST','/fapi/v1/order',{
    symbol:sym, side:dir==='LONG'?'SELL':'BUY',
    type:'STOP_MARKET', quantity:q, stopPrice:slP,
    reduceOnly:'true', workingType:'MARK_PRICE'
  });
  addLog(`🛑 SL placed @ $${fp(slP)} (id:${slOrd.orderId})`,'info');

  // Step 5: TP order
  const tpP=roundPrice(sym, dir==='LONG'?fill*(1+TP_PCT):fill*(1-TP_PCT));
  addLog(`📤 Placing TP order @ $${fp(tpP)}...`,'info');
  const tpOrd=await api('POST','/fapi/v1/order',{
    symbol:sym, side:dir==='LONG'?'SELL':'BUY',
    type:'TAKE_PROFIT_MARKET', quantity:q, stopPrice:tpP,
    reduceOnly:'true', workingType:'MARK_PRICE'
  });
  addLog(`🎯 TP placed @ $${fp(tpP)} (id:${tpOrd.orderId})`,'info');

  // Step 6: Store and refresh balance
  openPos={sym,dir,entry:fill,q,slP,tpP,orderId:entryOrd.orderId,slId:slOrd.orderId,tpId:tpOrd.orderId,uPnl:0,time:hms()};
  cooldowns[sym]=COOLDOWN;
  BAL=await getBalance();
  addLog(`📋 POSITION OPEN: ${dir} ${DISP[sym]} | SL:$${fp(slP)} → TP:$${fp(tpP)} | Bal:$${BAL.toFixed(2)}`,'win');
}

// ══════════════════════════════════════════════════
// POSITION POLL — runs every 5s when position open
// ══════════════════════════════════════════════════
async function pollPositions(){
  if(!openPos||!botOn)return;
  try{
    const positions=await getOpenPositions();
    const mine=positions.find(p=>p.symbol===openPos.sym);
    if(!mine){
      // Binance closed the position (TP or SL hit)
      const cur=RAW[openPos.sym]?.price||openPos.entry;
      const pctRaw=openPos.dir==='LONG'?(cur-openPos.entry)/openPos.entry:(openPos.entry-cur)/openPos.entry;
      const pnl=parseFloat((pctRaw*openPos.q*openPos.entry*LEV).toFixed(2));
      const isW=pnl>0.01,isBE=Math.abs(pnl)<=0.01;
      DAY_PNL=+(DAY_PNL+pnl).toFixed(2);
      stats.pnl=+(stats.pnl+pnl).toFixed(2);
      stats.n++;stats.w+=isW?1:0;stats.l+=(!isW&&!isBE)?1:0;stats.be+=isBE?1:0;
      trades.unshift({sym:openPos.sym,dir:openPos.dir,entry:openPos.entry,exit:cur,pnl,pct:+(pctRaw*100).toFixed(2),reason:'TP/SL',time:hms()});
      addLog(`${isW?'✅':isBE?'🔁':'❌'} Position closed by Binance | PnL: ${pnl>=0?'+':''}$${pnl}`,isW?'win':isBE?'info':'loss');
      openPos=null;
      BAL=await getBalance();
    }else{
      const uPnl=parseFloat(mine.unRealizedProfit||0);
      openPos={...openPos,uPnl:+uPnl.toFixed(2)};
    }
  }catch(e){addLog(`⚠ Poll error: ${e.message}`,'loss');}
  render();
}

// ══════════════════════════════════════════════════
// TICK — recalculates signals, updates UI every 2s
// ══════════════════════════════════════════════════
let lastScanLog=0;
function tick(){
  // Recalculate all signals from current raw data
  PAIRS.forEach(sym=>{
    const s=computeSignal(sym);
    Object.assign(SIG[sym],s);
  });
  // Scan log every 10s when bot is on
  const now=Date.now();
  if(botOn&&now-lastScanLog>10000){
    lastScanLog=now;
    const info=PAIRS.map(sym=>`${DISP[sym]}:${SIG[sym].sig}(L${SIG[sym].ls}S${SIG[sym].ss})`).join(' | ');
    addLog(`🔍 ${info}`,'info');
  }
  render();
}

// ══════════════════════════════════════════════════
// TRY OPEN — called every 3s when bot is on
// ══════════════════════════════════════════════════
async function tryOpen(){
  if(!botOn||paused||openPos||busy)return;
  // Daily loss limit check
  if(START_BAL>0&&DAY_PNL/START_BAL<DAY_LIM){
    paused=true;
    addLog('🚨 Daily -5% loss limit hit — bot paused','loss');
    setBadge('bot','🛑 PAUSED','var(--r)');
    return;
  }
  // Scan each pair for signal
  for(const sym of PAIRS){
    const d=RAW[sym], s=SIG[sym];
    if(!d.ready)continue;
    if(s.sig==='WAIT')continue;
    if((cooldowns[sym]||0)>0){addLog(`⏳ ${DISP[sym]}: cooldown ${cooldowns[sym]}`,'info');continue;}
    if(BAL<15){addLog('⚠ Balance too low (< $15)','loss');break;}
    busy=true;
    try{
      addLog(`⚡ SIGNAL CONFIRMED: ${s.sig} ${DISP[sym]} | ${s.reason}`,'open');
      await openTrade(sym,s.sig,d.price);
      break; // success — exit loop
    }catch(e){
      addLog(`❌ ${DISP[sym]} order FAILED: ${e.message}`,'loss');
      // Don't break — continue to next pair
    }finally{
      busy=false;
    }
  }
}

// ══════════════════════════════════════════════════
// WEBSOCKET — only updates RAW price data
// ══════════════════════════════════════════════════
async function loadHistory(sym){
  try{
    const r=await fetch(`https://fapi.binance.com/fapi/v1/klines?symbol=${sym}&interval=1m&limit=100`);
    const arr=await r.json();
    if(!Array.isArray(arr))throw new Error('bad response');
    RAW[sym].closes  =arr.map(k=>parseFloat(k[4]));
    RAW[sym].volumes =arr.map(k=>parseFloat(k[5]));
    RAW[sym].hist    =RAW[sym].closes.slice(-24);
    RAW[sym].price   =RAW[sym].closes[RAW[sym].closes.length-1];
    RAW[sym].ready   =true;
    addLog(`📊 ${DISP[sym]}: ${arr.length} candles loaded`,'info');
  }catch(e){addLog(`❌ History ${DISP[sym]}: ${e.message}`,'loss');}
}
function wsConnect(){
  if(ws)try{ws.close();}catch(_){}
  setBadge('ws','◌ WS...','var(--dim)');
  ws=new WebSocket(WS_URL);
  ws.onopen=()=>{
    clearTimeout(wsRecon);
    setBadge('ws','● WS LIVE','var(--g)');
    G('d-ws').textContent='Connected ✓';
    G('d-ws').style.color='var(--g)';
    addLog('🔗 WebSocket connected — live prices flowing','info');
  };
  ws.onmessage=e=>{
    try{
      const msg=JSON.parse(e.data);
      if(!msg||!msg.data||!msg.data.k)return;
      const k=msg.data.k;
      const sym=k.s;
      if(!RAW[sym])return;
      const c=parseFloat(k.c);
      const v=parseFloat(k.v);
      // Always update live price
      RAW[sym].price=c;
      RAW[sym].hist=[...RAW[sym].hist.slice(-23),c];
      // On closed candle: add to history, decrement cooldown
      if(k.x===true){
        RAW[sym].closes =[...RAW[sym].closes.slice(-99),c];
        RAW[sym].volumes=[...RAW[sym].volumes.slice(-99),v];
        if((cooldowns[sym]||0)>0)cooldowns[sym]--;
      }
      // Note: tick() handles signal recalculation every 2s
    }catch(err){
      // Never let WS errors break the handler
      console.warn('WS msg error:',err);
    }
  };
  ws.onerror=()=>{
    setBadge('ws','✗ WS ERR','var(--r)');
    G('d-ws').textContent='Error';
    G('d-ws').style.color='var(--r)';
  };
  ws.onclose=()=>{
    setBadge('ws','○ WS OFF','var(--r)');
    G('d-ws').textContent='Disconnected';
    G('d-ws').style.color='var(--r)';
    addLog('🔌 WS closed — reconnect in 3s','info');
    wsRecon=setTimeout(wsConnect,3000);
  };
}

// ══════════════════════════════════════════════════
// CONNECT / DISCONNECT
// ══════════════════════════════════════════════════
async function doConnect(){
  const k=G('inp-key').value.trim(), s=G('inp-sec').value.trim();
  const errEl=G('conn-err');
  errEl.textContent='';
  if(!k||!s){errEl.textContent='⚠ Enter both API key and secret key';return;}
  KEY=k;SEC=s;
  G('conn-btn').disabled=true;
  G('conn-btn').textContent='◌ Connecting...';
  try{
    // Test: fetch balance
    BAL=await getBalance();
    START_BAL=BAL;
    // Switch to dashboard
    G('setup').style.display='none';
    G('main').style.display='block';
    setBadge('api','● API OK','var(--g)');
    addLog(`🔑 Connected! Testnet balance: $${BAL.toFixed(2)} USDT`,'win');
    renderStats();
    // Load history for all pairs (parallel)
    addLog('📊 Loading candle history...','info');
    await Promise.all(PAIRS.map(loadHistory));
    addLog('✅ History loaded — signals active','win');
    // Connect WebSocket for live prices
    wsConnect();
    // Start intervals — clearly separated responsibilities
    tickTmr =setInterval(tick,    2000); // recalc signals + render
    pollTmr =setInterval(pollPositions,5000); // check Binance positions
    tryTmr  =setInterval(tryOpen, 3000); // try to open trades
    tick(); // immediate first pass
  }catch(e){
    KEY='';SEC='';
    errEl.textContent=`❌ ${e.message}`;
    G('conn-btn').disabled=false;
    G('conn-btn').textContent='🔗 CONNECT TO TESTNET';
  }
}
function doDisconnect(){
  if(ws)try{ws.close();}catch(_){}
  clearInterval(tickTmr);clearInterval(pollTmr);clearInterval(tryTmr);
  clearTimeout(wsRecon);
  KEY='';SEC='';botOn=false;busy=false;
  G('setup').style.display='flex';
  G('main').style.display='none';
  G('inp-key').value='';G('inp-sec').value='';
}
function toggleBot(){
  if(paused)return;
  botOn=!botOn;
  if(botOn){
    G('btn-start').textContent='⏹ STOP';G('btn-start').className='btn btn-r';
    G('log-st').textContent='● SCANNING';G('log-st').style.color='var(--g)';
    setBadge('bot','● SCANNING','var(--g)');
    addLog('🤖 Bot ON — placing real testnet orders on confirmed signals','open');
  }else{
    G('btn-start').textContent='▶ START';G('btn-start').className='btn btn-g';
    G('log-st').textContent='PAUSED';G('log-st').style.color='var(--dim)';
    setBadge('bot','● IDLE','var(--dim)');
    addLog('⏹ Bot paused','info');
  }
}
async function resetSession(){
  botOn=false;paused=false;busy=false;
  DAY_PNL=0;openPos=null;trades=[];cooldowns={};
  stats={w:0,l:0,be:0,pnl:0,n:0};
  G('btn-start').textContent='▶ START';G('btn-start').className='btn btn-g';
  G('log-st').textContent='IDLE';G('log-st').style.color='var(--dim)';
  setBadge('bot','● IDLE','var(--dim)');
  addLog('↺ Session reset','info');
  try{BAL=await getBalance();START_BAL=BAL;}catch(_){}
  render();
}

// ══════════════════════════════════════════════════
// UI HELPERS
// ══════════════════════════════════════════════════
function G(id){return document.getElementById(id);}
function hms(){return new Date().toLocaleTimeString('en-GB',{hour12:false});}
function fp(n){if(n===null||n===undefined)return'?';if(Math.abs(n)<0.01)return n.toFixed(5);if(Math.abs(n)<100)return n.toFixed(3);return n.toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:2});}
function pc(v){return v>0.01?'var(--g)':v<-0.01?'var(--r)':'var(--y)';}
function addLog(msg,type='info'){logs.unshift({msg,type,t:hms()});if(logs.length>80)logs.pop();renderLog();}
function setBadge(key,txt,col){
  const el=G('badge-'+key);if(!el)return;
  el.textContent=txt;el.style.color=col;
  el.style.background=col==='var(--g)'?'#0a180a':col==='var(--r)'?'#1a0808':'#111827';
  el.style.borderColor=col==='var(--g)'?'#00e5a040':col==='var(--r)'?'#ff406040':'#1a2535';
}
function drawSpark(canvas,data,col){
  if(!canvas||!data||data.length<2)return;
  const ctx=canvas.getContext('2d'),w=canvas.width,h=canvas.height;
  ctx.clearRect(0,0,w,h);
  const mn=Math.min(...data),mx=Math.max(...data),rng=mx-mn||1;
  const pts=data.map((v,i)=>[i/(data.length-1)*w,h-((v-mn)/rng)*(h-4)-2]);
  const g=ctx.createLinearGradient(0,0,0,h);
  g.addColorStop(0,col+'44');g.addColorStop(1,col+'00');
  ctx.beginPath();ctx.moveTo(0,h);pts.forEach(([x,y])=>ctx.lineTo(x,y));ctx.lineTo(w,h);ctx.closePath();ctx.fillStyle=g;ctx.fill();
  ctx.beginPath();pts.forEach(([x,y],i)=>i?ctx.lineTo(x,y):ctx.moveTo(x,y));
  ctx.strokeStyle=col;ctx.lineWidth=1.5;ctx.lineJoin='round';ctx.stroke();
}

// ══════════════════════════════════════════════════
// RENDER — each function is independent, safe to call anytime
// ══════════════════════════════════════════════════
function render(){
  try{renderDebug();}catch(_){}
  try{renderStats();}catch(_){}
  try{renderTabs();}catch(_){}
  try{renderMarket();}catch(_){}
  try{renderSignalDetail();}catch(_){}
  try{renderPosition();}catch(_){}
  try{renderHistory();}catch(_){}
}
function renderDebug(){
  const el=G('d-pairs');if(!el)return;
  el.innerHTML=PAIRS.map(sym=>{
    const d=RAW[sym],s=SIG[sym];
    const c=s.sig==='LONG'?'var(--g)':s.sig==='SHORT'?'var(--r)':'var(--dim)';
    return`<span style="color:${c}">${DISP[sym]}:${d.ready?'$'+fp(d.price):'...'} ${s.sig}(L${s.ls}S${s.ss})</span>`;
  }).join('<span style="color:#1a2535"> | </span>');
  const db=G('d-bot');if(db)db.textContent=botOn?'ON':'OFF';
  const dc=G('d-cd');if(dc)dc.textContent=Object.entries(cooldowns).filter(([,v])=>v>0).map(([k,v])=>`${k.replace('USDT','')}:${v}`).join(' ')||'none';
}
function renderStats(){
  const wr=stats.n>0?(stats.w/stats.n*100).toFixed(0)+'%':'--%';
  const delta=BAL-START_BAL;
  const sb=G('s-bal');if(sb){sb.textContent=`$${BAL.toFixed(2)}`;sb.style.color=pc(delta);}
  const sb2=G('s-bal2');if(sb2)sb2.textContent=`${delta>=0?'+':''}$${delta.toFixed(2)} this session`;
  const sp=G('s-pnl');if(sp){sp.textContent=`${stats.pnl>=0?'+':''}$${stats.pnl.toFixed(2)}`;sp.style.color=pc(stats.pnl);}
  const sp2=G('s-pnl2');if(sp2)sp2.textContent=`${stats.n} closed`;
  const sw=G('s-wr');if(sw){sw.textContent=wr;sw.style.color=parseFloat(wr)>=55?'var(--g)':parseFloat(wr)<45&&stats.n>2?'var(--r)':'var(--y)';}
  const sw2=G('s-wr2');if(sw2)sw2.textContent=`${stats.w}W ${stats.l}L ${stats.be}BE`;
  const spos=G('s-pos'),spos2=G('s-pos2');
  if(openPos){
    if(spos){spos.textContent=`${openPos.dir} ${DISP[openPos.sym]}`;spos.style.color=openPos.dir==='LONG'?'var(--g)':'var(--r)';}
    if(spos2){const u=openPos.uPnl||0;spos2.textContent=`${u>=0?'+':''}$${u.toFixed(2)} unrealised`;spos2.style.color=pc(u);}
  }else{
    if(spos){spos.textContent='NONE';spos.style.color='var(--dim)';}
    if(spos2)spos2.textContent='No active trade';
  }
}
function renderTabs(){
  const el=G('tabs');if(!el)return;
  el.innerHTML=PAIRS.map(sym=>{
    const s=SIG[sym];
    const c=s.sig==='LONG'?'var(--g)':s.sig==='SHORT'?'var(--r)':'transparent';
    const badge=s.sig!=='WAIT'?`<span style="color:${c};border:1px solid ${c};border-radius:2px;padding:1px 4px;font-size:8px;margin-left:3px">${s.sig}</span>`:'';
    return`<div class="tab ${sym===activePair?'on':''}" onclick="activePair='${sym}';renderTabs();renderMarket();renderSignalDetail();">${DISP[sym]}${badge}</div>`;
  }).join('');
}
function renderMarket(){
  const el=G('mrows');if(!el)return;
  el.innerHTML=PAIRS.map(sym=>{
    const d=RAW[sym],s=SIG[sym];
    const sc=s.sig==='LONG'?'var(--g)':s.sig==='SHORT'?'var(--r)':'var(--dim)';
    const rc=s.rsi<40?'var(--g)':s.rsi>60?'var(--r)':'var(--y)';
    const isOpen=openPos&&openPos.sym===sym;
    const cd=cooldowns[sym]||0;
    return`<div class="mrow ${sym===activePair?'on':''}" onclick="activePair='${sym}';renderTabs();renderMarket();renderSignalDetail();" style="${isOpen?'background:#07120a':''}">
      <div>
        <div style="font-weight:700;color:${isOpen?'var(--g)':'#9ab0cc'}">${DISP[sym]}${isOpen?' 🟢':''}</div>
        <div style="font-size:9px;color:${s.ema20>s.ema50?'var(--g)':'var(--r)'}">EMA${s.ema20>s.ema50?'↑BULL':'↓BEAR'}${cd?' CD:'+cd:''}</div>
      </div>
      <div>
        <div style="font-weight:600">${d.ready?'$'+fp(d.price):'Loading...'}</div>
        <div style="font-size:9px;color:${d.ready?'var(--dim)':'var(--y)'}"> ${d.ready?'LIVE':'WAIT'}</div>
      </div>
      <div><canvas id="sp-${sym}" width="80" height="26"></canvas></div>
      <div style="color:${rc}">${s.rsi.toFixed(0)}
        <div style="height:3px;background:#111827;border-radius:2px;margin-top:3px">
          <div style="width:${s.rsi}%;height:100%;background:${rc};border-radius:2px;transition:width .5s"></div>
        </div>
      </div>
      <div style="color:${sc};font-size:10px;line-height:1.8">L${s.ls}/3<br>S${s.ss}/3</div>
      <div><span style="font-size:10px;font-weight:700;color:${sc};background:${sc}18;border:1px solid ${sc}40;border-radius:3px;padding:3px 6px">${s.sig}</span></div>
    </div>`;
  }).join('');
  PAIRS.forEach(sym=>{
    const c=G('sp-'+sym),d=RAW[sym];
    if(c&&d.hist.length>1){const l=d.hist[d.hist.length-1],f=d.hist[0];drawSpark(c,d.hist,l>=f?'#00e5a0':'#ff4060');}
  });
}
function renderSignalDetail(){
  const s=SIG[activePair],d=RAW[activePair];
  const el=G('ind-detail');if(!el)return;
  const sc=s.sig==='LONG'?'var(--g)':s.sig==='SHORT'?'var(--r)':'var(--dim)';
  el.innerHTML=`
    <b style="color:var(--dim);letter-spacing:1px">SIGNAL DETAIL — ${DISP[activePair]}</b><br>
    RSI: <b style="color:${s.rsi<40?'var(--g)':s.rsi>60?'var(--r)':'var(--y)'}">${s.rsi.toFixed(1)}</b> &nbsp;|&nbsp;
    EMA20: <b style="color:#6a8aaa">$${fp(s.ema20)}</b> &nbsp;|&nbsp;
    EMA50: <b style="color:#6a8aaa">$${fp(s.ema50)}</b> &nbsp;|&nbsp;
    MACD: <b style="color:${s.macd>0?'var(--g)':'var(--r)'}">${s.macd>0?'▲':'▼'}${Math.abs(s.macd).toFixed(3)}</b><br>
    LONG <b style="color:var(--g)">${s.ls}/3</b> &nbsp;|&nbsp; SHORT <b style="color:var(--r)">${s.ss}/3</b> &nbsp;|&nbsp;
    Signal: <b style="color:${sc}">${s.sig}</b><br>
    <span style="color:var(--dim)">${s.reason}</span>`;
}
function renderPosition(){
  const el=G('pos-body'),oid=G('pos-id');
  if(!openPos){
    if(el)el.innerHTML=`<div class="empty">${botOn?`⏳ Scanning… ${PAIRS.map(p=>SIG[p].sig).join(' ')}`:'Press START to begin automated testnet trading'}</div>`;
    if(oid)oid.textContent='—';return;
  }
  const pos=openPos,cur=RAW[pos.sym]?.price||pos.entry;
  const pct=(pos.dir==='LONG'?(cur-pos.entry)/pos.entry:(pos.entry-cur)/pos.entry)*100;
  const u=pos.uPnl||0,dc=pos.dir==='LONG'?'var(--g)':'var(--r)';
  const dot=Math.min(95,Math.max(2,((pct+SL_PCT*100)/((TP_PCT+SL_PCT)*100))*100));
  if(oid)oid.textContent=`#${pos.orderId}`;
  if(el)el.innerHTML=`<div style="padding:10px 14px">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;flex-wrap:wrap;gap:5px">
      <div style="display:flex;align-items:center;gap:6px;flex-wrap:wrap">
        <b style="font-size:13px">${DISP[pos.sym]}</b>
        <span style="color:${dc};background:${dc}15;border:1px solid ${dc}40;border-radius:3px;padding:2px 8px;font-size:10px">${pos.dir} ${LEV}×</span>
      </div>
      <div style="font-size:16px;font-weight:700;color:${pc(u)}">${u>=0?'+':''}$${u.toFixed(2)} <span style="font-size:10px">(${pct>=0?'+':''}${pct.toFixed(2)}%)</span></div>
    </div>
    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin:8px 0">
      ${[['ENTRY','$'+fp(pos.entry)],['CURRENT','$'+fp(cur)],['QTY',pos.q],['SL/TP','$'+fp(pos.slP)+'/'+fp(pos.tpP)]].map(([l,v])=>`
        <div style="background:var(--bg);border-radius:4px;padding:6px 8px">
          <div style="font-size:8px;color:var(--dim);margin-bottom:2px">${l}</div>
          <div style="font-size:10px;color:#9ab0cc">${v}</div>
        </div>`).join('')}
    </div>
    <div style="position:relative;height:5px;background:#1a2535;border-radius:3px;margin-top:8px">
      <div style="position:absolute;left:0;top:0;height:100%;width:33%;background:#ff406015;border-radius:3px 0 0 3px"></div>
      <div style="position:absolute;right:0;top:0;height:100%;width:33%;background:#00e5a015;border-radius:0 3px 3px 0"></div>
      <div style="position:absolute;top:-3px;width:10px;height:10px;border-radius:50%;border:2px solid var(--bg);left:calc(${dot}% - 5px);background:${pc(u)};transition:left .4s"></div>
    </div>
    <div style="display:flex;justify-content:space-between;font-size:8px;color:var(--dim);margin-top:3px">
      <span>SL $${fp(pos.slP)}</span><span style="color:var(--y)">Since ${pos.time}</span><span>TP $${fp(pos.tpP)}</span>
    </div>
  </div>`;
}
function renderHistory(){
  const cnt=G('h-cnt');if(cnt)cnt.textContent=trades.length;
  const el=G('hist');if(!el)return;
  el.innerHTML=trades.length?trades.slice(0,12).map(t=>{
    const bg=t.pnl>0.01?'#070f0a':t.pnl<-0.01?'#0f0708':'transparent';
    const dc=t.dir==='LONG'?'var(--g)':'var(--r)';
    return`<div style="display:grid;grid-template-columns:62px 78px 48px 65px 64px 1fr;padding:7px 14px;border-bottom:1px solid #0d1220;font-size:10px;align-items:center;background:${bg}">
      <span style="color:var(--dim)">${t.time}</span>
      <span style="color:#8a9ab8">${DISP[t.sym]}</span>
      <span style="color:${dc}">${t.dir}</span>
      <span style="color:var(--dim)">$${fp(t.entry)}</span>
      <span style="color:${pc(t.pnl)};font-weight:700">${t.pnl>=0?'+':''}$${t.pnl}</span>
      <span style="color:var(--dim);font-size:9px">[${t.reason}]</span>
    </div>`;
  }).join(''):'<div class="empty">No trades this session</div>';
}
function renderLog(){
  const el=G('log');if(!el)return;
  const tc={win:'var(--g)',loss:'var(--r)',open:'var(--y)',info:'var(--dim)'};
  el.innerHTML=logs.map(l=>`<div style="padding:5px 11px;border-bottom:1px solid #0d1220;font-size:10px;line-height:1.4;color:${tc[l.type]||'var(--dim)'}"><span style="color:#1a2535;margin-right:5px">${l.t}</span>${l.msg}</div>`).join('');
}
// Enter key
document.addEventListener('keydown',e=>{
  if(e.key==='Enter'&&G('setup').style.display!=='none')doConnect();
});
</script>
</body>
</html>
