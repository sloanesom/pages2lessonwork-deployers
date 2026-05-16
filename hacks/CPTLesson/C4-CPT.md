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

<link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">
<script src="https://cdn.quilljs.com/1.3.7/quill.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<style>
.container {
    max-width: 900px;
    margin: auto;
    padding: 20px;
}

.frq-box {
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 25px;
}

.answer-box {
    width: 100%;
    min-height: 120px;
    padding: 10px;
    border-radius: 6px;
    border: 1px solid #ccc;
}

.ai-panel {
    margin-top: 10px;
    padding: 10px;
    border-left: 4px solid #007bff;
    background: #f8f9fa;
}
</style>

<div class="container">

## FRQ QUESTION 1 — Program Behavior Trace

**Prompt:**  
A student writes a program that loops through a list of numbers and sums only values greater than 10.

Explain step-by-step how this program executes.

<textarea id="q1-input" class="answer-box"></textarea>

<button onclick="runQ1()">🧠 Analyze Question 1</button>

<div id="q1-a1" class="ai-panel"></div>
<div id="q1-a2" class="ai-panel"></div>
<div id="q1-a3" class="ai-panel"></div>

---

## FRQ QUESTION 2 — Input / Output / List Identification

**Prompt:**  
Given a social media app, identify:
- Input
- Output
- List usage
- Procedure purpose

<textarea id="q2-input" class="answer-box"></textarea>

<button onclick="runQ2()">🧠 Analyze Question 2</button>

<div id="q2-a1" class="ai-panel"></div>
<div id="q2-a2" class="ai-panel"></div>
<div id="q2-a3" class="ai-panel"></div>

---

## FRQ QUESTION 3 — Algorithm + Logic Reasoning

**Prompt:**  
A program checks if a student passes a quiz:
- If score ≥ 70 → pass
- Else → fail  
It repeats for multiple students.

Explain how the algorithm works step-by-step.

<textarea id="q3-input" class="answer-box"></textarea>

<button onclick="runQ3()">🧠 Analyze Question 3</button>

<div id="q3-a1" class="ai-panel"></div>
<div id="q3-a2" class="ai-panel"></div>
<div id="q3-a3" class="ai-panel"></div>

</div>

<script type="module">
import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

function render(id, text) {
    document.getElementById(id).innerHTML = marked.parse(text || "");
}

/* ---------------- Q1 ---------------- */
window.runQ1 = function () {
    const text = document.getElementById("q1-input").value;

    const P1 = "Check correctness of program trace step-by-step. Identify logical errors.";
    const P2 = "Explain execution clearly like AP CSP scoring rubric. Focus on reasoning.";
    const P3 = "Give improvement suggestions and exam tips.";

    queryGemini({ prompt: P1, text }).then(r => render("q1-a1", r.text));
    queryGemini({ prompt: P2, text }).then(r => render("q1-a2", r.text));
    queryGemini({ prompt: P3, text }).then(r => render("q1-a3", r.text));
};

/* ---------------- Q2 ---------------- */
window.runQ2 = function () {
    const text = document.getElementById("q2-input").value;

    const P1 = "Identify input, output, list, and procedure usage clearly.";
    const P2 = "Check correctness against AP CSP Create Task rubric.";
    const P3 = "Suggest missing components or weak areas.";

    queryGemini({ prompt: P1, text }).then(r => render("q2-a1", r.text));
    queryGemini({ prompt: P2, text }).then(r => render("q2-a2", r.text));
    queryGemini({ prompt: P3, text }).then(r => render("q2-a3", r.text));
};

/* ---------------- Q3 ---------------- */
window.runQ3 = function () {
    const text = document.getElementById("q3-input").value;

    const P1 = "Trace algorithm step-by-step with loop and condition analysis.";
    const P2 = "Evaluate correctness and logical structure.";
    const P3 = "Explain how to improve for AP CSP scoring.";

    queryGemini({ prompt: P1, text }).then(r => render("q3-a1", r.text));
    queryGemini({ prompt: P2, text }).then(r => render("q3-a2", r.text));
    queryGemini({ prompt: P3, text }).then(r => render("q3-a3", r.text));
};

</script>