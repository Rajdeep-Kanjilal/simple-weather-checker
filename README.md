import requests

def get_weather(city, api_key):
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"

    try:
        response = requests.get(url)
        data = response.json()
        
        if data["cod"] != 200:
            print(f"Error: {data['message']}")
            return

        # Extract weather info
        weather = data['weather'][0]['description']
        temp = data['main']['temp']
        feels_like = data['main']['feels_like']
        humidity = data['main']['humidity']
        wind_speed = data['wind']['speed']

        print(f"\n🌤️ Weather in {city.title()}:")
        print(f"Condition   : {weather}")
        print(f"Temperature : {temp}°C (Feels like {feels_like}°C)")
        print(f"Humidity    : {humidity}%")
        print(f"Wind Speed  : {wind_speed} m/s")

    except Exception as e:
        print("An error occurred:", e)

# Use your API key here
api_key = "edb27490e4d8d07e63e298c432577c8c"
city_name = input("Enter city name: ")
get_weather(city_name, api_key)
