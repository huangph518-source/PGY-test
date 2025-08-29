<!DOCTYPE html>
<html lang="zh-Hant">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale-1.0">
    <title>呼吸治療臨床情境學習網</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700&display=swap');

        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: #f3f4f6;
            color: #374151;
        }

        .container {
            max-width: 900px;
        }

        .shadow-custom {
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }

        .btn-primary {
            transition: all 0.3s ease;
            transform: scale(1);
        }

        .btn-primary:hover {
            transform: scale(1.02);
        }

        .btn-primary:active {
            transform: scale(0.98);
        }

        .fade-in {
            animation: fadeIn 0.5s ease-in-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #3b82f6;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }
        
        #modal-content h1, #modal-content h2, #modal-content h3 {
            font-weight: bold;
            margin-top: 1rem;
            margin-bottom: 0.5rem;
        }
        #modal-content h1 { font-size: 1.5em; }
        #modal-content h2 { font-size: 1.25em; }
        #modal-content h3 { font-size: 1.1em; }
        #modal-content ul { list-style-type: disc; margin-left: 1.5rem; }
        #modal-content ol { list-style-type: decimal; margin-left: 1.5rem; }
        #modal-content p { margin-bottom: 0.5rem; }
        #modal-content strong { font-weight: bold; }
        #modal-content code { background-color: #e5e7eb; padding: 0.1rem 0.3rem; border-radius: 0.25rem; }

    </style>
</head>

<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">

    <div id="app" class="container bg-white rounded-xl shadow-custom p-6 sm:p-8 md:p-12 space-y-8">
        <!-- Introduction Section -->
        <div id="intro-and-guide" class="space-y-6">
            <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold text-center text-blue-800">呼吸治療臨床情境學習網</h1>
            <p class="text-lg sm:text-xl text-center text-gray-600">
                本網站旨在幫助你強化呼吸治療的進階判斷能力，採用**由淺入深**的學習模式，讓你循序漸進地精進技能。
            </p>
            <div id="study-guide" class="bg-blue-50 rounded-lg p-6 space-y-6 shadow-inner">
                <h2 class="text-2xl sm:text-3xl font-bold text-blue-700">學習指南：急診成人呼吸困難的快速評估與處置</h2>
                <p class="text-gray-700">
                    本指南專為強化你在急診中對呼吸困難病人的快速評估與處置能力而設計。我們將從基礎概念開始，逐步深入探討初期穩定措施、危險徵象的辨識，以及針對常見病因如哮喘發作、心臟衰竭或氣胸的緊急介入，幫助你在高壓環境下做出正確且果斷的決策。
                </p>
            </div>
            <button id="start-quiz-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 btn-primary">
                開始測驗
            </button>
        </div>

        <!-- Quiz Section -->
        <div id="quiz-flow" class="hidden space-y-6 fade-in">
            <div id="difficulty-level" class="text-lg font-bold text-center text-blue-600"></div>
            <!-- Teaching and Question Container -->
            <div id="teaching-and-question" class="space-y-4">
                <!-- Teaching Content -->
                <div id="teaching-content" class="bg-yellow-50 rounded-lg p-6 space-y-4 shadow-inner">
                    <h3 class="text-2xl font-bold text-yellow-700">教學內容</h3>
                    <div id="teaching-text" class="text-gray-800 space-y-2"></div>
                </div>
                <!-- Question Section -->
                <div id="question-section" class="hidden">
                    <p id="question-text" class="text-lg sm:text-xl font-medium text-gray-800"></p>
                    <div id="answer-options" class="grid grid-cols-1 sm:grid-cols-2 gap-4"></div>
                    <button id="submit-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 btn-primary mt-4">
                        送出答案
                    </button>
                </div>
            </div>
            <button id="show-question-btn" class="w-full bg-orange-500 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-orange-600 focus:outline-none focus:ring-4 focus:ring-orange-300 btn-primary">
                開始作答
            </button>
        </div>

        <!-- Result Section -->
        <div id="result-section" class="hidden space-y-4 bg-gray-50 p-6 rounded-lg fade-in">
            <h3 id="result-status" class="text-2xl font-bold text-center"></h3>
            <p id="correct-answer" class="text-lg text-gray-700"></p>
            <p id="rationale" class="text-lg text-gray-700 mt-2"></p>
            <button id="deep-explain-btn" class="w-full bg-purple-600 text-white font-bold py-2 px-4 rounded-lg text-md hover:bg-purple-700 focus:outline-none focus:ring-4 focus:ring-purple-300 btn-primary hidden">
                ✨ AI 深入解析
            </button>
            <button id="next-question-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 btn-primary">
                下一題
            </button>
        </div>

        <!-- Summary Section -->
        <div id="summary-section" class="hidden space-y-6 fade-in">
            <h2 class="text-3xl font-bold text-center text-blue-800">測驗結果總結</h2>
            <div id="summary-details" class="space-y-4"></div>
            <div id="analysis-details" class="space-y-4 p-4 rounded-lg bg-gray-100 border border-gray-200">
                <h3 class="text-2xl font-bold text-gray-800">學習成效分析</h3>
                <div id="performance-summary" class="space-y-2"></div>
                <div id="recommendations" class="space-y-2"></div>
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <button id="restart-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-blue-700 focus:outline-none focus:ring-4 focus:ring-blue-300 btn-primary">
                    重新開始測驗
                </button>
                <button id="generate-case-study-btn" class="w-full bg-teal-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-teal-700 focus:outline-none focus:ring-4 focus:ring-teal-300 btn-primary">
                     ✨ 產生個人化案例分析
                </button>
                 <button id="generate-more-btn" class="w-full bg-green-600 text-white font-bold py-3 px-6 rounded-lg text-lg hover:bg-green-700 focus:outline-none focus:ring-4 focus:ring-green-300 btn-primary sm:col-span-2">
                    <span id="generate-btn-text">生成更多選擇題</span>
                </button>
            </div>
        </div>
    </div>

    <!-- Gemini Modal -->
    <div id="gemini-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 max-w-2xl w-full max-h-[80vh] overflow-y-auto flex flex-col">
            <div class="flex justify-between items-center mb-4 flex-shrink-0">
                <h3 id="modal-title" class="text-2xl font-bold text-blue-800"></h3>
                <button id="modal-close-btn" class="text-3xl font-bold hover:text-red-500">&times;</button>
            </div>
            <div id="modal-content" class="text-gray-700 space-y-4 overflow-y-auto">
                <!-- Content will be injected here -->
            </div>
        </div>
    </div>

    <!-- Message Box for alerts -->
    <div id="message-box" class="fixed bottom-4 right-4 bg-red-500 text-white p-4 rounded-lg shadow-lg hidden z-50"></div>

    <script>
        // Initial quiz data
        const quizData = {
            "questions": [{
                "category": "基本評估與處置",
                "difficulty": "easy",
                "teaching": "臨床上，對於意識清醒且呼吸窘迫的病人，讓他們坐起來或採取**半坐臥位** (semi-Fowler's position) 是最基本且有效的初期處置。這個姿勢可以**幫助橫膈膜下降**，擴展胸腔容積，減少呼吸肌肉的做功，從而改善呼吸困難。",
                "question": "一位因呼吸困難至急診的病人，在初步評估後，應立即將其置於何種體位，以改善呼吸狀況？",
                "answerOptions": [{
                    "text": "完全平躺 (supine)",
                    "isCorrect": false
                }, {
                    "text": "完全俯臥 (prone)",
                    "isCorrect": false
                }, {
                    "text": "頭部朝下的傾斜臥位",
                    "isCorrect": false
                }, {
                    "text": "半坐臥位 (semi-Fowler's position)",
                    "isCorrect": true
                }],
                "rationale": "半坐臥位能利用重力幫助橫膈膜下移，增加肺部擴張空間，是緩解呼吸困難最直接且有效的方法之一。"
            }, {
                "category": "基本評估與處置",
                "difficulty": "easy",
                "teaching": "**非侵襲性呼吸器 (NIV)** 的 EPAP 類似於插管呼吸器的 PEEP，其主要作用是提供一個持續的陽壓，防止肺泡塌陷，**增加肺泡擴張**以改善血氧，特別適用於肺水腫或低血氧的病人。",
                "question": "一位因心臟衰竭導致肺水腫的病人，需要使用非侵襲性呼吸器 (NIV)。在 BiPAP 模式下，EPAP (呼氣末陽壓) 的主要治療作用是什麼？",
                "answerOptions": [{
                    "text": "幫助排出二氧化碳",
                    "isCorrect": false
                }, {
                    "text": "降低心臟負荷",
                    "isCorrect": false
                }, {
                    "text": "維持肺泡擴張，改善氧合",
                    "isCorrect": true
                }, {
                    "text": "增加病人的潮氣容積",
                    "isCorrect": false
                }],
                "rationale": "EPAP能提供持續的氣道正壓，防止肺泡在吐氣末塌陷，增加功能性肺餘容積 (FRC)，從而改善氧合。"
            }, {
                "category": "氧氣治療",
                "difficulty": "easy",
                "teaching": "對於急性呼吸困難的缺氧病人，初期處置的首要目標是優化氧合。這通常透過**非再呼吸面罩 (non-rebreather mask)** 來提供高濃度的氧氣。這種面罩能有效提升吸入氧濃度，快速改善低血氧狀態。",
                "question": "一位急性呼吸困難的病人到急診求助，脈搏血氧飽和度 (SpO₂) 為 88%。初步的氧合處置，最常使用下列哪種氧氣裝置？",
                "answerOptions": [{
                    "text": "鼻導管",
                    "isCorrect": false
                }, {
                    "text": "非再呼吸面罩",
                    "isCorrect": true
                }, {
                    "text": "簡易型氧氣面罩",
                    "isCorrect": false
                }, {
                    "text": "高流量鼻導管 (HFNC)",
                    "isCorrect": false
                }],
                "rationale": "非再呼吸面罩是急診初期快速提供高濃度氧氣的最佳選擇，能有效提升SpO₂，穩定病人狀況。"
            }, {
                "category": "氧氣治療",
                "difficulty": "medium",
                "teaching": "對於**慢性阻塞性肺病 (COPD)** 且有二氧化碳滯留病史的病人，其呼吸中樞的刺激主要依賴**低血氧**而非高二氧化碳。給予過高濃度的氧氣可能會**抑制其呼吸驅動**，導致二氧化碳進一步滯留，惡化為呼吸性酸中毒。因此，氧氣治療的目標是矯正危險的低血氧，同時避免過度抑制呼吸。",
                "question": "一位有慢性二氧化碳滯留病史的COPD病人，因喘來到急診，SpO₂為85%。在給予氧氣治療時，最恰當的目標SpO₂範圍是多少？",
                "answerOptions": [{
                    "text": "95-100%",
                    "isCorrect": false
                }, {
                    "text": "盡可能越高越好",
                    "isCorrect": false
                }, {
                    "text": "88-92%",
                    "isCorrect": true
                }, {
                    "text": "大於92%",
                    "isCorrect": false
                }],
                "rationale": "對於慢性二氧化碳滯留的COPD病人，氧氣治療的目標應是維持在88-92%的SpO₂範圍，這樣既能改善組織氧合，又能避免過度抑制其低血氧驅動的呼吸中樞，是臨床上的標準做法。"
            }, {
                "category": "病因鑑別與徵象",
                "difficulty": "medium",
                "teaching": "對於**阻塞性**呼吸道疾病，如哮喘發作或慢性阻塞性肺病 (COPD)，其特徵是呼吸道阻力增加。臨床上常表現為**喘鳴 (wheezing)** 和**吐氣期延長**。這與肺部僵硬 (如ARDS) 導致的**肺部囉音 (crackles)** 和**吸氣困難**不同。",
                "question": "一位年輕病人在接觸花粉後出現呼吸困難，其身體檢查發現雙側肺部有瀰漫性喘鳴聲 (wheezing) 且吐氣時間明顯延長。這種臨床表現最可能代表哪一類呼吸道疾病？",
                "answerOptions": [{
                    "text": "限制性肺病 (如肺纖維化)",
                    "isCorrect": false
                }, {
                    "text": "阻塞性肺病 (如哮喘)",
                    "isCorrect": true
                }, {
                    "text": "肺血管疾病 (如肺栓塞)",
                    "isCorrect": false
                }, {
                    "text": "神經肌肉疾病",
                    "isCorrect": false
                }],
                "rationale": "阻塞性肺病的特徵是呼吸道阻力增加，導致氣流受限，臨床上最典型的徵象就是喘鳴與吐氣延長。"
            }, {
                "category": "呼吸器問題排除",
                "difficulty": "medium",
                "teaching": "呼吸器高壓警報（High Pressure Alarm）是臨床常見問題，通常代表氣道阻力增加或肺順應性下降。可使用**DOPES**口訣快速排除原因：**D**-Dislodgement(管路異位)、**O**-Obstruction(管路阻塞，如痰或咬管)、**P**-Pneumothorax(氣胸)、**E**-Equipment failure(設備問題)、**S**-Stacking breaths(氣體滯留)。面對警報，首要之務是立即評估病人並依序排除問題。",
                "question": "一位使用呼吸器的病人突然觸發高壓警報，身為呼吸治療師，你應採取的首要處理措施是什麼？",
                "answerOptions": [{
                    "text": "立即給予病人鎮靜劑",
                    "isCorrect": false
                }, {
                    "text": "聯絡醫師，建議調整呼吸器模式",
                    "isCorrect": false
                }, {
                    "text": "檢查呼吸器管路是否通暢，並評估病人是否有痰或咬管",
                    "isCorrect": true
                }, {
                    "text": "直接調高壓力警報上限以解除警報",
                    "isCorrect": false
                }],
                "rationale": "處理高壓警報的首要原則是找出並解決根本原因。立即檢查管路通暢度、病人是否有痰或咬管等，是最直接且必要的步驟，可以快速排除外部因素，確保病人安全。"
            }, {
                "category": "緊急藥物處置",
                "difficulty": "hard",
                "teaching": "對於急性支氣管哮喘發作，最有效的初期治療是快速緩解支氣管痙攣，這通常透過吸入**短效型β2受體促進劑**來實現，如沙丁胺醇 (salbutamol)。這類藥物能迅速放鬆氣道平滑肌，改善氣流阻塞。",
                "question": "一位因嚴重哮喘發作而呼吸困難的病人，其初期處置應優先使用哪一類藥物？",
                "answerOptions": [{
                    "text": "全身性類固醇",
                    "isCorrect": false
                }, {
                    "text": "長效型β2受體促進劑",
                    "isCorrect": false
                }, {
                    "text": "吸入性短效型β2受體促進劑",
                    "isCorrect": true
                }, {
                    "text": "靜脈注射抗生素",
                    "isCorrect": false
                }],
                "rationale": "短效型β2受體促進劑是緩解急性哮喘發作的首選藥物，能迅速擴張支氣管，改善症狀。"
            }, {
                "category": "呼吸器進階設定",
                "difficulty": "hard",
                "teaching": "**肺保護性通氣**是治療 ARDS 的黃金標準。核心概念是使用**低潮氣容積** ($4-6 \\,ml/kg$ 理想體重) 和限制**平台壓** $(<30 \\,cmH_2O)$，以避免肺部過度擴張造成的傷害。",
                "question": "一位急性呼吸窘迫症候群 (ARDS) 病人正在使用侵襲性呼吸器。為了執行「肺保護性通氣策略」，潮氣容積 (Tidal Volume) 的設定目標應為多少？",
                "answerOptions": [{
                    "text": "10-12 ml/kg (理想體重)",
                    "isCorrect": false
                }, {
                    "text": "8-10 ml/kg (理想體重)",
                    "isCorrect": false
                }, {
                    "text": "6-8 ml/kg (理想體重)",
                    "isCorrect": false
                }, {
                    "text": "4-6 ml/kg (理想體重)",
                    "isCorrect": true
                }],
                "rationale": "低潮氣容積是肺保護策略的核心，能有效減少肺泡過度擴張與壓力傷，是目前治療ARDS的標準做法。"
            }, {
                "category": "拔管與脫離呼吸器",
                "difficulty": "hard",
                "teaching": "拔管評估的重點是確保病人能夠**自主維持呼吸**並**保護呼吸道**。重要指標包括：意識清醒、血液動力學穩定、有效的咳嗽能力以及足夠的氧合能力 ($PaO_2/FiO_2 > 150-200$)。對於COPD等**慢性** $CO_2$ 滯留的病人，其**基礎** $PaCO_2$ 就可能偏高，因此不能單純以「正常值」來判斷。",
                "question": "一位使用呼吸器超過一週的病人，狀況穩定，醫師考慮進行拔管。在進行自主呼吸測試 (SBT) 前，下列哪一項不是必要的評估標準？",
                "answerOptions": [{
                    "text": "穩定的血液動力學狀態",
                    "isCorrect": false
                }, {
                    "text": "足夠的氧合能力 (如 PaO₂/FiO₂ > 150-200)",
                    "isCorrect": false
                }, {
                    "text": "正常的動脈血二氧化碳分壓 (PaCO₂)",
                    "isCorrect": true
                }, {
                    "text": "清醒的意識狀態與有效的咳嗽能力",
                    "isCorrect": false
                }],
                "rationale": "雖然PaCO₂是重要指標，但對於慢性CO₂滯留的COPD病人，要求其PaCO₂完全正常是不切實際的，應看其是否回到基礎值。"
            }, {
                "category": "拔管與脫離呼吸器",
                "difficulty": "hard",
                "teaching": "脫離呼吸器的評估中，**淺快呼吸指數 (Rapid Shallow Breathing Index, RSBI)** 是一個重要的客觀指標。其計算公式為 **呼吸頻率(RR) / 潮氣容積(VT, 以公升為單位)**。一般而言，RSBI **小於 105** 被視為脫離成功率較高的預測因子，代表病人能夠以較深、較慢的模式自主呼吸。",
                "question": "一位病人正在進行自主呼吸訓練(SBT)，30分鐘後測得其呼吸頻率為 30 次/分，潮氣容積為 250 mL。請問其RSBI值為何？這代表什麼意義？",
                "answerOptions": [{
                    "text": "RSBI = 120，可能脫離失敗",
                    "isCorrect": true
                }, {
                    "text": "RSBI = 80，可能脫離成功",
                    "isCorrect": false
                }, {
                    "text": "RSBI = 120，可能脫離成功",
                    "isCorrect": false
                }, {
                    "text": "RSBI = 80，可能脫離失敗",
                    "isCorrect": false
                }],
                "rationale": "RSBI 的計算方式為 RR / VT (L)，因此計算為 30 / 0.25 = 120。臨床上普遍認為 RSBI > 105 是淺快呼吸的表現，代表呼吸肌疲乏，脫離呼吸器的失敗風險較高。"
            }, {
                "category": "緊急危急處置",
                "difficulty": "hard",
                "teaching": "當病人出現**張力性氣胸**時，其症狀會迅速惡化，包括單側呼吸音減弱或消失、低血壓、頸靜脈擴張。這是一種危及生命的急症，需要立即進行**針刺減壓 (needle decompression)**，以釋放積聚在胸腔內的壓力，恢復肺部功能。",
                "question": "一位胸部外傷病人出現單側呼吸音減弱、頸靜脈擴張與血壓驟降。你最可能懷疑哪一種危及生命的病況，並應立即採取何種處置？",
                "answerOptions": [{
                    "text": "心包膜填塞，應立即進行心包膜穿刺。",
                    "isCorrect": false
                }, {
                    "text": "氣胸，應立即進行胸腔穿刺放液。",
                    "isCorrect": false
                }, {
                    "text": "張力性氣胸，應立即進行針刺減壓。",
                    "isCorrect": true
                }, {
                    "text": "血胸，應立即進行導管胸腔造口術。",
                    "isCorrect": false
                }],
                "rationale": "單側呼吸音減弱、頸靜脈擴張和低血壓是張力性氣胸的典型三聯徵，這是一種急症，需要立即進行針刺減壓來挽救生命。"
            }, {
                "category": "呼吸器圖形判讀",
                "difficulty": "hard",
                "teaching": "**自體吐氣末陽壓 (Auto-PEEP)**，也稱為內因性PEEP或氣體滯留 (air trapping)，發生於吐氣時間不足，導致肺部在下次吸氣開始前仍殘留過多氣體。在呼吸器流速波形上，可見**吐氣流速未歸零**即開始下一次吸氣。Auto-PEEP會增加病人呼吸作功，甚至影響血液動力學。",
                "question": "在觀察呼吸器波形時，你發現病人的吐氣流速（flow）在下一次吸氣開始前並未回到基線零點，這最可能代表什麼臨床問題？",
                "answerOptions": [{
                    "text": "呼吸器管路嚴重漏氣",
                    "isCorrect": false
                }, {
                    "text": "病人呼吸作功不足",
                    "isCorrect": false
                }, {
                    "text": "病人有氣體滯留 (Auto-PEEP)",
                    "isCorrect": true
                }, {
                    "text": "吸氣時間設定過長",
                    "isCorrect": false
                }],
                "rationale": "吐氣流速未歸零是Auto-PEEP的典型圖形特徵，表示肺部氣體未完全排出，吐氣時間不足。這在阻塞性肺病的病人中尤其常見。"
            }, {
                "category": "呼吸器圖形判讀",
                "difficulty": "hard",
                "teaching": "呼吸器的**壓力-時間波形**可以提供關於人機同步性的重要資訊。當吸氣階段的壓力波形出現**凹陷**或**下墜**的現象 (scooped appearance)，通常代表呼吸器給予的流速不足以滿足病人的吸氣需求，這種情況稱為**流速飢餓 (Flow Starvation)**。",
                "question": "在觀察呼吸器的壓力-時間純量圖時，你注意到在吸氣過程中，壓力波形呈現凹陷的「勺子狀」，這最可能代表何種人機不同步問題？",
                "answerOptions": [{
                    "text": "設定的潮氣容積過高",
                    "isCorrect": false
                }, {
                    "text": "呼吸器管路有大量漏氣",
                    "isCorrect": false
                }, {
                    "text": "病人吸氣流速需求未被滿足 (流速飢餓)",
                    "isCorrect": true
                }, {
                    "text": "吐氣時間過短造成氣體滯留",
                    "isCorrect": false
                }],
                "rationale": "壓力波形呈凹陷狀是「流速飢餓」的典型特徵，表示病人需要比呼吸器設定更高的吸氣流速。此時應考慮增加流速設定、縮短吸氣時間或更換為能讓病人自主決定流速的呼吸模式。"
            }]
        };

        const questionOrder = {
            "easy": [],
            "medium": [],
            "hard": []
        };

        let quizQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let userAnswers = [];
        let currentDifficulty = "easy";
        let difficultyLevels = ["easy", "medium", "hard"];
        let correctCountAtDifficulty = 0;
        const requiredCorrectToAdvance = 2; // Number of correct answers to advance difficulty

        // Get all DOM elements
        const introAndGuide = document.getElementById('intro-and-guide');
        const quizFlow = document.getElementById('quiz-flow');
        const resultSection = document.getElementById('result-section');
        const summarySection = document.getElementById('summary-section');
        const startQuizBtn = document.getElementById('start-quiz-btn');
        const showQuestionBtn = document.getElementById('show-question-btn');
        const teachingText = document.getElementById('teaching-text');
        const questionSection = document.getElementById('question-section');
        const questionText = document.getElementById('question-text');
        const answerOptionsContainer = document.getElementById('answer-options');
        const submitBtn = document.getElementById('submit-btn');
        const resultStatus = document.getElementById('result-status');
        const correctAnswerText = document.getElementById('correct-answer');
        const rationaleText = document.getElementById('rationale');
        const nextQuestionBtn = document.getElementById('next-question-btn');
        const summaryDetails = document.getElementById('summary-details');
        const analysisDetails = document.getElementById('analysis-details');
        const performanceSummary = document.getElementById('performance-summary');
        const recommendations = document.getElementById('recommendations');
        const restartBtn = document.getElementById('restart-btn');
        const generateMoreBtn = document.getElementById('generate-more-btn');
        const generateBtnText = document.getElementById('generate-btn-text');
        const messageBox = document.getElementById('message-box');
        const difficultyLevelDisplay = document.getElementById('difficulty-level');
        const deepExplainBtn = document.getElementById('deep-explain-btn');
        const generateCaseStudyBtn = document.getElementById('generate-case-study-btn');

        // Modal elements
        const geminiModal = document.getElementById('gemini-modal');
        const modalTitle = document.getElementById('modal-title');
        const modalContent = document.getElementById('modal-content');
        const modalCloseBtn = document.getElementById('modal-close-btn');

        // --- Gemini API Call Function ---
        async function callGemini(prompt) {
            const apiKey = ""; 
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
            
            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
            };

            try {
                 let response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`API call failed with status: ${response.status}`);
                }
                
                const result = await response.json();
                const text = result.candidates?.[0]?.content?.parts?.[0]?.text;
                if (!text) {
                    throw new Error("Invalid response format from API.");
                }
                return text;

            } catch (error) {
                console.error("Gemini API call error:", error);
                showMessage("與 AI 溝通時發生錯誤，請稍後再試。");
                return null;
            }
        }
        
        // --- Modal Control Functions ---
        function showModal(title, content, isLoading = false) {
            modalTitle.textContent = title;
            if (isLoading) {
                modalContent.innerHTML = '<div class="flex justify-center items-center p-8"><div class="loader"></div></div>';
            } else {
                 modalContent.innerHTML = marked.parse(content);
            }
            geminiModal.style.display = 'flex';
        }

        function hideModal() {
            geminiModal.style.display = 'none';
        }

        modalCloseBtn.addEventListener('click', hideModal);

        // --- New Gemini Features ---
        async function getDeeperExplanation(currentQuestion, userAnswerText) {
            const correctAnswer = currentQuestion.answerOptions.find(opt => opt.isCorrect).text;
            const prompt = `你是一位專業的呼吸治療臨床教師。一位學習者回答了以下問題：\n\n**問題：** "${currentQuestion.question}"\n\n**正確答案是：** "${correctAnswer}"\n\n**學習者卻選擇了：** "${userAnswerText}"\n\n請用清晰易懂、循循善誘的語氣，以繁體中文深入解釋：\n1. 為什麼正確答案是正確的，並提供更詳細的臨床背景或原理。\n2. 為什麼學習者選擇的答案是錯誤的，點出可能的觀念盲點。\n3. 總結一個關鍵的記憶點或臨床提示。\n\n請以 Markdown 格式回覆，讓重點更清晰。`;
            
            showModal("✨ AI 深入解析", "", true);
            const explanation = await callGemini(prompt);
            if (explanation) {
                showModal("✨ AI 深入解析", explanation);
            } else {
                hideModal();
            }
        }
        
        async function generateCaseStudy() {
            const weakCategories = [...new Set(userAnswers
                .filter(ans => !ans.isCorrect)
                .map(ans => ans.category)
            )];

            if (weakCategories.length === 0) {
                 showMessage("恭喜！您沒有明顯的弱點領域，將為您生成一個綜合性的進階案例。");
                 weakCategories.push("呼吸器圖形判讀", "拔管與脫離呼吸器"); // Default for excellent performance
            }
            
            const prompt = `你是一位資深的呼吸治療臨床案例出題官。一位學習者在以下領域表現較弱：**${weakCategories.join('、')}**。\n\n請根據這些弱點，設計一個簡潔但具挑戰性的臨床案例分析題，以繁體中文撰寫。\n\n案例需包含：\n1. **病人簡介**：簡單的背景、主訴。\n2. **臨床情境**：生命體徵、呼吸器數據、或相關檢查結果。\n3. **問題**：提出 1-2 個需要學習者分析或決策的關鍵問題。\n\n在案例之後，請提供一份 **專家解析**，包含：\n1. **分析與判斷**：針對問題的詳細思考過程。\n2. **建議處置**：基於分析所建議的下一步臨床措施。\n\n請以 Markdown 格式回覆，使用標題和列表讓結構清晰。`;
        
            showModal("✨ 個人化案例分析", "", true);
            const caseStudy = await callGemini(prompt);
            if (caseStudy) {
                showModal("✨ 個人化案例分析", caseStudy);
            } else {
                hideModal();
            }
        }

        generateCaseStudyBtn.addEventListener('click', generateCaseStudy);

        // Helper function to shuffle an array
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        // Initialize question order by difficulty and shuffle them
        function initializeQuiz() {
            // Clear previous questions
            for (const key in questionOrder) {
                questionOrder[key] = [];
            }
            
            // Populate and shuffle all questions from quizData
            quizData.questions.forEach(q => {
                if (questionOrder[q.difficulty]) {
                    questionOrder[q.difficulty].push(q);
                }
            });
            shuffleArray(questionOrder["easy"]);
            shuffleArray(questionOrder["medium"]);
            shuffleArray(questionOrder["hard"]);

            quizQuestions = questionOrder["easy"].slice();
            currentDifficulty = "easy";
            updateDifficultyDisplay();
        }

        function updateDifficultyDisplay() {
            const difficultyMap = {
                "easy": "基礎",
                "medium": "中等",
                "hard": "進階"
            };
            difficultyLevelDisplay.textContent = `目前難度：${difficultyMap[currentDifficulty]}`;
        }
        
        // Handles the start quiz button click
        startQuizBtn.addEventListener('click', () => {
            introAndGuide.classList.add('hidden');
            quizFlow.classList.remove('hidden');
            currentQuestionIndex = 0;
            score = 0;
            userAnswers = [];
            correctCountAtDifficulty = 0;
            initializeQuiz(); // Reset and initialize
            loadTeachingContent();
        });

        // Handles the show question button click
        showQuestionBtn.addEventListener('click', () => {
            document.getElementById('teaching-content').classList.add('hidden');
            showQuestionBtn.classList.add('hidden');
            questionSection.classList.remove('hidden');
            loadQuestion();
        });

        // Handles the next question button click
        nextQuestionBtn.addEventListener('click', () => {
            const currentLevelIndex = difficultyLevels.indexOf(currentDifficulty);

            if (correctCountAtDifficulty >= requiredCorrectToAdvance && currentLevelIndex < difficultyLevels.length - 1) {
                // If correct answers met requirement and there's a next level, advance
                currentDifficulty = difficultyLevels[currentLevelIndex + 1];
                correctCountAtDifficulty = 0; // Reset correct count for new level
                quizQuestions = questionOrder[currentDifficulty].slice();
                currentQuestionIndex = 0; // Reset index for new level
                updateDifficultyDisplay();
            } else if (currentQuestionIndex >= quizQuestions.length - 1) {
                // If all questions in the current level are answered, but not enough correct answers
                if (currentLevelIndex < difficultyLevels.length - 1) {
                    showMessage("答對題數不足，將繼續練習本難度等級。");
                    shuffleArray(quizQuestions); // Reshuffle for more practice
                    currentQuestionIndex = 0; // Restart from the beginning of the shuffled array
                } else {
                    // All questions answered, show summary
                    showSummary();
                    return;
                }
            } else {
                currentQuestionIndex++;
            }

            resultSection.classList.add('hidden');
            quizFlow.classList.remove('hidden');
            document.getElementById('teaching-content').classList.remove('hidden');
            showQuestionBtn.classList.remove('hidden');
            questionSection.classList.add('hidden');
            loadTeachingContent();
        });

        // Handles the restart button click
        restartBtn.addEventListener('click', () => {
            currentQuestionIndex = 0;
            score = 0;
            userAnswers = [];
            summarySection.classList.add('hidden');
            introAndGuide.classList.remove('hidden');
            initializeQuiz();
        });

        // Handles the generate more questions button click
        generateMoreBtn.addEventListener('click', generateNewQuestions);

        // Handles the submit button click
        submitBtn.addEventListener('click', () => {
            const selectedOption = document.querySelector('#answer-options button.bg-blue-300');
            if (!selectedOption) {
                showMessage("請選擇一個答案！");
                return;
            }
            const selectedAnswerIndex = Array.from(answerOptionsContainer.children).indexOf(selectedOption);
            checkAnswer(selectedAnswerIndex);
        });

        // Function to show a temporary message box
        function showMessage(message) {
            messageBox.textContent = message;
            messageBox.classList.remove('hidden');
            messageBox.classList.add('fade-in');
            setTimeout(() => {
                messageBox.classList.remove('fade-in');
                messageBox.classList.add('fade-out');
                setTimeout(() => messageBox.classList.add('hidden'), 500);
            }, 3000);
        }

        // Function to load and display teaching content
        function loadTeachingContent() {
            const currentQuestion = quizQuestions[currentQuestionIndex];
            const content = currentQuestion.teaching.split('**').map((part, index) => {
                if (index % 2 === 1) {
                    const strong = document.createElement('strong');
                    strong.textContent = part;
                    return strong.outerHTML;
                }
                return part;
            }).join('');
            
            teachingText.innerHTML = content.replace(/\$(.*?)\$/g, (match, p1) => {
                return `<code>${p1}</code>`;
            });
            
            questionText.textContent = `${currentQuestionIndex + 1}. ${currentQuestion.question}`;
            answerOptionsContainer.innerHTML = '';
            submitBtn.disabled = true;
        }

        // Function to load and display a new question and its options
        function loadQuestion() {
            const currentQuestion = quizQuestions[currentQuestionIndex];
            
            // Shuffle answer options to avoid the same order every time
            const shuffledOptions = currentQuestion.answerOptions.slice();
            shuffleArray(shuffledOptions);
            
            answerOptionsContainer.innerHTML = ''; // Clear previous options
            submitBtn.disabled = false; // Enable the submit button

            shuffledOptions.forEach((option, index) => {
                const button = document.createElement('button');
                button.textContent = option.text;
                button.classList.add('bg-gray-200', 'text-gray-800', 'font-semibold', 'py-3', 'px-6', 'rounded-lg', 'text-left', 'hover:bg-gray-300', 'focus:outline-none', 'focus:ring-2', 'focus:ring-blue-500', 'transition', 'duration-200', 'ease-in-out');

                button.addEventListener('click', () => {
                    // Remove selection from other buttons
                    document.querySelectorAll('#answer-options button').forEach(btn => {
                        btn.classList.remove('bg-blue-300', 'ring-2', 'ring-blue-500');
                    });
                    // Add selection to the clicked button
                    button.classList.add('bg-blue-300', 'ring-2', 'ring-blue-500');
                });

                answerOptionsContainer.appendChild(button);
            });
        }

        // Function to check the user's answer and display the result
        function checkAnswer(selectedAnswerIndex) {
            const currentQuestion = quizQuestions[currentQuestionIndex];
            const selectedButton = document.querySelector('#answer-options button.bg-blue-300');
            const selectedText = selectedButton.textContent;
            
            const selectedOption = currentQuestion.answerOptions.find(option => option.text === selectedText);
            const correctOption = currentQuestion.answerOptions.find(option => option.isCorrect);
            let userIsCorrect = false;

            if (selectedOption.isCorrect) {
                userIsCorrect = true;
                score++;
                correctCountAtDifficulty++;
            }

            // Store the result
            userAnswers.push({
                question: currentQuestion.question,
                isCorrect: userIsCorrect,
                rationale: currentQuestion.rationale,
                correctAnswer: correctOption.text,
                category: currentQuestion.category,
                difficulty: currentQuestion.difficulty
            });

            // Disable all buttons and highlight correct/incorrect answers
            document.querySelectorAll('#answer-options button').forEach((btn, index) => {
                btn.disabled = true;
                btn.classList.remove('bg-blue-300', 'ring-2', 'ring-blue-500', 'hover:bg-gray-300');

                if (btn.textContent === correctOption.text) {
                    btn.classList.add('bg-green-400');
                } else if (btn.textContent === selectedText && !userIsCorrect) {
                    btn.classList.add('bg-red-400');
                }
            });

            // Display result section
            quizFlow.classList.add('hidden');
            resultSection.classList.remove('hidden');

            if (userIsCorrect) {
                resultStatus.textContent = "答對了！";
                resultStatus.classList.remove('text-red-600');
                resultStatus.classList.add('text-green-600');
                deepExplainBtn.classList.add('hidden');
            } else {
                resultStatus.textContent = "再努力看看！";
                resultStatus.classList.remove('text-green-600');
                resultStatus.classList.add('text-red-600');
                deepExplainBtn.classList.remove('hidden');
                deepExplainBtn.onclick = () => getDeeperExplanation(currentQuestion, selectedText);
            }

            correctAnswerText.innerHTML = `<strong>正確答案：</strong> ${correctOption.text}`;
            rationaleText.innerHTML = `<strong>解析：</strong> ${currentQuestion.rationale}`;
        }

        // Function to show the final summary with detailed analysis
        function showSummary() {
            quizFlow.classList.add('hidden');
            resultSection.classList.add('hidden');
            summarySection.classList.remove('hidden');
            summaryDetails.innerHTML = '';
            performanceSummary.innerHTML = '';
            recommendations.innerHTML = '';

            const summaryTitle = document.createElement('h3');
            summaryTitle.classList.add('text-xl', 'sm:text-2xl', 'font-bold', 'text-gray-800', 'mb-4');
            summaryTitle.textContent = `你的成績是： ${score} / ${userAnswers.length}`;
            summaryDetails.appendChild(summaryTitle);

            // Detailed question-by-question summary
            userAnswers.forEach((item, index) => {
                const itemDiv = document.createElement('div');
                itemDiv.classList.add('p-4', 'rounded-lg', 'border-l-4', 'space-y-2');
                itemDiv.classList.add(item.isCorrect ? 'bg-green-50' : 'bg-red-50');
                itemDiv.classList.add(item.isCorrect ? 'border-green-500' : 'border-red-500');

                const questionP = document.createElement('p');
                questionP.classList.add('font-semibold', 'text-gray-800');
                questionP.textContent = `第 ${index + 1} 題：${item.question}`;
                itemDiv.appendChild(questionP);

                const statusP = document.createElement('p');
                statusP.classList.add('font-bold');
                statusP.classList.add(item.isCorrect ? 'text-green-600' : 'text-red-600');
                statusP.textContent = item.isCorrect ? '✔ 答對了！' : '✘ 答錯了！';
                itemDiv.appendChild(statusP);

                const answerP = document.createElement('p');
                answerP.classList.add('text-gray-700');
                answerP.innerHTML = `<strong>正確答案：</strong> ${item.correctAnswer}`;
                itemDiv.appendChild(answerP);
                
                const rationaleP = document.createElement('p');
                rationaleP.classList.add('text-gray-700');
                rationaleP.innerHTML = `<strong>解析：</strong> ${item.rationale}`;
                itemDiv.appendChild(rationaleP);

                summaryDetails.appendChild(itemDiv);
            });

            // Categorized performance analysis by category and difficulty
            const categories = {};
            const allCategories = [...new Set(quizData.questions.map(q => q.category))];
            allCategories.forEach(cat => {
                categories[cat] = { easy: { total: 0, correct: 0 }, medium: { total: 0, correct: 0 }, hard: { total: 0, correct: 0 }};
            });

            userAnswers.forEach(ans => {
                if (categories[ans.category] && categories[ans.category][ans.difficulty]) {
                    categories[ans.category][ans.difficulty].total++;
                    if (ans.isCorrect) {
                        categories[ans.category][ans.difficulty].correct++;
                    }
                }
            });

            // Display performance
            let hasWeaknesses = false;
            let weakCategories = [];
            for (const category in categories) {
                const categorySection = document.createElement('div');
                categorySection.classList.add('space-y-1', 'py-2');
                const categoryTitle = document.createElement('h4');
                categoryTitle.classList.add('font-bold', 'text-blue-700');
                categoryTitle.textContent = category;
                categorySection.appendChild(categoryTitle);

                for (const difficulty of ['easy', 'medium', 'hard']) {
                    const result = categories[category][difficulty];
                    if (result.total > 0) {
                        const percentage = (result.correct / result.total * 100).toFixed(0);
                        const difficultyDiv = document.createElement('div');
                        difficultyDiv.classList.add('flex', 'justify-between', 'items-center', 'pl-4');
                        difficultyDiv.innerHTML = `
                            <span class="font-medium">${difficulty === 'easy' ? '基礎題' : (difficulty === 'medium' ? '中等題' : '進階題')}</span>
                            <span class="font-bold ${percentage >= 75 ? 'text-green-600' : (percentage >= 50 ? 'text-orange-600' : 'text-red-600')}">${percentage}% (${result.correct}/${result.total})</span>
                        `;
                        categorySection.appendChild(difficultyDiv);
                        if (percentage < 75) {
                            hasWeaknesses = true;
                            if (!weakCategories.includes(category)) {
                                weakCategories.push(category);
                            }
                        }
                    }
                }
                performanceSummary.appendChild(categorySection);
            }
            
            // Display recommendations
            if (hasWeaknesses) {
                const recommendationText = document.createElement('p');
                recommendationText.classList.add('text-lg', 'text-gray-800');
                recommendationText.innerHTML = `
                    <p class="font-bold text-red-700 mb-2">💡 你的學習建議：</p>
                    <p>你在 <span class="font-bold text-red-600">${weakCategories.join('、')}</span> 方面需要加強。建議你可以再次挑戰，或點擊下方的「✨ 產生個人化案例分析」來進行更深入的練習。</p>
                `;
                recommendations.appendChild(recommendationText);
            } else {
                 const recommendationText = document.createElement('p');
                 recommendationText.classList.add('text-lg', 'text-gray-800');
                 recommendationText.innerHTML = `
                    <p class="font-bold text-green-700 mb-2">🎉 恭喜你，表現優異！</p>
                    <p>你在所有主題的表現都非常出色！點擊「✨ 產生個人化案例分析」來挑戰一個綜合性的進階案例，進一步鞏固你的實力吧！</p>
                `;
                recommendations.appendChild(recommendationText);
            }
        }
        
        // Function to generate new questions via API call
        async function generateNewQuestions() {
            // Get all unique categories from the current question set to provide context to the LLM
            const existingCategories = [...new Set(quizData.questions.map(q => q.category))];
            // Determine which difficulty level to generate for
            const difficultyToGenerate = currentDifficulty; // Generate questions for the current level
            
            const generateBtnTextOriginal = generateBtnText.textContent;
            generateMoreBtn.disabled = true;
            generateBtnText.textContent = "正在生成中...";
            generateMoreBtn.classList.add('flex', 'items-center', 'justify-center', 'gap-2');
            const loader = document.createElement('div');
            loader.classList.add('loader');
            generateMoreBtn.appendChild(loader);

            try {
                const prompt = `你是一個專業的呼吸治療師，請根據呼吸治療的臨床情境學習，為以下類別生成 3 個新的繁體中文測驗問題。請以 ${difficultyToGenerate} 的難度等級撰寫。每個問題都必須提供詳細的「教學內容」、「題目」、「四個選項（其中一個為正確答案）」和「解析」。
                    教學內容應以清晰、簡潔的文字解釋一個相關概念。
                    題目應為單選題，情境模擬。
                    四個選項中的正確答案須標註 "isCorrect": true。
                    解析應解釋為何該選項是正確的。

                    請使用以下類別: ${existingCategories.join(', ')}。
                    
                    **非常重要：你只能回傳一個純粹的 JSON 陣列，不包含任何額外的文字、格式或程式碼區塊。**
                    
                    回傳的格式必須為一個JSON陣列，每個物件包含以下欄位：
                    "category": (字串，從提供的類別中選擇)
                    "difficulty": "${difficultyToGenerate}"
                    "teaching": (字串，繁體中文教學內容)
                    "question": (字串，繁體中文題目)
                    "answerOptions": (陣列，包含四個物件，每個物件有 "text" 和 "isCorrect" 兩個欄位)
                    "rationale": (字串，繁體中文解析)
                    
                    範例格式:
                    [
                        {
                            "category": "基本評估與處置",
                            "difficulty": "${difficultyToGenerate}",
                            "teaching": "...",
                            "question": "...",
                            "answerOptions": [
                                { "text": "...", "isCorrect": false },
                                { "text": "...", "isCorrect": true },
                                { "text": "...", "isCorrect": false },
                                { "text": "...", "isCorrect": false }
                            ],
                            "rationale": "..."
                        }
                    ]
                `;

                let chatHistory = [];
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                const payload = {
                    contents: chatHistory,
                    generationConfig: {
                        responseMimeType: "application/json",
                        responseSchema: {
                            type: "ARRAY",
                            items: {
                                type: "OBJECT",
                                properties: {
                                    "category": { "type": "STRING" },
                                    "difficulty": { "type": "STRING" },
                                    "teaching": { "type": "STRING" },
                                    "question": { "type": "STRING" },
                                    "answerOptions": {
                                        "type": "ARRAY",
                                        "items": {
                                            "type": "OBJECT",
                                            "properties": {
                                                "text": { "type": "STRING" },
                                                "isCorrect": { "type": "BOOLEAN" }
                                            }
                                        }
                                    },
                                    "rationale": { "type": "STRING" }
                                }
                            }
                        }
                    }
                };
                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

                let response;
                let retries = 0;
                const maxRetries = 3;
                while (retries < maxRetries) {
                    try {
                        response = await fetch(apiUrl, {
                            method: 'POST',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify(payload)
                        });
                        if (response.status === 429) {
                            retries++;
                            const delay = Math.pow(2, retries) * 1000;
                            await new Promise(res => setTimeout(res, delay));
                            continue;
                        }
                        break;
                    } catch (error) {
                        retries++;
                        const delay = Math.pow(2, retries) * 1000;
                        await new Promise(res => setTimeout(res, delay));
                        if (retries === maxRetries) throw error;
                    }
                }

                if (!response || !response.ok) {
                    throw new Error(`API call failed with status: ${response.status}`);
                }
                
                // Get the text from the response
                const result = await response.json();
                const jsonText = result.candidates?.[0]?.content?.parts?.[0]?.text;

                if (!jsonText) {
                    throw new Error("Invalid response format from API. No text content found.");
                }

                let newQuestions;
                try {
                    // Try to find the JSON array part and parse it more robustly
                    const startIndex = jsonText.indexOf('[');
                    const endIndex = jsonText.lastIndexOf(']');
                    if (startIndex !== -1 && endIndex !== -1 && endIndex > startIndex) {
                        const jsonString = jsonText.substring(startIndex, endIndex + 1);
                        newQuestions = JSON.parse(jsonString);
                    } else {
                        // Fallback to direct parsing if no array delimiters found
                        newQuestions = JSON.parse(jsonText);
                    }
                } catch (e) {
                    console.error("Failed to parse JSON string. The string received was:", jsonText, "Error:", e);
                    throw new Error("Failed to parse JSON from API response. The response might be malformed or contain extra text.");
                }
                
                if (Array.isArray(newQuestions) && newQuestions.length > 0) {
                    newQuestions.forEach(q => {
                        if (q.question && q.answerOptions && q.rationale && q.category && q.difficulty) {
                            quizData.questions.push(q);
                        } else {
                            console.warn("Skipping malformed question object:", q);
                        }
                    });
                    
                    summarySection.classList.add('hidden');
                    quizFlow.classList.remove('hidden');
                    currentQuestionIndex = 0;
                    score = 0;
                    userAnswers = [];
                    correctCountAtDifficulty = 0;
                    initializeQuiz(); // Re-initialize with the new data
                    loadTeachingContent();
                    showMessage("已成功生成新的題目！");
                } else {
                    throw new Error("Failed to parse new questions or array is empty. The response was not a valid question array.");
                }
            } catch (error) {
                console.error("Error generating new questions:", error);
                showMessage("生成題目失敗，請再試一次。");
            } finally {
                generateMoreBtn.disabled = false;
                generateBtnText.textContent = generateBtnTextOriginal;
                generateMoreBtn.classList.remove('flex', 'items-center', 'justify-center', 'gap-2');
                if (loader.parentNode) {
                    loader.parentNode.removeChild(loader);
                }
            }
        }

        // Initialize quiz on page load
        initializeQuiz();
    </script>
</body>

</html>

