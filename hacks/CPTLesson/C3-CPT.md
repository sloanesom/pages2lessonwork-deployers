---
layout: post
microblog: True
tailwind: True
breadcrumb: True
author: David M, Sloane S
permalink: /cpt/3
breadcrumb: True
---

<style>
  /* File-specific styles only - iridescent styles moved to _sass/open-coding/elements/buttons/iridescent.scss */
  .practice-container {
    max-width: 800px;
    margin: 20px auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  }
  
  .reference-card {
    border: 1px solid #6c757d;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .weak-reference {
    border-left: 4px solid #6c757d;
    padding: 15px;
    margin: 10px 0;
    border-radius: 4px;
  }
  
  .practice-textarea {
    width: 100%;
    min-height: 100px;
    padding: 12px;
    border: 1px solid #6c757d;
    border-radius: 4px;
    font-family: 'Times New Roman', serif;
    line-height: 1.6;
    resize: vertical;
  }
  
  .case-title {
    color: #495057;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .button-group {
    display: flex;
    gap: 10px;
    margin-top: 15px;
    flex-wrap: wrap;
  }
  
  .status-message {
    margin: 10px 0;
    padding: 8px;
    border-radius: 4px;
    display: none;
  }
</style>

## Reference Correction Practice

<div class="practice-container">
  <h3>Practice Session: Improve Weak References</h3>
  <p><strong>Instructions:</strong> The references below are incomplete or poorly formatted. Practice improving them using proper APA style. Your improvements will be saved for assessment.</p>
  
  <div class="reference-card">
    <div class="case-title">Case 1: Taylor Swift Copyright Lawsuit</div>

    <div class="weak-reference">
      <strong>❌ Current Weak Reference:</strong><br>
      MSN. (2025). Taylor Swift's legal odyssey: Unpacking the Shake It Off copyright resolution, industry repercussions, and emerging 2025 courtroom dramas.
    </div>
    
    <label for="taylor-reference"><strong>Your Improved Reference:</strong></label>
    <textarea id="taylor-reference" class="practice-textarea" placeholder="Write an improved APA reference here. Include proper author, date, title formatting, publication, and URL if available..."></textarea>
    
    <div class="button-group">
      <button id="save-taylor" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">💾 Save Taylor Swift Reference</button>
      <button id="load-taylor" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">📂 Load Saved Work</button>
    </div>
  </div>
  
  <div class="reference-card">
    <div class="case-title">Case 2: Pete Hegseth Academic Misconduct</div>

    <div class="weak-reference">
      <strong>❌ Current Weak Reference:</strong><br>
      News source on 2025 academic misconduct cases.
    </div>
    
    <label for="pete-reference"><strong>Your Improved Reference:</strong></label>
    <textarea id="pete-reference" class="practice-textarea" placeholder="Write an improved APA reference here. This reference is extremely weak - you'll need to create a proper citation with author, date, title, publication, and URL..."></textarea>
    
    <div class="button-group">
      <button id="save-pete" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">💾 Save Pete Hegseth Reference</button>
      <button id="load-pete" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">📂 Load Saved Work</button>
    </div>
  </div>
  
  <div class="button-group">
    <button id="test-mode-c3" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">🧪 Test Mode - Fill References</button>
    <button id="save-all" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">📤 Save All for Assessment</button>
    <button id="clear-all" class="iridescent flex-1 text-white text-center py-2 rounded-lg font-semibold transition">🗑️ Clear All Work</button>
  </div>
  
  <div id="practice-status" class="status-message"></div>
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {

    // Status message helper function
    function showStatusMessage(message, type) {
        const statusDiv = document.getElementById("practice-status");
        statusDiv.textContent = message;
        statusDiv.style.display = "block";

        // Style based on message type
        switch(type) {
            case "success":
                statusDiv.style.backgroundColor = "#d1ecf1";
                statusDiv.style.color = "#0c5460";
                statusDiv.style.border = "1px solid #bee5eb";
                break;
            case "error":
                statusDiv.style.backgroundColor = "#e9ecef";
                statusDiv.style.color = "#495057";
                statusDiv.style.border = "1px solid #6c757d";
                break;
            case "warning":
                statusDiv.style.backgroundColor = "#e2e3e5";
                statusDiv.style.color = "#383d41";
                statusDiv.style.border = "1px solid #adb5bd";
                break;
            case "info":
                statusDiv.style.backgroundColor = "#d1ecf1";
                statusDiv.style.color = "#0c5460";
                statusDiv.style.border = "1px solid #bee5eb";
                break;
        }

        // Auto-hide after 4 seconds
        setTimeout(() => {
            statusDiv.style.display = "none";
        }, 4000);
    }

    // Test Mode - Fill all references with sample data
    document.getElementById("test-mode-c3").onclick = function() {
        if (confirm("This will fill both reference corrections with sample data for testing. Continue?")) {
            // Taylor Swift Reference Correction
            document.getElementById("taylor-reference").value = `Marasco, K. (2025, April 15). Copyright infringement lawsuit against Taylor Swift. Entertainment Law Review, 45(8), 123-135. https://doi.org/10.1234/elr.2025.45.8.123`;
            
            // Pete Hegseth Reference Correction  
            document.getElementById("pete-reference").value = `Princeton University Academic Integrity Office. (2025, May 20). Investigation findings: Senior thesis plagiarism case. Princeton Academic Review, 78(3), 45-52. https://www.princeton.edu/academic-integrity/cases/2025-hegseth`;

            showStatusMessage("🧪 Test mode activated! Both references filled with corrected APA format.", "info");
        }
    };

    // Save Taylor Swift Reference
    document.getElementById("save-taylor").onclick = function() {
        const reference = document.getElementById("taylor-reference").value.trim();

        if (reference.length === 0) {
            showStatusMessage("⚠️ Please write a reference before saving", "warning");
            return;
        }

        try {
            localStorage.setItem('plagiarism-c3-1', JSON.stringify({
                title: 'Taylor Swift Copyright Lawsuit',
                originalReference: 'MSN. (2025). Taylor Swift\'s legal odyssey: Unpacking the Shake It Off copyright resolution, industry repercussions, and emerging 2025 courtroom dramas.',
                correctedReference: reference,
                timestamp: new Date().toISOString(),
                exercise: 'Reference Correction - Taylor Swift Case'
            }));
            showStatusMessage("✅ Taylor Swift reference saved successfully!", "success");
        } catch (error) {
            showStatusMessage("❌ Failed to save: " + error.message, "error");
        }
    };

    // Load Taylor Swift Reference
    document.getElementById("load-taylor").onclick = function() {
        try {
            const saved = localStorage.getItem('plagiarism-c3-1');
            if (saved) {
                const data = JSON.parse(saved);
                document.getElementById("taylor-reference").value = data.correctedReference || data.content || '';
                const saveDate = new Date(data.timestamp).toLocaleString();
                showStatusMessage(`✅ Taylor Swift reference loaded! (Saved: ${saveDate})`, "success");
            } else {
                showStatusMessage("⚠️ No saved Taylor Swift reference found", "warning");
            }
        } catch (error) {
            showStatusMessage("❌ Failed to load: " + error.message, "error");
        }
    };

    // Save Pete Hegseth Reference
    document.getElementById("save-pete").onclick = function() {
        const reference = document.getElementById("pete-reference").value.trim();

        if (reference.length === 0) {
            showStatusMessage("⚠️ Please write a reference before saving", "warning");
            return;
        }

        try {
            localStorage.setItem('plagiarism-c3-2', JSON.stringify({
                title: 'Pete Hegseth Academic Misconduct',
                originalReference: 'News source on 2025 academic misconduct cases.',
                correctedReference: reference,
                timestamp: new Date().toISOString(),
                exercise: 'Reference Correction - Pete Hegseth Case'
            }));
            showStatusMessage("✅ Pete Hegseth reference saved successfully!", "success");
        } catch (error) {
            showStatusMessage("❌ Failed to save: " + error.message, "error");
        }
    };

    // Load Pete Hegseth Reference
    document.getElementById("load-pete").onclick = function() {
        try {
            const saved = localStorage.getItem('plagiarism-c3-2');
            if (saved) {
                const data = JSON.parse(saved);
                document.getElementById("pete-reference").value = data.correctedReference || data.content || '';
                const saveDate = new Date(data.timestamp).toLocaleString();
                showStatusMessage(`✅ Pete Hegseth reference loaded! (Saved: ${saveDate})`, "success");
            } else {
                showStatusMessage("⚠️ No saved Pete Hegseth reference found", "warning");
            }
        } catch (error) {
            showStatusMessage("❌ Failed to load: " + error.message, "error");
        }
    };

    // Save All for Assessment
    document.getElementById("save-all").onclick = function() {
        const taylorRef = document.getElementById("taylor-reference").value.trim();
        const peteRef = document.getElementById("pete-reference").value.trim();

        if (taylorRef.length === 0 || peteRef.length === 0) {
            showStatusMessage("⚠️ Please complete both references before saving for assessment", "warning");
            return;
        }

        try {
            // Save consolidated assessment data
            const assessmentData = {
                lesson: 'C3-practice_reference_correction',
                studentWork: {
                    taylorSwiftReference: taylorRef,
                    peteHegsethReference: peteRef
                },
                timestamp: new Date().toISOString(),
                completed: true
            };

            localStorage.setItem('plagiarism-c3-assessment', JSON.stringify(assessmentData));
            
            // Also save individual exercises for C5 compatibility
            localStorage.setItem('plagiarism-c3-1', JSON.stringify({
                title: 'Taylor Swift Copyright Lawsuit',
                originalReference: 'MSN. (2025). Taylor Swift\'s legal odyssey: Unpacking the Shake It Off copyright resolution, industry repercussions, and emerging 2025 courtroom dramas.',
                correctedReference: taylorRef,
                timestamp: new Date().toISOString(),
                exercise: 'Reference Correction - Taylor Swift Case'
            }));
            
            localStorage.setItem('plagiarism-c3-2', JSON.stringify({
                title: 'Pete Hegseth Academic Misconduct',
                originalReference: 'News source on 2025 academic misconduct cases.',
                correctedReference: peteRef,
                timestamp: new Date().toISOString(),
                exercise: 'Reference Correction - Pete Hegseth Case'
            }));
            
            showStatusMessage("🎓 All references saved for instructor assessment!", "success");
        } catch (error) {
            showStatusMessage("❌ Failed to save for assessment: " + error.message, "error");
        }
    };

    // Clear All Work
    document.getElementById("clear-all").onclick = function() {
        if (confirm("Are you sure you want to clear all your work? This cannot be undone.")) {
            document.getElementById("taylor-reference").value = "";
            document.getElementById("pete-reference").value = "";

            // Clear individual saves
            localStorage.removeItem('plagiarism-c3-1');
            localStorage.removeItem('plagiarism-c3-2');
            localStorage.removeItem('plagiarism-c3-assessment');

            showStatusMessage("🗑️ All work cleared", "info");
        }
    };

    // Auto-load saved work on page load
    document.getElementById("load-taylor").click();
    document.getElementById("load-pete").click();
});
</script>
