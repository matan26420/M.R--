<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.R – הכול לבית שלך!</title>
    
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
        
        /* ראש העמוד - דמות ולוגו */
        .brand-header {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .brand-character-img {
            width: 130px;
            height: 130px;
            border-radius: 50%;
            object-fit: cover;
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
            border: 3px solid #007bff;
        }
        .brand-logo-img {
            width: 130px;
            height: 130px;
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
        
        /* חתימה בסוף */
        .footer-signature {
            margin-top: 30px;
            text-align: center;
        }
        .signature-img {
            max-width: 220px;
            height: auto;
            margin-bottom: 10px;
        }
        footer {
            font-size: 13px;
            color: #777;
        }
    </style>
</head>
<body>

<div class="container">
    <!-- ראש העמוד עם הדמות והלוגו -->
    <div class="brand-header">
        <img src="14856.jpg" alt="M.R דמות" class="brand-character-img">
        <img src="14855.jpg" alt="M.R לוגו" class="brand-logo-img">
    </div>
    
    <h1>M.R – הכול לבית שלך!</h1>
    <p>שירות מקיף, מקצועי ומהיר בכל מקום בישראל</p>

    <!-- כפתורי תקשורת ורשתות חברתיות -->
    <div class="social-links">
        <a href="https://wa.me/972559423309" class="social-btn whatsapp-btn">💬 WhatsApp · 055-9423309</a>
        <a href="https://www.instagram.com/m.r26420" target="_blank" class="social-btn instagram-btn">📸 Instagram @m.r26420</a>
        <a href="https://www.tiktok.com/@m.r26420" target="_blank" class="social-btn tiktok-btn">🎵 TikTok @m.r26420</a>
    </div>

    <h2>בחרו שירות</h2>
    <div class="services-grid">
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20באינסטלציה">🚰 אינסטלציה</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בצבע">🎨 צבע</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בחידוש%20רהיטים">🛋️ חידוש רהיטים</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בניקיון">🧹 ניקיון</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בהריסות">🧱 הריסות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בשיפוצים">📐 שיפוצים</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בעבודות%20גבס">🪚 עבודות גבס</a>
    </div>

    <h2>🚚 הובלות</h2>
    <div class="moves-grid">
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בהובלות%20גדולות">🚛 הובלות גדולות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בהובלות%20קטנות">📦 הובלות קטנות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בהובלת%20רהיט%20אחד">🛋️ הובלת רהיט אחד</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%20אני%20מעוניין%20בהובלות%20משרדים">🏢 הובלות משרדים</a>
    </div>

    <!-- אזור תגובות -->
    <div class="reviews-section">
        <h2>⭐ תגובות לקוחות ודירוגים</h2>
        <h3>✍️ השאר תגובה ודרג אותנו:</h3>
        
        <form id="reviewForm">
            <div class="form-group">
                <label for="reviewerName">שם מלא:</label>
                <input type="text" id="reviewerName" required placeholder="הכנס את שמך">
            </div>

            <div class="form-group">
                <label for="reviewCategory">בחר קטגוריה:</label>
                <select id="reviewCategory" required>
                    <option value="">בחר שירות...</option>
                    <option value="אינסטלציה">אינסטלציה</option>
                    <option value="צבע">צבע</option>
                    <option value="חידוש רהיטים">חידוש רהיטים</option>
                    <option value="ניקיון">ניקיון</option>
                    <option value="הריסות">הריסות</option>
                    <option value="שיפוצים">שיפוצים</option>
                    <option value="עבודות גבס">עבודות גבס</option>
                    <option value="הובלות גדולות">הובלות גדולות</option>
                    <option value="הובלות קטנות">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים">הובלות משרדים</option>
                </select>
            </div>

            <div class="form-group">
                <label>דירוג כוכבים:</label>
                <div class="stars-container" id="starPicker">
                    <span class="star" data-value="5">★</span>
                    <span class="star" data-value="4.5">★</span>
                    <span class="star" data-value="4">★</span>
                    <span class="star" data-value="3.5">★</span>
                    <span class="star" data-value="3">★</span>
                    <span class="star" data-value="2.5">★</span>
                    <span class="star" data-value="2">★</span>
                    <span class="star" data-value="1.5">★</span>
                    <span class="star" data-value="1">★</span>
                    <span class="star" data-value="0.5">★</span>
                </div>
                <div style="margin-top: 5px; font-weight: bold; color: #007bff;" id="ratingText">דירוג נבחר: 5 מתוך 5 כוכבים</div>
                <input type="hidden" id="reviewRating" value="5" required>
            </div>

            <div class="form-group">
                <label for="reviewText">התגובה שלך:</label>
                <textarea id="reviewText" rows="3" required placeholder="כתוב כאן את חוות דעתך..."></textarea>
            </div>

            <button type="submit" class="btn" style="background: #28a745; width: 100%; border: none; cursor: pointer; font-size: 16px;">פרסם תגובה באתר ושלח לוואטסאפ 🚀</button>
        </form>

        <div style="margin-top: 35px;">
            <div class="filter-container" style="text-align: right; margin-bottom: 15px;">
                <label for="filterCategory" style="font-weight: bold; margin-left: 10px;">סנן תגובות לפי קטגוריה:</label>
                <select id="filterCategory" onchange="renderReviews()" style="width: 200px; padding: 5px;">
                    <option value="all">הצג הכל</option>
                    <option value="אינסטלציה">אינסטלציה</option>
                    <option value="צבע">צבע</option>
                    <option value="חידוש רהיטים">חידוש רהיטים</option>
                    <option value="ניקיון">ניקיון</option>
                    <option value="הריסות">הריסות</option>
                    <option value="שיפוצים">שיפוצים</option>
                    <option value="עבודות גבס">עבודות גבס</option>
                    <option value="הובלות גדולות">הובלות גדולות</option>
                    <option value="הובלות קטנות">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים">הובלות משרדים</option>
                </select>
            </div>

            <div class="reviews-list" id="reviewsList">
                <p style="color: #777;">טוען תגובות...</p>
            </div>
        </div>
    </div>

    <!-- חתימה מובנית בתחתית -->
    <div class="footer-signature">
        <img src="14351.jpg" alt="Matan Richter Signature" class="signature-img">
        <footer>Matan Richter © M.R הכול לבית</footer>
    </div>
</div>

<script>
    // הגדרות Firebase עם הכתובת המעודכנת
    const firebaseConfig = {
        databaseURL: "https://mr-services26-default-rtdb.firebaseio.com"
    };
    firebase.initializeApp(firebaseConfig);
    const database = firebase.database();
    const reviewsRef = database.ref('reviews');

    let allReviews = [];

    const reviewForm = document.getElementById('reviewForm');
    const reviewsList = document.getElementById('reviewsList');
    const filterCategory = document.getElementById('filterCategory');
    const reviewRatingInput = document.getElementById('reviewRating');
    const ratingText = document.getElementById('ratingText');
    const stars = document.querySelectorAll('#starPicker .star');

    // ניהול בחירת כוכבים
    stars.forEach(star => {
        star.addEventListener('click', function() {
            let val = parseFloat(this.getAttribute('data-value'));
            reviewRatingInput.value = val;
            ratingText.innerHTML = `דירוג נבחר: ${val} מתוך 5 כוכבים`;

            stars.forEach(s => {
                let sVal = parseFloat(s.getAttribute('data-value'));
                if (sVal <= val) {
                    s.classList.add('active');
                } else {
                    s.classList.remove('active');
                }
            });
        });
    });
    stars.forEach(s => s.classList.add('active'));

    function getStarsHTML(rating) {
        let fulls = Math.floor(rating);
        let hasHalf = (rating - fulls) >= 0.5;
        let str = '';
        for(let i=0; i<fulls; i++) str += '⭐';
        if(hasHalf) str += '✨';
        return `${str} (${rating}/5)`;
    }

    function renderReviews() {
        reviewsList.innerHTML = '';
        let selectedFilter = filterCategory.value;

        let filteredReviews = allReviews;
        if (selectedFilter !== 'all') {
            filteredReviews = allReviews.filter(r => r.category === selectedFilter);
        }

        if (filteredReviews.length === 0) {
            reviewsList.innerHTML = '<p style="color: #777; text-align: center; padding: 10px;">אין עדיין תגובות להצגה בקטגוריה זו.</p>';
            return;
        }

        filteredReviews.forEach(review => {
            let card = document.createElement('div');
            card.className = 'review-card';
            card.innerHTML = `
                <div class="review-header">
                    <span>👤 ${review.name} <span style="color: #007bff; font-weight: normal;">(${review.category})</span></span>
                    <span>${getStarsHTML(review.rating)}</span>
                </div>
                <p style="margin: 8px 0; color: #333; word-break: break-word;">${review.text}</p>
                <div style="font-size: 11px; color: #888; text-align: left;">📅 ${review.date}</div>
            `;
            reviewsList.appendChild(card);
        });
    }

    // טעינת תגובות בזמן אמת
    reviewsRef.on('value', (snapshot) => {
        const data = snapshot.val();
        allReviews = [];
        if (data) {
            Object.keys(data).forEach(key => {
                allReviews.unshift(data[key]);
            });
        }
        renderReviews();
    });

    // שליחת תגובה
    reviewForm.addEventListener('submit', function(e) {
        e.preventDefault();

        let name = document.getElementById('reviewerName').value.trim();
        let category = document.getElementById('reviewCategory').value;
        let rating = parseFloat(reviewRatingInput.value);
        let text = document.getElementById('reviewText').value.trim();
        let date = new Date().toLocaleDateString('he-IL');

        if (!name || !category || !text) {
            alert('אנא מלא את כל השדות בטופס.');
            return;
        }

        let newReview = { name, category, rating, text, date };

        // שמירה בענן
        reviewsRef.push(newReview);

        // איפוס הטופס
        reviewForm.reset();
        reviewRatingInput.value = '5';
        ratingText.innerHTML = 'דירוג נבחר: 5 מתוך 5 כוכבים';
        stars.forEach(s => s.classList.add('active'));
        filterCategory.value = 'all';

        // שליחה לוואטסאפ
        let whatsappMessage = `*💬 תגובה חדשה התקבלה באתר!*%0A%0A` +
                              `👤 *שם:* ${encodeURIComponent(name)}%0A` +
                              `🏷️ *קטגוריה:* ${encodeURIComponent(category)}%0A` +
                              `⭐ *דירוג:* ${rating} כוכבים%0A` +
                              `📝 *תוכן התגובה:* ${encodeURIComponent(text)}`;

        let whatsappUrl = `https://wa.me/972559423309?text=${whatsappMessage}`;
        window.open(whatsappUrl, '_blank');
    });
</script>

</body>
</html>
