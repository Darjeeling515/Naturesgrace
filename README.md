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

        // 表のサプリメント
