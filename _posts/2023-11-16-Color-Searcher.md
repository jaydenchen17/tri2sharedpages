---
toc: False
comments: False
hide: True
layout: post
title: Color Searcher
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color Information</title>
    <style>
        #color-box {
            width: 100px;
            height: 100px;
            margin-top: 10px;
            border: 2px solid white; /* Add white border */
        }
    </style>
</head>
<body>

<h1>Color Information</h1>

<label for="colorName">Enter color name:</label>
<input type="text" id="colorName" placeholder="e.g., red">

<button onclick="getColorInfo()">Get Color Info</button>

<div>
    <p>Hex Code: <span id="hexCode"></span></p>
    <p>Binary Code: <span id="binaryCode"></span></p>
</div>

<div id="color-box"></div>

<script>
    function getColorInfo() {
        // Get the color name from the input field
        var colorName = document.getElementById('colorName').value.toLowerCase();

        // Dictionary mapping basic color names to hex codes
        var colors = {
            'red': '#FF0000',
            'green': '#00FF00',
            'blue': '#0000FF',
            'yellow': '#FFFF00',
            'orange': '#FFA500',
            'purple': '#800080',
            'pink': '#FFC0CB',
            'brown': '#A52A2A',
            'black': '#000000',
            'white': '#FFFFFF'
        };

        // Check if the entered color name is in the dictionary
        if (colorName in colors) {
            var hexCode = colors[colorName];
            var binaryCode = hexToBinary(hexCode);

            // Display the color information
            document.getElementById('hexCode').innerText = hexCode;
            document.getElementById('binaryCode').innerText = binaryCode;

            // Update the color box
            var colorBox = document.getElementById('color-box');
            colorBox.style.backgroundColor = hexCode;
        } else {
            alert('Invalid color name. Please enter a basic color name.');
        }
    }

    function hexToBinary(hex) {
        // Convert hex to binary and format in groups of 8
        var binaryString = parseInt(hex.substring(1), 16).toString(2);
        var paddedBinary = binaryString.padStart(Math.ceil(binaryString.length / 8) * 8, '0');

        // Insert spaces every 8 characters
        return paddedBinary.match(/.{1,8}/g).join(' ');
    }
</script>

</body>
</html>
