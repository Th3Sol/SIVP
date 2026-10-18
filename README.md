# SIVP Practicals

## Quick Navigation

- [Experiment 1](#experiment-1)
- [Experiment 2A — Basic Signals](#experiment-2a--basic-signals)
- [Experiment 2B — Exponential, Unit Step and Impulse Signals](#experiment-2b--exponential-unit-step-and-impulse-signals)
- [Experiment 3A — Display and Convert Images](#experiment-3a--display-and-convert-images)
- [Experiment 3B — Colour Mapping](#experiment-3b--colour-mapping)
- [Experiment 4 — Intensity Transformation](#experiment-4--intensity-transformation)
- [Experiment 5 — Gaussian Blur](#experiment-5--gaussian-blur)
- [Experiment 6 — Zooming and Compression](#experiment-6--zooming-and-compression)
- [Experiment 7 — Image Negative](#experiment-7--image-negative)
- [Experiment 8 — Contrast Enhancement and Histogram](#experiment-8--contrast-enhancement-and-histogram)
- [Experiment 9 — Noise Removal](#experiment-9--noise-removal)
- [Experiment 10 — Image Sampling](#experiment-10--image-sampling)
- [Experiment 11 — Pixel Neighbourhoods](#experiment-11--pixel-neighbourhoods)
- [Experiment 12 — Canny Edge Detection](#experiment-12--canny-edge-detection)

---

## Experiment 1

The supplied PDF contains only the heading **“Experiment No: 1”** on its final page; no program or experiment description is provided.

---

## Experiment 2A — Basic Signals

```matlab
clc;
clear all;
close all;

% Time vector
t = 0:0.01:1;

% Frequencies in Hz
f1 = 14;
f2 = 1;

% Sine and cosine waves
sine_wave = sin(2*pi*f1*t);
cosine_wave = cos(2*pi*f2*t);

% Plot the signals
figure;
subplot(3,1,1);
plot(t, sine_wave, 'r');
title('Sine Wave');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3,1,2);
plot(t, cosine_wave, 'y');
title('Cosine Wave');
xlabel('Time (s)');
ylabel('Amplitude');

% Signal addition
added_signal = sine_wave + cosine_wave;

figure;
plot(t, added_signal, 'm');
title('Added Signal (Sine + Cosine)');
xlabel('Time (s)');
ylabel('Amplitude');
```

---

## Experiment 2B — Exponential, Unit Step and Impulse Signals

```matlab
clc;
clear all;
close all;

% Time vectors
t = 0:0.01:5;
n = 0:10;

% 1. Continuous exponential function
et = exp(t);
figure(1);
subplot(2,2,1);
plot(t, et, 'r', 'linewidth', 2);
xlabel('time');
ylabel('exponential function');

% 2. Discrete exponential function
a = 5;
ed = a.^n;
subplot(2,2,2);
stem(n, ed, 'b', 'linewidth', 2);
xlabel('time');
ylabel('exponential function in discrete');

% 3. Continuous unit step function
N = 11;
n1 = 0:1:10;
ut = ones(1, N);
subplot(2,2,3);
plot(n1, ut, 'r', 'linewidth', 2);
xlabel('time');
ylabel('unit step function');

% 4. Discrete unit step function
subplot(2,2,4);
stem(n1, ut, 'b', 'linewidth', 2);
xlabel('time');
ylabel('unit step function');

% 5. Unit impulse function
n2 = 0;
imp = 1;
figure(3);
stem(n2, imp, 'b', 'linewidth', 2);
xlabel('time');
ylabel('unit impulse function');
```

---

## Experiment 2C — Square and Triangle Signals

```matlab
clc;
clear all;
close all;

t = 0:0.1:10;
n = 0:0.5:10;
n1 = 0:1:10;

figure(3);

% Fine time vector for analog wave
t2 = 0:0.01:10;

% 1. Square wave (analog)
sq_analog = sign(sin(2*pi*0.2*t2));
subplot(2,2,1);
plot(t2, sq_analog, 'c', 'LineWidth', 2);
xlabel('Time');
ylabel('Square Wave (Analog)');

% 2. Square pulse (digital)
sq = mod(n1, 2);
subplot(2,2,2);
stem(n1, sq, 'c', 'LineWidth', 2);
xlabel('Time');
ylabel('Square Pulse (Digital)');

% 3. Triangle wave (analog)
tri = [0:5, 4:-1:0];
subplot(2,2,3);
plot(n1, tri, 'c', 'LineWidth', 2);
xlabel('Time');
ylabel('Triangle Wave (Analog)');

% 4. Triangle wave (digital)
subplot(2,2,4);
stem(n1, tri, 'c', 'LineWidth', 2);
xlabel('Time');
ylabel('Triangle Wave (Digital)');
```

---

## Experiment 3A — Display and Convert Images

### 3A(i). Display an image

```matlab
pkg load image;

img = imread('img1.jpg');
imshow(img);
title('Original Image');
```

### 3A(ii). Convert an image to grayscale

```matlab
pkg load image;

img = imread('img1.jpg');

imshow(img);
title('Original Image');

gray_img = rgb2gray(img);

figure;
imshow(gray_img);
title('Grayscale Image');
```

### 3A(iii). Display three images side by side

```matlab
pkg load image;

img1 = imread('img1.jpg');
img2 = imread('img2.jpg');
img3 = imread('img3.jpg');

figure;

subplot(1, 3, 1);
imshow(img1);
title('Image 1');

subplot(1, 3, 2);
imshow(img2);
title('Image 2');

subplot(1, 3, 3);
imshow(img3);
title('Image 3');
```

### 3A(iv). Display three grayscale images side by side

```matlab
pkg load image;

img1 = imread('img1.jpg');
img2 = imread('img2.jpg');
img3 = imread('img3.jpg');

gray1 = rgb2gray(img1);
gray2 = rgb2gray(img2);
gray3 = rgb2gray(img3);

figure;

subplot(1, 3, 1);
imshow(gray1);
title('Grayscale Image 1');

subplot(1, 3, 2);
imshow(gray2);
title('Grayscale Image 2');

subplot(1, 3, 3);
imshow(gray3);
title('Grayscale Image 3');
```

---

## Experiment 3B — Colour Mapping

```matlab
pkg load image;

img = imread('img2.jpg');
figure;

% Original colour image
subplot(2, 2, 1);
imshow(img);
title('Original Color Image');

% Convert to grayscale
gray_img = rgb2gray(img);
subplot(2, 2, 2);
imshow(gray_img);
title('Grayscale Image');

% Re-create a three-channel image from grayscale
color_from_gray = cat(3, gray_img, gray_img, gray_img);
subplot(2, 2, 3);
imshow(color_from_gray);
title('Color Image from Grayscale');

% Apply a colormap to the grayscale image
colormap_img = ind2rgb(gray2ind(gray_img, 256), jet(256));
subplot(2, 2, 4);
imshow(colormap_img);
title('Color Mapped Grayscale Image');
```

---

## Experiment 4 — Intensity Transformation

```matlab
pkg load image;

imagePath = 'img4.jpg';
img = imread(imagePath);

figure;

% Original image
subplot(1, 3, 1);
imshow(img);
title('Original');

% Increase brightness
subplot(1, 3, 2);
imshow(img * 1.5);
title('Intensified');

% Reduce brightness
subplot(1, 3, 3);
imshow(img * 0.5);
title('Deintensified');
```

---

## Experiment 5 — Gaussian Blur

```matlab
pkg load image;

img = imread('img6.jpg');
gray_img = rgb2gray(img);

% Create Gaussian filter: size 10x10, sigma 6
gaussian_filter = fspecial('gaussian', [10 10], 6);

% Apply Gaussian blur
blurred_img = imfilter(gray_img, gaussian_filter, 'symmetric');

% Display images
figure;

subplot(1, 3, 1);
imshow(img);
title('Original Image');

subplot(1, 3, 2);
imshow(gray_img);
title('Original Grayscale Image');

subplot(1, 3, 3);
imshow(blurred_img);
title('Gaussian Blurred Image');
```

---

## Experiment 6 — Zooming and Compression

```matlab
pkg load image;

img = imread('img3.jpg');
figure;

% Original image
subplot(1, 3, 1);
imshow(img);
title('Original');

% Zoomed view
subplot(1, 3, 2);
imshow(img);
xlim([200 300]);
ylim([102 305]);
title('Zoomed [200 300]');

% Resize image to 8% of its original dimensions
compressed_img = imresize(img, 0.08);
subplot(1, 3, 3);
imshow(compressed_img);
title('Compressed (0.08)');
```

---

## Experiment 7 — Image Negative

```matlab
clear;
close all;
clc;

img = imread('img3.jpg');

% Convert to negative
img_negative = 255 - img;

figure;

subplot(1, 2, 1);
imshow(img);
title('Original Image');

subplot(1, 2, 2);
imshow(img_negative);
title('Negative Image');
```

---

## Experiment 8 — Contrast Enhancement and Histogram

```matlab
pkg load image;

img = imread('img3.jpg');

% Convert RGB image to grayscale if required
if size(img, 3) == 3
    gray_img = rgb2gray(img);
else
    gray_img = img;
end

% Create different contrast versions
low_contrast_img = imadjust(gray_img, [0.3, 0.7], []);
high_contrast_img = imadjust(gray_img, [0, 1], []);
equalized_img = histeq(gray_img);

% Display images and histograms
figure;

subplot(3, 4, 1);
imshow(gray_img);
title('Original Image');

subplot(3, 4, 2);
imhist(gray_img);
title('Original Histogram');

subplot(3, 4, 3);
imshow(low_contrast_img);
title('Low Contrast Image');

subplot(3, 4, 4);
imhist(low_contrast_img);
title('Low Contrast Histogram');

subplot(3, 4, 5);
imshow(high_contrast_img);
title('High Contrast Image');

subplot(3, 4, 6);
imhist(high_contrast_img);
title('High Contrast Histogram');

subplot(3, 4, 7);
imshow(equalized_img);
title('Equalized Image');

subplot(3, 4, 8);
imhist(equalized_img);
title('Equalized Histogram');
```

---

## Experiment 9 — Noise Removal

```matlab
pkg load image;

img = imread('img1.jpg');

% Convert RGB image to grayscale if required
if size(img, 3) == 3
    img = rgb2gray(img);
end

% Add salt-and-pepper noise
noisy_img = imnoise(img, 'salt & pepper', 0.02);

% Smooth with a Gaussian filter
sigma = 1;
h = fspecial('gaussian', [3 3], sigma);
smoothed_img = imfilter(noisy_img, h, 'replicate');

% Apply a median filter
filtered_img = medfilt2(smoothed_img, [3 3]);

% Display images
figure;

subplot(2, 2, 1);
imshow(img);
title('Original Image');

subplot(2, 2, 2);
imshow(noisy_img);
title('Image with Salt and Pepper Noise');

subplot(2, 2, 3);
imshow(smoothed_img);
title('Smoothed Image with Gaussian Filter');

subplot(2, 2, 4);
imshow(filtered_img);
title('Image after Median Filtering');
```

---

## Experiment 10 — Image Sampling

### 10(i). Reduce image dimensions to 20%

```matlab
pkg load image;

img = imread('img3.jpg');
gray_img = rgb2gray(img);

[rows, cols] = size(gray_img);

% Downsample to 20% using bilinear interpolation
sampled_img = imresize(gray_img, ...
    [round(rows * 0.2), round(cols * 0.2)], 'bilinear');

figure;

subplot(1, 3, 1);
imshow(img);
title('Image');

subplot(1, 3, 2);
imshow(gray_img);
title('Original Grayscale Image');

subplot(1, 3, 3);
imshow(sampled_img);
title('Sampled Image (20%)');
```

### 10(ii). Reduce image dimensions to 80%

```matlab
pkg load image;

img = imread('image.jpg');
gray_img = rgb2gray(img);

[rows, cols] = size(gray_img);

% Resize to 80% using bilinear interpolation
sampled_img = imresize(gray_img, ...
    [round(rows * 0.8), round(cols * 0.8)], 'bilinear');

figure;

subplot(1, 3, 1);
imshow(img);
title('Image');

subplot(1, 3, 2);
imshow(gray_img);
title('Original Grayscale Image');

subplot(1, 3, 3);
imshow(sampled_img);
title('Sampled Image (80%)');
```

---

## Experiment 11 — Pixel Neighbourhoods

```matlab
% Centre pixel
img = zeros(3, 3);
img(2, 2) = 1;

% Four-neighbourhood
img4 = img;
img4(1, 2) = 0.5;
img4(2, 1) = 0.5;
img4(2, 3) = 0.5;
img4(3, 2) = 0.5;

% Eight-neighbourhood
img8 = img4;
img8(1, 1) = 0.5;
img8(1, 3) = 0.5;
img8(3, 1) = 0.5;
img8(3, 3) = 0.5;

% Diagonal neighbourhood
imgD = img;
imgD(1, 1) = 0.5;
imgD(1, 3) = 0.5;
imgD(3, 1) = 0.5;
imgD(3, 3) = 0.5;

figure;

subplot(1, 3, 1);
imagesc(img4);
axis square;
title('4-Neighbours 0.5');

subplot(1, 3, 2);
imagesc(img8);
axis square;
title('8-Neighbours 0.5');

subplot(1, 3, 3);
imagesc(imgD);
axis square;
title('Diagonal Neighbours 0.5');
```

---

## Experiment 12 — Canny Edge Detection

```matlab
pkg load image;

img = imread('img4.jpg');

% Convert to grayscale
gray_img = rgb2gray(img);

% Apply Canny edge detection
edges = edge(gray_img, 'canny');

% Display original and edge-detected images
figure;

subplot(1, 2, 1);
imshow(img);
title('Original Image');

subplot(1, 2, 2);
imshow(edges);
title('Canny Edge Detection');
```
