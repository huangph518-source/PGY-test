<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>呼吸治療臨床情境學習網</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
        }
        .container {
            max-width: 800px;
            margin: auto;
        }
        .card {
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 2rem;
            transition: all 0.3s ease;
        }
        .card:hover {
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15);
            transform: translateY(-2px);
        }
        .button {
            transition: all 0.2s ease;
        }
        .button:hover {
            transform: translateY(-1px);
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15);
        }
        .button:active {
            transform: translateY(0);
            box-shadow: none;
        }
        .fade-in {
            animation: fadeIn 0.8s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .option-button {
            border: 2px solid #e5e7eb;
            color: #4b5563;
        }
        .option-button:hover {
            background-color: #f9fafb;
            border-color: #d1d5db;
        }
        .correct-answer {
            background-color: #d1fae5;
            border-color: #34d399;
            color: #065f46;
        }
        .incorrect-answer {
            background-color: #fee2e2;
            border-color: #ef4444;
            color: #991b1b;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">

<div id="app" class="container card fade-in">
    <!-- Quiz will be rendered here -->
</div>

<script>
    const questions = [
        {
            "questionNumber": 1,
            "question": "教學內容：\n\n壓力支持通氣模式 (PSV) 是一種自發性通氣模式，患者每次呼吸都會得到預設的壓力支持，以協助其完成吸氣。此模式的主要參數包括壓力支持水平 (Pressure Support)、吐氣靈敏度 (Expiratory Trigger Sensitivity, ETS) 和潮氣容積上限 (V_T limit)。其中，吐氣靈敏度 (ETS) 決定了患者吸氣結束並轉為吐氣的時機。當吸氣流速下降到某個百分比時，呼吸器便會結束壓力支持，讓患者進入吐氣。一般來說，此百分比設定在25-40%之間。\n\n**臨床情境題：**\n\n一位65歲的男性患者，因慢性阻塞性肺病（COPD）急性惡化而使用呼吸器，模式設定為PSV。護理師觀察到，患者的吸氣時間過長，顯得費力，且無法有效吐氣。此時，您認為應調整下列哪一項參數來改善此問題？",
            "answerOptions": [
                { "text": "增加壓力支持水平 (Pressure Support)", "isCorrect": false, "rationale": "增加壓力支持水平可以增加每次呼吸的潮氣容積，但不會直接縮短吸氣時間或改善吐氣困難。" },
                { "text": "減少吐氣靈敏度 (Expiratory Trigger Sensitivity, ETS)", "isCorrect": false, "rationale": "減少吐氣靈敏度（例如從30%調降至20%），會讓吸氣時間拉長，反而會加劇患者的吸氣費力與吐氣困難。" },
                { "text": "增加吐氣靈敏度 (Expiratory Trigger Sensitivity, ETS)", "isCorrect": true, "rationale": "增加吐氣靈敏度（例如從30%調高至40%），可以讓呼吸器在吸氣流速下降較早時就結束壓力支持，縮短吸氣時間，有助於改善患者的吐氣困難與吸氣費力。" },
                { "text": "減少吐氣靈敏度 (Expiratory Trigger Sensitivity, ETS) 並增加壓力支持水平", "isCorrect": false, "rationale": "此選項同時包含了會加劇問題的參數調整（減少ETS）與不直接相關的調整，因此不是最佳的解決方案。" }
            ]
        },
        {
            "questionNumber": 2,
            "question": "教學內容：\n\n高流量鼻導管氧氣治療（High-Flow Nasal Cannula, HFNC）是一種能提供高流速、加溫加濕氧氣的治療方式，常用於輕至中度呼吸衰竭的患者。此治療的主要優點包括：提供穩定的氧氣濃度、降低吸氣阻力、提供輕微的正壓（PEEP），並有助於清除鼻咽部的死腔。\n\n**臨床情境題：**\n\n一位70歲男性患者，因肺炎導致低血氧，使用HFNC治療。設定為流速40 L/min，氧氣濃度 (FiO$_{2}$) 50%。患者的動脈血氣體分析結果顯示：PaO$_{2}$ 65 mmHg，SpO$_{2}$ 91%，PaCO$_{2}$ 48 mmHg。考量到患者的狀況，您認為下一步最恰當的處置為何？",
            "answerOptions": [
                { "text": "維持現有設定，並持續觀察", "isCorrect": false, "rationale": "患者的PaO$_{2}$和SpO$_{2}$仍未達到理想範圍（通常期望SpO$_{2}$ > 92-95%），因此維持現有設定可能無法有效改善低血氧。" },
                { "text": "增加HFNC的流速至60 L/min", "isCorrect": false, "rationale": "增加流速有助於降低呼吸阻力、提供更好的PEEP效應，並減少吸入外界空氣的比例，但單純增加流速對PaO$_{2}$的提升效果可能有限。" },
                { "text": "調高HFNC的氧氣濃度 (FiO$_{2}$) 至60%", "isCorrect": true, "rationale": "患者的PaO$_{2}$和SpO$_{2}$偏低，直接調高氧氣濃度 (FiO$_{2}$) 是最直接且有效的改善低血氧的方法。由於PaCO$_{2}$僅輕微升高，因此提高氧氣濃度是安全的。" },
                { "text": "改用傳統非再吸入型面罩 (Non-rebreather mask)", "isCorrect": false, "rationale": "HFNC提供的氧氣濃度和舒適度通常優於非再吸入型面罩，且能提供PEEP效應。在HFNC仍可調整的情況下，不應輕易更換治療方式。" }
            ]
        },
        {
            "questionNumber": 3,
            "question": "教學內容：\n\n呼吸器警報 (Ventilator Alarms) 是臨床照護中不可或缺的一部分。高壓警報 (High Peak Pressure Alarm) 是最常見的警報之一，它通常代表氣道壓力超過了設定的上限。導致高壓警報的原因可能多樣，包括：患者自主呼吸與呼吸器不同步、氣道分泌物過多、氣管內管或呼吸迴路扭結、支氣管痙攣或肺部順應性下降 (例如：肺水腫、氣胸)。\n\n**臨床情境題：**\n\n一位使用呼吸器的患者，突然持續發出高壓警報。當您抵達床邊時，發現患者正用力咳嗽，且呼吸迴路管路有明顯的扭結。在確認警報聲來源後，您應採取的首要步驟為何？",
            "answerOptions": [
                { "text": "立即呼叫醫師，請求協助", "isCorrect": false, "rationale": "在處理呼吸器警報時，應先進行初步判斷與處理，若問題無法自行排除或患者狀況危急，再尋求支援。此舉可能會延誤處理時間。" },
                { "text": "立即解除呼吸器管路，改用手動甦醒球給予通氣", "isCorrect": false, "rationale": "雖然這是緊急狀況下的處理方式，但在發現明確原因（管路扭結）且患者並無立即危險時，首要步驟應是排除該原因，而非直接中斷呼吸器通氣。" },
                { "text": "給予患者鎮靜劑以減少咳嗽", "isCorrect": false, "rationale": "在未確定高壓警報的根本原因前，給予鎮靜劑並非首要處置。此外，此舉可能延誤對管路問題的即時解決。" },
                { "text": "排除呼吸迴路管路的扭結", "isCorrect": true, "rationale": "當發現明確可解決的物理性問題（如管路扭結）時，應立即排除。這是最直接且能快速解除高壓警報、恢復正常通氣的首要步驟。" }
            ]
        },
        {
            "questionNumber": 4,
            "question": "教學內容：\n\n潮氣容積 (Tidal Volume, V$_{T}$) 是指單次呼吸所吸入或吐出的氣體量。在機械通氣中，設定適當的潮氣容積對於避免肺部過度擴張損傷 (Volutrauma) 至關重要。對於急性呼吸窘迫症候群 (ARDS) 的患者，為了保護肺臟，通常會採用較低的潮氣容積設定，目標值約為6 mL/kg 理想體重 (Predicted Body Weight, PBW)。計算理想體重 (PBW) 的公式為：男性PBW = 50 + 0.91 × (身高cm - 152.4)；女性PBW = 45.5 + 0.91 × (身高cm - 152.4)。\n\n**臨床情境題：**\n\n一位55歲女性ARDS患者，身高165 cm，體重80 kg。您應設定多少潮氣容積來進行肺保護性通氣？",
            "answerOptions": [
                { "text": "約360 mL", "isCorrect": false, "rationale": "此選項是根據患者實際體重80 kg計算 (80 × 6 = 480 mL)，但肺保護性通氣應根據理想體重計算，以避免肺部過度擴張。" },
                { "text": "約420 mL", "isCorrect": false, "rationale": "此選項是將患者身高165 cm代入女性PBW公式：PBW = 45.5 + 0.91 × (165 - 152.4) = 45.5 + 0.91 × 12.6 = 45.5 + 11.466 ≈ 57 kg。潮氣容積應設定為57 × 6 = 342 mL，此選項不符合計算結果。" },
                { "text": "約342 mL", "isCorrect": true, "rationale": "首先計算女性理想體重：PBW = 45.5 + 0.91 × (165 - 152.4) = 56.966 ≈ 57 kg。接著計算潮氣容積：57 kg × 6 mL/kg = 342 mL。此選項符合肺保護性通氣的建議潮氣容積。" },
                { "text": "約480 mL", "isCorrect": false, "rationale": "此選項是根據患者實際體重80 kg計算 (80 × 6 = 480 mL)，但肺保護性通氣應根據理想體重計算，以避免肺部過度擴張。" }
            ]
        },
        {
            "questionNumber": 5,
            "question": "教學內容：\n\n非侵入性正壓通氣 (Non-invasive Positive Pressure Ventilation, NIV) 是一種透過面罩而非氣管內管來提供呼吸支持的治療方式。NIV可以改善通氣、減少呼吸功，並常用於慢性阻塞性肺病 (COPD) 惡化引起的急性高碳酸血症 (Acute Hypercapnic Respiratory Failure)。常用的NIV模式包括壓力支持 (PSV) 與雙相氣道正壓 (Bilevel Positive Airway Pressure, BiPAP)。\n\n**臨床情境題：**\n\n一位75歲COPD患者，因急性呼吸衰竭而使用NIV治療。您發現患者的PaCO$_{2}$持續升高，且呼吸淺快。您認為應調整下列哪一項參數來改善通氣效率，以降低PaCO$_{2}$？",
            "answerOptions": [
                { "text": "降低吐氣末正壓 (EPAP)", "isCorrect": false, "rationale": "降低EPAP可以降低死腔再呼吸，但此舉也會減少對肺部塌陷的保護，且通常不會直接有效地改善二氧化碳滯留。" },
                { "text": "降低吸氣壓力 (IPAP)", "isCorrect": false, "rationale": "IPAP是提供呼吸支持的主要壓力，降低IPAP會減少潮氣容積，導致通氣不足，進而使PaCO$_{2}$升高。" },
                { "text": "增加吸氣壓力 (IPAP)", "isCorrect": true, "rationale": "增加IPAP可以增加每次呼吸的壓力支持，有助於增加潮氣容積與肺泡通氣量，進而有效降低PaCO$_{2}$，改善高碳酸血症。" },
                { "text": "增加吐氣末正壓 (EPAP)", "isCorrect": false, "rationale": "增加EPAP可以維持氣道開放，改善血氧。但若EPAP過高，可能造成患者吐氣困難，反而加重二氧化碳滯留。" }
            ]
        },
        {
            "questionNumber": 6,
            "question": "教學內容：\n\n高壓警報 (High Peak Pressure Alarm) 是臨床上最常見的呼吸器警報之一。當氣道壓力超過預設上限時，警報就會啟動。導致高壓警報的原因多樣，可大致分為患者端與呼吸器/管路端兩大類：\n\n- **患者端**：咳嗽、掙扎 (fighting the ventilator)、氣道分泌物增加、支氣管痙攣、肺部順應性下降 (如肺水腫、肺炎) 或氣胸。\n- **呼吸器/管路端**：呼吸迴路管路扭結或被壓住、氣管內管阻塞或扭結、潮濕瓶積水或出氣口阻塞。\n\n**臨床情境題：**\n\n一位因肺炎而使用呼吸器的患者，模式為PCV (壓力控制通氣)。突然發出高壓警報，您發現患者沒有掙扎或咳嗽，但警報持續響起。您檢查後發現呼吸迴路管路上並無扭結或積水，且痰量不多。您應接著優先評估下列哪一個狀況？",
            "answerOptions": [
                { "text": "患者是否出現肺水腫或肺炎惡化", "isCorrect": true, "rationale": "由於患者無掙扎或咳嗽，且初步排除管路問題，此時應考慮肺部狀況是否惡化，導致肺順應性下降而引發高壓。這是一個合理的後續評估。" },
                { "text": "立即更換呼吸器管路", "isCorrect": false, "rationale": "更換管路是解決管路問題的最終手段，但在此情境中已初步排除管路扭結與積水，不應在未確定問題前貿然更換。" },
                { "text": "立即給予患者鎮靜劑", "isCorrect": false, "rationale": "給予鎮靜劑適用於患者掙扎或與呼吸器不同步的情境，但題目已說明患者無掙扎或咳嗽，因此此舉不恰當。" },
                { "text": "檢查潮氣容積 (V_T)", "isCorrect": false, "rationale": "在壓力控制模式 (PCV) 下，呼吸器會給予固定的壓力，潮氣容積會隨肺部順應性變化，因此檢查潮氣容積可以反映肺部狀況，但此時應優先考量導致高壓的根本原因。" }
            ]
        },
        {
            "questionNumber": 7,
            "question": "教學內容：\n\n低潮氣容積警報 (Low Tidal Volume Alarm) 通常表示患者單次呼吸所得到的氣體量低於預設的下限。這代表患者可能沒有得到足夠的通氣。常見的原因包括：\n\n- **管路漏氣**：呼吸迴路、加溫加濕器、或氣管內管 cuff 漏氣。\n- **呼吸器設定不當**：吸氣時間 (Inspiratory Time) 過短、吸氣壓力 (PIP) 過低或吐氣末正壓 (PEEP) 過高。\n- **患者問題**：自主呼吸微弱、呼吸衰竭加劇。\n\n**臨床情境題：**\n\n一位使用PSV模式的患者，呼吸器持續發出低潮氣容積警報。您檢查後發現患者意識清楚，並無呼吸費力現象。您也確認所有管路連接都緊密，但警報聲依然持續。此時，您應該如何快速找出並解決問題？",
            "answerOptions": [
                { "text": "檢查並灌注氣管內管的cuff", "isCorrect": true, "rationale": "在確認管路連接都緊密後，氣管內管的cuff漏氣是導致低潮氣容積警報最常見的原因之一。此時應優先檢查cuff的壓力並進行灌注，以確保密封，解決漏氣問題。" },
                { "text": "增加呼吸器吸氣壓力 (PIP)", "isCorrect": false, "rationale": "雖然增加壓力可以增加潮氣容積，但如果問題是漏氣，這只是治標不治本，且可能導致不必要的氣道壓力過高。" },
                { "text": "改變呼吸器模式", "isCorrect": false, "rationale": "在未找出根本原因前，不應輕易改變呼吸器模式。此舉可能延誤處理真正的問題。" },
                { "text": "立即更換呼吸器", "isCorrect": false, "rationale": "更換呼吸器是最後的手段。在確定問題來源之前，應優先檢查所有可能的環節，例如cuff漏氣。" }
            ]
        },
        {
            "questionNumber": 8,
            "question": "教學內容：\n\n呼吸器漏氣 (Leak) 是指在通氣迴路或氣道中，氣體外洩的情形。漏氣可能導致潮氣容積不足、壓力不穩定，並引發警報。最常見的漏氣位置包括：\n\n- **氣管內管cuff**：氣囊壓力不足或破裂。\n- **呼吸迴路**：管路連接處鬆脫、加濕瓶蓋未旋緊。\n- **胸腔引流**：若有胸腔引流，引流管路或接頭可能漏氣。\n- **非侵入性通氣面罩 (NIV)**：面罩未貼合、綁帶過鬆。\n\n**臨床情境題：**\n\n一位使用NIV面罩通氣的患者，呼吸器持續發出低潮氣容積與低潮氣壓力警報。您發現面罩周圍有明顯的氣體外洩聲，且患者的臉部皮膚有壓痕。您應採取的首要處理為何？",
            "answerOptions": [
                { "text": "重新調整面罩綁帶並確認貼合度", "isCorrect": true, "rationale": "面罩漏氣是非侵入性通氣中最常見的問題。當發現面罩周圍有氣體外洩時，應立即調整綁帶與面罩位置，以確保其緊密貼合患者臉部，這是解決漏氣問題的首要步驟。" },
                { "text": "立即更換更大尺寸的面罩", "isCorrect": false, "rationale": "在未嘗試調整現有面罩的情況下，不應貿然更換。可能只是貼合度問題，而非面罩尺寸不當。" },
                { "text": "立即調高吸氣壓力 (IPAP)", "isCorrect": false, "rationale": "調高壓力會導致漏氣更加嚴重，並可能讓患者感到不適，加重臉部壓痕。" },
                { "text": "立即改用傳統氧氣面罩", "isCorrect": false, "rationale": "非侵入性通氣對患者的呼吸支持是必要的，在未嘗試解決漏氣問題前，不應輕易終止NIV治療。" }
            ]
        }
    ];

    let currentQuestionIndex = 0;
    const app = document.getElementById('app');

    function renderQuestion() {
        if (currentQuestionIndex >= questions.length) {
            renderResult();
            return;
        }

        const q = questions[currentQuestionIndex];
        const isTroubleshooting = currentQuestionIndex >= 5; // Assuming troubleshooting questions start from index 5
        const titleText = isTroubleshooting ? "故障排除專題" : "情境題庫";
        const questionText = q.question.replace(/\n/g, '<br>');

        const content = `
            <div class="space-y-6">
                <h1 class="text-3xl font-bold text-center text-gray-800">呼吸治療臨床情境學習網</h1>
                <h2 class="text-xl font-semibold text-center text-gray-600">${titleText}</h2>
                
                <div id="quiz-container" class="space-y-6">
                    <p class="text-sm font-medium text-gray-500 text-center">問題 ${currentQuestionIndex + 1} / ${questions.length}</p>
                    <div class="bg-gray-50 rounded-lg p-6">
                        <p class="text-gray-700 leading-relaxed">${questionText}</p>
                    </div>

                    <div id="options-container" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        ${q.answerOptions.map((option, index) => `
                            <button
                                class="option-button w-full text-left py-4 px-6 rounded-lg font-medium hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50"
                                data-index="${index}"
                            >
                                ${option.text}
                            </button>
                        `).join('')}
                    </div>

                    <div id="rationale-container" class="hidden">
                        <div class="bg-gray-100 rounded-lg p-6 mt-6">
                            <h3 class="text-lg font-bold text-gray-800">答案解析</h3>
                            <p id="rationale-text" class="mt-2 text-gray-600 leading-relaxed"></p>
                        </div>
                        <button id="next-button" class="mt-6 w-full py-3 bg-blue-600 text-white rounded-lg font-bold button">下一題</button>
                    </div>
                </div>
            </div>
        `;
        app.innerHTML = content;

        document.querySelectorAll('.option-button').forEach(button => {
            button.addEventListener('click', handleAnswer);
        });
        document.getElementById('next-button').addEventListener('click', () => {
            currentQuestionIndex++;
            renderQuestion();
        });
    }

    function handleAnswer(event) {
        const selectedIndex = parseInt(event.target.dataset.index, 10);
        const q = questions[currentQuestionIndex];
        
        document.querySelectorAll('.option-button').forEach(button => {
            const buttonIndex = parseInt(button.dataset.index, 10);
            button.disabled = true; // Disable all buttons after one is clicked

            if (q.answerOptions[buttonIndex].isCorrect) {
                button.classList.add('correct-answer');
            }
            
            if (buttonIndex === selectedIndex && !q.answerOptions[buttonIndex].isCorrect) {
                 button.classList.add('incorrect-answer');
            }
        });

        const rationaleText = document.getElementById('rationale-text');
        rationaleText.innerHTML = q.answerOptions[selectedIndex].rationale;
        
        document.getElementById('rationale-container').classList.remove('hidden');
    }
    
    function renderResult() {
        const content = `
            <div class="text-center space-y-6">
                <h1 class="text-3xl font-bold text-gray-800">測驗完成！</h1>
                <p class="text-gray-600 text-lg">您已完成所有題目。希望這些情境對您的學習有所幫助！</p>
                <button onclick="window.location.reload()" class="py-3 px-6 bg-blue-600 text-white rounded-lg font-bold button">重新開始測驗</button>
            </div>
        `;
        app.innerHTML = content;
    }

    // Initial render
    window.onload = renderQuestion;
</script>

</body>
</html>
