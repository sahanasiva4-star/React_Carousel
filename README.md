# Ex05 Image Carousel
## Date:25.05.2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
~~~
# main.jsx:
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./App.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
~~~
~~~
# app.jsx:
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  const images = [
    "https://picsum.photos/id/1015/900/500",
    "https://picsum.photos/id/1018/900/500",
    "https://picsum.photos/id/1025/900/500",
    "https://picsum.photos/id/1035/900/500",
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextSlide = () => {
    setCurrentIndex((prev) =>
      prev === images.length - 1 ? 0 : prev + 1
    );
  };

  const prevSlide = () => {
    setCurrentIndex((prev) =>
      prev === 0 ? images.length - 1 : prev - 1
    );
  };

  useEffect(() => {
    const interval = setInterval(nextSlide, 3000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div className="container">
      <h1>React Image Carousel</h1>

      <div className="carousel">
        <img
          src={images[currentIndex]}
          alt="carousel"
          className="slide"
        />

        <button className="prev" onClick={prevSlide}>
          ❮
        </button>

        <button className="next" onClick={nextSlide}>
          ❯
        </button>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={
              currentIndex === index ? "dot active" : "dot"
            }
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
}

export default App;
~~~
~~~
# app.css:
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body {
  background: linear-gradient(135deg, #0f172a, #1e293b);
  min-height: 100vh;
}

.container {
  text-align: center;
  padding: 40px 20px;
}

.container h1 {
  color: white;
  margin-bottom: 25px;
}

.carousel {
  position: relative;
  max-width: 900px;
  margin: auto;
  overflow: hidden;
  border-radius: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
}

.slide {
  width: 100%;
  height: 500px;
  object-fit: cover;
  display: block;
}

.prev,
.next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border: none;
  padding: 15px;
  font-size: 24px;
  cursor: pointer;
  border-radius: 50%;
  color: white;
  background: rgba(0, 0, 0, 0.5);
  transition: 0.3s;
}

.prev:hover,
.next:hover {
  background: rgba(0, 0, 0, 0.8);
}

.prev {
  left: 15px;
}

.next {
  right: 15px;
}

.dots {
  margin-top: 20px;
}

.dot {
  display: inline-block;
  width: 14px;
  height: 14px;
  margin: 0 6px;
  border-radius: 50%;
  background: #94a3b8;
  cursor: pointer;
  transition: 0.3s;
}

.dot.active {
  background: white;
  transform: scale(1.2);
}

@media (max-width: 768px) {
  .slide {
    height: 300px;
  }

  .prev,
  .next {
    padding: 10px;
    font-size: 18px;
  }
}
~~~

## OUTPUT
<img width="1029" height="569" alt="{FAC89FEE-E8D1-406D-BF4C-0F36D015296D}" src="https://github.com/user-attachments/assets/08d5c5df-4e88-4c5f-806a-69394de34eea" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
