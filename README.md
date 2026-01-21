<html lang="th" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>คณิตศาสตร์การเงิน ป.5</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600;700&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Sarabun', sans-serif;
    }
    
    .coin {
      animation: bounce 0.6s ease infinite alternate;
    }
    
    @keyframes bounce {
      from { transform: translateY(0); }
      to { transform: translateY(-8px); }
    }
    
    .sparkle {
      animation: sparkle 1.5s ease-in-out infinite;
    }
    
    @keyframes sparkle {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.1); }
    }
    
    .slide-in {
      animation: slideIn 0.4s ease-out;
    }
    
    @keyframes slideIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .money-pattern {
      background-image: 
        radial-gradient(circle at 20% 30%, rgba(255,215,0,0.1) 0%, transparent 50%),
        radial-gradient(circle at 80% 70%, rgba(255,215,0,0.1) 0%, transparent 50%);
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div id="app" class="h-full overflow-auto money-pattern" style="background-color: #fef9e7;"><!-- หน้าแรก -->
   <div id="home-screen" class="min-h-full flex flex-col items-center justify-center p-6">
    <div class="text-center max-w-md"><!-- เหรียญตกแต่ง -->
     <div class="flex justify-center gap-4 mb-6">
      <div class="coin" style="animation-delay: 0s;">
       <svg width="60" height="60" viewbox="0 0 60 60"><circle cx="30" cy="30" r="28" fill="#FFD700" stroke="#DAA520" stroke-width="3" /> <text x="30" y="38" text-anchor="middle" font-size="24" font-weight="bold" fill="#8B4513">
         ฿
        </text>
       </svg>
      </div>
      <div class="coin" style="animation-delay: 0.2s;">
       <svg width="60" height="60" viewbox="0 0 60 60"><circle cx="30" cy="30" r="28" fill="#C0C0C0" stroke="#A9A9A9" stroke-width="3" /> <text x="30" y="38" text-anchor="middle" font-size="20" font-weight="bold" fill="#4A4A4A">
         10
        </text>
       </svg>
      </div>
      <div class="coin" style="animation-delay: 0.4s;">
       <svg width="60" height="60" viewbox="0 0 60 60"><circle cx="30" cy="30" r="28" fill="#CD7F32" stroke="#8B4513" stroke-width="3" /> <text x="30" y="38" text-anchor="middle" font-size="20" font-weight="bold" fill="#FFFFFF">
         5
        </text>
       </svg>
      </div>
     </div>
     <h1 id="main-title" class="text-4xl font-bold mb-4" style="color: #2c3e50;">คณิตศาสตร์การเงิน ป.5</h1>
     <p id="welcome-text" class="text-xl mb-8" style="color: #566573;">มาเรียนรู้เรื่องเงินกันเถอะ! 💰</p>
     <div class="grid gap-4"><button onclick="startGame('counting')" class="w-full py-4 px-6 rounded-2xl text-xl font-bold text-white transition-all hover:scale-105 hover:shadow-lg" style="background: linear-gradient(135deg, #3498db, #2980b9);"> 🪙 นับเงิน </button> <button onclick="startGame('addition')" class="w-full py-4 px-6 rounded-2xl text-xl font-bold text-white transition-all hover:scale-105 hover:shadow-lg" style="background: linear-gradient(135deg, #27ae60, #229954);"> ➕ บวกเงิน </button> <button onclick="startGame('subtraction')" class="w-full py-4 px-6 rounded-2xl text-xl font-bold text-white transition-all hover:scale-105 hover:shadow-lg" style="background: linear-gradient(135deg, #e74c3c, #c0392b);"> ➖ ลบเงิน (ทอนเงิน) </button> <button onclick="startGame('word-problem')" class="w-full py-4 px-6 rounded-2xl text-xl font-bold text-white transition-all hover:scale-105 hover:shadow-lg" style="background: linear-gradient(135deg, #9b59b6, #8e44ad);"> 📝 โจทย์ปัญหา </button>
     </div>
     <div id="score-display" class="mt-8 p-4 rounded-xl" style="background-color: #ffffff; border: 2px solid #f0b429;">
      <p class="text-lg" style="color: #2c3e50;">🏆 คะแนนรวม: <span id="total-score" class="font-bold text-2xl" style="color: #f39c12;">0</span></p>
     </div>
     <div class="mt-6 p-4 rounded-xl" style="background-color: rgba(255,255,255,0.6); border: 2px solid #e8daef;">
      <p class="text-sm font-semibold" style="color: #8e44ad;">👨‍💻 ผู้สร้างเกม</p>
      <p class="text-base font-bold mt-1" style="color: #2c3e50;">เด็กชายรชตพล อ่อนล่ะมูล</p>
      <p class="text-sm" style="color: #566573;">ชั้นประถมศึกษาปีที่ 5/5 สาย MEP</p>
     </div>
    </div>
   </div><!-- หน้าเกม -->
   <div id="game-screen" class="min-h-full flex flex-col p-4 hidden">
    <div class="flex justify-between items-center mb-4"><button onclick="goHome()" class="py-2 px-4 rounded-xl font-bold text-white" style="background-color: #95a5a6;"> ← กลับ </button>
     <div class="flex items-center gap-4"><span id="question-counter" class="font-bold text-lg" style="color: #2c3e50;">ข้อ 1/5</span> <span id="game-score" class="font-bold text-lg" style="color: #f39c12;">⭐ 0</span>
     </div>
    </div>
    <div id="game-content" class="flex-1 flex flex-col items-center justify-center"><!-- เนื้อหาเกมจะถูกสร้างที่นี่ -->
    </div>
    <div id="feedback" class="hidden text-center py-4 rounded-xl mt-4 slide-in">
     <p id="feedback-text" class="text-2xl font-bold"></p>
    </div>
    <div id="answer-section" class="mt-4"><!-- ส่วนตอบคำถามจะถูกสร้างที่นี่ -->
    </div>
   </div><!-- หน้าผลลัพธ์ -->
   <div id="result-screen" class="min-h-full flex flex-col items-center justify-center p-6 hidden">
    <div class="text-center max-w-md slide-in" style="background-color: #ffffff; border-radius: 24px; padding: 32px; box-shadow: 0 10px 40px rgba(0,0,0,0.1);">
     <div class="sparkle text-6xl mb-4">
      🎉
     </div>
     <h2 class="text-3xl font-bold mb-4" style="color: #2c3e50;">เก่งมาก!</h2>
     <p class="text-xl mb-2" style="color: #566573;">คะแนนที่ได้</p>
     <p id="final-score" class="text-5xl font-bold mb-6" style="color: #f39c12;">0/50</p>
     <div id="result-message" class="mb-6 p-4 rounded-xl" style="background-color: #e8f8f5;">
      <p class="text-lg" style="color: #27ae60;"></p>
     </div>
     <div class="grid gap-3"><button onclick="restartGame()" class="w-full py-3 px-6 rounded-xl font-bold text-white" style="background-color: #3498db;"> 🔄 เล่นอีกครั้ง </button> <button onclick="goHome()" class="w-full py-3 px-6 rounded-xl font-bold text-white" style="background-color: #27ae60;"> 🏠 กลับหน้าหลัก </button>
     </div>
    </div>
   </div>
  </div>
  <script>
    // Config และ SDK
    const defaultConfig = {
      app_title: 'คณิตศาสตร์การเงิน ป.5',
      welcome_message: 'มาเรียนรู้เรื่องเงินกันเถอะ!',
      primary_color: '#f39c12',
      secondary_color: '#3498db',
      background_color: '#fef9e7',
      text_color: '#2c3e50',
      accent_color: '#27ae60'
    };
    
    let config = { ...defaultConfig };
    
    // ตัวแปรเกม
    let currentGameType = '';
    let currentQuestion = 0;
    let gameScore = 0;
    let totalScore = 0;
    let questions = [];
    const TOTAL_QUESTIONS = 5;
    
    // ค่าเงินไทย
    const moneyValues = [1000, 500, 100, 50, 20, 10, 5, 2, 1];
    const moneyNames = {
      1000: 'ธนบัตร 1,000 บาท',
      500: 'ธนบัตร 500 บาท',
      100: 'ธนบัตร 100 บาท',
      50: 'ธนบัตร 50 บาท',
      20: 'ธนบัตร 20 บาท',
      10: 'เหรียญ 10 บาท',
      5: 'เหรียญ 5 บาท',
      2: 'เหรียญ 2 บาท',
      1: 'เหรียญ 1 บาท'
    };
    
    // สร้างภาพเงิน
    function createMoneyImage(value) {
      const isBill = value >= 20;
      const colors = {
        1000: { bg: '#8B4513', border: '#5D3A1A', text: '#FFD700' },
        500: { bg: '#800080', border: '#4B0082', text: '#FFFFFF' },
        100: { bg: '#DC143C', border: '#8B0000', text: '#FFFFFF' },
        50: { bg: '#4169E1', border: '#000080', text: '#FFFFFF' },
        20: { bg: '#228B22', border: '#006400', text: '#FFFFFF' },
        10: { bg: '#C0C0C0', border: '#808080', text: '#333' },
        5: { bg: '#CD7F32', border: '#8B4513', text: '#FFFFFF' },
        2: { bg: '#FFD700', border: '#DAA520', text: '#8B4513' },
        1: { bg: '#C0C0C0', border: '#A9A9A9', text: '#333' }
      };
      
      const c = colors[value];
      
      if (isBill) {
        return `
          <div class="inline-flex items-center justify-center m-1 rounded-lg shadow-md transition-transform hover:scale-110" 
               style="width: 80px; height: 40px; background-color: ${c.bg}; border: 2px solid ${c.border};">
            <span class="font-bold text-sm" style="color: ${c.text};">฿${value.toLocaleString()}</span>
          </div>
        `;
      } else {
        return `
          <div class="inline-flex items-center justify-center m-1 rounded-full shadow-md transition-transform hover:scale-110" 
               style="width: 50px; height: 50px; background-color: ${c.bg}; border: 3px solid ${c.border};">
            <span class="font-bold text-sm" style="color: ${c.text};">${value}</span>
          </div>
        `;
      }
    }
    
    // สุ่มตัวเลข
    function randomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    
    // สร้างคำถามนับเงิน
    function generateCountingQuestion() {
      const targetAmount = randomInt(50, 500);
      let remaining = targetAmount;
      const moneyList = [];
      
      for (const value of moneyValues) {
        while (remaining >= value && moneyList.length < 8) {
          moneyList.push(value);
          remaining -= value;
          if (Math.random() < 0.3 && remaining > 0) break;
        }
      }
      
      // เติมเงินที่เหลือ
      for (const value of moneyValues) {
        while (remaining >= value) {
          moneyList.push(value);
          remaining -= value;
        }
      }
      
      // สลับตำแหน่ง
      moneyList.sort(() => Math.random() - 0.5);
      
      const actualAmount = moneyList.reduce((sum, v) => sum + v, 0);
      
      return {
        type: 'counting',
        moneyList,
        answer: actualAmount,
        question: 'นับเงินต่อไปนี้รวมกันได้เท่าไหร่?'
      };
    }
    
    // สร้างคำถามบวกเงิน
    function generateAdditionQuestion() {
      const amount1 = randomInt(20, 300);
      const amount2 = randomInt(20, 300);
      const items = ['ดินสอ', 'ยางลบ', 'ไม้บรรทัด', 'สมุด', 'ปากกา', 'กล่องดินสอ', 'กาว', 'กรรไกร'];
      const item1 = items[randomInt(0, items.length - 1)];
      let item2 = items[randomInt(0, items.length - 1)];
      while (item2 === item1) {
        item2 = items[randomInt(0, items.length - 1)];
      }
      
      return {
        type: 'addition',
        amount1,
        amount2,
        item1,
        item2,
        answer: amount1 + amount2,
        question: `${item1}ราคา ${amount1} บาท และ${item2}ราคา ${amount2} บาท รวมเป็นเงินเท่าไหร่?`
      };
    }
    
    // สร้างคำถามลบเงิน (ทอนเงิน)
    function generateSubtractionQuestion() {
      const price = randomInt(30, 200);
      const paidOptions = [50, 100, 200, 500, 1000].filter(p => p > price);
      const paid = paidOptions[randomInt(0, paidOptions.length - 1)];
      const items = ['ขนม', 'น้ำผลไม้', 'นมกล่อง', 'ขนมปัง', 'ไอศกรีม', 'ลูกอม', 'มันฝรั่��ทอด'];
      const item = items[randomInt(0, items.length - 1)];
      
      return {
        type: 'subtraction',
        price,
        paid,
        item,
        answer: paid - price,
        question: `ซื้อ${item}ราคา ${price} บาท จ่ายเงิน ${paid} บาท จะได้รับเงินทอนเท่าไหร่?`
      };
    }
    
    // สร้างโจทย์ปัญหา
    function generateWordProblem() {
      const problemTypes = [
        () => {
          const savingPerDay = randomInt(10, 50);
          const days = randomInt(5, 14);
          return {
            question: `น้องเมย์ออมเงินวันละ ${savingPerDay} บาท ถ้าออมเงินติดต่อกัน ${days} วัน น้องเมย์จะมีเงินออมเท่าไหร่?`,
            answer: savingPerDay * days
          };
        },
        () => {
          const totalMoney = randomInt(200, 500);
          const spent = randomInt(50, totalMoney - 50);
          return {
            question: `น้องโอ๊ตมีเงิน ${totalMoney} บาท ซื้อของขวัญให้เพื่อนไ�� ${spent} บาท น้องโอ๊ตจะเหลือเงินเท่าไหร่?`,
            answer: totalMoney - spent
          };
        },
        () => {
          const pricePerItem = randomInt(15, 40);
          const quantity = randomInt(3, 8);
          return {
            question: `ปากการาคาด้ามละ ${pricePerItem} บาท ถ้าซื้อ ${quantity} ด้าม จะต้องจ่ายเงินเท่าไหร่?`,
            answer: pricePerItem * quantity
          };
        },
        () => {
          const allowance = randomInt(100, 300);
          const breakfast = randomInt(20, 40);
          const lunch = randomInt(30, 50);
          return {
            question: `พ่อให้เงินค่าขนม ${allowance} บาท ซื้ออาหารเช้า ${breakfast} บาท และอาหารกลางวัน ${lunch} บาท จะเหลือเงิ��เท่าไหร่?`,
            answer: allowance - breakfast - lunch
          };
        },
        () => {
          const momGave = randomInt(100, 200);
          const dadGave = randomInt(100, 200);
          const spent = randomInt(50, momGave + dadGave - 50);
          return {
            question: `แม่ให้เงิน ${momGave} บาท พ่อให้เงิน ${dadGave} บาท หลังจากซื้อของไป ${spent} บาท จะเหลือเงินเท่าไหร่?`,
            answer: momGave + dadGave - spent
          };
        }
      ];
      
      const problem = problemTypes[randomInt(0, problemTypes.length - 1)]();
      return {
        type: 'word-problem',
        ...problem
      };
    }
    
    // สร้างคำถามตามประเภท
    function generateQuestions(gameType) {
      questions = [];
      for (let i = 0; i < TOTAL_QUESTIONS; i++) {
        switch (gameType) {
          case 'counting':
            questions.push(generateCountingQuestion());
            break;
          case 'addition':
            questions.push(generateAdditionQuestion());
            break;
          case 'subtraction':
            questions.push(generateSubtractionQuestion());
            break;
          case 'word-problem':
            questions.push(generateWordProblem());
            break;
        }
      }
    }
    
    // เริ่มเกม
    function startGame(gameType) {
      currentGameType = gameType;
      currentQuestion = 0;
      gameScore = 0;
      generateQuestions(gameType);
      
      document.getElementById('home-screen').classList.add('hidden');
      document.getElementById('game-screen').classList.remove('hidden');
      document.getElementById('result-screen').classList.add('hidden');
      
      showQuestion();
    }
    
    // แสดงคำถาม
    function showQuestion() {
      const q = questions[currentQuestion];
      const gameContent = document.getElementById('game-content');
      const answerSection = document.getElementById('answer-section');
      const feedback = document.getElementById('feedback');
      
      feedback.classList.add('hidden');
      document.getElementById('question-counter').textContent = `ข้อ ${currentQuestion + 1}/${TOTAL_QUESTIONS}`;
      document.getElementById('game-score').textContent = `⭐ ${gameScore}`;
      
      let contentHTML = '';
      
      if (q.type === 'counting') {
        contentHTML = `
          <div class="text-center slide-in">
            <h2 class="text-2xl font-bold mb-6" style="color: ${config.text_color};">${q.question}</h2>
            <div class="flex flex-wrap justify-center gap-2 p-6 rounded-2xl max-w-lg" style="background-color: #ffffff; border: 2px dashed ${config.primary_color};">
              ${q.moneyList.map(v => createMoneyImage(v)).join('')}
            </div>
          </div>
        `;
      } else {
        contentHTML = `
          <div class="text-center slide-in max-w-lg">
            <div class="p-8 rounded-2xl mb-4" style="background-color: #ffffff; border: 2px solid ${config.secondary_color};">
              <div class="text-5xl mb-4">${q.type === 'addition' ? '🛒' : q.type === 'subtraction' ? '💵' : '🤔'}</div>
              <h2 class="text-xl font-bold leading-relaxed" style="color: ${config.text_color};">${q.question}</h2>
            </div>
          </div>
        `;
      }
      
      gameContent.innerHTML = contentHTML;
      
      // สร้างตัวเลือกคำตอบ
      const correctAnswer = q.answer;
      const options = generateOptions(correctAnswer);
      
      answerSection.innerHTML = `
        <div class="grid grid-cols-2 gap-3 max-w-md mx-auto">
          ${options.map(opt => `
            <button onclick="checkAnswer(${opt}, ${correctAnswer})" 
                    class="answer-btn py-4 px-6 rounded-xl text-xl font-bold transition-all hover:scale-105"
                    style="background-color: #ffffff; color: ${config.text_color}; border: 3px solid ${config.secondary_color};">
              ${opt.toLocaleString()} บาท
            </button>
          `).join('')}
        </div>
      `;
    }
    
    // สร้างตัวเลือก
    function generateOptions(correctAnswer) {
      const options = [correctAnswer];
      const range = Math.max(20, Math.floor(correctAnswer * 0.3));
      
      while (options.length < 4) {
        let wrongAnswer;
        const variation = randomInt(1, range);
        if (Math.random() < 0.5) {
          wrongAnswer = correctAnswer + variation;
        } else {
          wrongAnswer = Math.max(1, correctAnswer - variation);
        }
        
        if (!options.includes(wrongAnswer)) {
          options.push(wrongAnswer);
        }
      }
      
      return options.sort(() => Math.random() - 0.5);
    }
    
    // ตรวจคำต���บ
    function checkAnswer(selected, correct) {
      const feedback = document.getElementById('feedback');
      const feedbackText = document.getElementById('feedback-text');
      const buttons = document.querySelectorAll('.answer-btn');
      
      buttons.forEach(btn => {
        btn.disabled = true;
        const btnValue = parseInt(btn.textContent.replace(/[^0-9]/g, ''));
        if (btnValue === correct) {
          btn.style.backgroundColor = '#27ae60';
          btn.style.color = '#ffffff';
          btn.style.borderColor = '#27ae60';
        } else if (btnValue === selected && selected !== correct) {
          btn.style.backgroundColor = '#e74c3c';
          btn.style.color = '#ffffff';
          btn.style.borderColor = '#e74c3c';
        }
      });
      
      feedback.classList.remove('hidden');
      
      if (selected === correct) {
        gameScore += 10;
        feedbackText.textContent = '🎉 ถูกต้อง! +10 คะแนน';
        feedbackText.style.color = '#27ae60';
        feedback.style.backgroundColor = '#e8f8f5';
      } else {
        feedbackText.textContent = `❌ ��ำตอบที่ถูกคือ ${correct.toLocaleString()} บาท`;
        feedbackText.style.color = '#e74c3c';
        feedback.style.backgroundColor = '#fdedec';
      }
      
      document.getElementById('game-score').textContent = `⭐ ${gameScore}`;
      
      setTimeout(() => {
        currentQuestion++;
        if (currentQuestion < TOTAL_QUESTIONS) {
          showQuestion();
        } else {
          showResult();
        }
      }, 1500);
    }
    
    // แสดงผลลัพธ์
    function showResult() {
      totalScore += gameScore;
      document.getElementById('total-score').textContent = totalScore;
      
      document.getElementById('home-screen').classList.add('hidden');
      document.getElementById('game-screen').classList.add('hidden');
      document.getElementById('result-screen').classList.remove('hidden');
      
      document.getElementById('final-score').textContent = `${gameScore}/${TOTAL_QUESTIONS * 10}`;
      
      const resultMessage = document.getElementById('result-message').querySelector('p');
      const percentage = (gameScore / (TOTAL_QUESTIONS * 10)) * 100;
      
      if (percentage === 100) {
        resultMessage.textContent = '🌟 สุดยอด! ทำได้เต็ม 100%';
        resultMessage.style.color = '#f39c12';
      } else if (percentage >= 80) {
        resultMessage.textContent = '😊 เก่งมาก! ทำได้ดีเยี่ยม';
        resultMessage.style.color = '#27ae60';
      } else if (percentage >= 60) {
        resultMessage.textContent = '👍 ดีมาก! พยายามต่อไปนะ';
        resultMessage.style.color = '#3498db';
      } else {
        resultMessage.textContent = '💪 ไม่เป็นไร ลองใหม่อีกครั้งนะ';
        resultMessage.style.color = '#9b59b6';
      }
    }
    
    // เริ่มเกมใหม่
    function restartGame() {
      startGame(currentGameType);
    }
    
    // กลับหน้าหลัก
    function goHome() {
      document.getElementById('home-screen').classList.remove('hidden');
      document.getElementById('game-screen').classList.add('hidden');
      document.getElementById('result-screen').classList.add('hidden');
    }
    
    // SDK Functions
    async function onConfigChange(newConfig) {
      config = { ...defaultConfig, ...newConfig };
      
      const titleEl = document.getElementById('main-title');
      const welcomeEl = document.getElementById('welcome-text');
      const appEl = document.getElementById('app');
      
      if (titleEl) titleEl.textContent = config.app_title || defaultConfig.app_title;
      if (welcomeEl) welcomeEl.textContent = config.welcome_message || defaultConfig.welcome_message;
      if (appEl) appEl.style.backgroundColor = config.background_color || defaultConfig.background_color;
      
      document.querySelectorAll('h1, h2').forEach(el => {
        el.style.color = config.text_color || defaultConfig.text_color;
      });
    }
    
    function mapToCapabilities(cfg) {
      return {
        recolorables: [
          {
            get: () => cfg.background_color || defaultConfig.background_color,
            set: (value) => { cfg.background_color = value; window.elementSdk.setConfig({ background_color: value }); }
          },
          {
            get: () => cfg.text_color || defaultConfig.text_color,
            set: (value) => { cfg.text_color = value; window.elementSdk.setConfig({ text_color: value }); }
          },
          {
            get: () => cfg.primary_color || defaultConfig.primary_color,
            set: (value) => { cfg.primary_color = value; window.elementSdk.setConfig({ primary_color: value }); }
          },
          {
            get: () => cfg.secondary_color || defaultConfig.secondary_color,
            set: (value) => { cfg.secondary_color = value; window.elementSdk.setConfig({ secondary_color: value }); }
          },
          {
            get: () => cfg.accent_color || defaultConfig.accent_color,
            set: (value) => { cfg.accent_color = value; window.elementSdk.setConfig({ accent_color: value }); }
          }
        ],
        borderables: [],
        fontEditable: {
          get: () => cfg.font_family || 'Sarabun',
          set: (value) => { cfg.font_family = value; window.elementSdk.setConfig({ font_family: value }); }
        },
        fontSizeable: {
          get: () => cfg.font_size || 16,
          set: (value) => { cfg.font_size = value; window.elementSdk.setConfig({ font_size: value }); }
        }
      };
    }
    
    function mapToEditPanelValues(cfg) {
      return new Map([
        ['app_title', cfg.app_title || defaultConfig.app_title],
        ['welcome_message', cfg.welcome_message || defaultConfig.welcome_message]
      ]);
    }
    
    // Initialize SDK
    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities,
        mapToEditPanelValues
      });
    }
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9c133f04a05c74f2',t:'MTc2ODk2MTEyMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
