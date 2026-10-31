# PCD Assignment 03 - Segmentation and Morphological Processing

This assignment examines how morphological operations affect the results of binary image segmentation. Otsu's method is used to segment cell nuclei in fluorescence microscopy images, followed by erosion, dilation, opening, and closing. The resulting masks are compared with reference masks to evaluate changes in segmentation quality.

The segmentation and morphological algorithms are implemented manually. NumPy is used for array operations, OpenCV for reading images, and Matplotlib and Pandas for displaying the results.

## Dataset

The experiment uses three images from [BBBC008v1](https://bbbc.broadinstitute.org/BBBC008), part of the Broad Bioimage Benchmark Collection. Each image has a corresponding foreground mask used only for evaluation.

The notebook reads the images and masks from these directories:

```text
data/
├── human_ht29_colon_cancer_2_images/
└── human_ht29_colon_cancer_2_foreground/
```

## Method

Otsu's method selects a threshold by maximizing between-class variance. The binary masks are then processed with a 3 × 3 square structuring element using five configurations: erosion, dilation, opening, closing, and opening followed by closing. Each configuration starts from the same thresholded mask, except for the combined sequence.

The outputs are examined visually and evaluated against the reference masks using Intersection over Union (IoU), Dice coefficient, precision, and recall.

## Results

| Method | Mean IoU |
|---|---:|
| Otsu (without morphology) | 0.684 |
| Erosion | 0.395 |
| Dilation | **0.730** |
| Opening | 0.659 |
| Closing | 0.688 |
| Opening + closing | 0.657 |

Dilation produced the highest mean IoU across the three images, increasing recall at the expense of precision. It improved the results for two images but reduced IoU for the first image. Erosion removed too much foreground, while opening and the combined sequence did not improve the average result. These findings are specific to the three images and the 3 × 3 structuring element used in this experiment.

The notebook contains the implementations, image comparisons, per-image scores, and discussion.

## Running the notebook

Install the required packages:

```bash
pip install numpy opencv-python matplotlib pandas notebook
```

Open `PCD_Assignment03.ipynb` in Jupyter Notebook and run the cells in order. Run it from the repository root so the relative paths to `data/` resolve correctly.

## References

- Wahyono. *Segmentation (Thresholding)*, Topic 07, lecture slides.
- Wahyono. *Morphological Processing*, Topic 08, lecture slides.
- Broad Bioimage Benchmark Collection. [BBBC008v1](https://bbbc.broadinstitute.org/BBBC008). Image data and reference masks (CC BY-NC-SA 3.0).
