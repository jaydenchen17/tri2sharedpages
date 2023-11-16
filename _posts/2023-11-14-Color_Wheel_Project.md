---
toc: True
comments: True
hide: True
layout: post
title: Binary CSP Project
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rainbow Color Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #f0f0f0;
      color: #333;
    }
    table {
      border-collapse: collapse;
      width: 600px;
      background-color: #d9d9d9;
    }
    th, td {
      padding: 0;
      border: 1px solid #ccc;
    }
    th {
      background-color: #333;
      color: #fff;
    }
    .color-box {
      width: 60px;
      height: 60px;
      cursor: pointer;
      position: relative;
    }
    .details {
      display: none;
      position: absolute;
      width: 120px;
      background-color: #333;
      color: #fff;
      text-align: center;
      border-radius: 5px;
      padding: 5px;
      bottom: 100%;
      left: 50%;
      margin-left: -60px;
    }
    .color-box:hover .details {
      display: block;
    }
    .color-box:hover {
      filter: brightness(150%); 
    }
    #colorInfo {
      text-align: center;
    }
  </style>
</head>
<body>
  <table>
    <thead>
      <tr>
        <th>Colors:</th>
      </tr>
    </thead>
    <tbody id="colorTableBody">
    </tbody>
  </table>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      const colors = ['#ff0000', '#ff7f00', '#ffff00', '#00ff00', '#0000ff', '#8b00ff', '#000000', '#ffffff'];
      const tableBody = document.getElementById('colorTableBody');

      colors.forEach(color => {
        createColorRow(color);
      });

      function createColorRow(color) {
        const newRow = document.createElement('tr');
        newRow.innerHTML = `
          <td class="color-box" style="background-color: ${color};">
            <div class="details">${getColorName(color)}: RGB(${hexToRgb(color).r}, ${hexToRgb(color).g}, ${hexToRgb(color).b})<br>
              Binary: ${rgbToBinary(hexToRgb(color))}<br> Hex: ${color}</div>
          </td>
        `;
        tableBody.appendChild(newRow);

        newRow.addEventListener('click', function() {
          const allRows = document.querySelectorAll('tr');
          allRows.forEach(row => row.classList.remove('clicked'));

          newRow.classList.add('clicked');
        });
      }

      function getColorName(hexColor) {
        const colorNames = {
          '#ff0000': 'Red',
          '#ff7f00': 'Orange',
          '#ffff00': 'Yellow',
          '#00ff00': 'Green',
          '#0000ff': 'Blue',
          '#8b00ff': 'Purple',
          '#000000': 'Black',
          '#ffffff': 'White',
        };

        return colorNames[hexColor] || '';
      }

      function hexToRgb(hex) {
        hex = hex.slice(1);
        const bigint = parseInt(hex, 16);
        const r = (bigint >> 16) & 255;
        const g = (bigint >> 8) & 255;
        const b = bigint & 255;
        return { r, g, b };
      }

      function rgbToBinary(rgb) {
        return Object.values(rgb).map(val => val.toString(2).padStart(8, '0')).join(' ');
      }
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
