---
toc: true
comments: true
hide: true
layout: post
title: Binary Project
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Binary Color Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #111; 
      color: #fff; 
    }

    table {
      border-collapse: collapse;
    }

    th, td {
      padding: 10px;
      text-align: center;
    }

    th {
      background-color: #333; /* Header background color */
    }

    td {
      cursor: pointer;
      transition: background-color 0.3s ease-in-out;
    }

    td:hover {
      background-color: #555; /* Hover background color */
    }
  </style>
</head>
<body>
  <table>
    <thead>
      <tr>
        <th>Color</th>
        <th>Binary</th>
      </tr>
    </thead>
    <tbody id="colorTableBody">
    
    </tbody>
  </table>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
    
      const rainbowColors = ['#ff0000', '#ff7f00', '#ffff00', '#00ff00', '#0000ff', '#4b0082', '#8b00ff'];

      const tableBody = document.getElementById('colorTableBody');

      rainbowColors.forEach(color => {
        const binaryColor = rgbToBinary(hexToRgb(color));
        createColorRow(color, binaryColor);
      });

      function hexToRgb(hex) {
     
        hex = hex.slice(1);
      
        const bigint = parseInt(hex, 16);
        // Extract RGB components
        const r = (bigint >> 16) & 255;
        const g = (bigint >> 8) & 255;
        const b = bigint & 255;
      
        return { r, g, b };
      }

      function rgbToBinary(rgb) {
        return Object.values(rgb).map(val => val.toString(2).padStart(8, '0')).join(' ');
      }

      // Function to create a row in the table
      function createColorRow(color, binaryColor) {
        const newRow = document.createElement('tr');
        newRow.innerHTML = `
          <td style="background-color: ${color};" onclick="showBinary('${binaryColor}')"></td>
          <td>${binaryColor}</td>
        `;
        tableBody.appendChild(newRow);
      }

      // Function to display the binary color
      window.showBinary = function(binaryColor) {
        alert(`Binary Representation: ${binaryColor}`);
      };
    });
  </script>
</body>
</html>
