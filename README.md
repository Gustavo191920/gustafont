<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conversor Bold Unicode</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: #0a0a0a;
            color: #e0e0e0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            max-width: 700px;
            width: 100%;
        }

        h1 {
            font-size: 24px;
            font-weight: 600;
            color: #fff;
            margin-bottom: 40px;
            letter-spacing: -0.5px;
        }

        .text-area {
            width: 100%;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            border-radius: 8px;
            padding: 20px;
            font-size: 16px;
            color: #e0e0e0;
            resize: vertical;
            min-height: 120px;
            margin-bottom: 12px;
            font-family: 'SF Mono', 'Monaco', 'Cascadia Code', monospace;
            transition: border-color 0.2s ease;
        }

        .text-area:focus {
            outline: none;
            border-color: #404040;
        }

        .text-area::placeholder {
            color: #505050;
        }

        #output {
            background: #151515;
            font-size: 18px;
            letter-spacing: 0.3px;
        }

        .buttons {
            display: flex;
            gap: 8px;
            margin-top: 12px;
        }

        button {
            flex: 1;
            padding: 12px;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            border-radius: 6px;
            color: #e0e0e0;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        button:hover {
            background: #252525;
            border-color: #404040;
        }

        button:active {
            transform: scale(0.98);
        }

        .copy-btn:hover {
            color: #60d394;
        }

        .clear-btn:hover {
            color: #ff6b6b;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #1a1a1a;
            border: 1px solid #2a2a2a;
            color: #60d394;
            padding: 12px 20px;
            border-radius: 6px;
            font-size: 14px;
            display: none;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from {
                transform: translateX(400px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        .divider {
            height: 1px;
            background: #2a2a2a;
            margin: 30px 0;
        }

        .label {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #606060;
            margin-bottom: 8px;
            font-weight: 500;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Bold Unicode</h1>

        <div class="label">Input</div>
        <textarea id="input" class="text-area" placeholder="Digite seu texto aqui..."></textarea>

        <div class="divider"></div>

        <div class="label">Output</div>
        <textarea id="output" class="text-area" readonly></textarea>

        <div class="buttons">
            <button class="copy-btn" onclick="copyText()">Copiar</button>
            <button class="clear-btn" onclick="clearAll()">Limpar</button>
        </div>
    </div>

    <div class="notification" id="notification">Copiado</div>

    <script>
        function toBoldUnicode(text) {
            const boldMap = {
                'A': '𝗔', 'B': '𝗕', 'C': '𝗖', 'D': '𝗗', 'E': '𝗘', 'F': '𝗙', 'G': '𝗚', 'H': '𝗛',
                'I': '𝗜', 'J': '𝗝', 'K': '𝗞', 'L': '𝗟', 'M': '𝗠', 'N': '𝗡', 'O': '𝗢', 'P': '𝗣',
                'Q': '𝗤', 'R': '𝗥', 'S': '𝗦', 'T': '𝗧', 'U': '𝗨', 'V': '𝗩', 'W': '𝗪', 'X': '𝗫',
                'Y': '𝗬', 'Z': '𝗭',
                'a': '𝗮', 'b': '𝗯', 'c': '𝗰', 'd': '𝗱', 'e': '𝗲', 'f': '𝗳', 'g': '𝗴', 'h': '𝗵',
                'i': '𝗶', 'j': '𝗷', 'k': '𝗸', 'l': '𝗹', 'm': '𝗺', 'n': '𝗻', 'o': '𝗼', 'p': '𝗽',
                'q': '𝗾', 'r': '𝗿', 's': '𝘀', 't': '𝘁', 'u': '𝘂', 'v': '𝘃', 'w': '𝘄', 'x': '𝘅',
                'y': '𝘆', 'z': '𝘇',
                '0': '𝟬', '1': '𝟭', '2': '𝟮', '3': '𝟯', '4': '𝟰', '5': '𝟱', '6': '𝟲', '7': '𝟳',
                '8': '𝟴', '9': '𝟵'
            };

            return text.split('').map(char => boldMap[char] || char).join('');
        }

        function convertText() {
            const input = document.getElementById('input');
            const output = document.getElementById('output');
            output.value = toBoldUnicode(input.value);
        }

        function copyText() {
            const output = document.getElementById('output');
            if (output.value) {
                output.select();
                document.execCommand('copy');
                showNotification();
            }
        }

        function clearAll() {
            document.getElementById('input').value = '';
            document.getElementById('output').value = '';
        }

        function showNotification() {
            const notification = document.getElementById('notification');
            notification.style.display = 'block';
            setTimeout(() => {
                notification.style.display = 'none';
            }, 1500);
        }

        document.getElementById('input').addEventListener('input', convertText);
    </script>
</body>
</html>
