<div align="center">

# 🧬 Motorast-ARC
### Cloud-to-Kaggle Evolutionary Program Synthesis for ARC-AGI-2

**No GPUs. No Neural Networks. No Internet at test time.**
Just a 1MB Python file evolved in the cloud, going to war against 5GB models.

[🔗 Repository](https://github.com/wolffffmohammad1998-svg/Motorast-AI-Discoveries) · [📖 Methodology](#-how-it-works) · [🚀 Kaggle Submission](#-kaggle-submission) · [🏆 The ARC Prize](https://arcprize.org/)

</div>

---

## 🌌 The Problem: Why LLMs Fail at ARC

The **Abstraction and Reasoning Corpus (ARC-AGI-2)** is designed to break Large Language Models. Models like GPT-4 or Gemini have memorized the internet, but they lack true "fluid intelligence." When faced with a novel puzzle they haven't seen before, they hallucinate or fail.

To win ARC, you don't need more *memory* (parameters). You need better *reasoning* (search).

## 🛠 The Solution: The "Cloud-to-Kaggle" Pipeline

This project is a dual-engine system. It separates the **learning phase** (which can use LLMs and the internet) from the **execution phase** (which must be 100% offline and use only pure Python).

1. **The Forge (Cloudflare Worker - Online):**
   A massive evolutionary search engine runs on Cloudflare. It loads ARC training tasks and uses a custom Domain Specific Language (DSL) to evolve programs. It uses a Genetic Algorithm (GA) and breadth-first enumeration to find programs that map inputs to outputs perfectly. LLMs are used *only* as a fallback to suggest new code when the search gets stuck.
2. **The Library (Learned Knowledge):**
   Every successful program is saved into a "Library" (and macro-programs are created from combinations). This library represents the distilled "laws" of the ARC universe.
3. **The Sword (Offline Python):**
   The system exports the entire learned library into a single, standard-library-only Python file (`baseline_solver.py`). This file contains the DSL, the search engine, and the learned programs.
4. **The Arena (Kaggle):**
   We submit the Python file to Kaggle. It runs in a sandbox with **no internet**. It replays the learned programs, performs local searches, and writes `submission.json`.

## 🧠 The DSL (Domain Specific Language)

Instead of letting a model guess pixel by pixel, we search over a discrete space of grid operations:
*   **Geometry:** `rot90`, `flipH`, `flipV`, `transpose`
*   **Objects:** `cropLargest`, `keepColor`, `fillEnclosed`
*   **Logic:** `orLR`, `xorTB`, `symH`, `gravD`
*   **Learned Macros:** `@m1`, `@m2` (programs that solve multiple tasks)

## 🚀 How to Deploy (Cloudflare)

1. Deploy `worker.js` to Cloudflare Workers.
2. Set your `LAB_TOKEN` and LLM API keys in Cloudflare Variables.
3. Open the dashboard, load 30 tasks from GitHub, and turn on **Autopilot**.
4. Let the machine evolve. Watch the Library grow.

## 📦 Kaggle Submission

Once the Library is full of learned programs:
1. Go to the **Export** tab in the dashboard.
2. Download the `.ipynb` notebook (it contains the full library embedded).
3. Import it into Kaggle, turn off the internet, add the ARC dataset, and run it.
4. Submit `submission.json` to the competition.

*Note: The solver uses `attempt_1` and `attempt_2` per test input to maximize the score.*

## 📊 Current Status (Honest Metrics)

*   **Engine:** Genetic Algorithm + BFS Enumeration + DSL.
*   **Dependencies:** None (Standard Python 3 only).
*   **Internet at test time:** Forbidden (Kaggle rule).
*   **Size:** ~1MB.

---
<br>

🇮🇷 **به فارسی:**

**موتوراست-ARC** یک سیستم ترکیبی است که در فضای ابری (کلادفلر) با الگوریتم ژنتیک، برنامه‌نویسی تکاملی انجام می‌دهد و سپس خروجی آن به شکل یک فایل پایتونِ کاملاً آفلاین (بدون نیاز به اینترنت و LLM) به مسابقه کگل فرستاده می‌شود. 

ما به جای اتکا به مدل‌های ۵ گیگابایتی، یک زبان برنامه‌نویسی اختصاصی (DSL) برای گریدها ساختیم و با جستجوی تکاملی، قوانین پنهان پازل‌ها را کشف می‌کنیم. موتور در کلادفلر یاد می‌گیرد، و فایل نهایی (شمشیر) در کگل می‌جنگد.

<div align="center">
<br>
<b>Built from scratch by Mohammad Hossein (Iran 🇮🇷).</b><br>
Zero budget. Zero GPUs. Pure Logic.<br>
<a href="https://github.com/wolffffmohammad1998-svg/Motorast-AI-Discoveries">GitHub Repository</a>
<br><br>
🌱
</div>
