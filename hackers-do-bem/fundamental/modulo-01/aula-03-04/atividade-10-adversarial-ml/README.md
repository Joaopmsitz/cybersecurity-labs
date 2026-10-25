# Activity 1.10 — Adversarial Machine Learning

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 03–04  
> **Environment:** Web browser  
> **Status:** Completed

## Objective

Demonstrate the concept of **Adversarial Machine Learning** using an interactive image recognition application.

The activity compares an original image with a version modified by an **adversarial perturbation**, observing how a seemingly small, targeted change can cause a neural network to classify the image differently.

## Environment

- **Platform:** Web browser
- **Application:** Adversarial.js
- **Model:** Traffic sign recognition
- **Dataset:** GTSRB (German Traffic Sign Recognition Benchmark)

## Procedure

### 1. Access the Application

The activity was performed using the following web application:

[Adversarial.js — Interactive Adversarial Machine Learning Demo](https://kennysong.github.io/adversarial.js/)

The application provides an interactive way to explore image classification and demonstrate the effect of adversarial examples on a machine learning model.

### 2. Select the Model

The following model was selected in the application:

```text
GTSRB (street sign recognition)
```

This model is designed to recognize and classify traffic signs.

### 3. Select the Original Image

An image representing a **STOP** traffic sign was selected.

The original image served as the reference for comparing the model's classification before and after generating the adversarial example.

### 4. Classify the Original Image

With the original image selected, the following option was executed:

```text
RUN NEURAL NETWORK
```

The neural network processed the image and produced a classification consistent with the displayed traffic sign, correctly identifying the STOP sign.

### 5. Generate the Adversarial Example

The following option was then selected:

```text
GENERATE
```

The application generated a modified version of the image containing an **adversarial perturbation**.

This perturbation is designed to interfere with the model's classification process while keeping the modified image visually similar to the original.

### 6. Classify the Adversarial Image

After generating the modified image, the following option was executed again:

```text
RUN NEURAL NETWORK
```

This time, the model produced a different classification from the one obtained with the original image.

The network no longer correctly recognized the STOP sign, demonstrating the effect of the adversarial perturbation on the model's output.

### 7. Compare the Results

The activity allowed a direct comparison between the two classification results:

| Input Image | Observed Result |
| --- | --- |
| Original image | Correct classification of the STOP sign |
| Adversarial image | Incorrect classification by the model |

The result demonstrated that a small, targeted modification to an input can alter the output of a machine learning model.

### 8. Finish the Experiment

After comparing the classification results, the activity was completed and the application was closed.

## Commands Used

No terminal commands were required for this activity.

All steps were performed through the web interface:

[https://kennysong.github.io/adversarial.js/](https://kennysong.github.io/adversarial.js/)

## Interpreting the Results

An **adversarial example** is an input intentionally modified to cause a machine learning model to produce an incorrect prediction or classification.

In this experiment, the original STOP sign image was classified correctly. After an adversarial perturbation was generated, the same model produced an incorrect classification.

The key observation is that a model's classification behavior does not always match human visual perception. Specific changes to input data can exploit characteristics learned by the model during training.

This behavior is relevant to the security of systems that depend on machine learning, particularly applications in which automated decisions are based on images or other input data.

The experiment illustrates a potential weakness in model robustness; it does not, by itself, establish how a real-world deployment would behave under the same conditions.

## Result

The activity demonstrated, in a controlled environment, the difference between classifying an original image and classifying an image containing an adversarial perturbation.

The original STOP sign was correctly recognized, while the modified image produced an incorrect classification. This provided a practical demonstration of the **adversarial example** concept and its relationship to machine learning model robustness.

## Concepts Practiced

- Machine Learning
- Artificial Intelligence
- Adversarial Machine Learning
- Adversarial examples
- Adversarial perturbations
- Image classification
- Neural networks
- GTSRB (German Traffic Sign Recognition Benchmark)
- Model robustness
- AI security

## Evidence

The activity evidence is included in the PDF for Classes 03–04.

The relevant screenshots document the original image classification and the classification produced after generating the adversarial example.

[View Evidence — Classes 03–04](../evidencias.pdf)

---

[Back to Classes 03–04](../) · [Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
