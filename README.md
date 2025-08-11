<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Through the Bible — Reading Plan</title>
<meta name="color-scheme" content="light dark">
<style>
  :root{
    /* Dark header + light content to echo your site */
    --bg: #0a0a0a;           /* page background */
    --panel: #101214;        /* card bg */
    --panel-2:#0d0f12;
    --text: #eaeaea;         /* body text */
    --muted:#a1a1aa;         /* secondary text */
    --border:#1f242a;        /* borders */
    --primary:#ffffff;       /* buttons / emphasis on dark */
    --primary-text:#0a0a0a;  /* button text on light btn */
    --accent:#d4a017;        /* warm gold accent (subtle) */
    --radius: 16px;
    --font: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif;
  }
  html,body{height:100%}
  body{
    margin:0;background:var(--bg);color:var(--text);font-family:var(--font);
    -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
  }
  .hero{
    background: linear-gradient(180deg,#000 0%, #0b0b0b 70%, transparent 100%);
    padding: 28px 20px 8px; text-align:center; border-bottom:1px solid #151515;
  }
  .title{font-weight:800;letter-spacing:.4px;margin:0;font-size: clamp(22px, 3.5vw, 34px);color:#fff}
  .subtitle{margin:.35rem 0 0;color:#ccc;font-size:clamp(12px,1.7vw,14px)}
  .container{max-width:1080px;margin:10px auto 48px;padding:0 16px}
  .card{
    background:var(--panel); border:1px solid var(--border); border-radius:var(--radius);
    padding:16px; box-shadow:0 10px 30px rgba(0,0,0,.25);
  }
  .controls{
    display:grid; gap:12px; grid-template-columns: repeat(12,1fr); margin-bottom:8px;
  }
  .col-3{grid-column: span 3;}
  .col-4{grid-column: span 4;}
  .col-6{grid-column: span 6;}
  .col-12{grid-column: span 12;}
  @media (max-width:900px){
    .col-6,.col-4,.col-3{grid-column: span 12;}
  }
  label{display:block; font-size:12px; color:var(--muted); margin:2px 0 6px}
  select, input[type="date"], input[type="number"]{
    width:100%; padding:11px 12px; border-radius:12px; border:1px solid var(--border);
    background:var(--panel-2); color:var(--text); font-size:15px; outline:none;
  }
  .chip-row{display:flex;flex-wrap:wrap;gap:8px}
  .chip{
    padding:8px 12px; border-radius:999px; border:1px solid var(--border); background:var(--panel-2);
    color:var(--text); font-size:14px; cursor:pointer; user-select:none;
  }
  .chip[disabled]{opacity:.35; cursor:not-allowed}
  .chip.active{background:#fff;color:#000;border-color:#fff}
  .row{display:flex;align-items:center;gap:12px;flex-wrap:wrap}
  .btn{
    appearance:none; border:0; padding:11px 14px; border-radius:12px; font-weight:700; cursor:pointer;
  }
  .btn.primary{ background:#fff; color:#000 }
  .btn.secondary{ background:transparent; color:#fff; border:1px solid #fff }
  .btn.ghost{ background:transparent; color:#fff; opacity:.85 }
  .note{ color:var(--muted); font-size:13px }
  .progress{ height:10px; background:#161a1f; border-radius:999px; overflow:hidden; margin:6px 0 0 }
  .progress>span{ display:block; height:100%; width:0%; background:var(--accent) }
  .table-wrap{ margin-top:10px; border:1px solid var(--border); border-radius:12px; overflow:hidden }
  table{ width:100%; border-collapse:collapse; background:#0c0e11; color:#e8e8e8; font-size:15px }
  thead th{ position:sticky; top:0; background:#0f1216; padding:10px 12px; text-align:left; border-bottom:1px solid var(--border) }
  tbody td{ border-top:1px solid var(--border); padding:10px 12px; vertical-align:top }
  .checkcell{ width:44px; text-align:center }
  .daycell{ white-space:nowrap }
  .pill{ display:inline-block; padding:2px 8px; border-radius:999px; font-size:12px; background:#1b2026; color:#cfcfcf }
  .divider{height:1px;background:var(--border);margin:10px 0}
  .footer{color:#9aa1ab; font-size:12px; text-align:center; margin-top:18px}
  a.footer-link{color:#cfd6ff;text-decoration:none}
</style>
</head>
<body>
  <header class="hero">
    <h1 class="title">THROUGH THE BIBLE — READING PLAN</h1>
    <p class="subtitle">Default preset: <strong>Through the Bible Course (365 days)</strong> — Balanced OT/NT with Psalms &amp; Proverbs distributed.</p>
  </header>

  <main class="container">
    <section class="card" aria-label="Reading Plan Builder">
      <div class="controls">
        <div class="col-4">
          <label>Preset</label>
          <select id="presetSelect">
            <option value="tbc365">Through the Bible Course (365) — Default</option>
            <option value="balanced">Custom Balanced (choose pace)</option>
            <option value="sequential">Custom Sequential (choose pace)</option>
          </select>
        </div>
        <div class="col-6">
          <label>Pace</label>
          <div class="chip-row" id="paceChips">
            <button class="chip" data-days="30">30 days</button>
            <button class="chip" data-days="60">60 days</button>
            <button class="chip" data-days="90">90 days</button>
            <button class="chip" data-days="180">180 days</button>
            <button class="chip" data-days="365">365 days</button>
            <button class="chip" id="customChip">Custom…</button>
          </div>
        </div>
        <div class="col-3">
          <label>Custom days</label>
          <input id="customDays" type="number" min="1" placeholder="e.g., 120">
        </div>
        <div class="col-3">
          <label>Start date</label>
          <input id="startDate" type="date">
        </div>
        <div class="col-4">
          <label>Plan style</label>
          <select id="planStyle">
            <option value="balanced">Balanced (OT + NT)</option>
            <option value="sequential">Sequential (Genesis → Revelation)</option>
          </select>
        </div>
        <div class="col-4">
          <label>&nbsp;</label>
          <div class="row" style="align-items:center">
            <input id="spreadWisdom" type="checkbox" checked>
            <span class="note">Evenly distribute Psalms &amp; Proverbs</span>
          </div>
        </div>
      </div>

      <div class="row" style="justify-content:space-between;margin:8px 0 6px">
        <div class="row">
          <span class="pill">Progress saved on this device</span>
        </div>
        <div class="row">
          <button class="btn primary" id="generateBtn">Generate plan</button>
          <button class="btn secondary" id="exportBtn" disabled>Export CSV</button>
          <button class="btn ghost" id="resetBtn">Reset progress</button>
        </div>
      </div>

      <div class="progress"><span id="progressBar"></span></div>
      <div class="note" id="summaryLine" style="margin-top:6px"></div>
      <div class="divider"></div>

      <div id="tableWrap" class="table-wrap" style="display:none">
        <table>
          <thead>
            <tr><th class="checkcell">Done</th><th class="daycell">Day / Date</th><th>Readings</th></tr>
          </thead>
          <tbody id="planBody"></tbody>
        </table>
      </div>
    </section>

    <p class="footer">Tip: Add this page to your phone’s Home Screen for quick daily access.</p>
  </main>

<script>
(() => {
  // ---------- Data ----------
  const BOOKS = [
    {book:'Genesis',chapters:50,testament:'OT'},
    {book:'Exodus',chapters:40,testament:'OT'},
    {book:'Leviticus',chapters:27,testament:'OT'},
    {book:'Numbers',chapters:36,testament:'OT'},
    {book:'Deuteronomy',chapters:34,testament:'OT'},
    {book:'Joshua',chapters:24,testament:'OT'},
    {book:'Judges',chapters:21,testament:'OT'},
    {book:'Ruth',chapters:4,testament:'OT'},
    {book:'1 Samuel',chapters:31,testament:'OT'},
    {book:'2 Samuel',chapters:24,testament:'OT'},
    {book:'1 Kings',chapters:22,testament:'OT'},
    {book:'2 Kings',chapters:25,testament:'OT'},
    {book:'1 Chronicles',chapters:29,testament:'OT'},
    {book:'2 Chronicles',chapters:36,testament:'OT'},
    {book:'Ezra',chapters:10,testament:'OT'},
    {book:'Nehemiah',chapters:13,testament:'OT'},
    {book:'Esther',chapters:10,testament:'OT'},
    {book:'Job',chapters:42,testament:'OT'},
    {book:'Psalms',chapters:150,testament:'OT',tag:'psalms'},
    {book:'Proverbs',chapters:31,testament:'OT',tag:'proverbs'},
    {book:'Ecclesiastes',chapters:12,testament:'OT'},
    {book:'Song of Songs',chapters:8,testament:'OT'},
    {book:'Isaiah',chapters:66,testament:'OT'},
    {book:'Jeremiah',chapters:52,testament:'OT'},
    {book:'Lamentations',chapters:5,testament:'OT'},
    {book:'Ezekiel',chapters:48,testament:'OT'},
    {book:'Daniel',chapters:12,testament:'OT'},
    {book:'Hosea',chapters:14,testament:'OT'},
    {book:'Joel',chapters:3,testament:'OT'},
    {book:'Amos',chapters:9,testament:'OT'},
    {book:'Obadiah',chapters:1,testament:'OT'},
    {book:'Jonah',chapters:4,testament:'OT'},
    {book:'Micah',chapters:7,testament:'OT'},
    {book:'Nahum',chapters:3,testament:'OT'},
    {book:'Habakkuk',chapters:3,testament:'OT'},
    {book:'Zephaniah',chapters:3,testament:'OT'},
    {book:'Haggai',chapters:2,testament:'OT'},
    {book:'Zechariah',chapters:14,testament:'OT'},
    {book:'Malachi',chapters:4,testament:'OT'},
    {book:'Matthew',chapters:28,testament:'NT'},
    {book:'Mark',chapters:16,testament:'NT'},
    {book:'Luke',chapters:24,testament:'NT'},
    {book:'John',chapters:21,testament:'NT'},
    {book:'Acts',chapters:28,testament:'NT'},
    {book:'Romans',chapters:16,testament:'NT'},
    {book:'1 Corinthians',chapters:16,testament:'NT'},
    {book:'2 Corinthians',chapters:13,testament:'NT'},
    {book:'Galatians',chapters:6,testament:'NT'},
    {book:'Ephesians',chapters:6,testament:'NT'},
    {book:'Philippians',chapters:4,testament:'NT'},
    {book:'Colossians',chapters:4,testament:'NT'},
    {book:'1 Thessalonians',chapters:5,testament:'NT'},
    {book:'2 Thessalonians',chapters:3,testament:'NT'},
    {book:'1 Timothy',chapters:6,testament:'NT'},
    {book:'2 Timothy',chapters:4,testament:'NT'},
    {book:'Titus',chapters:3,testament:'NT'},
    {book:'Philemon',chapters:1,testament:'NT'},
    {book:'Hebrews',chapters:13,testament:'NT'},
    {book:'James',chapters:5,testament:'NT'},
    {book:'1 Peter',chapters:5,testament:'NT'},
    {book:'2 Peter',chapters:3,testament:'NT'},
    {book:'1 John',chapters:5,testament:'NT'},
    {book:'2 John',chapters:1,testament:'NT'},
    {book:'3 John',chapters:1,testament:'NT'},
    {book:'Jude',chapters:1,testament:'NT'},
    {book:'Revelation',chapters:22,testament:'NT'}
  ];

  // ---------- Helpers ----------
  const $ = s => document.querySelector(s);
  const todayISO = new Date().toISOString().slice(0,10);
  const addDays = (iso,n)=>{ const d=new Date(iso+'T00:00:00'); d.setDate(d.getDate()+n); return d.toISOString().slice(0,10); };
  const niceDate = iso => new Date(iso+'T00:00:00').toLocaleDateString(undefined,{year:'numeric',month:'short',day:'numeric'});

  function makeChapterStream(filter){
    const out=[]; for(const b of BOOKS.filter(filter)){ for(let c=1;c<=b.chapters;c++){ out.push({book:b.book,chapter:c}); } }
    return out;
  }
  function distributeStream(stream, days){
    const total = stream.length, per = total/days;
    const out = Array.from({length:days}, ()=>[]);
    let acc=0,i=0;
    for(let d=0; d<days; d++){
      acc += per;
      let take = Math.round(acc) - i;
      if (d === days-1) take = total - i;
      for(let t=0; t<take && i<total; t++,i++) out[d].push(stream[i]);
    }
    return out;
  }
  function spreadEvenly(count, days){
    if(!count) return [];
    const idxs=[]; for(let i=0;i<count;i++){ idxs.push(Math.round(i*(days-1)/(count-1))); } return idxs;
  }
  function refsToText(refs){
    if(!refs||!refs.length) return '';
    const out=[]; let i=0; 
    while(i<refs.length){
      const b=refs[i].book; let s=refs[i].chapter, e=s; i++;
      while(i<refs.length && refs[i].book===b && refs[i].chapter===e+1){ e=refs[i].chapter; i++; }
      out.push(`${b} ${s}${e>s?`–${e}`:''}`);
    }
    return out.join('; ');
  }
  function toCSV(rows){ const esc=s=>`"${String(s).replace(/"/g,'""')}"`; return rows.map(r=>r.map(esc).join(',')).join('\n'); }

  // ---------- Engines ----------
  function buildBalancedPlan(days, startISO, {spreadWisdom=true}={}){
    const ot = makeChapterStream(b=>b.testament==='OT' && b.tag!=='psalms' && b.tag!=='proverbs');
    const nt = makeChapterStream(b=>b.testament==='NT');
    const wisdom = makeChapterStream(b=>b.tag==='psalms'||b.tag==='proverbs');

    const otChunks = distributeStream(ot, days);
    const ntChunks = distributeStream(nt, days);

    let wisdomMap = Array.from({length:days},()=>[]);
    if (spreadWisdom){
      const idxs = spreadEvenly(wisdom.length, days);
      for(let i=0;i<wisdom.length;i++){ wisdomMap[idxs[i]].push(wisdom[i]); }
    } else {
      wisdomMap = distributeStream(wisdom, days);
    }

    return Array.from({length:days}, (_,i)=>({
      day:i+1, dateISO:addDays(startISO,i),
      bundle:{ ot:otChunks[i], nt:ntChunks[i], wisdom:wisd omMap[i] }
    }));
  }
  function buildSequentialPlan(days, startISO){
    const seq = makeChapterStream(()=>true);
    const chunks = distributeStream(seq, days);
    return chunks.map((c,i)=>({day:i+1, dateISO:addDays(startISO,i), bundle:{seq:c}}));
  }
  function buildTBC365(startISO){ return buildBalancedPlan(365, startISO, {spreadWisdom:true}); }

  // ---------- UI + Storage ----------
  const presetSelect = $('#presetSelect');
  const paceChips = $('#paceChips');
  const customChip = $('#customChip');
  const customDays = $('#customDays');
  const startDate = $('#startDate');
  const planStyle = $('#planStyle');
  const spreadWisdom = $('#spreadWisdom');
  const generateBtn = $('#generateBtn');
  const exportBtn = $('#exportBtn');
  const resetBtn = $('#resetBtn');
  const tableWrap = $('#tableWrap');
  const planBody = $('#planBody');
  const summaryLine = $('#summaryLine');
  const progressBar = $('#progressBar');

  const SETTINGS_KEY = 'ttb-standalone-settings-v1';
  const PROGRESS_KEY = 'ttb-standalone-progress-v1';

  function saveSettings(s){ localStorage.setItem(SETTINGS_KEY, JSON.stringify(s)); }
  function loadSettings(){ try{ return JSON.parse(localStorage.getItem(SETTINGS_KEY))||null }catch{return null} }
  function saveProgress(set){ localStorage.setItem(PROGRESS_KEY, JSON.stringify(Array.from(set))); }
  function loadProgress(){ try{ return new Set(JSON.parse(localStorage.getItem(PROGRESS_KEY))||[]) }catch{return new Set()} }

  function setActiveChip(days){
    paceChips.querySelectorAll('.chip').forEach(c=>c.classList.remove('active'));
    const btn = paceChips.querySelector(`.chip[data-days="${days}"]`);
    if (btn) btn.classList.add('active');
  }

  // defaults
  startDate.value = todayISO;
  presetSelect.value = 'tbc365';
  setActiveChip(365);
  planStyle.value = 'balanced';
  spreadWisdom.checked = true;
  lockForPreset();

  // restore
  const prev = loadSettings();
  if (prev){
    presetSelect.value = prev.preset || 'tbc365';
    if (prev.days){
      if ([30,60,90,180,365].includes(prev.days)) setActiveChip(prev.days);
      else { customChip.classList.add('active'); customDays.value = prev.days; }
    }
    startDate.value = prev.startDate || todayISO;
    planStyle.value = prev.planStyle || 'balanced';
    if (typeof prev.spreadWisdom === 'boolean') spreadWisdom.checked = prev.spreadWisdom;
    lockForPreset();
  }

  paceChips.addEventListener('click', e=>{
    const btn = e.target.closest('.chip'); if(!btn || btn.hasAttribute('disabled')) return;
    if (btn.id==='customChip'){
      customChip.classList.add('active');
      paceChips.querySelectorAll('.chip').forEach(b=>{ if(b!==customChip) b.classList.remove('active'); });
    } else {
      setActiveChip(btn.dataset.days);
      customChip.classList.remove('active');
    }
  });

  presetSelect.addEventListener('change', lockForPreset);
  function lockForPreset(){
    const isTBC = presetSelect.value==='tbc365';
    planStyle.disabled = isTBC;
    spreadWisdom.disabled = isTBC;
    customDays.disabled = isTBC;
    paceChips.querySelectorAll('.chip').forEach(ch=>ch.toggleAttribute('disabled', isTBC));
    if (isTBC){
      setActiveChip(365);
      planStyle.value='balanced'; spreadWisdom.checked=true;
    }
  }

  resetBtn.addEventListener('click', ()=>{
    saveProgress(new Set());
    planBody.querySelectorAll('input[type="checkbox"][data-day]').forEach(cb=>cb.checked=false);
    updateProgress();
  });

  function buildPlan(){
    const startISO = startDate.value || todayISO;
    if (presetSelect.value==='tbc365'){
      return {
        rows: buildTBC365(startISO),
        meta: {label:'Through the Bible Course (365)', days:365, style:'Balanced OT/NT • Psalms & Proverbs: Distributed'}
      };
    }
    // custom
    const customActive = customChip.classList.contains('active');
    let days = customActive ? parseInt(customDays.value||'0',10)
                            : parseInt((paceChips.querySelector('.chip.active')?.dataset.days)||'',10);
    if(!days || days<1) throw new Error('Please select a pace or enter a valid number of days.');
    const style = planStyle.value;
    const spread = !!spreadWisdom.checked;
    const rows = style==='sequential' ? buildSequentialPlan(days, startISO)
                                      : buildBalancedPlan(days, startISO, {spreadWisdom:spread});
    return {
      rows,
      meta: {label:'Custom Plan', days, style: style==='sequential' ? 'Sequential' : `Balanced OT/NT • Psalms & Proverbs: ${spread?'Distributed':'Grouped'}`}
    };
  }

  function render(plan){
    const progress = loadProgress();
    planBody.innerHTML = '';
    plan.rows.forEach(r=>{
      const tr = document.createElement('tr');
      const id = String(r.day);
      const cb = document.createElement('input');
      cb.type='checkbox'; cb.dataset.day=id; cb.checked=progress.has(id);
      cb.addEventListener('change', ()=>{
        const s=loadProgress(); if(cb.checked) s.add(id); else s.delete(id); saveProgress(s); updateProgress();
      });
      let readings='';
      if (r.bundle.seq){ readings = refsToText(r.bundle.seq); }
      else {
        const parts=[];
        const ot = refsToText(r.bundle.ot);
        const nt = refsToText(r.bundle.nt);
        const wi = refsToText(r.bundle.wisdom);
        if (ot) parts.push(`<strong>OT:</strong> ${ot}`);
        if (nt) parts.push(`<strong>NT:</strong> ${nt}`);
        if (wi) parts.push(`<strong>Psalms/Proverbs:</strong> ${wi}`);
        readings = parts.join('<br>');
      }
      tr.innerHTML = `<td class="checkcell"></td>
                      <td class="daycell"><strong>Day ${r.day}</strong><br><span class="note">${niceDate(r.dateISO)}</span></td>
                      <td>${readings}</td>`;
      tr.children[0].appendChild(cb);
      planBody.appendChild(tr);
    });
    tableWrap.style.display='block';
    const first = plan.rows[0]?.dateISO, last = plan.rows[plan.rows.length-1]?.dateISO;
    summaryLine.textContent = `${plan.meta.label} • ${plan.meta.days} days • ${niceDate(first)} → ${niceDate(last)} • ${plan.meta.style}`;
    updateProgress();
    exportBtn.disabled = false;
  }

  function updateProgress(){
    const total = planBody.querySelectorAll('input[type="checkbox"][data-day]').length;
    const done = loadProgress().size;
    const pct = total ? Math.round(done/total*100) : 0;
    progressBar.style.width = pct+'%';
    summaryLine.textContent = summaryLine.textContent.replace(/ · Progress: .+$/,'');
    if (total) summaryLine.textContent += ` · Progress: ${done}/${total} (${pct}%)`;
  }

  // Generate + Export
  let currentPlan=null;
  generateBtn.addEventListener('click', ()=>{
    try{
      const plan = buildPlan(); currentPlan = plan;
      // persist choices
      const customActive = customChip.classList.contains('active');
      const days = presetSelect.value==='tbc365' ? 365 :
        (customActive ? parseInt(customDays.value||'0',10) : parseInt((paceChips.querySelector('.chip.active')?.dataset.days)||'',10));
      saveSettings({
        preset: presetSelect.value,
        days,
        startDate: startDate.value || todayISO,
        planStyle: planStyle.value,
        spreadWisdom: !!spreadWisdom.checked
      });
      render(plan);
    }catch(err){ alert(err.message||String(err)); }
  });

  exportBtn.addEventListener('click', ()=>{
    if(!currentPlan) return;
    const rows = [['Day','Date','Readings']];
    currentPlan.rows.forEach(r=>{
      let readings='';
      if (r.bundle.seq) readings = refsToText(r.bundle.seq);
      else{
        const parts=[];
        const ot=refsToText(r.bundle.ot), nt=refsToText(r.bundle.nt), wi=refsToText(r.bundle.wisdom);
        if (ot) parts.push(`OT: ${ot}`); if (nt) parts.push(`NT: ${nt}`); if (wi) parts.push(`Psalms/Proverbs: ${wi}`);
        readings = parts.join(' | ');
      }
      rows.push([`Day ${r.day}`, niceDate(r.dateISO), readings]);
    });
    const blob=new Blob([toCSV(rows)],{type:'text/csv;charset=utf-8;'});
    const url=URL.createObjectURL(blob); const a=document.createElement('a');
    a.href=url; a.download='through-the-bible-plan.csv'; a.click(); URL.revokeObjectURL(url);
  });

  // First render (default preset today)
  try{ currentPlan = {rows: buildTBC365(todayISO), meta:{label:'Through the Bible Course (365)', days:365, style:'Balanced OT/NT • Psalms & Proverbs: Distributed'}};
       render(currentPlan); }catch{}
})();
</script>
</body>
</html>

