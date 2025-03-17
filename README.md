# Picoscenes Python Toolbox

The official Python toolbox for parsing **.csi** files from PicoScenes.

## Highlights

- Supports Linux, macOS, and Windows  
- Easy to use  
- Faster parsing than the MATLAB implementation  
- High scalability  
- The official toolbox for parsing **.csi** files  

## Preparation on Windows 10 or 11

1. Install [TDM-GCC-64](https://jmeubank.github.io/tdm-gcc/) (choose the MinGW-w64-based version, version 10.3+).
2. Set the compiler to MinGW64 using [mingw64ccompiler](https://github.com/imba-tjd/mingw64ccompiler):

```bash
pip install git+https://github.com/imba-tjd/mingw64ccompiler
python -m mingw64ccompiler install_specs  # Run once
python -m mingw64ccompiler install        # Works with venv
```

## Installation

1. Clone this repository with the `--recursive` option:

```bash
git clone https://github.com/Herrtian/PicoscenesToolbox.git --recursive
```

2. Install Python and dependencies:

```bash
sudo apt update
sudo apt install python3 python3-pip
```

- If you are a **Chinese** user, you can change the pip source to accelerate the download speed:

```bash
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
```

- Install dependencies:

```bash
pip3 install -r requirements.txt 
```

3. Build the program:

```bash
python3 setup.py build_ext --inplace
```

## Quick Start

A sample binary **.csi** file (**rx_by_usrpN210.csi**) created by **PicoScenes** will be used to generate a chart.

```python
# main.py

from picoscenes import Picoscenes
import numpy as np
import matplotlib.pyplot as plt

i = 0  # Index for the first CSI frame

frames = Picoscenes("rx_by_usrpN210.csi")
numTones = frames.raw[i].get("CSI").get("numTones")
SubcarrierIndex = np.array(frames.raw[i].get("CSI").get("SubcarrierIndex"))
Mag = np.array(frames.raw[i].get("CSI").get("Mag"))[:numTones]

plt.title("Magnitude Demo")
plt.xlabel("Subcarrier Index")
plt.ylabel("Magnitude")
plt.plot(SubcarrierIndex, Mag)
plt.show()
```

The file **main.py** is included in the working directory.

This program reads the first frame of **rx_by_usrpN210.csi** and generates a plot where the x-axis represents the **Subcarrier Index**, and the y-axis represents **Magnitude**.

### Run the script

```bash
python3 main.py
```

If the script runs successfully, you should see an output similar to:

![](docs/Figure_1.png)

## Documentation

For more details about **PicoscenesToolbox**, refer to the **./docs** folder or visit the [wiki]().

## Issues & Feedback

If you encounter any issues or have questions about **PicoscenesToolbox**, please submit an **issue** on GitHub.

Consider giving this project a **star** or **fork** if you find it useful!

## References

- **[PicoScenes](https://ps.zpj.io/)**: A powerful Wi-Fi sensing platform middleware for a wide range of hardware.  
  - This project was released by [Zhiping Jiang](https://zpj.io/bio/).
- [**csiread**](https://github.com/citysu/csiread): A fast channel state information parser for Intel, Atheros, Nexmon, and ESP32 in Python.  
  - This project, developed by [citysu](https://github.com/citysu/csiread), served as inspiration for **PicoscenesToolbox**.

## License

This project is licensed under the **MIT License**. If you use this toolbox in your project, citing this repository would be greatly appreciated.

```
Tian Teng. PicoscenesToolbox: An official tool plugin for parsing **.csi** from PicoScenes in Python. (2021). https://github.com/Herrtian/PicoscenesToolbox.
