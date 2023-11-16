---
toc: true
comments: false
layout: post
type: help
title: Binary Lightbulb 
---

{% assign BITS = 8 %}

<style>
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
            <th>Increment</th>
            <th>Binary</th>
            <th>Octal</th>
            <th>Hexadecimal</th>
            <th>Decimal</th>
            <th>Decrement</th>
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
            <th><img id="bulb{{ i }}" src="{{site.baseurl}}/images/lightbulbOff.png" alt="" width="40" height="Auto">
                <div class="button" id="butt{{ i }}" onclick="javascript:toggleBit({{ i }})">Turn on</div>
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
        
        if (image.src.match(IMAGE_ON)) {
            dig.value = 0;
            image.src = IMAGE_OFF;
            butt.innerHTML = MSG_ON;
        } else {
            dig.value = 1;
            image.src = IMAGE_ON;
            butt.innerHTML = MSG_OFF;
        }
        
        const binary = getBits();
        setConversions(binary);
    }

    function add(n) {
        let binary = getBits();
        
        let decimal = parseInt(binary, 2);
        if (n > 0) {
            decimal = MAX === decimal ? 0 : decimal += n;
        } else  {
            decimal = 0 === decimal ? MAX : decimal += n;
        }
        
        binary = decimal_2_base(decimal, 2);
        
        setConversions(binary);
        
        for (let i = 0; i < binary.length; i++) {
            let digit = binary.substr(i, 1);
            document.getElementById('digit' + i).value = digit;
            if (digit === "1") {
                document.getElementById('bulb' + i).src = IMAGE_ON;
                document.getElementById('butt' + i).innerHTML = MSG_OFF;
            } else {
                document.getElementById('bulb' + i).src = IMAGE_OFF;
                document.getElementById('butt' + i).innerHTML = MSG_ON;
            }
        }
    }
</script>