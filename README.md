<!doctype html>
<html lang="de"><head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Einfache Rezept-Sammlung (Baked)</title>
<style>
  :root{
    --bg:#f7f7f8;
    --panel:#ffffff;
    --text:#111827;
    --muted:#6b7280;
    --border:#e5e7eb;
    --accent:#2563eb;
    --radius:12px;
  }

  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0;
    background:var(--bg);
    color:var(--text);
    font:15px/1.5 system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;
  }

  .wrap{ max-width:900px; margin:auto; padding:20px 16px 28px; display:grid; gap:14px }

  .top{ position:sticky; top:0; z-index:2; background:linear-gradient(180deg,var(--bg) 85%,transparent); padding-top:4px; padding-bottom:8px }
  #q{ width:100%; padding:12px 14px; border-radius:var(--radius); border:1px solid var(--border); background:#fff; color:var(--text) }
  #q::placeholder{color:#9ca3af}
  #q:focus{ outline:2px solid var(--accent); outline-offset:2px }

  /* Kategorie-Leiste */
  .catbar{
    display:flex; gap:8px; flex-wrap:wrap; margin-top:8px
  }
  .catbtn{
    border:1px solid var(--border);
    background:#fff;
    color:var(--muted);
    border-radius:999px;
    padding:6px 10px;
    font-weight:600;
    cursor:pointer;
    transition: box-shadow .15s ease, border-color .12s ease, background .12s ease, color .12s ease;
    user-select:none;
  }
  .catbtn:hover{ box-shadow:0 4px 10px rgba(15,23,42,.08) }
  .catbtn.selected{
    background:var(--accent);
    color:#fff;
    border-color:transparent;
  }

  .list{ display:grid; gap:10px; margin-top:4px }
  .item{
    border:1px solid var(--border);
    border-radius:var(--radius);
    background:var(--panel);
    overflow:hidden;
    transition: border-color .12s ease, box-shadow .15s ease;
  }
  .item:hover{
    border-color:#d1d5db;
    box-shadow:0 6px 14px rgba(15,23,42,.08);
  }

  .title{
    width:100%; text-align:left; padding:12px 14px; cursor:pointer; background:transparent; color:var(--text); border:0; display:flex; gap:12px; align-items:center; justify-content:space-between; font-weight:600
  }
  .title:focus{ outline:2px solid var(--accent); outline-offset:2px; border-radius:calc(var(--radius) - 2px) }

  .left{ display:flex; gap:10px; align-items:center }
  .chev{ color:#9ca3af; transition:transform .15s ease, color .12s ease; font-size:12px }
  .item.open .chev{ transform:rotate(90deg); color:#6b7280 }

  .pill{ font-size:12px; padding:4px 8px; border:1px solid var(--border); border-radius:999px; color:var(--muted); background:#f3f4f6; white-space:nowrap }

  .content{ display:none; padding:12px 14px 14px; border-top:1px solid var(--border); white-space:pre-wrap; background:#fff }
  .item.open .content{ display:block }

  .empty{ color:var(--muted); text-align:center; padding:20px 12px }
  .empty .pill{ margin:4px }

  .new{ display:grid; gap:10px; border:1px dashed var(--border); border-radius:var(--radius); padding:12px; margin-top:6px; background:#fff }
  #newSection{ display:none }
  .new input,.new textarea{ width:100%; padding:10px 12px; border-radius:10px; border:1px solid var(--border); background:#fff; color:var(--text) }
  .new textarea{ min-height:110px; resize:vertical }

  .btn{ padding:9px 11px; border:1px solid var(--border); background:#ffffff; color:#111827; border-radius:10px; cursor:pointer; font-weight:600; transition: box-shadow .15s ease }
  .btn:hover{ box-shadow:0 4px 10px rgba(15,23,42,.08) }

  #toggleNewBtn{ margin-top:6px; text-align:center; background:var(--accent); color:#fff; border:none; border-radius:12px; font-weight:700; padding:11px 16px; cursor:pointer; transition: box-shadow .15s ease }
  #toggleNewBtn:hover{ box-shadow:0 8px 20px rgba(37,99,235,.3) }

  @media (max-width:520px){ .wrap{padding:16px 12px} }

  @media (prefers-color-scheme: dark){
    :root{ --bg:#0f1220; --panel:#0f172a; --text:#e5e7eb; --muted:#a1a1aa; --border:#1f273a; --accent:#3b82f6; }
    #q, .new, .content{ background:var(--panel) }
    .pill{ background:#111827; border-color:#1f273a }
    .btn{ background:#0f172a; color:var(--text) }
    .btn:hover{ box-shadow:0 6px 14px rgba(0,0,0,.35) }
    .catbtn{ background:#0f172a; color:#a1a1aa }
    .catbtn.selected{ background:var(--accent); color:#fff; border-color:transparent }
  }
</style>
</head>
<body>
  <div class="wrap">
    <div class="top">
      <input id="q" list="suggest" placeholder="Suche in Rezeptnamen, Texten &amp; Kategorien …" autocomplete="off" aria-label="Suche">
      <datalist id="suggest"><option value="🌶️ Chili con Carne"></option><option value="🍇 Stachelbeertorte (nach Oma Wüst)"></option><option value="🍎 Gedeckte Apfeltorte"></option><option value="🍒 Johannisbeerkuchen"></option><option value="🍝 Bandnudeln mit Spinat-Sahne"></option><option value="🍫 Marmorkuchen"></option><option value="🍮 Käsekuchen Opa"></option><option value="🍰 Buttermilchschnitten"></option><option value="🍰 Streuselkuchen"></option><option value="🥒 Römische Zucchini"></option><option value="🥕 Kohlrabi in Kresse-Creme"></option><option value="🥣 Hackfleisch-Sauerkrautsuppe"></option><option value="🥦 Grüne Bohnen mit Knoblauch"></option><option value="🥪 Partybrötchen"></option><option value="Beilage"></option><option value="Hauptgericht"></option><option value="Kuchen und Torten"></option><option value="Snack"></option><option value="Suppe"></option></datalist>

      <!-- Kategorie-Leiste -->
      <div id="cats" class="catbar" aria-label="Kategorien"><button class="catbtn " data-cat="">Alle</button><button class="catbtn " data-cat="Beilage">Beilage</button><button class="catbtn " data-cat="Hauptgericht">Hauptgericht</button><button class="catbtn " data-cat="Kuchen und Torten">Kuchen und Torten</button><button class="catbtn " data-cat="Snack">Snack</button><button class="catbtn " data-cat="Suppe">Suppe</button></div>
    </div>

    <div class="list" id="list"><div class="empty">Bitte eine Kategorie auswählen (oder Suchbegriff eingeben).</div></div>

    <button id="toggleNewBtn">+ Neues Rezept hinzufügen</button>

    <section class="new" id="newSection" aria-labelledby="newTitle">
      <strong id="newTitle">Neues Rezept</strong>
      <input id="newT" placeholder="Rezeptname (Titel)">
      <input id="newCat" list="catList" placeholder="Kategorie (z. B. Hauptgericht)">
      <datalist id="catList">
        <option>Hauptgericht</option>
        <option>Vorspeise</option>
        <option>Dessert</option>
        <option>Beilage</option>
        <option>Frühstück</option>
        <option>Snack</option>
        <option>Suppe</option>
        <option>Salat</option>
        <option>Kuchen und Torten</option>
      </datalist>
      <textarea id="newC" placeholder="Zutaten und Zubereitung …"></textarea>
      <div style="display:flex; gap:8px; justify-content:flex-end">
        <button id="addBtn" class="btn">Hinzufügen</button>
      </div>

      <!-- Utility-Buttons -->
      <div style="display:flex; gap:8px; flex-wrap:wrap; margin-top:8px">
        <button id="importBtn" class="btn" title="JSON-Datei auswählen &amp; mergen">Rezepte importieren (JSON)</button>
        <input id="importFile" type="file" accept="application/json,.json" style="display:none">
        <button id="exportBtn" class="btn" title="Aktuellen Stand als JSON herunterladen">Rezepte exportieren (JSON)</button>
        <button id="resetBtn" class="btn" title="Lokalen Speicher löschen &amp; eingebetteten Stand laden">Auf EMBEDDED zurücksetzen</button>
        <button id="bakeBtn" class="btn" title="Erzeugt eine neue HTML-Datei mit eingebetteten Rezepten">Baked-HTML herunterladen</button>
      </div>
    </section>
  </div>

<script>
(function(){
  const KEY = 'simpleRecipes.baked.v3';
  const $ = id => document.getElementById(id);

  let notes = migrate(load());

  // Suche + Kategorie-Status
  let query = '';
  // null = nichts gewählt (zeigt ohne Suchtext nichts), '' = „Alle“, sonst Kategoriename
  let selectedCat = null;

  const qEl = $('q'), listEl = $('list'), catsEl = $('cats');
  const suggestEl = $('suggest');
  const newT = $('newT'), newC = $('newC'), newCat = $('newCat'), addBtn = $('addBtn');
  const toggleBtn = $('toggleNewBtn'), newSection = $('newSection');

  // --- Storage & Seeds (Baked) ---
  function load(){
    const EMBEDDED = /*__EMBED_START__*/
[
  {
    "id": "oxd8eitfcv",
    "title": "🍰 Streuselkuchen",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 30 Minuten\n• Gehzeit: ca. 30 Minuten\n• Backzeit: ca. 30 Minuten\n• Gesamt: ca. 1½ Stunden\n\n🍽️ Portionen\nFür 1 Blech\n\n🧂 Zutaten\nHefeteig:\n• 1 Würfel Hefe\n• 500 g Mehl\n• ¼ l Milch\n• 125 g Margarine\n• 125 g Zucker\n• 1 Prise Salz\n• 1 Ei\nStreusel:\n• 200 g Mehl\n• 200 g Zucker\n• 100 g Mondamin (oder Mehl)\n• 200 g Butter\n• 1 Prise Salz, 1 Prise Zimt\n\n👩‍🍳 Zubereitung\n\t1. Mehl in Schüssel geben, Vertiefung formen. Hefe in Milch mit Zucker auflösen, hineingeben, 15 Minuten gehen lassen.\n\t2. Restliche Zutaten einarbeiten, 15 Minuten gehen lassen.\n\t3. Streuselzutaten verkneten.\n\t4. Teig auf Blech ausrollen, ggf. mit Obst belegen, Streusel darüber.\n\t5. Bei 180 °C ca. 30 Minuten backen.\n",
    "cat": "Kuchen und Torten",
    "updated": 1760177791083
  },
  {
    "id": "585k8ql9w2n",
    "title": "🍇 Stachelbeertorte (nach Oma Wüst)",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 45 Minuten\n• Backzeit: ca. 30 Minuten\n• Kühlzeit: ca. 1 Stunde\n• Gesamt: ca. 2 Stunden 15 Minuten\n\n🍽️ Portionen\nFür 1 Torte (26 cm Ø)\n\n🧂 Zutaten\nBoden:\n• 100 g Butter\n• 100 g Zucker\n• 1 Päckchen Vanillezucker\n• 4 Eigelb\n• 1 TL Backpulver\n• 125 g Mehl\nDeckel:\n• 4 Eiweiß\n• 150 g Zucker\n• 100 g gehobelte Mandeln\nFüllung:\n• 330 g Stachelbeeren (Glas)\n• 1 Tortenguss klar\n• 500 ml Sahne\n• 2 Päckchen Vanillezucker\n• 2 Päckchen Sahnesteif\n\n👩‍🍳 Zubereitung\n\t1. Butter, Zucker, Vanillezucker cremig rühren, Eigelb zugeben, Mehl und Backpulver einarbeiten.\n\t2. Auf 2 Formen verteilen.\n\t3. Eiweiß mit Zucker steif schlagen, aufstreichen, Mandeln daraufgeben.\n\t4. Bei 175 °C ca. 30 Minuten backen.\n\t5. Einen Boden mit Stachelbeeren und Tortenguss belegen, Sahne aufschlagen und daraufgeben.\nZweiten Boden in Stücke schneiden und als Deckel auflegen.",
    "cat": "Kuchen und Torten",
    "updated": 1760177691834
  },
  {
    "id": "xlgziq267u",
    "title": "🍫 Marmorkuchen",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 20 Minuten\n• Backzeit: ca. 60 Minuten\n• Gesamt: ca. 1 Stunde 20 Minuten\n\n🍽️ Portionen\nFür 1 Gugelhupfform\n\n🧂 Zutaten\n• 250 g Butter\n• 250 g Zucker\n• 4 Eier\n• 350 g Mehl\n• 1 Päckchen Backpulver\n• 1 Päckchen Vanillezucker\n• 1 EL Rum\n• 250 ml Milch\n• 3 EL Kakao\n• Puderzucker\n\n👩‍🍳 Zubereitung\n\t1. Butter, Zucker, Vanillezucker und Rum schaumig rühren.\n\t2. Eier einzeln zugeben, Mehl und Backpulver mit Milch abwechselnd einrühren.\n\t3. Teig halbieren, eine Hälfte mit Kakao mischen.\n\t4. Hellen und dunklen Teig abwechselnd in Form geben, marmorieren.\n\t5. Bei 175 °C ca. 60 Minuten backen, abkühlen lassen, mit Puderzucker bestreuen.\n",
    "cat": "Kuchen und Torten",
    "updated": 1760177635129
  },
  {
    "id": "rn2ef1m5zg",
    "title": "🍒 Johannisbeerkuchen",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 25 Minuten\n• Backzeit: ca. 30 Minuten\n• Gesamt: ca. 55 Minuten\n\n🍽️ Portionen\nFür 1 Torte\n\n🧂 Zutaten\nBoden:\n• 4 Eier\n• 125 g Zucker\n• 180 g Mehl\n• 9 EL Öl\n• ½ Päckchen Backpulver\nBelag:\n• Johannisbeeren nach Belieben\n• 2 Becher Crème fraîche\n• 1 Päckchen Vanillezucker\n• 2 Beutel Sahnesteif\n• 60 g Puderzucker\n\n👩‍🍳 Zubereitung\n\t1. Teigzutaten verrühren, in gefettete Form geben.\n\t2. Bei 175 °C ca. 30 Minuten backen, abkühlen lassen.\n\t3. Crème fraîche mit Vanillezucker, Sahnesteif, Puderzucker verrühren.\nJohannisbeeren unterheben und auf dem Boden verteilen.",
    "cat": "Kuchen und Torten",
    "updated": 1760177583660
  },
  {
    "id": "5zrfmr03cbx",
    "title": "🍮 Käsekuchen Opa",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 25 Minuten\n• Kühlzeit: ca. 1 Stunde\n• Backzeit: ca. 50–60 Minuten\n• Gesamt: ca. 2½ Stunden\n\n🍽️ Portionen\nFür eine Springform (26 cm Ø)\n\n🧂 Zutaten\nTeig:\n• 250 g Mehl\n• 125 g Butter\n• 30 g Zucker\n• 1 Eigelb\n• 1 Messerspitze Salz\n• 2 EL Wasser\nFüllung:\n• 750 g Quark (halb Mager-, halb Vollfettquark)\n• ½ Tasse Öl\n• 300 g Zucker\n• 3 Eigelb\n• 40 g Speisestärke\n• 1 Päckchen Vanillezucker\n• ⅛ l Milch\n• 3–4 Eiweiß\n\n👩‍🍳 Zubereitung\n\t1. Teigzutaten verkneten, 1 Stunde kalt stellen.\n\t2. Quarkmasse anrühren, Eiweiß steif schlagen und unterheben.\n\t3. Teig ausrollen, Form auskleiden, Füllung einfüllen.\n\t4. Bei 180 °C ca. 50–60 Minuten backen.\nIm ausgeschalteten Ofen abkühlen lassen.",
    "cat": "Kuchen und Torten",
    "updated": 1760177544114
  },
  {
    "id": "flo46e68pws",
    "title": "🍰 Buttermilchschnitten",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 20 Minuten\n• Backzeit: ca. 20 Minuten\n• Gesamt: ca. 40 Minuten\n\n🍽️ Portionen\nFür 1 Blech\n\n🧂 Zutaten\nTeig:\n• 3 Eier\n• 3 Tassen Zucker (nach Geschmack reduzieren)\n• 1 Päckchen Vanillezucker\n• 4 Tassen Mehl\n• 1 Päckchen Backpulver\n• 2 Tassen Buttermilch\nBelag:\n• 2 Tassen Kokosflocken\n• ½ Tasse Zucker\nGuss:\n• 200 g Sahne\n• 150 g Butter\n\n👩‍🍳 Zubereitung\n\t1. Eier, Zucker, Vanillezucker verrühren. Mehl, Backpulver, Buttermilch zugeben.\n\t2. Auf Blech geben, mit Kokos-Zucker-Mischung bestreuen.\n\t3. Bei 180 °C ca. 20 Minuten backen.\nGuss aus Sahne und Butter kochen und über den heißen Kuchen gießen.",
    "cat": "Kuchen und Torten",
    "updated": 1760177489675
  },
  {
    "id": "hv1wk5872oj",
    "title": "🍎 Gedeckte Apfeltorte",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 25 Minuten\n• Backzeit: ca. 70 Minuten\n• Gesamt: ca. 1 Stunde 35 Minuten\n\n🍽️ Portionen\nFür eine Springform (26 cm Ø)\n\n🧂 Zutaten\nTeig:\n• 150 g Margarine\n• 150 g Zucker\n• 1 Ei\n• 2 TL Backpulver\n• 1 Päckchen Vanillezucker\n• 300 g Mehl\nFüllung:\n• ca. 1 kg Äpfel\n• 1 Prise Zimt\n\n👩‍🍳 Zubereitung\n\t1. Äpfel schälen, entkernen, würfeln und mit Zimt mischen.\n\t2. Zutaten für den Teig verkneten.\n\t3. ⅔ Teig in Springform geben, Boden & Rand formen.\n\t4. Äpfel einfüllen, restlichen Teig ausrollen und als Deckel auflegen.\nBei 175 °C Umluft ca. 70 Minuten backen.",
    "cat": "Kuchen und Torten",
    "updated": 1760177446330
  },
  {
    "id": "sem5kah1b7h",
    "title": "🥪 Partybrötchen",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 10 Minuten\n• Backzeit: ca. 15 Minuten\n• Gesamt: ca. 25 Minuten\n\n🍽️ Portionen\n6 Brötchenhälften\n\n🧂 Zutaten\n• 1 Packung Brötchen (6 Stück)\n• 2 Becher Schmand\n• 1 Tüte geriebener Käse\n• Belag nach Geschmack: Salami, Schinken, Pilze, Ananas, Paprika, Zwiebeln\n\n👩‍🍳 Zubereitung\n\t1. Schmand mit Käse und Zutaten mischen.\n\t2. Auf Brötchenhälften streichen.\nBei 180 °C ca. 15 Minuten goldbraun backen.",
    "cat": "Snack",
    "updated": 1760177371002
  },
  {
    "id": "9dbh70u6afj",
    "title": "🥕 Kohlrabi in Kresse-Creme",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 20 Minuten\n• Kochzeit: ca. 10 Minuten\n• Gesamt: ca. 30 Minuten\n\n🍽️ Portionen\nFür 4 Personen\n\n🧂 Zutaten\n• 1 kg Kohlrabi (mit Herzblättern)\n• 150 g Crème fraîche\n• 3 EL Kresse\n• Salz, Pfeffer, Muskat\n• Etwas Zitronensaft\n\n👩‍🍳 Zubereitung\n\t1. Kohlrabi schälen, in Stifte schneiden. Herzblätter fein schneiden.\n\t2. In Salzwasser 8–10 Minuten garen, abgießen.\n\t3. Crème fraîche erhitzen, Kresse und Gewürze einrühren.\n\t4. Kohlrabi hinzufügen, abschmecken und servieren.\n",
    "cat": "Beilage",
    "updated": 1760177320203
  },
  {
    "id": "enl1ev4fogb",
    "title": "🥦 Grüne Bohnen mit Knoblauch",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 10 Minuten\n• Kochzeit: ca. 20 Minuten\n• Gesamt: ca. 30 Minuten\n\n🍽️ Portionen\nFür 4 Personen\n\n🧂 Zutaten\n• 750 g grüne Bohnen\n• 150 g Crème fraîche\n• 2 Knoblauchzehen\n• 1 EL Petersilie\n• Salz und Pfeffer\n\n👩‍🍳 Zubereitung\n\t1. Bohnen abfädeln, waschen, in Stücke schneiden und 15 Minuten in Salzwasser garen.\n\t2. Crème fraîche erhitzen, Knoblauch pressen, Petersilie zufügen.\n\t3. Mit Salz und Pfeffer würzen, Bohnen untermengen und kurz erhitzen.\n",
    "cat": "Beilage",
    "updated": 1760177285939
  },
  {
    "id": "j7nk6msqtg",
    "title": "🥣 Hackfleisch-Sauerkrautsuppe",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 20 Minuten\n• Kochzeit: ca. 60–90 Minuten\n• Gesamt: ca. 1 Stunde 30 Minuten\n\n🍽️ Portionen\nFür 4 Personen\n\n🧂 Zutaten\nFür die Suppe:\n• 2 große Zwiebeln\n• 250 g Hackfleisch\n• 2–3 Gewürzgurken\n• 3 gehäufte EL Sauerkraut\n• 3 EL Tomatenmark\n• 1 Liter Gemüse- oder Fleischbrühe\n• Salz und Pfeffer\n• Petersilie oder Schnittlauch zum Verfeinern\nFür den Dip:\n• ½ Becher saure Sahne\n• 2–3 EL Mayonnaise\n• 1–2 Knoblauchzehen\n• 1 TL Senf\n• Salz und Pfeffer\n\n👩‍🍳 Zubereitung\n\t1. Zwiebeln und Hackfleisch in einem Topf anbraten. Mit Brühe ablöschen und aufkochen.\n\t2. Gewürzgurken, Tomatenmark und Sauerkraut hinzufügen. Ca. 1–2 Stunden köcheln lassen.\n\t3. Mit Salz, Pfeffer und Kräutern abschmecken.\n\t4. Für den Dip saure Sahne, Mayonnaise, Knoblauch und Senf verrühren. Mit Salz und Pfeffer würzen und zur Suppe servieren.\n",
    "cat": "Suppe",
    "updated": 1760177236577
  },
  {
    "id": "rfxet4dtpmq",
    "title": "🍝 Bandnudeln mit Spinat-Sahne",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 25 Minuten\n• Gesamt: ca. 30 Minuten\n\n🍽️ Portionen\nFür 3 Portionen\n\n🧂 Zutaten\n• 500 g Blattspinat (frisch oder TK)\n• 1 kleine Zwiebel\n• 1 Knoblauchzehe\n• 400 g Bandnudeln\n• 1 EL Öl\n• 1 EL Pinienkerne (optional)\n• 200 g Sahne\n• Salz und Pfeffer\n• 2 EL Parmesan\n\n👩‍🍳 Zubereitung\n\t1. Spinat putzen. Nudeln in Salzwasser kochen.\n\t2. Zwiebel und Knoblauch in Öl glasig dünsten.\n\t3. Spinat und Pinienkerne zugeben, kurz mitdünsten.\n\t4. Sahne hinzufügen, würzen und cremig einkochen.\nNudeln abgießen, unterheben, mit Parmesan servieren.",
    "cat": "Hauptgericht",
    "updated": 1760177196326
  },
  {
    "id": "l5p05ejgrks",
    "title": "🌶️ Chili con Carne",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 20 Minuten\n• Kochzeit: ca. 40 Minuten\n• Gesamt: ca. 1 Stunde\n\n🍽️ Portionen\nFür 4 Personen\n\n🧂 Zutaten\n• 500 g Hackfleisch\n• 500 ml passierte Tomaten\n• 2 rote Paprika\n• 2 große Zwiebeln\n• 1 Dose Mais\n• 2 Dosen Kidneybohnen\n• 1 Packung Chili-Gewürzmischung\n• Salz, Pfeffer, Zucker oder Ketchup\n• Öl zum Braten\n\n👩‍🍳 Zubereitung\n\t1. Hackfleisch in Öl anbraten.\n\t2. Zwiebeln und Paprika zufügen, würzen.\n\t3. Tomaten, Bohnen und Gewürze zugeben, 30–40 Minuten köcheln lassen.\nMit Zucker oder Ketchup abschmecken, Mais kurz unterrühren.",
    "cat": "Hauptgericht",
    "updated": 1760177123593
  },
  {
    "id": "alv69y4hz5w",
    "title": "🥒 Römische Zucchini",
    "content": "⏱️ Zubereitungszeit\n• Aktive Zeit: ca. 25 Minuten\n• Backzeit: ca. 25 Minuten\n• Gesamt: ca. 50 Minuten\n\n🍽️ Portionen\nFür 2–3 Personen\n\n🧂 Zutaten\n• 50 g Speckwürfel\n• 1 EL Öl\n• 1 Zwiebel\n• 1 Knoblauchzehe\n• 500 g Tomatensoße\n• 1 EL Oregano\n• Salz und Pfeffer\n• 500 g Zucchini\n• 2 EL Semmelmehl\n• 4–5 EL gehackte Kräuter (Petersilie, Oregano, Rosmarin)\n• 40 g Parmesan\n• 6 EL Sahne oder Crème fraîche\n\n👩‍🍳 Zubereitung\n\t1. Speck in Öl anbraten, Zwiebel und Knoblauch zufügen und kurz andünsten.\n\t2. Tomatensoße, Oregano, Salz und Pfeffer zugeben, einköcheln lassen, in eine Auflaufform füllen.\n\t3. Zucchini längs halbieren, leicht salzen.\n\t4. Semmelmehl, Kräuter, Parmesan und Sahne zu einer Paste verrühren und auf die Zucchini streichen.\n\t5. In der Soße bei 230 °C ca. 25 Minuten backen.\n",
    "cat": "Hauptgericht",
    "updated": 1760176576342
  }
]
/*__EMBED_END__*/;

    try{
      const raw = localStorage.getItem(KEY);
      if(!raw) return EMBEDDED;
      const arr = JSON.parse(raw);
      return Array.isArray(arr) ? arr : EMBEDDED;
    }catch(e){ console.warn(e); return EMBEDDED; }
  }

  function save(){
    localStorage.setItem(KEY, JSON.stringify(notes));
    refreshSuggestions();
    buildCategoryBar();
    render();
  }

  function mk(title, content, cat){
    return { id: Math.random().toString(36).slice(2), title: String(title||'Ohne Titel'), content: String(content||''), cat: String(cat||'Unkategorisiert'), updated: Date.now() };
  }

  function migrate(arr){
    return (arr||[]).map(n => ({
      id: n.id || Math.random().toString(36).slice(2),
      title: String(n.title||'Ohne Titel'),
      content: String(n.content||''),
      cat: n.cat ? String(n.cat) : 'Unkategorisiert',
      updated: Number(n.updated || Date.now())
    }));
  }

  // --- Vorschläge füllen (Titel + Kategorien) ---
  function refreshSuggestions(){
    const titleSet = new Set(notes.map(n => n.title).filter(Boolean));
    const catSet   = new Set(notes.map(n => n.cat || 'Unkategorisiert'));
    const options = Array.from(new Set([...titleSet, ...catSet]))
      .sort((a,b)=>a.localeCompare(b,'de',{sensitivity:'base'}));
    suggestEl.innerHTML = options.map(v => `<option value="${escapeAttr(v)}"></option>`).join('');
  }

  // Merge-Helfer (für Import & optionales Laden)
  function mergeIncoming(fileArr){
    const incoming = migrate(fileArr || []);
    const key = r => (r.title||'').trim().toLowerCase()+'|'+(r.cat||'').trim().toLowerCase();
    const map = new Map(notes.map(r => [key(r), r]));
    for(const r of incoming){
      const k = key(r);
      if(!map.has(k)){
        map.set(k, {...r, id: r.id || Math.random().toString(36).slice(2), updated: r.updated || Date.now()});
      }
    }
    notes = Array.from(map.values()).sort((a,b)=>b.updated - a.updated);
    save();
  }

  // --- Kategorie-Leiste ---
  function buildCategoryBar(){
    const cats = Array.from(new Set(notes.map(n => n.cat || 'Unkategorisiert')))
      .sort((a,b)=>a.localeCompare(b,'de',{sensitivity:'base'}));
    const allBtn = `<button class="catbtn ${selectedCat===''? 'selected':''}" data-cat="">Alle</button>`;
    const catBtns = cats.map(c =>
      `<button class="catbtn ${selectedCat===c?'selected':''}" data-cat="${escapeAttr(c)}">${escapeHtml(c)}</button>`
    ).join('');
    catsEl.innerHTML = allBtn + catBtns;
  }

  catsEl.addEventListener('click', (e)=>{
    const btn = e.target.closest('.catbtn');
    if(!btn) return;
    const clicked = btn.getAttribute('data-cat'); // '' für Alle, sonst Kategoriename
    selectedCat = (clicked === selectedCat) ? null : clicked; // erneuter Klick -> abwählen
    buildCategoryBar();
    render();
  });

  // --- Render (mit Suche-zeigt-auch-ohne-Kategorie) ---
  function render(){
    const q = query.trim().toLowerCase();

    // Nichts ausgewählt + keine Suche => nichts anzeigen (Hinweis)
    if (selectedCat === null && q === '') {
      listEl.innerHTML = `<div class="empty">Bitte eine Kategorie auswählen (oder Suchbegriff eingeben).</div>`;
      return;
    }

    const list = notes
      .slice()
      .sort((a,b)=>b.updated - a.updated)
      .filter(n => {
        const matchesQuery = q === '' ? true : (
          n.title.toLowerCase().includes(q) ||
          n.content.toLowerCase().includes(q) ||
          (n.cat||'').toLowerCase().includes(q)
        );
        // Kategorie aktiv? (null = keine, '' = Alle)
        const catActive = (selectedCat !== null && selectedCat !== '');
        const matchesCat = catActive ? (n.cat === selectedCat) : true;
        return matchesQuery && matchesCat;
      });

    listEl.innerHTML = '';

    if(list.length===0){
      listEl.innerHTML = `<div class="empty">Keine Treffer.</div>`;
      return;
    }

    for(const n of list){
      const item = document.createElement('div');
      item.className = 'item';

      // NEU: Gesamtzeit aus dem Inhalt parsen
      const totalTime = getTotalTime(n.content);

      item.innerHTML = `
        <button class="title" aria-expanded="false">
          <span class="left">
            <span class="chev">▶</span>
            <strong>${escapeHtml(n.title||'Ohne Titel')}</strong>
          </span>
          <span style="display:flex; gap:8px; align-items:center">
            ${ totalTime ? `<span class="pill" title="Gesamtzeit">⏱ ${escapeHtml(totalTime)}</span>` : '' }
            <span class="pill" title="Kategorie">${escapeHtml(n.cat||'Unkategorisiert')}</span>
          </span>
        </button>
        <div class="content">${escapeHtml(n.content).replace(/\n/g,'<br>')}</div>
      `;
      const btn = item.querySelector('.title');
      btn.addEventListener('click', ()=>{
        const open = item.classList.toggle('open');
        btn.setAttribute('aria-expanded', String(open));
      });
      listEl.appendChild(item);
    }
  }

  // --- Utils ---
  function escapeHtml(s=''){ return s.replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
  function escapeAttr(s=''){ return String(s).replace(/"/g,'&quot;'); }

  // NEU: Zeit aus "Gesamt:" oder "Gesammt:" Zeile lesen
  function getTotalTime(text=''){
    const m = String(text).match(/^\s*(?:Gesamt|Gesammt)\s*:\s*(.+)$/im);
    return m ? m[1].trim() : null; // z.B. "45 Min", "1:15 h", "1 h 30 min"
  }

  // --- Events ---
  qEl.addEventListener('input', e=>{ query = e.target.value; render(); });
  qEl.addEventListener('keydown', e=>{ if(e.key === 'Enter'){ query = qEl.value; render(); } });

  addBtn.addEventListener('click', ()=>{
    const t = newT.value.trim();
    const c = newC.value;
    const cat = (newCat.value || 'Unkategorisiert').trim();
    if(!t && !c) return;
    notes.unshift(mk(t, c, cat));
    newT.value=''; newC.value=''; newCat.value='';
    save();

    if(newSection.style.display !== 'none'){
      newSection.style.display = 'none';
      toggleBtn.textContent = '+ Neues Rezept hinzufügen';
    }
  });

  toggleBtn.addEventListener('click', ()=>{
    const isHidden = newSection.style.display === 'none' || !newSection.style.display;
    newSection.style.display = isHidden ? 'grid' : 'none';
    toggleBtn.textContent = isHidden ? '– Formular ausblenden' : '+ Neues Rezept hinzufügen';
  });

  // --- Import (Datei auswählen & mergen) ---
  $('importBtn').addEventListener('click', ()=> $('importFile').click());
  $('importFile').addEventListener('change', async (e)=>{
    const file = e.target.files && e.target.files[0];
    if(!file) return;
    try{
      const text = await file.text();
      const json = JSON.parse(text);
      if(!Array.isArray(json)) throw new Error('Datei ist kein Array von Rezepten.');
      mergeIncoming(json);
    }catch(err){
      alert('Import fehlgeschlagen: '+err.message);
      console.error(err);
    }finally{
      e.target.value = '';
    }
  });

  // --- Export: aktuellen Stand als JSON herunterladen ---
  $('exportBtn').addEventListener('click', () => {
    const blob = new Blob([JSON.stringify(notes, null, 2)], {type:'application/json'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'recipes.json';
    a.click();
    URL.revokeObjectURL(url);
  });

  // --- Reset: lokalen Speicher löschen & Seite neu laden (zeigt EMBEDDED) ---
  $('resetBtn').addEventListener('click', () => {
    localStorage.removeItem(KEY);
    location.reload();
  });

  // --- Bake: komplette HTML mit EMBEDDED erzeugen & downloaden ---
  $('bakeBtn').addEventListener('click', () => {
    try{
      let html = '<!doctype html>\n' + document.documentElement.outerHTML;
      const embeddedJson = JSON.stringify(notes, null, 2);
      const embedRegex =
        /(const\s+EMBEDDED\s*=\s*\/\*__EMBED_START__\*\/)([\s\S]*?)(\/\*__EMBED_END__\*\/\s*;?)/;

      if(!embedRegex.test(html)){
        alert('EMBEDDED-Marker nicht gefunden. Bitte Funktion load() prüfen.');
        return;
      }
      html = html.replace(
        embedRegex,
        (_, start, _old, end) => `${start}\n${embeddedJson}\n${end}`
      );

      html = html.replace(
        /(const\s+KEY\s*=\s*['"])([^'"]*?\.baked\.v)(\d+)(['"]\s*;)/,
        (m, p1, base, num, p4) => p1 + base + (Number(num)+1) + p4
      );

      const blob = new Blob([html], {type:'text/html'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'rezepte_baked.html';
      a.click();
      URL.revokeObjectURL(url);
    }catch(err){
      console.error(err);
      alert('Konnte Baked-HTML nicht erzeugen. Siehe Konsole.');
    }
  });

  // --- Start ---
  refreshSuggestions();
  buildCategoryBar();
  render();
})();
</script>



</body></html>
