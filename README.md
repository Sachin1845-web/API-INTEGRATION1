# API-INTEGRATION1
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
        }

        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #ffffff;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        header {
            text-align: center;
            margin-bottom: 20px;
        }

        h1 {
            font-size: 2.5em;
            color: #2c3e50;
        }

        .search-bar {
            text-align: center;
            margin-bottom: 20px;
        }

        input {
            padding: 10px;
            font-size: 1em;
            width: 60%;
            margin-right: 10px;
            border: 2px solid #ccc;
            border-radius: 4px;
        }

        button {
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            background-color: #3498db;
            color: #fff;
            border: none;
            border-radius: 4px;
        }

        button:hover {
            background-color: #2980b9;
        }

        #weather-info {
            text-align: center;
        }

        #weather-info p {
            font-size: 1.2em;
            margin: 10px 0;
        }

        @media (max-width: 600px) {
            .container {
                padding: 10px;
            }

            input {
                width: 70%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Weather App</h1>
        </header>

        <section id="weather-section">
            <div class="search-bar">
                <input type="text" id="city-input" placeholder="Enter city name" />
                <button onclick="getWeather()">Search</button>
            </div>

            <div id="weather-info">
                <p id="location">Enter a city to get weather information.</p>
                <p id="temperature"></p>
                <p id="description"></p>
                <p id="humidity"></p>
            </div>
        </section>
    </div>

    <script>
        const apiKey = 'YOUR_API_KEY';  // Replace with your OpenWeather API key

        function getWeather() {
            const city = document.getElementById('city-input').value;
            if (!city) {
                alert('Please enter a city name.');
                return;
            }

            // URL to fetch weather data from OpenWeather API
            const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`;

            fetch(url)
                .then(response => response.json())
                .then(data => {
                    if (data.cod === '404') {
                        alert('City not found.');
                    } else {
                        displayWeather(data);
                    }
                })
                .catch(error => {
                    console.error('Error fetching weather data:', error);
                    alert('Error fetching data. Please try again later.');
                });
        }

        function displayWeather(data) {
            const location = document.getElementById('location');
            const temperature = document.getElementById('temperature');
            const description = document.getElementById('description');
            const humidity = document.getElementById('humidity');

            location.textContent = `${data.name}, ${data.sys.country}`;
            temperature.textContent = `Temperature: ${data.main.temp}°C`;
            description.textContent = `Description: ${data.weather[0].description}`;
            humidity.textContent = `Humidity: ${data.main.humidity}%`;
        }
    </script>
</body>
</html>
