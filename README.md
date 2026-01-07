# reimagined-lamp.github.io
ai generation check for images
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JSON to YAML Canvas</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/js-yaml/4.1.0/js-yaml.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            display: flex;
            flex-direction: column;
            height: 100-vh;
            padding: 20px;
            box-sizing: border-box;
        }
        header { margin-bottom: 20px; }
        .canvas {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            flex-grow: 1;
        }
        .panel {
            display: flex;
            flex-direction: column;
        }
        label {
            font-weight: bold;
            margin-bottom: 10px;
            color: #333;
        }
        textarea {
            flex-grow: 1;
            padding: 15px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-family: "Fira Code", "Courier New", monospace;
            font-size: 14px;
            resize: none;
            box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
        }
        textarea:focus {
            outline: none;
            border-color: #007bff;
        }
        .error {
            color: #d9534f;
            font-size: 13px;
            margin-top: 5px;
            height: 20px;
        }
        button {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 10px;
        }
        button:hover { background-color: #0056b3; }
    </style>
</head>
<body>

<header>
    <h2>JSON to YAML Converter</h2>
    <p>Paste your JSON on the left; get YAML on the right.</p>
</header>

<div class="canvas">
    <div class="panel">
        <label>JSON Input</label>
        <textarea id="jsonInput" placeholder='{ "key": "value" }'></textarea>
        <div id="errorMessage" class="error"></div>
    </div>
    <div class="panel">
        <label>YAML Output</label>
        <textarea id="yamlOutput" readonly placeholder="YAML result will appear here..."></textarea>
        <button onclick="copyToClipboard()">Copy YAML</button>
    </div>
</div>

<script>
    const jsonInput = document.getElementById('jsonInput');
    const yamlOutput = document.getElementById('yamlOutput');
    const errorMessage = document.getElementById('errorMessage');

    jsonInput.addEventListener('input', () => {
        const val = jsonInput.value.trim();
        
        if (!val) {
            yamlOutput.value = '';
            errorMessage.textContent = '';
            return;
        }

        try {
            // 1. Parse JSON
            const parsed = JSON.parse(val);
            // 2. Convert to YAML using js-yaml
            const yaml = jsyaml.dump(parsed);
            
            yamlOutput.value = yaml;
            errorMessage.textContent = '';
        } catch (e) {
            errorMessage.textContent = "Invalid JSON: " + e.message;
            yamlOutput.value = '';
        }
    });

    function copyToClipboard() {
        yamlOutput.select();
        document.execCommand('copy');
        alert('YAML copied to clipboard!');
    }
</script>

</body>
</html>
