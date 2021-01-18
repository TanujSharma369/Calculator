<!DOCTYPE html>
<html>
<head>
    <title>Calculator</title>
    <link rel="stylesheet" type = "text/css" href="style.css"> 
    
</head>
<body>
   
    <div id="calculator">
        <!-- <h1>Calculator</h1> -->
        <div id="display-container">
            <p id="display"> </p>
        </div>
        <div id="buttons-container">
            <div class="button grey" id="button-clear" data-value="ac">
                <span>C</span>
            </div>
            <div class="button grey" id="button-sign" data-value="sign">
                <span>+/-</span>
            </div>
            <div class="button grey" id="button-percent" data-value="%">
                <span> % </span>
            </div>
            <div class="button red" data-value="/" id="button-divide" >
                <span> / </span>
            </div>
            <div class="button" id="button-seven" data-value="7">
                <span>7</span>
            </div>
            <div class="button" id="button-eight" data-value="8">
                <span>8</span>
            </div>
            <div class="button" id="button-nine" data-value="9">
                <span>9</span>
            </div>
            <div class="button red" id="button-multiply" data-value="*">
                <span>*</span>
            </div>
            <div class="button" id="button-four" data-value="4">
                <span>4</span>
            </div>
            <div class="button" id="button-five" data-value="5">
                <span>5</span>
            </div>
            <div class="button" id="button-six" data-value="6">
                <span>6</span>
            </div>
            <div class="button red" id="button-minus" data-value="-">
                <span>-</span>
            </div>
            <div class="button" id="button-one" data-value="1">
                <span> 1 </span>
            </div>
            <div class="button" id="button-two" data-value="2">
                <span> 2 </span>
            </div>
            <div class="button" id="button-three" data-value="3">
                <span> 3 </span>
            </div>
            <div class="button red" id="button-plus" data-value="+">
                <span> + </span>
            </div>
            <div class="button" id="button-zero" data-value="0">
                <span> 0 </span>
            </div>
            <div class="button" id="button-one" data-value=" ">
                <span> </span>
            </div>            
            <div class="button" id="button-decimal" data-value=".">
                <span> . </span>
            </div>
            <div class="button yellow" id="button-equals" data-value="=">
                <span> = </span>
            </div>
        </div>
    </div>
    <script type="text/javascript" src="script.js"></script>
</body>
<html>



* {
    box-sizing: border-box;
}

:root {
    --border-radius: 5px;
    --border-width: 0.1px;
    --light-grey: #e2e0e0;
    --blue: #7f6cfc;
    --orange: #ffc877;
    --red: #c14444;
    
}

#calculator {
    width: 45%;
    height: 80%;
    min-width: 300px;
    min-height: 400px;
    background-color: var(--light-grey);
    margin: auto;
    margin-top: 80px;
    border: 20px;
    border-color: black;
    border-radius: var(--border-radius);
    padding: 0px;
}

#calculator h1 {
    background-color: black;
    color: white;
    text-transform: uppercase;
    text-align: center;
    padding: 10px;
}

#display-container {
    font-size: 2.8rem;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    color: var(--blue);
    width: 100%;
    height: 20%;
    min-height: 100px;
    border-radius: var(--border-radius);
    background-color: whitesmoke;
    margin-bottom: 10px;
}

#display-container p {
    margin: 0rem;
    vertical-align: text-bottom;
}

#buttons-container {
    width: 100%;
    height: 60%;
    min-height: 300px;
    border: var(--border-width) solid var(--light-grey);
    border-radius: var(--border-radius);
    background-color: var(--light-grey);
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    margin: 0%;
}

.button {
    width: 25%;
    height: 20%;
    min-height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: var(--border-width) solid var(--light-grey);
    background-color: white;
    font-size: 1.8rem;
    cursor: pointer;
    transition-duration: 1s;
}

.button:hover {
    background-color: var(--orange);
}

.red {
    background-color: #495464;
    color: white;
}

#button-zero {
    width: 25%;
}
.yellow {
    background-color: rgb(255, 200, 0);
    color: white;
}
.grey{
    background-color: #e8e8e8;
    color : black;
}


var buttons = document.getElementsByClassName("button");
var display = document.getElementById("display");

// display.textContent = 0;
var operand1 = 0;
var operand2 = null;
var operator = null;

function isOperator(value) {
    return value == "+" || value == "-" || value == "*" || value == "/";
}

for (var i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', function () {

        var value = this.getAttribute('data-value');
        var text = display.textContent.trim();

        if (isOperator(value)) {
            operator = value;
            operand1 = parseFloat(text);
            display.textContent = "";
        } else if (value == "ac") {
            display.textContent = "";
        } else if (value == "sign") {
            operand1 = parseFloat(text);
            operand1 = -1 * operand1;
            display.textContent = operand1;
        } else if (value == ".") {
            if (text.length && !text.includes('.')) {
                display.textContent = text + '.';
            }
        } else if (value == "%") {
            operand1 = parseFloat(text);
            operand1 = operand1 / 100;
            display.textContent = operand1
        } else if (value == "=") {
            operand2 = parseFloat(text);
            var result = eval(operand1 + ' ' + operator + ' ' + operand2);
            if (result) {
                display.textContent = result;
                operand1 = result;
                operand2 = null;
                operator = null;
            }
        } else {
            display.textContent += value;
        }
    });
}

