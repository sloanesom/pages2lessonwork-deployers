---
layout: post
microblog: True
breadcrumb: True
title: CPT Collegeboard FRQ Workshop
description: A multi-question AP CSP FRQ practice tool with AI-powered rubric feedback and structured evaluation panels.
author: David M, Sloane S
permalink: /cpt/4
---

## AP CSP FRQ Practice + AI Feedback System

This tool helps you practice AP CSP FRQs by:
- Answering structured exam-style questions
- Tracing program behavior
- Identifying inputs, outputs, lists, and procedures
- Receiving AI rubric-based feedback

Key idea: Each question is evaluated from **multiple grading perspectives**, not just one answer.

---

# =========================
# FRQ 1
# =========================

### CPT FRQ 1 – Program Behavior & Tracing

<link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">
<script src="https://cdn.quilljs.com/1.3.7/quill.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<style>
#output-1 { padding:10px; word-wrap:break-word; overflow-wrap:break-word; }
.controls { margin:10px 0; display:flex; gap:10px; flex-wrap:wrap; }
.control-group { display:flex; flex-direction:column; gap:5px; }
label { font-weight:bold; font-size:14px; }
select, button { padding:8px 12px; border-radius:4px; }
button { background:#007bff; color:white; border:none; cursor:pointer; }
button:hover { background:#0056b3; }
.sample-text { display:none; }
</style>

<details>
<summary><b>FRQ 1 Guide</b></summary>
Trace program execution, identify inputs/outputs, and explain list behavior step-by-step.
</details>

<div id="editor-1" style="height:200px;"></div>

<button id="check-1">Review FRQ 1</button>

<div id="output-1"></div>

<div class="sample-text" data-type="trace">
A program stores a list of quiz scores: [72, 88, 95, 61, 84]

The program loops through each value in the list. For each score, it prints "PASS" if the score is greater than or equal to 70, otherwise it prints "FAIL".

Question:
Describe step-by-step how the program processes the list and determine the exact output that is produced.
</div>

<div class="sample-text" data-type="io">
A program takes a list of user-entered temperatures and outputs the highest, lowest, and average values.
</div>

<div class="sample-text" data-type="logic">
A program checks each element in a list and counts how many values are above a threshold of 50.
</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

const quill1 = new Quill('#editor-1', { theme:'snow' });

document.getElementById("check-1").onclick = function() {
    const text = quill1.getText();
    document.getElementById("output-1").innerText = "Checking FRQ 1...";

    queryGemini({
        prompt: "AP CSP FRQ: Trace program execution. Identify inputs, outputs, and list processing behavior.",
        text
    }).then(r=>{
        document.getElementById("output-1").innerHTML = marked.parse(r.text);
    });
};
</script>

---

# =========================
# FRQ 2
# =========================

### CPT FRQ 2 – Lists, Iteration, and Data Processing

<style>
#output-2 { padding:10px; word-wrap:break-word; overflow-wrap:break-word; }
</style>

<select id="mode-2">
  <option value="list">List Processing</option>
  <option value="filter">Filtering</option>
  <option value="compute">Computation</option>
</select>

<div id="editor-2" style="height:200px;"></div>

<button id="check-2">Review FRQ 2</button>

<div id="output-2"></div>

<div class="sample-text" data-type="list">
A program is designed to analyze daily temperatures stored in a list called temps.

The program:
- Stores temperatures in a list called temps
- Creates a second list called hot_days
- Loops through temps
- Adds temperatures greater than 30 to hot_days
- Outputs the number of items in hot_days

Question:
Explain how the program uses a list, iteration, and selection to process the data and what the final output represents.
</div>

<div class="sample-text" data-type="filter">
A program filters a list of expenses and removes values that exceed a given budget limit.
</div>

<div class="sample-text" data-type="compute">
A program iterates through a list of numbers and computes the sum and average.
</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

const quill2 = new Quill('#editor-2', { theme:'snow' });

document.getElementById("check-2").onclick = function() {
    const text = quill2.getText();
    document.getElementById("output-2").innerText = "Checking FRQ 2...";

    queryGemini({
        prompt: "AP CSP FRQ: Analyze list usage, iteration, filtering, and data processing correctness.",
        text
    }).then(r=>{
        document.getElementById("output-2").innerHTML = marked.parse(r.text);
    });
};
</script>

---

# =========================
# FRQ 3
# =========================

### CPT FRQ 3 – Procedures and Abstraction

<style>
#output-3 { padding:10px; word-wrap:break-word; overflow-wrap:break-word; }
</style>

<select id="mode-3">
  <option value="procedure">Procedures</option>
  <option value="abstraction">Abstraction</option>
  <option value="parameters">Parameters</option>
</select>

<div id="editor-3" style="height:200px;"></div>

<button id="check-3">Review FRQ 3</button>

<div id="output-3"></div>

<div class="sample-text" data-type="procedure">
A programmer creates a procedure to calculate a discounted price for items in a shopping app.

The procedure is defined as:

procedure applyDiscount(price, discountRate)
    return price - (price * discountRate)

The program uses this procedure multiple times with different values for price and discountRate.

Question:
Explain how this procedure works, how parameters are used, and why using a procedure improves the design of the program.
</div>

<div class="sample-text" data-type="abstraction">
A program uses a function to simplify repeated logic and hide complex calculations.
</div>

<div class="sample-text" data-type="parameters">
A procedure takes a list of values and returns the maximum value found in that list.
</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

const quill3 = new Quill('#editor-3', { theme:'snow' });

document.getElementById("check-3").onclick = function() {
    const text = quill3.getText();
    document.getElementById("output-3").innerText = "Checking FRQ 3...";

    queryGemini({
        prompt: "AP CSP FRQ: Analyze procedures, parameters, return values, and abstraction quality.",
        text
    }).then(r=>{
        document.getElementById("output-3").innerHTML = marked.parse(r.text);
    });
};
</script>