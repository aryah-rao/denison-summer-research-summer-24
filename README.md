# Task Confusion State Data Acquision

## Overview

This repository contains the source code and resources for a research project utilizing Stereolabs AI camera ZED. The project aims to develop a system capable of predicting when a person may require assistance from a robot, focusing on analyzing facial and body movements using computer vision algorithms. 

## Prerequisites

To run the provided script, ensure you have the following dependencies installed:

- Python 3.x
- PyZED SDK: Make sure you have installed the latest version of PyZED by following the installation guide provided by Stereolabs.
- zed-tools: This includes `zed360` for camera calibration.
- Other dependencies specified in `requirements.txt`.

## Setup

### Clone this repository to your local machine:

```bash
git clone https://github.com/aryah-rao/denison-research-summer-24
```

### Install the required dependencies:

Please follow the installation guide provided by Stereolabs to install the latest version of PyZED SDK:
[PyZED SDK Installation Guide](https://www.stereolabs.com/docs/app-development/python/install)

Install OpenCV using your Linux distro's package manager. For Ubuntu/Debian, this is:

```bash
sudo apt install libopencv-dev python3-opencv
```

Install other requirements:

```bash
pip install -r requirements.txt
```

## Usage

### Recording

### 1. Run the Script

Run the `recording.py` script and enter `CONTEXT` to create a unique folder and identiy the experiment.

```bash
python recording.py
```

You will be prompted to enter the context:
```bash
Please enter the context for the experiment: my_experiment
```

### 2. Calibrate Cameras

The script will automatically start the `ZED360` executable for calibration. Ensure the `ZED360` executable is located in the `./zed-tools/` directory. If not, adjust the path accordingly in the script.

Follow the guide [here](https://www.stereolabs.com/docs/fusion/zed360) to complete calibration.

Save the calibration file in the file path `./experiments/DATE/DATE_CONTEXT/`, where `DATE` is the current date and `CONTEXT` is the context you entered for your experiment.

Example structure:
```bash
./experiments/2024-05-21/2024-05-21_my_experiment/calibration.json
```

### 3. Recording and Output

Once calibration is complete, close `ZED360`, and then press any key to start recording. The script will begin capturing body tracking data from the connected ZED cameras.

### 4. Stopping thaudio_recording.wave script:

To stop the script and save the recorded data, press CTRL+C. The script will handle the shutdown process, save the recorded svo2 & wav files, and close all cameras. The script will output:
- One or more .svo files for each camera.
- One .wav file.

All these files will be saved in the same directory as the calibration file.

Example output:

```bash
./experiments/YY-MM-DD/YY-MM-DD_my_experiment/
    calibration.json
    YY-MM-DD_12345_my_experiment.svo
    YY-MM-DD_67890_my_experiment.svo
    audio_recording.wav
```

### Body Tracking

### 5. Run the Script

The body_tracking.py script detects human bodies and visualizes their skeletal models. Here, the localization file is the path to the calibration file that is in the same directory as the svo2 files.

```bash
python body_tracking.py <path_to_localization_file>
```

### 6. End of the Script

The script will save the body tracking data to a JSON file, and close all cameras. The script will output:
- A body_tracking.json file with the recorded body tracking data.

All these files will be saved in the same directory as the calibration file.

Example output:

```bash
./experiments/YY-MM-DD/YY-MM-DD_my_experiment/
    calibration.json
    YY-MM-DD_12345_my_experiment.svo
    YY-MM-DD_67890_my_experiment.svo
    audio_recording.wav
    body_tracking.json
```

### Notes

- Ensure your ZED cameras are properly connected and recognized by the system.
- The script requires the pyzed and cv2 libraries, among others. Make sure you have all dependencies installed.
- The experiments directory will be created if it does not exist.

### Troubleshooting

- If the script cannot find the calibration file, ensure it is saved in the correct directory structure.
- If any errors occur during camera initialization or recording, check the ZED SDK documentation and ensure your cameras are properly set up and connected.

## Contributors

- Matthew Law
- Shaina Khan
- Aryah Rao

## License

This repository is licensed under the [MIT License](LICENSE).
