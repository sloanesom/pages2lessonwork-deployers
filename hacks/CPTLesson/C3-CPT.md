---
layout: post
microblog: True
title: CPT Program Trace Builder
description: A simple manual tool for tracing program execution step-by-step for AP CSP CPT practice.
author: David M, Sloane S
permalink: /cpt/3
breadcrumb: True
---

## CPT Program Tracing Overview

In AP CSP, “tracing a program” means explaining how a program runs step-by-step.

You should describe:
- Input or starting state
- How values change during execution
- How loops repeat actions
- How conditions affect decisions
- Final output

Key idea: You are tracking execution over time, not just describing code.

---

<style>
.container {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.section {
  margin-top: 18px;
  padding: 14px;
  border: 1px solid #ddd;
  border-radius: 10px;
}

label {
  display: block;
  margin-top: 10px;
  font-weight: bold;
}

textarea {
  width: 100%;
  min-height: 140px;
  margin-top: 6px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-family: Arial, sans-serif;
}

button {
  margin-top: 6px;
  padding: 8px 12px;
  border: 1px solid #ccc;
  background: #f5f5f5;
  cursor: pointer;
  border-radius: 6px;
}
</style>

<div class="container">

<div class="section">
<h3>📘 CPT Trace Guide</h3>
<ul>
  <li>Input</li>
  <li>Loop</li>
  <li>Condition</li>
  <li>Updates</li>
  <li>Output</li>
</ul>
</div>

<div class="section">
<h3>🧠 Program Idea</h3>
<textarea id="programInput"></textarea>
<button onclick="save('programInput')">Save</button>
</div>

<div class="section">
<h3>✍️ Program Trace</h3>

<label>Input / Start State</label>
<textarea id="inputState"></textarea>
<button onclick="save('inputState')">Save</button>

<label>Loop Behavior</label>
<textarea id="loopState"></textarea>
<button onclick="save('loopState')">Save</button>

<label>Condition</label>
<textarea id="conditionState"></textarea>
<button onclick="save('conditionState')">Save</button>

<label>Updates</label>
<textarea id="updateState"></textarea>
<button onclick="save('updateState')">Save</button>

<label>Output</label>
<textarea id="outputState"></textarea>
<button onclick="save('outputState')">Save</button>

</div>

</div>

<script>
function save(id) {
  const el = document.getElementById(id);
  if (!el) return;
  localStorage.setItem(id, el.value);
}

window.addEventListener("DOMContentLoaded", () => {
  ["programInput","inputState","loopState","conditionState","updateState","outputState"]
  .forEach(id => {
    const saved = localStorage.getItem(id);
    if (saved) document.getElementById(id).value = saved;
  });
});
</script>