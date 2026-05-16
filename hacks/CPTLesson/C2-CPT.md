---
layout: post
microblog: True
title: CPT Project Layout Builder (Enhanced)
description: A structured AP CSP CPT drafting tool that maps student ideas into required components with guided AI feedback.
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

Key idea: You are evaluated on whether these components are clearly implemented and explained.

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
  color: #000;
}

label {
  font-weight: bold;
  display: block;
  margin-top: 10px;
  color: #000;
}

input, textarea {
  width: 100%;
  padding: 10px;
  margin-top: 6px;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 14px;
  color: #000;
  background: #fff;
}

button {
  margin-top: 10px;
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

.ai-box {
  margin-top: 12px;
  padding: 12px;
  border-left: 4px solid #007bff;
  background: #f8f9fa;
  white-space: pre-wrap;
  color: #000;
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}

small {
  color: #666;
  font-size: 13px;
}
</style>

<div class="container">

<!-- ================= GUIDE ================= -->
<div class="section">
<details>
<summary style="cursor:pointer;color:#007bff;font-weight:bold;">
📘 CPT Builder Guide
</summary>

### How to use this tool
1. Enter your CPT project idea
2. Click generate
3. Review AI-generated structure
4. Refine manually if needed

### CPT Components
- Input → user interaction
- Output → displayed result
- List → stored data collection
- Procedure → reusable function
- Algorithm → loop + condition + sequence

</details>
</div>

<!-- ================= AI INPUT ================= -->
<div class="section">

<h3>🧠 AI CPT Structure Generator</h3>

<textarea id="ideaInput" placeholder="Describe your CPT project idea..."></textarea>

<button onclick="generateStructure()">Generate CPT Structure</button>

<div id="status" class="ai-box" style="display:none;"></div>

</div>

<!-- ================= MANUAL ================= -->
<div class="section">

<h3>✍️ Manual CPT Builder</h3>

<div class="grid">

<div>
<label>Input</label>
<input id="inputField">
</div>

<div>
<label>Output</label>
<input id="outputField">
</div>

<div>
<label>List</label>
<input id="listField">
</div>

<div>
<label>Procedure</label>
<input id="procedureField">
</div>

<div>
<label>Algorithm</label>
<input id="algorithmField">
</div>

</div>

</div>

<!-- ================= FEEDBACK ================= -->
<div class="section">

<h3>📊 AI Feedback</h3>
<div id="feedback" class="ai-box">
Waiting for AI output...
</div>

</div>

</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

function setStatus(msg, type="info") {
    const el = document.getElementById("status");
    el.style.display = "block";
    el.textContent = msg;

    const colors = {
        info: "#d1ecf1",
        success: "#d4edda",
        error: "#f8d7da"
    };

    el.style.background = colors[type] || "#d1ecf1";
}

window.generateStructure = function () {

    const idea = document.getElementById("ideaInput").value.trim();

    if (!idea) {
        setStatus("Enter your CPT idea first.", "error");
        return;
    }

    const PROMPT = `
You are an AP CSP CPT structure assistant.

Return ONLY valid JSON:

{
  "input": {"value":"","feedback":""},
  "output": {"value":"","feedback":""},
  "list": {"value":"","feedback":""},
  "procedure": {"value":"","feedback":""},
  "algorithm": {"value":"","feedback":""}
}

Rules:
- value = clear CPT-ready response
- feedback = how to improve for AP CSP alignment
- ensure realism and correctness
- ensure all required CPT components are included

Student idea:
`;

    setStatus("Generating CPT structure...", "info");

    queryGemini({
        prompt: PROMPT,
        text: idea,
        parseJSON: true
    })
    .then(data => {

        const set = (id, val) => {
            const el = document.getElementById(id);
            if (el) el.value = val || "";
        };

        set("inputField", data.input?.value);
        set("outputField", data.output?.value);
        set("listField", data.list?.value);
        set("procedureField", data.procedure?.value);
        set("algorithmField", data.algorithm?.value);

        document.getElementById("feedback").innerHTML = `
<b>Input:</b> ${data.input?.feedback || "No feedback"}<br><br>
<b>Output:</b> ${data.output?.feedback || "No feedback"}<br><br>
<b>List:</b> ${data.list?.feedback || "No feedback"}<br><br>
<b>Procedure:</b> ${data.procedure?.feedback || "No feedback"}<br><br>
<b>Algorithm:</b> ${data.algorithm?.feedback || "No feedback"}
        `;

        setStatus("Structure generated successfully.", "success");
    })
    .catch(() => {

        document.getElementById("inputField").value = "User input interaction";
        document.getElementById("outputField").value = "Program displays results";
        document.getElementById("listField").value = "Stores multiple data items";
        document.getElementById("procedureField").value = "function process(input)";
        document.getElementById("algorithmField").value =
`loop through items:
  if condition:
    update value`;

        document.getElementById("feedback").innerHTML =
            "Fallback mode active. Manual editing required.";

        setStatus("Fallback loaded.", "error");
    });
};
</script>