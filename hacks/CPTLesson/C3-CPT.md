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
/* Fix text visibility */
body, .container, .container * {
  color: #000;
}

.CodeMirror, .CodeMirror * {
  color: inherit !important;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.section {
  margin-top: 16px;
  padding: 16px;
  border-radius: 10px;
  border: 1px solid #ddd;
  background: #f8f8f8;
}

textarea {
  width: 100%;
  min-height: 120px;
  padding: 10px;
  margin-top: 6px;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 14px;
  background: #fff;
}

label {
  font-weight: bold;
  display: block;
  margin-top: 10px;
}

button {
  padding: 10px 14px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  margin-right: 8px;
  margin-top: 10px;
  font-weight: bold;
}

.save {
  background: #28a745;
  color: white;
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
<h3>Written Response of Purpose</h3>
<textarea id="programInput"></textarea>
<button class="save" onclick="save('programInput')">Save</button>
</div>

<div class="section">
<h3>🧾 Finalized Trace Box</h3>
{% include code-runner.html
   runner_id="trace_final_runner"
   language="python"
   code=""
%}
</div>

<div class="section">
<h3>✍️ Program Trace</h3>

<label>Input / Start State</label>
{% include code-runner.html
   runner_id="trace_input_runner"
   language="python"
   code=""
%}

<label>Loop Behavior</label>
{% include code-runner.html
   runner_id="trace_loop_runner"
   language="python"
   code=""
%}

<label>Condition</label>
{% include code-runner.html
   runner_id="trace_condition_runner"
   language="python"
   code=""
%}

<label>Updates</label>
{% include code-runner.html
   runner_id="trace_updates_runner"
   language="python"
   code=""
%}

<label>Output</label>
{% include code-runner.html
   runner_id="trace_output_runner"
   language="python"
   code=""
%}

</div>

</div>

<script>
function save(id) {
  const el = document.getElementById(id);
  if (!el) return;
  localStorage.setItem(id, el.value);
}

window.addEventListener("DOMContentLoaded", () => {
  ["programInput"]
  .forEach(id => {
    const saved = localStorage.getItem(id);
    if (saved) document.getElementById(id).value = saved;
  });
});
</script>