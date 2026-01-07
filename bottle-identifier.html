<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bottle Detector Canvas</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/coco-ssd"></script>

    <style>
        body {
            font-family: sans-serif;
            background-color: #f0f2f5;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        .controls {
            margin-bottom: 20px;
            padding: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            text-align: center;
        }

        #status {
            margin-top: 10px;
            font-weight: bold;
            color: #666;
        }

        /* The container for the image and canvas overlay */
        #canvas-container {
            position: relative;
            /* Start with a reasonable default size, it will adjust to image */
            min-width: 300px;
            min-height: 200px;
            border: 2px dashed #ccc;
            background: white;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: auto; /* Allow scrolling for large images */
             max-width: 90vw;
             max-height: 80vh;
        }

        /* Key part: Overlap image and canvas precisely */
        #uploaded-image, #overlay-canvas {
            position: absolute;
            top: 0;
            left: 0;
        }

        /* Hide image initially */
        #uploaded-image {
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        #uploaded-image.loaded {
            opacity: 1;
            position: relative; /* Switch back to relative once loaded to give container size */
        }

         /* Canvas must remain absolute to overlap the relative image */
        #overlay-canvas.loaded {
             pointer-events: none; /* Let clicks pass through to image if needed */
        }

        .placeholder-text {
            color: #aaa;
            pointer-events: none;
        }
    </style>
</head>
<body>

    <div class="controls">
        <h2>Bottle Detector</h2>
        <p>Paste an image (Ctrl+V) directly onto the page, or upload one.</p>
        <input type="file" id="fileInput" accept="image/*">
        <div id="status">Loading AI Model... (this may take a few seconds initially)</div>
    </div>

    <div id="canvas-container">
        <span class="placeholder-text" id="placeholder">No image loaded yet...</span>
        <img id="uploaded-image" crossorigin="anonymous">
        <canvas id="overlay-canvas"></canvas>
    </div>


<script>
    let model = null;
    const statusEl = document.getElementById('status');
    const imgEl = document.getElementById('uploaded-image');
    const canvasEl = document.getElementById('overlay-canvas');
    const containerEl = document.getElementById('canvas-container');
    const placeholderEl = document.getElementById('placeholder');
    const ctx = canvasEl.getContext('2d');

    // --- 1. Initialization ---

    // Load the COCO-SSD model first
    cocoSsd.load().then(loadedModel => {
        model = loadedModel;
        statusEl.innerText = "AI Model Ready. Paste or upload an image.";
        statusEl.style.color = "green";
    });

    // --- 2. Input Handling (Paste & Upload) ---

    // Handle File Upload
    document.getElementById('fileInput').addEventListener('change', (e) => {
        if (e.target.files[0]) {
            processFile(e.target.files[0]);
        }
    });

    // Handle Paste Event anywhere on the document
    document.addEventListener('paste', (e) => {
        const items = (e.clipboardData || e.originalEvent.clipboardData).items;
        for (const index in items) {
            const item = items[index];
            if (item.kind === 'file') {
                const blob = item.getAsFile();
                processFile(blob);
                return; // Stop after finding the first file
            }
        }
    });

    function processFile(file) {
        if (!file.type.startsWith('image/')){
             statusEl.innerText = "Error: Paste or upload an image file.";
             statusEl.style.color = "red";
             return;
        }

        const reader = new FileReader();
        reader.onload = (event) => {
            // Set the image source to the uploaded data
            imgEl.src = event.target.result;
            // The rest of the logic happens in imgEl.onload below
        };
        reader.readAsDataURL(file);
    }


    // --- 3. Core Logic: When image loads, detect and draw ---

    imgEl.onload = () => {
        // UI updates
        placeholderEl.style.display = 'none';
        imgEl.classList.add('loaded');
        canvasEl.classList.add('loaded');
        statusEl.innerText = "Analyzing image for bottles...";
        statusEl.style.color = "#666";

        // 1. Resize Canvas to match Image exactly
        canvasEl.width = imgEl.width;
        canvasEl.height = imgEl.height;
        
        // Clear previous drawings
        ctx.clearRect(0, 0, canvasEl.width, canvasEl.height);

        // Ensure model is loaded before running detection
        if (!model) {
            statusEl.innerText = "Error: Model not loaded yet. Please refresh.";
             statusEl.style.color = "red";
            return;
        }

        // 2. Run Detection
        model.detect(imgEl).then(predictions => {
            statusEl.innerText = `Analysis complete. Found ${predictions.length} objects.`;
             statusEl.style.color = "green";
            drawBoxes(predictions);
        });
    };


    // --- 4. Drawing Logic ---

    function drawBoxes(predictions) {
        predictions.forEach(prediction => {
            // Filter: We only care about bottles
            if (prediction.class === 'bottle') {
                
                const [x, y, width, height] = prediction.bbox;
                const score = Math.round(prediction.score * 100);

                // Draw Rectangle Style
                ctx.strokeStyle = '#FF0000'; // Red box
                ctx.lineWidth = 4;
                ctx.strokeRect(x, y, width, height);

                // Draw Label Style
                ctx.font = '18px Arial';
                ctx.fillStyle = '#FF0000';
                // Draw background for text for readability
                const textWidth = ctx.measureText(text).width;
                ctx.fillRect(x, y - 25, textWidth + 10, 25);

                // Draw text over the background
                ctx.fillStyle = '#FFFFFF';
                const text = `Bottle (${score}%)`;
                ctx.fillText(text, x + 5, y - 7);
            }
        });
    }

</script>
</body>
</html>
