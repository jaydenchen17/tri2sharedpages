---
toc: False
comments: False
hide: True
layout: post
title: Color Searcher
---
<button onclick="window.location.href='/Nighthawk-Pages/2023/11/16/Binary_Logic_Warmup_Homepage.html'" style="background-color: #add8e6; color: white; padding: 15px 30px; font-size: 20px; cursor: pointer;">Back to Home</button>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color Information</title>
    <style>
        body {
            background-color: #add8e6; 
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }
        #color-box {
            width: 100px;
            height: 100px;
            margin-top: 10px;
            border: 2px solid white; 
            border: 2px solid black; 
        }
    </style>
</head>
<body>

<h1>Color Information</h1>

<label for="colorInput">Enter color name or hex code:</label>
<input type="text" id="colorInput" placeholder="e.g., red or #FF0000">

<button onclick="getColorInfo()">Get Color Info</button>

<div>
    <p>Hex Code: <span id="hexCode"></span></p>
    <p>Binary Code: <span id="binaryCode"></span></p>
</div>

<div id="color-box"></div>

<script>
    function getColorInfo() {
 
        var colorInput = document.getElementById('colorInput').value.toLowerCase();

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

        if (colorInput in colors) {
            var hexCode = colors[colorInput];
            var binaryCode = hexToBinary(hexCode);

            document.getElementById('hexCode').innerText = hexCode;
            document.getElementById('binaryCode').innerText = binaryCode;

          
            var colorBox = document.getElementById('color-box');
            colorBox.style.backgroundColor = hexCode;
        } else {
 
            if (/^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/.test(colorInput)) {
                var hexCode = colorInput;
                var binaryCode = hexToBinary(hexCode);

         
                document.getElementById('hexCode').innerText = hexCode;
                document.getElementById('binaryCode').innerText = binaryCode;

             
                var colorBox = document.getElementById('color-box');
                colorBox.style.backgroundColor = hexCode;
            } else {
                alert('Invalid color name or hex code. Please enter a basic color name or a valid hex code.');
            }
        }
    }

    function hexToBinary(hex) {
       
        var binaryString = parseInt(hex.substring(1), 16).toString(2);
        var paddedBinary = binaryString.padStart(Math.ceil(binaryString.length / 8) * 8, '0');
        return paddedBinary.match(/.{1,8}/g).join(' ');
    }
</script>

</body>
</html>

When you click the button, it runs the function called getColorInfo. This function has gets the color you inputted and also has a variable with a list of colors and their hex codes. Then, the text inputted is compared to all the colors in the list and if it matches it displays the color name, hex code, and color in the box. Next, another function called hexToBinary converts the hex code into binary and displays it. I also added a hex color searcher where when you input a hex code it outputs a color as well as its binary.