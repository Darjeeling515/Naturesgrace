<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nature's Grace - サプリメント公式通販</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkbg: '#050505',
                        darkcard: '#111111',
                        darkaccent: '#8b0000',
                    }
                }
            }
        }
    </script>
    <style>
        /* カスタムスクロールバーとアニメーション */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .dark ::-webkit-scrollbar-thumb { background: #3f3f46; }

        .fade-in { animation: fadeIn 0.5s ease-in forwards; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .glitch {
            position: relative;
            text-shadow: 0.05em 0 0 #ff0000, -0.05em -0.025em 0 #00ff00, -0.025em 0.05em 0 #0000ff;
            animation: glitch 500ms infinite;
        }
        @keyframes glitch {
            0% { text-shadow: 0.05em 0 0 #ff0000, -0.05em -0.025em 0 #00ff00, -0.025em 0.05em 0 #0000ff; }
            14% { text-shadow: 0.05em 0 0 #ff0000, -0.05em -0.025em 0 #00ff00, -0.025em 0.05em 0 #0000ff; }
            15% { text-shadow: -0.05em -0.025em 0 #ff0000, 0.025em 0.025em 0 #00ff00, -0.05em -0.05em 0 #0000ff; }
            49% { text-shadow: -0.05em -0.025em 0 #ff0000, 0.025em 0.025em 0 #00ff00, -0.05em -0.05em 0 #0000ff; }
            50% { text-shadow: 0.025em 0.05em 0 #ff0000, 0.05em 0 0 #00ff00, 0 -0.05em 0 #0000ff; }
            99% { text-shadow: 0.025em 0.05em 0 #ff0000, 0.05em 0 0 #00ff00, 0 -0.05em 0 #0000ff; }
            100% { text-shadow: -0.025em 0 0 #ff0000, -0.025em -0.025em 0 #00ff00, -0.025em -0.05em 0 #0000ff; }
        }

        /* トースト通知 */
        #toast {
            visibility: hidden;
            min-width: 250px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 8px;
            padding: 16px;
            position: fixed;
            z-index: 10000;
            left: 50%;
            bottom: 30px;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.3s, bottom 0.3s;
        }
        #toast.show {
            visibility: visible;
            opacity: 1;
            bottom: 50px;
        }
        .dark #toast {
            background-color: #8b0000;
            border: 1px solid #ff0000;
        }
    </style>
</head>
<body class="bg-green-50 text-slate-800 transition-colors duration-1000 font-sans dark:bg-darkbg dark:text-gray-300">

    <!-- 通知トースト -->
    <div id="toast">メッセージ</div>

    <!-- モーダルオーバーレイ -->
    <div id="modal-overlay" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <!-- 警告モーダル -->
        <div id="warning-modal" class="hidden bg-darkcard border border-red-800 text-center p-8 rounded-xl max-w-lg w-full shadow-[0_0_30px_rgba(220,38,38,0.3)]">
            <h2 class="text-3xl font-bold text-red-600 mb-4 glitch">【警告】認証完了</h2>
            <p class="text-gray-300 mb-6 leading-relaxed">
                これより先は一般法規適用外の特設カタログとなります。<br>
                商品の性質上、閲覧および購入による一切の責任は負いかねます。
            </p>
            <div class="flex gap-4 justify-center">
                <button onclick="closeModal()" class="px-6 py-2 border border-gray-600 text-gray-400 rounded hover:bg-gray-800 transition">キャンセル</button>
                <button onclick="executeTransition()" class="px-6 py-2 bg-red-900 hover:bg-red-700 text-white font-bold rounded border border-red-500 transition shadow-[0_0_10px_rgba(220,38,38,0.5)]">承諾して入室</button>
            </div>
        </div>

        <!-- カートモーダル -->
        <div id="cart-modal" class="hidden bg-white dark:bg-darkcard dark:border-red-900 dark:border p-8 rounded-xl max-w-2xl w-full shadow-2xl relative max-h-[90vh] overflow-y-auto">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-500 hover:text-gray-800 dark:text-gray-400 dark:hover:text-white text-2xl">&times;</button>
            
            <h2 id="cart-title" class="text-2xl font-bold mb-6 dark:text-red-500 border-b pb-2 dark:border-red-900">ショッピングカート</h2>
            
            <div id="cart-content" class="min-h-[100px]">
                <!-- JSで動的に書き換え -->
            </div>
            
            <div class="mt-8 text-right">
                <button onclick="closeModal()" class="px-6 py-2 bg-gray-200 text-gray-800 rounded hover:bg-gray-300 dark:bg-gray-800 dark:text-white dark:hover:bg-gray-700 transition">閉じる</button>
            </div>
        </div>
    </div>

    <!-- ヘッダー -->
    <header class="bg-white dark:bg-[#0a0a0a] shadow-md dark:shadow-red-900/20 sticky top-0 z-40 transition-colors duration-1000 border-b dark:border-red-900/50 border-transparent">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div>
                <h1 id="site-title" class="text-2xl font-bold text-green-700 dark:text-red-600 transition-colors">Nature's Grace</h1>
                <p id="site-subtitle" class="text-xs text-gray-500 dark:text-gray-400">自然の力で、健やかな毎日を</p>
            </div>
            <div class="flex items-center gap-4">
                <button id="return-btn" onclick="returnToNormal()" class="hidden px-4 py-2 text-sm border border-gray-600 text-gray-400 hover:text-white hover:border-white rounded transition">表サイトへ戻る</button>
                <button onclick="openCart()" class="flex items-center gap-2 bg-green-50 text-green-700 px-4 py-2 rounded-lg font-bold hover:bg-green-100 transition shadow-sm dark:bg-black dark:text-red-500 dark:border dark:border-red-800 dark:hover:bg-red-900/30">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 0a2 2 0 100 4 2 2 0 000-4z" /></svg>
                    カート
                </button>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
        <!-- プロモーションコード入力欄 (表でのみ表示) -->
        <div id="promo-section" class="mb-16 bg-gradient-to-r from-green-100 to-teal-50 rounded-2xl p-8 shadow-sm border border-green-200 text-center transition-all duration-500">
            <h2 class="text-xl font-bold text-green-800 mb-2">★ VIP会員様限定プロモーション ★</h2>
            <p class="text-gray-600 mb-6">招待状に記載のコードを入力して、特別セールに参加しましょう。</p>
            <div class="flex justify-center items-center gap-3 max-w-md mx-auto">
                <input type="password" id="promo-code" placeholder="例: 1111" class="flex-1 px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent text-center tracking-widest text-lg shadow-inner">
                <button onclick="checkCode()" class="px-8 py-3 bg-green-600 hover:bg-green-700 text-white font-bold rounded-lg transition shadow-md">適用</button>
            </div>
            <p id="error-msg" class="text-red-500 mt-3 font-bold hidden opacity-0 transition-opacity">※無効なプロモーションコードです</p>
        </div>

        <!-- ヒーローヘッダー (裏でのみ表示) -->
        <div id="dark-hero" class="hidden mb-16 text-center border-b border-red-900 pb-8 pt-8">
            <h2 class="text-5xl font-black text-red-600 mb-4 glitch tracking-widest">UNDERGROUND MARKET</h2>
            <p class="text-red-500 text-sm tracking-widest font-mono">CONNECTION SECURED. NO TRACES.</p>
        </div>

        <!-- 商品グリッド -->
        <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            <!-- JSで動的に生成 -->
        </div>
    </main>

    <footer class="bg-white dark:bg-[#050505] border-t dark:border-red-900/30 py-8 text-center text-gray-500 dark:text-gray-700 transition-colors mt-auto">
        <p id="footer-text">&copy; 2026 Nature's Grace. All rights reserved.</p>
    </footer>

    <script>
        // --- データ定義 ---
        const normalProducts = [
            { id: "N-001", name: "ピュアビタミンC 1000", desc: "レモン50個分のビタミンC。透明感のある毎日に。", price: "¥1,800", icon: "🍋" },
            { id: "N-002", name: "オーガニックプロテイン", desc: "植物由来のタンパク質。人工甘味料不使用。", price: "¥3,980", icon: "🌱" },
            { id: "N-003", name: "DHA&EPA フィッシュオイル", desc: "青魚のサラサラ成分。考える力をサポート。", price: "¥2,400", icon: "🐟" },
            { id: "N-004", name: "マルチビタミン＆ミネラル", desc: "22種類の必須栄養素をバランス良く配合。", price: "¥2,100", icon: "💊" },
            { id: "N-005", name: "プレミアムマカ＆亜鉛", desc: "エネルギッシュな毎日をサポート。", price: "¥2,800", icon: "⚡" },
            { id: "N-006", name: "ヘム鉄プラス葉酸", desc: "吸収率の高いヘム鉄を採用。女性の味方。", price: "¥1,650", icon: "🩸" },
            { id: "N-007", name: "カルシウム＆マグネシウム", desc: "理想のバランス2:1で配合。丈夫な体に。", price: "¥1,500", icon: "🦴" },
            { id: "N-008", name: "ビタミンB群コンプレックス", desc: "エネルギー生成を助ける8種類のビタミンB群。", price: "¥1,200", icon: "✨" },
            { id: "N-009", name: "快眠サポート メラトニン", desc: "深い休息をサポートし、すっきりとした朝へ。", price: "¥2,900", icon: "🌙" },
            { id: "N-010", name: "プロバイオティクス乳酸菌", desc: "奥まで届くカプセルで腸内環境を整える。", price: "¥3,200", icon: "🦠" },
            { id: "N-011", name: "低分子コラーゲンペプチド", desc: "吸収力にこだわったコラーゲン。ハリを。", price: "¥3,500", icon: "💧" },
            { id: "N-012", name: "ビルベリーEX＆ルテイン", desc: "PCやスマホをよく使う方に。クリアな視界を。", price: "¥2,600", icon: "👁️" },
            { id: "N-013", name: "ヒアルロン酸モイスチャー", desc: "内側から潤いをキープする美容サプリ。", price: "¥2,200", icon: "💦" },
            { id: "N-014", name: "高麗人参エキストラクト", desc: "古来から伝わる滋養強壮成分を凝縮。", price: "¥4,500", icon: "🌿" },
            { id: "N-015", name: "グルコサミン＆コンドロイチン", desc: "スムーズな歩みをサポートする軟骨成分。", price: "¥3,100", icon: "🏃" },
            { id: "N-016", name: "食物繊維イヌリン", desc: "毎日のスッキリをサポートする水溶性食物繊維。", price: "¥1,400", icon: "🌾" }
        ];

        const darkProducts = [
            { id: "DW-001", name: "【指定劇薬】仮死後致死カプセル", desc: "服用後1時間の「仮死状態」に陥り、その後多臓器不全により確実に死亡する。※カートに追加済", price: "¥1,500,000", icon: "💀" },
            { id: "DW-002", name: "忘却の滴（記憶消去剤）", desc: "直近24時間の記憶を不可逆的に完全に消去する無色無臭の液体。", price: "¥850,000", icon: "🧠" },
            { id: "DW-003", name: "狂気の粉（幻覚誘発剤）", desc: "極度のパラノイアと悪夢のような幻覚を72時間継続させる。", price: "¥420,000", icon: "👁️‍🗨️" },
            { id: "DW-004", name: "暴走ステロイド【リミットブレイク】", desc: "筋力を通常の5倍に引き上げるが、効果終了後に筋繊維が崩壊する。", price: "¥600,000", icon: "💉" },
            { id: "DW-005", name: "マインドハック・シリンジ", desc: "対象の自我を奪い、術者の命令に絶対服従させる薬液。", price: "¥2,800,000", icon: "🔗" },
            { id: "DW-006", name: "ペインキラー・ゼロ", desc: "痛覚神経を焼き切る。致命傷を負っても一切の痛みを感じない。", price: "¥300,000", icon: "⚡" },
            { id: "DW-007", name: "不眠不休剤（デスマーチ）", desc: "14日間一睡もせず活動可能になるが、終了時に脳血管が破裂する。", price: "¥550,000", icon: "⏱️" },
            { id: "DW-008", name: "感情凍結シロップ", desc: "扁桃体を麻痺させ、喜怒哀楽と恐怖心を完全に失わせる。", price: "¥700,000", icon: "🧊" },
            { id: "DW-009", name: "クロノス・エリクサー", desc: "寿命を10年削り、一時的に肉体を全盛期まで若返らせる。", price: "¥3,500,000", icon: "⏳" },
            { id: "DW-010", name: "ブラッドボイル・パウダー", desc: "血圧を数秒で異常上昇させ、自然死に見せかけた脳溢血を引き起こす。", price: "¥1,200,000", icon: "🩸" },
            { id: "DW-011", name: "虚無堕ちのタブレット", desc: "精神構造を破壊し、一切の反応を示さない廃人へと変貌させる。", price: "¥1,800,000", icon: "⬛" },
            { id: "DW-012", name: "即効性細胞融解液", desc: "皮膚に触れた瞬間から組織をドロドロに溶かす劇薬。", price: "¥2,500,000", icon: "🧪" },
            { id: "DW-013", name: "真実の吐息（自白剤改）", desc: "脳の嘘をつく機能を麻痺させ、質問に対して全て真実を強制的に喋らせる。", price: "¥900,000", icon: "🗣️" },
            { id: "DW-014", name: "サイレント・パルス", desc: "服用後、声帯の神経を一時的に麻痺させ、48時間一切の声を奪う。", price: "¥250,000", icon: "🔇" },
            { id: "DW-015", name: "腐敗促進ガス弾", desc: "密閉空間で使用すると、有機物の腐敗速度を通常の1000倍に加速させる。", price: "¥4,000,000", icon: "☣️" },
            { id: "DW-016", name: "ドッペルゲンガー・エキス", desc: "顔の骨格と筋肉を一時的に軟化させ、他者の顔を模倣しやすくする。", price: "¥5,500,000", icon: "🎭" }
        ];

        // --- 状態管理 ---
        let isDarkMode = false;
        let toastTimeout;

        // --- UI描画関数 ---
        function renderProducts(products, isDark) {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = '';
            
            products.forEach((p, index) => {
                const delay = index * 50; // アニメーションのディレイ
                
                if (!isDark) {
                    // 表のカードUI
                    grid.innerHTML += `
                        <div class="bg-white rounded-xl p-6 shadow-md hover:shadow-xl transition-shadow border border-gray-100 flex flex-col h-full fade-in" style="animation-delay: ${delay}ms; opacity: 0;">
                            <div class="text-4xl text-center mb-4 bg-green-50 w-16 h-16 mx-auto rounded-full flex items-center justify-center">${p.icon}</div>
                            <div class="text-xs text-gray-400 font-mono mb-2">品番: ${p.id}</div>
                            <h3 class="text-lg font-bold text-gray-800 mb-2 leading-tight">${p.name}</h3>
                            <p class="text-sm text-gray-600 flex-grow mb-4">${p.desc}</p>
                            <div class="text-xl font-bold text-green-600 mb-4">${p.price}</div>
                            <button onclick="showToast('「${p.name}」をカートに追加しました')" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-lg transition-colors mt-auto">カートに入れる</button>
                        </div>
                    `;
                } else {
                    // 裏のカードUI
                    grid.innerHTML += `
                        <div class="bg-darkcard rounded-lg p-6 shadow-[0_4px_15px_rgba(0,0,0,0.5)] hover:shadow-[0_4px_20px_rgba(220,38,38,0.2)] transition-shadow border border-red-900/30 flex flex-col h-full fade-in relative overflow-hidden group" style="animation-delay: ${delay}ms; opacity: 0;">
                            <div class="absolute top-0 right-0 bg-red-900 text-white text-[10px] px-2 py-1 font-mono rounded-bl-lg opacity-80">CLASSIFIED</div>
                            <div class="text-3xl mb-4 grayscale group-hover:grayscale-0 transition-all">${p.icon}</div>
                            <div class="text-xs text-red-500 font-mono mb-1">CODE: ${p.id}</div>
                            <h3 class="text-lg font-bold text-gray-200 mb-2 leading-tight group-hover:text-red-400 transition-colors">${p.name}</h3>
                            <p class="text-sm text-gray-400 flex-grow mb-4 border-l-2 border-red-900 pl-2">${p.desc}</p>
                            <div class="text-xl font-bold text-red-600 mb-4 font-mono">${p.price}</div>
                            <button onclick="showToast('承認待機中... 取引ログは暗号化されます。')" class="w-full bg-transparent hover:bg-red-900/40 text-red-500 hover:text-white font-bold py-2 px-4 rounded border border-red-800 transition-colors mt-auto uppercase tracking-widest text-sm">取扱申請</button>
                        </div>
                    `;
                }
            });
        }

        // カスタムトースト通知 (alertの代わり)
        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.innerText = message;
            toast.classList.add('show');
            
            clearTimeout(toastTimeout);
            toastTimeout = setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // --- ロジック関数 ---
        
        // パスワード判定
        function checkCode() {
            const code = document.getElementById('promo-code').value;
            const errorMsg = document.getElementById('error-msg');
            
            if (code === "0729") {
                errorMsg.classList.add('hidden');
                errorMsg.classList.remove('opacity-100');
                document.getElementById('promo-code').value = '';
                
                // 警告モーダルを表示
                document.getElementById('modal-overlay').classList.remove('hidden');
                document.getElementById('warning-modal').classList.remove('hidden');
            } else {
                errorMsg.classList.remove('hidden');
                // reflowを挟んでアニメーション
                void errorMsg.offsetWidth; 
                errorMsg.classList.add('opacity-100');
            }
        }

        // モーダルを閉じる
        function closeModal() {
            document.getElementById('modal-overlay').classList.add('hidden');
            document.getElementById('warning-modal').classList.add('hidden');
            document.getElementById('cart-modal').classList.add('hidden');
        }

        // 裏世界へ移行
        function executeTransition() {
            closeModal();
            isDarkMode = true;
            document.documentElement.classList.add('dark');
            
            // UIの切り替え
            document.getElementById('promo-section').classList.add('hidden');
            document.getElementById('dark-hero').classList.remove('hidden');
            document.getElementById('return-btn').classList.remove('hidden');
            
            // テキストの書き換え
            document.getElementById('site-title').innerText = "UNDERGROUND PHARMACY";
            document.getElementById('site-subtitle').innerText = "※取引記録は全て破棄されます";
            document.getElementById('footer-text').innerHTML = "ENCRYPTED CONNECTION <span class='text-red-500'>SECURE</span>";
            
            // 商品再描画
            renderProducts(darkProducts, true);
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // 表世界へ戻る
        function returnToNormal() {
            isDarkMode = false;
            document.documentElement.classList.remove('dark');
            
            // UIの切り替え
            document.getElementById('promo-section').classList.remove('hidden');
            document.getElementById('dark-hero').classList.add('hidden');
            document.getElementById('return-btn').classList.add('hidden');
            
            // テキストの書き換え
            document.getElementById('site-title').innerText = "Nature's Grace";
            document.getElementById('site-subtitle').innerText = "自然の力で、健やかな毎日を";
            document.getElementById('footer-text').innerHTML = "&copy; 2026 Nature's Grace. All rights reserved.";
            
            // 商品再描画
            renderProducts(normalProducts, false);
            window.scrollTo({ top: 0, behavior: 'smooth' });
            showToast("安全な接続に切り替わりました");
        }

        // カートを開く
        function openCart() {
            const content = document.getElementById('cart-content');
            const title = document.getElementById('cart-title');
            
            if (!isDarkMode) {
                // 表のカート
                title.innerText = "ショッピングカート";
                content.innerHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 mx-auto mb-4 text-gray-300" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 0a2 2 0 100 4 2 2 0 000-4z" /></svg>
                        <p>現在カートには何も入っていません。</p>
                    </div>
                `;
            } else {
                // 裏のカート (劇薬とレシピ入り、制限時間「2時間」)
                title.innerHTML = "<span class='glitch'>ENCRYPTED CART DATA</span>";
                content.innerHTML = `
                    <div class="bg-red-900/10 border border-red-800 p-6 rounded-lg text-gray-300 relative overflow-hidden">
                        <div class="absolute top-0 left-0 w-1 h-full bg-red-600"></div>
                        
                        <div class="flex justify-between items-start mb-4 border-b border-red-900/50 pb-4">
                            <div>
                                <span class="text-xs bg-red-900 text-white px-2 py-1 rounded font-mono mb-2 inline-block">DW-001</span>
                                <h3 class="text-xl font-bold text-white">【指定劇薬】仮死後致死カプセル</h3>
                                <p class="text-sm text-gray-400 mt-1">数量: 1</p>
                            </div>
                            <div class="text-xl font-mono text-red-500 font-bold">¥1,500,000</div>
                        </div>

                        <div class="mt-6 bg-black/50 p-4 rounded border border-gray-800">
                            <p class="text-red-500 font-bold mb-2 flex items-center gap-2">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" /></svg>
                                売人からのメッセージ (自動消去対象)
                            </p>
                            <p class="text-sm leading-relaxed mb-4">
                                「例の件、手配は完了した。手違いで死なせたくないなら、<span class="text-red-400 font-bold underline">仮死状態から2時間以内</span>に以下の手順で解毒剤を作って飲ませろ。材料はそっちで用意しろよ。」
                            </p>
                            
                            <div class="font-mono text-xs text-gray-400 bg-gray-900 p-3 rounded border border-gray-700 whitespace-pre-wrap">【緊急解毒薬（リヴァイブ・ドロップ）調合手順】
1. 純水 50ml に「アズライト結晶の粉末」を2g溶かす。
2. 液体が青く変色したら、「合成ペプチドX-9」を3滴垂らし、激しく撹拌する。
3. 最後に塩化ナトリウムを少々加え、対象の舌下（ぜっか）に投与しろ。

※警告: 2時間を過ぎると心筋が完全に壊死し、蘇生は不可能になる。健闘を祈る。</div>
                        </div>
                        
                        <div class="mt-6 flex justify-between items-center">
                            <span class="text-gray-500 text-sm">合計:</span>
                            <span class="text-2xl font-bold text-red-500 font-mono">¥1,500,000</span>
                        </div>
                    </div>
                    
                    <button onclick="showToast('送金アドレスを生成しています...')" class="w-full mt-6 bg-red-900 hover:bg-red-700 text-white font-bold py-3 rounded uppercase tracking-widest transition shadow-[0_0_15px_rgba(220,38,38,0.4)]">暗号資産で決済する</button>
                `;
            }
            
            document.getElementById('modal-overlay').classList.remove('hidden');
            document.getElementById('cart-modal').classList.remove('hidden');
        }

        // エンターキーでの入力サポート
        document.getElementById('promo-code').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkCode();
            }
        });

        // 初期描画
        renderProducts(normalProducts, false);
    </script>
</body>
</html>
