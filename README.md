<doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>شرح The Dude - واجهة موقع بديلة للبوربوينت</title>
  <style>
    :root{
      --bg:#0b1020; --panel:#0f1730; --card:#111c3a; --card2:#0d1630;
      --text:#e9eeff; --muted:rgba(233,238,255,.72);
      --line:rgba(255,255,255,.10);
      --accent:#4cc9f0; --good:#66ffb3; --warn:#ffd166; --bad:#ff6b6b;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
      --r:18px;
      --font: system-ui,-apple-system,Segoe UI,Roboto,Arial,"Noto Sans Arabic","Tahoma";
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:var(--font);
      background: radial-gradient(1200px 700px at 85% 20%, rgba(76,201,240,.14), transparent 55%),
                  radial-gradient(900px 500px at 15% 85%, rgba(102,255,179,.10), transparent 55%),
                  var(--bg);
      color:var(--text);
    }
    a{color:inherit}
    .app{
      height:100vh;
      display:grid;
      grid-template-columns: 340px 1fr;
      overflow:hidden;
    }
    /* Sidebar */
    .sidebar{
      background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));
      border-left:1px solid var(--line);
      padding:18px;
      overflow:auto;
    }
    .brand{
      display:flex; gap:10px; align-items:center;
      padding:12px 12px;
      border:1px solid var(--line);
      border-radius: var(--r);
      background: rgba(0,0,0,.18);
      box-shadow: var(--shadow);
      margin-bottom:14px;
    }
    .logo{
      width:36px;height:36px;border-radius:12px;
      background: radial-gradient(circle at 30% 30%, rgba(255,255,255,.35), transparent 45%),
                  linear-gradient(135deg, rgba(76,201,240,.9), rgba(102,255,179,.6));
      box-shadow: 0 0 18px rgba(76,201,240,.25);
      flex:0 0 auto;
    }
    .brand h1{font-size:14px;margin:0}
    .brand p{margin:2px 0 0; font-size:12px; color:var(--muted); line-height:1.35}
    .search{
      width:100%;
      padding:10px 12px;
      border-radius: 14px;
      border:1px solid var(--line);
      background: rgba(0,0,0,.20);
      color:var(--text);
      outline:none;
      margin: 8px 0 14px;
    }
    .nav{
      display:grid;
      gap:10px;
    }
    .nav button{
      width:100%;
      text-align:right;
      border:1px solid var(--line);
      background: rgba(255,255,255,.03);
      color:var(--text);
      padding:12px 12px;
      border-radius: 16px;
      cursor:pointer;
      transition: transform .12s ease, background .12s ease, border-color .12s ease;
      display:flex;
      gap:10px;
      align-items:flex-start;
    }
    .nav button:hover{transform: translateY(-1px); background: rgba(255,255,255,.05); border-color: rgba(255,255,255,.18);}
    .nav button.active{background: rgba(76,201,240,.14); border-color: rgba(76,201,240,.38);}
    .nav .ic{
      width:34px;height:34px;border-radius:14px;
      background: rgba(255,255,255,.06);
      border:1px solid var(--line);
      display:grid; place-items:center;
      flex:0 0 auto;
    }
    .nav .ttl{font-weight:700; font-size:13px; margin:0 0 2px}
    .nav .dsc{margin:0; font-size:12px; color:var(--muted); line-height:1.35}
    .sideFooter{
      margin-top:14px;
      border:1px solid var(--line);
      background: rgba(0,0,0,.18);
      border-radius: var(--r);
      padding:12px;
      color:var(--muted);
      font-size:12px;
      line-height:1.55;
    }
    .chip{
      display:inline-flex; align-items:center; gap:8px;
      padding:6px 10px;
      border-radius:999px;
      border:1px solid var(--line);
      background: rgba(0,0,0,.22);
      margin-top:10px;
      color:var(--text);
      font-size:12px;
    }
    .dot{width:8px;height:8px;border-radius:50%; background:var(--good); box-shadow: 0 0 12px rgba(102,255,179,.55);}

    /* Main */
    .main{
      overflow:auto;
      padding:18px 18px 40px;
    }
    .topbar{
      display:flex; gap:12px; align-items:center; justify-content:space-between;
      margin-bottom:14px;
    }
    .breadcrumbs{
      display:flex; gap:8px; align-items:center; flex-wrap:wrap;
      color:var(--muted); font-size:12px;
    }
    .breadcrumbs b{color:var(--text)}
    .actions{
      display:flex; gap:10px; align-items:center; flex-wrap:wrap;
    }
    .btn{
      border:1px solid var(--line);
      background: rgba(0,0,0,.20);
      color:var(--text);
      padding:9px 12px;
      border-radius: 14px;
      cursor:pointer;
      transition: background .12s ease, border-color .12s ease, transform .12s ease;
      font-size:12px;
      display:inline-flex; gap:8px; align-items:center;
    }
    .btn:hover{background: rgba(255,255,255,.05); border-color: rgba(255,255,255,.18); transform: translateY(-1px);}
    .btn.primary{background: rgba(76,201,240,.18); border-color: rgba(76,201,240,.45);}
    .grid{
      display:grid;
      grid-template-columns: 1.25fr .75fr;
      gap:14px;
      align-items:start;
    }
    .hero{
      border:1px solid var(--line);
      background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));
      border-radius: 22px;
      padding:16px;
      box-shadow: var(--shadow);
    }
    .hero h2{margin:0 0 8px; font-size:20px}
    .hero p{margin:0; color:var(--muted); line-height:1.7; font-size:13px}
    .hero .metaRow{
      display:flex; flex-wrap:wrap; gap:8px;
      margin-top:12px;
    }
    .pill{
      display:inline-flex; align-items:center; gap:8px;
      padding:7px 10px;
      border-radius:999px;
      border:1px solid var(--line);
      background: rgba(0,0,0,.22);
      font-size:12px;
      color:var(--text);
    }
    .pill .s{opacity:.9}
    .status{
      width:10px;height:10px;border-radius:50%;
      background: var(--accent);
      box-shadow: 0 0 14px rgba(76,201,240,.45);
    }
    .card{
      border:1px solid var(--line);
      background: rgba(255,255,255,.03);
      border-radius: 22px;
      padding:14px;
      box-shadow: var(--shadow);
    }
    .card h3{margin:0 0 8px; font-size:14px}
    .card p{margin:0; color:var(--muted); line-height:1.65; font-size:12.5px}
    .split{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap:12px;
      margin-top:14px;
    }
    .box{
      border:1px solid var(--line);
      background: rgba(0,0,0,.18);
      border-radius: 18px;
      padding:12px;
    }
    .box h4{margin:0 0 6px; font-size:13px}
    .box ul{margin:0; padding:0 18px 0 0; color:var(--muted); font-size:12.5px; line-height:1.65}
    .box li{margin:4px 0}
    .section{
      margin-top:14px;
      border:1px solid var(--line);
      border-radius: 22px;
      background: rgba(255,255,255,.02);
      padding:14px;
    }
    .sectionTitle{
      display:flex; align-items:center; justify-content:space-between;
      gap:10px;
      margin-bottom:10px;
    }
    .sectionTitle h3{margin:0; font-size:14px}
    .sectionTitle .small{color:var(--muted); font-size:12px}
    .hotspots{
      display:grid;
      grid-template-columns: 1.2fr .8fr;
      gap:12px;
      align-items:start;
    }
    .mock{
      border:1px solid var(--line);
      border-radius: 18px;
      background: linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.02));
      padding:12px;
      position:relative;
      overflow:hidden;
      min-height: 260px;
    }
    .mockHeader{
      display:flex; align-items:center; justify-content:space-between;
      gap:10px;
      margin-bottom:10px;
    }
    .mockHeader .tag{
      display:inline-flex; align-items:center; gap:8px;
      padding:6px 10px;
      border-radius:999px;
      border:1px solid var(--line);
      background: rgba(0,0,0,.20);
      font-size:12px;
      color:var(--text);
    }
    .mockArea{
      display:grid;
      grid-template-columns: repeat(2, 1fr);
      gap:10px;
      margin-top:10px;
    }
    .node{
      border:1px solid rgba(255,255,255,.10);
      border-radius: 16px;
      padding:10px;
      cursor:pointer;
      background: rgba(0,0,0,.18);
      transition: transform .12s ease, border-color .12s ease, background .12s ease;
      position:relative;
    }
    .node:hover{transform: translateY(-1px); border-color: rgba(76,201,240,.35); background: rgba(76,201,240,.08);}
    .node .name{font-weight:700; font-size:12px; margin:0 0 6px}
    .node .mini{font-size:11px; color:var(--muted); margin:0}
    .badge{
      position:absolute; left:10px; top:10px;
      font-size:10px;
      padding:4px 8px;
      border-radius:999px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(0,0,0,.24);
    }
    .badge.good{border-color: rgba(102,255,179,.35); }
    .badge.warn{border-color: rgba(255,209,102,.35); }
    .badge.bad{border-color: rgba(255,107,107,.35); }

    .infoPanel{
      border:1px solid var(--line);
      border-radius: 18px;
      background: rgba(0,0,0,.18);
      padding:12px;
      position:sticky;
      top:14px;
    }
    .infoPanel h4{margin:0 0 8px; font-size:13px}
    .infoPanel p{margin:0; color:var(--muted); font-size:12.5px; line-height:1.65}
    .kv{
      margin-top:10px;
      display:grid; gap:6px;
      font-size:12px;
      color:var(--muted);
    }
    .kv div{
      display:flex; justify-content:space-between; gap:10px;
      border:1px solid rgba(255,255,255,.08);
      background: rgba(255,255,255,.02);
      padding:8px 10px;
      border-radius: 12px;
    }
    .kv b{color:var(--text); font-weight:700}

    .timeline{
      display:grid; gap:10px;
      margin-top:10px;
    }
    .step{
      border:1px solid rgba(255,255,255,.10);
      background: rgba(0,0,0,.16);
      border-radius: 16px;
      padding:10px;
      display:flex; gap:10px;
      align-items:flex-start;
    }
    .num{
      width:26px;height:26px;border-radius:10px;
      display:grid; place-items:center;
      background: rgba(76,201,240,.15);
      border:1px solid rgba(76,201,240,.35);
      font-weight:800;
      flex:0 0 auto;
    }
    .step h5{margin:0 0 4px; font-size:12.5px}
    .step p{margin:0; font-size:12px; color:var(--muted); line-height:1.55}

    .table{
      width:100%;
      border-collapse: separate;
      border-spacing: 0;
      overflow:hidden;
      border-radius: 16px;
      border:1px solid var(--line);
      margin-top:10px;
    }
    .table th, .table td{
      padding:10px 10px;
      font-size:12.5px;
      border-bottom:1px solid rgba(255,255,255,.08);
      text-align:right;
    }
    .table th{color:var(--text); background: rgba(255,255,255,.04); font-weight:800}
    .table td{color:var(--muted); background: rgba(0,0,0,.10)}
    .table tr:last-child td{border-bottom:0}

    .kbd{
      display:inline-flex; align-items:center;
      padding:2px 7px;
      border-radius: 8px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(0,0,0,.25);
      font-size:11px; color:var(--text);
    }

    /* Modal */
    .overlay{
      position:fixed; inset:0;
      background: rgba(0,0,0,.55);
      display:none;
      align-items:center; justify-content:center;
      padding:16px;
      z-index: 50;
    }
    .modal{
      width:min(820px, 100%);
      border-radius: 22px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(12,16,32,.92);
      backdrop-filter: blur(12px);
      box-shadow: 0 20px 60px rgba(0,0,0,.55);
      padding:14px;
    }
    .modalHeader{
      display:flex; align-items:center; justify-content:space-between; gap:12px;
      padding:4px 6px 10px;
      border-bottom:1px solid rgba(255,255,255,.10);
    }
    .modalHeader h3{margin:0; font-size:14px}
    .modalBody{padding:10px 6px 6px}
    pre{
      margin:0;
      padding:12px;
      border-radius: 16px;
      border:1px solid rgba(255,255,255,.10);
      background: rgba(0,0,0,.30);
      color:#e9eeff;
      overflow:auto;
      font-size:12px;
      line-height:1.6;
      direction:ltr;
      text-align:left;
      white-space: pre-wrap;
    }

    /* Responsive */
    @media (max-width: 980px){
      .app{grid-template-columns: 1fr; grid-template-rows: auto 1fr;}
      .sidebar{border-left:0; border-bottom:1px solid var(--line);}
      .grid{grid-template-columns: 1fr;}
      .hotspots{grid-template-columns: 1fr;}
      .infoPanel{position:static;}
    }
  </style>
</head>
<body>
  <div class="app">
    <!-- Sidebar -->
    <aside class="sidebar">
      <div class="brand">
        <div class="logo"></div>
        <div>
          <h1>شرح The Dude (MikroTik)</h1>
          <p>واجهة موقع تفاعلية بديلة للبوربوينت — صفحات + تفاعل + أمثلة عملية</p>
        </div>
      </div>

      <input id="search" class="search" placeholder="ابحث… (Devices / Probes / Notifications / SNMP)" />

      <nav class="nav" id="nav"></nav>

      <div class="sideFooter">
        <div><b>طريقة الاستخدام:</b></div>
        <div>• اختر قسم من القائمة.</div>
        <div>• اضغط على العناصر التفاعلية داخل الصفحة.</div>
        <div>• استخدم زر <span class="kbd">عرض سكربت</span> لعرض أوامر MikroTik.</div>
        <div class="chip"><span class="dot"></span>مناسب لعرض تدريبي/NOC</div>
      </div>
    </aside>

    <!-- Main -->
    <main class="main">
      <div class="topbar">
        <div class="breadcrumbs" id="crumbs">أنت الآن: <b>—</b></div>
        <div class="actions">
          <button class="btn" id="prevBtn">⬅ السابق</button>
          <button class="btn" id="nextBtn">التالي ➡</button>
          <button class="btn primary" id="openScript">عرض سكربت</button>
        </div>
      </div>

      <div id="content"></div>
    </main>
  </div>

  <!-- Modal -->
  <div class="overlay" id="overlay" role="dialog" aria-modal="true">
    <div class="modal">
      <div class="modalHeader">
        <h3 id="modalTitle">أوامر/ملاحظات</h3>
        <button class="btn" id="closeModal">إغلاق ✕</button>
      </div>
      <div class="modalBody">
        <pre id="modalCode"></pre>
      </div>
    </div>
  </div>

  <script>
    // ========== Content Data (Edit freely) ==========
    const SECTIONS = [
      {
        id: "intro",
        title: "1) ما هو The Dude؟",
        desc: "تعريف سريع + لماذا نستخدمه بدل ما تضل تتابع يدوي.",
        hero: {
          title: "The Dude = مراقبة الشبكة + خريطة + تنبيهات",
          text:
            "The Dude من MikroTik هو نظام مراقبة شبكات يساعدك على رسم الشبكة تلقائيًا، متابعة حالة الأجهزة (Online/Down)، مراقبة الخدمات (Ping/SNMP/TCP)، وإرسال تنبيهات عند الأعطال."
        },
        bulletsA: {
          title: "ليش مهم؟",
          items: [
            "يعطيك رؤية لحظية للشبكة (Real-time).",
            "يرسم Map للأجهزة والروابط تلقائيًا.",
            "تنبيهات (Popup/Email/Telegram) عند Down/Up.",
            "يدعم أجهزة MikroTik وغيرها عبر SNMP/ICMP."
          ]
        },
        bulletsB: {
          title: "مصطلحات سريعة",
          items: [
            "Device: الجهاز نفسه (Router/Switch/Server).",
            "Service: شيء نراقبه على الجهاز (Ping/SNMP/HTTP...).",
            "Probe: طريقة الفحص (ICMP/SNMP/TCP...).",
            "Notification: ماذا يحدث عند تغيّر الحالة."
          ]
        },
        rightCard: {
          title: "متى تستخدمه؟",
          text: "ممتاز لـ NOC، مزود إنترنت ISP، أبراج واتصالات، شبكات كبيرة، شبكات Hotspot/PPPoE."
        },
        scripts: [
          { name: "ملاحظة مهمة", code: "• يمكن تشغيل The Dude كـ Client على Windows أو كـ Server على MikroTik.\n• الأفضل للشبكات الكبيرة: تشغيل Server على Router مناسب أو VM." }
        ]
      },
      {
        id: "arch",
        title: "2) كيف يعمل؟ (Architecture)",
        desc: "فهم Client/Server/Devices/Probes بطريقة واضحة.",
        hero: {
          title: "فكرة العمل: Server يفحص — Client يعرض",
          text:
            "عادةً يوجد Dude Server (مكان تخزين + فحص) و Dude Client (واجهة التحكم). السيرفر يقوم بعمل probes للأجهزة والخدمات ويحتفظ بالتاريخ والرسوم البيانية."
        },
        rightCard: {
          title: "نصيحة تصميم",
          text:
            "قسّم الشبكة إلى Maps: Core / Access / Wireless / Power. هذا يسهّل العرض للإدارة ويقلّل الزحمة."
        },
        extra: {
          title: "تسلسل العمل",
          steps: [
            { t: "إضافة/اكتشاف الأجهزة", d: "تضيف Range أو Subnet → Dude يكتشف الأجهزة والخدمات." },
            { t: "تحديد الخدمات المهمة", d: "Ping + SNMP + منافذ حساسة (SSH/HTTP/Winbox…)." },
            { t: "ربط التنبيهات", d: "عند Down/Up أو عند تجاوز Threshold." },
            { t: "تقارير ورسوم", d: "Traffic/CPU/RAM/Links history." }
          ]
        },
        scripts: [
          { name: "أفضل بروتوكولات المراقبة", code: "ICMP (Ping)\nSNMP (CPU/RAM/Interfaces)\nTCP (Port check)\nHTTP/HTTPS (Web health)\nDNS (Resolution)" }
        ]
      },
      {
        id: "ui",
        title: "3) الواجهة الرئيسية",
        desc: "Map / Devices / Services / Notifications بشكل تفاعلي.",
        hero: {
          title: "أهم أقسام الواجهة",
          text:
            "الواجهة تتقسم لأربع مناطق: Map لعرض الخريطة، Devices للأجهزة، Services للخدمات، Notifications للتنبيهات. كل عنصر له حالة ورسوم."
        },
        hotspots: {
          title: "اضغط على عنصر للتعلّم (Interactive)",
          nodes: [
            {
              key: "Map",
              state: "good",
              title: "Map (الخريطة)",
              text: "ترتيب الأجهزة بصريًا. تقدر تعمل خرائط متعددة حسب المنطقة/الطبقة.",
              meta: { "استخدام": "عرض الشبكة", "أفضل ممارسة": "خرائط حسب Core/Access" }
            },
            {
              key: "Devices",
              state: "good",
              title: "Devices (الأجهزة)",
              text: "قائمة كل الأجهزة مع الحالة والـ IP والتصنيف. منها تعمل Groups و Templates.",
              meta: { "مهم": "تصنيف جيد", "تلميح": "استخدم Icons" }
            },
            {
              key: "Services",
              state: "warn",
              title: "Services (الخدمات)",
              text: "الخدمات على كل جهاز: Ping/SNMP/TCP… لو خدمة Down تظهر لك المشكلة بدقة.",
              meta: { "فائدة": "تحديد سبب العطل", "تنبيه": "لا تراقب كل شيء بلا داعي" }
            },
            {
              key: "Notifications",
              state: "bad",
              title: "Notifications (التنبيهات)",
              text: "إعداد ما يحدث عند Down/Up: Email/Popup/Telegram… مع شروط مثل تأخير 30 ثانية.",
              meta: { "أفضل شرط": "Delay", "سبب": "منع إنذارات كاذبة" }
            }
          ]
        },
        scripts: [
          { name: "فكرة إعداد Delay للتنبيه", code: "مثال سياسة:\nإذا الجهاز Down لمدة 30 ثانية → أرسل تنبيه\nإذا عاد Up → أرسل إشعار رجوع\n\nالهدف: تقليل False alarms بسبب تقلبات قصيرة." }
        ]
      },
      {
        id: "devices-services",
        title: "4) Devices & Services",
        desc: "الفرق العملي بين Device و Service مع أمثلة.",
        hero: {
          title: "Device ≠ Service",
          text:
            "الجهاز هو الراوتر/السويتش/السيرفر. الخدمات هي ما تراقبه على هذا الجهاز. ممكن الجهاز Online لكن خدمة معينة Down (مثلاً HTTP Down)."
        },
        rightCard: {
          title: "مثال سريع",
          text:
            "Router Online (Ping OK) لكن SNMP Down → لن ترى CPU/RAM/Traffic. أو HTTP Down → الموقع لا يعمل رغم أن Ping يعمل."
        },
        table: {
          title: "أمثلة شائعة",
          head: ["العنصر", "ماذا يعني؟", "متى تستخدمه؟"],
          rows: [
            ["Ping (ICMP)", "اختبار اتصال عام", "معرفة Online/Down بشكل سريع"],
            ["SNMP", "قراءة CPU/RAM/Interfaces", "تقارير وGraphs وTraffic"],
            ["TCP Port", "فحص منفذ (22/80/8291…)", "التأكد أن الخدمة تعمل"],
            ["HTTP/HTTPS", "فحص موقع/واجهة ويب", "تطبيقات أو صفحات إدارية"]
          ]
        },
        scripts: [
          {
            name: "SNMP على MikroTik",
            code:
`/snmp set enabled=yes
/snmp community add name=dude addresses=0.0.0.0/0

# ملاحظة: غيّر addresses لتكون محددة (Subnet السيرفر) للأمان.`
          }
        ]
      },
      {
        id: "probes",
        title: "5) Probes (طرق الفحص)",
        desc: "كيف تختار Probe صحيح بدون ما تثقل السيرفر.",
        hero: {
          title: "Probes = طريقة القياس",
          text:
            "الـ Probe هو الاختبار الذي يقوم به Dude ليتأكد أن الجهاز/الخدمة تعمل. اختار probes حسب أهمية الخدمة لتقليل الحمل."
        },
        rightCard: {
          title: "قاعدة ذهبية",
          text:
            "ابدأ بـ Ping + SNMP للأجهزة المهمة فقط. ثم أضف TCP/HTTP للخدمات الحساسة. لا تراقب كل شيء على كل جهاز."
        },
        table: {
          title: "أشهر Probes",
          head: ["Probe", "الوصف", "متى يُستخدم؟"],
          rows: [
            ["ICMP", "Ping", "أساس المراقبة للأجهزة"],
            ["SNMP", "قراءات وCounters", "Traffic/CPU/RAM/Signal"],
            ["TCP", "Port check", "SSH/Winbox/Web/DB"],
            ["HTTP", "Health check للويب", "واجهات الإدارة/المواقع"],
            ["DNS", "Resolution", "تأكد أن DNS يعمل"]
          ]
        },
        scripts: [
          { name: "اقتراح توزيع Probes", code: "Core routers: Ping + SNMP + BGP port\nAccess switches: Ping + SNMP\nServers: Ping + TCP (ports) + HTTP\nWireless links: SNMP + Signal (إن توفر MIB)" }
        ]
      },
      {
        id: "alerts",
        title: "6) Notifications & Policies",
        desc: "كيف تبني تنبيه محترم (بدون إزعاج).",
        hero: {
          title: "تنبيه صحيح = شرط + قناة + رسالة واضحة",
          text:
            "Notifications هي ماذا سيحصل عند Down/Up. Policies تضبط من يستلم ومتى وكيف. الأفضل وضع Delay وفلترة حسب الأهمية."
        },
        extra: {
          title: "سيناريو عملي للتنبيه",
          steps: [
            { t: "Down", d: "إذا الجهاز انقطع (Ping fail)" },
            { t: "Delay", d: "انتظر 30 ثانية لتأكيد العطل" },
            { t: "Notify", d: "أرسل Email/Popup/Telegram" },
            { t: "Up", d: "عند الرجوع أرسل إشعار رجوع (Recovery)" }
          ]
        },
        rightCard: {
          title: "رسالة تنبيه احترافية",
          text:
            "لا ترسل فقط 'Down'. اكتب: اسم الجهاز + IP + الموقع + الوقت + آخر خدمة فشلت."
        },
        scripts: [
          { name: "نص رسالة تنبيه مقترح", code: "ALERT: Device Down\nName: {device.name}\nIP: {device.ip}\nMap: {map.name}\nTime: {time}\nLast service: {service.name}" },
          { name: "Telegram (فكرة عامة)", code: "يمكنك إرسال Telegram عبر Script/HTTP request.\nإذا بدك، أعطيك سكربت جاهز حسب البوت والـ chat_id." }
        ]
      },
      {
        id: "practice",
        title: "7) تطبيق عملي (NOC/ISP)",
        desc: "كيف ترتب الشبكة وتعرضها للإدارة.",
        hero: {
          title: "أفضل شكل للعرض بدل PowerPoint",
          text:
            "اعرض خرائط حسب المناطق والطبقات: Core / Access / Towers / Power. كل خريطة فيها أهم الأجهزة فقط، مع Links وTraffic. هذا يعطي عرض حيّ أفضل من السلايدات."
        },
        bulletsA: {
          title: "تقسيم خرائط مقترح",
          items: [
            "Core Map: Routers, Core Switches, Upstream links",
            "Access Map: OLTs, Agg switches, Distribution",
            "Wireless/Towers: Backhaul, Sectors, Radios",
            "Power: Rectifiers, batteries, mains status"
          ]
        },
        bulletsB: {
          title: "قواعد ذهبية في العرض",
          items: [
            "استخدم ألوان حالة واضحة (Online/Warning/Down).",
            "اعرض Links الحرجة مع Traffic graphs.",
            "لا تحط أجهزة ثانوية إلا عند الحاجة.",
            "حافظ على نفس الترتيب في كل Map لتسهيل الفهم."
          ]
        },
        scripts: [
          { name: "Checklist قبل العرض", code: "✓ SNMP شغال للأجهزة المهمة\n✓ Notifications مفعلة مع Delay\n✓ Maps مرتبة حسب الطبقات\n✓ Graphs مفعلة للروابط الحرجة\n✓ Backup للإعدادات" }
        ]
      }
    ];

    // ========== App State ==========
    let activeIndex = 0;
    let selectedHotspot = null;

    const navEl = document.getElementById("nav");
    const contentEl = document.getElementById("content");
    const crumbsEl = document.getElementById("crumbs");
    const searchEl = document.getElementById("search");

    const prevBtn = document.getElementById("prevBtn");
    const nextBtn = document.getElementById("nextBtn");
    const openScriptBtn = document.getElementById("openScript");

    const overlay = document.getElementById("overlay");
    const modalTitle = document.getElementById("modalTitle");
    const modalCode = document.getElementById("modalCode");
    const closeModal = document.getElementById("closeModal");

    // ========== Render Sidebar ==========
    function iconSVG(name){
      // Tiny inline SVG icons
      const common = (p)=>`<svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">${p}</svg>`;
      const icons = {
        intro: common(`<path d="M12 2l9 4.8v10.4L12 22 3 17.2V6.8L12 2Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M12 7v10" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/><path d="M8 11h8" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/>`),
        arch: common(`<path d="M6 7h12v4H6V7Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M8 17h8v4H8v-4Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M12 11v6" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/>`),
        ui: common(`<path d="M4 5h16v14H4V5Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M4 9h16" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/><path d="M8 13h4" stroke="rgba(233,238,255,.6)" stroke-width="1.8"/><path d="M8 16h8" stroke="rgba(233,238,255,.6)" stroke-width="1.8"/>`),
        "devices-services": common(`<path d="M7 3h10v6H7V3Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M5 13h14v8H5v-8Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M9 16h6" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/>`),
        probes: common(`<path d="M12 2v20" stroke="rgba(233,238,255,.35)" stroke-width="1.8"/><path d="M6 8l6-6 6 6" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/><path d="M6 16l6 6 6-6" stroke="rgba(102,255,179,.85)" stroke-width="1.8"/>`),
        alerts: common(`<path d="M12 3a6 6 0 0 0-6 6v4l-2 2h16l-2-2V9a6 6 0 0 0-6-6Z" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M10 19a2 2 0 0 0 4 0" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/>`),
        practice: common(`<path d="M4 20V6a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v14" stroke="rgba(233,238,255,.9)" stroke-width="1.8"/><path d="M7 8h10" stroke="rgba(76,201,240,.9)" stroke-width="1.8"/><path d="M7 12h10" stroke="rgba(233,238,255,.6)" stroke-width="1.8"/><path d="M7 16h7" stroke="rgba(102,255,179,.8)" stroke-width="1.8"/>`)
      };
      return icons[name] || icons.ui;
    }

    function renderNav(filter=""){
      navEl.innerHTML = "";
      const f = filter.trim().toLowerCase();

      SECTIONS.forEach((s, idx)=>{
        const match = !f || (s.title + " " + s.desc + " " + JSON.stringify(s)).toLowerCase().includes(f);
        if(!match) return;

        const btn = document.createElement("button");
        btn.className = idx === activeIndex ? "active" : "";
        btn.innerHTML = `
          <div class="ic">${iconSVG(s.id)}</div>
          <div>
            <div class="ttl">${s.title}</div>
            <p class="dsc">${s.desc}</p>
          </div>
        `;
        btn.addEventListener("click", ()=>{ activeIndex = idx; selectedHotspot=null; renderAll(); });
        navEl.appendChild(btn);
      });
    }

    // ========== Render Content ==========
    function escapeHtml(str){
      return (str ?? "").toString()
        .replaceAll("&","&amp;")
        .replaceAll("<","&lt;")
        .replaceAll(">","&gt;");
    }

    function statusBadgeClass(state){
      if(state==="good") return "good";
      if(state==="warn") return "warn";
      return "bad";
    }

    function renderHero(section){
      const h = section.hero;
      return `
        <div class="hero">
          <h2>${escapeHtml(h.title)}</h2>
          <p>${escapeHtml(h.text)}</p>
          <div class="metaRow">
            <span class="pill"><span class="status"></span><span class="s">شرح تفاعلي بدل PowerPoint</span></span>
            <span class="pill"><span class="status" style="background:var(--good); box-shadow:0 0 14px rgba(102,255,179,.45)"></span><span class="s">جاهز Offline/Online</span></span>
            <span class="pill"><span class="status" style="background:var(--warn); box-shadow:0 0 14px rgba(255,209,102,.45)"></span><span class="s">قابل للتعديل</span></span>
          </div>
        </div>
      `;
    }

    function renderBullets(block){
      if(!block) return "";
      const items = (block.items||[]).map(i=>`<li>${escapeHtml(i)}</li>`).join("");
      return `
        <div class="box">
          <h4>${escapeHtml(block.title)}</h4>
          <ul>${items}</ul>
        </div>
      `;
    }

    function renderSteps(extra){
      if(!extra) return "";
      const steps = (extra.steps||[]).map((s,i)=>`
        <div class="step">
          <div class="num">${i+1}</div>
          <div>
            <h5>${escapeHtml(s.t)}</h5>
            <p>${escapeHtml(s.d)}</p>
          </div>
        </div>
      `).join("");
      return `
        <div class="section">
          <div class="sectionTitle">
            <h3>${escapeHtml(extra.title)}</h3>
            <div class="small">سيناريو عملي</div>
          </div>
          <div class="timeline">${steps}</div>
        </div>
      `;
    }

    function renderTable(tbl){
      if(!tbl) return "";
      const head = tbl.head.map(h=>`<th>${escapeHtml(h)}</th>`).join("");
      const rows = tbl.rows.map(r=>`<tr>${r.map(c=>`<td>${escapeHtml(c)}</td>`).join("")}</tr>`).join("");
      return `
        <div class="section">
          <div class="sectionTitle">
            <h3>${escapeHtml(tbl.title)}</h3>
            <div class="small">مرجع سريع</div>
          </div>
          <table class="table">
            <thead><tr>${head}</tr></thead>
            <tbody>${rows}</tbody>
          </table>
        </div>
      `;
    }

    function renderHotspots(section){
      const hs = section.hotspots;
      if(!hs) return "";
      const nodes = hs.nodes.map(n=>`
        <div class="node" data-key="${escapeHtml(n.key)}">
          <span class="badge ${statusBadgeClass(n.state)}">
            ${n.state==="good" ? "OK" : n.state==="warn" ? "INFO" : "ALERT"}
          </span>
          <div class="name">${escapeHtml(n.title)}</div>
          <p class="mini">${escapeHtml(n.text)}</p>
        </div>
      `).join("");

      const right = selectedHotspot ? selectedHotspot : hs.nodes[0];
      const meta = Object.entries(right.meta || {}).map(([k,v])=>`
        <div><span>${escapeHtml(k)}</span><b>${escapeHtml(v)}</b></div>
      `).join("");

      return `
        <div class="section">
          <div class="sectionTitle">
            <h3>${escapeHtml(hs.title)}</h3>
            <div class="small">اضغط على أي مربع</div>
          </div>

          <div class="hotspots">
            <div class="mock">
              <div class="mockHeader">
                <div class="tag">📍 محاكاة واجهة — Components</div>
                <div class="tag">Tip: Hover ثم Click</div>
              </div>
              <div class="mockArea">
                ${nodes}
              </div>
            </div>

            <div class="infoPanel" id="infoPanel">
              <h4>تفاصيل العنصر</h4>
              <p><b style="color:var(--text)">${escapeHtml(right.title)}</b><br/>${escapeHtml(right.text)}</p>
              <div class="kv">${meta}</div>
            </div>
          </div>
        </div>
      `;
    }

    function renderRightCard(section){
      if(!section.rightCard) return "";
      return `
        <div class="card">
          <h3>${escapeHtml(section.rightCard.title)}</h3>
          <p>${escapeHtml(section.rightCard.text)}</p>
          <div style="margin-top:10px; display:grid; gap:8px;">
            <div class="pill"><span class="status" style="background:var(--good)"></span><span class="s">نقطة: استخدم Delay للتنبيهات</span></div>
            <div class="pill"><span class="status" style="background:var(--accent)"></span><span class="s">نقطة: خرائط حسب الطبقات</span></div>
          </div>
        </div>
      `;
    }

    function renderSection(section){
      const splitHtml = (section.bulletsA || section.bulletsB) ? `
        <div class="split">
          ${renderBullets(section.bulletsA)}
          ${renderBullets(section.bulletsB)}
        </div>
      ` : "";

      const mainHtml = `
        <div class="grid">
          <div>
            ${renderHero(section)}
            ${splitHtml}
            ${renderHotspots(section)}
            ${renderSteps(section.extra)}
            ${renderTable(section.table)}
          </div>
          <div>
            ${renderRightCard(section)}  
          </div>
        </div>
      `;
      return mainHtml;
    }

    function renderCrumbs(section){
      crumbsEl.innerHTML = `أنت الآن: <b>${escapeHtml(section.title)}</b> <span style="opacity:.6">•</span> <span>${escapeHtml(section.desc)}</span>`;
    }

    function renderContent(){
      const section = SECTIONS[activeIndex];
      renderCrumbs(section);
      contentEl.innerHTML = renderSection(section);

      // Attach hotspot clicks if exists
      const nodes = contentEl.querySelectorAll(".node");
      if(nodes && nodes.length){
        nodes.forEach(el=>{
          el.addEventListener("click", ()=>{
            const key = el.getAttribute("data-key");
            const hs = section.hotspots;
            const found = hs.nodes.find(n=>n.key === key);
            if(found){
              selectedHotspot = found;
              renderAll(); // re-render to update right panel
              // scroll to info panel on small screens
              const info = document.getElementById("infoPanel");
              if(info) info.scrollIntoView({behavior:"smooth", block:"center"});
            }
          });
        });
      }

      prevBtn.disabled = activeIndex === 0;
      nextBtn.disabled = activeIndex === SECTIONS.length - 1;
    }

    function renderAll(){
      renderNav(searchEl.value);
      // mark active in nav after filtering
      [...navEl.querySelectorAll("button")].forEach((b)=>{
        // re-apply active state based on text match of title
        if(b.textContent.includes(SECTIONS[activeIndex].title)) b.classList.add("active");
      });
      renderContent();
    }

    // ========== Modal Scripts ==========
    function openModal(){
      const s = SECTIONS[activeIndex];
      const scripts = s.scripts || [];
      if(!scripts.length){
        modalTitle.textContent = "لا يوجد سكربت في هذا القسم";
        modalCode.textContent = "—";
      }else{
        modalTitle.textContent = "أوامر/ملاحظات — " + s.title;
        modalCode.textContent = scripts.map((x,i)=>`# ${i+1}) ${x.name}\n${x.code}`).join("\n\n");
      }
      overlay.style.display = "flex";
    }
    function closeModalFn(){
      overlay.style.display = "none";
    }

    // ========== Events ==========
    prevBtn.addEventListener("click", ()=>{
      if(activeIndex>0){ activeIndex--; selectedHotspot=null; renderAll(); window.scrollTo({top:0, behavior:"smooth"}); }
    });
    nextBtn.addEventListener("click", ()=>{
      if(activeIndex<SECTIONS.length-1){ activeIndex++; selectedHotspot=null; renderAll(); window.scrollTo({top:0, behavior:"smooth"}); }
    });
    openScriptBtn.addEventListener("click", openModal);
    closeModal.addEventListener("click", closeModalFn);
    overlay.addEventListener("click", (e)=>{ if(e.target===overlay) closeModalFn(); });

    searchEl.addEventListener("input", ()=> renderNav(searchEl.value));

    window.addEventListener("keydown", (e)=>{
      if(e.key==="Escape") closeModalFn();
      if(e.key==="ArrowLeft") prevBtn.click();
      if(e.key==="ArrowRight") nextBtn.click();
    });

    // Init
    renderAll();
  </script>
</body>
</html>
