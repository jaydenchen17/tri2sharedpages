---
toc: true
comments: false
layout: post
type: help
title: Binary Lightbulb 
---
<button onclick="window.location.href='/Nighthawk-Pages/2023/11/16/Binary_Logic_Warmup_Homepage.html'" style="background-color: #add8e6; color: white; padding: 15px 30px; font-size: 20px; cursor: pointer;">Back to Home</button>

<br>

{% assign BITS = 8 %}

<style>
    body {
            background-color: #add8e6; /* Change the background color here */
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }
    td {
        text-align: center;
        vertical-align: middle;
    }

    .button {
        cursor: pointer;
        padding: 8px;
        border: 1px solid #ccc;
        border-radius: 5px;
        background-color: #f0f0f0;
        color: black; /* Add this line to set the button text color to black */
    }

    .button:hover {
        background-color: #ddd;
    }
</style>

<table>
    <thead>
        <tr class="header" id="table">
            <th>Increase</th>
            <th>Binary</th>
            <th>Octal</th>
            <th>Hexadecimal</th>
            <th>Decimal</th>
            <th>Decrease</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><div class="button" id="add1" onclick="add(1)">+ 1</div></td>
            <td id="binary">00000000</td>
            <td id="octal">0</td>
            <td id="hexadecimal">0</td>
            <td id="decimal">0</td>
            <td><div class="button" id="sub1" onclick="add(-1)">- 1</div></td>
        </tr>
    </tbody>
</table>

{% comment %}
Liquid for loop includes the last number, thus the Minus
{% endcomment %}
{% assign bits = BITS | minus: 1 %} 

<table>
    <thead>
        <tr>
            {% comment %}
            Build many bits
            {% endcomment %}
            {% for i in (0..bits) %}
            <th>
                <img id="bulb{{  i }}" src="{{site.baseurl}}/images/lightbulbOff.png" alt="" width="60" height="Auto">
                <div class="button" id="butt{{ i }}" name="{{ names[i] }}" onclick="javascript:toggleBit({{ i }})">Turn on {{ names[i] }}</div>
            </th>
            {% endfor %}
        </tr>
    </thead>
    <tbody>
        <tr>
            {% comment %}
            Value of bit
            {% endcomment %}
            {% for i in (0..bits) %}
            <td><input type='text' id="digit{{ i }}" Value="0" size="1" readonly></td>
            {% endfor %}
        </tr>
    </tbody>
</table>

<script>
    const BITS = {{ BITS }};
    const MAX = 2 ** BITS - 1;
    const MSG_ON = "Turn on";
    const IMAGE_ON = "{{site.baseurl}}/images/lightbulbOn.png";
    const MSG_OFF = "Turn off";
    const IMAGE_OFF = "{{site.baseurl}}/images/lightbulbOff.png"

    const names = ['marcus', 'nihar', 'miguel', 'brandon', 'jayden', 'aiden', 'chris', 'mr. lopez'];

    function getBits() {
        let bits = "";
        for(let i = 0; i < BITS; i++) {
            bits = bits + document.getElementById('digit' + i).value;
        }
        return bits;
    }

    function setConversions(binary) {
        document.getElementById('binary').innerHTML = binary;

        document.getElementById('octal').innerHTML = parseInt(binary, 2).toString(8);

        document.getElementById('hexadecimal').innerHTML = parseInt(binary, 2).toString(16);

        document.getElementById('decimal').innerHTML = parseInt(binary, 2).toString();
    }

    function decimal_2_base(decimal, base) {
        let conversion = "";

        do {
            let digit = decimal % base;
            conversion = "" + digit + conversion;
            decimal = ~~(decimal / base);
        } while (decimal > 0);
            
            if (base === 2) {
                for (let i = 0; conversion.length < BITS; i++) {
                    conversion = "0" + conversion;
            }
        }
        return conversion;
    }

    function toggleBit(i) {
        const dig = document.getElementById('digit' + i);
        const image = document.getElementById('bulb' + i);
        const butt = document.getElementById('butt' + i);

        const name = names[i];

        if (image.src.match(IMAGE_ON)) {
            dig.value = 0;
            image.src = IMAGE_OFF;
            butt.innerHTML = `Turn on ${name}`;
        } else {
            dig.value = 1;
            image.src = IMAGE_ON;
            butt.innerHTML = `Turn off ${name}`;
        }

        const binary = getBits();
        setConversions(binary);
    }
        

    function add(n) {
        let binary = getBits();

        let decimal = parseInt(binary, 2);
        if (n > 0) {
            decimal = MAX === decimal ? 0 : decimal += n;
        } else {
            decimal = 0 === decimal ? MAX : decimal += n;
        }

        binary = decimal_2_base(decimal, 2);

        setConversions(binary);

        for (let i = 0; i < binary.length; i++) {
            let digit = binary.substr(i, 1);
            document.getElementById('digit' + i).value = digit;
            const name = names[i];  // Get the corresponding name from the array
            if (digit === "1") {
                document.getElementById('bulb' + i).src = IMAGE_ON;
                document.getElementById('butt' + i).innerHTML = `Turn off ${name}`;
            } else {
                document.getElementById('bulb' + i).src = IMAGE_OFF;
                document.getElementById('butt' + i).innerHTML = `Turn on ${name}`;
            }
        }
    }

</script>


Our code creates a web page with a binary lightbulb interface, allowing users to interact with binary values that correspond with the lightbulbs. This binary representation is  displayed through lightbulb icons, and users can increase or decrease the binary number, to make changes to the binary, octal, hexadecimal, and decimal values. What we tried to make different was that we made each lightbulb button with specific names, like "nihar", "brandon" and "Mr. Lopez," making the user experience more engaging and customized to our group. 

We added names by creating an array called `names` that holds the corresponding names for each lightbulb button. Within the JavaScript section of the code, the toggleBit function was modified to include an additional parameter name, ensuring that each button displays the appropriate name when turned on or off. 