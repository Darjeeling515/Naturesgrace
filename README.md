<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Health & Wellness - サプリメント公式通販</title>
    <style>
        /* 基本スタイル・変数定義 */
        :root {
            --primary-color: #2e7d32;
            --bg-color: #f5f5f5;
            --text-color: #333;
            --card-bg: #fff;
            --border-color: #e0e0e0;
            --accent-color: #e65100;
        }

        /* 暗転後（ダークモード）の変数 */
        body.dark-mode {
            --primary-color: #8b0000;
            --bg-color: #0a0a0a;
            --text-color: #e0e0e0;
            --card-bg: #1a1a1a;
            --border-color: #333;
            --accent-color: #ff1744;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN', Meiryo, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            transition: background-color 1.5s ease, color 1.5s ease;
        }

        /* ヘッダー */
        header {
            background-color: var(--primary-color);
            color: #fff;
            padding: 2rem 1rem;
            text-align: center;
            position: relative;
            transition: background-color 1.5s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .header-buttons {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
        }

        .btn-header {
            background: #fff;
            color: var(--primary-color);
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }

        body.dark-mode .btn-header.cart-btn {
            background: #000;
            color: red;
            border: 1px solid red;
        }

        /* 表に戻るボタン（初期は非表示） */
        #return-btn {
            display: none;
            background: #333;
            color: #fff;
            border: 1px solid #555;
        }
        body.dark-mode #return-btn {
            display: block;
        }

        .container { max-width: 1200px; margin: 0 auto; padding: 2rem 1rem; }

        /* VIPコード入力エリア */
        .vip-banner {
            background: linear-gradient(135deg, #fff3e0, #ffe0b2);
            border: 2px dashed var(--accent-color);
            border-radius: 8px;
            padding: 2rem;
            text-align: center;
            margin-bottom: 3rem;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            transition: opacity 1s ease;
        }
        body.dark-mode .vip-banner { display: none; }

        .vip-banner h2 { color: var(--accent-color); margin-bottom: 1rem; font-size: 1.5rem; }
        .vip-input-group { display: flex; justify-content: center; gap: 10px; margin-top: 1rem; flex-wrap: wrap; }
        .vip-input-group input { padding: 12px 20px; font-size: 1.2rem; border: 2px solid #ccc; border-radius: 4px; width: 300px; text-align: center; letter-spacing: 2px; }
        .vip-input-group button { padding: 12px 30px; font-size: 1.1rem; background-color: var(--accent-color); color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: bold; transition: background 0.3s; }
        .vip-input-group button:hover { background-color: #bf360c; }
        #error-msg { color: red; margin-top: 10px; font-weight: bold; display: none; }

        /* 商品グリッド */
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; }
        .card { background-color: var(--card-bg); border: 1px solid var(--border-color); border-radius: 8px; padding: 20px; text-align: center; transition: transform 0.3s, box-shadow 0.3s, background-color 1.5s, border-color 1.5s; display: flex; flex-direction: column; justify-content: space-between;}
        .card:hover { transform: translateY(-5px); box-shadow: 0 8px 15px rgba(0,0,0,0.1); }
        body.dark-mode .card:hover { box-shadow: 0 8px 20px rgba(255, 0, 0, 0.2); }

        .item-code { font-family: monospace; color: #888; font-size: 0.9rem; margin-bottom: 10px; display: inline-block; background: rgba(0,0,0,0.05); padding: 3px 8px; border-radius: 4px; }
        body.dark-mode .item-code { color: #ff5252; background: rgba(255,0,0,0.1); }

        .card h3 { font-size: 1.1rem; margin-bottom: 10px; min-height: 2.8rem; display: flex; align-items: center; justify-content: center; }
        .card p { font-size: 0.9rem; line-height: 1.5; margin-bottom: 15px; color: var(--text-color); flex-grow: 1;}
        .price { font-size: 1.3rem; font-weight: bold; color: var(--accent-color); margin-bottom: 15px; }

        .add-to-cart { width: 100%; padding: 10px; background-color: var(--primary-color); color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 1rem; transition: opacity 0.3s; }
        .add-to-cart:hover { opacity: 0.8; }

        /* モーダル共通スタイル */
        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.8); z-index: 1000; justify-content: center; align-items: center; padding: 10px; }
        .modal-content { background: var(--card-bg); padding: 30px; border-radius: 8px; max-width: 600px; width: 100%; border: 1px solid var(--border-color); max-height: 90vh; overflow-y: auto; }
        
        /* カート専用スタイル */
        .close-btn { margin-top: 20px; padding: 12px 20px; cursor: pointer; width: 100%; background: #333; color: white; border: none; border-radius: 4px; font-size: 1.1rem; }
        .dark-cart-warning { color: #ff5252; border: 1px solid #ff5252; padding: 20px; margin-top: 20px; background: rgba(255,0,0,0.05); text-align: left; border-radius: 4px; }
        .recipe { font-family: monospace; color: #ccc; margin-top: 15px; white-space: pre-wrap; font-size: 0.95rem; border-top: 1px dashed #555; padding-top: 15px; line-height: 1.6; }

        /* トースト通知 (alertの代わり) */
        #toast-container { position: fixed; bottom: 20px; right: 20px; z-index: 9999; display: flex; flex-direction: column; gap: 10px; }
        .toast { background: var(--primary-color); color: #fff; padding: 15px 25px; border-radius: 5px; box-shadow: 0 4px 12px rgba(0,0,0,0.15); animation: fadein 0.3s, fadeout 0.3s 2.7s forwards; opacity: 1; }
        body.dark-mode .toast { background: #8b0000; border: 1px solid red; }
        @keyframes fadein { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes fadeout { from { opacity: 1; } to { opacity: 0; display: none; } }

    </style>
</head>
<body>

    <!-- トースト通知用コンテナ -->
    <div id="toast-container"></div>

    <!-- 警告モーダル（裏ページ侵入時） -->
    <div class="modal-overlay" id="warning-modal" style="background: rgba(0,0,0,0.95); z-index: 9999;">
        <div style="text-align: center; color: red;">
            <h1 style="font-size: 2.5rem; margin-bottom: 20px; text-shadow: 0 0 10px red;">【警告】認証コードを受理</h1>
            <p style="font-size: 1.2rem; margin-bottom: 30px; line-height: 1.6;">
                これより先は、一般法規の適用外となる闇市場の販売カタログとなります。<br>
                閲覧および購入による一切の責任を当サイトは負いません。
            </p>
            <button onclick="acceptRisk()" style="background: transparent; color: red; border: 2px solid red; padding: 15px 40px; font-size: 1.2rem; cursor: pointer; transition: all 0.3s;" onmouseover="this.style.background='red'; this.style.color='black'" onmouseout="this.style.background='transparent'; this.style.color='red'">承諾して入室する</button>
        </div>
    </div>

    <!-- カートモーダル -->
    <div class="modal-overlay" id="cart-modal">
        <div class="modal-content" id="cart-content">
            <!-- JSで動的に書き換え -->
        </div>
    </div>

    <header>
        <div class="header-buttons">
            <button id="return-btn" class="btn-header" onclick="returnToNormal()">セーフモードに戻る</button>
            <button class="btn-header cart-btn" onclick="openCart()">🛒 カートを見る</button>
        </div>
        <h1 id="site-title">Health & Wellness公式ストア</h1>
        <p id="site-desc" style="margin-top: 10px;">自然の力で、あなたの健やかな毎日をサポートします</p>
    </header>

    <div class="container">
        <!-- VIPコード入力エリア -->
        <div class="vip-banner" id="vip-area">
            <h2>★ VIP会員様限定 シークレットセール ★</h2>
            <p>招待状に記載されている専用プロモーションコードをご入力ください。</p>
            <div class="vip-input-group">
                <input type="password" id="promo-code" placeholder="コードを入力 (例: 1111)">
                <button onclick="checkCode()">適用する</button>
            </div>
            <p id="error-msg">※無効なプロモーションコードです</p>
        </div>

        <!-- 商品リストが展開されるエリア -->
        <div class="grid" id="product-grid">
            <!-- JavaScriptで動的に生成 -->
        </div>
    </div>

    <script>
        let isDarkMode = false;

        // 表のサプリメントデータ（16種類）
        const normalProducts = [
            { code: "H&W-001", name: "ピュアビタミンC 1000mg", desc: "レモン50個分のビタミンCを1粒に凝縮。透明感のある毎日に。", price: "¥1,800" },
            { code: "H&W-002", name: "オーガニック・プロテイン", desc: "植物由来のタンパク質。人工甘味料不使用の自然な味わい。", price: "¥3,980" },
            { code: "H&W-003", name: "DHA&EPA フィッシュオイル", desc: "青魚のサラサラ成分。考える力と健康診断の数値が気になる方に。", price: "¥2,400" },
            { code: "H&W-004", name: "マルチビタミン＆ミネラル", desc: "22種類の必須栄養素をバランス良く配合したベースサプリ。", price: "¥2,100" },
            { code: "H&W-005", name: "プレミアムマカ＆亜鉛", desc: "エネルギッシュな毎日をサポート。男性にも女性にもおすすめ。", price: "¥2,800" },
            { code: "H&W-006", name: "ヘム鉄プラス葉酸", desc: "吸収率の高いヘム鉄を採用。クラクラが気になる女性の味方。", price: "¥1,650" },
            { code: "H&W-007", name: "カルシウム＆マグネシウム", desc: "理想のバランス2:1で配合。丈夫な骨と歯の形成を助けます。", price: "¥1,500" },
            { code: "H&W-008", name: "ビタミンB群コンプレックス", desc: "エネルギー生成を助ける8種類のビタミンB群を網羅。", price: "¥1,200" },
            { code: "H&W-009", name: "快眠サポート メラトニン", desc: "深い休息をサポートし、すっきりとした朝の目覚めへ。", price: "¥2,900" },
            { code: "H&W-010", name: "プロバイオティクス乳酸菌", desc: "奥まで届くカプセルで腸内フローラを整え、スッキリを実感。", price: "¥3,200" },
            { code: "H&W-011", name: "低分子コラーゲンペプチド", desc: "吸収力にこだわったコラーゲン。ぷるんとしたハリとうるおいを。", price: "¥3,500" },
            { code: "H&W-012", name: "ビルベリーEX＆ルテイン", desc: "PCやスマホをよく使う方に。クリアでピントの合った視界を。", price: "¥2,600" },
            { code: "H&W-013", name: "ヒアルロン酸モイスチャー", desc: "内側から潤いをキープする美容サプリ。乾燥しがちな季節に。", price: "¥2,200" },
            { code: "H&W-014", name: "高麗人参エキストラクト", desc: "古来から伝わる滋養強壮成分を独自の製法で高濃度に凝縮。", price: "¥4,500" },
            { code: "H&W-015", name: "グルコサミン＆コンドロイチン", desc: "階段の上り下りやスムーズな歩みをサポートする軟骨成分。", price: "¥3,100" },
            { code: "H&W-016", name: "食物繊維イヌリンパウダー", desc: "毎日のスッキリをサポートする水溶性食物繊維。無味無臭。", price: "¥1,400" }
        ];

        // 裏の怪しい薬データ（16種類）
        const darkProducts = [
            { code: "DW-RX-001", name: "【指定劇薬】仮死後致死カプセル", desc: "服用後すぐに心停止し「仮死状態」に陥る。その後多臓器不全で確実に死亡する。※現在カートに入っています", price: "¥1,500,000" },
            { code: "DW-RX-002", name: "忘却の滴（記憶消去剤）", desc: "飲料に数滴混ぜるだけで、直近24時間の記憶を不可逆的に完全に消去する無色無臭の液体。", price: "¥850,000" },
            { code: "DW-RX-003", name: "狂気の粉（幻覚誘発剤）", desc: "対象に極度のパラノイアと悪夢のような幻覚を72時間継続して引き起こす。精神崩壊リスク高。", price: "¥420,000" },
            { code: "DW-RX-004", name: "暴走ステロイド【リミットブレイク】", desc: "筋力を一時的に通常の5倍に引き上げるが、効果終了後に全身の筋繊維がズタズタに崩壊する。", price: "¥600,000" },
            { code: "DW-RX-005", name: "マインドハック・シリンジ", desc: "注射された対象の自我と自由意志を奪い、術者の命令に絶対服従する状態にする薬液。", price: "¥2,800,000" },
            { code: "DW-RX-006", name: "ペインキラー・ゼロ", desc: "痛覚神経を完全に焼き切る。致死量の出血や骨折などの致命傷を負っても一切の痛みを感じなくなる。", price: "¥300,000" },
            { code: "DW-RX-007", name: "不眠不休剤（デスマーチ）", desc: "14日間、一睡もせず極度の集中力を保ったまま活動可能になるが、効果終了時に脳血管が破裂する。", price: "¥550,000" },
            { code: "DW-RX-008", name: "感情凍結シロップ", desc: "脳の扁桃体を麻痺させ、一切の喜怒哀楽、共感能力、恐怖心を完全に失わせる。", price: "¥700,000" },
            { code: "DW-RX-009", name: "クロノス・エリクサー", desc: "自身の寿命を10年削り落とす代わりに、細胞分裂を暴走させ一時的に肉体を全盛期まで若返らせる。", price: "¥3,500,000" },
            { code: "DW-RX-010", name: "ブラッドボイル・パウダー", desc: "吸引させた対象の血圧を数秒で異常上昇させ、自然死に見せかけた脳溢血を引き起こす。", price: "¥1,200,000" },
            { code: "DW-RX-011", name: "虚無堕ちのタブレット", desc: "服用者の精神構造を根底から破壊し、一切の反応を示さない生ける屍（廃人）へと変貌させる。", price: "¥1,800,000" },
            { code: "DW-RX-012", name: "即効性細胞融解液", desc: "皮膚に一滴触れた瞬間から組織の融解が始まり、跡形もなくドロドロに溶かす極秘の劇薬。", price: "¥2,500,000" },
            { code: "DW-RX-013", name: "真実の吐息（自白剤・改）", desc: "脳の嘘をつく機能を物理的に麻痺させ、質問に対して全て真実を強制的に喋らせるガス。", price: "¥900,000" },
            { code: "DW-RX-014", name: "サイレント・パルス", desc: "服用後、声帯の神経を一時的に完全に麻痺させ、48時間一切の声を奪う錠剤。", price: "¥250,000" },
            { code: "DW-RX-015", name: "腐敗促進ガス弾", desc: "密閉空間で使用すると、有機物の腐敗速度を通常の1000倍に加速させる特殊兵器。", price: "¥4,000,000" },
            { code: "DW-RX-016", name: "ドッペルゲンガー・エキス", desc: "顔の骨格と筋肉を一時的に軟化させ、他者の顔を物理的に模倣しやすくする変装専用薬。", price: "¥5,500,000" }
        ];

        // トースト通知を表示する関数（alertの代替）
        function showToast(message) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.innerText = message;
            container.appendChild(toast);
            
            // アニメーション完了後に削除
            setTimeout(() => {
                if(toast.parentElement) toast.parentElement.removeChild(toast);
            }, 3000);
        }

        // 商品を描画する関数
        function renderProducts(products) {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = '';
            products.forEach(p => {
                const card = document.createElement('div');
                card.className = 'card';
                card.innerHTML = `
                    <div>
                        <span class="item-code">品番: ${p.code}</span>
                        <h3>${p.name}</h3>
                        <p>${p.desc}</p>
                    </div>
                    <div>
                        <div class="price">${p.price}</div>
                        <button class="add-to-cart" onclick="showToast('カートに追加しました')">カートに入れる</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // 初期表示（表のサプリメント）
        renderProducts(normalProducts);

        // パスワード判定（0729）
        function checkCode() {
            const code = document.getElementById('promo-code').value;
            const errorMsg = document.getElementById('error-msg');
            
            if (code === "0729") {
                errorMsg.style.display = 'none';
                document.getElementById('warning-modal').style.display = 'flex';
                document.getElementById('promo-code').value = ''; // 入力をクリア
            } else {
                errorMsg.style.display = 'block';
            }
        }

        // 警告モーダルを承諾して裏ページへ
        function acceptRisk() {
            document.getElementById('warning-modal').style.display = 'none';
            isDarkMode = true;
            document.body.classList.add('dark-mode');
            
            document.getElementById('site-title').innerText = "【闇市場】非合法薬物・劇薬取引所";
            document.getElementById('site-desc').innerText = "※取扱厳重注意：アクセスログおよび取引履歴は全て暗号化されます。";
            
            renderProducts(darkProducts);
        }

        // セーフモード（表）へ戻る
        function returnToNormal() {
            isDarkMode = false;
            document.body.classList.remove('dark-mode');
            
            document.getElementById('site-title').innerText = "Health & Wellness公式ストア";
            document.getElementById('site-desc').innerText = "自然の力で、あなたの健やかな毎日をサポートします";
            
            renderProducts(normalProducts);
            showToast('安全な接続に切り替わりました');
        }

        // カートの開閉処理
        function openCart() {
            const cartContent = document.getElementById('cart-content');
            
            if (!isDarkMode) {
                // 表モードのカート
                cartContent.innerHTML = `
                    <h2 style="margin-bottom: 20px; font-size: 1.5rem;">ショッピングカート</h2>
                    <p style="font-size: 1.1rem;">現在カートには何も入っていません。</p>
                    <button class="close-btn" onclick="closeCart()">閉じる</button>
                `;
            } else {
                // 裏モードのカート（タイムリミット2時間）
                cartContent.innerHTML = `
                    <h2 style="color: #ff5252; margin-bottom: 10px; font-size: 1.5rem;">現在のカート内容（暗号化済）</h2>
                    <div class="dark-cart-warning">
                        <strong>【強制追加アイテム】</strong><br>
                        品番: DW-RX-001<br>
                        品名: 【指定劇薬】仮死後致死カプセル x 1<br>
                        小計: ¥1,500,000<br><br>
                        <em>※売人からのメッセージ※</em><br>
                        「例の件、承知した。手違いで死なせたくないなら、仮死状態から<b>【2時間以内（120分）】</b>に以下の手順で解毒剤を作って飲ませろ。材料はそっちで用意しろよ。」
                        <div class="recipe">
【緊急解毒薬（リヴァイブ・ドロップ）の調合手順】
1. 純水 50ml に「アズライト結晶の粉末」を2g溶かす。
2. 液体が青く変色したら、「合成ペプチドX-9」を3滴垂らし、激しく撹拌する。
3. 最後に塩化ナトリウムを少々加え、対象の舌下（ぜっか）に投与しろ。

※タイムリミット（2時間）を過ぎると心筋が完全に壊死し、蘇生は不可能になる。健闘を祈る。
                        </div>
                    </div>
                    <button class="close-btn" onclick="closeCart()" style="background: #ff5252; color: #fff; font-weight: bold;">閉じて取引を続ける</button>
                `;
            }
            document.getElementById('cart-modal').style.display = 'flex';
        }

        function closeCart() {
            document.getElementById('cart-modal').style.display = 'none';
        }
    </script>
</body>
</html>
