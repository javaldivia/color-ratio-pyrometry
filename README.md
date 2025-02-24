# Color Ratio Pyrometry

This repository contains code for color ratio pyrometry, a technique for temperature measurement based on the ratio of emitted radiation in different spectral bands. The repository includes tools for processing RAW images captured using a SONY RX10 IV camera and generating calibration data for ratio pyrometry.

### Features:
1. **RAW to TIFF Conversion**: Code to convert RAW images captured with the SONY RX10 IV camera to TIFF format using DCRAW, enabling further image analysis.
2. **Ratio Pyrometry Calibration**: Tools for generating the calibration curve necessary for color ratio pyrometry, enabling precise temperature measurements based on the emitted radiation in different bands.

### Requirements:
- SONY RX10 IV camera
- DCRAW for RAW image conversion
- Python (with dependencies for image processing and calibration)

### Usage:
Instructions on how to convert RAW images to TIFF and generate calibration data for ratio pyrometry will be provided in the documentation.

## RAW to TIFF Conversion for SONY RX10 IV Images

This repository contains code for converting RAW `.ARW` files from the SONY RX10 IV camera into `.TIFF` format. The code iterates through subdirectories containing temperature folders (e.g., 650, 700, ..., 1200), processes all `.ARW` files, and saves the resulting TIFF files in a corresponding `Results_DCRAW_` folder, organized by temperature folder. Metadata from corresponding `.JPG` files is transferred to the `.TIFF` files, including exposure time, ISO speed ratings, and F-number.

### Code Description

The `RAW_to_TIFF.ipynb` notebook performs the following steps:

1. **Setup and Arguments**:
   - Defines the path to the `dcraw` tool and arguments for conversion.
   - Sets the directory structure for images and results. Creates a results folder named `Results_DCRAW_<today_date>` where `<today_date>` is the current date in the format `MM_DD_YYYY`.

2. **Iterate Through Subdirectories**:
   - Iterates over subdirectories in the `img` folder that are named numerically (e.g., 650, 700, 750).
   - For each subfolder, it processes all `.ARW` files by calling `dcraw` to convert them to `.TIFF`.

3. **Conversion Process**:
   - The code runs `dcraw` with the arguments specified in the `dcraw_args` variable.
   - After conversion, the resulting `.TIFF` files are moved to the appropriate results folder.
   
4. **Metadata Transfer**:
   - If a corresponding `.JPG` file is found for each `.ARW`, the code uses `pyexiv2` to extract metadata (exposure time, ISO, and F-number) from the `.JPG` file and applies it to the `.TIFF` file.

### dcraw Arguments

The following `dcraw_args` are used in the script for conversion:

```python
dcraw_args = " -v -T -4 -q 1"
```

- `-v`: **Verbose output** – Provides detailed output during the conversion process, which can help with debugging and understanding the conversion process.
- `-T`: **Output TIFF format** – Specifies that the output should be in TIFF format (instead of the default PPM format).
- `-4`: **Four-pass conversion** – 16-bit depth – Outputs the image with 16-bit depth for greater precision.
- `-q 1`: **Variable Number of Gradients (VNG) interpolation** – Uses VNG interpolation for better quality when converting RAW to the output format, which helps in reducing artifacts.

### Requirements

- **DCRAW**: Used for converting `.ARW` files to `.TIFF`. 
  - You can find the installation instructions in the [DCRAW GitHub repository](https://github.com/Armando-Mendez/dcraw).
- **Python Libraries**: Make sure you have the necessary libraries installed:
  - `os`
  - `sys`
  - `subprocess`
  - `pyexiv2`
  - `glob`
  - `datetime`

To install the necessary Python libraries, you can run:

```bash
pip install pyexiv2
```

### Version History

- **Version 0.1**: 12/22/2023  
  Initial release.

- **Version 0.2**: 01/05/2023  
  Added background conversion from RAW to TIFF (not always required).

- **Version 0.3**: 02/10/2024  
  - Included `-q 1` in DCRAW arguments for Variable Number of Gradients (VNG) interpolation.
  - Checks only numeric string folders for iteration.
  - Saves the resulting `.tiff` files into a `results_folder`.

## Acknowledgments

This project uses [DCRAW](https://www.dechifro.org/dcraw/) for converting RAW images to TIFF format.
