<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Professional Temperature Converter</title>
    <style>
        :root {
            --primary-color: #4361ee;
            --primary-dark: #3a56d4;
            --secondary-color: #3f37c9;
            --background-color: #f8f9fa;
            --card-color: #ffffff;
            --text-color: #2b2d42;
            --text-light: #8d99ae;
            --error-color: #ef233c;
            --success-color: #2ec4b6;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #e0f2fe, #f0f9ff);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .converter-container {
            background-color: var(--card-color);
            padding: 2.5rem;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            width: 100%;
            max-width: 500px;
            text-align: center;
            transition: all 0.3s ease;
        }
        
        .converter-container:hover {
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.12);
        }
        
        h1 {
            color: var(--text-color);
            margin-bottom: 1.5rem;
            font-size: 1.8rem;
            font-weight: 600;
        }
        
        .input-group {
            margin-bottom: 1.5rem;
            text-align: left;
        }
        
        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--text-color);
            font-size: 0.95rem;
        }
        
        input[type="number"] {
            width: 100%;
            padding: 0.8rem 1rem;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            box-sizing: border-box;
            transition: all 0.3s ease;
            background-color: #f8fafc;
        }
        
        input[type="number"]:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        .unit-selection {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
            margin-bottom: 2rem;
        }
        
        .radio-group {
            background-color: #f8fafc;
            padding: 1.2rem;
            border-radius: 10px;
            border: 1px solid #e2e8f0;
        }
        
        .radio-group label {
            color: var(--text-color);
            font-size: 0.9rem;
            margin-bottom: 0.8rem;
            display: block;
            font-weight: 600;
        }
        
        .radio-option {
            display: flex;
            align-items: center;
            margin-bottom: 0.6rem;
        }
        
        .radio-option input {
            appearance: none;
            width: 18px;
            height: 18px;
            border: 2px solid #cbd5e1;
            border-radius: 50%;
            margin-right: 0.6rem;
            position: relative;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .radio-option input:checked {
            border-color: var(--primary-color);
            background-color: var(--primary-color);
        }
        
        .radio-option input:checked::after {
            content: '';
            position: absolute;
            width: 8px;
            height: 8px;
            background-color: white;
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        
        .radio-option label {
            color: var(--text-color);
            font-weight: 400;
            margin-bottom: 0;
            cursor: pointer;
            flex: 1;
            text-align: left;
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 0.9rem 1.5rem;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            box-shadow: 0 4px 6px rgba(67, 97, 238, 0.1);
        }
        
        button:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(67, 97, 238, 0.15);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        .result {
            margin-top: 1.5rem;
            padding: 1.2rem;
            background-color: #f0fdf4;
            border-radius: 8px;
            font-size: 1.1rem;
            display: none;
            border: 1px solid #bbf7d0;
            color: var(--text-color);
            animation: fadeIn 0.4s ease-out;
        }
        
        .error {
            color: var(--error-color);
            margin-top: 0.8rem;
            display: none;
            font-size: 0.9rem;
            font-weight: 500;
            text-align: left;
            padding-left: 0.5rem;
            animation: fadeIn 0.3s ease-out;
        }
        
        #converted-temp {
            font-weight: 600;
            color: var(--primary-color);
        }
        
        #converted-unit {
            font-weight: 600;
            color: var(--secondary-color);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @media (max-width: 600px) {
            .converter-container {
                padding: 1.8rem;
            }
            
            .unit-selection {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="converter-container">
        <h1>Temperature Converter</h1>
        
        <div class="input-group">
            <label for="temperature">Temperature Value</label>
            <input type="number" id="temperature" placeholder="Enter temperature value" step="0.01">
        </div>
        
        <div class="unit-selection">
            <div class="radio-group">
                <label>Convert From</label>
                <div class="radio-option">
                    <input type="radio" id="from-celsius" name="from-unit" value="celsius" checked>
                    <label for="from-celsius">Celsius (°C)</label>
                </div>
                <div class="radio-option">
                    <input type="radio" id="from-fahrenheit" name="from-unit" value="fahrenheit">
                    <label for="from-fahrenheit">Fahrenheit (°F)</label>
                </div>
                <div class="radio-option">
                    <input type="radio" id="from-kelvin" name="from-unit" value="kelvin">
                    <label for="from-kelvin">Kelvin (K)</label>
                </div>
            </div>
            
            <div class="radio-group">
                <label>Convert To</label>
                <div class="radio-option">
                    <input type="radio" id="to-celsius" name="to-unit" value="celsius">
                    <label for="to-celsius">Celsius (°C)</label>
                </div>
                <div class="radio-option">
                    <input type="radio" id="to-fahrenheit" name="to-unit" value="fahrenheit" checked>
                    <label for="to-fahrenheit">Fahrenheit (°F)</label>
                </div>
                <div class="radio-option">
                    <input type="radio" id="to-kelvin" name="to-unit" value="kelvin">
                    <label for="to-kelvin">Kelvin (K)</label>
                </div>
            </div>
        </div>
        
        <button id="convert-btn">Convert Temperature</button>
        
        <div class="error" id="error-msg">Please enter a valid temperature value</div>
        
        <div class="result" id="result">
            Converted Temperature: <span id="converted-temp"></span> <span id="converted-unit"></span>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const convertBtn = document.getElementById('convert-btn');
            const temperatureInput = document.getElementById('temperature');
            const resultDiv = document.getElementById('result');
            const convertedTemp = document.getElementById('converted-temp');
            const convertedUnit = document.getElementById('converted-unit');
            const errorMsg = document.getElementById('error-msg');
            
            convertBtn.addEventListener('click', function() {
                // Hide previous result and error
                resultDiv.style.display = 'none';
                errorMsg.style.display = 'none';
                
                // Get input value
                const tempValue = parseFloat(temperatureInput.value);
                
                // Validate input
                if (isNaN(tempValue)) {
                    errorMsg.style.display = 'block';
                    return;
                }
                
                // Get selected units
                const fromUnit = document.querySelector('input[name="from-unit"]:checked').value;
                const toUnit = document.querySelector('input[name="to-unit"]:checked').value;
                
                // Convert temperature
                let convertedValue;
                let unitSymbol;
                
                if (fromUnit === toUnit) {
                    // No conversion needed
                    convertedValue = tempValue;
                } else {
                    // First convert to Celsius as intermediate step
                    let celsius;
                    switch(fromUnit) {
                        case 'celsius':
                            celsius = tempValue;
                            break;
                        case 'fahrenheit':
                            celsius = (tempValue - 32) * 5/9;
                            break;
                        case 'kelvin':
                            celsius = tempValue - 273.15;
                            break;
                    }
                    
                    // Then convert from Celsius to target unit
                    switch(toUnit) {
                        case 'celsius':
                            convertedValue = celsius;
                            unitSymbol = '°C';
                            break;
                        case 'fahrenheit':
                            convertedValue = (celsius * 9/5) + 32;
                            unitSymbol = '°F';
                            break;
                        case 'kelvin':
                            convertedValue = celsius + 273.15;
                            unitSymbol = 'K';
                            break;
                    }
                }
                
                // Round to 2 decimal places
                convertedValue = Math.round(convertedValue * 100) / 100;
                
                // Display result
                convertedTemp.textContent = convertedValue;
                convertedUnit.textContent = unitSymbol;
                resultDiv.style.display = 'block';
            });
            
            // Allow pressing Enter key to convert
            temperatureInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    convertBtn.click();
                }
            });
        });
    </script>
</body>
</html>
