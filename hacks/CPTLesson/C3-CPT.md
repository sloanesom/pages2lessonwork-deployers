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
.trace-box {
  width: 90%;
  padding: 10px;
  margin: 6px 0;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 14px;
}

.trace-label {
  font-weight: bold;
  margin-top: 10px;
  display: block;
  color: #333;
}

.ai-box {
  margin-top: 16px;
  padding: 12px;
  border-left: 4px solid #007bff;
  background: #f8f9fa;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 20px;
}
</style>

<div class="container">

<details style="padding: 15px; border-radius: 8px; border-left: 4px solid #007bff;">
<summary style="cursor:pointer; font-weight:bold; color:#007bff;">
CPT Trace Guide (Click to expand)
</summary>

### What is program tracing?
Tracing is writing out what happens in a program step-by-step.

### What you should include:
- Initial values
- Each loop iteration
- Each condition result (true/false)
- Changes to variables
- Final output

### Why it matters:
It proves you understand how your program actually runs.

</details>

---

## AI CPT Trace Helper

<label class="trace-label">Paste or describe your program:</label>
<textarea id="program-input" class="trace-box" rows="5"
placeholder="Example: I have a loop that goes through a list of scores and adds them..."></textarea>

<button onclick="generateTrace()" style="margin-top:10px;padding:10px;border:none;background:#007bff;color:white;border-radius:6px;">
🧠 Generate Program Trace
</button>

<div id="ai-status" style="margin-top:10px;display:none;padding:8px;border-radius:4px;"></div>

---

## Manual Trace Builder

<label class="trace-label">Step 1: Input / Start State</label>
<input id="trace-input" class="trace-box" type="text">

<label class="trace-label">Step 2: Loop / Repetition</label>
<input id="trace-loop" class="trace-box" type="text">

<label class="trace-label">Step 3: Condition Checks (if/else)</label>
<input id="trace-condition" class="trace-box" type="text">

<label class="trace-label">Step 4: Variable Changes</label>
<input id="trace-update" class="trace-box" type="text">

<label class="trace-label">Step 5: Output</label>
<input id="trace-output" class="trace-box" type="text">

---

## AI Trace Feedback

<div id="trace-feedback" class="ai-box">
Your AI feedback will appear here after generation.
</div>

</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

function showStatus(msg, type) {
    const el = document.getElementById("ai-status");
    el.style.display = "block";
    el.textContent = msg;

    const styles = {
        loading: "#cce5ff",
        success: "#d4edda",
        error: "#f8d7da"
    };

    el.style.background = styles[type] || "#d1ecf1";
}

window.generateTrace = function () {

    const input = document.getElementById("program-input").value.trim();

    if (!input) {
        showStatus("Enter your program first", "error");
        return;
    }

    const PROMPT = `
You are an AP CSP program tracing assistant.

Return ONLY JSON:

{
  "input": {"value":"","suggestion":""},
  "loop": {"value":"","suggestion":""},
  "condition": {"value":"","suggestion":""},
  "update": {"value":"","suggestion":""},
  "output": {"value":"","suggestion":""}
}

Rules:
- value = student-ready trace step
- suggestion = improvement tip
- focus on step-by-step program execution

Program:
`;

    showStatus("Generating trace...", "loading");

    queryGemini({
        prompt: PROMPT,
        text: input,
        parseJSON: true
    })
    .then(data => {

        document.getElementById("trace-input").value = data.input?.value || "";
        document.getElementById("trace-loop").value = data.loop?.value || "";
        document.getElementById("trace-condition").value = data.condition?.value || "";
        document.getElementById("trace-update").value = data.update?.value || "";
        document.getElementById("trace-output").value = data.output?.value || "";

        document.getElementById("trace-feedback").innerHTML = `
<h4>AI Suggestions</h4>
<b>Input:</b> ${data.input?.suggestion || ""}<br><br>
<b>Loop:</b> ${data.loop?.suggestion || ""}<br><br>
<b>Condition:</b> ${data.condition?.suggestion || ""}<br><br>
<b>Update:</b> ${data.update?.suggestion || ""}<br><br>
<b>Output:</b> ${data.output?.suggestion || ""}
        `;

        showStatus("Trace generated", "success");
    })
    .catch(() => {

        document.getElementById("trace-feedback").innerHTML =
        "Fallback trace mode active.";

        showStatus("Fallback loaded", "success");
    });
};
</script>