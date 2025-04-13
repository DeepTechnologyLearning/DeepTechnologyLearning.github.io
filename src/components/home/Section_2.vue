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
          <div class="terminal-lines">
            <div class="terminal-line" :class="log.type" v-for="(log, i) in terminalLogs" :key="i">
              <span class="terminal-prefix">[DLT]</span>
              <span>{{ log.text }}</span>
              <span class="spinner" :class="log.type"></span>
            </div>
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
          "📌 Quel que soit le domaine, nous couvrons tout :",
          "    ✅ Programmation bas niveau 🖥️",
          "    ✅ Ingénierie logicielle et prompts ⚙️🤖",
          "    ✅ Science des données & Deep Learning 📊🧠",
          "    ✅ IA et automatisation avancée 🚀",
          "✨ Explorez les horizons du futur avec Deep Tech learning ! ✨",
          "💡 Une expertise partagée pour libérer votre potentiel.",
          "🌍 Rejoignez Deep Tech learning 🌍",
          "🚀 Plateforme d'apprentissage dédiée à l'IA et l'ingénierie logicielle 🚀",
          "🎓 Apprenez gratuitement avec nous ! 🎓",
          "📢 Chaque jour, des conseils, tutos et ressources GRATUITES :",
          "    🔹 LinkedIn 🔗",
          "    🔹 Instagram 📸",
          "    🔹 Twitter 🐦",
          "    🔹 Youtube 🐦",
          "💡 Pour progresser en IA & ingénierie logicielle 💡",
          "📈 Vous voulez aller plus loin ? 📈",
          "🔥 Formations complètes disponibles sur :",
          "    🎯 Udemy",
          "    🎯 Teachable",
          "    🎯 Skool",
          "    🎯 ...et d'autres en cours",
          "💻📚 Rejoignez-nous et montez en compétence dès aujourd'hui ! 💻📚",
          "💬 Prêt à booster vos compétences ?",
          "👉 Suivez-nous dès maintenant ! 🚀🔥"
        ],
        'liberez-votre-potentiel.js': [
          "🚀 Plongez dans une aventure d'apprentissage ","Qui révolutionnera votre maîtrise des technologies.",
          "",
          "🎯 Développez vos compétences grâce à nos formations en ligne de haut niveau,","Conçues pour accélérer votre carrière ","Et maximiser votre potentiel.",
          "",
          "💡 Chez Deep Intelli Tech, ","Nous savons que choisir la bonne plateforme d'apprentissage","Est une étape essentielle. ","C'est pourquoi des milliers d'apprenants à travers le monde","Nous font confiance pour se former aux technologies de demain."
        ]
      },
      terminalText: `Deep Technology Learning - 
Votre Apprentissage profond de la technologie vas commenencer dans un instant ...

---

1. Développement Web
Frontend

HTML, CSS, JavaScript

Frameworks : React, Vue.js, Angular, Svelte

Outils : Webpack, Vite, Tailwind CSS

Backend

Langages : Node.js, Python (Django, Flask), PHP (Laravel), Ruby on Rails, Go, Java (Spring)

Bases de données : MySQL, PostgreSQL, MongoDB, Redis

Fullstack & DevOps

Frameworks Fullstack : Next.js, Nuxt.js, Meteor

CI/CD : GitHub Actions, Jenkins, Docker, Kubernetes

2. Intelligence Artificielle & Machine Learning
Fondamentaux

Langages : Python, R, Julia

Bibliothèques : TensorFlow, PyTorch, scikit-learn, Keras

Applications

Vision par ordinateur : OpenCV, YOLO, Detectron2

NLP (traitement du langage) : spaCy, NLTK, Transformers (HuggingFace)

IA générative : GPT, DALL·E, Stable Diffusion, Midjourney

Approches avancées

Reinforcement learning, Federated Learning, AutoML

Fine-tuning et Prompt Engineering

3. Cybersécurité
Sécurité offensive (red team)

Pentesting : Metasploit, Nmap, Burp Suite, Wireshark

Ethical hacking, reverse engineering

Sécurité défensive (blue team)

SIEM : Splunk, Wazuh, ELK Stack

Firewalls, IDS/IPS, endpoint protection

Sécurité réseau et cryptographie

Protocoles : TLS, SSH, IPsec

Chiffrement : AES, RSA, ECC, Zero Trust

Tendances futures

Sécurité post-quantique, IA pour la détection d'intrusion

4. Développement Mobile
Natif

iOS : Swift, SwiftUI

Android : Kotlin, Jetpack Compose

Cross-platform

React Native, Flutter, Ionic, Xamarin

Backend mobile

Firebase, Supabase, Appwrite

API REST et GraphQL

5. Cloud Computing & Infonuagique
Fournisseurs cloud

AWS, Azure, Google Cloud Platform

Conteneurisation & Orchestration

Docker, Kubernetes, Helm

Serverless & microservices

AWS Lambda, Azure Functions, Cloudflare Workers

Architecture microservices, gRPC, API Gateway

DevOps Cloud

Terraform, Ansible, CI/CD pipelines, monitoring (Prometheus, Grafana)`
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
      let currentCategory = '';
      let currentSubCategory = '';

      const addLine = () => {
        if (this.currentLogIndex < lines.length) {
          const line = lines[this.currentLogIndex].trim();
          
          // Détection des catégories principales (commencent par un chiffre suivi d'un point)
          if (/^\d+\./.test(line)) {
            currentCategory = line;
            currentSubCategory = '';
            this.terminalLogs.push({
              text: line,
              type: 'main-category'
            });
            this.currentLogIndex++;
            setTimeout(addLine, 1500);
            return;
          }
          
          // Détection des sous-catégories (commencent par une majuscule et ne sont pas vides)
          if (line && line[0] === line[0].toUpperCase() && !/^\d+\./.test(line) && !line.includes(':')) {
            currentSubCategory = line;
            this.terminalLogs.push({
              text: line,
              type: 'sub-category'
            });
            this.currentLogIndex++;
            setTimeout(addLine, 300);
            return;
          }

          // Pour les éléments avec deux-points (sous-sous-catégories)
          if (line && line.includes(':')) {
            const [title, content] = line.split(':').map(item => item.trim());
            this.terminalLogs.push({
              text: title + ':',
              type: 'sub-sub-category'
            });
            
            // Traitement des éléments séparés par des virgules
            if (content) {
              const items = content.split(',').map(item => item.trim());
              items.forEach((item, index) => {
                setTimeout(() => {
                  this.terminalLogs.push({
                    text: item,
                    type: 'sub-sub-category-item'
                  });
                }, index * 150);
              });
              setTimeout(() => {
                this.currentLogIndex++;
                setTimeout(addLine, items.length * 150 + 100);
              }, items.length * 150);
            } else {
              this.currentLogIndex++;
              setTimeout(addLine, 150);
            }
            return;
          }

          // Pour les éléments vides (sauts de ligne)
          if (!line) {
            this.terminalLogs.push({
              text: '',
              type: 'empty'
            });
            this.currentLogIndex++;
            setTimeout(addLine, 100);
            return;
          }

          // Pour les autres éléments
          this.terminalLogs.push({
            text: line,
            type: 'sub-sub-category-item'
          });
          this.currentLogIndex++;
          setTimeout(addLine, 150);
        } else {
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
  width: 100%;
  text-align: left;
  color: #fff;
  margin: 0;
  overflow: hidden;
  background-color: #000;
  padding: 0;
  z-index: 0;
}

.cursor-editor {
  font-family: 'Courier New', Courier, monospace;
  background-color: #0a0a0a;
  color: #d4d4d4;
  width: 100%;
  height: auto;
  min-height: 70vh;
  display: flex;
  flex-direction: column;
  border-radius: 0;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
  border: 1px solid #222;
}

.window-bar {
  display: flex;
  align-items: center;
  padding: 6px 12px;
  background-color: #111;
  border-bottom: 1px solid #222;
  flex-wrap: wrap;
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
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.3);
}

.red { background-color: #ff5f56; }
.yellow { background-color: #ffbd2e; }
.green { background-color: #27c93f; }

.menu-bar {
  display: flex;
  gap: 10px;
  margin-left: 15px;
  color: #888;
  font-size: 12px;
  flex-wrap: wrap;
}

.editor-layout {
  display: flex;
  flex: 1;
  overflow: hidden;
  flex-direction: column;
  background-color: #0a0a0a;
}

.icon-sidebar {
  display: none;
  width: 50px;
  background-color: #111;
  padding-top: 10px;
  border-right: 1px solid #222;
}

.icon {
  color: #666;
  font-size: 18px;
  margin: 8px 0;
  display: block;
  text-align: center;
  transition: color 0.2s;
}

.icon:hover {
  color: #fff;
}

.file-explorer {
  width: 100%;
  background-color: #0a0a0a;
  padding: 10px;
  border-right: none;
  border-bottom: 1px solid #222;
}

.file-title {
  font-size: 12px;
  color: #666;
  margin-bottom: 10px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.file {
  padding: 6px 10px;
  color: #999;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
}

.file.active, .file:hover {
  background-color: #222;
  color: #fff;
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
  overflow: auto;
  background-color: #0a0a0a;
}

.tab-bar {
  background-color: #111;
  padding: 5px 10px;
  border-bottom: 1px solid #222;
}

.tab {
  color: #999;
  font-size: 13px;
}

.code-area {
  flex: 1;
  padding: 10px;
  overflow-y: auto;
  background-color: #0a0a0a;
  font-size: 12px;
}

.code-line {
  white-space: pre-wrap;
  margin: 0;
  color: #9cdcfe;
  font-size: 14px;
  line-height: 1.4;
  display: flex;
  align-items: flex-start;
}

.line-number {
  color: #444;
  width: 30px;
  text-align: right;
  margin-right: 10px;
  user-select: none;
  flex-shrink: 0;
  padding-top: 2px;
}

.terminal {
  background-color: #0a0a0a;
  padding: 10px;
  font-size: 11px;
  border-top: 1px solid #222;
  color: #888;
  height: 200px;
  overflow: hidden;
  position: relative;
}

.terminal-lines {
  position: absolute;
  width: 100%;
  bottom: 0;
}

.terminal-line {
  display: flex;
  gap: 5px;
  align-items: center;
  margin-bottom: 2px;
  animation: appear 0.2s ease-out forwards;
  word-break: break-word;
}

.terminal-line.main-category {
  font-size: 13px;
  color: #4CAF50;
}

.terminal-line.sub-category {
  font-size: 12px;
  margin-left: 10px;
  color: #2196F3;
}

.terminal-line.sub-sub-category {
  font-size: 11px;
  margin-left: 20px;
  color: #FFC107;
}

.terminal-line.sub-sub-category-item {
  font-size: 11px;
  margin-left: 30px;
  color: #999;
}

.terminal-line.empty {
  height: 10px;
  animation: none;
}

.terminal-line.empty .terminal-prefix,
.terminal-line.empty .spinner {
  display: none;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(5px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
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

.spinner.main-category {
  border-top-color: #4CAF50;
}

.spinner.sub-category {
  border-top-color: #2196F3;
}

.spinner.sub-sub-category {
  border-top-color: #FFC107;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.empty-editor {
  text-align: center;
  padding: 30px 20px;
  color: #888;
}

.empty-editor h1 {
  font-size: 24px;
  color: #fff;
  margin-bottom: 20px;
}

.empty-editor p {
  font-size: 13px;
  margin-bottom: 10px;
  line-height: 1.6;
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

/* Styles spécifiques pour mobile */
@media (max-width: 767px) {
  .Section_2 {
    padding: 0;
  }

  .cursor-editor {
    margin-top: 70px;
    min-height: 100vh;
  }

  .editor-layout {
    flex-direction: column;
  }

  .icon-sidebar {
    display: none;
  }

  .file-explorer {
    width: 100%;
    border-right: none;
    border-bottom: 1px solid #444;
  }

  .menu-bar {
    gap: 8px;
    margin-left: 10px;
    font-size: 11px;
  }

  .terminal {
    height: 150px;
    padding: 8px;
    font-size: 10px;
  }

  .terminal-line.main-category {
    font-size: 12px;
  }

  .terminal-line.sub-category {
    font-size: 11px;
    margin-left: 8px;
  }

  .terminal-line.sub-sub-category {
    font-size: 10px;
    margin-left: 16px;
  }

  .terminal-line.sub-sub-category-item {
    font-size: 10px;
    margin-left: 24px;
  }

  .empty-editor {
    padding: 20px 10px;
  }

  .empty-editor h1 {
    font-size: 20px;
  }

  .empty-editor p {
    font-size: 12px;
  }

  .code-line {
    font-size: 12px;
    line-height: 1.3;
  }

  .line-number {
    width: 25px;
    margin-right: 8px;
    font-size: 11px;
    padding-top: 1px;
  }
}

/* Media Queries pour les tablettes */
@media (min-width: 768px) {
  .Section_2 {
    padding: 0;
  }

  .cursor-editor {
    width: 90%;
    max-width: 1200px;
    margin: 70px auto;
  }

  .editor-layout {
    flex-direction: row;
  }

  .icon-sidebar {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    padding-top: 5px;
  }

  .file-explorer {
    width: 25%;
    border-right: 1px solid #444;
    border-bottom: none;
  }

  .terminal {
    height: 15rem;
  }
}

/* Media Queries pour les grands écrans */
@media (min-width: 1024px) {
  .cursor-editor {
    margin-top: 70px;
    width: 80%;
  }

  .terminal {
    height: 18rem;
  }
}

/* Media Queries pour les très grands écrans */
@media (min-width: 1440px) {
  .cursor-editor {
    margin-top: 70px;
    width: 70%;
  }

  .terminal {
    height: 20rem;
  }
}
</style> 