# Bienvenidos 



## Introducción

La ciudad de Guayaquil es cuna de muchos lugares y edificios de gran interés e historia, por ello se ha preparado esta aplicación para que nos resulte mucho más sencillo identificar dichos puntos, muchos turistas e incluso personas de la ciudad no conocen o identifican bien estos lugares, esta herramienta puede ser de gran ayuda para esas personas.

## Resumen 

Se ha realizado una aplicación mediante Teachable Machine, con ella podemos identificar algunos de los edificios más emblemáticos de la ciudad de Guayaquil. Para su desarrollo se ha recolectado varias imágenes de muestra que han servido como referencia para que la aplicación pueda identificar estos puntos importantes. Esta aplicación puede llegar a ser muy útil para los turistas u otras personas que están conociendo la ciudad, y quieran identi-ficar ciertos puntos de la misma.

## Desarrollo de la Aplicación

1. **¿Que es teachable Machine?**

Aplicación Web que de una forma rápida y sencilla nos permite crear modelos de aprendizaje automático para nuestros sitios web, aplicaciones y mucho más, sin necesidad de conocimientos especializados ni de programar.

![Interfaz Gráfica](https://storage.googleapis.com/replit/images/1574009876324_2721855c91f32df0231822bf36e84568.png)
`Interfaz Gráfica`

2. **¿Como se realizo la preparacion del modelo?**

Teachable Machine se utiliza para reconocer imágenes, sonidos o posturas. Sube tus propios archivos de imagen o captúralos en vivo con un micrófono o una cámara web , Estos ejemplos permanecen en el dispositivo y nun-ca abandonan tu ordenador a menos que elijas guardar el proyecto en Google Drive.

## Link de la Aplicación 

Visita el modelo directamente desde la apliación de Teachable Machine: _[Edificios Emblemáticos](https://teachablemachine.withgoogle.com/models/8PDaz04GQ/)_

## Markdown

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List
```


# Teachable Machine Image Model

El Modelo consiste en utilizar imagenes para lograr identificar algún edificio emblemático de la ciudad de Guayaquil.

<!--<div> ### Teachable Machine Image Model </div>-->
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@1.3.1/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js"></script>
<script type="text/javascript">
    // More API functions here:
    // https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image

    // the link to your model provided by Teachable Machine export panel
    const URL = "https://teachablemachine.withgoogle.com/models/8PDaz04GQ/";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        // Refer to tmImage.loadFromFiles() in the API to support files from a file picker
        // or files from your local hard drive
        // Note: the pose library adds "tmImage" object to your window (window.tmImage)
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script>







