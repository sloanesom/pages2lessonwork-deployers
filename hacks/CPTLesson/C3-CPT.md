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
/* Global text: black */
body, .container, .container * {
  color: #000 !important;
  font-family: Arial, sans-serif;
}

/* CodeMirror: white background, black text */
.CodeMirror,
.CodeMirror * {
  background: #fff !important;
  color: #000 !important;
}

/* CodeMirror gutters (line numbers) */
.CodeMirror-gutters {
  background: #fff !important;
  border-right: 1px solid #ccc !important;
}

.CodeMirror-linenumber {
  color: #000 !important;
}

/* Textareas: white background, black text */
textarea {
  background: #fff;
  color: #000;
  border: 1px solid #ccc;
  padding: 10px;
  width: 100%;
  border-radius: 6px;
}

/* Buttons: simple gray */
button {
  background: #e0e0e0;
  color: #000;
  border: none;
  padding: 10px 14px;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}

/* Green Save button (your only colored element) */
button.save {
  background: #28a745;
  color: #fff;
}
</style>

<div class="container">

<div class="section">
<h3>CPT Trace Guide</h3>
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
<h3>Finalized Trace Box</h3>
{% include code-runner.html
   runner_id="trace_final_runner"
   language="python"
   code=""
%}
</div>

<div class="section">
<h3>Program Trace</h3>

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
  ["programInput"].forEach(id => {
    const saved = localStorage.getItem(id);
    if (saved) document.getElementById(id).value = saved;
  });
});
</script>
