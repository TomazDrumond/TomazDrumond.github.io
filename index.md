---
layout: default
title: Home
---
<section id="home" markdown="1">
![Hero](/asset/images/hero_variant_F.png)
# One scorecard. One clear answer: is this loan any good.
Credit analysis and quantitative finance.
</section>
<hr>
<section id="projects" markdown="1">
# Projects
## Done
![Loan Tape Credit Analysis](/asset/images/cover_loantape.png)
![Scorecard](/asset/images/scorecard_framed.png)
![Domestic Macro Review](/asset/images/cover_macro.png)
![Macro charts](/asset/images/macro_framed.png)
## In Progress
Itaú Quant Model · CFA · MBA models · Quant models

<section id="calculator">
 
# Live Scorecard Calculator
 
<p>Enter your own portfolio's six indicators below to see the exact weighted scoring model from my Loan Tape Credit Analysis run live, in your browser.</p>
 
<div class="calc-form">
  <label>NPL 90+ DPD (%)
    <input type="number" id="calc-npl" step="0.1" placeholder="e.g. 9.2">
  </label>
  <label>IAG Global (%)
    <input type="number" id="calc-iag" step="0.1" placeholder="e.g. 13.7">
  </label>
  <label>FPD Rate (%)
    <input type="number" id="calc-fpd" step="0.1" placeholder="e.g. 9.1">
  </label>
  <label>Recovery Rate (%)
    <input type="number" id="calc-recovery" step="0.1" placeholder="e.g. 39.4">
  </label>
  <label>EL / EAD (%)
    <input type="number" id="calc-el" step="0.1" placeholder="e.g. 11.5">
  </label>
  <label>Cure Rate (%)
    <input type="number" id="calc-cure" step="0.1" placeholder="e.g. 15.0">
  </label>
 
  <button id="calc-submit" type="button">Calculate Score</button>
 
  <div id="calc-result" class="calc-result" style="display:none;"></div>
  <div id="calc-error" class="calc-error" style="display:none;"></div>
</div>
 
</section>
 
<style>
  .calc-form{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:16px;
    margin-top:20px;
  }
  .calc-form label{
    display:flex;
    flex-direction:column;
    font-family:'IBM Plex Mono', monospace;
    font-size:12px;
    text-transform:uppercase;
    letter-spacing:.04em;
    color:var(--muted);
    gap:6px;
  }
  .calc-form input{
    font-family:'IBM Plex Sans', sans-serif;
    font-size:16px;
    padding:10px 12px;
    border:1px solid var(--rule);
    border-radius:4px;
    background:var(--bg);
    color:var(--ink);
  }
  .calc-form button{
    grid-column:1 / -1;
    font-family:'IBM Plex Mono', monospace;
    font-size:13px;
    text-transform:uppercase;
    letter-spacing:.04em;
    padding:12px;
    background:var(--navy);
    color:var(--bg);
    border:none;
    border-radius:4px;
    cursor:pointer;
    margin-top:8px;
  }
  .calc-form button:hover{ background:var(--gold); }
  .calc-result{
    grid-column:1 / -1;
    border:1px solid var(--rule);
    border-radius:4px;
    padding:20px;
    margin-top:8px;
  }
  .calc-result .score{
    font-family:'IBM Plex Serif', serif;
    font-size:40px;
    font-weight:700;
    color:var(--navy);
  }
  .calc-error{
    grid-column:1 / -1;
    color:#8C2A2A;
    font-size:13px;
    margin-top:8px;
  }
 
  @media (max-width:600px){
    .calc-form{ grid-template-columns:1fr; }
  }
</style>
 
<script>
  document.getElementById('calc-submit').addEventListener('click', async function () {
    const getVal = (id) => parseFloat(document.getElementById(id).value) / 100;
 
    const payload = {
      npl: getVal('calc-npl'),
      iag: getVal('calc-iag'),
      fpd: getVal('calc-fpd'),
      recovery: getVal('calc-recovery'),
      el: getVal('calc-el'),
      cure: getVal('calc-cure'),
    };
 
    const errorBox = document.getElementById('calc-error');
    const resultBox = document.getElementById('calc-result');
    errorBox.style.display = 'none';
    resultBox.style.display = 'none';
 
    // Basic client-side check before even calling the backend
    for (const [key, val] of Object.entries(payload)) {
      if (isNaN(val)) {
        errorBox.textContent = 'Please fill in all six fields with numbers.';
        errorBox.style.display = 'block';
        return;
      }
    }
 
    try {
      const response = await fetch('https://charming-treacle-5a8219.netlify.app/.netlify/functions/scorecard', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload),
      });
 
      const data = await response.json();
 
      if (!response.ok) {
        errorBox.textContent = data.error || 'Something went wrong.';
        errorBox.style.display = 'block';
        return;
      }
 
      resultBox.innerHTML =
        '<div class="score">' + data.final_score + ' / 100</div>' +
        '<div>' + data.verdict + '</div>' +
        (data.veto_active ? '<div style="color:#8C2A2A;margin-top:6px;">Veto: ' + data.veto_reasons.join(', ') + '</div>' : '');
      resultBox.style.display = 'block';
    } catch (err) {
      errorBox.textContent = 'Could not reach the scoring service. Please try again.';
      errorBox.style.display = 'block';
    }
  });
</script>

</section>
<hr>
<section id="about" markdown="1">
 
# About

![Tomaz Drumond](/asset/images/photo_framed.png)

I'm a Scientific Initiation Fellow at UFMG, working on credit and macro analysis. My loan tape project scored a portfolio at medium quality using vintage curves and CreditMetrics. My macro review modeled two 2026 election scenarios and found the real risk isn't the election — it's Brazil's fiscal position. I want to keep doing this kind of work, for a team that needs someone who can turn a messy dataset into a decision.

Stack: Python, R, SQL, VBA, Power BI, Excel.

</section>

<hr>

<section id="contact" markdown="1">

# Contact

<div class="cta-row">
  <a class="cta-icon" href="https://www.linkedin.com/in/tomazdrumond" target="_blank" rel="noopener">
    <img src="/asset/icons/linkedin.svg" alt="" width="18" height="18"> LinkedIn
  </a>
  <a class="cta-icon" href="https://github.com/TomazDrumond/MYREPO" target="_blank" rel="noopener">
    <img src="/asset/icons/github.svg" alt="" width="18" height="18"> GitHub
  </a>
  <a class="cta-icon" href="/asset/CVTomaz.pdf" target="_blank" rel="noopener">
    <img src="/asset/icons/file.svg" alt="" width="18" height="18"> CV
  </a>
  <a class="cta-icon" href="https://calendly.com/tomaz96321/30min" target="_blank" rel="noopener">
    <img src="/asset/icons/calendar.svg" alt="" width="18" height="18"> Book 15 min
  </a>
</div>

</section>
