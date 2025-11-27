<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Advanced English Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Advanced English Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>pretend (fare finta)</h3>
                    <p><strong>Definition:</strong> To behave as if something is true when it is not; to simulate or feign.</p>
                    <p><strong>Usage:</strong> Often used when someone acts in a way that doesn't reflect reality.</p>
                    <p class="example"><strong>Example:</strong> "The children pretend to be superheroes when they play together."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>sweat</h3>
                    <p><strong>Definition:</strong> To excrete moisture through the pores of the skin, typically as a response to heat, physical exertion, or stress.</p>
                    <p><strong>Usage:</strong> Can be used literally or metaphorically to indicate hard work or anxiety.</p>
                    <p class="example"><strong>Example:</strong> "After running for 30 minutes, he began to sweat profusely."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>behave</h3>
                    <p><strong>Definition:</strong> To act or conduct oneself in a specified way, especially in relation to others.</p>
                    <p><strong>Usage:</strong> Often used when referring to appropriate or inappropriate actions.</p>
                    <p class="example"><strong>Example:</strong> "The children were told to behave properly at the wedding."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>high stakes</h3>
                    <p><strong>Definition:</strong> A situation involving the potential for significant gain or loss.</p>
                    <p><strong>Usage:</strong> Often used in contexts like gambling, business, or important decisions.</p>
                    <p class="example"><strong>Example:</strong> "The negotiation was a high-stakes game that could determine the company's future."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>disappear</h3>
                    <p><strong>Definition:</strong> To cease to be visible; to vanish.</p>
                    <p><strong>Usage:</strong> Can refer to people, objects, or abstract concepts.</p>
                    <p class="example"><strong>Example:</strong> "The magician made the rabbit disappear in front of the audience."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>lightning</h3>
                    <p><strong>Definition:</strong> A sudden electrostatic discharge during a thunderstorm, typically seen as a bright flash.</p>
                    <p><strong>Usage:</strong> Can be used literally or metaphorically to describe something very fast.</p>
                    <p class="example"><strong>Example:</strong> "The lightning illuminated the entire night sky for a brief moment."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>escape</h3>
                    <p><strong>Definition:</strong> To break free from confinement or control; to avoid something undesirable.</p>
                    <p><strong>Usage:</strong> Can refer to physical escape or mental/emotional avoidance.</p>
                    <p class="example"><strong>Example:</strong> "The prisoner managed to escape from the high-security prison."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>beliefs</h3>
                    <p><strong>Definition:</strong> Mental acceptance or conviction that something is true or real.</p>
                    <p><strong>Usage:</strong> Often refers to religious, political, or personal convictions.</p>
                    <p class="example"><strong>Example:</strong> "Her strong beliefs guided her decisions throughout her life."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>once</h3>
                    <p><strong>Definition:</strong> At some time in the past; formerly; or one single time.</p>
                    <p><strong>Usage:</strong> Can be used as an adverb or conjunction.</p>
                    <p class="example"><strong>Example:</strong> "I visited Paris once when I was a teenager."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>rights (diritti)</h3>
                    <p><strong>Definition:</strong> Moral or legal entitlements to have or do something.</p>
                    <p><strong>Usage:</strong> Often used in contexts of human rights, civil rights, or legal rights.</p>
                    <p class="example"><strong>Example:</strong> "Every citizen should be aware of their legal rights."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>as the crow flies</h3>
                    <p><strong>Definition:</strong> In a straight line; the shortest distance between two points.</p>
                    <p><strong>Usage:</strong> Used to describe distance without considering the actual route or obstacles.</p>
                    <p class="example"><strong>Example:</strong> "The town is only 10 miles away as the crow flies, but the winding road makes it 15 miles."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">pretend</span>
                    <span class="word-option">sweat</span>
                    <span class="word-option">behave</span>
                    <span class="word-option">high stakes</span>
                    <span class="word-option">disappear</span>
                    <span class="word-option">lightning</span>
                    <span class="word-option">escape</span>
                    <span class="word-option">beliefs</span>
                    <span class="word-option">once</span>
                    <span class="word-option">rights</span>
                    <span class="word-option">as the crow flies</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="pretend" onclick="selectMatch(this)">pretend</div>
                    <div class="match-item" data-word="sweat" onclick="selectMatch(this)">sweat</div>
                    <div class="match-item" data-word="behave" onclick="selectMatch(this)">behave</div>
                    <div class="match-item" data-word="high stakes" onclick="selectMatch(this)">high stakes</div>
                    <div class="match-item" data-word="disappear" onclick="selectMatch(this)">disappear</div>
                    <div class="match-item" data-word="lightning" onclick="selectMatch(this)">lightning</div>
                    <div class="match-item" data-word="escape" onclick="selectMatch(this)">escape</div>
                    <div class="match-item" data-word="beliefs" onclick="selectMatch(this)">beliefs</div>
                    <div class="match-item" data-word="once" onclick="selectMatch(this)">once</div>
                    <div class="match-item" data-word="rights" onclick="selectMatch(this)">rights</div>
                    <div class="match-item" data-word="as the crow flies" onclick="selectMatch(this)">as the crow flies</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "pretend" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To work very hard</div>
                    <div class="option" onclick="selectOption(this, true)">To behave as if something is true when it is not</div>
                    <div class="option" onclick="selectOption(this, false)">To disappear suddenly</div>
                    <div class="option" onclick="selectOption(this, false)">To believe strongly in something</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "sweat" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To run very fast</div>
                    <div class="option" onclick="selectOption(this, true)">To excrete moisture through the skin</div>
                    <div class="option" onclick="selectOption(this, false)">To think deeply</div>
                    <div class="option" onclick="selectOption(this, false)">To make a loud noise</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "behave" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To have strong opinions</div>
                    <div class="option" onclick="selectOption(this, true)">To act or conduct oneself in a specified way</div>
                    <div class="option" onclick="selectOption(this, false)">To disappear quickly</div>
                    <div class="option" onclick="selectOption(this, false)">To work under pressure</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "high stakes" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of gambling game</div>
                    <div class="option" onclick="selectOption(this, true)">A situation with potential for significant gain or loss</div>
                    <div class="option" onclick="selectOption(this, false)">A very tall building</div>
                    <div class="option" onclick="selectOption(this, false)">An important person</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What does "disappear" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To appear suddenly</div>
                    <div class="option" onclick="selectOption(this, true)">To cease to be visible; to vanish</div>
                    <div class="option" onclick="selectOption(this, false)">To make a loud sound</div>
                    <div class="option" onclick="selectOption(this, false)">To work very hard</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "lightning" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of rain</div>
                    <div class="option" onclick="selectOption(this, true)">A sudden electrostatic discharge during a thunderstorm</div>
                    <div class="option" onclick="selectOption(this, false)">A very bright light</div>
                    <div class="option" onclick="selectOption(this, false)">A fast animal</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "escape" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To enter a place</div>
                    <div class="option" onclick="selectOption(this, true)">To break free from confinement or control</div>
                    <div class="option" onclick="selectOption(this, false)">To capture someone</div>
                    <div class="option" onclick="selectOption(this, false)">To hide something</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What are "beliefs"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Physical objects</div>
                    <div class="option" onclick="selectOption(this, true)">Mental acceptance that something is true or real</div>
                    <div class="option" onclick="selectOption(this, false)">Legal documents</div>
                    <div class="option" onclick="selectOption(this, false)">Types of food</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "once" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Many times</div>
                    <div class="option" onclick="selectOption(this, true)">At some time in the past; one single time</div>
                    <div class="option" onclick="selectOption(this, false)">In the future</div>
                    <div class="option" onclick="selectOption(this, false)">Never</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What are "rights"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Responsibilities</div>
                    <div class="option" onclick="selectOption(this, true)">Moral or legal entitlements</div>
                    <div class="option" onclick="selectOption(this, false)">Physical abilities</div>
                    <div class="option" onclick="selectOption(this, false)">Types of food</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What does "as the crow flies" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Following a winding path</div>
                    <div class="option" onclick="selectOption(this, true)">In a straight line; the shortest distance</div>
                    <div class="option" onclick="selectOption(this, false)">Flying very high</div>
                    <div class="option" onclick="selectOption(this, false)">Moving very slowly</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "pretend", text: "To behave as if something is true when it is not" },
            { meaning: "sweat", text: "To excrete moisture through the skin" },
            { meaning: "behave", text: "To act or conduct oneself in a specified way" },
            { meaning: "high stakes", text: "A situation with potential for significant gain or loss" },
            { meaning: "disappear", text: "To cease to be visible; to vanish" },
            { meaning: "lightning", text: "A sudden electrostatic discharge during a thunderstorm" },
            { meaning: "escape", text: "To break free from confinement or control" },
            { meaning: "beliefs", text: "Mental acceptance that something is true or real" },
            { meaning: "once", text: "At some time in the past; one single time" },
            { meaning: "rights", text: "Moral or legal entitlements" },
            { meaning: "as the crow flies", text: "In a straight line; the shortest distance" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "Children often <input type='text' class='fill-blank' data-answer='pretend' placeholder='answer'> to be superheroes when they play.", answer: "pretend" },
            { text: "After running for 30 minutes, he began to <input type='text' class='fill-blank' data-answer='sweat' placeholder='answer'> profusely.", answer: "sweat" },
            { text: "Parents expect their children to <input type='text' class='fill-blank' data-answer='behave' placeholder='answer'> properly in public places.", answer: "behave" },
            { text: "The business negotiation was a <input type='text' class='fill-blank' data-answer='high stakes' placeholder='answer'> situation that could determine the company's future.", answer: "high stakes" },
            { text: "The magician made the rabbit <input type='text' class='fill-blank' data-answer='disappear' placeholder='answer'> in front of the amazed audience.", answer: "disappear" },
            { text: "During the storm, the <input type='text' class='fill-blank' data-answer='lightning' placeholder='answer'> illuminated the entire sky for a brief moment.", answer: "lightning" },
            { text: "The prisoner managed to <input type='text' class='fill-blank' data-answer='escape' placeholder='answer'> from the high-security prison.", answer: "escape" },
            { text: "Everyone should respect other people's religious <input type='text' class='fill-blank' data-answer='beliefs' placeholder='answer'> even if they differ from their own.", answer: "beliefs" },
            { text: "I visited Rome <input type='text' class='fill-blank' data-answer='once' placeholder='answer'> when I was a child, and I've wanted to return ever since.", answer: "once" },
            { text: "Every citizen should be aware of their legal <input type='text' class='fill-blank' data-answer='rights' placeholder='answer'> and responsibilities.", answer: "rights" },
            { text: "The town is only 5 miles away <input type='text' class='fill-blank' data-answer='as the crow flies' placeholder='answer'>, but the winding road makes it 8 miles.", answer: "as the crow flies" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
