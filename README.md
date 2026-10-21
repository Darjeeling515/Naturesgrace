<!DOCTYPE html>
<html lang="ja" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nature's Grace - サプリメント公式通販</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class', // htmlタグのclass="dark"で切り替え
            theme: {
                extend: {
                    colors: {
                        darkbg: '#050505',
                        darkcard: '#111111',
                    }
                }
            }
        }
    </script>
    <style>
        /* カスタムスクロールバー */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .dark ::-webkit-scrollbar-thumb { background: #3f3f46; }

        /* アニメーション */
        .fade-in { animation: fadeIn 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .glitch {
            position: relative;
            text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75), -0.025em 0.05em 0 rgba(0,0,255,0.75);
            animation: glitch 1s infinite;
        }
        @keyframes glitch {
            0% { text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75), -0.025em 0.05em 0 rgba(0,0,255,0.75); }
            14% { text-shadow: 0.05em 0 0 rgba(255,0,0,0.75), -0.05em -0.025em 0 rgba(0,255,0,0.75), -0.025em 0.05em 0 rgba(0,0,255,0.75); }
            15% { text-shadow: -0.05em -0.025em 0 rgba(255,0,0,0.75), 0.025em 0.025em 0 rgba(0,255,0,0.75), -0.05em -0.05em 0 rgba(0,0,255,0.75); }
            49% { text-shadow: -0.05em -0.025em 0 rgba(255,0,0,0.75), 0.025em 0.025em 0 rgba(0,255,0,0.75), -0.05em -0.05em 0 rgba(0,0,255,0.75); }
            50% { text-shadow: 0.025em 0.05em 0 rgba(255,0,0,0.75), 0.05em 0 0 rgba(0,255,0,0.75), 0 -0.05em 0 rgba(0,0,255,0.75); }
            99% { text-shadow: 0.025em 0.05em 0 rgba(255,0,0,0.75), 0.05em 0 0 rgba(0,255,0,0.75), 0 -0.05em 0 rgba(0,0,255,0.75); }
            100% { text-shadow: -0.025em 0 0 rgba(255,0,0,0.75), -0.025em -0.025em 0 rgba(0,255,0,0.75), -0.025em -0.05em 0 rgba(0,0,255,0.75); }
        }

        /* トースト通知 (alert代替) */
        #toast-container {
            position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%);
            display: flex; flex-direction: column; gap: 10px; z-index: 10000; pointer-events: none;
        }
        .toast {
            background-color: #1f2937; color: #f9fafb; padding: 12px 24px; border-radius: 8px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1); font-weight: 500; text-align: center;
            animation: toastEnter 0.3s ease-out, toastLeave 0.3s ease-in 2.7s forwards;
            pointer-events: auto;
        }
        .dark .toast { background-color: #7f1d1d; border: 1px solid #dc2626; box-shadow: 0 0 15px rgba(220, 38, 38, 0.3); }
        @keyframes toastEnter { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes toastLeave { from { opacity: 1; transform: translateY(0); } to { opacity: 0; transform: translateY(20px); } }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 font-sans transition-colors duration-1000 dark:bg-darkbg dark:text-gray-300 min-h-screen flex flex-col">

    <!-- トースト通知コンテナ -->
    <div id="toast-container"></div>

    <!-- モーダル群 (初期非表示) -->
    <div id="modal-overlay" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4 transition-opacity duration-300 opacity-0">
        
        <!-- 警告モーダル (裏サイト移行前) -->
        <div id="warning-modal" class="hidden bg-darkcard border border-red-800 text-center p-8 rounded-2xl max-w-lg w-full shadow-[0_0_40px_rgba(220,38,38,0.4)] transform transition-transform scale-95">
            <h2 class="text-4xl font-black text-red-600 mb-6 glitch tracking-widest">【警告】<br>認証コード受理</h2>
            <p class="text-gray-300 mb-8 leading-relaxed font-medium">
                これより先は一般法規の適用外となる<br>
                <span class="text-red-400">「非合法・特設カタログ」</span>となります。<br>
                閲覧および取引による一切の責任は負いかねます。
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center">
                <button onclick="closeModal()" class="px-6 py-3 border border-gray-600 text-gray-400 font-bold rounded-lg hover:bg-gray-800 hover:text-white transition w-full sm:w-auto">キャンセル</button>
                <button onclick="enterDarkWeb()" class="px-6 py-3 bg-red-900 hover:bg-red-700 text-white font-bold rounded-lg border border-red-500 transition shadow-[0_0_15px_rgba(220,38,38,0.6)] w-full sm:w-auto">承諾して入室</button>
            </div>
        </div>

        <!-- カートモーダル -->
        <div id="cart-modal" class="hidden bg-white dark:bg-darkcard dark:border-red-900/50 dark:border p-6 sm:p-8 rounded-2xl max-w-2xl w-full shadow-2xl relative max-h-[90vh] overflow-y-auto transform transition-transform scale-95">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-gray-400 hover:text-gray-800 dark:hover:text-white text-3xl font-light transition">&times;</button>
            <h2 id="cart-title" class="text-2xl font-bold mb-6 text-slate-800 dark:text-red-500 border-b pb-4 dark:border-red-900/50 flex items-center gap-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 0a2 2 0 100 4 2 2 0 000-4z" /></svg>
                <span>ショッピングカート</span>
            </h2>
            <div id="cart-content" class="min-h-[150px]">
                <!-- JSで動的書き換え -->
            </div>
            <div class="mt-8 text-center sm:text-right">
                <button onclick="closeModal()" class="w-full sm:w-auto px-8 py-3 bg-slate-200 text-slate-800 font-bold rounded-lg hover:bg-slate-300 dark:bg-gray-800 dark:text-gray-300 dark:hover:bg-gray-700 transition">閉じる</button>
            </div>
        </div>

    </div>

    <!-- ヘッダー -->
    <header class="bg-white dark:bg-[#080808] shadow-sm dark:shadow-red-900/10 sticky top-0 z-40 transition-colors duration-1000 border-b border-transparent dark:border-red-900/30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div>
                <h1 id="site-title" class="text-2xl sm:text-3xl font-black text-emerald-700 dark:text-red-600 transition-colors tracking-tight">Nature's Grace</h1>
                <p id="site-subtitle" class="text-xs sm:text-sm text-slate-500 dark:text-gray-500 font-medium tracking-wide">自然の力で、健やかな毎日を</p>
            </div>
            <div class="flex items-center gap-3 sm:gap-4">
                <!-- セーフモードに戻るボタン (裏でのみ表示) -->
                <button id="return-btn" onclick="returnToNormal()" class="hidden px-3 py-2 sm:px-4 sm:py-2 text-xs sm:text-sm font-bold border border-red-900/50 text-red-500 hover:bg-red-900/20 hover:text-red-400 rounded-lg transition flex items-center gap-1">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" /></svg>
                    <span class="hidden sm:inline">セーフモードに戻る</span>
                </button>
                <!-- カートボタン -->
                <button onclick="openCart()" class="flex items-center gap-2 bg-emerald-50 text-emerald-700 border border-emerald-100 px-4 py-2 rounded-lg font-bold hover:bg-emerald-100 transition shadow-sm dark:bg-black dark:text-red-500 dark:border-red-900 dark:hover:bg-red-900/30 dark:shadow-[0_0_10px_rgba(220,38,38,0.2)]">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 0a2 2 0 100 4 2 2 0 000-4z" /></svg>
                    <span class="hidden sm:inline">カート</span>
                </button>
            </div>
        </div>
    </header>

    <!-- メインコンテンツ -->
    <main class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 sm:py-12 w-full">
        
        <!-- プロモーション入力エリア (表でのみ表示) -->
        <div id="promo-section" class="mb-12 sm:mb-16 bg-gradient-to-br from-emerald-50 to-teal-50 rounded-2xl p-6 sm:p-10 shadow-sm border border-emerald-100 text-center relative overflow-hidden">
            <div class="absolute top-0 left-0 w-full h-1 bg-emerald-400"></div>
            <h2 class="text-xl sm:text-2xl font-bold text-emerald-800 mb-3 tracking-wide">★ VIP会員様限定 シークレットセール ★</h2>
            <p class="text-slate-600 mb-8 font-medium">招待状に記載されている専用プロモーションコードをご入力ください。</p>
            <div class="flex flex-col sm:flex-row justify-center items-center gap-3 max-w-md mx-auto">
                <input type="password" id="promo-code" placeholder="例: 1111" class="w-full sm:flex-1 px-4 py-3 rounded-lg border border-slate-300 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:border-transparent text-center tracking-[0.2em] text-lg shadow-inner font-mono transition">
                <button onclick="checkCode()" class="w-full sm:w-auto px-8 py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-lg transition shadow-md active:scale-95">適用</button>
            </div>
            <p id="error-msg" class="text-red-500 mt-4 font-bold text-sm hidden opacity-0 transition-opacity">※無効なプロモーションコードです</p>
        </div>

        <!-- ダークウェブ ヒーローエリア (裏でのみ表示) -->
        <div id="dark-hero" class="hidden mb-12 sm:mb-16 text-center border-b border-red-900/50 pb-10 pt-4">
            <h2 class="text-4xl sm:text-6xl font-black text-red-600 mb-4 glitch tracking-widest uppercase">Underground Market</h2>
            <p class="text-red-500/80 text-xs sm:text-sm tracking-[0.3em] font-mono uppercase bg-red-900/10 inline-block px-4 py-1 rounded border border-red-900/30">Encrypted Connection Secured</p>
        </div>

        <!-- 商品グリッド -->
        <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 sm:gap-8">
            <!-- JSで動的生成 -->
        </div>
    </main>

    <!-- フッター -->
    <footer class="bg-white dark:bg-[#030303] border-t border-slate-200 dark:border-red-900/30 py-8 text-center transition-colors">
        <p id="footer-text" class="text-slate-400 dark:text-red-900/50 text-sm font-medium tracking-wide">&copy; 2026 Nature's Grace. All rights reserved.</p>
    </footer>

    <!-- JavaScript ロジック -->
    <script>
        // --- 商品データ (16種 x 2) ---
        const normalProducts = [
            { id: "NG-01", name: "ピュアビタミンC 1000mg", desc: "レモン50個分のビタミンCを1粒に凝縮。透明感のある毎日に。", price: "¥1,800", icon: "🍋" },
            { id: "NG-02", name: "オーガニック・プロテイン", desc: "植物由来のタンパク質。人工甘味料不使用の自然な味わい。", price: "¥3,980", icon: "🌱" },
            { id: "NG-03", name: "DHA&EPA フィッシュオイル", desc: "青魚のサラサラ成分。考える力と健康診断の数値が気になる方に。", price: "¥2,400", icon: "🐟" },
            { id: "NG-04", name: "マルチビタミン＆ミネラル", desc: "22種類の必須栄養素をバランス良く配合したベースサプリ。", price: "¥2,100", icon: "💊" },
            { id: "NG-05", name: "プレミアムマカ＆亜鉛", desc: "エネルギッシュな毎日をサポート。男性にも女性にもおすすめ。", price: "¥2,800", icon: "⚡" },
            { id: "NG-06", name: "ヘム鉄プラス葉酸", desc: "吸収率の高いヘム鉄を採用。クラクラが気になる女性の味方。", price: "¥1,650", icon: "🩸" },
            { id: "NG-07", name: "カルシウム＆マグネシウム", desc: "理想のバランス2:1で配合。丈夫な骨と歯の形成を助けます。", price: "¥1,500", icon: "🦴" },
            { id: "NG-08", name: "ビタミンB群コンプレックス", desc: "エネルギー生成を助ける8種類のビタミンB群を網羅。", price: "¥1,200", icon: "✨" },
            { id: "NG-09", name: "快眠サポート メラトニン", desc: "深い休息をサポートし、すっきりとした朝の目覚めへ。", price: "¥2,900", icon: "🌙" },
            { id: "NG-10", name: "プロバイオティクス乳酸菌", desc: "奥まで届くカプセルで腸内フローラを整え、スッキリを実感。", price: "¥3,200", icon: "🦠" },
            { id: "NG-11", name: "低分子コラーゲンペプチド", desc: "吸収力にこだわったコラーゲン。ぷるんとしたハリとうるおいを。", price: "¥3,500", icon: "💧" },
            { id: "NG-12", name: "ビルベリーEX＆ルテイン", desc: "PCやスマホをよく使う方に。クリアでピントの合った視界を。", price: "¥2,600", icon: "👁️" },
            { id: "NG-13", name: "ヒアルロン酸モイスチャー", desc: "内側から潤いをキープする美容サプリ。乾燥しがちな季節に。", price: "¥2,200", icon: "💦" },
            { id: "NG-14", name: "高麗人参エキストラクト", desc: "古来から伝わる滋養強壮成分を独自の製法で高濃度に凝縮。", price: "¥4,500", icon: "🌿" },
            { id: "NG-15", name: "グルコサミン＆コンドロイチン", desc: "階段の上り下りやスムーズな歩みをサポートする軟骨成分。", price: "¥3,100", icon: "🏃" },
            { id: "NG-16", name: "食物繊維イヌリンパウダー", desc: "毎日のスッキリをサポートする水溶性食物繊維。無味無臭。", price: "¥1,400", icon: "🌾" }
        ];

        const darkProducts = [
            { id: "DW-RX01", name: "【指定劇薬】仮死後致死カプセル", desc: "服用後すぐに心停止し「仮死状態」に陥る。その後多臓器不全で確実に死亡する。※カート追加済", price: "¥1,500,000", icon: "💀" },
            { id: "DW-RX02", name: "忘却の滴（記憶消去剤）", desc: "飲料に数滴混ぜるだけで、直近24時間の記憶を不可逆的に完全に消去する無色無臭の液体。", price: "¥850,000", icon: "🧠" },
            { id: "DW-RX03", name: "狂気の粉（幻覚誘発剤）", desc: "対象に極度のパラノイアと悪夢のような幻覚を72時間継続して引き起こす。精神崩壊リスク高。", price: "¥420,000", icon: "👁️‍🗨️" },
            { id: "DW-RX04", name: "暴走ステロイド【リミットブレイク】", desc: "筋力を一時的に通常の5倍に引き上げるが、効果終了後に全身の筋繊維がズタズタに崩壊する。", price: "¥600,000", icon: "💉" },
            { id: "DW-RX05", name: "マインドハック・シリンジ", desc: "注射された対象の自我と自由意志を奪い、術者の命令に絶対服従する状態にする薬液。", price: "¥2,800,000", icon: "🔗" },
            { id: "DW-RX06", name: "ペインキラー・ゼロ", desc: "痛覚神経を完全に焼き切る。致死量の出血や骨折などの致命傷を負っても一切の痛みを感じなくなる。", price: "¥300,000", icon: "⚡" },
            { id: "DW-RX07", name: "不眠不休剤（デスマーチ）", desc: "14日間、一睡もせず極度の集中力を保ったまま活動可能になるが、効果終了時に脳血管が破裂する。", price: "¥550,000", icon: "⏱️" },
            { id: "DW-RX08", name: "感情凍結シロップ", desc: "脳の扁桃体を麻痺させ、一切の喜怒哀楽、共感能力、恐怖心を完全に失わせる。", price: "¥700,000", icon: "🧊" },
            { id: "DW-RX09", name: "クロノス・エリクサー", desc: "自身の寿命を10年削り落とす代わりに、細胞分裂を暴走させ一時的に肉体を全盛期まで若返らせる。", price: "¥3,500,000", icon: "⏳" },
            { id: "DW-RX10", name: "ブラッドボイル・パウダー", desc: "吸引させた対象の血圧を数秒で異常上昇させ、自然死に見せかけた脳溢血を引き起こす。", price: "¥1,200,000", icon: "🩸" },
            { id: "DW-RX11", name: "虚無堕ちのタブレット", desc: "服用者の精神構造を根底から破壊し、一切の反応を示さない生ける屍（廃人）へと変貌させる。", price: "¥1,800,000", icon: "⬛" },
            { id: "DW-RX12", name: "即効性細胞融解液", desc: "皮膚に一滴触れた瞬間から組織の融解が始まり、跡形もなくドロドロに溶かす極秘の劇薬。", price: "¥2,500,000", icon: "🧪" },
            { id: "DW-RX13", name: "真実の吐息（自白剤・改）", desc: "脳の嘘をつく機能を物理的に麻痺させ、質問に対して全て真実を強制的に喋らせるガス。", price: "¥900,000", icon: "🗣️" },
            { id: "DW-RX14", name: "サイレント・パルス", desc: "服用後、声帯の神経を一時的に完全に麻痺させ、48時間一切の声を奪う錠剤。", price: "¥250,000", icon: "🔇" },
            { id: "DW-RX15", name: "腐敗促進ガス弾", desc: "密閉空間で使用すると、有機物の腐敗速度を通常の1000倍に加速させる特殊兵器。", price: "¥4,000,000", icon: "☣️" },
            { id: "DW-RX16", name: "ドッペルゲンガー・エキス", desc: "顔の骨格と筋肉を一時的に軟化させ、他者の顔を物理的に模倣しやすくする変装専用薬。", price: "¥5,500,000", icon: "🎭" }
        ];

        let isDarkMode = false;

        // --- コア機能 ---

        // トースト通知の表示 (alertの代わり)
        function showToast(message) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.textContent = message;
            container.appendChild(toast);
            setTimeout(() => {
                if(toast.parentElement) toast.parentElement.removeChild(toast);
            }, 3000);
        }

        // 商品のレンダリング
        function renderProducts(products, dark) {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = '';
            
            products.forEach((p, index) => {
                const delay = index * 30; // アニメーションの時差
                
                if (!dark) {
                    grid.innerHTML += `
                        <div class="bg-white rounded-xl p-6 shadow-sm hover:shadow-xl transition-all duration-300 border border-slate-100 flex flex-col h-full fade-in group" style="animation-delay: ${delay}ms; opacity: 0;">
                            <div class="text-4xl text-center mb-4 bg-emerald-50 w-16 h-16 mx-auto rounded-full flex items-center justify-center group-hover:scale-110 transition-transform">${p.icon}</div>
                            <div class="text-xs text-slate-400 font-mono mb-2 bg-slate-50 inline-block px-2 py-1 rounded">品番: ${p.id}</div>
                            <h3 class="text-lg font-bold text-slate-800 mb-2 leading-tight">${p.name}</h3>
                            <p class="text-sm text-slate-600 flex-grow mb-4 leading-relaxed">${p.desc}</p>
                            <div class="text-xl font-black text-emerald-600 mb-4">${p.price}</div>
                            <button onclick="showToast('「${p.name}」をカートに追加しました')" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-bold py-2.5 px-4 rounded-lg transition-colors mt-auto active:scale-95 shadow-md">カートに入れる</button>
                        </div>
                    `;
                } else {
                    grid.innerHTML += `
                        <div class="bg-darkcard rounded-lg p-6 shadow-[0_4px_20px_rgba(0,0,0,0.8)] hover:shadow-[0_4px_25px_rgba(220,38,38,0.25)] transition-all duration-300 border border-red-900/30 flex flex-col h-full fade-in relative overflow-hidden group" style="animation-delay: ${delay}ms; opacity: 0;">
                            <div class="absolute top-0 right-0 bg-red-900/80 text-white text-[9px] px-2 py-1 font-mono rounded-bl-lg tracking-wider">CLASSIFIED</div>
                            <div class="text-3xl mb-4 grayscale opacity-70 group-hover:grayscale-0 group-hover:opacity-100 transition-all group-hover:scale-110 origin-left">${p.icon}</div>
                            <div class="text-xs text-red-500/70 font-mono mb-1 tracking-widest">ID: ${p.id}</div>
                            <h3 class="text-lg font-bold text-gray-200 mb-2 leading-tight group-hover:text-red-400 transition-colors">${p.name}</h3>
                            <p class="text-sm text-gray-400 flex-grow mb-4 border-l-2 border-red-900/50 pl-3 leading-relaxed">${p.desc}</p>
                            <div class="text-xl font-bold text-red-600 mb-4 font-mono tracking-wider">${p.price}</div>
                            <button onclick="showToast('承認待機中... 取引ログは暗号化されます。')" class="w-full bg-transparent hover:bg-red-900/30 text-red-500 hover:text-red-300 font-bold py-2 px-4 rounded border border-red-800/50 transition-colors mt-auto uppercase tracking-widest text-sm active:scale-95">取扱申請</button>
                        </div>
                    `;
                }
            });
        }

        // モーダル操作
        function openModal(id) {
            const overlay = document.getElementById('modal-overlay');
            const target = document.getElementById(id);
            
            // 全モーダルを一旦隠す
            document.querySelectorAll('#modal-overlay > div').forEach(el => {
                el.classList.add('hidden');
                el.classList.remove('scale-100');
                el.classList.add('scale-95');
            });
            
            overlay.classList.remove('hidden');
            target.classList.remove('hidden');
            
            // アニメーション用
            requestAnimationFrame(() => {
                overlay.classList.add('opacity-100');
                target.classList.remove('scale-95');
                target.classList.add('scale-100');
            });
        }

        function closeModal() {
            const overlay = document.getElementById('modal-overlay');
            overlay.classList.remove('opacity-100');
            
            document.querySelectorAll('#modal-overlay > div').forEach(el => {
                el.classList.remove('scale-100');
                el.classList.add('scale-95');
            });

            setTimeout(() => {
                overlay.classList.add('hidden');
                document.querySelectorAll('#modal-overlay > div').forEach(el => el.classList.add('hidden'));
            }, 300); // transition durationと合わせる
        }

        // パスワード判定 (0729)
        function checkCode() {
            const code = document.getElementById('promo-code').value;
            const errorMsg = document.getElementById('error-msg');
            
            if (code === "0729") {
                errorMsg.classList.add('hidden');
                errorMsg.classList.remove('opacity-100');
                document.getElementById('promo-code').value = '';
                openModal('warning-modal');
            } else {
                errorMsg.classList.remove('hidden');
                void errorMsg.offsetWidth; // reflow
                errorMsg.classList.add('opacity-100');
                if(code !== "") showToast('無効なプロモーションコードです');
            }
        }

        // エンターキー対応
        document.getElementById('promo-code').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') checkCode();
        });

        // 状態遷移：裏サイトへ
        function enterDarkWeb() {
            closeModal();
            isDarkMode = true;
            document.documentElement.classList.add('dark');
            
            // UIトグル
            document.getElementById('promo-section').classList.add('hidden');
            document.getElementById('dark-hero').classList.remove('hidden');
            document.getElementById('return-btn').classList.remove('hidden');
            document.getElementById('return-btn').classList.add('flex');
            
            // テキスト変更
            document.getElementById('site-title').innerText = "Underground Pharmacy";
            document.getElementById('site-subtitle').innerText = "CONNECTION SECURED. NO TRACES.";
            document.getElementById('footer-text').innerHTML = "ENCRYPTED CONNECTION <span class='text-red-600 font-bold glitch'>SECURE</span>";
            
            renderProducts(darkProducts, true);
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // 状態遷移：表サイトへ戻る
        function returnToNormal() {
            isDarkMode = false;
            document.documentElement.classList.remove('dark');
            
            // UIトグル
            document.getElementById('promo-section').classList.remove('hidden');
            document.getElementById('dark-hero').classList.add('hidden');
            document.getElementById('return-btn').classList.add('hidden');
            document.getElementById('return-btn').classList.remove('flex');
            
            // テキスト復元
            document.getElementById('site-title').innerText = "Nature's Grace";
            document.getElementById('site-subtitle').innerText = "自然の力で、健やかな毎日を";
            document.getElementById('footer-text').innerText = "© 2026 Nature's Grace. All rights reserved.";
            
            renderProducts(normalProducts, false);
            window.scrollTo({ top: 0, behavior: 'smooth' });
            showToast("安全な接続に切り替わりました");
        }

        // カート機能（ギミック中核）
        function openCart() {
            const content = document.getElementById('cart-content');
            const title = document.getElementById('cart-title');
            
            if (!isDarkMode) {
                // 表：空のカート
                title.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-emerald-600" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 0a2 2 0 100 4 2 2 0 000-4z" /></svg>
                    <span>ショッピングカート</span>
                `;
                content.innerHTML = `
                    <div class="text-center py-16 text-slate-500">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-16 w-16 mx-auto mb-4 text-slate-300" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
                        <p class="font-medium text-lg">現在カートには何も入っていません。</p>
                        <p class="text-sm mt-2 text-slate-400">お買い物をお楽しみください。</p>
                    </div>
                `;
            } else {
                // 裏：劇薬と解毒レシピ入り（2時間制限）
                title.innerHTML = `<span class='glitch text-red-600 tracking-widest'>ENCRYPTED CART DATA</span>`;
                content.innerHTML = `
                    <div class="bg-[#1a0505] border border-red-900/50 p-4 sm:p-6 rounded-xl text-gray-300 relative overflow-hidden shadow-inner">
                        <div class="absolute top-0 left-0 w-1.5 h-full bg-red-600"></div>
                        
                        <div class="flex flex-col sm:flex-row justify-between items-start mb-6 border-b border-red-900/40 pb-5 gap-4">
                            <div>
                                <span class="text-[10px] bg-red-900/80 text-white px-2 py-1 rounded font-mono mb-2 inline-block tracking-widest">FORCE ADDED: DW-RX01</span>
                                <h3 class="text-lg sm:text-xl font-bold text-white leading-tight">【指定劇薬】仮死後致死カプセル</h3>
                                <p class="text-sm text-red-400 mt-2 font-medium">数量: 1</p>
                            </div>
                            <div class="text-xl sm:text-2xl font-mono text-red-500 font-bold tracking-wider">¥1,500,000</div>
                        </div>

                        <div class="mt-4 bg-black/60 p-4 sm:p-5 rounded-lg border border-red-900/30 shadow-md">
                            <p class="text-red-500 font-bold mb-3 flex items-center gap-2 text-sm sm:text-base border-b border-red-900/30 pb-2">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" /></svg>
                                売人からのメッセージ (自動消去対象)
                            </p>
                            <p class="text-sm leading-relaxed mb-4 text-gray-300">
                                「例の件、手配は完了した。手違いで死なせたくないなら、<span class="text-red-400 font-bold border-b border-red-400">仮死状態から2時間以内</span>に以下の手順で解毒剤を作って飲ませろ。材料はそっちで用意しろよ。」
                            </p>
                            
                            <div class="font-mono text-xs sm:text-sm text-emerald-400/80 bg-[#0a0a0a] p-4 rounded border border-gray-800 whitespace-pre-wrap leading-relaxed shadow-inner">【緊急解毒薬（リヴァイブ・ドロップ）調合手順】
1. 純水 50ml に「アズライト結晶の粉末」を2g溶かす。
2. 液体が青く変色したら、「合成ペプチドX-9」を3滴垂らし、激しく撹拌する。
3. 最後に塩化ナトリウムを少々加え、対象の舌下（ぜっか）に投与しろ。

<span class="text-red-500 font-bold">※警告: 2時間を過ぎると心筋が完全に壊死し、蘇生は不可能になる。健闘を祈る。</span></div>
                        </div>
                        
                        <div class="mt-6 flex justify-between items-center bg-black/40 p-4 rounded-lg">
                            <span class="text-gray-400 font-bold">合計決済額:</span>
                            <span class="text-2xl sm:text-3xl font-black text-red-600 font-mono tracking-widest">¥1,500,000</span>
                        </div>
                    </div>
                    
                    <button onclick="showToast('送金用アドレスを生成しています...')" class="w-full mt-6 bg-red-900 hover:bg-red-700 text-white font-bold py-4 rounded-lg uppercase tracking-[0.2em] transition-all shadow-[0_0_20px_rgba(220,38,38,0.3)] hover:shadow-[0_0_25px_rgba(220,38,38,0.5)] active:scale-95 border border-red-500">暗号資産で決済する</button>
                `;
            }
            openModal('cart-modal');
        }

        // 初期描画
        renderProducts(normalProducts, false);
    </script>
</body>
</html>
