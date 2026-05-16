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
  color: #000;
}

.section {
  margin-top: 20px;
  padding: 16px;
  border: 1px solid #ddd;
  border-radius: 10px;
  background: #fafafa;
}

label {
  font-weight: bold;
  display: block;
  margin-top: 12px;
  color: #000;
}

textarea {
  width: 100%;
  min-height: 160px;
  padding: 12px;
  margin-top: 6px;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 15px;
  resize: vertical;
  background: #fff;
  color: #000;
}

button {
  margin-top: 12px;
  padding: 10px 14px;
  border: none;
  border-radius: 6px;
  background: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background: #0056b3;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 14px;
}
</style>

<div class="container">

<!-- GUIDE -->
<div class="section">
<h3>📘 CPT Trace Guide</h3>

<ul>
  <li><b>Input:</b> starting data or user input</li>
  <li><b>Loop:</b> repeated steps in the program</li>
  <li><b>Condition:</b> if/else decisions</li>
  <li><b>Updates:</b> how variables change</li>
  <li><b>Output:</b> final result of program</li>
</ul>
</div>

<!-- MAIN IDEA -->
<div class="section">
<h3>🧠 Program Idea</h3>
<label>Describe your program</label>
<textarea id="programInput" placeholder="Write what your program does..."></textarea>
</div>

<!-- TRACE BOXES -->
<div class="section">
<h3>✍️ Program Trace</h3>

<label>Input / Start State</label>
<textarea id="inputState" placeholder="What starts the program?"></textarea>

<label>Loop Behavior</label>
<textarea id="loopState" placeholder="Does it repeat? What happens in the loop?"></textarea>

<label>Condition (if/else)</label>
<textarea id="conditionState" placeholder="What decisions are made?"></textarea>

<label>Variable Updates</label>
<textarea id="updateState" placeholder="How do values change?"></textarea>

<label>Final Output</label>
<textarea id="outputState" placeholder="What does the program output?"></textarea>

</div>

</div>