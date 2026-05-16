---
layout: post
microblog: True
breadcrumb: True
title: CPT Project Idea and Purpose 
description: A tool to help students brainstorm and refine their CPT project ideas and purpose.  
author: David M, Sloane S
permalink: /cpt/1
---

## Evaluate Sample Paragraphs

Spend time individually and as a pair adjusting your paragraph using this tool.  Progress though plagiarism, these building, and 5-paragraph essay or resarch paper.  

Review work an progress with advanced cohort.

### Gemini Citation Helper

<link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">
<script src="https://cdn.quilljs.com/1.3.7/quill.min.js"></script>

<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

<style>
/* Target the output container */
#output {
    padding: 10px;
    word-wrap: break-word;
    overflow-wrap: break-word;
}

.controls {
    margin: 10px 0;
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    align-items: center;
}

.control-group {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

label {
    font-weight: bold;
    font-size: 14px;
}

select {
    padding: 8px 12px;
    border-radius: 4px;
    border: 1px solid #ccc;
    color: white;
    background-color: #333;
}

button {
    padding: 8px 12px;
    border-radius: 4px;
    border: 1px solid #ccc;
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

.sample-text {
    display: none;
}
</style>

<details style="padding: 15px; border-radius: 8px; margin-bottom: 20px; border-left: 4px solid #007bff;">
  <summary style="cursor: pointer; font-weight: bold; color: #007bff; font-size: 18px;">Writing Helper (Click to see guide)</summary>
  <div style="margin-top: 10px;">
    <p>This writing analysis tool helps you improve your academic writing by providing AI-powered feedback on different aspects of your text.</p>

    <h4>Analysis Modes:</h4>
    <ul>
      <li><strong>Plagiarism Check:</strong> Identifies missing citations and suggests proper APA references</li>
      <li><strong>Thesis Building:</strong> Evaluates thesis clarity, argument structure, and coherence</li>
      <li><strong>5-Paragraph Outline:</strong> Checks essay structure and paragraph organization</li>
      <li><strong>Research Paper:</strong> Assesses academic tone, evidence quality, and scholarly writing</li>
    </ul>
    
    <p><em>Note: Sample texts are provided for each mode to help you explore different types of feedback. You can replace them with your own writing.</em></p>
  </div>
</details>

<div class="controls">
    <div class="control-group">
        <select id="analysisMode">
            <option value="plagiarism">Plagiarism Check</option>
            <option value="thesis">Thesis Building</option>
            <option value="five-paragraph">5-Paragraph Outline</option>
            <option value="research">Research Paper</option>
        </select>
    </div>
    <div class="control-group">
        <button id="saveBtn" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">💾 Save Draft</button>
        <button id="loadBtn" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">📂 Load Draft</button>
    </div>
</div>

<div id="quill-editor" style="height: 200px;"></div>
<div class="controls">
    <button id="test-mode-c4" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">🧪 Test Mode - Fill Editor</button>
    <button id="checkBtn" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">🔍 Analyze Text</button>
    <button id="submitBtn" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition" style="background-color: #28a745;" disabled>📤 Submit for Grading</button>
</div>
<div id="status-message" style="margin: 10px 0; padding: 8px; border-radius: 4px; display: none;"></div>
<div id="output"></div>

<!-- Hidden sample CPT idea texts (UPDATED) -->
<div class="sample-text" data-type="plagiarism">
My CPT project is a School Club Finder. The purpose of my program is to help students find clubs, meeting times, and locations. Users can search for clubs and see basic information about each club.
</div>

<div class="sample-text" data-type="plagiarism">
My CPT project is a Fast Food Comparison Tool. The purpose of my program is to help users compare food items based on price, calories, and ratings. Users can select meals and see which option is best for them.
</div>

<div class="sample-text" data-type="plagiarism">
My CPT project is a Homework Tracker. The purpose of my program is to help students organize assignments, due dates, and classwork. Users can add tasks and mark them as complete when finished.
</div>

<div class="sample-text" data-type="thesis">
My CPT project is a Study Planner that helps students organize their study schedule. Users can add assignments, plan study sessions, and track what they need to complete each day.
</div>

<div class="sample-text" data-type="five-paragraph">
My CPT project is a Quiz Practice App that helps students study by answering questions and tracking their score. Users can take quizzes and review their mistakes to improve.
</div>

<div class="sample-text" data-type="research">
My CPT project is a Fitness Tracker that helps users log workouts and track progress over time. Users can record exercises and view their improvement.
</div>

<script type="module">
    // Import the new modular API
    import { queryGemini } from '{{ site.baseurl }}/assets/js/api/gemini.js';

    const ANALYSIS_PROMPTS = {
        plagiarism: "Please look at this text for correct academic reference, document citations, and make recommendations for each area of concern: ",
        thesis: "Please analyze this text for thesis development. Check for clear thesis statement, supporting arguments, and overall coherence: ",
        "five-paragraph": "Please analyze this text for 5-paragraph essay structure. Check for introduction with thesis, three body paragraphs with supporting details, and conclusion: ",
        research: "Please analyze this text for research paper quality. Check for proper academic tone, evidence-based arguments, and scholarly writing style: "
    };

    document.addEventListener("DOMContentLoaded", function() {
        var quill = new Quill('#quill-editor', {
            theme: 'snow'
        });

        // Load a random sample on page load
        loadRandomSample();

        // Test Mode - Fill editor with sample text
        document.getElementById("test-mode-c4").onclick = function() {
            if (confirm("This will fill the editor with sample text for testing. Continue?")) {
                const sampleText = `
Artificial intelligence is transforming education by providing personalized learning experiences. Many educators are exploring how AI can enhance traditional teaching methods.
`;
                quill.setText(sampleText);
                document.getElementById("submitBtn").disabled = false;
                showStatusMessage("🧪 Test mode activated!", "info");
            }
        };

        document.getElementById("saveBtn").onclick = function() {
            const text = quill.getContents();
            const plainText = quill.getText();
            const mode = document.getElementById("analysisMode").value;

            const draft = {
                content: text,
                plainText: plainText,
                mode: mode,
                timestamp: new Date().toISOString(),
                id: 'writing-draft-v1'
            };

            localStorage.setItem('plagiarism-writing-draft', JSON.stringify(draft));
            showStatusMessage("Draft saved!", "success");
        };

        document.getElementById("loadBtn").onclick = function() {
            const savedDraft = localStorage.getItem('plagiarism-writing-draft');

            if (savedDraft) {
                const draft = JSON.parse(savedDraft);
                quill.setContents(draft.content);
                showStatusMessage("Draft loaded!", "success");
            } else {
                showStatusMessage("No draft found", "warning");
            }
        };

        document.getElementById("checkBtn").onclick = function() {
            const text = quill.getText();
            const mode = document.getElementById("analysisMode").value;

            document.getElementById("output").textContent = "Analyzing...";

            queryGemini({
                prompt: ANALYSIS_PROMPTS[mode],
                text: text
            })
            .then(result => {
                document.getElementById("output").innerHTML = marked.parse(result.text);
                showStatusMessage("Analysis complete!", "success");
            })
            .catch(err => {
                showStatusMessage("Error analyzing text", "error");
            });
        };

        function loadRandomSample() {
            const samples = document.querySelectorAll('.sample-text[data-type="plagiarism"]');
            const pick = Math.floor(Math.random() * samples.length);
            quill.setText(samples[pick].textContent.trim());
        }

        function showStatusMessage(msg, type) {
            const el = document.getElementById("status-message");
            el.textContent = msg;
            el.style.display = "block";
            setTimeout(() => el.style.display = "none", 3000);
        }

        loadRandomSample();
    });
</script>