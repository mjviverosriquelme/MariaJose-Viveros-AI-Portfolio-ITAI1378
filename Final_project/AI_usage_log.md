# AI Usage Log – Data Clocking Experiment B

This document records how I used AI tools while developing and refining the **Data Clocking Prediction** experiment for the binary classification task (`form` vs `No_form`) using TensorFlow and Keras.

---

## Entry 1 – Using AI to set up the unzip process and folder structure

- **Goal:** Prepare the CDT clock dataset in a clean and reproducible way.
- **AI tool used:** ChatGPT.
- **How I used it:** I asked for help to write Python code that:
  - Unzips the file `CDT_Clock_JPG.zip` into a folder (e.g., `unzipped_data`).
  - Generates an absolute path `UNZIP_DIR`.
  - Prints a confirmation message so I can quickly see where the data was extracted.
- **Concrete example:** The AI suggested a block using `zipfile.ZipFile`, `os.makedirs`, and `extractall()` to automate the process instead of unzipping manually in the UI.
- **Human oversight:** I verified that the unzipped folders matched the expected structure and that the images were actually readable.

---

## Entry 2 – Verifying directory structure and file extensions with AI support

- **Goal:** Confirm that the dataset contained the correct subfolders (`form` and `No_form`) and valid image formats before training.
- **AI tool used:** ChatGPT.
- **How I used it:** I requested code to:
  - Check if the main directory exists.
  - Assert that `form` and `No_form` subdirectories are present.
  - List and compare file extensions in each class folder to detect possible issues (for example, unexpected formats).
- **Concrete example:** The AI generated loops with `os.listdir()` and `os.path.splitext()` to collect extensions in sets and print them, so I could visually inspect the results.
- **Human oversight:** I reviewed the printed extensions and cleaned any problematic files if necessary.

---

## Entry 3 – Building the TensorFlow input pipeline and basic CNN architecture

- **Goal:** Create a robust TensorFlow pipeline for loading images and design a CNN model appropriate for the `form` vs `No_form` classification.
- **AI tool used:** ChatGPT.
- **How I used it:** I asked for:
  - A template using `image_dataset_from_directory()` with train/validation/test splits.
  - Image resizing parameters and batch size suggestions.
  - A baseline CNN model using `Conv2D`, `MaxPooling2D`, `Dropout`, and `Dense` layers for binary classification.
- **Concrete example:** The AI proposed a model that outputs a single neuron with a sigmoid activation for the binary target, and recommended using `binary_crossentropy` as the loss function.
- **Human oversight:** I adjusted hyperparameters such as image size, batch size, and number of filters according to the dataset size and the GPU limits.

---

## Entry 4 – Using AI to configure callbacks and reduce overfitting

- **Goal:** Monitor training and avoid overfitting between training and validation sets.
- **AI tool used:** ChatGPT.
- **How I used it:** I requested code snippets for:
  - `EarlyStopping` based on `val_loss` with a patience value.
  - `ModelCheckpoint` to save the best model during training.
  - Optionally `ReduceLROnPlateau` to decrease the learning rate when validation performance stopped improving.
- **Concrete example:** The AI helped me define a `callbacks` list that I could pass directly into `model.fit()`, including a checkpoint path like `"best_model.keras"` for the best-performing weights.
- **Human oversight:** I interpreted the training and validation curves afterwards to confirm that the callbacks actually stabilized the model instead of just shortening training.

---

## Entry 5 – Plotting training vs validation curves with AI-generated code

- **Goal:** Visualize whether the model was learning correctly and whether there were signs of overfitting.
- **AI tool used:** ChatGPT.
- **How I used it:** I asked for plotting code that:
  - Uses the `history` object from `model.fit()` to extract `accuracy`, `val_accuracy`, `loss`, and `val_loss`.
  - Plots the curves in a clear figure with labels and a title.
- **Concrete example:** The AI provided a function using `matplotlib` to draw two subplots, one for accuracy and one for loss, so I could compare train and validation trends epoch by epoch.
- **Human oversight:** I interpreted the plots, confirming that the training and validation accuracy were close and that there was no strong divergence in loss, which indicated that overfitting was under control.

---

## Entry 6 – Generating a prediction visualization function with AI help

- **Goal:** Inspect individual test images and see how the model classified them, especially in ambiguous or irregular cases.
- **AI tool used:** ChatGPT.
- **How I used it:** I requested a function that:
  - Samples random images from the test set.
  - Displays each image with the true label, the predicted label, and the confidence score.
- **Concrete example:** The AI suggested using `plt.subplot()` to show multiple images in a grid and overlaying the predicted class and probability in the title of each image.
- **Human oversight:** I manually reviewed cases where the model struggled (for example, clocks that were incomplete or messy) to understand the limitations of the classifier.

---

## Entry 7 – Computing the confusion matrix and classification report with AI assistance

- **Goal:** Evaluate the model beyond simple accuracy and get a clearer view of performance on each class (`form` vs `No_form`).
- **AI tool used:** ChatGPT.
- **How I used it:** I asked for code to:
  - Convert model predictions into class labels.
  - Compute the confusion matrix using `sklearn.metrics.confusion_matrix`.
  - Plot the confusion matrix with `seaborn.heatmap`.
  - Generate a classification report (`precision`, `recall`, `f1-score`) using `classification_report`.
- **Concrete example:** The AI provided a template that sets `CLASS_NAMES` as tick labels on the heatmap and prints the full classification report after the plot.
- **Human oversight:** I interpreted the confusion matrix to see whether one class was favored over the other and used the `f1-score` to judge the overall balance of the model.

---

## Entry 8 – Interpreting final metrics with AI-guided reflection

- **Goal:** Understand what an accuracy around ~0.93 and a similar F1-score mean in the context of this specific binary classification task.
- **AI tool used:** ChatGPT.
- **How I used it:** I asked for help interpreting:
  - The meaning of accuracy, precision, recall, and F1-score in a medical/clinical-inspired context (cognitive impairment screening).
  - Whether the balance between the classes was acceptable for this use case.
- **Concrete example:** The AI explained that a high F1-score (~0.93) suggests a strong balance between precision and recall, which is especially important when misclassifying “not formed” drawings could have practical consequences in a screening scenario.
- **Human oversight:** I connected these metrics with the research context and considered how future work might address potential biases or edge cases.

---

## Summary of AI usage

Across this experiment, AI tools were used primarily for:
- Generating boilerplate and utility code (data loading, plotting, metrics).
- Suggesting model architectures and training strategies.
- Supporting interpretation of results and metrics.

In all cases, I kept **human oversight** over the code and the decisions, reviewing outputs, adjusting parameters, and interpreting the results in the context of my own learning process and research goals.

