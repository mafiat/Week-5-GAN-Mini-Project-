# Monet-style Image Generation with CycleGAN

This project, detailed in the `week-5-gan-mini-project - final.ipynb` notebook, implements a CycleGAN (Cycle-Consistent Generative Adversarial Network) to transform real-world photographs into images that mimic the artistic style of Claude Monet. This is a classic example of an image-to-image translation task where the goal is to learn a mapping `G: X -> Y` from a source domain `X` (photos) to a target domain `Y` (Monet paintings), without requiring paired training examples.

## Dataset

The project utilizes the dataset from the Kaggle competition "gan-getting-started". This dataset contains two sets of images:

1.  **Monet Paintings:** A collection of paintings by Claude Monet.
2.  **Photos:** A set of real-world landscape photographs.

The notebook expects the data to be in a directory structure similar to the one provided by the Kaggle competition.

## Model Architecture: CycleGAN

A CycleGAN consists of two main components, duplicated for each translation direction:

1.  **Generators:**
    *   `G_XtoY`: Takes a photograph and attempts to generate a Monet-style painting.
    *   `G_YtoX`: Takes a Monet painting and attempts to generate a realistic photograph.
    The notebook uses a generator architecture based on ResNet blocks.

2.  **Discriminators:**
    *   `D_Y`: Tries to distinguish between real Monet paintings and fake (generated) ones.
    *   `D_X`: Tries to distinguish between real photos and fake (generated) ones.

### Loss Functions

The model is trained using a combination of losses:

*   **Adversarial Loss:** The standard GAN loss where the generator tries to fool the discriminator, and the discriminator tries to correctly classify real and fake images.
*   **Cycle-Consistency Loss:** Ensures that if you translate an image from domain X to Y and back to X, the result should be close to the original image (`X -> G(X) -> F(G(X)) ≈ X`). This preserves the underlying content of the image while changing its style.
*   **Identity Loss:** Encourages the generator to not alter an image that is already in the target domain.

## How to Run

1.  **Environment Setup:**
    *   Ensure you have Python and Jupyter Notebook installed.
    *   Install the required libraries from the notebook. The main dependencies are:
        *   `tensorflow`
        *   `tensorflow_datasets`
        *   `matplotlib`
        *   `keras`

2.  **Dataset:**
    *   Download the `gan-getting-started` dataset from Kaggle.
    *   Update the `ROOT` path in the notebook to point to the dataset directory.

3.  **Execution:**
    *   Open the `week-5-gan-mini-project - final.ipynb` notebook in a Jupyter environment.
    *   Run the cells sequentially to:
        1.  Load and preprocess the data.
        2.  Define and build the CycleGAN model.
        3.  Train the model. The notebook saves model checkpoints during training.
        4.  Evaluate the model by generating Monet-style images from photos.
        5.  Generate a submission file with the translated images.

## Results

The trained model is capable of generating convincing Monet-style paintings from landscape photographs, capturing the characteristic color palette and brush strokes of the artist. The notebook includes visualizations of the input photos and the corresponding generated images.
