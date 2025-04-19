# Wheather--App
import React, { useState } from 'react';

const mockWeatherData = {
  "New York": { temperature: "15°C", wind: "10 km/h", sky: "Cloudy" },
  "London": { temperature: "10°C", wind: "12 km/h", sky: "Rainy" },
  "Tokyo": { temperature: "20°C", wind: "8 km/h", sky: "Sunny" },
  "Delhi": { temperature: "30°C", wind: "5 km/h", sky: "Clear" },
};

export default function WeatherApp() {
  const [city, setCity] = useState('');
  const [weather, setWeather] = useState(null);
  const [error, setError] = useState('');

  
  const handleSearch = () => {
    const data = mockWeatherData[city.trim()];
    if (data) {
      setWeather(data);
      setError('');
    } else {
      setWeather(null);
      setError('City not found in our data.');
    }
  };

  
  const handleKeyDown = (e) => {
    if (e.key === 'Enter') handleSearch();
  };

  return (
    <div style={styles.container}>
      <h2 style={styles.heading}>Weather App</h2>

      <input
        type="text"
        placeholder="Enter city name"
        value={city}
        onChange={(e) => setCity(e.target.value)}
        onKeyDown={handleKeyDown}
        style={styles.input}
      />

      <button onClick={handleSearch} style={styles.button}>Search</button>

      {weather && (
        <div style={styles.result}>
          <p><strong>Temperature:</strong> {weather.temperature}</p>
          <p><strong>Wind Speed:</strong> {weather.wind}</p>
          <p><strong>Sky Condition:</strong> {weather.sky}</p>
        </div>
      )}

      {error && <p style={styles.error}>{error}</p>}
    </div>
  );
}


const styles = {
  container: {
    maxWidth: '400px',
    margin: '50px auto',
    padding: '20px',
    textAlign: 'center',
    border: '1px solid #ccc',
    borderRadius: '10px',
    fontFamily: 'Arial, sans-serif',
    backgroundColor: '#f9f9f9',
  },
  heading: {
    marginBottom: '20px',
  },
  input: {
    padding: '10px',
    width: '80%',
    marginBottom: '10px',
    borderRadius: '5px',
    border: '1px solid #ccc',
    fontSize: '16px',
  },
  button: {
    padding: '10px 20px',
    backgroundColor: '#007BFF',
    color: 'white',
    border: 'none',
    borderRadius: '5px',
    cursor: 'pointer',
    marginBottom: '20px',
  },
  result: {
    backgroundColor: '#e6f2ff',
    padding: '15px',
    borderRadius: '8px',
    marginTop: '10px',
  },
  error: {
    color: 'red',
    marginTop: '10px',
  },
};
