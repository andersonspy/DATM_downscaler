# 🌦️ DATM_downscaler User Manual

**DATM_downscaler** is a statistical downscaling tool developed by Pengyuan Shen at Shenzhen International Graduate School of Tsinghua University. It is designed to generate future weather data in EPW format for building performance simulation. The program uses a distribution mapping approach to downscale Global Climate Model (GCM) projections to local-scale hourly weather data.

## System Requirements

*   **Operating System:** Windows
*   **RAM:** Minimum 8GB
*   **Disk Space:** 8GB free disk space
*   **Python Dependencies:** Packaged within the executable

## Installation

1.  **Download:** Download the `DATM_downscaler.exe` file.
2.  **Create Parent Directory:** Create a parent directory for the program.
3.  **Place Executable:** Place `DATM_downscaler.exe` in the parent directory.
4.  **Create Subdirectories:** Create the required subdirectories as detailed in the [Directory Structure](#directory-structure) section below.

## Directory Structure

The program requires the following directory structure:
```
Parent_Directory/
├── DATM_downscaler.exe
├── Climate/
│ ├── TMYs/ # Store TMY files here
├── SSPs/ # GCM projection data
│ └── [Model_Name (MRI-ESM2-0, users can download other GCMs)]/
│ ├── tas/ # Mean temperature
│ ├── tasmax/ # Maximum temperature
│ ├── tasmin/ # Minimum temperature
│ ├── rsds/ # Solar radiation
│ ├── hurs/ # Relative humidity
│ └── sfcWind/ # Wind speed
└── SM/ # Output directory
```
## Input Data Requirements

### TMY Files

*   **Location:** Place your TMY file(s) in the `Climate/TMYs/` directory.
*   **Format:** Files must be in EPW format.
*   **Filename:** The filename should include the city name (e.g., `"Hong.Kong.epw"`).

### GCM Data Requirements

**Important:** You need to download GCM projection data from external sources. For the default model `MRI-ESM2-0`, you can download the required data from [MRI-ESN2-0 Datasets](https://huggingface.co/datasets/ITOTII/MRI-ESM2-0).

Place the downloaded GCM projection files in the corresponding subdirectories under `SSPs/[MRI-ESM2-0]/`:

*   **Variable Subdirectories:**
    *   `tas`: Mean temperature
    *   `tasmax`: Maximum temperature
    *   `tasmin`: Minimum temperature
    *   `rsds`: Solar radiation
    *   `hurs`: Relative humidity
    *   `sfcWind`: Wind speed
*   **Format:** Each variable should be in NetCDF (`.nc`) format.
*   **Filename:** The filename should include the SSP scenario (e.g., `tas_ssp245.nc`).

## Running the Program

1.  **Open Command Prompt:** Open the command prompt.
2.  **Navigate to Directory:** Navigate to the directory containing `DATM_downscaler.exe` using the `cd` command.
3.  **Run Command:** Execute the program using the following command:
    ```
    DATM_downscaler.exe [city_name]
    ```
    **Example:**
    ```
    DATM_downscaler.exe Hong.Kong
    ```

## Output Files

### Main Outputs

The program generates the following outputs in the `SM/` directory:

1.  **Distribution Parameters:**
    *   `[city]_dist_params.csv`: Contains fitted distribution parameters.
    *   `[city]_best_fit_distributions.png`: Visualization of distribution fitting.

2.  **Future Weather Files:**
    *   **Location:** `SM/[model_name]/[city]/SSP[scenario]/`
    *   **Format:** EPW files for each year (2015-2099).
    *   **Naming Convention:** `[year].epw` (e.g., `2050.epw`)

### Diagnostic Plots

The program also generates diagnostic plots in the `Climate/[model_name]/[city]/` directory:

*   `temperature`: Temperature projections.
*   `ghi`: Solar radiation projections.
*   `wind_speed_month`: Monthly wind speed patterns.
*   `hurs_month`: Monthly relative humidity patterns.

## Troubleshooting

### Common Issues and Solutions

1.  **"File not found" error:**
    *   Verify the TMY file exists in `Climate/TMYs/`.
    *   Check that the city name provided in the command matches the TMY filename.
    *   Ensure all required directories (`Climate`, `SSPs`, `SM`, etc.) exist.
2.  **"Invalid NetCDF file" error:**
    *   Verify that GCM data files are in the correct NetCDF format (`.nc`).
    *   Check if all required variables (`tas`, `tasmax`, `tasmin`, `rsds`, `hurs`, `sfcWind`) are present in the NetCDF file.
    *   Ensure GCM files have the correct naming convention and are placed in the correct directories.
3.  **Memory errors:**
    *   Close other running applications to free up memory.
    *   Ensure your system meets the minimum RAM requirements (8GB).
4.  **Output directory errors:**
    *   Verify that the program has write permissions for the `SM` directory.
    *   Ensure there is sufficient free disk space on the drive where the `SM` directory is located.

## Best Practices

1.  **Consistent Naming:** Use consistent naming conventions for all input files.
2.  **Regular Backups:** Regularly back up TMY and GCM data.
3.  **Disk Space Monitoring:** Monitor disk space usage during processing.
4.  **Output Verification:** Check output EPW files for consistency and accuracy after generation.

## Support

For additional support or bug reports, please contact the development team at [Pengyuan_pub@163.com](mailto:Pengyuan_pub@163.com).
