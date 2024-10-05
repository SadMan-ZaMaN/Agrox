# Python image processing code that generates a graph  based on plant data

import matplotlib.pyplot as plt
from PIL import Image, ImageDraw, ImageFont
import numpy as np

time_range = np.array([1, 2, 3, 4, 5])  # 5 days or 5 time points
rainfall = np.array([20, 35, 30, 25, 40])  # in mm
temperature = np.array([22, 24, 20, 23, 25])  # in °C
humidity = np.array([75, 80, 70, 72, 85])  # in %

# Step 1: Image Processing (Loading and annotating the image)
def process_plant_image(image_path, text):
    # Load the plant image
    img = Image.open(image_path)
    
    # Create a drawing object
    draw = ImageDraw.Draw(img)
    
    # Optional: Load a font
    # font = ImageFont.truetype("arial.ttf", 24)  # You can specify a font if needed

    
    draw.text((10, 10), text, fill="white")  # Use white color for the text
    
    # Show the image
    img.show()
    
    
    img.save("annotated_plant_image.jpg")
    
# Step 2: Data Visualization (Creating a graph)
def create_graph():
    # Create a figure and axes
    fig, ax1 = plt.subplots()

    # Plot rainfall data on the first axis
    ax1.set_xlabel('Time (days)')
    ax1.set_ylabel('Rainfall (mm)', color='blue')
    ax1.plot(time_range, rainfall, color='blue', marker='o', label="Rainfall")
    ax1.tick_params(axis='y', labelcolor='blue')

    # Create a second axis for temperature and humidity
    ax2 = ax1.twinx()  # Instantiate a second axis sharing the same x-axis
    ax2.set_ylabel('Temperature (°C) and Humidity (%)', color='red')
    ax2.plot(time_range, temperature, color='red', marker='s', label="Temperature")
    ax2.plot(time_range, humidity, color='green', marker='^', label="Humidity")
    ax2.tick_params(axis='y', labelcolor='red')

    # Add legends
    ax1.legend(loc="upper left")
    ax2.legend(loc="upper right")
    
    # Add a title
    plt.title('Plant Environment Data Over Time')

    # Show the plot
    plt.show()


plant_image_path = 'plant.jpg'
process_plant_image(plant_image_path, text="Plant Growth Analysis")


create_graph()

