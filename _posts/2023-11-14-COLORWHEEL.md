---
toc: True
comments: True
hide: True
layout: post
title: Binary CSP Project
---
 <button onclick="window.location.href='/Nighthawk-Pages/2023/11/16/Binary_Logic_Warmup_Homepage.html'" style="background-color: #add8e6; color: white; padding: 15px 30px; font-size: 20px; cursor: pointer;">Back to Home</button>

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Color Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #add8e6;
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

