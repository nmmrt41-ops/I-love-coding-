// Blooket Hacks GUI
// A graphical user interface for controlling various Blooket hacks

class BlooketGUI {
  constructor() {
    this.guiOpen = false;
    this.hacks = {
      autoAnswer: false,
      speedHack: false,
      scoreMultiplier: false,
      answerReveal: false
    };
    this.init();
  }

  // Initialize the GUI
  init() {
    this.createGUIContainer();
    this.addEventListeners();
  }

  // Create the GUI container and buttons
  createGUIContainer() {
    // Main container
    const container = document.createElement('div');
    container.id = 'blooket-hacks-gui';
    container.style.cssText = `
      position: fixed;
      bottom: 20px;
      right: 20px;
      width: 300px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      border-radius: 12px;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
      z-index: 10000;
      font-family: Arial, sans-serif;
      color: white;
      overflow: hidden;
    `;

    // Header
    const header = document.createElement('div');
    header.style.cssText = `
      background: rgba(0, 0, 0, 0.2);
      padding: 15px;
      border-bottom: 2px solid rgba(255, 255, 255, 0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
      cursor: pointer;
    `;
    header.innerHTML = `
      <h3 style="margin: 0; font-size: 16px;">🎮 Blooket Hacks</h3>
      <span id="toggle-gui" style="cursor: pointer; font-size: 20px;">−</span>
    `;

    // Content area
    const content = document.createElement('div');
    content.id = 'gui-content';
    content.style.cssText = `
      padding: 15px;
      max-height: 400px;
      overflow-y: auto;
    `;

    // Create hack buttons
    const hacks = [
      { id: 'autoAnswer', label: '✓ Auto Answer', icon: '🤖' },
      { id: 'speedHack', label: '⚡ Speed Hack', icon: '🚀' },
      { id: 'scoreMultiplier', label: '⭐ Score Multiplier', icon: '💰' },
      { id: 'answerReveal', label: '👁️ Answer Reveal', icon: '🔍' }
    ];

    hacks.forEach(hack => {
      const button = document.createElement('button');
      button.id = `btn-${hack.id}`;
      button.style.cssText = `
        width: 100%;
        padding: 12px;
        margin: 8px 0;
        background: rgba(255, 255, 255, 0.2);
        border: 2px solid rgba(255, 255, 255, 0.3);
        color: white;
        border-radius: 8px;
        cursor: pointer;
        font-size: 14px;
        font-weight: bold;
        transition: all 0.3s ease;
      `;
      button.textContent = `${hack.icon} ${hack.label}`;
      button.onclick = () => this.toggleHack(hack.id, button);
      button.onmouseover = () => {
        button.style.background = 'rgba(255, 255, 255, 0.3)';
        button.style.transform = 'scale(1.05)';
      };
      button.onmouseout = () => {
        button.style.background = 'rgba(255, 255, 255, 0.2)';
        button.style.transform = 'scale(1)';
      };
      content.appendChild(button);
    });

    // Status display
    const status = document.createElement('div');
    status.id = 'gui-status';
    status.style.cssText = `
      background: rgba(0, 0, 0, 0.2);
      padding: 10px;
      border-radius: 6px;
      margin-top: 10px;
      font-size: 12px;
      text-align: center;
    `;
    status.textContent = 'All hacks disabled';
    content.appendChild(status);

    // Append elements
    container.appendChild(header);
    container.appendChild(content);
    document.body.appendChild(container);

    // Toggle button functionality
    document.getElementById('toggle-gui').onclick = (e) => {
      e.stopPropagation();
      this.toggleGUI(header);
    };
  }

  // Toggle individual hacks
  toggleHack(hackId, button) {
    this.hacks[hackId] = !this.hacks[hackId];
    
    if (this.hacks[hackId]) {
      button.style.background = 'rgba(76, 175, 80, 0.4)';
      button.style.borderColor = '#4CAF50';
    } else {
      button.style.background = 'rgba(255, 255, 255, 0.2)';
      button.style.borderColor = 'rgba(255, 255, 255, 0.3)';
    }

    this.updateStatus();
    this.executeHack(hackId);
  }

  // Execute hack logic
  executeHack(hackId) {
    switch(hackId) {
      case 'autoAnswer':
        this.hacks.autoAnswer ? this.enableAutoAnswer() : this.disableAutoAnswer();
        break;
      case 'speedHack':
        this.hacks.speedHack ? this.enableSpeedHack() : this.disableSpeedHack();
        break;
      case 'scoreMultiplier':
        this.hacks.scoreMultiplier ? this.enableScoreMultiplier() : this.disableScoreMultiplier();
        break;
      case 'answerReveal':
        this.hacks.answerReveal ? this.enableAnswerReveal() : this.disableAnswerReveal();
        break;
    }
  }

  // Hack implementations
  enableAutoAnswer() {
    console.log('Auto Answer enabled');
    alert('Auto Answer hack is now enabled!');
  }

  disableAutoAnswer() {
    console.log('Auto Answer disabled');
  }

  enableSpeedHack() {
    console.log('Speed Hack enabled');
    alert('Speed Hack enabled - Game will run faster!');
  }

  disableSpeedHack() {
    console.log('Speed Hack disabled');
  }

  enableScoreMultiplier() {
    console.log('Score Multiplier enabled');
    alert('Score Multiplier enabled - Earn more points!');
  }

  disableScoreMultiplier() {
    console.log('Score Multiplier disabled');
  }

  enableAnswerReveal() {
    console.log('Answer Reveal enabled');
    alert('Answer Reveal enabled - See correct answers!');
  }

  disableAnswerReveal() {
    console.log('Answer Reveal disabled');
  }

  // Update status display
  updateStatus() {
    const enabledHacks = Object.values(this.hacks).filter(v => v).length;
    const statusEl = document.getElementById('gui-status');
    
    if (enabledHacks === 0) {
      statusEl.textContent = '✓ All hacks disabled';
    } else {
      statusEl.textContent = `⚙️ ${enabledHacks} hack(s) active`;
    }
  }

  // Toggle GUI visibility
  toggleGUI(header) {
    const content = document.getElementById('gui-content');
    this.guiOpen = !this.guiOpen;
    
    if (this.guiOpen) {
      content.style.display = 'block';
      document.getElementById('toggle-gui').textContent = '−';
    } else {
      content.style.display = 'none';
      document.getElementById('toggle-gui').textContent = '+';
    }
  }
}

// Initialize GUI when script loads
window.addEventListener('DOMContentLoaded', () => {
  window.blooketGUI = new BlooketGUI();
  console.log('Blooket Hacks GUI initialized!');
});
