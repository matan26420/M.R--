<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>עמוד עסק וביקורות</title>

    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
        }
        .container {
            max-width: 650px;
            margin: 0 auto;
            background: #fff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        
        /* ראש העמוד - לוגו וחתימה (הכי למעלה) */
        .top-brand-bar {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        .brand-logo-img {
            width: 110px;
            height: 110px;
            border-radius: 50%;
            object-fit: cover;
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
            border: 3px solid #007bff;
        }
        .signature-top-img {
            max-width: 180px;
            height: auto;
        }

        /* מתחת ללוגו - כרטיס ביקור עם הדמות */
        .business-card-section {
            background: #fafafa;
            border: 2px solid #007bff;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .brand-character-img {
            width: 110px;
            height: 110px;
            border-radius: 50%;
            object-fit: cover;
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
            border: 3px solid #007bff;
        }
        
        h1 { margin: 10px 0 5px 0; color: #222; }
        h2 { color: #007bff; margin-top: 25px; }

        .services-grid, .moves-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }
        a.btn {
            display: block;
            background: #007bff;
            color: white;
            padding: 12px;
            text-decoration: none;
            border-radius: 6px;
            font-weight: bold;
            transition: background 0.3s;
        }
        a.btn:hover { background: #0056b3; }

        /* אזור קישורים רשתות חברתיות */
        .social-links {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        .social-btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 10px 18px;
            border-radius: 6px;
            color: white;
            text-decoration: none;
            font-weight: bold;
            font-size: 14px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .instagram-btn { background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); }
        .tiktok-btn { background: #000000; }
        .whatsapp-btn { background: #25d366; }

        /* סקציית תגובות */
        .reviews-section {
            margin-top: 30px;
            background: #fafafa;
            border: 2px dashed #007bff;
            padding: 20px;
            border-radius: 8px;
            text-align: right;
        }
        .form-group {
            margin-bottom: 15px;
            text-align: right;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .stars-container {
            display: flex;
            flex-direction: row-reverse;
            justify-content: flex-end;
            gap: 5px;
            font-size: 32px;
        }
        .star {
            color: #ddd;
            cursor: pointer;
            transition: color 0.2s;
        }
        .star.active { color: #ffc107; }

        .reviews-list {
            margin-top: 20px;
            border-top: 1px solid #ddd;
            padding-top: 15px;
        }
        .review-card {
            background: #fff;
            border: 1px solid #e1e1e1;
            padding: 12px 15px;
            border-radius: 6px;
            margin-bottom: 12px;
            text-align: right;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .review-header {
            display: flex;
            justify-content: space-between;
            font-weight: bold;
            font-size: 14px;
            color: #444;
            margin-bottom: 5px;
        }
        .review-image {
            max-width: 100%;
            max-height: 300px;
            border-radius: 6px;
            margin-top: 10px;
            display: block;
        }
        
        footer {
            margin-top: 30px;
            font-size: 13px;
            color: #777;
            border-top: 1px solid #eee;
            padding-top: 15px;
        }
    </style>
</head>
<body>

<div class="container">
    <!-- ראש העמוד - לוגו וחתימה -->
    <div class="top-brand-bar">
        <img src="1793908641410.jpg" alt="לוגו" class="brand-logo-img">
        <img src="IMG_20261021_205959.jpg" alt="חתימה" class="signature-top-img">
    </div>

    <!-- כרטיס ביקור עם הדמות -->
    <div class="business-card-section">
        <img src="1793908727293.jpg" alt="דמות מותג" class="brand-character-img">
        <div>
            <h1>שם העסק / דמות</h1>
            <p>תיאור קצר או מועדון חברים</p>
        </div>
    </div>

    <!-- רשתות חברתיות -->
    <div class="social-links">
        <a href="#" class="social-btn instagram-btn">אינסטגרם</a>
        <a href="#" class="social-btn tiktok-btn">טיקטוק</a>
        <a href="#" class="social-btn whatsapp-btn">וואטסאפ</a>
    </div>

    <!-- סקציית תגובות וביקורות -->
    <div class="reviews-section">
        <h2>הוסף ביקורת</h2>
        <div class="form-group">
            <label for="reviewer-name">שם מלא:</label>
            <input type="text" id="reviewer-name" placeholder="הכנס את שמך">
        </div>
        <div class="form-group">
            <label>דירוג:</label>
            <div class="stars-container">
                <span class="star">&#9733;</span>
                <span class="star">&#9733;</span>
                <span class="star">&#9733;</span>
                <span class="star">&#9733;</span>
                <span class="star">&#9733;</span>
            </div>
        </div>
        <div class="form-group">
            <label for="review-text">חוות דעת:</label>
            <textarea id="review-text" rows="3" placeholder="כתוב את חוות הדעת שלך..."></textarea>
        </div>
        <div class="form-group">
            <label for="review-file">העלאת תמונה:</label>
            <input type="file" id="review-file" accept="image/*">
        </div>

        <!-- רשימת ביקורות לדוגמה -->
        <div class="reviews-list">
            <div class="review-card">
                <div class="review-header">
                    <span>ישראל ישראלי</span>
                    <span>★★★★★</span>
                </div>
                <p>שירות מעולה וחוויה נהדרת!</p>
                <img src="1793908867065.jpg" alt="תמונת ביקורת" class="review-image">
            </div>
        </div>
    </div>

    <footer>
        <p>&copy; כל הזכויות שמורות</p>
    </footer>
</div>

</body>
</html>

