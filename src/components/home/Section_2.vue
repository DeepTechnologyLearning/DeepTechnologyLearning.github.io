<template>
  <section class="Section_2">
    <div class="cursor-editor">
    <!-- Barre supérieure avec boutons -->
    <div class="window-bar">
      <div class="window-buttons">
        <span class="btn red"></span>
        <span class="btn yellow"></span>
        <span class="btn green"></span>
      </div>
      <div class="menu-bar">
        <span>Fichier</span>
        <span>Éditer</span>
        <span>Affichage</span>
        <span>Aller</span>
        <span>Exécuter</span>
        <span>Aide</span>
      </div>
    </div>

    <div class="editor-layout">
      <!-- Icônes latérales -->
      <div class="icon-sidebar">
        <i class="icon">📁</i>
        <i class="icon">🔍</i>
        <i class="icon">🔃</i>
        <i class="icon">🔧</i>
        <i class="icon">🧩</i>
      </div>

      <!-- Explorateur de fichiers -->
      <div class="file-explorer">
        <div class="file-title">EXPLORATEUR</div>
        <div
          class="file"
          :class="{ active: activeFile === 'deep-tech-learning.js', 'clickable-file': activeFile === null }"
          @click="openFile('deep-tech-learning.js')"
        >
          pourquoi-deep-technology-learning.js
        </div>
        <div
          class="file"
          :class="{ active: activeFile === 'liberez-votre-potentiel.js', 'clickable-file': activeFile === null }"
          @click="openFile('liberez-votre-potentiel.js')"
        >
          liberez-votre-potentiel.js
        </div>
      </div>

      <!-- Zone de code -->
      <div class="main-editor">
        <div class="tab-bar">
          <div class="tab">{{ activeFile || 'Aucun fichier ouvert' }}</div>
        </div>
        <div class="code-area">
          <div v-if="!activeFile" class="empty-editor">
            <h1>Deep Technology Learning</h1>
            <p>Apprenez l'intelligence artificielle, le développement logiciel et bien plus encore.</p>
            <p>Une plateforme de formation pensée pour l'excellence.</p>
            <p>Rejoignez une communauté d'innovateurs et de créateurs.</p>
          </div>
          <pre v-else v-for="(line, i) in visibleLines" :key="i" class="code-line">
            <span class="line-number">{{ i + 1 }}</span>
            <span v-html="line"></span>
          </pre>
        </div>

        <!-- Terminal -->
        <div class="terminal" v-if="activeFile === 'deep-tech-learning.js'">
          <div class="terminal-line" v-for="(log, i) in terminalLogs" :key="i">
            <span class="terminal-prefix">[DLT]</span>
            <span :style="{ color: colors[i % colors.length] }">{{ log }}</span>
            <span class="spinner"></span>
          </div>
        </div>
      </div>
    </div>
  </div>
    
  </section>
</template>

<script>
export default {
  data() {
    return {
      activeFile: null,
      visibleLines: [],
      currentLine: 0,
      lineBuffer: "",
      terminalLogs: [],
      currentLogIndex: 0,
      colors: ['#ccc', '#888', '#666'],
      filesContent: {
        'deep-tech-learning.js': [
          "🎯 Nous mettons à votre disposition les meilleurs cours en ligne 🎯",
          "",
          "📌 Quel que soit le domaine, nous couvrons tout :",
          "",
          "    ✅ Programmation bas niveau 🖥️",
          "    ✅ Ingénierie logicielle et prompts ⚙️🤖",
          "    ✅ Science des données & Deep Learning 📊🧠",
          "    ✅ IA et automatisation avancée 🚀",
          "",
          "✨ Explorez les horizons du futur avec Deep Tech learning ! ✨",
          "💡 Une expertise partagée pour libérer votre potentiel.",
          "",
          "🌍 Rejoignez Deep Tech learning 🌍",
          "🚀 Plateforme d’apprentissage dédiée à l’IA et l’ingénierie logicielle 🚀",
          "",
          "🎓 Apprenez gratuitement avec nous ! 🎓",
          "📢 Chaque jour, des conseils, tutos et ressources GRATUITES :",
          "    🔹 LinkedIn 🔗",
          "    🔹 Instagram 📸",
          "    🔹 Twitter 🐦",
          "    🔹 Youtube 🐦",
          "",
          "💡 Pour progresser en IA & ingénierie logicielle 💡",
          "📈 Vous voulez aller plus loin ? 📈",
          "🔥 Formations complètes disponibles sur :",
          "    🎯 Udemy",
          "    🎯 Teachable",
          "    🎯 Skool",
          "    🎯 ...et d'autres en cours",
          "",
          "💻📚 Rejoignez-nous et montez en compétence dès aujourd’hui ! 💻📚",
          "💬 Prêt à booster vos compétences ?",
          "👉 Suivez-nous dès maintenant ! 🚀🔥"
        ],
        'liberez-votre-potentiel.js': [
          "🚀 Plongez dans une aventure d’apprentissage qui révolutionnera votre maîtrise des technologies.",
          "",
          "🎯 Développez vos compétences grâce à nos formations en ligne de haut niveau, conçues pour accélérer votre carrière et maximiser votre potentiel.",
          "",
          "💡 Chez Deep Intelli Tech, nous savons que choisir la bonne plateforme d’apprentissage est une étape essentielle. C’est pourquoi des milliers d’apprenants à travers le monde nous font confiance pour se former aux technologies de demain."
        ]
      },
      terminalText: `Apprentissage\nTechnologique\nProfond\n\nApprennez n’importe quelle technologies de manière clair, consise et approfondie!\n\ndeveloppement web\nentreprise\ningénierie front end UI/UX\ningénierie back end\ningénierie full stack\njavascript\nreact\nvueJS\nangular\nhTML\nCSS\nfigma\nà propos\nservice\nabonnement et tarifs\n\ngestion de projet\nprogrammation\nPMP Certification\u2028Agile et Scrum\u2028PRINCE2\u2028Gestion des risques\u2028Lean Six Sigma\njava\njavascript\npython\nC\nC++\nc#\ndata structure\nalgorithmies\noOP\nScience des Données et bi\nsciences des données\nCloud Computing\nAnalyse de données avec Excel\u2028SQL\u2028Python pour la science des données\u2028R pour la science des données\u2028Visualisation de données avec Tableau\u2028Power BI\nScience des données\nPython\nMachine Learning\nChatGPT\nDeep Learning\nAWS\u2028Microsoft Azure\u2028Google Cloud Platform\u2028Cloud hybride\ndevops\nAI & machine learning\nDocker\u2028Kubernetes\u2028Jenkins\u2028Ansible\u2028Chef\nApprentissage profond (Deep Learning)\u2028Traitement du langage naturel (NLP)\u2028Réseaux de neurones\u2028IA pour les entreprises\nCybersécurité\nMarketing Digital\nHacking éthique\u2028Sécurité des réseaux\u2028Sécurité des applications\u2028Gestion des risques\u2028Conformité\nSEO (Optimisation pour les moteurs de recherche)\u2028Marketing sur les réseaux sociaux\u2028Publicité par e-mail\u2028Marketing de contenu\u2028Publicité PPC (Pay-Per-Click)\nMéthodologies Agiles et Scrum\nSalesforce\nScrum Master\u2028Product Owner\u2028Kanban\u2028SAFe (Scaled Agile Framework)\nAdministration Salesforce\u2028Développement Salesforce\u2028Consultant en implémentation\nGestion de la Qualité\u2028Lean Six Sigma\u2028ISO\u2028Gestion des processus\nDéveloppement Logiciel\nDéveloppement Full-Stack\u2028Java\u2028Python\u2028JavaScript\u2028C#\u2028Développement mobile`
    };
  },
  methods: {
    openFile(file) {
      this.activeFile = file;
      this.visibleLines = [""];
      this.currentLine = 0;
      this.typeLineByLine();

      if (file === 'deep-tech-learning.js') {
        this.terminalLogs = [];
        this.currentLogIndex = 0;
        this.runTerminalLogs();
      }
    },
    typeLineByLine() {
      const lines = this.filesContent[this.activeFile];
      if (!lines || this.currentLine >= lines.length) return;

      const line = lines[this.currentLine];
      let charIndex = 0;
      this.lineBuffer = "";

      const typeChar = () => {
        if (charIndex < line.length) {
          const char = line[charIndex] === " " ? "&nbsp;" : line[charIndex];
          this.lineBuffer += char;
          this.$set(this.visibleLines, this.currentLine, this.lineBuffer);
          charIndex++;
          setTimeout(typeChar, 10);
        } else {
          this.currentLine++;
          this.visibleLines.push("");
          setTimeout(this.typeLineByLine, 200);
        }
      };

      typeChar();
    },
    runTerminalLogs() {
      const lines = this.terminalText.split("\n");
      const addLine = () => {
        if (this.currentLogIndex < lines.length) {
          this.terminalLogs.push(lines[this.currentLogIndex]);
          this.currentLogIndex++;
          setTimeout(addLine, 300);
        } else {
          this.terminalLogs = [];
          this.currentLogIndex = 0;
          setTimeout(addLine, 1000);
        }
      };
      addLine();
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Crimson+Text:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&display=swap');

.Section_2 {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  min-width: 100%;
  text-align: left;
  color: #fff;
  margin: 0;
  overflow: hidden;
  background-color: #000;
  padding: 4rem 0;
  z-index: 0;
}

.cursor-editor {
  font-family: 'Courier New', Courier, monospace;
  background-color: #1e1e1e;
  color: #d4d4d4;
  height: 70vh;
  min-width: 70%;
  max-width: 70%;
  display: flex;
  flex-direction: column;
}
.window-bar {
  display: flex;
  align-items: center;
  padding: 6px 12px;
  background-color: #2c2c2c;
  border-bottom: 1px solid #444;
}
.window-buttons {
  display: flex;
  gap: 6px;
}
.btn {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  display: inline-block;
}
.red { background-color: #ff5f56; }
.yellow { background-color: #ffbd2e; }
.green { background-color: #27c93f; }
.menu-bar {
  display: flex;
  gap: 20px;
  margin-left: 30px;
  color: #ccc;
  font-size: 13px;
}
.editor-layout {
  display: flex;
  flex: 1;
  overflow: hidden;
}
.icon-sidebar {
  width: 50px;
  background-color: #252526;
  padding-top: 10px;
  border-right: 1px solid #444;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}
.icon { color: #888; font-size: 18px; }
.file-explorer {
  width: 25%;
  background-color: #1e1e1e;
  padding: 10px;
  border-right: 1px solid #444;
}
.file-title {
  font-size: 12px;
  color: #888;
  margin-bottom: 10px;
}
.file {
  padding: 6px 10px;
  color: #ddd;
  font-size: 13px;
  cursor: pointer;
}
.file.active, .file:hover {
  background-color: #333;
}
.clickable-file {
  animation: pulse 1.5s infinite;
}
@keyframes pulse {
  0% { background-color: #1e1e1e; }
  50% { background-color: #333333; }
  100% { background-color: #1e1e1e; }
}
.main-editor {
  flex: 1;
  display: flex;
  flex-direction: column;
}
.tab-bar {
  background-color: #2d2d2d;
  padding: 5px 10px;
  border-bottom: 1px solid #444;
}
.tab {
  color: #fff;
  font-size: 13px;
}
.code-area {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
  background-color: #1e1e1e;
}
.code-line {
  white-space: pre-wrap;
  margin: 0;
  color: #9cdcfe;
  font-size: 14px;
  line-height: 1.4;
  display: flex;
}
.line-number {
  color: #666;
  width: 30px;
  text-align: right;
  margin-right: 10px;
  user-select: none;
}
.terminal {
  background-color: #111;
  padding: 10px 20px;
  font-size: 12px;
  border-top: 1px solid #444;
  color: #ccc;
  height: 180px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}
.terminal-line {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-bottom: 2px;
}
.terminal-prefix {
  color: #0ff;
  font-weight: bold;
}
.spinner {
  display: inline-block;
  width: 10px;
  height: 10px;
  border: 2px solid transparent;
  border-top-color: #888;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
@keyframes spin {
  to { transform: rotate(360deg); }
}
.empty-editor {
  text-align: center;
  padding-top: 60px;
}
.empty-editor h1 {
  font-size: 28px;
  font-weight: bold;
  color: #f0f0f0;
}
.empty-editor p {
  font-size: 14px;
  color: #aaa;
  margin-top: 10px;
}

@keyframes scroll-up {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-100%);
  }
}

.terminal-lines::-webkit-scrollbar,
.file-item::-webkit-scrollbar {
  display: none;
}

.terminal-lines,
.file-item {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style> 