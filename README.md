# Helixha.LoveJar.oi
This is a love jar for Bence (A digital gift). This is also a just because gift for him. LoveJar.oi HTML web/app 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Reasons I Love You- for Bence</title>
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #fff0f5 0%, #ffe4e1 100%);
      --primary: #e11d48;
      --primary-hover: #be123c;
      --jar-glass: rgba(255, 255, 255, 0.55);
      --jar-border: rgba(255, 255, 255, 0.85);
      --text-dark: #331d2c;
      --note-bg: #fffdf7;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Balonku', Alex-Brush, Pacifico, Tangelo;
    }

    body {
      min-height: 100vh;
      background: var(--bg-gradient);
      color: var(--text-dark);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      overflow-x: hidden;
    }

    header {
      text-align: center;
      margin-bottom: 24px;
    }

    h1 {
      font-size: 2.2rem;
      color: var(--primary);
      margin-bottom: 6px;
      letter-spacing: -0.5px;
    }

    p.subtitle {
      font-size: 1rem;
      opacity: 0.8;
    }

    /* Jar Container */
    .jar-wrapper {
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
      cursor: pointer;
      user-select: none;
      margin: 10px 0 28px;
      transition: transform 0.2s ease;
    }

    .jar-wrapper:hover {
      transform: scale(1.03);
    }

    .jar-wrapper:active {
      transform: scale(0.97);
    }

    .jar-lid {
      width: 130px;
      height: 24px;
      background: linear-gradient(90deg, #d97706, #fbbf24, #d97706);
      border-radius: 6px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.12);
      z-index: 2;
    }

    .jar-neck {
      width: 116px;
      height: 18px;
      background: var(--jar-glass);
      border-left: 3px solid var(--jar-border);
      border-right: 3px solid var(--jar-border);
    }

    .jar-body {
      width: 210px;
      height: 260px;
      background: var(--jar-glass);
      border: 4px solid var(--jar-border);
      border-radius: 36px 36px 44px 44px;
      box-shadow: 0 18px 35px rgba(225, 29, 72, 0.12), inset 0 0 25px rgba(255, 255, 255, 0.7);
      position: relative;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* Decorative Paper Folded Notes inside the Jar */
    .paper-scrap {
      position: absolute;
      width: 44px;
      height: 22px;
      border-radius: 4px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.08);
      transition: transform 0.4s ease;
    }

    .jar-label {
      background: #fff;
      padding: 10px 18px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.08);
      border: 1px dashed #fda4af;
      z-index: 3;
      text-align: center;
      pointer-events: none;
    }

    .jar-label span {
      display: block;
      font-weight: 700;
      color: var(--primary);
      font-size: 0.95rem;
    }

    .jar-label small {
      font-size: 0.75rem;
      color: #6b7280;
    }

    /* Shake Animation */
    @keyframes shake {
      0%, 100% { transform: rotate(0deg); }
      20% { transform: rotate(-6deg); }
      40% { transform: rotate(6deg); }
      60% { transform: rotate(-4deg); }
      80% { transform: rotate(4deg); }
    }

    .shake {
      animation: shake 0.45s ease-in-out;
    }

    /* Buttons */
    .controls {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      justify-content: center;
    }

    button {
      border: none;
      padding: 12px 22px;
      border-radius: 999px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    }

    .btn-primary {
      background: var(--primary);
      color: white;
    }

    .btn-primary:hover {
      background: var(--primary-hover);
      transform: translateY(-2px);
    }

    .btn-secondary {
      background: white;
      color: var(--text-dark);
    }

    .btn-secondary:hover {
      background: #fff1f2;
      transform: translateY(-2px);
    }

    /* Note Popup Modal */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(51, 29, 44, 0.5);
      backdrop-filter: blur(4px);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 20px;
      z-index: 50;
    }

    .modal-overlay.active {
      display: flex;
    }

    .note-card {
      background: var(--note-bg);
      max-width: 420px;
      width: 100%;
      padding: 32px 28px;
      border-radius: 18px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
      text-align: center;
      position: relative;
      border-top: 8px solid var(--primary);
      animation: popIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    @keyframes popIn {
      from { opacity: 0; transform: scale(0.85) translateY(15px); }
      to { opacity: 1; transform: scale(1) translateY(0); }
    }

    .note-number {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 1.5px;
      color: #9ca3af;
      margin-bottom: 12px;
      display: block;
    }

    .note-text {
      font-size: 1.35rem;
      line-height: 1.5;
      color: var(--text-dark);
      margin-bottom: 24px;
      font-weight: 500;
    }

    /* Customize Drawer / Modal */
    .editor-card {
      background: white;
      max-width: 500px;
      width: 100%;
      max-height: 85vh;
      overflow-y: auto;
      padding: 24px;
      border-radius: 18px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
    }

    .editor-card h2 {
      color: var(--primary);
      margin-bottom: 8px;
    }

    .editor-card p {
      font-size: 0.9rem;
      color: #6b7280;
      margin-bottom: 16px;
    }

    .input-group {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 18px;
    }

    input[type="text"], textarea {
      width: 100%;
      padding: 10px 14px;
      border: 1px solid #e5e7eb;
      border-radius: 10px;
      font-size: 0.95rem;
    }

    textarea {
      resize: vertical;
      min-height: 70px;
    }

    .reasons-list {
      list-style: none;
      margin-top: 14px;
      display: flex;
      flex-direction: column;
      gap: 8px;
      max-height: 220px;
      overflow-y: auto;
      padding-right: 4px;
    }

    .reasons-list li {
      background: #f9fafb;
      padding: 10px 12px;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      font-size: 0.9rem;
    }

    .delete-btn {
      background: #fee2e2;
      color: #dc2626;
      padding: 4px 10px;
      font-size: 0.8rem;
      border-radius: 6px;
      box-shadow: none;
    }

    .delete-btn:hover {
      background: #fecaca;
    }
  </style>
</head>
<body>

  <header>
    <h1 id="pageTitle">Reasons I Love You</h1>
    <p class="subtitle" id="pageSubtitle">Tap the jar!:3</p>
  </header>

  <div class="jar-wrapper" id="jar" onclick="pickReason()">
    <div class="jar-lid"></div>
    <div class="jar-neck"></div>
    <div class="jar-body" id="jarBody">
      <div class="jar-label">
        <span>Tap to Open</span>
        <medium id="counterText">1000 notes inside</medium>
      </div>
    </div>
  </div>

  <div class="controls">
    <button class="btn-primary" onclick="pickReason()">Pull a Note <3</button>
    <button class="btn-secondary" onclick="openEditor()">Customize Notes ✏️</button>
  </div>

  <!-- Note Display Modal -->
  <div class="modal-overlay" id="noteModal" onclick="closeNoteModal(event)">
    <div class="note-card" onclick="event.stopPropagation()">
      <span class="note-number" id="noteNumber">Reason #1</span>
      <p class="note-text" id="noteText">You always know how to make me laugh.</p>
      <div class="controls">
        <button class="btn-primary" onclick="pickReason()">Pick Another</button>
        <button class="btn-secondary" onclick="closeNoteModal()">Close</button>
      </div>
    </div>
  </div>

  <!-- Customize Modal -->
  <div class="modal-overlay" id="editorModal" onclick="closeEditor(event)">
    <div class="editor-card" onclick="event.stopPropagation()">
      <h2>Customize Your Jar</h2>
      <p>Personalize the title and add your own sweet notes or inside jokes blluulul>:3.</p>

      <div class="input-group">
        <label><strong>Jar Title:</strong></label>
        <input type="text" id="titleInput" placeholder="e.g., Reasons I Love Alex" oninput="updateTitle()" />
      </div>

      <div class="input-group">
        <label><strong>Add a New Reason:</strong></label>
        <textarea id="newReasonInput" placeholder="Write something you love about him..."></textarea>
        <button class="btn-primary" onclick="addReason()">+ Add Note to Jar</button>
      </div>

      <label><strong>Current Notes (<span id="editorCount">0</span>):</strong></label>
      <ul class="reasons-list" id="reasonsList"></ul>

      <div style="margin-top: 20px; text-align: right;">
        <button class="btn-secondary" onclick="closeEditor()">Done</button>
      </div>
    </div>
  </div>

  <script>
    // ==========================================
    // CUSTOMIZE YOUR DEFAULT NOTES RIGHT HERE:
    // ==========================================
    const defaultTitle = "Reasons I Love You- for Bence";
    const defaultReasons = [
      "Just by the way that you act, its very silly, and i love that.",
      "You make me feel so loved i couldnt even comprehend the feeling of it.",
      "Your You're my sweet lil husbun, my cutie lil baby, and my sweet sweet boy.",
      "The little details about you.",
      "You make me smile and happy everyday, which always gives me a reason why i should live another day despite knowing that there's a lot of reasons why i shoudlnt.",
      "Your eyes; they really do sparkle like topaz when they hit the sun.",
      "Your very caring and almost everything about you is really unique and beautiful in ways i cant explain.",
      "I love you for who you are and not for who they think you are.",
      "You play those silly games with me and even answer my hyper silly, ragebaiting, and dumb questions.",
      "Your voice; they really do sound heavenly, just so you know.",
      "Your intelligence is bountiful, even though you say that you arent just because. Nontheless, to me you are smart you just dont see it i mean who on earth would be crazy to take AppEng while maintaining being good in games??",
      "Your strength. I really admire it. For someone thats been through a whole lot, and still being able to carry the weigth of it all is amazing to me. You should know that even if you think that there's other people out there that has been worse than you; you still should think about the people who didnt went through what you went through."
    ];

    // Load saved data from browser storage or use defaults
    let jarTitle = localStorage.getItem("loveJarTitle") || defaultTitle;
    let reasons = JSON.parse(localStorage.getItem("loveJarReasons")) || [...defaultReasons];
    let lastIndex = -1;

    const noteColors = ["#fda4af", "#faedcd", "#93c5fd", "#c4b5fd", "#6ee7b7", "#fdba74"];

    function init() {
      document.getElementById("pageTitle").textContent = jarTitle;
      document.getElementById("titleInput").value = jarTitle;
      renderJarScraps();
      updateCounters();
    }

    // Visually fills the jar with colorful folded paper scraps
    function renderJarScraps() {
      const jarBody = document.getElementById("jarBody");
      // Remove existing scraps
      document.querySelectorAll(".paper-scrap").forEach(el => el.remove());

      const count = Math.min(reasons.length, 28);
      for (let i = 0; i < count; i++) {
        const scrap = document.createElement("div");
        scrap.className = "paper-scrap";
        scrap.style.backgroundColor = noteColors[i % noteColors.length];
        
        // Position scraps in the lower half of the jar
        const left = 15 + Math.random() * 135;
        const bottom = 12 + Math.random() * 110;
        const rotate = -35 + Math.random() * 70;

        scrap.style.left = `${left}px`;
        scrap.style.bottom = `${bottom}px`;
        scrap.style.transform = `rotate(${rotate}deg)`;
        jarBody.appendChild(scrap);
      }
    }

    function updateCounters() {
      const count = reasons.length;
      document.getElementById("counterText").textContent = `${count} ${count === 1 ? "note" : "notes"} inside`;
      document.getElementById("editorCount").textContent = count;
    }

    function pickReason() {
      if (reasons.length === 0) {
        alert("The jar is empty! Click 'Customize Notes' to add some reasons first.");
        return;
      }

      const jar = document.getElementById("jar");
      jar.classList.remove("shake");
      void jar.offsetWidth; // trigger reflow
      jar.classList.add("shake");

      // Pick a random index (avoiding repeating the exact same note twice in a row if possible)
      let index;
      if (reasons.length === 1) {
        index = 0;
      } else {
        do {
          index = Math.floor(Math.random() * reasons.length);
        } while (index === lastIndex);
      }
      lastIndex = index;

      setTimeout(() => {
        document.getElementById("noteNumber").textContent = `Reason #${index + 1} of ${reasons.length}`;
        document.getElementById("noteText").textContent = reasons[index];
        document.getElementById("noteModal").classList.add("active");
      }, 300);
    }

    function closeNoteModal(event) {
      if (!event || event.target.id === "noteModal") {
        document.getElementById("noteModal").classList.remove("active");
      }
    }

    // Editor Functions
    function openEditor() {
      renderEditorList();
      document.getElementById("editorModal").classList.add("active");
    }

    function closeEditor(event) {
      if (!event || event.target.id === "editorModal") {
        document.getElementById("editorModal").classList.remove("active");
      }
    }

    function updateTitle() {
      jarTitle = document.getElementById("titleInput").value || "Reasons I Love You";
      document.getElementById("pageTitle").textContent = jarTitle;
      localStorage.setItem("loveJarTitle", jarTitle);
    }

    function addReason() {
      const input = document.getElementById("newReasonInput");
      const text = input.value.trim();
      if (!text) return;

      reasons.push(text);
      saveAndRefresh();
      input.value = "";
    }

    function deleteReason(index) {
      reasons.splice(index, 1);
      saveAndRefresh();
    }

    function saveAndRefresh() {
      localStorage.setItem("loveJarReasons", JSON.stringify(reasons));
      renderJarScraps();
      updateCounters();
      renderEditorList();
    }

    function renderEditorList() {
      const list = document.getElementById("reasonsList");
      list.innerHTML = "";
      reasons.forEach((reason, idx) => {
        const li = document.createElement("li");
        li.innerHTML = `
          <span>${reason}</span>
          <button class="delete-btn" onclick="deleteReason(${idx})">Delete</button>
        `;
        list.appendChild(li);
      });
    }

    // Start app
    init();
  </script>
</body>
</html>
