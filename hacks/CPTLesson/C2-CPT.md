---
layout: post
microblog: True
title: CPT Project Layout Builder
description: A structured AP CSP CPT drafting tool for manually building required components.
author: David M, Sloane S
permalink: /cpt/2
breadcrumb: True
---

## CPT Requirements Overview

The Create Performance Task (CPT) requires a program that demonstrates core computational thinking concepts.

Your program must include:

- **Input**: user interaction (typing, clicking, selecting)
- **Output**: program-generated result
- **List**: collection of multiple data items
- **Procedure**: reusable function with at least one parameter
- **Algorithm**: includes sequencing, selection (if), and iteration (loop)

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
  margin-top: 18px;
  padding: 16px;
  border: 1px solid #e0e0e0;
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
  min-height: 180px;
  padding: 12px;
  margin-top: 6px;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 15px;
  resize: vertical;
  background: #fff;
  color: #000;
}

input {
  width: 100%;
  min-height: 70px;
  padding: 10px;
  margin-top: 6px;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 14px;
  background: #fff;
  color: #000;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 14px;
}

small {
  color: #666;
  font-size: 13px;
}
</style>

<div class="container">

<!-- ================= GUIDE ================= -->
<div class="section">

<h3>📘 CPT Builder Guide</h3>

<p>This tool helps you manually structure your CPT project.</p>

<ul>
  <li><b>Input:</b> What the user does</li>
  <li><b>Output:</b> What the program shows</li>
  <li><b>List:</b> Data storage</li>
  <li><b>Procedure:</b> Function with parameter</li>
  <li><b>Algorithm:</b> Loop + condition + sequence</li>
</ul>

</div>

<!-- ================= MAIN INPUT ================= -->
<div class="section">

<h3>🧠 CPT Idea</h3>

<label>Describe your CPT project idea</label>
<textarea id="ideaInput" placeholder="Write your project idea here..."></textarea>

</div>

<!-- ================= MANUAL FIELDS ================= -->
<div class="section">

<h3>✍️ CPT Builder Fields</h3>

<div class="grid">

<div>
<label>Input</label>
<textarea id="inputField"></textarea>
</div>

<div>
<label>Output</label>
<textarea id="outputField"></textarea>
</div>

<div>
<label>List</label>
<textarea id="listField"></textarea>
</div>

<div>
<label>Procedure</label>
<textarea id="procedureField"></textarea>
</div>

<div>
<label>Algorithm</label>
<textarea id="algorithmField"></textarea>
</div>

</div>

</div>

</div>