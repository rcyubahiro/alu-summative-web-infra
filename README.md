# alu-summative-web-infra   README FILE:
🌍 InfoTrip Navigator
Your command-line companion for smart travel decisions — explore countries with cultural insights, real-time weather, and quality of life data.

✨ Features
🗺️ Country Information
Get details like capital, population, languages, and currency.

🌦️ Current Weather
Displays real-time weather in the capital city.

🌆 Quality of Life Insights
Access city-specific quality of life data including cost of living, safety, healthcare, and more.

🎲 Random Country Generator
Get inspired to travel by discovering a random country and its highlights.

🧩 APIs Used
🌐 REST Countries API
Provides country-related data like capital, currency, population, languages.

☁️ OpenWeatherMap API (Requires API Key)
Provides real-time weather data for cities.

🏙️ Teleport API
Provides quality of life insights for major cities around the world.

⚙️ Installation
Clone the repository

bash
Copy
Edit
git clone https://github.com/your-username/infoTrip-navigator.git
cd infoTrip-navigator
Install Python 3
Make sure you have Python 3 installed. You can download it from python.org.

Install dependencies

bash
Copy
Edit
pip install -r requirements.txt
Make sure to add your OpenWeatherMap API key in the environment or a config file used in the project.

🔑 Setup API Key
To use the weather feature, you must sign up on OpenWeatherMap and obtain an API key.

You can set your key in the environment:

bash
Copy
Edit
export OPENWEATHER_API_KEY='your_api_key_here'
Or place it in a .env file if you're using python-dotenv.

🖥️ Usage
Run the app from the command line:

bash
Copy
Edit
python main.py
You'll be presented with a menu to:

Enter a country name to view insights

Get a random travel recommendation

Exit the app

📌 Example Output
yaml
Copy
Edit
Country: Japan
Capital: Tokyo
Population: 125.8 million
Currency: Japanese Yen (JPY)
Languages: Japanese

Weather in Tokyo: 29°C, Clear Sky

Quality of Life Index in Tokyo:
- Safety: High
- Healthcare: Excellent
- Cost of Living: Moderate
- Commute Time: 35 minutes
📋 Requirements
Python 3.7+

Libraries:

requests

python-dotenv (if using .env files)
