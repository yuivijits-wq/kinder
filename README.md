<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Kindergarten Care Dashboard — Student Health & Safety</title>

  <!-- Modern playful font + Chart.js CDN -->
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;600;800&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>

  <style>
    :root{
      --bg: #fff9f2;
      --card: #ffffff;
      --muted: #6b6b6b;
      --accent: #ff7aa2; /* pink */
      --accent-2: #ffd166; /* soft yellow */
      --accent-3: #6dd3b3; /* mint */
      --shadow: 0 6px 20px rgba(16,24,40,0.08);
      --radius: 14px;
      --glass: rgba(255,255,255,0.6);
    }
    *{box-sizing:border-box}
    html,body{height:100%;}
    body{
      margin:0;
      font-family: "Nunito", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background:
        radial-gradient(1200px 400px at -10% -10%, rgba(255,122,162,0.06), transparent 10%),
        radial-gradient(800px 300px at 110% 110%, rgba(109,211,179,0.05), transparent 10%),
        var(--bg);
      color:#1f2937;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      padding:24px;
    }

    .container{
      max-width:1200px;
      margin:0 auto;
    }

    header{
      display:flex;
      gap:16px;
      align-items:center;
      justify-content:space-between;
      margin-bottom:18px;
    }

    .brand{
      display:flex;
      gap:12px;
      align-items:center;
    }
    .logo{
      width:64px;
      height:64px;
      background:linear-gradient(135deg,var(--accent),var(--accent-2));
      border-radius:18px;
      display:flex;
      align-items:center;
      justify-content:center;
      color:white;
      font-weight:800;
      box-shadow: var(--shadow);
      font-size:22px;
    }
    h1{font-size:20px; margin:0}
    p.lead{margin:0; color:var(--muted); font-size:13px}

    .controls{
      display:flex;
      gap:10px;
      align-items:center;
      flex-wrap:wrap;
    }
    .control{
      display:flex;
      gap:8px;
      align-items:center;
      background:var(--card);
      padding:8px 12px;
      border-radius:12px;
      box-shadow:var(--shadow);
    }
    select,input[type=date]{
      border:0;
      background:transparent;
      font-size:14px;
      outline:none;
    }
    button.primary{
      background:linear-gradient(90deg,var(--accent),var(--accent-2));
      color:white;
      border:0;
      padding:8px 12px;
      border-radius:12px;
      font-weight:700;
      box-shadow:0 6px 18px rgba(255,122,162,0.18);
      cursor:pointer;
    }
    main{
      display:grid;
      grid-template-columns: 1fr 380px;
      gap:20px;
      align-items:start;
    }

    /* left area */
    .panels{
      display:grid;
      gap:16px;
    }

    .cards{
      display:grid;
      grid-template-columns: repeat(3,1fr);
      gap:12px;
    }
    .card{
      background:var(--card);
      border-radius:var(--radius);
      padding:14px;
      box-shadow:var(--shadow);
      display:flex;
      gap:12px;
      align-items:center;
    }
    .icon{
      width:54px;
      height:54px;
      border-radius:12px;
      display:grid;
      place-items:center;
      font-size:22px;
      color:white;
      flex-shrink:0;
    }
    .icon.all{ background:linear-gradient(135deg,var(--accent),#ffb1c9) }
    .icon.beh{ background:linear-gradient(135deg,var(--accent-3),#8de9d1) }
    .icon.ill{ background:linear-gradient(135deg,#ffd166,#ffefd6) ; color:#6b4a00}
    .icon.acc{ background:linear-gradient(135deg,#a3b3ff,#d9e0ff) ; color:#172554}

    .card .meta{ font-size:13px; color:var(--muted) }
    .card .value{ font-size:20px; font-weight:800 }

    .panel{
      background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(255,255,255,0.98));
      border-radius:18px;
      padding:16px;
      box-shadow:var(--shadow);
    }

    .flex-row{display:flex; align-items:center; justify-content:space-between; gap:12px}
    .chart-wrap{height:240px}

    /* right sidebar */
    aside{
      position:sticky;
      top:24px;
      align-self:start;
    }
    .list{
      display:flex;
      flex-direction:column;
      gap:8px;
    }
    .incident{
      padding:10px;
      border-radius:12px;
      background:linear-gradient(180deg, rgba(255,255,255,0.85), rgba(255,255,255,0.95));
      box-shadow:var(--shadow);
      display:flex;
      gap:10px;
      align-items:flex-start;
    }
    .incident .time{font-size:12px;color:var(--muted)}
    .pill{padding:6px 8px;border-radius:10px;font-weight:700;font-size:12px}

    .tiny{
      font-size:12px;color:var(--muted)
    }

    /* table */
    table{
      width:100%;
      border-collapse:collapse;
      font-size:13px;
    }
    th,td{padding:8px 10px; text-align:left; border-bottom:1px dashed #f0f0f0}
    th{color:var(--muted); font-weight:600; font-size:12px}

    /* responsive */
    @media (max-width:980px){
      main{grid-template-columns:1fr}
      .cards{grid-template-columns: repeat(2,1fr)}
    }
    @media (max-width:640px){
      .cards{grid-template-columns:1fr}
      header{flex-direction:column;align-items:flex-start;gap:12px}
      .controls{width:100%}
    }

    /* subtle animations */
    .fade-in{animation:fade .5s ease both}
    @keyframes fade{from{opacity:0; transform:translateY(6px)} to{opacity:1; transform:none}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo" aria-hidden="true">KG</div>
        <div>
          <h1>Sunflower Kindergarten — Care Dashboard</h1>
          <p class="lead">At-a-glance stats for allergies, behaviors, illnesses, and accidents.</p>
        </div>
      </div>

      <div class="controls" role="region" aria-label="Filters">
        <div class="control">
          <label for="classSelect" class="tiny" style="min-width:48px">Class</label>
          <select id="classSelect" aria-label="Select class">
            <option value="all">All classes</option>
            <option value="sunflower">Sunflower</option>
            <option value="rainbow">Rainbow</option>
            <option value="butterfly">Butterfly</option>
          </select>
        </div>

        <div class="control">
          <label class="tiny" for="from">From</label>
          <input id="from" type="date" />
          <label class="tiny" for="to">To</label>
          <input id="to" type="date" />
        </div>

        <div class="control">
          <button class="primary" id="apply">Apply</button>
        </div>

        <div class="control" title="Export filtered incidents">
          <button id="export" style="background:transparent;border:0;cursor:pointer;font-weight:700;color:var(--muted)">Export CSV</button>
        </div>
      </div>
    </header>

    <main>
      <section class="panels">
        <div class="cards fade-in" role="region" aria-label="Summary cards">
          <div class="card" aria-hidden="false">
            <div class="icon all">🍯</div>
            <div>
              <div class="meta">Allergies</div>
              <div class="value" id="allergyCount">—</div>
              <div class="tiny">Most common: <span id="allergyTop">—</span></div>
            </div>
          </div>

          <div class="card">
            <div class="icon beh">🦋</div>
            <div>
              <div class="meta">Monitored behaviors</div>
              <div class="value" id="behCount">—</div>
              <div class="tiny">Top: <span id="behTop">—</span></div>
            </div>
          </div>

          <div class="card">
            <div class="icon ill">🤒</div>
            <div>
              <div class="meta">Illness reports</div>
              <div class="value" id="illCount">—</div>
              <div class="tiny">Trend: <span id="illTrend">—</span></div>
            </div>
          </div>
        </div>

        <div class="panel fade-in" aria-labelledby="chartsHeading">
          <div class="flex-row">
            <h2 id="chartsHeading" style="font-size:16px;margin:0">Visual summary</h2>
            <div class="tiny">Interactive — hover for details</div>
          </div>

          <div style="display:grid; grid-template-columns: 1fr 1fr; gap:12px; margin-top:12px">
            <div class="panel" style="padding:12px">
              <div class="tiny">Allergies by type</div>
              <div class="chart-wrap"><canvas id="allergyChart" aria-label="Allergies chart"></canvas></div>
            </div>

            <div class="panel" style="padding:12px">
              <div class="tiny">Behavior incidents (last 6 months)</div>
              <div class="chart-wrap"><canvas id="behChart" aria-label="Behavior chart"></canvas></div>
            </div>
          </div>

          <div style="display:grid; grid-template-columns: 1fr 1fr; gap:12px; margin-top:12px">
            <div class="panel" style="padding:12px">
              <div class="tiny">Illness reports (monthly)</div>
              <div class="chart-wrap"><canvas id="illChart" aria-label="Illness chart"></canvas></div>
            </div>

            <div class="panel" style="padding:12px">
              <div class="tiny">Accident severity</div>
              <div class="chart-wrap"><canvas id="accChart" aria-label="Accident chart"></canvas></div>
            </div>
          </div>
        </div>

        <div class="panel fade-in" aria-labelledby="tableHeading">
          <div class="flex-row">
            <h2 id="tableHeading" style="font-size:16px;margin:0">Recent incidents</h2>
            <div class="tiny">Last 30 records</div>
          </div>

          <div style="margin-top:12px; overflow:auto; max-height:300px">
            <table role="table" aria-label="Recent incidents table">
              <thead>
                <tr><th>Date</th><th>Student</th><th>Class</th><th>Type</th><th>Details</th></tr>
              </thead>
              <tbody id="incidentTable">
                <!-- populated by JS -->
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <aside>
        <div class="panel fade-in" style="margin-bottom:12px">
          <div class="flex-row">
            <div>
              <h3 style="margin:0;font-size:16px">Quick insights</h3>
              <div class="tiny">Auto-generated highlights</div>
            </div>
            <div style="text-align:right">
              <div class="tiny">Updated just now</div>
            </div>
          </div>

          <ul style="margin:12px 0 0 0; padding-left:16px; color:var(--muted); font-size:13px">
            <li id="insight1">—</li>
            <li id="insight2">—</li>
            <li id="insight3">—</li>
          </ul>
        </div>

        <div class="panel fade-in">
          <div class="flex-row">
            <h3 style="margin:0;font-size:16px">Notifications</h3>
            <div class="tiny">Admin</div>
          </div>

          <div class="list" style="margin-top:10px" id="notificationList" aria-live="polite">
            <!-- recent notifications -->
          </div>
        </div>
      </aside>
    </main>
  </div>

  <script>
    // Sample dataset: each record = incident event or allergy entry
    const rawData = [
      // allergies
      {id:1, date:'2025-11-01', class:'sunflower', student:'Ava M', category:'allergy', subtype:'Peanut', severity:'moderate', note:'EpiPen on file'},
      {id:2, date:'2025-10-10', class:'rainbow', student:'Ben R', category:'allergy', subtype:'Dairy', severity:'mild'},
      {id:3, date:'2025-09-22', class:'butterfly', student:'Clara J', category:'allergy', subtype:'Peanut', severity:'severe'},
      {id:4, date:'2025-08-03', class:'sunflower', student:'Diego S', category:'allergy', subtype:'Pollen', severity:'mild'},
      // behaviors
      {id:5, date:'2025-11-04', class:'rainbow', student:'Ella P', category:'behavior', subtype:'Aggression', severity:'moderate', note:'2 staff reported'},
      {id:6, date:'2025-10-29', class:'sunflower', student:'Finn K', category:'behavior', subtype:'Withdrawn', severity:'mild'},
      {id:7, date:'2025-11-10', class:'butterfly', student:'Gina A', category:'behavior', subtype:'Tantrum', severity:'mild'},
      {id:8, date:'2025-07-18', class:'sunflower', student:'Hugo B', category:'behavior', subtype:'Aggression', severity:'severe'},
      // illnesses
      {id:9, date:'2025-11-05', class:'rainbow', student:'Ivy L', category:'illness', subtype:'Cold', severity:'mild'},
      {id:10, date:'2025-10-18', class:'butterfly', student:'Jack C', category:'illness', subtype:'Stomach', severity:'moderate'},
      {id:11, date:'2025-11-12', class:'sunflower', student:'Kira M', category:'illness', subtype:'Fever', severity:'mild'},
      {id:12, date:'2025-09-03', class:'rainbow', student:'Liam Q', category:'illness', subtype:'Flu', severity:'severe'},
      // accidents
      {id:13, date:'2025-11-11', class:'butterfly', student:'Maya T', category:'accident', subtype:'Trip', severity:'minor'},
      {id:14, date:'2025-10-31', class:'sunflower', student:'Noah Z', category:'accident', subtype:'Cut', severity:'moderate'},
      {id:15, date:'2025-10-05', class:'rainbow', student:'Olive R', category:'accident', subtype:'Fall', severity:'minor'},
      {id:16, date:'2025-08-13', class:'butterfly', student:'Pablo N', category:'accident', subtype:'Head bump', severity:'major'},
      // more synthetic data to show trends
      {id:17, date:'2025-06-12', class:'sunflower', student:'Quinn V', category:'illness', subtype:'Cold', severity:'mild'},
      {id:18, date:'2025-06-20', class:'rainbow', student:'Rosa H', category:'behavior', subtype:'Tantrum', severity:'mild'},
      {id:19, date:'2025-05-03', class:'butterfly', student:'Sam E', category:'allergy', subtype:'Dairy', severity:'mild'},
      {id:20, date:'2025-04-07', class:'sunflower', student:'Tia G', category:'accident', subtype:'Fall', severity:'minor'},
      // add recent items for table
      {id:21, date:'2025-11-14', class:'sunflower', student:'Uma I', category:'illness', subtype:'Cold', severity:'mild'},
      {id:22, date:'2025-11-15', class:'rainbow', student:'Vik J', category:'behavior', subtype:'Aggression', severity:'moderate'},
      {id:23, date:'2025-11-15', class:'butterfly', student:'Wendy K', category:'accident', subtype:'Trip', severity:'minor'},
      {id:24, date:'2025-11-15', class:'sunflower', student:'Xander L', category:'allergy', subtype:'Peanut', severity:'severe'},
      {id:25, date:'2025-11-16', class:'rainbow', student:'Yara M', category:'illness', subtype:'Fever', severity:'moderate'},
      {id:26, date:'2025-11-16', class:'butterfly', student:'Zane N', category:'behavior', subtype:'Withdrawn', severity:'mild'}
    ];

    // utilities
    function parseDate(s){ return new Date(s + 'T00:00:00'); }
    function formatDate(s){
      const d = parseDate(s);
      return d.toLocaleDateString(undefined, {month:'short', day:'numeric'});
    }

    // controls
    const classSelect = document.getElementById('classSelect');
    const fromInput = document.getElementById('from');
    const toInput = document.getElementById('to');
    const applyBtn = document.getElementById('apply');
    const exportBtn = document.getElementById('export');

    // set default date range: last 6 months
    (function setDefaults(){
      const today = new Date();
      const sixMonthsAgo = new Date(today);
      sixMonthsAgo.setMonth(today.getMonth() - 5);
      fromInput.value = sixMonthsAgo.toISOString().slice(0,10);
      toInput.value = today.toISOString().slice(0,10);
    })();

    // charts
    let allergyChart, behChart, illChart, accChart;

    function aggregateFiltered(){
      // get filters
      const cls = classSelect.value;
      const from = fromInput.value ? parseDate(fromInput.value) : null;
      const to = toInput.value ? parseDate(toInput.value) : null;

      return rawData.filter(r=>{
        if(cls !== 'all' && r.class !== cls) return false;
        if(from && parseDate(r.date) < from) return false;
        if(to && parseDate(r.date) > to) return false;
        return true;
      });
    }

    function computeMetrics(filtered){
      const metrics = {
        allergies: filtered.filter(r=>r.category==='allergy'),
        behaviors: filtered.filter(r=>r.category==='behavior'),
        illnesses: filtered.filter(r=>r.category==='illness'),
        accidents: filtered.filter(r=>r.category==='accident'),
      };

      return metrics;
    }

    function topOf(list, key='subtype', fallback='—'){
      if(!list.length) return fallback;
      const freq = {};
      for(const it of list){ freq[it[key]] = (freq[it[key]]||0) + 1; }
      const entries = Object.entries(freq).sort((a,b)=>b[1]-a[1]);
      return entries.length ? entries[0][0] : fallback;
    }

    function renderSummary(metrics){
      document.getElementById('allergyCount').innerText = metrics.allergies.length;
      document.getElementById('behCount').innerText = metrics.behaviors.length;
      document.getElementById('illCount').innerText = metrics.illnesses.length;

      document.getElementById('allergyTop').innerText = topOf(metrics.allergies);
      document.getElementById('behTop').innerText = topOf(metrics.behaviors);
      // illness trend: compare last two months
      const lastMonth = monthCount(metrics.illnesses, 0);
      const prevMonth = monthCount(metrics.illnesses, 1);
      const trendText = prevMonth===0 ? '—' : (Math.round(((lastMonth-prevMonth)/prevMonth)*100)) + '%';
      document.getElementById('illTrend').innerText = trendText;
    }

    function monthCount(list, monthsAgo=0){
      // counts in the month relative to now
      const now = new Date();
      const target = new Date(now.getFullYear(), now.getMonth()-monthsAgo, 1);
      const month = target.getMonth(), year = target.getFullYear();
      return list.filter(r=>{
        const d = parseDate(r.date);
        return d.getMonth()===month && d.getFullYear()===year;
      }).length;
    }

    function makeCharts(metrics){
      // allergies donut
      const allergyTypes = {};
      metrics.allergies.forEach(a=> allergyTypes[a.subtype] = (allergyTypes[a.subtype]||0)+1);
      const allergyLabels = Object.keys(allergyTypes);
      const allergyValues = Object.values(allergyTypes);

      const allergyCtx = document.getElementById('allergyChart').getContext('2d');
      if(allergyChart) allergyChart.destroy();
      allergyChart = new Chart(allergyCtx, {
        type:'doughnut',
        data:{
          labels: allergyLabels.length? allergyLabels : ['None'],
          datasets:[{
            data: allergyValues.length? allergyValues : [1],
            backgroundColor: ['#ff9ab3','#ffd166','#6dd3b3','#a3b3ff','#ffd6a5'],
            hoverOffset:8,
            borderWidth:0
          }]
        },
        options:{
          plugins:{legend:{display:true,position:'bottom'}, tooltip:{callbacks:{label:ctx=> `${ctx.label}: ${ctx.parsed}`}},},
          maintainAspectRatio:false,
        }
      });

      // behaviors: simple monthly counts for last 6 months by subtype stacked
      const months = [];
      const now = new Date();
      for(let i=5;i>=0;i--){
        const d = new Date(now.getFullYear(), now.getMonth()-i, 1);
        months.push(d.toLocaleString(undefined,{month:'short', year:'numeric'}));
      }
      const behaviorTypes = [...new Set(metrics.behaviors.map(b=>b.subtype))].slice(0,5);
      const behDatasets = behaviorTypes.map((t,idx)=>{
        const data = months.map((m,i)=>{
          const d = new Date();
          d.setMonth(now.getMonth()-5+i);
          const month = d.getMonth(), year = d.getFullYear();
          return metrics.behaviors.filter(b=>{
            const bd = parseDate(b.date);
            return bd.getMonth()===month && bd.getFullYear()===year && b.subtype===t;
          }).length;
        });
        const palette = ['#a3b3ff','#6dd3b3','#ffd166','#ff9ab3','#ffd6a5'];
        return {label:t, data, backgroundColor:palette[idx%palette.length]};
      });
      const behCtx = document.getElementById('behChart').getContext('2d');
      if(behChart) behChart.destroy();
      behChart = new Chart(behCtx, {
        type:'bar',
        data:{labels:months, datasets:behDatasets},
        options:{plugins:{legend:{position:'bottom'}}, maintainAspectRatio:false, responsive:true, scales:{x:{stacked:true}, y:{stacked:true, beginAtZero:true}}}
      });

      // illnesses: line monthly counts for last 8 months
      const illMonths = [];
      const illCounts = [];
      for(let i=7;i>=0;i--){
        const d = new Date(now.getFullYear(), now.getMonth()-i,1);
        illMonths.push(d.toLocaleString(undefined,{month:'short'}));
        illCounts.push(metrics.illnesses.filter(it=>{
          const dd=parseDate(it.date);
          return dd.getMonth()===d.getMonth() && dd.getFullYear()===d.getFullYear();
        }).length);
      }
      const illCtx = document.getElementById('illChart').getContext('2d');
      if(illChart) illChart.destroy();
      illChart = new Chart(illCtx, {
        type:'line',
        data:{labels:illMonths, datasets:[{label:'Illness reports', data:illCounts, borderColor:'#ff7aa2', backgroundColor:'rgba(255,122,162,0.12)', tension:.3, fill:true}]},
        options:{plugins:{legend:{display:false}}, maintainAspectRatio:false}
      });

      // accidents: severity pie
      const sev = {};
      metrics.accidents.forEach(a=> sev[a.severity] = (sev[a.severity]||0)+1);
      const accLabels = Object.keys(sev);
      const accValues = Object.values(sev);
      const accCtx = document.getElementById('accChart').getContext('2d');
      if(accChart) accChart.destroy();
      accChart = new Chart(accCtx, {
        type:'pie',
        data:{labels:accLabels.length?accLabels:['None'], datasets:[{data:accValues.length?accValues:[1], backgroundColor:['#ffd166','#ff9ab3','#a3b3ff']}]},
        options:{plugins:{legend:{position:'bottom'}}, maintainAspectRatio:false}
      });
    }

    function renderTable(filtered){
      const tbody = document.getElementById('incidentTable');
      tbody.innerHTML = '';
      const rows = filtered.slice().sort((a,b)=> new Date(b.date)-new Date(a.date)).slice(0,30);
      for(const r of rows){
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${formatDate(r.date)}</td>
                        <td>${r.student}</td>
                        <td style="text-transform:capitalize">${r.class}</td>
                        <td style="text-transform:capitalize">${r.category} ${r.subtype?(' — '+r.subtype):''}</td>
                        <td>${r.note? r.note : (r.severity?('Severity: '+r.severity):'')}</td>`;
        tbody.appendChild(tr);
      }
    }

    function renderSidebar(metrics, filtered){
      // quick insights
      const insight1 = document.getElementById('insight1');
      const insight2 = document.getElementById('insight2');
      const insight3 = document.getElementById('insight3');

      insight1.innerText = metrics.illnesses.length > 5 ? `High illness reports: ${metrics.illnesses.length} events` : `Illness reports: ${metrics.illnesses.length}`;
      insight2.innerText = metrics.accidents.length ? `Accidents this range: ${metrics.accidents.length}` : `No accidents reported in range`;
      insight3.innerText = metrics.allergies.length ? `Allergy cases logged: ${metrics.allergies.length}` : `No allergy updates`;

      // notifications (recent serious items)
      const noteList = document.getElementById('notificationList');
      noteList.innerHTML = '';
      const serious = filtered.filter(r=> r.severity && (r.severity==='severe' || r.severity==='major'));
      if(serious.length===0){
        const d = document.createElement('div'); d.className='incident'; d.innerHTML = `<div style="font-weight:700">All clear</div><div class="time">No critical incidents</div>`;
        noteList.appendChild(d);
      } else {
        serious.slice(0,6).forEach(s=>{
          const el = document.createElement('div');
          el.className='incident';
          el.innerHTML = `<div style="font-size:18px">${s.category==='allergy'?'🥜': s.category==='illness'?'🤒': s.category==='accident'?'⚕️':'📝'}</div>
                          <div style="flex:1">
                            <div style="font-weight:700">${s.student} — ${s.subtype}</div>
                            <div class="time">${formatDate(s.date)} · ${s.class}</div>
                          </div>
                          <div><div class="pill" style="background:#ffefef;color:#a12b2b">${s.severity}</div></div>`;
          noteList.appendChild(el);
        });
      }
    }

    function exportCSV(filtered){
      const rows = filtered.slice().sort((a,b)=> new Date(a.date)-new Date(b.date));
      const headers = ['id','date','class','student','category','subtype','severity','note'];
      const csv = [headers.join(',')].concat(rows.map(r=>{
        return headers.map(h=> {
          const v = r[h] || '';
          // escape quotes
          return `"${String(v).replace(/"/g,'""')}"`;
        }).join(',');
      })).join('\n');

      const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `incidents-${new Date().toISOString().slice(0,10)}.csv`;
      a.click();
      URL.revokeObjectURL(url);
    }

    function refreshAll(){
      const filtered = aggregateFiltered();
      const metrics = computeMetrics(filtered);
      renderSummary(metrics);
      makeCharts(metrics);
      renderTable(filtered);
      renderSidebar(metrics, filtered);
    }

    // initial render
    refreshAll();

    // interactions
    applyBtn.addEventListener('click', ()=> {
      refreshAll();
    });

    exportBtn.addEventListener('click', ()=> {
      const filtered = aggregateFiltered();
      exportCSV(filtered);
    });

    // keyboard accessibility: Enter on selects triggers apply
    [classSelect, fromInput, toInput].forEach(el=>{
      el.addEventListener('keydown', (e)=>{ if(e.key==='Enter') refreshAll(); });
    });

    // small live update to show dynamic feel: when date changes, auto-refresh after pause
    let timer;
    [fromInput,toInput].forEach(i=>{
      i.addEventListener('input', ()=> {
        clearTimeout(timer);
        timer = setTimeout(refreshAll, 700);
      });
    });

    // Optional: show a tooltip-like pointer when hovering cards
    document.querySelectorAll('.card').forEach(c=>{
      c.addEventListener('mouseenter', ()=> c.style.transform='translateY(-6px)');
      c.addEventListener('mouseleave', ()=> c.style.transform='none');
    });

    // Accessibility: announce changes to summary counts
    const liveSummary = new MutationObserver(()=> {
      // could be extended to voice, for now it's a console hint
      console.debug('Summary updated');
    });
    liveSummary.observe(document.getElementById('allergyCount'), {childList:true, subtree:true});

  </script>
</body>
</html>
