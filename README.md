# ekstraksi fitur #
# hsv #
```
# Step 1: Upload gambar
from google.colab import files
from PIL import Image
import io
import numpy as np
import matplotlib.pyplot as plt
import cv2

uploaded = files.upload()

# Step 2: Baca gambar
for filename in uploaded.keys():
    image = Image.open(io.BytesIO(uploaded[filename]))
    image_np = np.array(image)

# Step 3: Konversi RGB ke HSV menggunakan OpenCV
hsv_image = cv2.cvtColor(image_np, cv2.COLOR_RGB2HSV)
hue_channel = hsv_image[:, :, 0]

# Step 4: Hitung histogram Hue
hist = cv2.calcHist([hue_channel], [0], None, [180], [0, 180])

# Step 5: Tampilkan gambar asli dan histogram hue dalam satu baris
plt.figure(figsize=(12, 5))

# Gambar asli
plt.subplot(1, 2, 1)
plt.imshow(image_np)
plt.axis('off')
plt.title('Gambar Asli')

# Histogram hue
plt.subplot(1, 2, 2)
plt.plot(hist, color='orange')
plt.title('Histogram Hue')
plt.xlabel('Hue value (0-179)')
plt.ylabel('Jumlah piksel')
plt.grid(True)
plt.tight_layout()
plt.show()
```
