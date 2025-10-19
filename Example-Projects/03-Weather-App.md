# Weather App - SwiftUI Example Project

## Project Overview
A weather app that demonstrates API integration, async/await, JSON decoding, and advanced UI components in SwiftUI.

## What You'll Learn
- Async/await in SwiftUI
- Network requests
- JSON decoding
- Error handling
- Loading states
- Custom UI components
- GeometryReader
- Gradients and visual effects

## Complete Code

```swift
import SwiftUI

// MARK: - Data Models
struct WeatherResponse: Codable {
    let name: String
    let main: MainWeather
    let weather: [WeatherCondition]
    let wind: Wind
    let sys: Sys
    
    struct MainWeather: Codable {
        let temp: Double
        let feelsLike: Double
        let humidity: Int
        let pressure: Int
        
        enum CodingKeys: String, CodingKey {
            case temp
            case feelsLike = "feels_like"
            case humidity
            case pressure
        }
    }
    
    struct WeatherCondition: Codable {
        let main: String
        let description: String
        let icon: String
    }
    
    struct Wind: Codable {
        let speed: Double
    }
    
    struct Sys: Codable {
        let country: String
    }
}

// MARK: - Weather Service
class WeatherService {
    // Note: Replace with your actual API key from OpenWeatherMap
    private let apiKey = "YOUR_API_KEY_HERE"
    private let baseURL = "https://api.openweathermap.org/data/2.5/weather"
    
    func fetchWeather(for city: String) async throws -> WeatherResponse {
        let urlString = "\(baseURL)?q=\(city)&appid=\(apiKey)&units=metric"
        
        guard let url = URL(string: urlString) else {
            throw WeatherError.invalidURL
        }
        
        let (data, response) = try await URLSession.shared.data(from: url)
        
        guard let httpResponse = response as? HTTPURLResponse,
              httpResponse.statusCode == 200 else {
            throw WeatherError.invalidResponse
        }
        
        let decoder = JSONDecoder()
        return try decoder.decode(WeatherResponse.self, from: data)
    }
    
    enum WeatherError: LocalizedError {
        case invalidURL
        case invalidResponse
        
        var errorDescription: String? {
            switch self {
            case .invalidURL:
                return "Invalid URL"
            case .invalidResponse:
                return "Invalid server response"
            }
        }
    }
}

// MARK: - ViewModel
@MainActor
class WeatherViewModel: ObservableObject {
    @Published var weather: WeatherResponse?
    @Published var isLoading = false
    @Published var errorMessage: String?
    
    private let weatherService = WeatherService()
    
    func fetchWeather(for city: String) async {
        isLoading = true
        errorMessage = nil
        
        do {
            weather = try await weatherService.fetchWeather(for: city)
        } catch {
            errorMessage = error.localizedDescription
        }
        
        isLoading = false
    }
}

// MARK: - Main View
struct WeatherView: View {
    @StateObject private var viewModel = WeatherViewModel()
    @State private var cityName = "London"
    
    var body: some View {
        ZStack {
            // Background gradient
            LinearGradient(
                gradient: Gradient(colors: [Color.blue, Color.purple]),
                startPoint: .topLeading,
                endPoint: .bottomTrailing
            )
            .ignoresSafeArea()
            
            VStack {
                // Search bar
                searchBar
                
                if viewModel.isLoading {
                    ProgressView()
                        .scaleEffect(2)
                        .tint(.white)
                } else if let errorMessage = viewModel.errorMessage {
                    errorView(message: errorMessage)
                } else if let weather = viewModel.weather {
                    weatherContent(weather: weather)
                } else {
                    welcomeView
                }
                
                Spacer()
            }
            .padding()
        }
        .task {
            await viewModel.fetchWeather(for: cityName)
        }
    }
    
    // MARK: - Subviews
    
    var searchBar: some View {
        HStack {
            TextField("Enter city name", text: $cityName)
                .textFieldStyle(RoundedBorderTextFieldStyle())
            
            Button(action: {
                Task {
                    await viewModel.fetchWeather(for: cityName)
                }
            }) {
                Image(systemName: "magnifyingglass")
                    .foregroundColor(.white)
                    .padding(10)
                    .background(Color.white.opacity(0.3))
                    .clipShape(Circle())
            }
        }
        .padding()
    }
    
    var welcomeView: some View {
        VStack {
            Image(systemName: "cloud.sun.fill")
                .font(.system(size: 100))
                .foregroundColor(.white)
            Text("Search for a city")
                .font(.title)
                .foregroundColor(.white)
        }
    }
    
    func errorView(message: String) -> some View {
        VStack {
            Image(systemName: "exclamationmark.triangle")
                .font(.system(size: 60))
                .foregroundColor(.white)
            Text("Error")
                .font(.title)
                .foregroundColor(.white)
            Text(message)
                .foregroundColor(.white.opacity(0.8))
                .multilineTextAlignment(.center)
        }
    }
    
    func weatherContent(weather: WeatherResponse) -> some View {
        VStack(spacing: 20) {
            // Location
            Text("\(weather.name), \(weather.sys.country)")
                .font(.system(size: 32, weight: .medium))
                .foregroundColor(.white)
            
            // Weather icon
            weatherIcon(for: weather.weather.first?.main ?? "Clear")
            
            // Temperature
            Text("\(Int(weather.main.temp))°C")
                .font(.system(size: 70, weight: .bold))
                .foregroundColor(.white)
            
            // Description
            Text(weather.weather.first?.description.capitalized ?? "")
                .font(.title2)
                .foregroundColor(.white.opacity(0.8))
            
            // Weather details
            HStack(spacing: 40) {
                weatherDetail(
                    icon: "thermometer",
                    title: "Feels Like",
                    value: "\(Int(weather.main.feelsLike))°C"
                )
                
                weatherDetail(
                    icon: "humidity",
                    title: "Humidity",
                    value: "\(weather.main.humidity)%"
                )
                
                weatherDetail(
                    icon: "wind",
                    title: "Wind",
                    value: "\(Int(weather.wind.speed)) km/h"
                )
            }
            .padding()
            .background(Color.white.opacity(0.2))
            .cornerRadius(15)
        }
    }
    
    func weatherIcon(for condition: String) -> some View {
        let iconName: String
        switch condition.lowercased() {
        case "clear":
            iconName = "sun.max.fill"
        case "clouds":
            iconName = "cloud.fill"
        case "rain", "drizzle":
            iconName = "cloud.rain.fill"
        case "snow":
            iconName = "cloud.snow.fill"
        case "thunderstorm":
            iconName = "cloud.bolt.fill"
        default:
            iconName = "cloud.fill"
        }
        
        return Image(systemName: iconName)
            .font(.system(size: 100))
            .foregroundColor(.white)
            .shadow(radius: 10)
    }
    
    func weatherDetail(icon: String, title: String, value: String) -> some View {
        VStack {
            Image(systemName: icon)
                .font(.title2)
            Text(title)
                .font(.caption)
            Text(value)
                .font(.headline)
        }
        .foregroundColor(.white)
    }
}

// MARK: - Preview
struct WeatherView_Previews: PreviewProvider {
    static var previews: some View {
        WeatherView()
    }
}
```

## Setup Instructions

### 1. Get API Key
1. Go to [OpenWeatherMap](https://openweathermap.org/api)
2. Sign up for a free account
3. Get your API key from the dashboard
4. Replace `YOUR_API_KEY_HERE` in the code with your actual API key

### 2. Add Networking Capability
1. In Xcode, select your project
2. Go to "Signing & Capabilities"
3. Ensure "Outgoing Connections (Client)" is enabled

### 3. Update Info.plist
Add the following to allow HTTP requests (if needed):
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

## Features

### Current Features
- **City Search**: Search for any city worldwide
- **Current Weather**: Display temperature, conditions, and description
- **Weather Details**: Shows feels-like temperature, humidity, and wind speed
- **Dynamic Icons**: Weather icons change based on conditions
- **Beautiful UI**: Gradient background with clean design
- **Error Handling**: Graceful error messages
- **Loading States**: Shows progress indicator while fetching

### Weather Icons
- ☀️ Clear skies
- ☁️ Cloudy
- 🌧️ Rain
- ⛈️ Thunderstorm
- ❄️ Snow

## Exercises to Extend This App

1. **Add Forecast**: Show 5-day weather forecast
2. **Add Location**: Use CoreLocation to get user's current location
3. **Add Favorites**: Save favorite cities
4. **Add Units**: Toggle between Celsius and Fahrenheit
5. **Add More Details**: Show sunrise/sunset times, UV index
6. **Add Animations**: Animate weather changes
7. **Add Background**: Change background based on weather conditions
8. **Add Notifications**: Weather alerts and notifications
9. **Add Widget**: Create a widget for home screen
10. **Add Charts**: Show temperature trends

## Key Concepts

### Async/Await
```swift
func fetchWeather(for city: String) async throws -> WeatherResponse {
    let (data, response) = try await URLSession.shared.data(from: url)
    // ...
}
```
Modern Swift concurrency for asynchronous operations.

### Task Modifier
```swift
.task {
    await viewModel.fetchWeather(for: cityName)
}
```
Automatically handles the lifecycle of async operations in views.

### JSON Decoding
```swift
struct WeatherResponse: Codable {
    let name: String
    let main: MainWeather
}
```
Automatic JSON parsing using Codable protocol.

### Custom CodingKeys
```swift
enum CodingKeys: String, CodingKey {
    case feelsLike = "feels_like"
}
```
Maps JSON keys to Swift property names.

### @MainActor
```swift
@MainActor
class WeatherViewModel: ObservableObject {
    // ...
}
```
Ensures UI updates happen on the main thread.

## Architecture

### MVVM + Services
- **Model**: `WeatherResponse` and related structs
- **View**: `WeatherView` and subviews
- **ViewModel**: `WeatherViewModel` manages state
- **Service**: `WeatherService` handles networking

## Common Issues and Solutions

### Issue: "Invalid API key"
**Solution**: Make sure you've replaced `YOUR_API_KEY_HERE` with your actual API key.

### Issue: Network request fails
**Solution**: Check your internet connection and Info.plist settings.

### Issue: City not found
**Solution**: Verify the city name spelling or try a different city.

## Next Steps
After completing this app, try building:
- A news app with API integration
- A cryptocurrency tracker
- A movie database app
- A social media feed
