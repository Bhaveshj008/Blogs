---
title: "My First React Mini Project: Weather & Notepad App!"
seoTitle: "React Mini Project: Weather & Notepad App"
seoDescription: "React mini project: Weather & Notepad app with real-time data, responsive UI, interactive charts. Available on GitHub and Vercel!"
datePublished: Fri May 24 2024 19:08:49 GMT+0000 (Coordinated Universal Time)
cuid: clwl224ms000t0aju7kxj3txd
slug: my-first-react-mini-project-weather-notepad-app
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/xkBaqlcqeb4/upload/7c2ca658f9ec2110352ccd447ef324dc.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1716577712616/8f1a60a3-f6bd-4735-9f1b-470ecf6cfd1d.png
tags: programming-blogs, javascript, frontend, technology, web-development, apis, reactjs, frontend-development, material-ui, programming-languages, recharts, api-basics, weatherapp, developer-community, projects-for-portfolio

---

---

I'm thrilled to share my first mini project using React! This application combines real-time weather data with a simple notepad feature. It was a fantastic learning experience, and I'm excited to walk you through it.

## 🔧 Features

### Weather Data Integration

The app fetches weather data using Axios and integrates with the Weatherbit API. It displays:

* Average temperature for the week
    
* Average rainfall for the week
    
* Average humidity for the week
    
* Current temperature
    
* A bar chart showing the temperature for each day of the previous week
    

### Responsive UI

Using Material-UI, I built a clean and responsive interface that adapts well to different screen sizes.

### Interactive Charts

I used Recharts to create a dynamic bar chart that visualizes the weekly temperature data.

### Notepad Functionality

The app includes a notepad where users can:

* Add new notes
    
* Delete existing notes
    

## Project Links

Check out the project on GitHub and see it live on Vercel:

* GitHub: [Weather & Notepad App](https://github.com/Bhaveshj008/whether-notepad-app)
    
* Vercel: [Live demo](https://weather-notepad-app.vercel.app/)
    

## Technologies Used

* **React**: For building the user interface
    
* **Axios**: For making HTTP requests
    
* **Weatherbit API**: For fetching weather data
    
* **Material-UI**: For UI components
    
* **Recharts**: For data visualization
    

## Code Overview

### Fetching Weather Data

Using Axios, I fetch the weather data from the Weatherbit API:

```javascript
useEffect(() => {
  const fetchWeatherData = async () => {
    const API_KEY = 'your_api_key';
    const CITY = 'london';
    const URL = `https://api.weatherbit.io/v2.0/forecast/daily?city=${CITY}&key=${API_KEY}&days=7&units=M`;

    try {
      const response = await axios.get(URL);
      const data = response.data;

      setWeatherData({
        avgTemp: data.data.reduce((acc, day) => acc + day.temp, 0) / data.data.length,
        avgRainfall: data.data.reduce((acc, day) => acc + (day.precip || 0), 0) / data.data.length,
        avgHumidity: data.data.reduce((acc, day) => acc + day.rh, 0) / data.data.length,
        currentTemp: data.data[0].temp,
        weeklyTemp: data.data.map((day, index) => ({
          day: `Day ${index + 1}`,
          temp: day.temp
        }))
      });
    } catch (error) {
      console.error('Error fetching weather data', error);
    }
  };

  fetchWeatherData();
}, []);
```

### UI Components

I used Material-UI for building a responsive and visually appealing interface:

```javascript
<Grid container spacing={2}>
  <Grid item xs={3}>
    <Card className="card animated fadeInLeft">
      <CardContent>
        <Typography variant="h6">Avg Temp of Week</Typography>
        <Typography variant="h4">{weatherData.avgTemp.toFixed(2)}°C</Typography>
      </CardContent>
    </Card>
  </Grid>
  {/* More cards here for Rainfall, Humidity, and Current Temp */}
</Grid>
```

### Notepad Functionality

Users can add and delete notes:

```javascript
const handleDeleteNote = (index) => {
  setNotes(notes.filter((_, i) => i !== index));
};

const handleAddNote = () => {
  if (newNote.trim()) {
    if (newNote.length > 200) {
      alert("Note cannot exceed 200 characters.");
    } else {
      setNotes([...notes, newNote.trim()]);
      setNewNote('');
    }
  } else {
    alert("Note cannot be empty.");
  }
};
```

## Conclusion

Building this Weather & Notepad app has been a great learning experience. I've enhanced my skills in React, API integration, and data visualization. I look forward to building more projects and sharing my journey with you all!

Feel free to check out the code on GitHub and try the live demo on Vercel. Let me know your thoughts and any feedback you might have!

Happy coding! 🚀

#React #WebDevelopment #JavaScript #FirstProject #APIIntegration #MaterialUI #Recharts #Hashnode