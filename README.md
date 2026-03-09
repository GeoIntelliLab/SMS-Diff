# 🌍 MMG-5 Dataset & SMS-Diff

**[Your Name]**, **[Co-Author 1]**, **[Co-Author 2]**, **[Co-Author 3]**

> **A globally sampled, strictly aligned multi-modal benchmark integrating LULC, RGB, SWIR, SAR, and DEM data for physics-consistent geospatial reconstruction.**

**MMG-5** represents a significant leap in geospatial data resources, addressing the severe multi-modal data scarcity and inherent modality barriers in the remote sensing domain. It is designed to support the **SMS-Diff** foundation model and other advanced generative frameworks, enabling tasks ranging from heterogeneous image translation to robust downstream anomaly detection (e.g., extreme landslide detection).

---

## 📑 Table of Contents

* [Overview](https://www.google.com/search?q=%23overview)
* [Dataset Features](https://www.google.com/search?q=%23dataset-features)
* [Getting Started](https://www.google.com/search?q=%23getting-started)
* [Usage](https://www.google.com/search?q=%23usage)
* [📖 Extract Semantic Captions](https://www.google.com/search?q=%23-extract-semantic-captions)
* [🖼️ Extract Multi-Modal Images](https://www.google.com/search?q=%23-extract-multi-modal-images)


* [Citation](https://www.google.com/search?q=%23citation)
* [Notes & License](https://www.google.com/search?q=%23notes--license)

---

## 🔭 Overview

**MMG-5** tackles the challenge of capturing the complex multi-modal symbiosis of Earth scenes. Unlike traditional datasets confined to easily accessible optical imagery, this benchmark provides a unified, pixel-wise co-registered view of the Earth's surface through five distinct physical sensors and cartographic representations.

| Modality | Description | Key Features |
| --- | --- | --- |
| 🗺️ **LULC** | Land Use / Land Cover (ESA WorldCover) | Semantic labels, surface type constraints, 10m |
| 📸 **RGB** | Optical Imagery (Sentinel-2 MSI) | Visual texture, color, lithologic contrast |
| 🌈 **SWIR** | Shortwave Infrared (Sentinel-2 Band 12) | Material composition, moisture-influenced surfaces |
| 📡 **SAR** | Synthetic Aperture Radar (Sentinel-1 VV) | Surface roughness, dielectric properties, structural cues |
| ⛰️ **DEM** | Digital Elevation Models (NASA SRTM V3) | Topography, elevation, mesoscale geomorphic gradients |

---

## 🚀 Getting Started

### 1. Install Dependencies

Ensure you have the necessary Python libraries installed for binary parsing and image processing:

```bash
pip install pillow numpy
# 'struct' and 'io' are built-in Python libraries

```

### 2. Prepare Dataset Files

Place the sample binary files in your working directory. These files contain the globally sampled and synchronized multi-modal data:

* `mmg5_captions.bin`: Packaged semantic text descriptions and metadata.
* `mmg5_images.bin`: Packaged multi-modal image tiles.

---

## 💻 Usage

We provide efficient Python scripts to unpack and visualize the binary data.

### 📖 Extract Semantic Captions

Use this script to read the aligned textual descriptions for each modality.

```python
import os
import struct

def unpack_captions(bin_file):
    print(f"🚀 Starting extraction for: {bin_file}")
    try:
        with open(bin_file, 'rb') as f_in:
            # Read total file count
            file_count = struct.unpack('I', f_in.read(4))[0]
            print(f"Found {file_count} caption entries.")
            
            for i in range(file_count):
                # 1. Read filename length & filename
                name_len = struct.unpack('H', f_in.read(2))[0]
                file_name = f_in.read(name_len).decode('utf-8')
                
                # 2. Read encoding info
                enc_len = struct.unpack('B', f_in.read(1))[0]
                encoding = f_in.read(enc_len).decode('ascii')
                
                # 3. Read content length & content
                content_len = struct.unpack('Q', f_in.read(8))[0]
                content = f_in.read(content_len).decode(encoding)
                
                # Display result
                print(f"\n--- Entry {i+1}/{file_count} ---")
                print(f"📄 File: {file_name}")
                print(f"📝 Caption: {content.strip()}")
        
        print("\n✅ Unpacking completed successfully.")
    
    except Exception as e:
        print(f"❌ Unpacking failed: {str(e)}")

if __name__ == '__main__':
    # Replace with your actual bin file path
    unpack_captions('mmg5_captions.bin')

```

### 🖼️ Extract Multi-Modal Images

Use this script to extract and verify the pixel data for LULC, RGB, SWIR, SAR, and DEM images.

```python
import os
import struct
import io
from PIL import Image

def unpack_images(bin_file, sample_size=10):
    print(f"🚀 Starting image extraction for: {bin_file}")
    try:
        with open(bin_file, 'rb') as f_in:
            file_count = struct.unpack('I', f_in.read(4))[0]
            print(f"Found {file_count} image files.")

            for i in range(file_count):
                # 1. Read filename
                name_len = struct.unpack('H', f_in.read(2))[0]
                file_name = f_in.read(name_len).decode('utf-8')
                
                # 2. Read image binary data
                data_len = struct.unpack('Q', f_in.read(8))[0]
                image_data = f_in.read(data_len)
                
                try:
                    # Process image using PIL
                    image = Image.open(io.BytesIO(image_data))
                    width, height = image.size
                    mode = image.mode
                    # Get a sample of pixels
                    pixels = list(image.getdata())
                    
                    print(f"\n--- Image {i+1}/{file_count}: {file_name} ---")
                    print(f"📐 Dimensions: {width}x{height} | 🎨 Mode: {mode}")
                    print(f"📊 Pixel Sample (First {sample_size}): {pixels[:sample_size]}")
                    
                    # Optional: Save image to verify
                    # image.save(f"extracted_{file_name}")

                except Exception as e:
                    print(f"⚠️ Error parsing {file_name}: {str(e)}")
        
        print("\n✅ Image unpacking completed!")
    
    except Exception as e:
        print(f"❌ Critical Error: {str(e)}")

if __name__ == '__main__':
    # Replace with your actual bin file path
    unpack_images('mmg5_images.bin', sample_size=10)

```

---

## 📚 Citation

If you find the **MMG-5** dataset and the **SMS-Diff** framework useful for your research, please consider citing our paper:

```bibtex
@Article{YourName2026,
  author    = {LastName, FirstName and CoAuthor, First and CoAuthor, Second},
  title     = {SMS-Diff: Elevating Geospatial Image Translation to Physics-Consistent Multi-Modal Reconstruction},
  journal   = {ISPRS Journal of Photogrammetry and Remote Sensing}, 
  year      = {2026},
  publisher = {Elsevier}
}

```

---

## ⚠️ Notes & License

* **Sample Data:** The data provided here are merely sample subsets. The complete **MMG-5** dataset will be gradually made public following the acceptance of the associated paper.
* **Copyright:** The data are protected by copyright. Any unauthorized alteration of the images, pixel values, or semantic text content is strictly prohibited.
* **Non-Commercial Use:** This dataset is released exclusively for **academic research and educational purposes**. Commercial use without explicit written authorization is prohibited.

---

*Maintained by the SMS-Diff Research Team.*
