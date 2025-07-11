# 📝 Image Annotation & Dataset Preparation Summary

## 🎯 Goal
Teach a computer to recognize objects (e.g., cat, dog, person) in images using labeled data.

---

## ✅ Step-by-Step Process

1. **Image Annotation**
   - Tool: `LabelMe`
   - Action: Draw boxes/shapes around objects in an image.
   - Save format: `.json` file per image with labels & coordinates.

2. **Create Labels File**
   - `labels.txt` → contains all class names (one per line).

3. **Convert Annotation Format**
   - Required because ML models can't read raw LabelMe `.json` directly.

   ### ➤ VOC Format (for Semantic Segmentation)
   - Use: `python labelme2voc.py data_annotated data_dataset_voc --labels labels.txt`
   - Output: PNG mask images per class (pixel-level)
   - Use Case: Color every pixel based on category (e.g., road, sky, dog)

   ### ➤ COCO Format (for Object Detection / Instance Segmentation)
   - Use: `python labelme2coco.py data_annotated data_dataset_coco --labels labels.txt`
   - Output: Single `.json` for all annotations (bbox, segmentation, category_id)
   - Use Case: Detect/count each object separately (e.g., detect 3 dogs)

---

## 📌 Format Comparison

| Feature                | VOC Format           | COCO Format                      |
|------------------------|----------------------|----------------------------------|
| Type of task           | Semantic Segmentation| Detection / Instance Segmentation|
| Pixel-level labels     | ✅ Yes               | ❌ No                             |
| Counts multiple objects| ❌ No                | ✅ Yes                            |
| File structure         | Mask PNG + images    | All-in-one JSON + images         |

---

## 📥 Input Format Differences

| Format       | Annotation File Type | Image Format     | How Labels Are Stored                        |
|--------------|----------------------|------------------|----------------------------------------------|
| **VOC**      | `.png` (mask images) | `.jpg` / `.png`  | Each **pixel** in PNG = class ID             |
| **COCO**     | `.json`              | `.jpg` / `.png`  | JSON contains bbox, segmentation, labels     |

### Example:
#### VOC:
- `image1.jpg` ← original image  
- `SegmentationClass/image1.png` ← mask image (pixel ID = class)

#### COCO:
- `image1.jpg` ← original image  
- `annotations/instances_train2017.json` ← all label info in JSON

---

## 💡 Tip
👉 Choose only **one format** based on your ML task — **VOC** for pixel labeling, **COCO** for object detection.
