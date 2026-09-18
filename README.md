# MNIST CNN Error Analysis

## Project Overview

This project investigates not only how accurately a convolutional neural network (CNN) can classify handwritten digits, but also where it makes mistakes.

The main question is:

**Where does the CNN make its mistakes, and does one controlled change to the model change those mistakes?**

The project uses the MNIST dataset and compares a baseline CNN with a slightly deeper CNN.

---

## Dataset

The MNIST dataset contains 70,000 grayscale images of handwritten digits from 0 to 9.

Each image has a resolution of:

- 28 × 28 pixels
- 1 grayscale channel

The dataset was downloaded from OpenML.

The pixel values were normalised from the range 0–255 to 0–1.

The data was split into:

- 80% training data
- 20% test data

A stratified split was used to preserve the class distribution.

---

## Baseline CNN

The baseline model contains:

- Conv2D layer with 32 filters
- MaxPooling2D layer
- Dropout layer with rate 0.3
- Flatten layer
- Dense layer with 64 units
- Softmax output layer with 10 units

The model was trained using:

- Adam optimiser
- Sparse categorical crossentropy loss
- Accuracy as the evaluation metric
- Batch size of 128
- Up to 15 epochs
- Early stopping based on validation loss

---

## Model Modification

For the second experiment, one controlled change was made to the baseline model.

A second convolutional block was added:

- Conv2D layer with 64 filters
- MaxPooling2D layer

All other training settings were kept the same so that the comparison between the two models remained fair.

---

## Results

| Model | Test Accuracy |
|---|---:|
| Baseline CNN | 98.59% |
| Deeper CNN | 98.84% |

The deeper model improved overall test accuracy by **0.25 percentage points**.

### Error Analysis

The two most common confusion pairs in the baseline CNN were:

- 4 predicted as 9: 12 errors
- 9 predicted as 7: 12 errors

After adding the second convolutional block:

| Confusion pair | Baseline | Deeper CNN |
|---|---:|---:|
| 4 → 9 | 12 | 28 |
| 9 → 7 | 12 | 3 |

The deeper network therefore changed the pattern of mistakes rather than reducing all of them.

The number of 9 → 7 errors decreased substantially, while the number of 4 → 9 errors increased.

---

## Interpretation

The baseline CNN already achieved very high accuracy.

The deeper CNN produced a small improvement in overall accuracy, but the confusion matrix showed that this improvement was not uniform across all digit pairs.

This demonstrates why overall accuracy alone is not enough to fully evaluate a classifier. Error analysis can reveal important changes in model behaviour that are hidden by a single accuracy score.

---

## Ethical Considerations

Handwriting styles can vary with factors such as age, country, and education. Some handwriting styles may therefore be under-represented in the training data and classified less reliably.

In a real automated system, a confident but incorrect prediction could send a letter to the wrong destination or cause an account number to be read incorrectly. High-risk or uncertain predictions should therefore be checked rather than accepted automatically.

---

## Reflection

The baseline CNN performed very well, which made further improvement difficult.

One of the most useful parts of the project was analysing the confusion matrices rather than relying only on test accuracy. The deeper model improved the overall accuracy and strongly reduced one important error pattern, but it also increased another one.

With more time, I would test the models across multiple training runs and compare the average results in order to determine whether the small accuracy difference is consistent. I would also investigate additional controlled changes, such as stronger regularisation or data augmentation.

---

## Repository Contents

- `Final_Project_Option1_CNN_MNIST.ipynb` — completed notebook with all code, outputs, confusion matrices, and written interpretations
- `Final_Project_Option1_CNN_MNIST.html` — static HTML export of the completed notebook with saved outputs
- `README.md` — summary of the project and main results

---

## How to Run

1. Open `Final_Project_Option1_CNN_MNIST.ipynb` in Google Colab or Jupyter Notebook.
2. Run the notebook from top to bottom.
3. An internet connection is required the first time the MNIST dataset is downloaded from OpenML.

---

## Conclusion

The baseline CNN achieved **98.59% test accuracy**, while the deeper CNN achieved **98.84%**.

Although the deeper network slightly improved overall accuracy, it did not reduce every type of error. The 9 → 7 confusion decreased from 12 to 3, while the 4 → 9 confusion increased from 12 to 28.

The experiment shows that a model can improve in overall accuracy while still becoming worse on specific kinds of mistakes.
