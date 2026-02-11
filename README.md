# Teachable_Machine
Supervised Learning
To create a professional GitHub README for your model, you should include an overview of what the model does, how to use it in code, and technical details about the classes it recognizes.

## Proof of Our Model:
Here is the screenshot.

<img width="509" height="691" alt="Screenshot 2026-02-11 112614" src="https://github.com/user-attachments/assets/eea46f38-eb99-49c5-9a3f-27e821115f8d" />
<img width="587" height="740" alt="Screenshot 2026-02-11 112708" src="https://github.com/user-attachments/assets/2d66dba8-7291-4360-8593-a2f08d4e4221" />
<img width="696" height="782" alt="Screenshot 2026-02-11 112731" src="https://github.com/user-attachments/assets/e60b1de3-c61c-442f-bf03-1277afe23262" />


### 💡 Preparation Tip
 I trained AI in three different Classes:
 
 1st Class: Back side of the mobile: Identifies the mobile's back side while showing it in the camera.
 
 2nd class: Copy/notebook: Identifies the copy/notebook while showing it in the camera.
 
 3rd class: Blank: 3rd class for when no objects are present.
 

---
# Tools Used
**Machine Learning**: To gather data and train the AI.
**GitHub:** To host the machine learning document and share this project in the Word file.

# Reflection:
This repository contains a machine learning model trained using [Google's Teachable Machine](https://teachablemachine.withgoogle.com/). This specific model is an **Image Project** that classifies images in real time via a webcam or file uploads.

## 🔗 Model Link

* **Hosted Model:** [https://teachablemachine.withgoogle.com/models/BJSG26qnI/](https://teachablemachine.withgoogle.com/models/BJSG26qnI/)

## 🏷️ Classes

The model is trained to recognize the following categories:

* **[Class 1 Name]** - *Brief description of what this class represents.*
* **[Class 2 Name]** - *Brief description of what this class represents.*
* *(Add more if applicable)*

## 🚀 How to Use

### 1. Web Integration (JavaScript/TensorFlow.js)

You can use this model directly in your web applications. Copy the code below into an `index.html` file to get started:

```html
<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start Webcam</button>
<div id="webcam-container"></div>
<div id="label-container"></div>

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    const URL = "https://teachablemachine.withgoogle.com/models/BJSG26qnI/";

    let model, webcam, labelContainer, maxPredictions;

    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Setup webcam
        const flip = true; 
        webcam = new tmImage.Webcam(200, 200, flip); 
        await webcam.setup(); 
        await webcam.play();
        window.requestAnimationFrame(loop);

        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) {
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); 
        await predict();
        window.requestAnimationFrame(loop);
    }

    async function predict() {
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>

```

### 2. Python Integration (TensorFlow)

If you prefer to use the model locally in Python, download the model from the Teachable Machine dashboard and use the following snippet:

```python
from keras.models import load_model
from PIL import Image, ImageOps
import numpy as np

# Load the model
model = load_model('keras_model.h5')

# Create the array of the right shape to feed into the keras model
data = np.ndarray(shape=(1, 224, 224, 3), dtype=np.float32)
image = Image.open('test_image.jpg')
size = (224, 224)
image = ImageOps.fit(image, size, Image.Resampling.LANCZOS)

image_array = np.asarray(image)
normalized_image_array = (image_array.astype(np.float32) / 127.0) - 1
data[0] = normalized_image_array

# Run inference
prediction = model.predict(data)
print(prediction)

```

## 🛠️ Technical Details

* **Framework:** TensorFlow.js / Keras
* **Input Shape:** 224x224 RGB Images
* **Algorithm:** Transfer Learning (based on MobileNet)

## 📜 License

This project is for educational/demonstration purposes. Feel free to use the code provided by Teachable Machine under their [Terms of Service](https://policies.google.com/terms).
