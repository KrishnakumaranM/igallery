# Ex.08 Design of Interactive Image Gallery
## Date:21/12/2024

## AIM:
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS:

### Step 1:
Clone the github repository and create Django admin interface.

### Step 2:
Change settings.py file to allow request from all hosts.

### Step 3:
Use CSS for positioning and styling.

### Step 4:
Write JavaScript program for implementing interactivity.

### Step 5:
Validate the HTML and CSS code.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
scripts.js
const initSlider = () => {
    const imageList = document.querySelector(".slider-wrapper .image-list");
    const slideButtons = document.querySelectorAll(".slider-wrapper .slide-button");
    const sliderScrollbar = document.querySelector(".container .slider-scrollbar");
    const scrollbarThumb = sliderScrollbar.querySelector(".scrollbar-thumb");
    const maxScrollLeft = imageList.scrollWidth - imageList.clientWidth;
    
    // Handle scrollbar thumb drag
    scrollbarThumb.addEventListener("mousedown", (e) => {
        const startX = e.clientX;
        const thumbPosition = scrollbarThumb.offsetLeft;
        const maxThumbPosition = sliderScrollbar.getBoundingClientRect().width - scrollbarThumb.offsetWidth;
        
        // Update thumb position on mouse move
        const handleMouseMove = (e) => {
            const deltaX = e.clientX - startX;
            const newThumbPosition = thumbPosition + deltaX;
            // Ensure the scrollbar thumb stays within bounds
            const boundedPosition = Math.max(0, Math.min(maxThumbPosition, newThumbPosition));
            const scrollPosition = (boundedPosition / maxThumbPosition) * maxScrollLeft;
            
            scrollbarThumb.style.left = `${boundedPosition}px`;
            imageList.scrollLeft = scrollPosition;
        }
        // Remove event listeners on mouse up
        const handleMouseUp = () => {
            document.removeEventListener("mousemove", handleMouseMove);
            document.removeEventListener("mouseup", handleMouseUp);
        }
        // Add event listeners for drag interaction
        document.addEventListener("mousemove", handleMouseMove);
        document.addEventListener("mouseup", handleMouseUp);
    });
    // Slide images according to the slide button clicks
    slideButtons.forEach(button => {
        button.addEventListener("click", () => {
            const direction = button.id === "prev-slide" ? -1 : 1;
            const scrollAmount = imageList.clientWidth * direction;
            imageList.scrollBy({ left: scrollAmount, behavior: "smooth" });
        });
    });
     // Show or hide slide buttons based on scroll position
    const handleSlideButtons = () => {
        slideButtons[0].style.display = imageList.scrollLeft <= 0 ? "none" : "flex";
        slideButtons[1].style.display = imageList.scrollLeft >= maxScrollLeft ? "none" : "flex";
    }
    // Update scrollbar thumb position based on image scroll
    const updateScrollThumbPosition = () => {
        const scrollPosition = imageList.scrollLeft;
        const thumbPosition = (scrollPosition / maxScrollLeft) * (sliderScrollbar.clientWidth - scrollbarThumb.offsetWidth);
        scrollbarThumb.style.left = `${thumbPosition}px`;
    }
    // Call these two functions when image list scrolls
    imageList.addEventListener("scroll", () => {
        updateScrollThumbPosition();
        handleSlideButtons();
    });
}
window.addEventListener("resize", initSlider);
window.addEventListener("load", initSlider);
```
```
index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Image Slider in HTML CSS and JavaScript | CodingNepal</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Rounded:opsz,wght,FILL,GRAD@48,400,0,0" />
    <link rel="stylesheet" href="style.css" />
    <script src="script.js" defer></script>
  </head>
  <body>
    <div class="container">
      <div class="slider-wrapper">
        <button id="prev-slide" class="slide-button material-symbols-rounded">
          chevron_left
        </button>
        <ul class="image-list">
          <img class="image-item" src="Thalapathy Vijay.jpg" alt="img-1" />
          <img class="image-item" src="𝐓𝐇𝐄 𝐆𝐎𝐀𝐓.jpg" alt="img-2" />
          <img class="image-item" src="Pikachu.jpg" alt="img-3" />
          <img class="image-item" src="Iron Man Walpaper.jpg" alt="img-4" />
          <img class="image-item" src="Groot 4K Wallpaper_ Guardians of the Galaxy Marvel Fan Art.jpg" alt="img-5" />
          <img class="image-item" src="Captain America.jpg" alt="img-6" />
          <img class="image-item" src="3054337b-2144-4405-a939-c71cac573fc2.jpg" alt="img-7" />
          <img class="image-item" src="4dc24748-b33e-49e2-9b10-e55995238c37.jpg" alt="img-8" />
          <img class="image-item" src="3f0959f1-36ee-4d68-8d3f-954bb912a82a.jpg" alt="img-9" />
          <img class="image-item" src="꒰𝙰𝚒 𝙰𝚛𝚝꒱ Wallpaper.jpg" alt="img-10" />
        </ul>
        <button id="next-slide" class="slide-button material-symbols-rounded">
          chevron_right
        </button>
      </div>
      <footer>
        &copy; 2024 Designed and Developed by M krishna kumaran.
    </footer>
      <div class="slider-scrollbar">
        <div class="scrollbar-track">
          <div class="scrollbar-thumb"></div>
        </div>
      </div>
    </div>
  </body>
</html>
```
```
style.css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: #f1f4fd;
  }
  .container {
    max-width: 1200px;
    width: 95%;
  }
  .slider-wrapper {
    position: relative;
  }
  .slider-wrapper .slide-button {
    position: absolute;
    top: 50%;
    outline: none;
    border: none;
    height: 50px;
    width: 50px;
    z-index: 5;
    color: #fff;
    display: flex;
    cursor: pointer;
    font-size: 2.2rem;
    background: #000;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transform: translateY(-50%);
  }
  .slider-wrapper .slide-button:hover {
    background: #404040;
  }
  .slider-wrapper .slide-button#prev-slide {
    left: -25px;
    display: none;
  }
  .slider-wrapper .slide-button#next-slide {
    right: -25px;
  }
  .slider-wrapper .image-list {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    gap: 18px;
    font-size: 0;
    list-style: none;
    margin-bottom: 30px;
    overflow-x: auto;
    scrollbar-width: none;
  }
  .slider-wrapper .image-list::-webkit-scrollbar {
    display: none;
  }
  .slider-wrapper .image-list .image-item {
    width: 325px;
    height: 400px;
    object-fit: cover;
  }
  .container .slider-scrollbar {
    height: 24px;
    width: 100%;
    display: flex;
    align-items: center;
  }
  .slider-scrollbar .scrollbar-track {
    background: #ccc;
    width: 100%;
    height: 2px;
    display: flex;
    align-items: center;
    border-radius: 4px;
    position: relative;
  }
  .slider-scrollbar:hover .scrollbar-track {
    height: 4px;
  }
  .slider-scrollbar .scrollbar-thumb {
    position: absolute;
    background: #000;
    top: 0;
    bottom: 0;
    width: 50%;
    height: 100%;
    cursor: grab;
    border-radius: inherit;
  }
  .slider-scrollbar .scrollbar-thumb:active {
    cursor: grabbing;
    height: 8px;
    top: -2px;
  }
  .slider-scrollbar .scrollbar-thumb::after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    top: -10px;
    bottom: -10px;
  }
  /* Styles for mobile and tablets */
  @media only screen and (max-width: 1023px) {
    .slider-wrapper .slide-button {
      display: none !important;
    }
    .slider-wrapper .image-list {
      gap: 10px;
      margin-bottom: 15px;
      scroll-snap-type: x mandatory;
    }
    .slider-wrapper .image-list .image-item {
      width: 280px;
      height: 380px;
    }
    .slider-scrollbar .scrollbar-thumb {
      width: 20%;
    }
  }
```

## OUTPUT:
![Screenshot (46)](https://github.com/user-attachments/assets/3717a949-6dce-4efe-a71c-37b2dec58afd)
![Screenshot (47)](https://github.com/user-attachments/assets/ab80f2fb-7cb0-4528-be5d-7e99e1255275)
![Screenshot (48)](https://github.com/user-attachments/assets/67af9165-d8e0-4055-aaa6-3958a103dc73)



## RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
