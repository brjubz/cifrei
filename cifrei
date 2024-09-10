<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cifrei - Transposição de Tom de Música</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #121212;
            color: #1DB954;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        header {
            background-color: #1DB954;
            width: 100%;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        header h1 {
            color: #fff;
            margin: 0;
            font-size: 2.5em;
        }
        main {
            width: 90%;
            max-width: 800px;
            margin: 20px auto;
            background-color: #282828;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: fadeIn 1s ease-in-out;
        }
        textarea {
            width: 100%;
            height: 300px;
            border: 1px solid #1DB954;
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
            background-color: #333;
            color: #fff;
            font-size: 1em;
        }
        .select-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }
        .select-container label {
            display: flex;
            align-items: center;
            gap: 5px;
            color: #fff;
        }
        select, button {
            padding: 10px;
            border: 1px solid #1DB954;
            border-radius: 5px;
            background-color: #1DB954;
            color: white;
            cursor: pointer;
            font-size: 1em;
        }
        button:hover {
            background-color: #1aa34a;
        }
        .paste-button {
            background-color: #808080;
            border: 1px solid #808080;
        }
        .paste-button:hover {
            background-color: #696969;
        }
        .copy-button {
            background-color: #808080;
            border: 1px solid #808080;
        }
        .copy-button:hover {
            background-color: #696969;
        }
        .transpose-button {
            background-color: #14833b;
            border: 1px solid #14833b;
        }
        .transpose-button:hover {
            background-color: #11632e;
        }
        pre {
            background-color: #333;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #1DB954;
            color: #fff;
            font-size: 1em;
        }
        .highlight {
            color: #1DB954;
            font-weight: bold;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>
    <header>
        <h1>Cifrei</h1>
    </header>
    <main>
        <h2>Transposição de Tom de Música</h2>
        <form id="musicForm">
            <label for="musicText">Digite a letra da música com as notas:</label><br>
            <textarea id="musicText" name="musicText"></textarea><br>
            <div class="select-container">
                <label for="originalKey">Tom Original:</label>
                <select id="originalKey" name="originalKey">
                    <option value="C">C (Dó)</option>
                    <option value="C#">C# (Dó#)</option>
                    <option value="D">D (Ré)</option>
                    <option value="D#">D# (Ré#)</option>
                    <option value="E">E (Mi)</option>
                    <option value="F">F (Fá)</option>
                    <option value="F#">F# (Fá#)</option>
                    <option value="G">G (Sol)</option>
                    <option value="G#">G# (Sol#)</option>
                    <option value="A">A (Lá)</option>
                    <option value="A#">A# (Lá#)</option>
                    <option value="B">B (Si)</option>
                </select>
            </div>
            <div class="select-container">
                <label for="desiredKey">Tom Desejado:</label>
                <select id="desiredKey" name="desiredKey">
                    <option value="C">C (Dó)</option>
                    <option value="C#">C# (Dó#)</option>
                    <option value="D">D (Ré)</option>
                    <option value="D#">D# (Ré#)</option>
                    <option value="E">E (Mi)</option>
                    <option value="F">F (Fá)</option>
                    <option value="F#">F# (Fá#)</option>
                    <option value="G">G (Sol)</option>
                    <option value="G#">G# (Sol#)</option>
                    <option value="A">A (Lá)</option>
                    <option value="A#">A# (Lá#)</option>
                    <option value="B">B (Si)</option>
                </select>
            </div>
            <button type="button" class="transpose-button" onclick="transpose()" style="width: 100%; margin-top: 20px; padding: 15px; font-size: 1.2em;">Transpor</button>
        </form>
        <h2>Resultado:</h2>
        <pre id="result"></pre>
        <button class="copy-button" onclick="copyToClipboard()">Copiar Texto</button>
    </main>

    <script>
        const notes = ['C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#', 'A', 'A#', 'B'];
        const complexNotes = ['maj7', 'm7', '7', 'm', 'dim', 'aug', 'sus2', 'sus4', 'add9', '6', '9', '11', '13'];
        const noteRegex = new RegExp(`\\b([A-G]#?)(maj7|m7|7|m|dim|aug|sus2|sus4|add9|6|9|11|13)?\\b`, 'g');

        function transpose() {
            const musicText = document.getElementById('musicText').value;
            const originalKey = document.getElementById('originalKey').value;
            const desiredKey = document.getElementById('desiredKey').value;

            const originalIndex = notes.indexOf(originalKey);
            const desiredIndex = notes.indexOf(desiredKey);
            const transposition = desiredIndex - originalIndex;

            const transposedText = musicText.replace(noteRegex, (match, baseNote, modifier) => {
                const noteIndex = notes.indexOf(baseNote);
                const newIndex = (noteIndex + transposition + notes.length) % notes.length;
                return `<span class="highlight">${notes[newIndex]}${modifier || ''}</span>`;
            });

            document.getElementById('result').innerHTML = transposedText;
        }

        function copyToClipboard() {
            const resultText = document.getElementById('result').innerText;
            const textarea = document.createElement('textarea');
            textarea.value = resultText;
            document.body.appendChild(textarea);
            textarea.select();
            document.execCommand('copy');
            document.body.removeChild(textarea);
            alert('Texto copiado para a área de transferência!');
        }

        function pasteFromClipboard() {
            const textarea = document.createElement('textarea');
            document.body.appendChild(textarea);
            textarea.focus();
            document.execCommand('paste');
            const pastedText = textarea.value;
            document.body.removeChild(textarea);
            document.getElementById('musicText').value = pastedText;
        }
    </script>
</body>
</html>
