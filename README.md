# Ex.05 Design a Website for Server Side Processing
# Date:30:11:2024
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
P = I2R
P --> Power (in watts)
 I --> Intensity
 R --> Resistance

# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
```
html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lamp Filament Power Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #f4f4f9;
    }
    .container {
      width: 100%;
      max-width: 500px;
      margin: 0 auto;
      background-color: #ffffff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
    }
    label {
      font-size: 18px;
      margin-bottom: 10px;
      display: block;
    }
    input[type="number"] {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      margin: 10px 0;
      border-radius: 4px;
      border: 1px solid #ccc;
    }
    .btn {
      width: 100%;
      padding: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 4px;
      cursor: pointer;
    }
    .btn:hover {
      background-color: #45a049;
    }
    .output {
      margin-top: 20px;
      padding: 10px;
      background-color: #f4f4f4;
      border: 1px solid #ccc;
      border-radius: 4px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Lamp Filament Power Calculator</h1>

    <label for="intensity">Intensity (I in Amps):</label>
    <input type="number" id="intensity" placeholder="Enter intensity" step="any">

    <label for="resistance">Resistance (R in Ohms):</label>
    <input type="number" id="resistance" placeholder="Enter resistance" step="any">

    <label for="power">Power (P in Watts):</label>
    <input type="number" id="power" placeholder="Enter power" step="any">

    <button class="btn" onclick="calculate()">Calculate</button>

    <div id="output" class="output" style="display:none;">
      <h3>Calculated Result:</h3>
      <p id="calculated-value"></p>
    </div>
  </div>

  <script>
    function calculate() {
      let intensity = parseFloat(document.getElementById('intensity').value);
      let resistance = parseFloat(document.getElementById('resistance').value);
      let power = parseFloat(document.getElementById('power').value);
      let result;

      // Check how many fields are filled
      if (intensity && resistance && !power) {
        // Calculate Power (P = I^2 * R)
        result = Math.pow(intensity, 2) * resistance;
        document.getElementById('calculated-value').innerText = `Power (P) = ${result.toFixed(2)} Watts`;
      } else if (resistance && power && !intensity) {
        // Calculate Intensity (I = sqrt(P / R))
        result = Math.sqrt(power / resistance);
        document.getElementById('calculated-value').innerText = `Intensity (I) = ${result.toFixed(2)} Amps`;
      } else if (intensity && power && !resistance) {
        // Calculate Resistance (R = P / I^2)
        result = power / Math.pow(intensity, 2);
        document.getElementById('calculated-value').innerText = `Resistance (R) = ${result.toFixed(2)} Ohms`;
      } else {
        document.getElementById('calculated-value').innerText = 'Please enter two values to calculate the third.';
      }

      // Show the result div
      document.getElementById('output').style.display = 'block';
    }
  </script>
</body>
</html>

views.py

from django.shortcuts import render 
def power(request): 
    context={} 
    context['power'] = "0" 
    context['r'] = "0" 
    context['i'] = "0" 
    if request.method == 'POST': 
        print("POST method is used")
        r = request.POST.get('Resistance','0')
        i = request.POST.get('Intensity','0')
        print('request=',request) 
        print('Resistance=',r) 
        print('Intensity=',i) 
        power = int(r) *int(i) *int(i) 
        context['power'] = power
        context['r'] = r
        context['i'] = i
        print('power=',power) 
    return render(request,'app1/home.html',context)

urls.py

from django.contrib import admin 
from django.urls import path 
from app1 import views 
urlpatterns = [ 
    path('admin/', admin.site.urls), 
    path('power/',views.power,name="calculatepower"),
    path('',views.power,name="calculatepower")
]

```


# SERVER SIDE PROCESSING:

![Screenshot 2024-12-08  001917](https://github.com/user-attachments/assets/79bb8028-2eac-4f3e-9654-70c03777d546)


# HOMEPAGE:
![Screenshot 2024-12-8  002039](https://github.com/user-attachments/assets/ee23b516-9d3f-41fa-b6c0-e9de9d6c615d)


# RESULT:
The program for performing server side processing is completed successfully.
