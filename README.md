<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الموسوعة الإسلامية الشاملة للأذكار والأدعية</title>
    <link href="https://fonts.googleapis.com/css2?family=Amiri&family=Tajawal:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #f8fafc;
            --card-bg: #ffffff;
            --text-dark: #1e293b;
            --text-muted: #64748b;
            --border: #e2e8f0;
            --primary: #0f766e;
            --accent: #d97706;
            --btn-bg: #f1f5f9;
            --overlay: rgba(0,0,0,0.4);
        }

        [data-theme="dark"] {
            --bg: #0f172a;
            --card-bg: #1e293b;
            --text-dark: #f8fafc;
            --text-muted: #94a3b8;
            --border: #334155;
            --btn-bg: #334155;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Tajawal', sans-serif; transition: background-color 0.3s, border-color 0.3s, color 0.3s; }
        body { background-color: var(--bg); color: var(--text-dark); padding: 20px; max-width: 650px; margin: 0 auto; }
        
        header { text-align: center; padding: 30px 25px; background: linear-gradient(135deg, #064e3b, #0f766e); color: white; border-radius: 16px; margin-bottom: 20px; position: relative; }
        header h1 { font-family: 'Amiri', serif; font-size: 32px; margin-bottom: 5px; }
        
        .settings-btn { position: absolute; top: 15px; right: 15px; background: rgba(255,255,255,0.2); border: none; color: white; padding: 8px; border-radius: 50px; cursor: pointer; font-size: 18px; display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; }
        html[dir="ltr"] .settings-btn { right: auto; left: 15px; }

        .settings-modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: var(--overlay); z-index: 1000; align-items: center; justify-content: center; }
        .settings-content { background: var(--card-bg); padding: 25px; border-radius: 16px; width: 90%; max-width: 400px; border: 1px solid var(--border); box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .settings-content h3 { margin-bottom: 20px; border-bottom: 1px solid var(--border); padding-bottom: 10px; font-size: 20px; }
        .setting-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .setting-row span { font-weight: bold; }
        .setting-select { padding: 8px 12px; border-radius: 8px; border: 1px solid var(--border); background: var(--btn-bg); color: var(--text-dark); font-weight: bold; font-size: 14px; cursor: pointer; }
        .close-btn { width: 100%; padding: 12px; background: var(--primary); color: white; border: none; border-radius: 10px; font-weight: bold; cursor: pointer; font-size: 16px; margin-top: 10px; }

        .tabs { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 20px; }
        .tab-btn { flex: 1; min-width: 100px; padding: 12px 8px; border: none; background-color: var(--btn-bg); color: var(--text-dark); font-weight: bold; border-radius: 10px; cursor: pointer; font-size: 13px; text-align: center; }
        .tab-btn.active { background-color: var(--primary); color: white; }
        
        .dhikr-section { display: none; }
        .dhikr-section.active { display: block; }
        
        .card { background-color: var(--card-bg); border-radius: 14px; padding: 20px; margin-bottom: 15px; border: 1px solid var(--border); box-shadow: 0 2px 4px rgba(0,0,0,0.02); }
        .text { font-family: 'Amiri', serif; font-size: 23px; line-height: 1.7; margin-bottom: 12px; text-align: justify; color: var(--text-dark); }
        html[dir="ltr"] .text { font-family: 'Tajawal', sans-serif; font-size: 17px; text-align: left; }
        .source { font-size: 12px; color: var(--text-muted); border-top: 1px dashed var(--border); padding-top: 8px; margin-bottom: 12px; font-style: italic; }
        
        .counter-btn { width: 100%; padding: 12px; background-color: var(--btn-bg); border: 2px solid var(--border); color: var(--text-dark); font-weight: bold; border-radius: 10px; cursor: pointer; font-size: 15px; }
        .counter-btn.done { background-color: #d1fae5; border-color: #10b981; color: #065f46; }
        [data-theme="dark"] .counter-btn.done { background-color: #064e3b; color: #a7f3d0; }
    </style>
</head>
<body>

    <header>
        <button class="settings-btn" onclick="toggleSettings()">⚙️</button>
        <h1 id="mainTitle">حصن المسلم الشامل</h1>
        <p id="mainSub">الموسوعة الكاملة للأذكار والأدعية والاستغفار</p>
    </header>

    <div class="settings-modal" id="settingsModal">
        <div class="settings-content">
            <h3 id="settingsTitle">الإعدادات ⚙️</h3>
            <div class="setting-row">
                <span id="langLabel">اللغة</span>
                <select class="setting-select" id="langSelect" onchange="changeLanguage()">
                    <option value="ar">العربية</option>
                    <option value="en">English</option>
                </select>
            </div>
            <div class="setting-row">
                <span id="themeLabel">المظهر</span>
                <select class="setting-select" id="themeSelect" onchange="changeTheme()">
                    <option value="light">☀️ فاتح</option>
                    <option value="dark">🌙 داكن</option>
                </select>
            </div>
            <button class="close-btn" onclick="toggleSettings()" id="closeBtn">حفظ وإغلاق</button>
        </div>
    </div>

    <!-- التابات لتغطية كل الأقسام الكبيرة -->
    <div class="tabs">
        <button class="tab-btn active" id="tabMorning" onclick="switchTab('morning')">أذكار الصباح</button>
        <button class="tab-btn" id="tabEvening" onclick="switchTab('evening')">أذكار المساء</button>
        <button class="tab-btn" id="tabSleeping" onclick="switchTab('sleeping')">أذكار النوم</button>
        <button class="tab-btn" id="tabIstighfar" onclick="switchTab('istighfar')">الاستغفار والتسبيح</button>
        <button class="tab-btn" id="tabDuas" onclick="switchTab('duas')">أدعية جامعة</button>
    </div>

    <!-- ================= أذكار الصباح كاملة ================= -->
    <div id="morning" class="dhikr-section active">
        <div class="card">
            <p class="text" data-ar="أَعُوذُ بِاللهِ مِنَ الشَّيْطَانِ الرَّجِيمِ: اللَّهُ لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ لَا تَأْخُذُهُ سِنَةٌ وَلَا نَوْمٌ..." data-en="Ayat al-Kursi: Allah! There is no deity except Him, the Alive, the Sustainer..."></p>
            <p class="source" data-ar="آية الكرسي - من قالها حين يصبح أجير من الجن حتى يمسي" data-en="Protection from Jinn until evening"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ: قُلْ هُوَ اللَّهُ أَحَدٌ... قُلْ أَعُوذُ بِرَبِّ الْفَلَقِ... قُلْ أَعُوذُ بِرَبِّ النَّاسِ..." data-en="Surah Al-Ikhlas, Al-Falaq, Al-Nas."></p>
            <p class="source" data-ar="الإخلاص والمعوذتين (3 مرات) - تكفيك من كل شيء" data-en="Sufficient for you against everything"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="أَصْبَحْنَا وَأَصْبَحَ الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ، لَهُ الْمُلْكُ وَلَهُ الْحَمْدُ وَهُوَ عَلَى كُلِّ شَيْءٍ قَدِيرٌ." data-en="We have entered upon morning and the whole kingdom belongs to Allah..."></p>
            <p class="source" data-ar="رواه مسلم" data-en="Narrated by Muslim"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ أَنْتَ رَبِّي لَا إِلَهَ إِلَّا أَنْتَ، خَلَقْتَنِي وَأَنَا عَبْدُكَ، وَأَنَا عَلَى عَهْدِكَ وَوَعْدِكَ مَا اسْتَطَعْتُ، أَعُوذُ بِكَ مِنْ شَرِّ مَا صَنَعْتُ..." data-en="O Allah, You are my Lord, there is no deity except You. You created me and I am Your servant..."></p>
            <p class="source" data-ar="سيد الاستغفار - من قالها موقناً بها ومات دخل الجنة" data-en="The Master of Seeking Forgiveness"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ عافِني في بَدَني، اللَّهُمَّ عافِني في سَمْعي، اللَّهُمَّ عافِني في بَصَري، لا إلهَ إلَّا أنتَ." data-en="O Allah, grant health to my body, my hearing, and my sight..."></p>
            <p class="source" data-ar="رواه أبو داود" data-en="Narrated by Abu Dawud"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="بِسْمِ اللَّهِ الَّذِي لَا يَضُرُّ مَعَ اسْمِهِ شَيْءٌ فِي الْأَرْضِ وَلَا فِي السَّمَاءِ وَهُوَ السَّمِيعُ الْعَلِيمُ." data-en="In the name of Allah, with Whose name nothing is harmed on earth nor in heaven..."></p>
            <p class="source" data-ar="لم يضره شيء في ذلك اليوم" data-en="Nothing will harm him on that day"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="رَضِيتُ بِاللَّهِ رَبَّاً، وَبِالْإِسْلَامِ دِيناً، وَبِمُحَمَّدٍ ﷺ نَبِيَّاً." data-en="I am pleased with Allah as my Lord, Islam as my religion, and Muhammad as my Prophet."></p>
            <p class="source" data-ar="كان حقاً على الله أن يرضيه يوم القيامة" data-en="Allah will please him on Judgement Day"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="يَا حَيُّ يَا قَيُّومُ بِرَحْمَتِكَ أَسْتَغِيثُ، أَصْلِحْ لِي شَأْنِي كُلَّهُ وَلَا تَكِلْنِي إِلَى نَفْسِي طَرْفَةَ عَيْنٍ." data-en="O Ever-Living, O Sustainer, by Your mercy I seek help, rectify all my affairs..."></p>
            <p class="source" data-ar="رواه الحاكم" data-en="Narrated by Al-Hakim"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
    </div>

    <!-- ================= أذكار المساء كاملة ================= -->
    <div id="evening" class="dhikr-section">
        <div class="card">
            <p class="text" data-ar="أَعُوذُ بِاللهِ مِنَ الشَّيْطَانِ الرَّجِيمِ: اللَّهُ لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ..." data-en="Ayat al-Kursi: Allah! There is no deity except Him, the Alive, the Sustainer..."></p>
            <p class="source" data-ar="من قالها حين يمسي أجير من الجن حتى يصبح" data-en="Protection from Jinn until morning"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="أَمْسَيْنَا وَأَمْسَى الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ." data-en="We have entered upon evening and the whole kingdom belongs to Allah..."></p>
            <p class="source" data-ar="رواه مسلم" data-en="Narrated by Muslim"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ بِكَ أَمْسَيْنَا، وَبِكَ أَصْبَحْنَا، وَبِكَ نَحْيَا، وَبِكَ نَمُوتُ، وَإِلَيْكَ الْمَصِيرُ." data-en="O Allah, by You we enter the evening and by You we enter the morning..."></p>
            <p class="source" data-ar="رواه الترمذي" data-en="Narrated by Al-Tirmidhi"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="أَعُوذُ بِكَلِمَاتِ اللَّهِ التَّامَّاتِ مِنْ شَرِّ مَا خَلَقَ." data-en="I seek refuge in the perfect words of Allah from the evil of what He has created."></p>
            <p class="source" data-ar="من قالها حين يمسي لم تضره لدغة حية في تلك الليلة" data-en="Protection against harm during the night"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ عافِني في بَدَني، اللَّهُمَّ عافِني في سَمْعي، اللَّهُمَّ عافِني في بَصَري، لا إلهَ إلَّا أنتَ." data-en="O Allah, grant health to my body, my hearing, and my sight..."></p>
            <p class="source" data-ar="رواه أبو داود" data-en="Narrated by Abu Dawud"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
    </div>

    <!-- ================= أذكار النوم كاملة ================= -->
    <div id="sleeping" class="dhikr-section">
        <div class="card">
            <p class="text" data-ar="بِاسْمِكَ رَبِّي وَضَعْتُ جَنْبِي، وَبِكَ أَرْفَعُهُ، فَإِنْ أَمْسَكْتَ نَفْسِي فَارْحَمْهَا، وَإِنْ أَرْسَلْتَهَا فَاحْفَظْهَا بِمَا تَحْفَظُ بِهِ عِبَادَكَ الصَّالِحِينَ." data-en="In Your name my Lord, I lie down and by Your glory I rise..."></p>
            <p class="source" data-ar="رواه البخاري ومسلم" data-en="Al-Bukhari & Muslim"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ قِنِي عَذَابَكَ يَوْمَ تَبْعَثُ عِبَادَكَ." data-en="O Allah, protect me from Your punishment on the Day You resurrect Your servants."></p>
            <p class="source" data-ar="يُقال عند وضع اليد اليمنى تحت الخد عند النوم" data-en="Said when placing the right hand under the cheek"></p>
            <button class="counter-btn" onclick="count(this, 3)">3</button>
        </div>
        <div class="card">
            <p class="text" data-ar="بِاسْمِكَ اللَّهُمَّ أَمُوتُ وَأَحْيَا." data-en="In Your name, O Allah, I die and I live."></p>
            <p class="source" data-ar="رواه البخاري" data-en="Narrated by Al-Bukhari"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
    </div>

    <!-- ================= قسم الاستغفار والتسبيح الشامل ================= -->
    <div id="istighfar" class="dhikr-section">
        <div class="card">
            <p class="text" data-ar="أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ." data-en="I seek Allah's forgiveness and turn to Him in repentance."></p>
            <p class="source" data-ar="مائة مرة - استغفار يومي متواصل" data-en="100 Times Daily"></p>
            <button class="counter-btn" onclick="count(this, 100)">100</button>
        </div>
        <div class="card">
            <p class="text" data-ar="سُبْحَانَ اللَّهِ وَبِحَمْدِهِ." data-en="Glory be to Allah and praise is due to Him."></p>
            <p class="source" data-ar="مئة مرة - تحط الخطايا وإن كانت مثل زبد البحر" data-en="100 Times - Wipes away sins"></p>
            <button class="counter-btn" onclick="count(this, 100)">100</button>
        </div>
        <div class="card">
            <p class="text" data-ar="سُبْحَانَ اللَّهِ، وَالْحَمْدُ لِلَّهِ، وَلَا إِلَهَ إِلَّا اللَّهُ، وَاللَّهُ أَكْبَرُ." data-en="Glory be to Allah, Praise be to Allah, There is no God but Allah, Allah is the Greatest."></p>
            <p class="source" data-ar="الباقيات الصالحات وأحب الكلام إلى الله" data-en="The most beloved words to Allah"></p>
            <button class="counter-btn" onclick="count(this, 33)">33</button>
        </div>
        <div class="card">
            <p class="text" data-ar="لَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ." data-en="There is no might nor power except with Allah."></p>
            <p class="source" data-ar="كنز من كنوز الجنة والدافعة للهموم" data-en="A treasure from Paradise"></p>
            <button class="counter-btn" onclick="count(this, 100)">100</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ صَلِّ وَسَلِّمْ عَلَى نَبِيِّنَا مُحَمَّدٍ." data-en="O Allah, send blessings and peace upon our Prophet Muhammad."></p>
            <p class="source" data-ar="من صلى عليّ صلاة صلى الله عليه بها عشراً" data-en="10 to 100 times for blessings"></p>
            <button class="counter-btn" onclick="count(this, 100)">100</button>
        </div>
    </div>

    <!-- ================= قسم الأدعية الجامعة المستجابة ================= -->
    <div id="duas" class="dhikr-section">
        <div class="card">
            <p class="text" data-ar="رَبَّنَا آتِنَا فِي الدُّنْيَا حَسَنَةً وَفِي الْآخِرَةُ حَسَنَةً وَقِنَا عَذَابَ النَّارِ." data-en="Our Lord, give us in this world that which is good and in the Hereafter that which is good..."></p>
            <p class="source" data-ar="من أجمع أدعية القرآن الكريم وكان يكثر منها النبي ﷺ" data-en="From the Holy Quran"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="يَا مُقَلِّبَ الْقُلُوبِ ثَبِّتْ قَلْبِي عَلَى دِينِكَ." data-en="O Turner of the hearts, keep my heart firm upon Your religion."></p>
            <p class="source" data-ar="دعاء النبي ﷺ المستمر للثبات" data-en="Prophet's Dua for steadfastness"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ إِنِّي أَسْأَلُكَ الْعَفْوَ وَالْعَافِيَةَ فِي الدُّنْيَا وَالْآخِرَةِ." data-en="O Allah, I ask You for forgiveness and well-being in this world and the Hereafter."></p>
            <p class="source" data-ar="دعاء العافية والستر" data-en="Supplication for well-being"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
        <div class="card">
            <p class="text" data-ar="اللَّهُمَّ إِنَّكَ عَفُوٌّ تُحِبُّ الْعَفْوَ فَاعْفُ عَنِّي." data-en="O Allah, You are Forgiving and You love forgiveness, so forgive me."></p>
            <p class="source" data-ar="دعاء ليلة القدر والأوقات المباركة" data-en="Dua for forgiveness"></p>
            <button class="counter-btn" onclick="count(this, 1)">1</button>
        </div>
    </div>

    <script>
        let currentLang = 'ar';

        const uiTexts = {
            ar: {
                title: "حصن المسلم الشامل", sub: "الموسوعة الكاملة للأذكار والأدعية والاستغفار", settings: "الإعدادات ⚙️",
                lang: "اللغة", theme: "المظهر", close: "حفظ وإغلاق",
                morning: "أذكار الصباح", evening: "أذكار المساء", sleeping: "أذكار النوم", istighfar: "الاستغفار والتسبيح", duas: "أدعية جامعة",
                remaining: "المتبقي: ", done: "تم بنجاح ✓"
            },
            en: {
                title: "The Ultimate Fortress", sub: "The Complete Encyclopedia of Azkar, Duas & Repentance", settings: "Settings ⚙️",
                lang: "Language", theme: "Theme", close: "Save & Close",
                morning: "Morning Azkar", evening: "Evening Azkar", sleeping: "Sleeping", istighfar: "Praises & Forgiveness", duas: "Comprehensive Duas",
                remaining: "Remaining: ", done: "Completed ✓"
            }
        };

        function toggleSettings() {
            const modal = document.getElementById('settingsModal');
            modal.style.display = (modal.style.display === 'flex') ? 'none' : 'flex';
        }

        function switchTab(tabId) {
            document.querySelectorAll('.dhikr-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            event.currentTarget.classList.add('active');
        }

        function count(btn, max) {
            if (btn.classList.contains('done')) return;
            let currentText = btn.innerText.replace(/[^0-9]/g, '');
            let current = currentText === "" ? max : parseInt(currentText);
            
            if (current > 1) {
                current--;
                btn.innerText = uiTexts[currentLang].remaining + current;
            } else {
                btn.classList.add('done');
                btn.innerText = uiTexts[currentLang].done;
            }
        }

        function changeTheme() {
            const theme = document.getElementById('themeSelect').value;
            if (theme === 'dark') {
                document.documentElement.setAttribute('data-theme', 'dark');
            } else {
                document.documentElement.removeAttribute('data-theme');
            }
        }

        function changeLanguage() {
            currentLang = document.getElementById('langSelect').value;
            const html = document.documentElement;
            
            if (currentLang === 'en') {
                html.setAttribute('lang', 'en');
                html.setAttribute('dir', 'ltr');
            } else {
                html.setAttribute('lang', 'ar');
                html.setAttribute('dir', 'rtl');
            }
            updateDOMTexts();
        }

        function updateDOMTexts() {
            const t = uiTexts[currentLang];
            document.getElementById('mainTitle').innerText = t.title;
            document.getElementById('mainSub').innerText = t.sub;
            document.getElementById('settingsTitle').innerText = t.settings;
            document.getElementById('langLabel').innerText = t.lang;
            document.getElementById('themeLabel').innerText = t.theme;
            document.getElementById('closeBtn').innerText = t.close;
            document.getElementById('tabMorning').innerText = t.morning;
            document.getElementById('tabEvening').innerText = t.evening;
            document.getElementById('tabSleeping').innerText = t.sleeping;
            document.getElementById('tabIstighfar').innerText = t.istighfar;
            document.getElementById('tabDuas').innerText = t.duas;

            document.querySelectorAll('[data-ar]').forEach(el => {
                el.innerText = el.getAttribute('data-' + currentLang);
            });

            document.querySelectorAll('.counter-btn').forEach(btn => {
                if (!btn.classList.contains('done')) {
                    let num = btn.innerText.replace(/[^0-9]/g, '');
                    btn.innerText = t.remaining + (num || btn.getAttribute('onclick').match(/\d+/)[0]);
                } else {
                    btn.innerText = t.done;
                }
            });
        }

        updateDOMTexts();
    </script>
</body>
</html>
