---
layout: post
microblog: True
title: CPT Project Layout Builder
description: A drafting tool that helps students map their CPT project to AP CSP requirements (input, output, lists, procedures, and algorithms).
author: David M, Sloane S
permalink: /cpt/2
breadcrumb: True
---

## CPT Requirements Overview

The Create Performance Task (CPT) requires you to build a program and explain how it works.

Your program MUST include:
- Input: user interaction (typing, clicking, etc.)
- Output: result displayed to the user
- List: used to store multiple related pieces of data
- Procedure: a function with at least one parameter (variable that receives input)
- Algorithm: must include sequencing, selection (if), and iteration (loop)

Key idea: You are graded on whether these parts are clearly shown and explained.

---

<style>
  .apa-tool-label {
    display: block;
    margin-top: 8px;
    font-weight: bold;
    color: #333;
  }

  .apa-tool-input {
    width: 90%;
    padding: 8px;
    margin-bottom: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 14px;
  }

  .apa-tool-output {
    margin-top: 16px;
    border-left: 4px solid #007bff;
    padding: 15px;
    font-family: 'Times New Roman', serif;
    line-height: 1.6;
    border-radius: 4px;
  }

  .citation-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }
</style>

<details style="padding: 15px; border-radius: 8px; margin-bottom: 20px; border-left: 4px solid #007bff ">
  <summary style="cursor: pointer; font-weight: bold; color: #007bff; font-size: 18px;">
    CPT Builder Guide (Click to expand)
  </summary>

  <div style="margin-top: 15px;">
    <h4>Purpose</h4>
    <p>This tool helps you break down your CPT project into AP CSP requirements.</p>

    <h4>How to Use</h4>
    <ol>
      <li>Write your CPT project idea</li>
      <li>Click generate to auto-fill structure</li>
      <li>Review and edit each field</li>
      <li>Save your progress</li>
    </ol>

    <h4>CPT Requirements</h4>
    <ul>
      <li><strong>Input:</strong> User interaction</li>
      <li><strong>Output:</strong> Program result</li>
      <li><strong>List:</strong> Stored collection of data</li>
      <li><strong>Procedure:</strong> Function with parameter</li>
      <li><strong>Algorithm:</strong> Must include sequencing, selection, iteration</li>
    </ul>
  </div>
</details>

<div class="citation-container">

  <h3>CPT Project Layout Builder</h3>

  <!-- AI SECTION -->
  <div style="padding: 15px; border-radius: 6px; margin-bottom: 20px; border: 1px solid #dee2e6;">
    <h4 style="margin-top: 0;">AI CPT Idea Helper</h4>

    <label class="apa-tool-label">Project Idea:</label>
    <textarea class="apa-tool-input" id="user-provided-quote"
      placeholder="Describe your CPT project idea..."
      style="min-height: 80px; resize: vertical;"></textarea>

    <div style="display: flex; gap: 10px; flex-wrap: wrap;">
      <button onclick="generateCPTStructure()"
        class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">
        🔍 Generate CPT Structure
      </button>

      <button onclick="saveCurrentCitation()"
        class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition"
        style="background-color: #28a745;">
        💾 Save
      </button>

      <button onclick="loadSavedCitation()"
        class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition"
        style="background-color: #17a2b8;">
        📂 Load
      </button>
    </div>

    <div id="ai-status" style="margin-top:10px;padding:8px;border-radius:4px;display:none;"></div>
  </div>

  <!-- CPT FIELDS -->
  <h4>Manual CPT Builder</h4>

  <label class="apa-tool-label">Input:</label>
  <input class="apa-tool-input" id="cpt-input" type="text">

  <label class="apa-tool-label">Output:</label>
  <input class="apa-tool-input" id="cpt-output" type="text">

  <label class="apa-tool-label">List:</label>
  <input class="apa-tool-input" id="cpt-list" type="text">

  <label class="apa-tool-label">Procedure:</label>
  <input class="apa-tool-input" id="cpt-procedure" type="text">

  <label class="apa-tool-label">Algorithm:</label>
  <input class="apa-tool-input" id="cpt-algorithm" type="text">

  <div class="apa-tool-output" id="cpt-output-box">
    <strong>Generated CPT Layout:</strong><br>
    <span id="cpt-layout-text"></span>
  </div>

</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

function showCPTStatus(message, type) {
    const el = document.getElementById("ai-status");
    if (!el) return;

    el.textContent = message;
    el.style.display = "block";

    const styles = {
        loading: ["#cce5ff", "#004085", "#99d3ff"],
        success: ["#d1ecf1", "#0c5460", "#bee5eb"],
        error: ["#f8d7da", "#721c24", "#f5c6cb"]
    };

    const s = styles[type] || styles.success;

    el.style.backgroundColor = s[0];
    el.style.color = s[1];
    el.style.border = "1px solid " + s[2];

    if (type !== "loading") {
        setTimeout(() => el.style.display = "none", 5000);
    }
}

window.generateCPTStructure = function () {

    const idea = document.getElementById("user-provided-quote")?.value.trim();
    if (!idea) {
        showCPTStatus("⚠️ Enter your CPT idea first", "error");
        return;
    }

    const PROMPT = `
Return ONLY JSON with:
input, output, list, procedure, algorithm.

Rules:
- input = user interaction
- output = result
- list = stored data
- procedure = function with parameter
- algorithm = must include loop + if + sequencing

Project:
`;

    showCPTStatus("🧠 Generating CPT structure...", "loading");

    queryGemini({
        prompt: PROMPT,
        text: idea,
        parseJSON: true
    })
    .then(data => {

        const set = (id, val) => {
            const el = document.getElementById(id);
            if (el && val) el.value = val;
        };

        set("cpt-input", data.input);
        set("cpt-output", data.output);
        set("cpt-list", data.list);
        set("cpt-procedure", data.procedure);
        set("cpt-algorithm", data.algorithm);

        showCPTStatus("✅ CPT generated", "success");
    })
    .catch(() => {

        document.getElementById("cpt-input").value = "User interacts with system";
        document.getElementById("cpt-output").value = "System displays results";
        document.getElementById("cpt-list").value = "Stores user data";
        document.getElementById("cpt-procedure").value = "function process(input)";
        document.getElementById("cpt-algorithm").value =
`FOR each item:
 IF condition:
  update result
 ENDIF
ENDFOR`;

        showCPTStatus("📚 Fallback loaded", "success");
    });
};

</script>