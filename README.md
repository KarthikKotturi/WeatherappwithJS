# WeatherappwithJS
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
</head>
<body>

    <h1>Weather App</h1>
    
    <label for="cityInput">Enter City:</label>
    <input type="text" id="cityInput">
    <button onclick="getWeather()">Get Weather</button>

    <div id="weatherResult"></div>

    <script>
        async function getWeather() {
            const apiKey = 'YOUR_OPENWEATHERMAP_API_KEY';
            const cityInput = document.getElementById('cityInput').value;

            const apiUrl = https://api.openweathermap.org/data/2.5/weather?q=${cityInput}&appid=${apiKey}&units=metric;

            try {
                const response = await fetch(apiUrl);
                const data = await response.json();

                if (response.ok) {
                    const weatherResult = document.getElementById('weatherResult');
                    weatherResult.innerHTML = `
                        <p>City: ${data.name}</p>
                        <p>Temperature: ${data.main.temp}°C</p>
                        <p>Weather: ${data.weather[0].description}</p>
                    `;
                } else {
                    alert(Error: ${data.message});
                }
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        }
    </script>

</body>
</html>
from flask import Flask, request, jsonify
import requests

app = Flask(_name_)

@app.route('/weather')
def get_weather():
    city = request.args.get('city')
    api_key = 'YOUR_WEATHER_API_KEY'
    weather_api_url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}'
    response = requests.get(weather_api_url)
    data = response.json()
    if data.get('cod') == 200:
        weather = data['weather'][0]['description']
        return jsonify({'weather': weather})
    else:
        return jsonify({'error': 'City not found'}), 404

if _name_ == '_main_':
    app.run(debug=True)
