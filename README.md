<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>文化祭アンケート - 投票</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background-attachment: fixed;
        }
        .nature-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .option-button {
            transition: all 0.3s ease;
        }
        .option-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
        }
        .option-button.selected {
            background: linear-gradient(135deg, #10b981, #059669);
            color: white;
            transform: scale(1.02);
        }
        .submit-button {
            background: linear-gradient(135deg, #10b981, #059669);
            transition: all 0.3s ease;
        }
        .submit-button:hover {
            background: linear-gradient(135deg, #059669, #047857);
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.4);
        }
        .submit-button:disabled {
            background: #d1d5db;
            transform: none;
            box-shadow: none;
        }
        .floating-emoji {
            position: absolute;
            animation: float 3s ease-in-out infinite;
            pointer-events: none;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-15px) rotate(3deg); }
        }
        .success-animation {
            animation: successPulse 0.6s ease-out;
        }
        @keyframes successPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body class="min-h-screen p-4">
    <!-- 浮遊する絵文字 -->
    <div class="floating-emoji text-3xl" style="top: 15%; left: 10%; animation-delay: 0s;">🌸</div>
    <div class="floating-emoji text-2xl" style="top: 25%; right: 15%; animation-delay: 1s;">🎭</div>
    <div class="floating-emoji text-3xl" style="top: 70%; left: 5%; animation-delay: 2s;">🎵</div>
    <div class="floating-emoji text-2xl" style="bottom: 20%; right: 10%; animation-delay: 0.5s;">🎨</div>

    <div class="max-w-md mx-auto">
        <!-- ヘッダー -->
        <div class="text-center mb-6">
            <h1 class="text-4xl font-bold text-white mb-3">🌸 文化祭アンケート 🌸</h1>
            <p class="text-lg text-white opacity-90">あなたの声を聞かせてください！</p>
            <div class="mt-2 text-sm text-white opacity-75">
                📊 回答はリアルタイムで結果に反映されます
            </div>
        </div>

        <!-- デバッグ情報 -->
        <div id="debugInfo" class="mb-4 p-3 bg-blue-100 rounded-lg text-sm text-blue-800">
            <div>現在の投票数: <span id="currentVotes">0</span></div>
            <div>最終更新: <span id="debugTime">-</span></div>
            <div>保存状況: <span id="saveStatus">待機中</span></div>
        </div>

        <!-- アンケートフォーム -->
        <div class="nature-card rounded-3xl p-6 shadow-2xl mb-6">
            <form id="surveyForm" class="space-y-8">
                <!-- 質問1 -->
                <div>
                    <label class="block text-xl font-bold text-green-800 mb-4 text-center">
                        今日の文化祭はどうでしたか？
                    </label>
                    <div class="space-y-3">
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="satisfaction" data-value="とても楽しかった">
                            <span class="text-3xl mr-4">🌟</span>
                            <span>とても楽しかった</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="satisfaction" data-value="楽しかった">
                            <span class="text-3xl mr-4">😊</span>
                            <span>楽しかった</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="satisfaction" data-value="普通">
                            <span class="text-3xl mr-4">😐</span>
                            <span>普通</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="satisfaction" data-value="あまり楽しくなかった">
                            <span class="text-3xl mr-4">😕</span>
                            <span>あまり楽しくなかった</span>
                        </button>
                    </div>
                </div>

                <!-- 質問2 -->
                <div>
                    <label class="block text-xl font-bold text-green-800 mb-4 text-center">
                        一番印象に残った出し物は？
                    </label>
                    <div class="space-y-3">
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="favorite" data-value="演劇">
                            <span class="text-3xl mr-4">🎭</span>
                            <span>演劇</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="favorite" data-value="音楽発表">
                            <span class="text-3xl mr-4">🎵</span>
                            <span>音楽発表</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="favorite" data-value="展示">
                            <span class="text-3xl mr-4">🎨</span>
                            <span>展示</span>
                        </button>
                        <button type="button" class="option-button w-full p-4 rounded-2xl border-3 border-green-200 bg-white text-left font-semibold text-green-800 flex items-center text-lg" data-name="favorite" data-value="食べ物屋台">
                            <span class="text-3xl mr-4">🍜</span>
                            <span>食べ物屋台</span>
                        </button>
                    </div>
                </div>

                <button type="submit" id="submitButton" class="submit-button w-full text-white font-bold py-5 px-6 rounded-2xl text-xl shadow-lg disabled:cursor-not-allowed" disabled>
                    🌸 回答を送信する
                </button>
            </form>
        </div>

        <!-- 感謝メッセージ -->
        <div id="thankYouMessage" class="hidden">
            <div class="nature-card rounded-3xl p-8 shadow-2xl text-center success-animation">
                <div class="text-6xl mb-4">🎉</div>
                <h2 class="text-3xl font-bold text-green-800 mb-3">ありがとうございました！</h2>
                <p class="text-lg text-green-600 mb-4">あなたの回答が送信されました</p>
                <div class="bg-green-50 rounded-2xl p-4 border-2 border-green-200">
                    <p class="text-green-700 font-semibold">📊 結果ページで確認してね！</p>
                    <p class="text-sm text-green-600 mt-1">リアルタイムで反映されています</p>
                </div>
                <button id="submitAnotherButton" class="mt-6 bg-green-100 hover:bg-green-200 text-green-800 font-bold py-3 px-6 rounded-xl transition duration-300">
                    もう一度回答する
                </button>
            </div>
        </div>

        <!-- 進行状況インジケーター -->
        <div class="mt-4">
            <div class="flex justify-center space-x-2">
                <div id="progress1" class="w-3 h-3 rounded-full bg-white opacity-30"></div>
                <div id="progress2" class="w-3 h-3 rounded-full bg-white opacity-30"></div>
            </div>
        </div>
    </div>

    <script>
        let selectedAnswers = {
            satisfaction: null,
            favorite: null
        };

        // 初期データを確実に設定
        function initializeData() {
            const defaultData = {
                satisfaction: {
                    'とても楽しかった': 0,
                    '楽しかった': 0,
                    '普通': 0,
                    'あまり楽しくなかった': 0
                },
                favorite: {
                    '演劇': 0,
                    '音楽発表': 0,
                    '展示': 0,
                    '食べ物屋台': 0
                }
            };

            // 既存データがない場合は初期データを設定
            if (!localStorage.getItem('surveyData')) {
                localStorage.setItem('surveyData', JSON.stringify(defaultData));
                console.log('初期データを設定しました:', defaultData);
            }
        }

        // デバッグ用の現在の投票数表示
        function updateDebugInfo() {
            try {
                const data = JSON.parse(localStorage.getItem('surveyData')) || {
                    satisfaction: { 'とても楽しかった': 0, '楽しかった': 0, '普通': 0, 'あまり楽しくなかった': 0 },
                    favorite: { '演劇': 0, '音楽発表': 0, '展示': 0, '食べ物屋台': 0 }
                };
                const total = Object.values(data.satisfaction).reduce((a, b) => a + b, 0);
                document.getElementById('currentVotes').textContent = total;
                document.getElementById('debugTime').textContent = new Date().toLocaleTimeString();
                
                // 詳細なデータ表示
                console.log('現在のデータ:', data);
                console.log('総投票数:', total);
                
            } catch (error) {
                console.error('デバッグ情報更新エラー:', error);
                document.getElementById('saveStatus').textContent = 'エラー';
            }
        }

        // 初期化時にデータを設定
        document.addEventListener('DOMContentLoaded', function() {
            initializeData();
            updateDebugInfo();
            setInterval(updateDebugInfo, 1000);
        });

        // オプションボタンのクリック処理
        document.querySelectorAll('.option-button').forEach(button => {
            button.addEventListener('click', function() {
                const name = this.dataset.name;
                const value = this.dataset.value;
                
                // 同じグループの他のボタンの選択を解除
                document.querySelectorAll(`[data-name="${name}"]`).forEach(btn => {
                    btn.classList.remove('selected');
                });
                
                // このボタンを選択状態にする
                this.classList.add('selected');
                selectedAnswers[name] = value;
                
                // 進行状況を更新
                updateProgress();
                
                // 送信ボタンの状態を更新
                updateSubmitButton();
            });
        });

        // 進行状況の更新
        function updateProgress() {
            const progress1 = document.getElementById('progress1');
            const progress2 = document.getElementById('progress2');
            
            if (selectedAnswers.satisfaction) {
                progress1.classList.remove('opacity-30');
                progress1.classList.add('bg-green-400');
            }
            
            if (selectedAnswers.favorite) {
                progress2.classList.remove('opacity-30');
                progress2.classList.add('bg-green-400');
            }
        }

        // 送信ボタンの状態更新
        function updateSubmitButton() {
            const submitButton = document.getElementById('submitButton');
            const allAnswered = selectedAnswers.satisfaction && selectedAnswers.favorite;
            
            submitButton.disabled = !allAnswered;
            
            if (allAnswered) {
                submitButton.classList.remove('opacity-50');
                submitButton.innerHTML = '🌸 回答を送信する';
            }
        }

        // フォーム送信処理
        document.getElementById('surveyForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (!selectedAnswers.satisfaction || !selectedAnswers.favorite) {
                alert('すべての質問にお答えください 🌿');
                return;
            }
            
            // 送信中の表示
            const submitButton = document.getElementById('submitButton');
            submitButton.innerHTML = '📤 送信中...';
            submitButton.disabled = true;
            
            // データを保存
            saveVoteData();
            
            // 少し待ってから感謝メッセージを表示
            setTimeout(() => {
                showThankYouMessage();
            }, 800);
        });

        function saveVoteData() {
            try {
                document.getElementById('saveStatus').textContent = '保存中...';
                
                // 既存のデータを取得
                let surveyData = JSON.parse(localStorage.getItem('surveyData')) || {
                    satisfaction: {
                        'とても楽しかった': 0,
                        '楽しかった': 0,
                        '普通': 0,
                        'あまり楽しくなかった': 0
                    },
                    favorite: {
                        '演劇': 0,
                        '音楽発表': 0,
                        '展示': 0,
                        '食べ物屋台': 0
                    }
                };
                
                console.log('送信前のデータ:', surveyData);
                console.log('選択された回答:', selectedAnswers);
                
                // 新しい回答を追加
                surveyData.satisfaction[selectedAnswers.satisfaction]++;
                surveyData.favorite[selectedAnswers.favorite]++;
                
                console.log('送信後のデータ:', surveyData);
                
                // localStorageに保存
                localStorage.setItem('surveyData', JSON.stringify(surveyData));
                localStorage.setItem('lastVoteTime', Date.now().toString());
                
                // 保存確認
                const savedData = localStorage.getItem('surveyData');
                console.log('保存確認:', savedData);
                
                if (savedData) {
                    document.getElementById('saveStatus').textContent = '保存完了';
                    console.log('✅ 投票データを正常に保存しました！');
                } else {
                    throw new Error('データの保存に失敗しました');
                }
                
                // デバッグ情報を即座に更新
                updateDebugInfo();
                
            } catch (error) {
                console.error('❌ データ保存エラー:', error);
                document.getElementById('saveStatus').textContent = 'エラー';
                alert('データの保存に失敗しました。もう一度お試しください。');
            }
        }

        function showThankYouMessage() {
            document.getElementById('surveyForm').style.display = 'none';
            document.getElementById('thankYouMessage').classList.remove('hidden');
            
            // 紙吹雪エフェクト
            createConfetti();
        }

        function createConfetti() {
            const colors = ['🎉', '🎊', '✨', '🌟', '🎈'];
            
            for (let i = 0; i < 15; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.innerHTML = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.position = 'fixed';
                    confetti.style.left = Math.random() * 100 + '%';
                    confetti.style.top = '-50px';
                    confetti.style.fontSize = '2rem';
                    confetti.style.pointerEvents = 'none';
                    confetti.style.zIndex = '1000';
                    confetti.style.animation = 'fall 3s linear forwards';
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        confetti.remove();
                    }, 3000);
                }, i * 200);
            }
        }

        // もう一度回答するボタン
        document.getElementById('submitAnotherButton').addEventListener('click', function() {
            // リセット
            selectedAnswers = { satisfaction: null, favorite: null };
            
            // UI をリセット
            document.querySelectorAll('.option-button').forEach(btn => {
                btn.classList.remove('selected');
            });
            
            document.getElementById('progress1').classList.add('opacity-30');
            document.getElementById('progress1').classList.remove('bg-green-400');
            document.getElementById('progress2').classList.add('opacity-30');
            document.getElementById('progress2').classList.remove('bg-green-400');
            
            const submitButton = document.getElementById('submitButton');
            submitButton.innerHTML = '🌸 回答を送信する';
            submitButton.disabled = true;
            
            document.getElementById('saveStatus').textContent = '待機中';
            
            // フォームを再表示
            document.getElementById('surveyForm').style.display = 'block';
            document.getElementById('thankYouMessage').classList.add('hidden');
        });

        // CSS アニメーション追加
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fall {
                to {
                    transform: translateY(100vh) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97c54e9f97b6fcbd',t:'MTc1NzQwNjQ1NC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
