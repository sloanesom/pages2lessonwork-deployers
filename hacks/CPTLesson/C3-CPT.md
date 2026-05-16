---
layout: post
microblog: True
title: CPT Program Trace Builder
description: A drafting tool that helps students trace program execution step-by-step and connect it to AP CSP CPT requirements with AI-assisted feedback.
author: David M, Sloane S
permalink: /cpt/3
breadcrumb: True
---

## CPT Program Tracing Overview

In AP CSP, “tracing a program” means explaining **how a program runs step-by-step**.

You are expected to understand and explain:
- What the program starts with (input/state)
- How data changes during execution
- How loops repeat steps
- How conditions affect decisions
- What the final output becomes

Key idea: You are not just describing code — you are explaining **how the program behaves over time**.

---

<style>
.container {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.box {
  width: 100%;
  padding: 10px;
  margin: 6px 0;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 14px;
}

.label {
  font-weight: bold;
  margin-top: 10px;
  display: block;
}

.section {
  margin-top: 20px;
  padding: 15px;
  border-radius: 10px;
  border: 1px solid #ddd;
  background: #fafafa;
}

button {
  padding: 10px 14px;
  border: none;
  border-radius: 6px;
  background: #007bff;
  color: white;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background: #0056b3;
}

.ai-box {
  margin-top: 15px;
  padding: 12px;
  border-left: 4px solid #007bff;
  background: #f8f9fa;
  white-space: pre-wrap;
}

.small {
  font-size: 13px;
  color: #555;
}
</style>

<div class="container">

<!-- ================= GUIDE ================= -->
<div class="section">
<details>
<summary style="cursor:pointer;font-weight:bold;color:#007bff;">
📘 CPT Trace Guide (Click to expand)
</summary>

### What is tracing?
Tracing explains how a program runs step-by-step.

### You must include:
- Starting values
- Loop iterations
- Condition results
- Variable updates
- Final output

</details>
</div>

<!-- ================= AI INPUT ================= -->
<div class="section">

<h3>🧠 AI Program Trace Generator</h3>

<textarea id="programInput" class="box" rows="5"
placeholder="Paste or describe your program logic here..."></textarea>

<button onclick="generateTrace()">Generate Trace</button>

<div id="statusBox" class="ai-box" style="display:none;"></div>

</div>

<!-- ================= MANUAL TRACE ================= -->
<div class="section">

<h3>✍️ Manual Trace Builder</h3>

<label class="label">Input / Start State</label>
<input id="inputState" class="box" type="text">

<label class="label">Loop Behavior</label>
<input id="loopState" class="box" type="text">

<label class="label">Condition (if/else)</label>
<input id="conditionState" class="box" type="text">

<label class="label">Variable Updates</label>
<input id="updateState" class="box" type="text">

<label class="label">Final Output</label>
<input id="outputState" class="box" type="text">

</div>

<!-- ================= FEEDBACK ================= -->
<div class="section">

<h3>📊 AI Feedback</h3>

<div id="feedbackBox" class="ai-box">
AI feedback will appear here after generation.
</div>

</div>

</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

function setStatus(msg, type="info") {
    const el = document.getElementById("statusBox");
    el.style.display = "block";
    el.textContent = msg;

    const colors = {
        info: "#d1ecf1",
        success: "#d4edda",
        error: "#f8d7da"
    };

    el.style.background = colors[type] || "#d1ecf1";
}

window.generateTrace = function () {

    const input = document.getElementById("programInput").value.trim();

    if (!input) {
        setStatus("Please enter program description first.", "error");
        return;
    }

    const PROMPT = `
You are an AP CSP Program Trace Assistant.

Return ONLY valid JSON:

{
  "input": {"value":"","feedback":""},
  "loop": {"value":"","feedback":""},
  "condition": {"value":"","feedback":""},
  "update": {"value":"","feedback":""},
  "output": {"value":"","feedback":""}
}

Rules:
- value = student-ready trace step
- feedback = improvement explanation
- keep steps realistic and AP CSP aligned

Program:
`;

    setStatus("Generating trace...", "info");

    queryGemini({
        prompt: PROMPT,
        text: input,
        parseJSON: true
    })
    .then(data => {

        document.getElementById("inputState").value = data.input?.value || "";
        document.getElementById("loopState").value = data.loop?.value || "";
        document.getElementById("conditionState").value = data.condition?.value || "";
        document.getElementById("updateState").value = data.update?.value || "";
        document.getElementById("outputState").value = data.output?.value || "";

        document.getElementById("feedbackBox").innerHTML = `
<b>Input:</b> ${data.input?.feedback || ""}<br><br>
<b>Loop:</b> ${data.loop?.feedback || ""}<br><br>
<b>Condition:</b> ${data.condition?.feedback || ""}<br><br>
<b>Update:</b> ${data.update?.feedback || ""}<br><br>
<b>Output:</b> ${data.output?.feedback || ""}
        `;

        setStatus("Trace generated successfully.", "success");
    })
    .catch(err => {

        document.getElementById("feedbackBox").innerHTML =
            "AI unavailable. Please use manual trace section.";

        setStatus("Fallback mode activated.", "error");
    });
};
</script>