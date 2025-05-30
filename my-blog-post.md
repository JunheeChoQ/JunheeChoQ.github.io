# Construction of Ion Counting System by Convolutional Neural Network
**Author**: Yongha Shin and Junhee Cho

## Introduction
Ion traps are a promising candidate platform for quantum computing due to their exceptional coherence times, high-fidelity qubit operations, and scalability compared to other quantum computing platforms. To enable their use in quantum computing, real-time tracking of ion positions and counts is critical for precise qubit control and error correction. This work utilizes EMCCD imaging to achieve such tracking, employing multiple convolutional neural network (CNN) models. By comparing the classification results of several popular pre-trained CNN models, we identified the best models for determining ion positions and numbers with high accuracy, advancing ion trap-based quantum computing experiments.

## Ion Trap and Imaging System
The ion trap, depicted in Figure 1(a), employs a quadrupole electrode configuration to provide radial confinement of ions, while static electrodes ensure axial confinement, enabling precise control of individual ions for quantum computing applications. Figure 1(a) illustrates a Linear Paul Trap, where RF and DC electrodes work together to trap ions in a linear arrangement, as shown in Figure 1(b), which displays trapped ions within the trap. The imaging system captures ion fluorescence using a high numerical aperture (NA) lens for efficient light collection and collimation. The collimated fluorescence is then recorded by an EMCCD camera, providing high-sensitivity imaging for real-time analysis of ion positions and counts.

## Motivation
Conventional ion tracking systems rely on contour Gaussian fitting to localize individual ions, a computationally intensive method that hinders real-time tracking. Moreover, this approach is highly susceptible to background noise, often resulting in inaccurate fitting and unreliable ion detection. To address these limitations, we propose a novel ion tracking system leveraging convolutional neural network (CNN) models, enabling robust and efficient real-time ion localization even in noisy environments.

## Methods
### Image generation.
* EMCCD images of 1D and 2D ion crystals were generated.
* Number of trapped ions ranging from 3 to 49
### Setup.
* Dataset: EMCCD image with different size (500, 1000, 2000, 4526)
* Backbone: ResNet
* CNN Models: Retinanet, Faster R-CNN
* Accuracy: mean average precision (mAP)

## Results
Each dataset, with sizes of 450, 900, 1800, and 4074 EMCCD images, was used to train the CNN models—RetinaNet, Faster R-CNN, and MnasNet—to predict the positions and counts of ions in real-time. The Faster R-CNN model was employed to generate the predictions visualized in Figure 2, where red dots represent predicted ion positions and green dots indicate the ground truth. Figure 2 demonstrates that prediction accuracy improves significantly as dataset size increases, with the largest dataset (4074 samples) achieving the closest alignment between predicted and true positions compared to the smallest dataset (450 samples).

The largest dataset of 4000 samples was used to train Faster R-CNN and RetinaNet, with a batch size of 32 and 100 epochs, during which the training loss and validation accuracy (mAP) were measured at each epoch to evaluate model performance. These results are presented in Figure 3, which comprises two graphs: one illustrating the training loss trends and the other showing the validation accuracy trends for Faster R-CNN and RetinaNet over the 100 epochs. As the epochs increase, the training loss consistently decreases while the validation accuracy improves, reflecting effective model optimization over time.

To compare model performance, a bar graph of mAP accuracy for Faster R-CNN and RetinaNet across training dataset sizes of 500, 1000, 2000, and 4000 samples is presented in Figure 4. Both models exhibit increasing accuracy with larger datasets; however, at 4000 samples, Faster R-CNN achieves a significantly higher mAP of 96.81%, while RetinaNet reaches 54.42%. This substantial gap is attributed to Faster R-CNN's two-stage architecture, which enhances feature extraction and region proposal accuracy, making it more effective at handling complex ion patterns in larger datasets compared to RetinaNet's single-stage approach.
