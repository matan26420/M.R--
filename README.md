<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>כרטיס ביקור וביקורות</title>

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
        
        /* אזור כרטיס הביקור והלוגו בחלק העליון */
        .top-brand-bar {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 25px;
            margin-bottom: 30px;
        }

        /* כרטיס הביקור מוגדל משמעותית לקריאות מקסימלית */
        .business-card-section {
            background: #ffffff;
            border: 3px solid #007bff;
            padding: 25px;
            border-radius: 16px;
            width: 100%;
            box-sizing: border-box;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }
        
        .brand-character-img {
            width: 100%;
            max-width: 400px;
            height: auto;
            border-radius: 12px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* הלוגו מוגדל ללא מסגרת כחולה */
        .brand-logo-img {
            width: 220px;
            height: 220px;
            border-radius: 50%;
            object-fit: cover;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
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

        /* חתימה מוגדלת וברורה בצד */
        .signature-container {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background: #f9f9f9;
            padding: 10px 20px;
            border-radius: 8px;
            border: 1px solid #eee;
        }
        
        .signature-inline-img {
            height: 60px;
            width: auto;
            object-fit: contain;
        }

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
        <!-- חלק עליון - לוגו וכרטיס ביקור -->
        <div class="top-brand-bar">
            <img class="brand-logo-img" src="https://via.placeholder.com/220" alt="לוגו העסק">
            
            <div class="business-card-section">
                <img class="brand-character-img" src="https://via.placeholder.com/400x250" alt="כרטיס ביקור">
            </div>
        </div>

        <h1>שם העסק / המותג שלך</h1>
        <p>תיאור קצר ומנצח על השירותים והאיכות שאתה מציע ללקוחות שלך.</p>

        <!-- רשתות חברתיות -->
        <div class="social-links">
            <div class="social-btns-row">
                <a href="#" class="social-btn whatsapp-btn" target="_blank">וואטסאפ</a>
                <a href="#" class="social-btn instagram-btn" target="_blank">אינסטגרם</a>
                <a href="#" class="social-btn tiktok-btn" target="_blank">טיקטוק</a>
            </div>
        </div>

        <!-- שירותים -->
        <h2>השירותים שלנו</h2>
        <div class="services-grid">
            <a href="#" class="btn">שירות 1</a>
            <a href="#" class="btn">שירות 2</a>
            <a href="#" class="btn">שירות 3</a>
            <a href="#" class="btn">שירות 4</a>
        </div>

        <!-- סקציית ביקורות ותגובות -->
        <div class="reviews-section">
            <h2>הוסף חוות דעת</h2>
            <form id="reviewForm">
                <div class="form-group">
                    <label for="authorName">שם מלא:</label>
                    <input type="text" id="authorName" required placeholder="הכנס את שמך">
                </div>

                <div class="form-group">
                    <label for="serviceType">סוג השירות:</label>
                    <select id="serviceType">
                        <option value="כללי">שירות כללי</option>
                        <option value="ייעוץ">ייעוץ</option>
                        <option value="טיפול">טיפול / עבודה</option>
                    </select>
                </div>

                <div class="form-group">
                    <label>דירוג:</label>
                    <div class="stars-container" id="starsContainer">
                        <span class="star" data-rating="5">★</span>
                        <span class="star" data-rating="4">★</span>
                        <span class="star" data-rating="3">★</span>
                        <span class="star" data-rating="2">★</span>
                        <span class="star" data-rating="1">★</span>
                    </div>
                </div>

                <div class="form-group">
                    <label for="reviewText">חוות הדעת שלך:</label>
                    <textarea id="reviewText" rows="4" required placeholder="ספר לנו על החוויה שלך..."></textarea>
                </div>

                <button type="submit" class="btn" style="width: 100%; cursor: pointer;">שלח חוות דעת</button>
            </form>

            <!-- רשימת תגובות -->
            <div class="reviews-list" id="reviewsList">
                <h3>חוות דעת של לקוחות</h3>
                <!-- הביקורות יופיעו כאן -->
            </div>
        </div>

        <!-- חתימה -->
        <div class="signature-container" style="margin-top: 25px;">
            <span>בברכה,</span>
            <img src="https://via.placeholder.com/150x60?text=Signature" alt="חתימה" class="signature-inline-img">
        </div>

        <footer>
            <p>© כל הזכויות שמורות לעסק שלך</p>
        </footer>
    </div>

    <script>
        // ניהול מערכת הדירוג בכוכבים
        let selectedRating = 5;
        const stars = document.querySelectorAll('.star');

        function updateStars(rating) {
            stars.forEach(star => {
                const starVal = parseInt(star.getAttribute('data-rating'));
                if (starVal <= rating) {
                    star.classList.add('active');
                } else {
                    star.classList.remove('active');
                }
            });
        }

        stars.forEach(star => {
            star.addEventListener('click', function() {
                selectedRating = parseInt(this.getAttribute('data-rating'));
                updateStars(selectedRating);
            });
        });

        // ברירת מחדל 5 כוכבים
        updateStars(5);

        // טעינה והצגה של תגובות (אחסון מקומי localStorage)
        const reviewForm = document.getElementById('reviewForm');
        const reviewsList = document.getElementById('reviewsList');

        function loadReviews() {
            const reviews = JSON.parse(localStorage.getItem('user_reviews') || '[]');
            const listHtml = reviews.map(r => `
                <div class="review-card">
                    <div class="review-header">
                        <span>${escapeHtml(r.name)} (${escapeHtml(r.service)})</span>
                        <span style="color: #ffc107;">${'★'.repeat(r.rating)}</span>
                    </div>
                    <p style="margin: 5px 0 0 0; color: #555;">${escapeHtml(r.text)}</p>
                </div>
            `).join('');
            
            reviewsList.innerHTML = '<h3>חוות דעת של לקוחות</h3>' + (listHtml || '<p style="color:#777;">עדיין אין חוות דעת. היה הראשון לדרג!</p>');
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        reviewForm.addEventListener('submit', function(e) {
            e.preventDefault();
            const name = document.getElementById('authorName').value;
            const service = document.getElementById('serviceType').value;
            const text = document.getElementById('reviewText').value;

            const newReview = { name, service, text, rating: selectedRating, date: new Date().toISOString() };
            
            const reviews = JSON.parse(localStorage.getItem('user_reviews') || '[]');
            reviews.unshift(newReview);
            localStorage.setItem('user_reviews', JSON.stringify(reviews));

            reviewForm.reset();
            selectedRating = 5;
            updateStars(5);
            loadReviews();
        });

        loadReviews();
    </script>
</body>
</html>
