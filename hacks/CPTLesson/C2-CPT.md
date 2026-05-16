---
layout: post
microblog: True
title: CPT Project Layout Builder
description: A structured AP CSP CPT drafting tool for manually building components.
author: David M, Sloane S
permalink: /cpt/2
breadcrumb: True
---

## CPT Requirements Overview

The Create Performance Task (CPT) requires a program that demonstrates core computational thinking concepts.

Your program must include:

- **Input**: user interaction
- **Output**: program-generated result
- **List**: collection of data items
- **Procedure**: reusable function with parameter
- **Algorithm**: sequencing, selection, iteration

---

<style>
body, .container, .container * {
  color: #000 !important;
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

.load {
  background: #007bff;
  color: white;
}

.clear {
  background: #dc3545;
  color: white;
}
</style>

<div class="container">

<div class="section">
<h3>📘 CPT Builder Guide</h3>
<ul>
  <li>Input = user action</li>
  <li>Output = program result</li>
  <li>List = stored data</li>
  <li>Procedure = function with parameter</li>
  <li>Algorithm = loop + if + sequence</li>
</ul>
</div>

<div class="section">
<h3>🧠 CPT Idea</h3>
<textarea id="ideaInput"></textarea>
</div>

<div class="section">
<h3>✍️ CPT Components</h3>

<label>Input</label>
<textarea id="inputField"></textarea>

<label>Output</label>
<textarea id="outputField"></textarea>

<label>List</label>
<textarea id="listField"></textarea>

<label>Procedure</label>
<textarea id="procedureField"></textarea>

<label>Algorithm</label>
<textarea id="algorithmField"></textarea>
</div>

<div class="section">
<h3>💾 Save System</h3>

<button class="save" onclick="saveCPT()">Save</button>
<button class="load" onclick="loadCPT()">Load</button>
<button class="clear" onclick="clearCPT()">Clear</button>

<p id="status" style="margin-top:10px;"></p>
</div>

</div>

<script>
function saveCPT() {
  const data = {
    idea: ideaInput.value,
    input: inputField.value,
    output: outputField.value,
    list: listField.value,
    procedure: procedureField.value,
    algorithm: algorithmField.value
  };

  localStorage.setItem("cpt_data", JSON.stringify(data));
  status.innerText = "Saved successfully.";
}

function loadCPT() {
  const data = JSON.parse(localStorage.getItem("cpt_data"));
  if (!data) {
    status.innerText = "No saved data.";
    return;
  }

  ideaInput.value = data.idea || "";
  inputField.value = data.input || "";
  outputField.value = data.output || "";
  listField.value = data.list || "";
  procedureField.value = data.procedure || "";
  algorithmField.value = data.algorithm || "";

  status.innerText = "Loaded successfully.";
}

function clearCPT() {
  localStorage.removeItem("cpt_data");

  ideaInput.value = "";
  inputField.value = "";
  outputField.value = "";
  listField.value = "";
  procedureField.value = "";
  algorithmField.value = "";

  status.innerText = "Cleared.";
}
</script>