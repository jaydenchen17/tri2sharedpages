---
toc: true
comments: false
hide: true
layout: post
type: help
title: Color Wheel 
---

>>>>>>> 5c971c7 (color searcher)
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Color Wheel</title>
  <style>
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    canvas {
      border: 2px solid #000;
      cursor: crosshair;
    }
    #colorInfo {
      text-align: center;
    }
  </style>
</head>
<body>
  <canvas id="colorWheel" width="400" height="400"></canvas>
  <div id="colorInfo">
    <p id="rgbLabel">RGB: </p>
    <p id="binaryLabel">Binary: </p>
  </div>

  <script>
    const canvas = document.getElementById('colorWheel');
    const ctx = canvas.getContext('2d');
    const colorInfo = document.getElementById('colorInfo');
    const rgbLabel = document.getElementById('rgbLabel');
    const binaryLabel = document.getElementById('binaryLabel');

    function drawColorWheel() {
      const radius = canvas.width / 2;
      const centerX = canvas.width / 2;
      const centerY = canvas.height / 2;

      for (let angle = 0; angle < 360; angle++) {
        const startAngle = (angle * Math.PI) / 180;
        const endAngle = ((angle + 1) * Math.PI) / 180;
        const color = hsvToRgb(angle, 1, 1);
        ctx.beginPath();
        ctx.moveTo(centerX, centerY);
        ctx.arc(centerX, centerY, radius, startAngle, endAngle);
        ctx.fillStyle = `rgb(${color[0]}, ${color[1]}, ${color[2]})`;
        ctx.fill();
      }
    }

    function hsvToRgb(h, s, v) {
      h = (h + 360) % 360; // Ensure h is between 0 and 360 degrees
      h /= 360;
      s = Math.min(1, Math.max(0, s));
      v = Math.min(1, Math.max(0, v));

      let r, g, b;
      const i = Math.floor(h * 6);
      const f = h * 6 - i;
      const p = v * (1 - s);
      const q = v * (1 - f * s);
      const t = v * (1 - (1 - f) * s);

      switch (i % 6) {
        case 0: r = v; g = t; b = p; break;
        case 1: r = q; g = v; b = p; break;
        case 2: r = p; g = v; b = t; break;
        case 3: r = p; g = q; b = v; break;
        case 4: r = t; g = p; b = v; break;
        case 5: r = v; g = p; b = q; break;
      }

      return [Math.round(r * 255), Math.round(g * 255), Math.round(b * 255)];
    }

    function updateColorInfo(x, y) {
      const radius = canvas.width / 2;
      const centerX = canvas.width / 2;
      const centerY = canvas.height / 2;
      const angle = Math.atan2(y - centerY, x - centerX);
      const distance = Math.sqrt((x - centerX) ** 2 + (y - centerY) ** 2);
      const normalizedDistance = Math.min(1, Math.max(0, distance / radius));
      const color = hsvToRgb((angle * 180) / Math.PI, normalizedDistance, 1);

      rgbLabel.textContent = `RGB: ${color[0]}, ${color[1]}, ${color[2]}`;
      binaryLabel.textContent = `Binary: ${rgbToBinary(color)}`;
    }

    function rgbToBinary(rgb) {
      return `${rgb[0].toString(2).padStart(8, '0')} ${rgb[1].toString(2).padStart(8, '0')} ${rgb[2].toString(2).padStart(8, '0')}`;
    }

    drawColorWheel();

    canvas.addEventListener('mousemove', (event) => {
      const rect = canvas.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;

      updateColorInfo(x, y);
    });
  </script>
</body>
</html>


<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Color Searcher</title>
  <style>
    #colorBox {
      width: 100px;
      height: 100px;
      margin-bottom: 10px;
    }
  </style>
  <script>
    function updateColorAndBinary() {
      // Get the hex color code from the user
      var hexColorInput = document.getElementById('hexColorInput').value;
      // Validate the hex color code
      var isValidHex = /^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/.test(hexColorInput);
      if (!isValidHex) {
        alert('Please enter a valid hex color code.');
        return;
      }
      // Display the color
      var colorBox = document.getElementById('colorBox');
      colorBox.style.backgroundColor = hexToRgb(hexColorInput);
      // Display the binary representation of the color
      var decimalColorValue = parseInt(hexColorInput.substring(1), 16); // Remove '#' and convert to decimal
      var binaryResult = decimalColorValue.toString(2);
      document.getElementById('binaryResult').textContent = binaryResult;
    }
    function hexToRgb(hex) {
      // Remove the '#' character, if present
      hex = hex.replace(/^#/, '');
      // Parse the hex code to RGB
      var bigint = parseInt(hex, 16);
      var r = (bigint >> 16) & 255;
      var g = (bigint >> 8) & 255;
      var b = bigint & 255;
      // Return the RGB format
      return 'rgb(' + r + ',' + g + ',' + b + ')';
    }
  </script>
</head>
<body>
  <h2>Hex Color and Binary Operations</h2>

  <label for="hexColorInput">Enter Hex Color Code:</label>
  <input type="text" id="hexColorInput" placeholder="Enter hex color code" maxlength="7">

  <button onclick="updateColorAndBinary()">Update Color and Binary</button>

  <h3>Results:</h3>
  <div id="colorBox"></div>
  <p><strong>Binary Representation:</strong> <span id="binaryResult"></span></p>
</body>
</html>
