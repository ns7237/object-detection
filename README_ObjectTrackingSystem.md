
# Object Tracking & Surveillance System (C++ / OpenCV / Qt)

## 🎯 Project Objective

Build a real-time object tracking and surveillance system using **C++**, **OpenCV**, and a **Qt GUI**. The application should detect, classify, and track objects in live or recorded video streams, with alert mechanisms, video recording, and visualization tools. Designed for desktop deployment with minimum 30 FPS performance.

---

## 🧱 Project Structure

```
<Project_Root_Folder>/
├── build/                      # CMake build directory
├── data/                       # Model files
│   ├── yolov4-tiny.weights
│   ├── yolov4-tiny.cfg
│   └── coco.names
├── install/                    # Installed binaries and dependencies
│   ├── bin/
│   │   └── ObjectTrackingApp.exe + DLLs + Qt platform plugins
│   └── data/
├── src/                        # Source files
│   ├── main.cpp
│   ├── MainWindow.h / .cpp
│   ├── VideoProcessor.h / .cpp
├── CMakeLists.txt              # Build configuration
```

---

## ⚙️ Development Setup

- **OS**: Windows
- **Environment**: MSYS2 (mingw64 terminal)
- **Language**: C++17
- **Build Tool**: CMake (MinGW Makefiles)
- **Libraries**:
  - OpenCV 4.11.0 (Core, DNN, Tracking, etc.)
  - Qt5 (Core, Widgets, GUI)
  - Protobuf (for DNN)

### ✅ Install with pacman:
```bash
pacman -S mingw-w64-x86_64-toolchain mingw-w64-x86_64-cmake \
          mingw-w64-x86_64-opencv mingw-w64-x86_64-protobuf \
          mingw-w64-x86_64-qt5-base mingw-w64-x86_64-qt5-svg \
          mingw-w64-x86_64-qt5-tools
```

---

## 🧪 Build & Run Instructions

```bash
# 1. From project root
rm -rf build install
mkdir build && cd build

# 2. Configure with CMake
cmake .. -G "MinGW Makefiles" -DCMAKE_INSTALL_PREFIX=../install

# 3. Build the project
mingw32-make

# 4. Install the project (copies files to install/bin)
mingw32-make install

# 5. Manually copy DLLs to install/bin
cp /mingw64/bin/*.dll ../install/bin/
cp ../install/bin/libprotobuf-lite.dll ../install/bin/libprotobuf-lite320.dll

# 6. Run the app
cd ../install/bin
./ObjectTrackingApp.exe
```

---

## 🧠 Features Implemented

- ✅ Real-time video processing (≥ 30 FPS)
- ✅ Object detection using YOLOv4-tiny
- ✅ Object tracking with MOSSE (via OpenCV Legacy)
- ✅ Re-identification of objects using bounding box IoU
- ✅ GUI (Qt) to load video or start live feed
- ✅ Toggleable overlays (Restricted zone, Trajectory)
- ✅ Alerts for restricted area entry
- ✅ Velocity computation
- ✅ Frame-by-frame display & status updates
- ✅ Video recording with timestamp filename

---

## 📦 Final Working Summary

### `main.cpp`
- Qt app launcher, instantiates `MainWindow`.

### `MainWindow.cpp/h`
- Qt window setup (buttons, layout, labels)
- Signal-slot connections to worker (`VideoProcessor`)
- File dialogs, thread creation & cleanup

### `VideoProcessor.cpp/h`
- Handles YOLO loading, video I/O, detection/tracking loop
- MOSSE-based tracking using `LegacyTrackerWrapper`
- Emit processed frames to UI (`frameProcessed` signal)
- Velocity/trajectory calculations
- Alert logic for restricted zone (speed alert pending)
- Save video via `VideoWriter`

---

## 🛠️ Issues Solved

- Qt5/Qt6 conflicts (solved by pacman-specific versions)
- Missing DLLs in install directory (manual copying)
- C++ errors (`cv::Rect` vs `Rect2d`, namespace issues)
- Replaced slow KCF with fast MOSSE tracker
- Debugged tracker crash via scope and lifecycle control

---

## 🚧 To Do

- ⚠️ **Speed-based alert** (currently placeholder)
- 📈 Review velocity & trajectory logic
- 🔧 Add settings to GUI (thresholds, configs)
- 🔐 Basic security for app (obfuscation, settings access)
- 🧩 Documentation & UML Class Diagram
- 🧪 Add test cases

---

## 👨‍💻 Contributors

- You (and team)
- Built using OpenCV + Qt5 on MSYS2 (MinGW)
