 

#   Wrong-Way Vehicle Detection

[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![Ultralytics YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange)](https://github.com/ultralytics/ultralytics)

A Python project to detect vehicles going the **wrong way** in traffic videos using **YOLOv8** and a custom tracker. The system marks wrong-way vehicles in the output video, even if vehicles enter mid-frame or the video is partially cut.

---

##   Features

* Detects cars, trucks, and buses using YOLOv8 (`yolov8s.pt`)
* Tracks vehicles with a custom **Tracker** class
* Handles **video cuts** or missed frames using **accumulated motion**
* Marks **wrong-way vehicles in red** in output video
* Counts total wrong-way vehicles dynamically
* Saves **output video** with visual annotations
* Adjustable polygons (`area1`, `area2`) for lane detection

---

##   Installation

1. Clone this repository:

```bash
git clone https://github.com/yourusername/wrong-way-detection.git
cd wrong-way-detection
```

2. Install dependencies:

```bash
pip install ultralytics opencv-python cvzone pandas numpy
```

3. Place your traffic video in the project directory:

```text
wrongway.mp4
```

4. Download YOLOv8 model:

```text
yolov8s.pt
```

5. Ensure you have `coco.txt` for class labels.

---

##   Usage

Run the detection script:

```bash
python detect_wrong_way.py
```

Output video will be saved as:

```text
output_wrongway.mp4
```

---

##   Configuration

* **Lane polygons**: Adjust `area1` and `area2` coordinates to match your lanes:

```python
area1 = [(593,227),(602,279),(785,274),(774,220)]
area2 = [(747,92),(785,208),(823,202),(773,95)]
```

* **Motion threshold**: Adjust sensitivity for fallback detection:

```python
motion_sum[obj_id] < -15
```

* **Frame skipping**: Default skips every other frame for speed:

```python
if count % 2 != 0:
    continue
```

---

##   Output

* Wrong-way vehicles highlighted in **red**
* Normal vehicles highlighted in **purple**
* Total wrong-way vehicle count displayed on top-left

![wrongway.png]  

---

##   How It Works

1. **YOLOv8** detects vehicles in each frame.
2. **Tracker** assigns unique IDs and keeps their center positions.
3. **Motion accumulation** calculates movement direction.
4. **Detection rules**:

   * Vehicle passes `area1` then enters `area2` → marked wrong-way
   * Vehicle enters `area2` moving opposite direction → fallback triggers
5. Annotated frames are written to `output_wrongway.mp4`.

---

##   Future Improvements

* Export CSV with timestamps and violation IDs
* Automatically learn lane direction
* Support multiple lanes and intersections
* Integrate DeepSORT for robust multi-object tracking
* Real-time detection from live camera feed

---

##   License

MIT License — free to use and modify.

---
 
