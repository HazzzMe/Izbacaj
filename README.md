<!DOCTYPE html>
<html lang="da">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Storskrald – Afhentningsoversigt 2026</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:wght@300;400;500;600&display=swap');

  :root {
    --green: #1a6b3c;
    --green-light: #2d8a52;
    --green-pale: #e8f5ee;
    --amber: #e07b2a;
    --amber-light: #fef3e8;
    --dark: #1a2018;
    --mid: #4a5240;
    --light: #f4f7f2;
    --white: #ffffff;
    --border: #d4dfd0;
    --shadow: 0 2px 16px rgba(26,107,60,0.10);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--light);
    color: var(--dark);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  header {
    background: var(--green);
    color: var(--white);
    padding: 18px 32px;
    display: flex;
    align-items: center;
    gap: 16px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.15);
  }

  header .logo {
    font-family: 'DM Serif Display', serif;
    font-size: 1.5rem;
    letter-spacing: -0.5px;
  }

  header .logo span {
    color: #7edb9e;
  }

  header .subtitle {
    font-size: 0.8rem;
    opacity: 0.75;
    font-weight: 300;
    margin-top: 1px;
  }

  .app {
    display: flex;
    flex: 1;
    height: calc(100vh - 68px);
  }

  /* SIDEBAR */
  .sidebar {
    width: 380px;
    min-width: 320px;
    background: var(--white);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }

  .controls {
    padding: 20px;
    border-bottom: 1px solid var(--border);
    background: var(--white);
  }

  .controls label {
    display: block;
    font-size: 0.72rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--mid);
    margin-bottom: 6px;
  }

  .date-row {
    display: flex;
    gap: 8px;
    align-items: center;
    margin-bottom: 12px;
  }

  input[type="date"] {
    flex: 1;
    padding: 10px 12px;
    border: 1.5px solid var(--border);
    border-radius: 8px;
    font-size: 0.95rem;
    font-family: 'DM Sans', sans-serif;
    color: var(--dark);
    background: var(--light);
    outline: none;
    transition: border-color 0.2s;
  }

  input[type="date"]:focus {
    border-color: var(--green);
  }

  .btn {
    padding: 10px 16px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    font-weight: 600;
    font-size: 0.88rem;
    transition: all 0.15s;
  }

  .btn-primary {
    background: var(--green);
    color: var(--white);
  }

  .btn-primary:hover { background: var(--green-light); }

  .btn-today {
    background: var(--amber-light);
    color: var(--amber);
    border: 1.5px solid #f0c49a;
    font-size: 0.8rem;
    padding: 8px 12px;
  }

  .btn-today:hover { background: #fde8d0; }

  .stats-bar {
    display: flex;
    gap: 0;
    border-top: 1px solid var(--border);
    padding-top: 12px;
    margin-top: 0;
  }

  .stat {
    flex: 1;
    text-align: center;
    padding: 6px 0;
  }

  .stat:not(:last-child) {
    border-right: 1px solid var(--border);
  }

  .stat .num {
    font-family: 'DM Serif Display', serif;
    font-size: 1.6rem;
    color: var(--green);
    line-height: 1;
  }

  .stat .lbl {
    font-size: 0.68rem;
    color: var(--mid);
    text-transform: uppercase;
    letter-spacing: 0.07em;
    margin-top: 2px;
  }

  /* Address list */
  .addr-list {
    flex: 1;
    overflow-y: auto;
    padding: 0;
  }

  .addr-list::-webkit-scrollbar { width: 4px; }
  .addr-list::-webkit-scrollbar-track { background: transparent; }
  .addr-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

  .addr-item {
    padding: 14px 20px;
    border-bottom: 1px solid var(--border);
    cursor: pointer;
    transition: background 0.12s;
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }

  .addr-item:hover { background: var(--green-pale); }
  .addr-item.active { background: var(--green-pale); border-left: 3px solid var(--green); }

  .addr-num {
    width: 24px;
    height: 24px;
    min-width: 24px;
    background: var(--green);
    color: var(--white);
    border-radius: 50%;
    font-size: 0.7rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 1px;
  }

  .addr-info .name {
    font-weight: 600;
    font-size: 0.92rem;
    color: var(--dark);
  }

  .addr-info .loc {
    font-size: 0.78rem;
    color: var(--mid);
    margin-top: 2px;
  }

  .addr-info .next-date {
    font-size: 0.72rem;
    color: var(--green);
    font-weight: 600;
    margin-top: 4px;
  }

  .no-results {
    padding: 48px 32px;
    text-align: center;
    color: var(--mid);
  }

  .no-results .icon { font-size: 2.5rem; margin-bottom: 12px; }
  .no-results p { font-size: 0.9rem; }

  /* Map */
  #map {
    flex: 1;
    height: 100%;
  }

  /* Info panel in map */
  .info-popup {
    font-family: 'DM Sans', sans-serif;
    min-width: 200px;
    max-width: 260px;
  }

  .info-popup h3 {
    font-family: 'DM Serif Display', serif;
    font-size: 1.05rem;
    color: var(--green);
    margin-bottom: 4px;
  }

  .info-popup .city {
    font-size: 0.8rem;
    color: var(--mid);
    margin-bottom: 8px;
  }

  .info-popup .dates-label {
    font-size: 0.68rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--mid);
    margin-bottom: 4px;
  }

  .info-popup .date-chip {
    display: inline-block;
    background: var(--green-pale);
    color: var(--green);
    border-radius: 4px;
    padding: 2px 7px;
    font-size: 0.75rem;
    font-weight: 600;
    margin: 2px 2px 2px 0;
  }

  .info-popup .date-chip.today-chip {
    background: var(--amber);
    color: var(--white);
  }

  /* Legend */
  .legend {
    position: absolute;
    bottom: 32px;
    right: 16px;
    background: var(--white);
    border-radius: 10px;
    box-shadow: var(--shadow);
    padding: 12px 16px;
    font-size: 0.8rem;
    z-index: 1;
  }

  .legend .legend-title {
    font-weight: 700;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--mid);
    margin-bottom: 8px;
  }

  .legend-item {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 5px;
  }

  .legend-dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
  }

  .dot-today { background: var(--amber); }
  .dot-other { background: var(--green); }
</style>
</head>
<body>

<header>
  <div>
    <div class="logo">Storskrald<span>Kort</span></div>
    <div class="subtitle">Afhentningsoversigt 2026</div>
  </div>
</header>

<div class="app">
  <div class="sidebar">
    <div class="controls">
      <label>Vælg dato</label>
      <div class="date-row">
        <input type="date" id="datePicker" />
        <button class="btn btn-today" onclick="setToday()">I dag</button>
        <button class="btn btn-primary" onclick="filterByDate()">Vis</button>
      </div>
      <div class="stats-bar" id="statsBar" style="display:none;">
        <div class="stat">
          <div class="num" id="statCount">0</div>
          <div class="lbl">Afhentninger</div>
        </div>
        <div class="stat">
          <div class="num" id="statKommuner">0</div>
          <div class="lbl">Kommuner</div>
        </div>
        <div class="stat">
          <div class="num" id="statByer">0</div>
          <div class="lbl">Byer</div>
        </div>
      </div>
    </div>

    <div class="addr-list" id="addrList">
      <div class="no-results">
        <div class="icon">📅</div>
        <p>Vælg en dato for at se<br>hvilke adresser der skal afhentes</p>
      </div>
    </div>
  </div>

  <div style="flex:1;position:relative;">
    <div id="map"></div>
    <div class="legend" id="legend" style="display:none;">
      <div class="legend-title">Forklaring</div>
      <div class="legend-item"><div class="legend-dot dot-today"></div>Valgt dato</div>
      <div class="legend-item"><div class="legend-dot dot-other"></div>Øvrige datoer</div>
    </div>
  </div>
</div>

<script>
const ADDRESSES = [{"address":"Skovalleen 33 B","city":"Bagsværd","kommune":"Gladsaxe","fullAddress":"Skovalleen 33 B, Bagsværd, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-12","2026-08-18","2026-09-15","2026-10-11","2026-10-13"]},{"address":"Skovbrynet 49","city":"Bagsværd","kommune":"Gladsaxe","fullAddress":"Skovbrynet 49, Bagsværd, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-18","2026-09-15"]},{"address":"Skovdiget 1","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Skovdiget 1, Birkerød, Danmark","dates":["2026-01-22","2026-03-09","2026-03-19","2026-05-14","2026-09-07","2026-10-29","2026-12-24"]},{"address":"Lærkebakken 20","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Lærkebakken 20, Birkerød, Danmark","dates":["2026-01-27","2026-03-11","2026-03-24","2026-05-19","2026-07-14","2026-08-08","2026-12-29"]},{"address":"Fyrrebakken 6","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Fyrrebakken 6, Birkerød, Danmark","dates":["2026-01-27","2026-03-11","2026-03-24","2026-05-19","2026-07-14","2026-08-08","2026-12-29"]},{"address":"Carl Plougs Vej 5","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Carl Plougs Vej 5, Birkerød, Danmark","dates":["2026-01-22","2026-03-09","2026-03-19","2026-05-14","2026-09-07","2026-10-29","2026-12-24"]},{"address":"Vestervang 25","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Vestervang 25, Birkerød, Danmark","dates":["2026-02-26","2026-03-12","2026-04-23","2026-06-18","2026-08-10","2026-08-13"]},{"address":"Birkevej 33A","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Birkevej 33A, Birkerød, Danmark","dates":["2026-02-26","2026-03-12","2026-04-23","2026-06-18","2026-08-10","2026-08-13"]},{"address":"Rolighedsvej 31","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Rolighedsvej 31, Birkerød, Danmark","dates":["2026-02-26","2026-03-12","2026-04-23","2026-06-18","2026-08-10","2026-08-13"]},{"address":"Kajerødvej 97","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Kajerødvej 97, Birkerød, Danmark","dates":["2026-01-29","2026-03-26","2026-05-11","2026-05-21","2026-07-16","2026-10-09","2026-12-31"]},{"address":"Nobisvej 9","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Nobisvej 9, Birkerød, Danmark","dates":["2026-01-10","2026-02-19","2026-04-16","2026-06-08","2026-11-06","2026-11-26"]},{"address":"Biskop Svanes Vej 15","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Biskop Svanes Vej 15, Birkerød, Danmark","dates":["2026-01-22","2026-03-09","2026-03-19","2026-05-14","2026-09-07","2026-10-29","2026-12-24"]},{"address":"Traneholmen 19","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Traneholmen 19, Birkerød, Danmark","dates":["2026-01-22","2026-03-09","2026-03-19","2026-05-14","2026-09-07","2026-10-29","2026-12-24"]},{"address":"Storevang 25","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Storevang 25, Birkerød, Danmark","dates":["2026-01-19","2026-03-16","2026-06-07","2026-08-31","2026-10-26","2026-11-05","2026-12-21"]},{"address":"Bøgebakken 5","city":"Birkerød","kommune":"Rudersdal","fullAddress":"Bøgebakken 5, Birkerød, Danmark","dates":["2026-01-27","2026-03-11","2026-03-24","2026-05-19","2026-07-14","2026-08-08","2026-12-29"]},{"address":"Eivindsvej","city":"Charlottenlund","kommune":"Gentofte","fullAddress":"Eivindsvej, Charlottenlund, Danmark","dates":["2026-01-28","2026-02-12","2026-02-25","2026-03-25","2026-04-11","2026-04-22","2026-05-20","2026-06-17","2026-07-10","2026-07-15","2026-09-09","2026-12-08","2026-12-30"]},{"address":"L E Bruuns vej 35","city":"Charlottenlund","kommune":"Gentofte","fullAddress":"L E Bruuns vej 35, Charlottenlund, Danmark","dates":["2026-01-28","2026-02-12","2026-02-25","2026-03-25","2026-04-11","2026-04-22","2026-05-20","2026-06-17","2026-07-10","2026-07-15","2026-09-09","2026-12-08","2026-12-30"]},{"address":"Ingeborgvej 36","city":"Charlottenlund","kommune":"Gentofte","fullAddress":"Ingeborgvej 36, Charlottenlund, Danmark","dates":["2026-01-28","2026-02-12","2026-02-25","2026-03-25","2026-04-11","2026-04-22","2026-05-20","2026-06-17","2026-07-10","2026-07-15","2026-09-09","2026-12-08","2026-12-30"]},{"address":"Kanalbuen 6","city":"Dyssegård","kommune":"Gentofte","fullAddress":"Kanalbuen 6, Dyssegård, Danmark","dates":["2026-01-10","2026-01-22","2026-02-19","2026-03-09","2026-03-19","2026-04-16","2026-05-14","2026-06-08","2026-09-07","2026-10-29","2026-11-06","2026-11-29","2026-12-24"]},{"address":"Dalstrøget","city":"Dyssegård","kommune":"Gentofte","fullAddress":"Dalstrøget, Dyssegård, Danmark","dates":["2026-01-10","2026-01-22","2026-02-19","2026-03-09","2026-03-19","2026-04-16","2026-05-14","2026-06-08","2026-09-07","2026-10-29","2026-11-06","2026-11-29","2026-12-24"]},{"address":"Sønderengen 10","city":"Dyssegård","kommune":"Gentofte","fullAddress":"Sønderengen 10, Dyssegård, Danmark","dates":["2026-02-04","2026-04-30","2026-05-02","2026-05-03","2026-05-28","2026-06-25","2026-07-23","2026-08-01","2026-08-20","2026-09-17","2026-10-12","2026-10-15","2026-12-11"]},{"address":"Fruevej","city":"Dyssegård","kommune":"Gentofte","fullAddress":"Fruevej, Dyssegård, Danmark","dates":["2026-02-04","2026-04-30","2026-05-02","2026-05-03","2026-05-28","2026-06-25","2026-07-23","2026-08-01","2026-08-20","2026-09-17","2026-10-12","2026-10-15","2026-12-11"]},{"address":"Almindingen","city":"Dyssegård","kommune":"Gentofte","fullAddress":"Almindingen, Dyssegård, Danmark","dates":["2026-02-04","2026-04-30","2026-05-02","2026-05-03","2026-05-28","2026-06-25","2026-07-23","2026-08-01","2026-08-20","2026-09-17","2026-10-12","2026-10-15","2026-12-11"]},{"address":"Bakkevænget 10","city":"Gentofte","kommune":"Gentofte","fullAddress":"Bakkevænget 10, Gentofte, Danmark","dates":["2026-01-04","2026-04-02","2026-04-03","2026-04-29","2026-05-27","2026-06-24","2026-07-01","2026-07-22","2026-08-19","2026-09-12","2026-09-16","2026-10-14","2026-11-11"]},{"address":"Fuglegårdsvænget","city":"Gentofte","kommune":"Gentofte","fullAddress":"Fuglegårdsvænget, Gentofte, Danmark","dates":["2026-01-04","2026-04-02","2026-04-03","2026-04-29","2026-05-27","2026-06-24","2026-07-01","2026-07-22","2026-08-19","2026-09-12","2026-09-16","2026-10-14","2026-11-11"]},{"address":"Kildeskovsvej 31","city":"Gentofte","kommune":"Gentofte","fullAddress":"Kildeskovsvej 31, Gentofte, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-12","2026-08-18","2026-09-15","2026-10-11","2026-10-13"]},{"address":"Middelvej 9","city":"Gentofte","kommune":"Gentofte","fullAddress":"Middelvej 9, Gentofte, Danmark","dates":["2026-01-21","2026-02-09","2026-02-18","2026-03-18","2026-04-15","2026-05-08","2026-05-13","2026-08-07","2026-09-30","2026-10-06","2026-10-28","2026-11-25","2026-12-23"]},{"address":"Snogegårdsvej 39","city":"Gentofte","kommune":"Gentofte","fullAddress":"Snogegårdsvej 39, Gentofte, Danmark","dates":["2026-01-21","2026-02-09","2026-02-18","2026-03-18","2026-04-15","2026-05-08","2026-05-13","2026-08-07","2026-09-30","2026-10-06","2026-10-28","2026-11-25","2026-12-23"]},{"address":"Snerlevej 6","city":"Gentofte","kommune":"Gentofte","fullAddress":"Snerlevej 6, Gentofte, Danmark","dates":["2026-01-04","2026-04-02","2026-04-03","2026-04-29","2026-05-27","2026-06-24","2026-07-01","2026-07-22","2026-08-19","2026-09-12","2026-09-16","2026-10-14","2026-11-11"]},{"address":"Gladsaxevej 51","city":"Gladsaxe","kommune":"Gladsaxe","fullAddress":"Gladsaxevej 51, Gladsaxe, Danmark","dates":["2026-01-29","2026-02-01","2026-02-26","2026-03-12","2026-03-26","2026-04-23","2026-05-11","2026-05-21","2026-06-18","2026-07-16","2026-08-10","2026-08-13","2026-10-09","2026-12-31"]},{"address":"Maglegårds Alle 16A","city":"Gladsaxe","kommune":"Gladsaxe","fullAddress":"Maglegårds Alle 16A, Gladsaxe, Danmark","dates":["2026-01-28","2026-02-12","2026-02-25","2026-03-25","2026-04-11","2026-04-22","2026-05-20","2026-06-17","2026-07-10","2026-07-15","2026-09-09","2026-12-08","2026-12-30"]},{"address":"Solvangsvej 7","city":"Glostrup","kommune":"Glostrup","fullAddress":"Solvangsvej 7, Glostrup, Danmark","dates":["2026-01-26","2026-02-11","2026-02-23","2026-03-23","2026-04-20","2026-05-10","2026-05-18","2026-06-15","2026-07-09","2026-07-13","2026-10-08","2026-11-30","2026-12-28"]},{"address":"Højsgårds alle","city":"Hellerup","kommune":"Gentofte","fullAddress":"Højsgårds alle, Hellerup, Danmark","dates":["2026-01-23","2026-02-10","2026-02-20","2026-03-20","2026-04-09","2026-04-17","2026-05-15","2026-07-08","2026-10-07","2026-10-30","2026-11-27","2026-12-06","2026-12-25"]},{"address":"Ellebakken 10","city":"Hellerup","kommune":"Gentofte","fullAddress":"Ellebakken 10, Hellerup, Danmark","dates":["2026-01-23","2026-02-10","2026-02-20","2026-03-20","2026-04-09","2026-04-17","2026-05-15","2026-07-08","2026-10-07","2026-10-30","2026-11-27","2026-12-06","2026-12-25"]},{"address":"Grants Alle","city":"Hellerup","kommune":"Gentofte","fullAddress":"Grants Alle, Hellerup, Danmark","dates":["2026-01-05","2026-03-04","2026-05-29","2026-06-02","2026-06-03","2026-06-26","2026-07-24","2026-08-21","2026-09-01","2026-09-18","2026-10-16","2026-11-12","2026-11-13"]},{"address":"Niels Andersens vej 43","city":"Hellerup","kommune":"Gentofte","fullAddress":"Niels Andersens vej 43, Hellerup, Danmark","dates":["2026-01-13","2026-02-06","2026-05-05","2026-06-30","2026-07-04","2026-07-28","2026-08-25","2026-09-22","2026-10-02","2026-10-03","2026-10-20","2026-11-17","2026-12-15"]},{"address":"Eggersvej","city":"Hellerup","kommune":"Gentofte","fullAddress":"Eggersvej, Hellerup, Danmark","dates":["2026-01-13","2026-02-06","2026-05-05","2026-06-30","2026-07-04","2026-07-28","2026-08-25","2026-09-22","2026-10-02","2026-10-03","2026-10-20","2026-11-17","2026-12-15"]},{"address":"Henningsens Alle 8","city":"Hellerup","kommune":"Gentofte","fullAddress":"Henningsens Alle 8, Hellerup, Danmark","dates":["2026-01-13","2026-02-06","2026-05-05","2026-06-30","2026-07-04","2026-07-28","2026-08-25","2026-09-22","2026-10-02","2026-10-03","2026-10-20","2026-11-17","2026-12-15"]},{"address":"Ellemosevej 8","city":"Hellerup","kommune":"Gentofte","fullAddress":"Ellemosevej 8, Hellerup, Danmark","dates":["2026-01-23","2026-02-10","2026-02-20","2026-03-20","2026-04-09","2026-04-17","2026-05-15","2026-07-08","2026-10-07","2026-10-30","2026-11-27","2026-12-06","2026-12-25"]},{"address":"Teglværksbakken","city":"Hellerup","kommune":"Gentofte","fullAddress":"Teglværksbakken, Hellerup, Danmark","dates":["2026-01-05","2026-03-04","2026-05-29","2026-06-02","2026-06-03","2026-06-26","2026-07-24","2026-08-21","2026-09-01","2026-09-18","2026-10-16","2026-11-12","2026-11-13"]},{"address":"Landsevej 8A","city":"Holte","kommune":"Rudersdal","fullAddress":"Landsevej 8A, Holte, Danmark","dates":["2026-04-06","2026-07-30","2026-09-04","2026-09-24","2026-11-19","2026-12-02"]},{"address":"Landsebakken 24","city":"Holte","kommune":"Rudersdal","fullAddress":"Landsebakken 24, Holte, Danmark","dates":["2026-04-06","2026-07-30","2026-09-04","2026-09-24","2026-11-19","2026-12-02"]},{"address":"Kollemosevej 7","city":"Holte","kommune":"Rudersdal","fullAddress":"Kollemosevej 7, Holte, Danmark","dates":["2026-01-09","2026-01-20","2026-03-17","2026-07-07","2026-10-27","2026-12-05","2026-12-22"]},{"address":"Rønnebærvej 140","city":"Holte","kommune":"Rudersdal","fullAddress":"Rønnebærvej 140, Holte, Danmark","dates":["2026-01-10","2026-02-19","2026-04-16","2026-06-08","2026-11-06","2026-11-26"]},{"address":"Pile Alle 22","city":"Holte","kommune":"Rudersdal","fullAddress":"Pile Alle 22, Holte, Danmark","dates":["2026-04-06","2026-07-30","2026-09-04","2026-09-24","2026-11-19","2026-12-02"]},{"address":"Rudersdalsvej 63","city":"Holte","kommune":"Rudersdal","fullAddress":"Rudersdalsvej 63, Holte, Danmark","dates":["2026-04-06","2026-07-30","2026-09-04","2026-09-24","2026-11-19","2026-12-02"]},{"address":"Rudegårds Alle 29","city":"Holte","kommune":"Rudersdal","fullAddress":"Rudegårds Alle 29, Holte, Danmark","dates":["2026-01-10","2026-02-19","2026-04-16","2026-06-08","2026-11-06","2026-11-26"]},{"address":"Solbakken 43","city":"Holte","kommune":"Rudersdal","fullAddress":"Solbakken 43, Holte, Danmark","dates":["2026-02-17","2026-04-08","2026-04-14","2026-09-06","2026-09-29","2026-11-24"]},{"address":"Borgevej 25 B","city":"Lyngby","kommune":"Lyngby-Taarbæk","fullAddress":"Borgevej 25 B, Lyngby, Danmark","dates":["2026-01-23","2026-02-10","2026-02-20","2026-03-20","2026-04-09","2026-04-17","2026-05-15","2026-07-08","2026-10-07","2026-10-30","2026-11-27","2026-12-06","2026-12-25"]},{"address":"Risums Alle 6","city":"Rødovre","kommune":"Rødovre","fullAddress":"Risums Alle 6, Rødovre, Danmark","dates":["2026-01-22","2026-02-04","2026-02-19","2026-03-19","2026-04-16","2026-05-02","2026-05-03","2026-08-01"]},{"address":"Sydtoftevej 11","city":"Søborg","kommune":"Gladsaxe","fullAddress":"Sydtoftevej 11, Søborg, Danmark","dates":["2026-01-30","2026-02-01","2026-02-27","2026-03-27","2026-04-12","2026-04-24","2026-05-22","2026-06-11","2026-06-19","2026-07-17","2026-08-14","2026-09-10","2026-11-09"]},{"address":"Gorkis Alle 6","city":"Søborg","kommune":"Gladsaxe","fullAddress":"Gorkis Alle 6, Søborg, Danmark","dates":["2026-01-21","2026-02-09","2026-02-18","2026-03-18","2026-04-15","2026-05-08","2026-05-13","2026-08-07","2026-09-30","2026-10-06","2026-10-28","2026-11-25","2026-12-23"]},{"address":"Virumgårdsvej 2","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Virumgårdsvej 2, Virum, Danmark","dates":["2026-01-10","2026-01-22","2026-02-19","2026-03-09","2026-03-19","2026-04-16","2026-05-14","2026-06-08","2026-09-07","2026-10-29","2026-11-06","2026-11-29","2026-12-24"]},{"address":"Bernhard Olsensvej 7","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Bernhard Olsensvej 7, Virum, Danmark","dates":["2026-01-10","2026-01-22","2026-02-19","2026-03-09","2026-03-19","2026-04-16","2026-05-14","2026-06-08","2026-09-07","2026-10-29","2026-11-06","2026-11-29","2026-12-24"]},{"address":"Krogvej 16","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Krogvej 16, Virum, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-12","2026-08-18","2026-09-15","2026-10-11","2026-10-13"]},{"address":"Parkvej 43","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Parkvej 43, Virum, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-12","2026-08-18","2026-09-15","2026-10-11","2026-10-13"]},{"address":"Holmevej 44","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Holmevej 44, Virum, Danmark","dates":["2026-03-02","2026-03-03","2026-03-31","2026-04-28","2026-05-26","2026-06-01","2026-06-23","2026-07-21","2026-08-12","2026-08-18","2026-09-15","2026-10-11","2026-10-13"]},{"address":"Højdevej 29","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Højdevej 29, Virum, Danmark","dates":["2026-01-13","2026-02-06","2026-05-05","2026-06-30","2026-07-04","2026-07-28","2026-08-25","2026-09-22","2026-10-02","2026-10-03","2026-10-20","2026-11-17","2026-12-15"]},{"address":"Kollemosevej 30","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Kollemosevej 30, Virum, Danmark","dates":["2026-01-13","2026-02-06","2026-05-05","2026-06-30","2026-07-04","2026-07-28","2026-08-25","2026-09-22","2026-10-02","2026-10-03","2026-10-20","2026-11-17","2026-12-15"]},{"address":"Kongestien 41","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Kongestien 41, Virum, Danmark","dates":["2026-01-04","2026-04-02","2026-04-03","2026-04-29","2026-05-27","2026-06-24","2026-07-01","2026-07-22","2026-08-19","2026-09-12","2026-09-16","2026-10-14","2026-11-11"]},{"address":"Hummeltoften 46","city":"Virum","kommune":"Lyngby-Taarbæk","fullAddress":"Hummeltoften 46, Virum, Danmark","dates":["2026-01-21","2026-02-09","2026-02-18","2026-03-18","2026-04-15","2026-05-08","2026-05-13","2026-08-07","2026-09-30","2026-10-06","2026-10-28","2026-11-25","2026-12-23"]}];

let map, geocoder, markers = [], infoWindow, selectedDate = '';

function initMap() {
  map = new google.maps.Map(document.getElementById('map'), {
    center: { lat: 55.73, lng: 12.52 },
    zoom: 11,
    mapTypeControl: false,
    streetViewControl: false,
    styles: [
      { featureType: 'poi', elementType: 'labels', stylers: [{ visibility: 'off' }] },
      { featureType: 'transit', elementType: 'labels', stylers: [{ visibility: 'off' }] }
    ]
  });
  geocoder = new google.maps.Geocoder();
  infoWindow = new google.maps.InfoWindow();

  // Set today's date
  const today = new Date().toISOString().split('T')[0];
  document.getElementById('datePicker').value = today;
}

function setToday() {
  const today = new Date().toISOString().split('T')[0];
  document.getElementById('datePicker').value = today;
  filterByDate();
}

function formatDanishDate(isoDate) {
  const [y,m,d] = isoDate.split('-');
  const months = ['jan','feb','mar','apr','maj','jun','jul','aug','sep','okt','nov','dec'];
  return `${parseInt(d)}. ${months[parseInt(m)-1]} ${y}`;
}

function filterByDate() {
  selectedDate = document.getElementById('datePicker').value;
  if (!selectedDate) return;

  // Filter addresses for the selected date
  const filtered = ADDRESSES.filter(a => a.dates.includes(selectedDate));
  
  // Update sidebar
  renderList(filtered, selectedDate);
  
  // Update stats
  const kommuner = new Set(filtered.map(a => a.kommune)).size;
  const byer = new Set(filtered.map(a => a.city)).size;
  document.getElementById('statCount').textContent = filtered.length;
  document.getElementById('statKommuner').textContent = kommuner;
  document.getElementById('statByer').textContent = byer;
  document.getElementById('statsBar').style.display = filtered.length > 0 ? 'flex' : 'none';
  document.getElementById('legend').style.display = filtered.length > 0 ? 'block' : 'none';

  // Clear old markers
  markers.forEach(m => m.setMap(null));
  markers = [];
  infoWindow.close();

  // Geocode and place markers
  filtered.forEach((addr, i) => {
    geocoder.geocode({ address: addr.fullAddress, region: 'DK' }, (results, status) => {
      if (status === 'OK') {
        const pos = results[0].geometry.location;
        const marker = new google.maps.Marker({
          position: pos,
          map,
          title: addr.address,
          label: {
            text: String(i + 1),
            color: '#fff',
            fontFamily: 'DM Sans',
            fontSize: '11px',
            fontWeight: '700'
          },
          icon: {
            path: google.maps.SymbolPath.CIRCLE,
            scale: 16,
            fillColor: '#e07b2a',
            fillOpacity: 1,
            strokeColor: '#fff',
            strokeWeight: 2
          },
          zIndex: 100
        });

        markers.push(marker);

        marker.addListener('click', () => {
          const datesHtml = addr.dates.map(d => {
            const isSelected = d === selectedDate;
            return `<span class="date-chip ${isSelected ? 'today-chip' : ''}">${formatDanishDate(d)}</span>`;
          }).join('');

          infoWindow.setContent(`
            <div class="info-popup">
              <h3>${addr.address}</h3>
              <div class="city">${addr.city} – ${addr.kommune} Kommune</div>
              <div class="dates-label">Alle afhentningsdatoer</div>
              ${datesHtml}
            </div>
          `);
          infoWindow.open(map, marker);
          highlightListItem(i);
        });

        // Sync list item click
        const listItem = document.getElementById(`item-${i}`);
        if (listItem) {
          listItem.addEventListener('click', () => {
            map.panTo(pos);
            map.setZoom(15);
            google.maps.event.trigger(marker, 'click');
          });
        }
      }
    });
  });

  // Fit bounds after small delay
  if (filtered.length > 0) {
    setTimeout(() => {
      if (markers.length > 0) {
        const bounds = new google.maps.LatLngBounds();
        markers.forEach(m => bounds.extend(m.getPosition()));
        map.fitBounds(bounds, { padding: 60 });
      }
    }, 1500);
  }
}

function renderList(filtered, date) {
  const list = document.getElementById('addrList');
  if (filtered.length === 0) {
    list.innerHTML = `
      <div class="no-results">
        <div class="icon">🔍</div>
        <p>Ingen afhentninger den<br><strong>${formatDanishDate(date)}</strong></p>
      </div>`;
    return;
  }

  list.innerHTML = filtered.map((a, i) => `
    <div class="addr-item" id="item-${i}">
      <div class="addr-num">${i + 1}</div>
      <div class="addr-info">
        <div class="name">${a.address}</div>
        <div class="loc">${a.city} · ${a.kommune}</div>
        <div class="next-date">✓ Afhentes ${formatDanishDate(date)}</div>
      </div>
    </div>
  `).join('');
}

function highlightListItem(index) {
  document.querySelectorAll('.addr-item').forEach(el => el.classList.remove('active'));
  const item = document.getElementById(`item-${index}`);
  if (item) {
    item.classList.add('active');
    item.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
  }
}

// Auto-filter on page load after map init
window.filterByDateOnLoad = function() {
  filterByDate();
};
</script>

<!-- 
  VIGTIGT: Erstat DIN_API_NØGLE herunder med din Google Maps API-nøgle.
  Hent en nøgle gratis på: https://console.cloud.google.com/
  Aktiver: Maps JavaScript API + Geocoding API
-->
<script async defer
  src="https://maps.googleapis.com/maps/api/js?key=AIzaSyBN9XgE66jnuP-oJ1vFSshGeljKMKhe594&callback=initMap&language=da">
</script>

</body>
</html>
