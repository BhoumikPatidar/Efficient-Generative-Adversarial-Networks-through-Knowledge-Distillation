# GAN Knowledge Distillation for MNIST Digit Generation

### Project done as summer research intern at Computer Vision, Imaging and Graphics (CVIG) Lab at IIT Gandhinagar under Prof. Shanmuganathan Raman.

![Knowledge Distillation Visualization](https://github.com/BhoumikPatidar/Efficient-Generative-Adversarial-Networks-through-Knowledge-Distillation/blob/main/knowledge_distillation_visualization.png)



## Problem Statement

Generative Adversarial Networks (GANs) are powerful models for generating realistic data, but they often come with high computational costs and large model sizes. This project addresses the challenge of creating a more efficient GAN model for generating MNIST digits through knowledge distillation without compromising on performance.

## Process

1. **Teacher Model Training**: We first train a full-sized GAN (teacher model) on the MNIST dataset.
2. **Student Model Design**: A smaller, more efficient GAN (student model) is designed with fewer parameters.
3. **Knowledge Distillation**: The student model learns from both the MNIST dataset and the teacher model's intermediate representations.
4. **Evaluation**: We compare the performance of the student model against the teacher model.

## Benefits

- **Reduced Model Size**: The student model has fewer parameters, making it more memory-efficient.
- **Faster Inference**: With a smaller architecture, the student model can generate digits more quickly.
- **Maintained Quality**: Through knowledge distillation, the student model aims to preserve the generation quality of the larger teacher model.
- **Resource Efficiency**: Smaller models are more suitable for deployment on resource-constrained devices.

## Project Structure
## Results

### Teacher Model Generation
![Example Image](https://github.com/BhoumikPatidar/Efficient-Generative-Adversarial-Networks-through-Knowledge-Distillation/blob/main/generated%20images/student_generated.png)

### Student Model Generation
![Example Image](https://github.com/BhoumikPatidar/Efficient-Generative-Adversarial-Networks-through-Knowledge-Distillation/blob/main/generated%20images/teacher_generated.png)
### Model Comparison

| Model   | Parameters | 
|---------|------------|
| Teacher | 1,961,728  | 
| Student | 784,640    |

## Technical Details

### Teacher Model Architecture

The teacher model is a standard DCGAN with the following structure:

- Generator:
- Dense layer (7x7x256)
- 2 Transposed Convolutional layers
- Output shape: 28x28x1

- Discriminator:
- 2 Convolutional layers
- Dense layer for classification

### Student Model Architecture

The student model is a simplified version of the teacher:

- Generator:
- Dense layer (7x7x128)
- 1 Transposed Convolutional layer
- Output shape: 28x28x1

- Discriminator:
- Same as the teacher model

### Knowledge Distillation Process

1. The student generator learns to mimic the teacher's intermediate layer outputs.
2. A combination of adversarial loss and distillation loss is used to train the student.
3. The discriminator is trained on both real MNIST images and the student's generated images.

### Training Loop and Loss Functions

The training process involves two main components: adversarial training and knowledge distillation. Here's an overview of the training loop and the loss functions involved:

#### Loss Functions

1. **Adversarial Loss**: 
- For the generator: Binary cross-entropy between the discriminator's output on generated images and a tensor of ones (fooling the discriminator).
- For the discriminator: Sum of binary cross-entropy between the discriminator's output on real images and a tensor of ones, and the output on generated images and a tensor of zeros.

2. **Distillation Loss**: Mean Squared Error (MSE) between the intermediate layer outputs of the teacher and student generators.

#### Training Loop

For each epoch:
1. Generate noise vectors.
2. Generate images using both teacher and student generators.
3. Get intermediate layer outputs from both generators.
4. Compute discriminator outputs for real and student-generated images.
5. Calculate losses:
- Generator loss = 0.5 * adversarial loss + 0.5 * distillation loss
- Discriminator loss = adversarial loss on real and generated images
6. Compute gradients and update model parameters.

This combined approach allows the student model to learn both from the data distribution (via adversarial training) and from the teacher's learned representations (via distillation).

## Future Work

- Experiment with different architectures for the student model.
- Apply the distillation process to other datasets and GAN applications.
- Investigate the trade-off between model size and generation quality.

## Acknowledgments

- The MNIST dataset providers
- TensorFlow and Keras documentation
- Research papers on GAN compression and knowledge distillation
