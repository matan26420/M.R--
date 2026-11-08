<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>כרטיס ביקור דיגיטלי</title>
    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)), 
                        url('21215792-729b-4a30-ac73-18f9a904b58c.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
            min-height: 100vh;
        }

        .container {
            max-width: 650px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            backdrop-filter: blur(5px);
        }
        
        .top-brand-bar {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 25px;
            margin-bottom: 30px;
        }

        .business-card-section {
            background: #ffffff;
            padding: 10px;
            border-radius: 12px;
            width: 100%;
            max-width: 520px;
            box-sizing: border-box;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }
        .brand-character-img {
            width: 100%;
            height: auto;
            aspect-ratio: 1 / 1;
            object-fit: cover;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .brand-logo-img {
            width: 260px;
            height: 240px;
            border-radius: 50%;
            object-fit: cover;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        h1 { margin: 10px 0 5px 0; color: #222; font-size: 30px; font-weight: bold; }
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

        .social-links {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
            margin: 25px 0;
        }
        .social-btns-row {
            display: flex;
            justify-content: center;
            gap: 15px;
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

        .signature-container {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            background: #f9f9f9;
            padding: 15px 30px;
            border-radius: 12px;
            border: 1px solid #e0e0e0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            width: 100%;
            max-width: 450px;
            box-sizing: border-box;
            margin: 0 auto;
        }
        .signature-label {
            font-size: 18px;
            color: #333;
            font-weight: bold;
        }
        .signature-inline-img {
            max-height: 120px;
            width: auto;
            object-fit: contain;
        }

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
            gap: 8px;
            font-size: 34px;
            padding: 5px 0;
            unicode-bidi: bidi-override;
        }
        .star {
            color: #ddd;
            cursor: pointer;
            padding: 0 4px;
            display: inline-block;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            transition: color 0.1s ease, transform 0.1s ease;
        }
        .star.active { color: #ffc107; }
        .star:active { transform: scale(1.2); }

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
        <!-- אזור לוגו וכרטיס ביקור -->
        <div class="top-brand-bar">
            <img src="logo.jpg" alt="לוגו העסק" class="brand-logo-img">
            <h1>שם העסק / השירות</h1>
            <div class="business-card-section">
                <img src="character.jpg" alt="תמונת דמות / תדמית" class="brand-character-img">
            </div>
        </div>

        <!-- כפתורי שירותים -->
        <h2>השירותים שלנו</h2>
        <div class="services-grid">
            <a href="#service1" class="btn">שירות א'</a>
            <a href="#service2" class="btn">שירות ב'</a>
        </div>

        <!-- קישורים רשתות חברתיות -->
        <div class="social-links">
            <h2>עקבו אחרינו</h2>
            <div class="social-btns-row">
                <a href="https://instagram.com" target="_blank" class="social-btn instagram-btn">אינסטגרם</a>
                <a href="https://tiktok.com" target="_blank" class="social-btn tiktok-btn">טיקטוק</a>
                <a href="https://wa.me/972000000000" target="_blank" class="social-btn whatsapp-btn">וואטסאפ</a>
            </div>
        </div>

        <!-- חתימה -->
        <div class="signature-container">
            <span class="signature-label">בברכה, המנהל</span>
            <img src="signature.png" alt="חתימה" class="signature-inline-img">
        </div>

        <!-- סקציית תגובות ודירוגים -->
        <div class="reviews-section">
            <h2>לקוחות מספרים</h2>
            <form id="reviewForm">
                <div class="form-group">
                    <label for="reviewerName">השם שלך:</label>
                    <input type="text" id="reviewerName" required placeholder="הכנס את שמך המלא">
                </div>
                
                <div class="form-group">
                    <label>דירוג:</label>
                    <div class="stars-container" id="starRating">
                        <span class="star" data-value="5">★</span>
                        <span class="star" data-value="4">★</span>
                        <span class="star" data-value="3">★</span>
                        <span class="star" data-value="2">★</span>
                        <span class="star" data-value="1">★</span>
                    </div>
                </div>

                <div class="form-group">
                    <label for="reviewText">חוות דעת:</label>
                    <textarea id="reviewText" rows="3" required placeholder="איך היה השירות?"></textarea>
                </div>

                <button type="submit" class="btn" style="width:100%;">שליחת חוות דעת</button>
            </form>

            <div class="reviews-list" id="reviewsList">
                <!-- כאן יופיעו הביקורות הדינאמיות -->
            </div>
        </div>

        <footer>
            כל הזכויות שמורות &copy; 2026
        </footer>
    </div>

    <script>
        // ניהול בחירת הכוכבים
        let selectedRating = 5;
        const stars = document.querySelectorAll('.star');
        
        stars.forEach(star => {
            star.addEventListener('click', function() {
                selectedRating = this.getAttribute('data-value');
                stars.forEach(s => s.classList.remove('active'));
                this.classList.add('active');
                // סימון כל הכוכבים מימינו (בשל RTL)
                let current = this;
                while(current) {
                    current.classList.add('active');
                    current = current.nextElementSibling;
                }
            });
        });

        // טיפול בטופס (ניתן לחבר בהמשך ל-Firebase Realtime Database בהתאם לנתונים שלך)
        document.getElementById('reviewForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const name = document.getElementById('reviewerName').value;
            const text = document.getElementById('reviewText').value;

            const list = document.getElementById('reviewsList');
            const card = document.createElement('div');
            card.className = 'review-card';
            card.innerHTML = `
                <div class="review-header">
                    <span>${name}</span>
                    <span>${'★'.repeat(selectedRating)}${'☆'.repeat(5 - selectedRating)}</span>
                </div>
                <p>${text}</p>
            `;
            list.prepend(card);
            this.reset();
            selectedRating = 5;
            stars.forEach(s => s.classList.add('active'));
        });
    </script>
</body>
</html>
