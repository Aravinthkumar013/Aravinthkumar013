import tensorflow as tf
from tensorflow.keras.models import load_model
from tensorflow.keras.preprocessing import image
import os 
import numpy as np

model = load_model('D:/Josika/GDSC/models/plant_disease_model.h5')

img_size = (224, 224)

def predict_class(image_path):
    img = image.load_img(image_path, target_size=img_size)
    img = image.img_to_array(img)
    img = np.expand_dims(img, axis=0)
    img = img / 255.0
    prediction = model.predict(img)
    predicted_class = np.argmax(prediction)
    return predicted_class

class_names = [
    "Apple Scab",
    "Blue Berry (healthy)",
    "Cherry Powdery Mildew",
    "Corn Common rust",
    "Corn Nortern Leaf Blight",
    "Grape Black Rot",
    "Grape Healthy",
    "Orange Citrus Greening",
    "Peach Bacterial spot",
    "Peach Healthy",
    "Pepper Bell Bacterial spot",
    "Pepper Bell Healthy",
    "Potato Late Blight",
    "Raspberry Healthy",
    "Soybean Healthy",
    "Squash Powdery Mildew",
    "Strawberry Healthy",
    "Strawberry Leaf Scorch",
    "Tomato Leaf Mold",
    "Tomato Mosaic virus",
]

while True:

    image_path = input("Enter the path of the image: ")

    if not os.path.isfile(image_path):
        print("Error: File not found.")
    else:
        predicted_class = predict_class(image_path)
        print(f"Predicted Class Name: {class_names[int(predicted_class)]}")
    ran = input("Do You Want to Continue? (y/n): ").lower().strip()
    if ran == "y":
        continue
    else:
        brea
