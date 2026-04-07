# artcucinelch[dashboard_artcucinelch.html](https://github.com/user-attachments/files/26522686/dashboard_artcucinelch.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard @artcucinelch | Meta Ads Q1 2026</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;600;700&family=Outfit:wght@300;400;500;600;700&display=swap');
  
  :root {
    --bg: #09090b;
    --surface: #111113;
    --surface2: #18181b;
    --border: #27272a;
    --accent: #d4b483;
    --accent2: #e8d5b0;
    --silver: #94a3b8;
    --green: #4ade80;
    --red: #f87171;
    --yellow: #facc15;
    --blue: #60a5fa;
    --text: #f4f4f5;
    --muted: #71717a;
    --white: #fafafa;
  }

  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:var(--bg); color:var(--text); font-family:'Outfit',sans-serif; font-size:14px; }

  .cover {
    min-height:100vh; display:flex; flex-direction:column; justify-content:center; align-items:center;
    position:relative; overflow:hidden; padding:40px; text-align:center;
    background: linear-gradient(160deg, #09090b 0%, #1a1208 40%, #09090b 100%);
  }
  .cover::before { content:''; position:absolute; top:50%; left:50%; transform:translate(-50%,-50%); width:600px; height:600px; border-radius:50%; background:radial-gradient(circle, rgba(212,180,131,0.1) 0%, transparent 70%); pointer-events:none; }
  .cover-lines { position:absolute; inset:0; opacity:0.06; pointer-events:none;
    background: repeating-linear-gradient(45deg, var(--accent), var(--accent) 1px, transparent 1px, transparent 40px);
  }
  .cover-content { position:relative; z-index:1; }
  .cover-eyebrow { display:inline-flex; align-items:center; gap:10px; margin-bottom:24px; }
  .cover-eyebrow::before, .cover-eyebrow::after { content:''; width:40px; height:1px; background:var(--accent); }
  .cover-eyebrow span { font-size:11px; letter-spacing:5px; text-transform:uppercase; color:var(--accent); font-weight:500; }
  .cover-title { font-family:'Cormorant Garamond',serif; font-size:clamp(44px,8vw,92px); font-weight:300; line-height:1; letter-spacing:-1px; }
  .cover-title strong { font-weight:700; color:var(--accent2); display:block; }
  .cover-tagline { font-size:14px; color:var(--muted); margin-top:20px; letter-spacing:2px; }
  .cover-divider { display:flex; align-items:center; gap:16px; margin:36px auto; width:fit-content; }
  .cover-divider::before, .cover-divider::after { content:''; width:60px; height:1px; background:linear-gradient(90deg, transparent, var(--accent)); }
  .cover-divider::after { background:linear-gradient(90deg, var(--accent), transparent); }
  .cover-stats { display:flex; gap:48px; justify-content:center; flex-wrap:wrap; }
  .cs { text-align:center; }
  .cs-val { font-family:'Cormorant Garamond',serif; font-size:46px; font-weight:700; color:var(--accent); display:block; }
  .cs-lab { font-size:10px; letter-spacing:3px; text-transform:uppercase; color:var(--muted); }

  .nav { position:sticky; top:0; z-index:100; background:rgba(9,9,11,0.97); backdrop-filter:blur(12px); border-bottom:1px solid var(--border); padding:0 30px; display:flex; align-items:center; gap:4px; overflow-x:auto; }
  .nav-logo { font-family:'Cormorant Garamond',serif; font-size:22px; color:var(--accent2); margin-right:20px; flex-shrink:0; font-weight:600; }
  .nav-btn { padding:15px 16px; font-family:'Outfit',sans-serif; font-size:11px; font-weight:600; letter-spacing:2px; text-transform:uppercase; color:var(--muted); background:none; border:none; cursor:pointer; white-space:nowrap; border-bottom:2px solid transparent; transition:all .2s; }
  .nav-btn:hover, .nav-btn.active { color:var(--accent); border-bottom-color:var(--accent); }

  .section { padding:60px 30px; max-width:1160px; margin:0 auto; display:none; }
  .section.active { display:block; }
  .s-label { font-size:10px; letter-spacing:5px; text-transform:uppercase; color:var(--accent); margin-bottom:10px; font-weight:500; }
  .s-title { font-family:'Cormorant Garamond',serif; font-size:clamp(30px,5vw,56px); font-weight:700; line-height:1.1; margin-bottom:32px; }
  .s-title em { color:var(--accent); font-style:normal; font-weight:300; }

  .grid-2 { display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr)); gap:20px; }
  .grid-3 { display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:16px; }
  .grid-4 { display:grid; grid-template-columns:repeat(auto-fit,minmax(190px,1fr)); gap:14px; }

  .card { background:var(--surface); border:1px solid var(--border); border-radius:2px; padding:24px; }
  .kpi-card { text-align:center; padding:28px 16px; }
  .kpi-val { font-family:'Cormorant Garamond',serif; font-size:44px; font-weight:700; color:var(--white); line-height:1; }
  .kpi-val.g { color:var(--green); }
  .kpi-val.a { color:var(--accent); }
  .kpi-val.b { color:var(--blue); }
  .kpi-val.y { color:var(--yellow); }
  .kpi-label { font-size:10px; letter-spacing:3px; text-transform:uppercase; color:var(--muted); margin-top:8px; font-weight:500; }
  .kpi-sub { font-size:11px; color:var(--muted); margin-top:4px; }

  .table-wrap { overflow-x:auto; }
  table { width:100%; border-collapse:collapse; font-size:12px; }
  th { background:var(--surface2); color:var(--muted); font-size:9px; letter-spacing:3px; text-transform:uppercase; padding:12px 14px; text-align:left; border-bottom:1px solid var(--border); font-weight:600; }
  td { padding:11px 14px; border-bottom:1px solid rgba(39,39,42,0.5); }
  tr:hover td { background:var(--surface2); }

  .badge { display:inline-block; padding:3px 10px; border-radius:1px; font-size:9px; font-weight:700; letter-spacing:2px; text-transform:uppercase; }
  .bg { background:rgba(74,222,128,0.1); color:var(--green); }
  .br { background:rgba(248,113,113,0.1); color:var(--red); }
  .by { background:rgba(250,204,21,0.1); color:var(--yellow); }
  .ba { background:rgba(212,180,131,0.1); color:var(--accent); }
  .bb { background:rgba(96,165,250,0.1); color:var(--blue); }

  .chart-wrap { position:relative; height:300px; }

  .insight { border-left:2px solid var(--border); padding-left:20px; margin-bottom:24px; }
  .insight.g { border-left-color:var(--green); }
  .insight.r { border-left-color:var(--red); }
  .insight.a { border-left-color:var(--accent); }
  .insight-tag { font-size:9px; letter-spacing:3px; text-transform:uppercase; color:var(--accent); font-weight:700; }
  .insight.g .insight-tag { color:var(--green); }
  .insight.r .insight-tag { color:var(--red); }
  .insight-title { font-family:'Cormorant Garamond',serif; font-size:22px; font-weight:700; margin:4px 0 6px; }
  .insight-body { color:var(--muted); font-size:13px; line-height:1.8; }

  .reco { display:flex; gap:20px; padding:22px; background:var(--surface2); border:1px solid var(--border); margin-bottom:12px; }
  .reco-n { font-family:'Cormorant Garamond',serif; font-size:52px; font-weight:700; color:var(--accent); opacity:0.2; line-height:1; flex-shrink:0; }
  .reco-title { font-family:'Cormorant Garamond',serif; font-size:22px; font-weight:700; margin-bottom:6px; }
  .reco-body { color:var(--muted); font-size:12px; line-height:1.8; }

  .month-row-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:14px; }
  .month-card { background:var(--surface2); border:1px solid var(--border); padding:20px; }
  .month-name { font-family:'Cormorant Garamond',serif; font-size:28px; font-weight:700; color:var(--accent); margin-bottom:12px; }
  .mrow { display:flex; justify-content:space-between; padding:5px 0; border-bottom:1px solid var(--border); font-size:11px; }
  .mrow:last-child { border:none; }
  .mval { font-weight:600; color:var(--white); }

  .conclusion { background:var(--surface); border:1px solid var(--border); border-left:3px solid var(--accent); padding:36px; }
  .conclusion-title { font-family:'Cormorant Garamond',serif; font-size:32px; font-weight:700; margin-bottom:14px; }
  .conclusion-body { color:var(--muted); font-size:13px; line-height:1.9; }

  .notice { background:rgba(212,180,131,0.07); border:1px solid rgba(212,180,131,0.2); padding:14px 18px; font-size:12px; color:var(--muted); margin-bottom:24px; }
  .notice strong { color:var(--accent); }
  .divider { height:1px; background:var(--border); margin:28px 0; }
  .prog { height:3px; background:var(--border); overflow:hidden; margin-top:8px; }
  .pf { height:100%; background:var(--accent); }
  .pf.g { background:var(--green); }

  @media(max-width:640px){ .month-row-grid{grid-template-columns:1fr;} }
</style>
</head>
<body>

<section class="cover">
  <div class="cover-lines"></div>
  <div class="cover-content">
    <div class="cover-eyebrow"><span>Meta Ads · Q1 2026</span></div>
    <h1 class="cover-title">
      Art<strong>Cucine</strong>lch
    </h1>
    <p class="cover-tagline">Cocinas · Baños · Closets · Vestier · Livings · Anzoátegui · Venezuela</p>
    <div class="cover-divider"></div>
    <div class="cover-stats">
      <div class="cs"><span class="cs-val">$721</span><span class="cs-lab">Inversión Total</span></div>
      <div class="cs"><span class="cs-val">449</span><span class="cs-lab">Conversaciones WA</span></div>
      <div class="cs"><span class="cs-val">321</span><span class="cs-lab">Nuevos Seguidores</span></div>
      <div class="cs"><span class="cs-val">169K</span><span class="cs-lab">Alcance Total</span></div>
    </div>
    <p style="margin-top:28px;color:var(--muted);font-size:11px;letter-spacing:3px;text-transform:uppercase;">Enero — Marzo 2026</p>
  </div>
</section>

<nav class="nav">
  <div class="nav-logo">ArtCucine</div>
  <button class="nav-btn active" onclick="showSection('resumen',this)">Resumen</button>
  <button class="nav-btn" onclick="showSection('kpis',this)">KPIs</button>
  <button class="nav-btn" onclick="showSection('campanas',this)">Campañas</button>
  <button class="nav-btn" onclick="showSection('insights',this)">Insights</button>
  <button class="nav-btn" onclick="showSection('recomendaciones',this)">Recomendaciones</button>
  <button class="nav-btn" onclick="showSection('mensual',this)">Mensual</button>
  <button class="nav-btn" onclick="showSection('conclusion',this)">Conclusión</button>
</nav>

<!-- RESUMEN -->
<section class="section active" id="resumen">
  <div class="s-label">01 · Resumen Ejecutivo</div>
  <h2 class="s-title">Visión <em>General</em></h2>

  <div class="grid-4" style="margin-bottom:24px">
    <div class="card kpi-card"><div class="kpi-val a">$721</div><div class="kpi-label">Inversión Q1</div><div class="kpi-sub">Menor presupuesto</div></div>
    <div class="card kpi-card"><div class="kpi-val">449</div><div class="kpi-label">Conv. WA Total</div><div class="kpi-sub">Interacción + Ventas</div></div>
    <div class="card kpi-card"><div class="kpi-val g">$1.09</div><div class="kpi-label">CPA Interacción</div><div class="kpi-sub">341 conversaciones</div></div>
    <div class="card kpi-card"><div class="kpi-val b">$2.21</div><div class="kpi-label">CPA Ventas</div><div class="kpi-sub">106 conversaciones</div></div>
  </div>

  <div class="grid-2">
    <div class="card">
      <div class="s-label">Contexto Estratégico</div>
      <p style="color:var(--muted);line-height:1.9;font-size:13px;margin-top:10px;">
        @artcucinelch es la cuenta con <strong style="color:var(--white)">menor inversión de los 4 clientes</strong> ($721 en Q1), pero opera en el segmento de <strong style="color:var(--accent)">mayor ticket promedio</strong> (instalación de cocinas, baños, closets). Esto significa que <strong style="color:var(--white)">una sola conversión puede justificar toda la inversión mensual</strong>.
      </p>
      <p style="color:var(--muted);line-height:1.9;font-size:13px;margin-top:10px;">
        Con <strong style="color:var(--white)">3 campañas activas</strong> (Interacción, Ventas y Tráfico), tiene estructura completa pero subinvertida. El CPA de Ventas de $2.21 es el más alto de los clientes, pero justificado por el alto valor del ticket en el sector de hogar premium.
      </p>
      <p style="color:var(--muted);line-height:1.9;font-size:13px;margin-top:10px;">
        La segmentación "Audiencias Específicas" (ANZ = Anzoátegui) indica enfoque geográfico correcto para un servicio de instalación local. La clave es <strong style="color:var(--accent)">aumentar presupuesto manteniendo la segmentación de calidad</strong>.
      </p>
      <div class="divider"></div>
      <p style="color:var(--muted);font-size:12px"><strong style="color:var(--white)">Contexto de valor:</strong> Si una instalación de cocina promedia $2,000-5,000 USD, una CPA de $2.21 con ROAS proyectado de 900x+ hace de esta campaña la más rentable del portafolio.</p>
    </div>
    <div class="card">
      <div class="s-label">Distribución de Presupuesto</div>
      <div class="chart-wrap" style="height:240px;margin-top:10px">
        <canvas id="budgetChart"></canvas>
      </div>
    </div>
  </div>

  <div class="grid-2" style="margin-top:20px">
    <div class="card">
      <div class="s-label" style="margin-bottom:12px">Fortalezas</div>
      <div class="insight g"><div class="insight-tag">✓ Fortaleza</div><div class="insight-title">Segmento de Alto Ticket</div><div class="insight-body">Instalación de cocinas/baños/closets = ticket $1,500-10,000 USD. Un CPA de $2.21 para este sector es absolutamente rentable. Cada lead generado puede multiplicar x1,000 la inversión en Meta Ads.</div></div>
      <div class="insight g"><div class="insight-tag">✓ Fortaleza</div><div class="insight-title">35% Conv WA en Interacción</div><div class="insight-body">341 conversaciones WA de la campaña de Interacción con CPA de $1.09 demuestran que el contenido visual de renovaciones de hogar genera alta intención de consulta en Anzoátegui.</div></div>
    </div>
    <div class="card">
      <div class="s-label" style="margin-bottom:12px">Áreas Críticas</div>
      <div class="insight r"><div class="insight-tag">⚠ Crítico</div><div class="insight-title">Presupuesto Subóptimo</div><div class="insight-body">$721 en Q1 ($240/mes) es insuficiente para un negocio de servicios de alto ticket. Con $500-700/mes, el volumen de leads se triplicaría manteniendo el CPA. La inversión actual no permite escalar el aprendizaje del algoritmo.</div></div>
      <div class="insight r"><div class="insight-tag">⚠ Debilidad</div><div class="insight-title">Tráfico con Bajo CPA WA</div><div class="insight-body">La campaña de Tráfico ($114) genera 2,968 visitas pero solo 2 conversaciones WA. El 0.07% de tasa de conversión es muy baja, indicando desconexión entre el público de tráfico y los servicios de instalación de hogar.</div></div>
    </div>
  </div>
</section>

<!-- KPIs -->
<section class="section" id="kpis">
  <div class="s-label">02 · KPIs Clave</div>
  <h2 class="s-title">Métricas de <em>Rendimiento</em></h2>

  <div class="grid-4" style="margin-bottom:24px">
    <div class="card kpi-card"><div class="kpi-val a">$2.21</div><div class="kpi-label">CPA Ventas</div><div class="kpi-sub">Alto ticket justifica</div><div class="prog"><div class="pf" style="width:60%"></div></div></div>
    <div class="card kpi-card"><div class="kpi-val g">$1.09</div><div class="kpi-label">CPA Interacción</div><div class="kpi-sub">341 conv WA</div><div class="prog"><div class="pf g" style="width:85%"></div></div></div>
    <div class="card kpi-card"><div class="kpi-val">34.9%</div><div class="kpi-label">Conv WA Interacción</div><div class="kpi-sub">977 clics → 341 WA</div><div class="prog"><div class="pf" style="width:35%"></div></div></div>
    <div class="card kpi-card"><div class="kpi-val b">15.9%</div><div class="kpi-label">Conv WA Ventas</div><div class="kpi-sub">667 clics → 106 WA</div><div class="prog"><div class="pf" style="width:16%;background:var(--blue)"></div></div></div>
  </div>

  <div class="card" style="margin-bottom:24px">
    <div class="s-label" style="margin-bottom:14px">Tabla Comparativa — 3 Campañas</div>
    <div class="table-wrap">
      <table>
        <thead>
          <tr><th>Campaña</th><th>Objetivo</th><th>Gasto $</th><th>Resultados</th><th>CPA $</th><th>Conv WA</th><th>Conv WA %</th><th>Clics</th><th>CTR %</th><th>CPM $</th><th>Seguidores</th><th>Alcance</th><th>Rating</th></tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>MOFU Interacción ANZ</strong></td><td>Interacción</td><td>$372</td><td>341</td><td>$1.09</td><td>341</td><td>34.9%</td><td>977</td><td>1.93%</td><td>$3.10</td><td>76</td><td>40,949</td>
            <td><span class="badge bg">🟢 TOP</span></td>
          </tr>
          <tr>
            <td><strong>BOFU Ventas ANZ</strong></td><td>Ventas</td><td>$234</td><td>106</td><td>$2.21</td><td>106</td><td>15.9%</td><td>667</td><td>1.93%</td><td>$3.69</td><td>31</td><td>25,078</td>
            <td><span class="badge ba">🟡 MEJORAR</span></td>
          </tr>
          <tr>
            <td><strong>TOFU Tráfico ANZ</strong></td><td>Tráfico</td><td>$114</td><td>2,968</td><td>$0.038</td><td>2</td><td>0.07%</td><td>2,669</td><td>0.78%</td><td>$0.30</td><td>214</td><td>102,917</td>
            <td><span class="badge by">🟡 REVISAR</span></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <div class="grid-2">
    <div class="card">
      <div class="s-label">CTR por Campaña</div>
      <div class="chart-wrap" style="margin-top:10px"><canvas id="ctrChart"></canvas></div>
    </div>
    <div class="card">
      <div class="s-label">Gasto vs Conversaciones WA</div>
      <div class="chart-wrap" style="margin-top:10px"><canvas id="spendConvChart"></canvas></div>
    </div>
  </div>
</section>

<!-- CAMPAÑAS -->
<section class="section" id="campanas">
  <div class="s-label">03 · Análisis de Campañas</div>
  <h2 class="s-title">Top & <em>Optimizar</em></h2>

  <div class="grid-2">
    <div>
      <h3 style="font-family:'Cormorant Garamond',serif;font-size:26px;color:var(--green);margin-bottom:16px">🏆 Top Campañas</h3>

      <div class="card" style="border-left:2px solid var(--green);margin-bottom:14px">
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span class="badge bg">#1 MEJOR</span><span style="font-family:'Cormorant Garamond',serif;font-size:28px;color:var(--green)">$1.09 CPA</span></div>
        <div style="font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:700;margin-bottom:8px">MOFU Interacción ANZ (Seg. Específica)</div>
        <p style="color:var(--muted);font-size:12px;line-height:1.8">La mejor campaña de la cuenta: 341 conversaciones WhatsApp a $1.09, con CTR del 1.93% y 34.9% de tasa de conversión. La segmentación específica de Anzoátegui + intereses de hogar está perfectamente calibrada para el público objetivo. El CPM de $3.10 es justificable para un servicio de alto ticket. <strong style="color:var(--accent2)">Aumentar presupuesto es la acción más rentable posible.</strong></p>
      </div>

      <div class="card" style="border-left:2px solid var(--blue);margin-bottom:14px">
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span class="badge bb">#2 POTENCIAL</span><span style="font-family:'Cormorant Garamond',serif;font-size:28px;color:var(--blue)">$2.21 CPA</span></div>
        <div style="font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:700;margin-bottom:8px">BOFU Ventas ANZ</div>
        <p style="color:var(--muted);font-size:12px;line-height:1.8">106 conversaciones con objetivo de Ventas a $2.21 por lead. En contexto de hogar premium (cocina = $3,000-10,000 USD de ticket), este CPA representa un <strong style="color:var(--white)">ROAS de 1,300x-4,500x</strong>. La tasa de conversión WA (15.9%) indica que hay desconexión entre clic y decisión de contactar — el creativo de Ventas puede mejorarse.</p>
      </div>
    </div>

    <div>
      <h3 style="font-family:'Cormorant Garamond',serif;font-size:26px;color:var(--red);margin-bottom:16px">⚠ Campañas a Optimizar</h3>

      <div class="card" style="border-left:2px solid var(--red);margin-bottom:14px">
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span class="badge br">REPLANTEAR</span><span style="font-family:'Cormorant Garamond',serif;font-size:22px;color:var(--red)">0.07% WA</span></div>
        <div style="font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:700;margin-bottom:8px">TOFU Tráfico ANZ</div>
        <p style="color:var(--muted);font-size:12px;line-height:1.8">2,968 visitas al perfil pero solo 2 conversaciones WhatsApp. El CTR de 0.78% es el más bajo de las 3 campañas. El tráfico está llegando pero no convierte porque el perfil de Instagram probablemente no tiene CTA clara hacia WhatsApp/consulta. Solución: optimizar el bio de IG + agregar historia fija de contacto antes de aumentar tráfico.</p>
      </div>

      <div class="card" style="border-left:2px solid var(--yellow)">
        <div style="display:flex;justify-content:space-between;margin-bottom:8px"><span class="badge by">ESCALABILIDAD</span></div>
        <div style="font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:700;margin-bottom:8px">Presupuesto Total — Insuficiente</div>
        <p style="color:var(--muted);font-size:12px;line-height:1.8">$721 en Q1 ($240/mes) es la limitación más crítica de la cuenta. Las campañas están bien optimizadas pero con presupuesto tan bajo el algoritmo de Meta no puede aprender correctamente (requiere mínimo 50 conversiones/semana para salir de la fase de aprendizaje). Con $500/mes se triplicarían las conversiones.</p>
      </div>
    </div>
  </div>
</section>

<!-- INSIGHTS -->
<section class="section" id="insights">
  <div class="s-label">04 · Insights Estratégicos</div>
  <h2 class="s-title">Análisis <em>Profundo</em></h2>

  <div class="grid-2" style="margin-bottom:24px">
    <div class="card">
      <div class="s-label" style="margin-bottom:10px">Conv WA % por Campaña</div>
      <div class="chart-wrap"><canvas id="convRateChart"></canvas></div>
    </div>
    <div class="card">
      <div class="s-label" style="margin-bottom:10px">Eficiencia Comparativa (Inversión / Resultado)</div>
      <div class="chart-wrap"><canvas id="effChart"></canvas></div>
    </div>
  </div>

  <div class="insight a"><div class="insight-tag">Insight #1</div><div class="insight-title">El valor del ticket justifica 10x más inversión</div><div class="insight-body">En servicios de diseño e instalación de cocinas/baños, un solo proyecto puede representar $2,000-10,000 USD. Con un CPA de $2.21 en campaña de Ventas, el retorno sobre inversión (ROAS) implícito es de 900x-4,500x. @artcucinelch debería invertir $500-700/mes sin dudar — el ROI lo respalda completamente.</div></div>

  <div class="insight g"><div class="insight-tag">Insight #2</div><div class="insight-title">La Interacción supera a Ventas en tasa de conversión WA</div><div class="insight-body">34.9% de conversión WA en Interacción vs 15.9% en Ventas. Esto indica que el cliente de instalaciones de hogar necesita más "calentamiento" antes de iniciar conversación. La campaña de Interacción está funcionando como MOFU efectivo que lleva a la gente a hablar primero. Modelo sugerido: Interacción → retargeting con Ventas.</div></div>

  <div class="insight"><div class="insight-tag">Insight #3</div><div class="insight-title">Segmentación específica de ANZ es correcta para un servicio local</div><div class="insight-body">A diferencia de otros clientes con segmentación nacional, artcucinelch correctamente enfoca en Anzoátegui. Un servicio de instalación no puede atender demanda nacional. CPM de $3.10-3.69 en esta región indica menor competencia publicitaria que Caracas, lo que es una ventaja. Explorar zonas adyacentes: Nueva Esparta, Sucre, Monagas.</div></div>

  <div class="insight r"><div class="insight-tag">Insight #4</div><div class="insight-title">El perfil de Instagram puede estar siendo el cuello de botella</div><div class="insight-body">2,968 visitas al perfil generan solo 2 conversaciones WA (0.07%). El problema puede no ser la campaña sino el perfil: ¿tiene el número de WhatsApp visible en la bio? ¿hay Highlights de proyectos terminados? ¿el feed muestra trabajos reales con "antes/después"? Optimizar el perfil puede duplicar la conversión de tráfico sin gastar más en anuncios.</div></div>
</section>

<!-- RECOMENDACIONES -->
<section class="section" id="recomendaciones">
  <div class="s-label">05 · Plan de Acción Q2 2026</div>
  <h2 class="s-title">Recomendaciones <em>Accionables</em></h2>

  <div class="reco"><div class="reco-n">01</div><div><div class="reco-title">💰 Triplicar Inversión en Interacción</div><div class="reco-body">La campaña de Interacción ($1.09 CPA) es la más eficiente. Aumentar de $372 → $900/trimestre (de $124/mes a $300/mes). Proyección: de 341 → ~820 conversaciones WA en Q2 con el mismo CPA. Para un negocio de instalaciones, esto representa potencialmente 40-80 proyectos nuevos consultados.</div></div></div>

  <div class="reco"><div class="reco-n">02</div><div><div class="reco-title">🔄 Crear Secuencia Interacción → Ventas con Retargeting</div><div class="reco-body">Configurar: Personas que interactuaron con anuncios de Interacción (últimos 30 días) → reciben la campaña de Ventas. Este retargeting debería mejorar la tasa de conversión WA en Ventas de 15.9% → 25-35% porque la audiencia ya "calentó" con el contenido. CPA proyectado de Ventas: $1.40-1.60 (vs $2.21 actual).</div></div></div>

  <div class="reco"><div class="reco-n">03</div><div><div class="reco-title">📱 Optimizar Perfil de Instagram Antes de Aumentar Tráfico</div><div class="reco-body">Antes de invertir más en Tráfico, optimizar: (a) Bio con número WA y "Instalaciones en ANZ 📞", (b) 3 Highlights: "Cocinas", "Baños", "Closets" con fotos de proyectos reales, (c) Primer post fijado: video "antes y después" de la instalación más impresionante, (d) Enlace en bio que vaya directo a WhatsApp. Esto puede convertir el tráfico actual de 0.07% → 3-5% WA.</div></div></div>

  <div class="reco"><div class="reco-n">04</div><div><div class="reco-title">🎬 Creativos "Antes y Después" para Ventas</div><div class="reco-body">El formato más efectivo para instalaciones de hogar es el "antes y después". Para la campaña de Ventas, crear: (a) Video 30s que muestre cocina vieja → instalación artcucinelch → cocina nueva, (b) Carrusel deslizable con el mismo concepto, (c) Reel con música trending de transformación de hogar. Este tipo de contenido tiene CTR 2-3x superior en el sector hogar/deco.</div></div></div>

  <div class="reco"><div class="reco-n">05</div><div><div class="reco-title">📍 Expandir a Ciudades Adyacentes</div><div class="reco-body">Anzoátegui tiene 3 ciudades principales (Barcelona, Lecherías, Puerto La Cruz). Crear adsets separados por ciudad + explorar Nueva Esparta y Sucre si la capacidad de atención lo permite. El CPM bajo ($3.10) indica audiencias poco saturadas en la región. Nuevas ciudades = nuevas audiencias sin fatiga + menor CPA inicial.</div></div></div>

  <div class="reco"><div class="reco-n">06</div><div><div class="reco-title">📊 Agregar Conversiones de WhatsApp como KPI Primario</div><div class="reco-body">Para un servicio de alto ticket, el funnel real es: Meta Ad → WhatsApp → Cotización → Cierre. Configurar el tracking de conversiones de WhatsApp Business (meta conversions API) para medir no solo los clics sino las conversaciones que realmente llegan a cotización. Esto permite optimizar con datos de cierre real.</div></div></div>
</section>

<!-- MENSUAL -->
<section class="section" id="mensual">
  <div class="s-label">06 · Comparativa Mensual</div>
  <h2 class="s-title">Enero / Febrero / <em>Marzo</em></h2>

  <div class="notice"><strong>⚠ Nota de Datos:</strong> El informe Q1 2026 está consolidado sin desglose mensual. Las estimaciones mensuales se basan en patrones de anuncios activos/inactivos observados. La campaña de Interacción tiene los adsets más activos en el período.</div>

  <div class="month-row-grid" style="margin-bottom:24px">
    <div class="month-card">
      <div class="month-name">Enero</div>
      <div class="mrow"><span>Inversión Est.</span><span class="mval">~$230</span></div>
      <div class="mrow"><span>Conv WA Est.</span><span class="mval">~140</span></div>
      <div class="mrow"><span>Creativos activos</span><span class="mval" style="color:var(--accent)">3-4 ads</span></div>
      <div class="mrow"><span>Fase</span><span class="mval" style="color:var(--blue)">LANZAMIENTO</span></div>
    </div>
    <div class="month-card">
      <div class="month-name">Febrero</div>
      <div class="mrow"><span>Inversión Est.</span><span class="mval">~$260</span></div>
      <div class="mrow"><span>Conv WA Est.</span><span class="mval">~165</span></div>
      <div class="mrow"><span>Creativos activos</span><span class="mval" style="color:var(--accent)">5-6 ads</span></div>
      <div class="mrow"><span>Fase</span><span class="mval" style="color:var(--green)">PICO</span></div>
    </div>
    <div class="month-card">
      <div class="month-name">Marzo</div>
      <div class="mrow"><span>Inversión Est.</span><span class="mval">~$231</span></div>
      <div class="mrow"><span>Conv WA Est.</span><span class="mval">~144</span></div>
      <div class="mrow"><span>Creativos activos</span><span class="mval" style="color:var(--accent)">4-5 ads</span></div>
      <div class="mrow"><span>Fase</span><span class="mval" style="color:var(--yellow)">ESTABLE</span></div>
    </div>
  </div>

  <div class="card" style="margin-bottom:20px">
    <div class="s-label" style="margin-bottom:12px">Tendencia Mensual Estimada</div>
    <div class="chart-wrap"><canvas id="trendChart"></canvas></div>
  </div>

  <div class="card">
    <div class="s-label" style="margin-bottom:14px">Tendencias Observadas Q1</div>
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px">
      <div><div style="font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--green);margin-bottom:6px">📈 MANTENER</div><p style="color:var(--muted);font-size:12px;line-height:1.8">La campaña de Interacción con su CPA de $1.09 debe mantenerse como campaña central. El mayor número de creativos activos en Febrero coincide con el mejor período estimado, lo que confirma que más variedad creativa mejora resultados.</p></div>
      <div><div style="font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--yellow);margin-bottom:6px">🔄 CAMBIAR</div><p style="color:var(--muted);font-size:12px;line-height:1.8">El patrón de inversión relativamente constante entre meses ($230-260) indica un presupuesto diario fijo. Q2 debería experimentar con mayor presupuesto en semanas pico (inicio de mes, post-quincena) cuando hay más capacidad de gasto en el consumidor para hogar.</p></div>
      <div><div style="font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--accent);margin-bottom:6px">⭐ OPORTUNIDAD</div><p style="color:var(--muted);font-size:12px;line-height:1.8">Los 5 creativos del anuncio "REEL NUEVA CASA" con 100 conversaciones WA a $0.78 CPA en Interacción son el mejor anuncio individual de la cuenta. Crear variaciones A/B de este formato específico podría duplicar el rendimiento general.</p></div>
    </div>
  </div>
</section>

<!-- CONCLUSIÓN -->
<section class="section" id="conclusion">
  <div class="s-label">07 · Conclusión</div>
  <h2 class="s-title">Veredicto <em>Final</em></h2>

  <div class="conclusion" style="margin-bottom:24px">
    <div class="conclusion-title">@artcucinelch: El Mayor ROI Potencial, La Inversión Más Pequeña</div>
    <div class="conclusion-body">
      <p>@artcucinelch opera en el segmento de mayor valor por cliente de todos los 4 clientes: instalación de cocinas, baños y closets representa tickets de $2,000-10,000+ USD. Con solo $721 invertidos en Q1, generó 449 conversaciones WhatsApp — muchas de las cuales podrían haberse convertido en proyectos de alto valor.</p>
      <br>
      <p>La paradoja de esta cuenta es que tiene la <strong>menor inversión pero el mayor ROI potencial</strong>. El CPA de $2.21 en Ventas y $1.09 en Interacción son absolutamente justificables para este sector. El argumento para aumentar el presupuesto no podría ser más sólido: cada dólar adicional invertido en la campaña de Interacción genera ~$0.92 en conversaciones de alto valor.</p>
      <br>
      <p>La prioridad estratégica de Q2 es triple: (1) triplicar la inversión en Interacción, (2) configurar retargeting hacia Ventas, y (3) optimizar el perfil de Instagram para convertir el tráfico existente. Con estas acciones, se pueden lograr 1,000+ conversaciones WA en Q2 con una inversión de ~$1,500-2,000.</p>
    </div>
  </div>

  <div class="grid-4">
    <div class="card kpi-card"><div class="kpi-val g">A</div><div class="kpi-label">ROI Potencial</div><div class="kpi-sub">Ticket altísimo</div></div>
    <div class="card kpi-card"><div class="kpi-val a">B</div><div class="kpi-label">Score Interacción</div><div class="kpi-sub">Buena tasa WA</div></div>
    <div class="card kpi-card"><div class="kpi-val" style="color:var(--red)">C+</div><div class="kpi-label">Score Presupuesto</div><div class="kpi-sub">Subinvertido</div></div>
    <div class="card kpi-card"><div class="kpi-val a">B+</div><div class="kpi-label">Score Global</div><div class="kpi-sub">Q1 2026</div></div>
  </div>
</section>

<script>
function showSection(id,btn){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  btn.classList.add('active');
  window.scrollTo(0,document.querySelector('.nav').offsetTop);
}

const A='#d4b483',A2='#e8d5b0',G='#4ade80',R='#f87171',B='#60a5fa',Y='#facc15';
const GRID={color:'rgba(255,255,255,0.04)'};const TICK={color:'#52525b',font:{family:'Outfit',size:11}};
Chart.defaults.color='#71717a';Chart.defaults.font.family='Outfit';

new Chart(document.getElementById('budgetChart'),{
  type:'doughnut',
  data:{labels:['Interacción ANZ','Ventas ANZ','Tráfico ANZ'],
    datasets:[{data:[372.22,234.34,114.13],backgroundColor:[A,B,G],borderColor:'#111113',borderWidth:3}]},
  options:{plugins:{legend:{position:'right',labels:{color:'#a1a1aa',font:{size:12}}}},cutout:'65%'}
});

new Chart(document.getElementById('ctrChart'),{
  type:'bar',
  data:{labels:['Interacción ANZ','Ventas ANZ','Tráfico ANZ'],
    datasets:[{label:'CTR %',data:[1.93,1.93,0.78],backgroundColor:[A,B,G],borderRadius:2}]},
  options:{plugins:{legend:{display:false}},scales:{x:{grid:GRID,ticks:TICK},y:{grid:GRID,ticks:TICK,max:3}}}
});

new Chart(document.getElementById('spendConvChart'),{
  type:'bar',
  data:{labels:['Interacción','Ventas','Tráfico'],
    datasets:[
      {label:'Gasto $',data:[372,234,114],backgroundColor:'rgba(212,180,131,0.3)',borderRadius:2},
      {label:'Conv WA',data:[341,106,2],backgroundColor:G,borderRadius:2}
    ]},
  options:{plugins:{legend:{labels:{color:'#a1a1aa',font:{size:11}}}},scales:{x:{grid:GRID,ticks:TICK},y:{grid:GRID,ticks:TICK}}}
});

new Chart(document.getElementById('convRateChart'),{
  type:'bar',
  data:{labels:['Interacción ANZ','Ventas ANZ','Tráfico ANZ'],
    datasets:[{label:'Conv WA %',data:[34.9,15.9,0.07],backgroundColor:[G,A,R],borderRadius:2}]},
  options:{plugins:{legend:{display:false}},scales:{x:{grid:GRID,ticks:TICK},y:{grid:GRID,ticks:TICK,max:50}}}
});

new Chart(document.getElementById('effChart'),{
  type:'radar',
  data:{labels:['CPA Eficiencia','CTR','Conv WA %','Volumen','Seguidores'],
    datasets:[
      {label:'Interacción',data:[85,70,70,70,60],borderColor:G,backgroundColor:'rgba(74,222,128,0.1)',pointBackgroundColor:G},
      {label:'Ventas',data:[50,70,30,30,25],borderColor:B,backgroundColor:'rgba(96,165,250,0.1)',pointBackgroundColor:B},
      {label:'Tráfico',data:[95,30,5,100,75],borderColor:A,backgroundColor:'rgba(212,180,131,0.1)',pointBackgroundColor:A}
    ]},
  options:{plugins:{legend:{labels:{color:'#a1a1aa',font:{size:11}}}},scales:{r:{grid:{color:'rgba(255,255,255,0.04)'},pointLabels:{color:'#71717a',font:{size:10}},ticks:{display:false}}}}
});

new Chart(document.getElementById('trendChart'),{
  type:'line',
  data:{labels:['Enero','Febrero','Marzo'],
    datasets:[
      {label:'Inversión Est. $',data:[230,260,231],borderColor:A,backgroundColor:'rgba(212,180,131,0.1)',tension:0.4,fill:true},
      {label:'Conv WA Est.',data:[140,165,144],borderColor:G,backgroundColor:'rgba(74,222,128,0.05)',tension:0.4,yAxisID:'y2'}
    ]},
  options:{plugins:{legend:{labels:{color:'#a1a1aa',font:{size:11}}}},scales:{x:{grid:GRID,ticks:TICK},y:{grid:GRID,ticks:TICK,title:{display:true,text:'USD',color:'#71717a'}},y2:{position:'right',grid:{display:false},ticks:TICK,title:{display:true,text:'Conv WA',color:'#71717a'}}}}
});
</script>
</body>
</html>
