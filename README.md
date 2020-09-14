# Detection of Cancer Metastases
For a detailed walk through of the project, refer to [ADL Final Presentation](https://github.com/lullaby1024/Detection_of_Cancer_Metastases/blob/master/ADL%20Final%20Project%20Presentation.pdf).

## Goal
- Given a gigapixel pathology image (slide), the goal is to classify if the image contains tumor and localize the tumors for a pathologist’s review.

## Preprocessing
- Data loading
  - Sanity check
    - Number of slides == Number of tumor masks
      - Remedy: drop slide/mask with no match.
      - Total slides: 21
    - Slide dimensions == Tumor mask dimensions
      - Minimum dimensions: 8 (level 0-7)
- Patch extraction
  - Parameters used for sliding-window
    - LEVELS = [3, 4]
    - PATCH_SIZE = 300
    - STRIDE = 128
- Train-test-split
  - Randomly select two slides for testing: ['tumor_075', 'tumor_084']
  - Draw overlapping patches for the training set (stride = 128).
  - Draw non-overlapping patches for the test set (stride = 300).
- Class Imbalance
  - Tumor patches are rare
  - Solution: class weights

## Models
- Single scale, simple CNN
- Single scale, one Inception tower
- Multi-scales, two CNNs

## Conclusion
- The simple CNN has the best performance
  - InceptionV3 is the worst
  - Overfitting (small training set)
- Context patches are not so helpful

## Limitations
- InceptionV3 fine tuning
- Data augmentation
- Larger scales, e.g., level 2
