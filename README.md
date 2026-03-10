# 🌍 MMG-5 Dataset & SMS-Diff

**Wenzheng Zhang**, **Zhanlong Chen** *(SMS-Diff Research Team)* *China University of Geosciences (Wuhan)*

> **A globally sampled, strictly aligned multi-modal benchmark integrating LULC, RGB, SWIR, SAR, and DEM data for physics-consistent geospatial reconstruction.**

**MMG-5** represents a significant leap in geospatial data resources, addressing the severe multi-modal data scarcity and inherent modality barriers in the remote sensing domain. It is designed to support the **SMS-Diff** foundation model and other advanced generative frameworks, enabling tasks ranging from heterogeneous image translation to robust downstream anomaly detection (e.g., extreme landslide detection).

---

## 📢 Announcement
**The complete dataset, pre-trained models, and source code will be gradually made public according to the team's open-source plan following the acceptance of the associated paper.** Please stay tuned!

## 🔭 Overview
**MMG-5** tackles the challenge of capturing the complex multi-modal symbiosis of Earth scenes. Unlike traditional datasets confined to easily accessible optical imagery, this benchmark provides a unified, pixel-wise co-registered view of the Earth's surface through five distinct physical sensors and cartographic representations.

| Modality | Description | Key Features |
| :--- | :--- | :--- |
| 🗺️ **LULC** | Land Use / Land Cover (ESA WorldCover) | Semantic labels, surface type constraints, 10m |
| 📸 **RGB** | Optical Imagery (Sentinel-2 MSI) | Visual texture, color, lithologic contrast |
| 🌈 **SWIR** | Shortwave Infrared (Sentinel-2 Band 12) | Material composition, moisture-influenced surfaces |
| 📡 **SAR** | Synthetic Aperture Radar (Sentinel-1 VV) | Surface roughness, dielectric properties, structural cues |
| ⛰️ **DEM** | Digital Elevation Models (NASA SRTM V3) | Topography, elevation, mesoscale geomorphic gradients |

## 🗺️ Dataset Visualization
Our dataset features 18 globally distributed representative geological sites, covering extreme and diverse terrain structures to ensure robust physical representation. 

*(Here is the global distribution and multi-modal sample display of the MMG-5 dataset:)*

<img width="2075" height="1456" alt="图2" src="[https://github.com/user-attachments/assets/2ea1f153-cd28-4c27-ad53-361c8c1d11d8](https://github.com/user-attachments/assets/2ea1f153-cd28-4c27-ad53-361c8c1d11d8)" />

## 📚 Citation
If you find the **MMG-5** dataset and the **SMS-Diff** framework useful for your research, please consider citing our paper (Currently under review; detailed citation will be updated upon acceptance):

```bibtex
@Article{Zhang2026SMSDiff,
  author    = {Zhang, Wenzheng and Chen, Zhanlong and others},
  title     = {SMS-Diff: Elevating Geospatial Image Translation to Physics-Consistent Multi-Modal Reconstruction},
  journal   = {Under Review}, 
  year      = {2026}
}
