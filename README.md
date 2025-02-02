# Practice-Math-with-Emacs
**Development Plan: Emacs-Based AI Math Solver on Arch Linux**

## **Overview**
This project will transform Emacs into an intelligent math-solving assistant that dynamically generates problems, tracks progress, checks answers using AI, and requeues unsolved problems for later attempts. It will leverage C++ for performance-critical operations, Python for symbolic computation and API integration, Emacs Lisp for UI and workflow inside Emacs, and external problem sources like Khan Academy.

---

## **Tech Stack & Tools**
- **Arch Linux**: Development environment
- **Emacs**: Primary UI and workflow
- **C++**: Efficient problem queueing and difficulty scaling
- **Python**: Symbolic computation (SymPy) and API handling
- **Emacs Lisp**: Frontend UI inside Emacs
- **LaTeX**: Typeset solutions for clean formatting
- **Org-mode**: Data storage and question display
- **Khan Academy API**: External problem source

---

## **Key Features & Implementation**

### **1. Question Generation & Queueing Mechanics**
- **Adaptive Question Difficulty**
  - Initial difficulty starts at a default level.
  - Solved quickly → Increase difficulty.
  - Solved slowly or incorrect → Lower difficulty and requeue.
- **Queueing System**
  - Maintain an in-memory queue for problems.
  - Store unsolved problems in a file (\`math-queue.org\`) for later retry.
  - Use a **C++ priority queue** for optimized problem selection.
- **Data Sources for Questions**
  - **Khan Academy API**: Fetch problem sets dynamically.
  - **Predefined Database**: Manually curated problems in a local file.
  - **Auto-Generated Problems**: Python script using SymPy.
  - **Incorrectly Answered Problems**: Problems requeued from \`incorrect-queue.org\`.

---

### **2. Khan Academy API Integration**
- **Retrieve Math Problems Programmatically**
  - Fetch structured math problem sets legally via the Khan Academy API.
  - Process JSON-formatted data to extract relevant problems.
  - Filter problems based on topics (e.g., algebra, calculus, probability).
- **Integration Strategy**
  - Python handles API requests and data parsing.
  - Store fetched problems in \`questions.txt\` for C++ queue processing.
  - Cache-fetched problems to reduce repeated API calls.

---

### **3. LaTeX Answer Formatting & DeepSeek AI Verification**
- **User writes answers in LaTeX within Emacs Org-mode.**
- **Answers are saved and sent to DeepSeek AI for verification.**
- **If correct:** Mark as solved and move to next.
- **If incorrect:** Requeue the problem and adjust the difficulty.
- **Components Involved:**
  - **Emacs Lisp:** UI for writing and submitting answers.
  - **Python:** Processes LaTeX input and sends it to DeepSeek AI.
  - **API Request Handling:** Sends user input and receives AI feedback.

---

### **4. Retry Mechanism & Adaptive Learning**
- **Incorrect answers automatically requeue with a lower difficulty.**
- **Track user performance to refine future problem selection.**
- **Use metadata (time taken, attempts, accuracy) to optimize problem difficulty.**
- **Ensure integration with Org-mode to review past mistakes.**

---

## **Development Roadmap**

| **Phase**   | **Task** | **Implementation** |
|------------|---------|------------------|
| **1. Setup** | Configure Emacs on Arch | Install Emacs, Python, C++, LaTeX, Org-mode |
| **2. UI** | Emacs Lisp UI | Create Org-mode based question display |
| **3. Queue System** | Implement problem queue | C++ priority queue for problems |
| **4. Khan API Integration** | Retrieve math problems | Python handles API requests |
| **5. Answer Checking** | LaTeX formatting + AI verification | Python script for DeepSeek API |
| **6. Adaptive Learning** | Track user performance | Modify queue system for difficulty scaling |
| **7. Final Integration** | Connect all components | Ensure smooth workflow between C++, Python, and Emacs Lisp |

---

## **Final Features**
- [ ] **Emacs UI for displaying questions**  
- [ ] **C++ Problem Queue for efficient problem selection**  
- [ ] **Python Khan Academy API Handler for dynamic problem retrieval**  
- [ ] **Python DeepSeek AI Checker for answer validation**  
- [ ] **LaTeX-based Answer Formatting for clean solution representation**  
- [ ] **Adaptive Difficulty & Learning Mechanism**  
