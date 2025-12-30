# VSP5600 Performance Analysis

A Jupyter Notebook for analyzing Hitachi VSP5600 storage performance data. This notebook processes performance export ZIP files and generates visualizations for IOPS, response times, transfer rates, and other key metrics.

## Prerequisites

- Python 3.8 or higher
- Required Python packages:
  - `pandas`
  - `matplotlib`
  - `numpy`

## Data Setup

1. Place your performance data ZIP file (e.g., `out_VSP5600_65535_Performance_Data.20251222.0923.zip`) in the root directory
2. Update the `DATA_FOLDER_NAME` constant in the notebook to match your ZIP file name (without the `.zip` extension)

---

## Running the Notebook

### Option 1: VS Code

1. **Install VS Code** from [https://code.visualstudio.com/](https://code.visualstudio.com/)

2. **Install the Jupyter extension**:
   - Open VS Code
   - Go to Extensions (⌘+Shift+X on Mac, Ctrl+Shift+X on Windows)
   - Search for "Jupyter" and install the Microsoft Jupyter extension

3. **Set up Python environment**:

   ```bash
   # Navigate to the project directory
   cd /path/to/PerformanceExportAnalysis
   
   # Create a virtual environment
   python3 -m venv .venv
   
   # Activate the virtual environment
   # On macOS/Linux:
   source .venv/bin/activate
   # On Windows:
   .venv\Scripts\activate
   
   # Install dependencies
   pip install pandas matplotlib numpy
   ```

4. **Open and run the notebook**:
   - Open VS Code in the project folder: `code .`
   - Open `VSP5600_Performance_Analysis.ipynb`
   - Select the Python interpreter (click on the kernel selector in the top right)
   - Choose the `.venv` environment
   - Run cells using Shift+Enter or click "Run All" in the toolbar

---

### Option 2: Google Colab

1. **Upload to GitHub** (if not already):

   ```bash
   git add .
   git commit -m "Update notebook"
   git push origin main
   ```

2. **Open in Colab**:
   - Go to [https://colab.research.google.com/](https://colab.research.google.com/)
   - Click **File → Open notebook**
   - Select the **GitHub** tab
   - Enter the repository URL: `https://github.com/visubramaniam/PerformanceExportAnalysis`
   - Select `VSP5600_Performance_Analysis.ipynb`

3. **Upload your data**:
   - In Colab, use the file browser (folder icon on the left)
   - Upload your ZIP file to the Colab runtime
   - Update the `ROOT_DIR` path in the constants cell to `/content/`

4. **Run the notebook**:
   - Click **Runtime → Run all** or run cells individually with Shift+Enter

> **Note**: Colab sessions are temporary. Your uploaded data will be lost when the session ends.

---

### Option 3: Jupyter Notebook (Classic)

1. **Install Jupyter**:

   ```bash
   # Create and activate virtual environment (recommended)
   python3 -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   
   # Install Jupyter and dependencies
   pip install jupyter pandas matplotlib numpy
   ```

2. **Start Jupyter Notebook server**:

   ```bash
   cd /path/to/PerformanceExportAnalysis
   jupyter notebook
   ```

3. **Run the notebook**:
   - A browser window will open automatically
   - Click on `VSP5600_Performance_Analysis.ipynb` to open it
   - Run cells using Shift+Enter or **Cell → Run All**

4. **Stop the server**:
   - Press Ctrl+C in the terminal to stop the Jupyter server

---

### Option 4: JupyterLab

1. **Install JupyterLab**:

   ```bash
   # Create and activate virtual environment (recommended)
   python3 -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   
   # Install JupyterLab and dependencies
   pip install jupyterlab pandas matplotlib numpy
   ```

2. **Start JupyterLab**:

   ```bash
   cd /path/to/PerformanceExportAnalysis
   jupyter lab
   ```

3. **Run the notebook**:
   - Navigate to `VSP5600_Performance_Analysis.ipynb` in the file browser
   - Run cells using Shift+Enter or **Run → Run All Cells**

---

### Option 5: Command Line (nbconvert)

Run the notebook non-interactively and generate an HTML report:

1. **Install dependencies**:

   ```bash
   pip install jupyter nbconvert pandas matplotlib numpy
   ```

2. **Execute the notebook**:

   ```bash
   cd /path/to/PerformanceExportAnalysis
   
   # Execute and create a new notebook with outputs
   jupyter nbconvert --to notebook --execute VSP5600_Performance_Analysis.ipynb --output VSP5600_Output.ipynb
   
   # Or execute and convert to HTML
   jupyter nbconvert --to html --execute VSP5600_Performance_Analysis.ipynb
   ```

3. **View results**:
   - Open `VSP5600_Performance_Analysis.html` in a web browser
   - Or open `VSP5600_Output.ipynb` in Jupyter/VS Code

---

### Option 6: Command Line (papermill)

For parameterized execution (useful for batch processing multiple datasets):

1. **Install papermill**:

   ```bash
   pip install papermill pandas matplotlib numpy
   ```

2. **Execute with parameters**:

   ```bash
   papermill VSP5600_Performance_Analysis.ipynb output.ipynb
   ```

---

## Project Structure

```
PerformanceExportAnalysis/
├── VSP5600_Performance_Analysis.ipynb  # Main analysis notebook
├── README.md                            # This file
├── .gitignore                           # Git ignore rules
├── .venv/                               # Python virtual environment (not in git)
├── archive/                             # Archived ZIP files after extraction
├── images/                              # Generated chart images
├── merged/                              # Merged/processed data
└── out_VSP5600_*/                       # Extracted performance data
```

## Configuration

Key constants to modify in the notebook (Cell 2):

| Constant | Description |
|----------|-------------|
| `ROOT_DIR` | Root directory containing the data |
| `DATA_FOLDER_NAME` | Name of the ZIP file (without .zip) |
| `MBPS_THRESHOLD` | MB/s threshold for transfer rate analysis |
| `MIN_IOPS_THRESHOLD` | Minimum IOPS to consider LDEV active |
| `PORT_RESPONSE_THRESHOLD` | Port response time threshold (µs) |
| `LDEV_RESPONSE_THRESHOLD` | LDEV response time threshold (µs) |

## Chart Visualization

The notebook generates 8 main performance charts that are automatically saved to the `images/` folder:

1. **Cache Metrics** - Write Pending Rate vs Cache Usage Rate
2. **MPU Usage** - Processor utilization across MPU groups
3. **HIE Metrics** - HIE ISW vs MPU HIE internal paths
4. **Port Response** - Port response times with latency detection
5. **LDEV IOPS** - Read/Write IOPS for high-activity logical devices
6. **LDEV Transfer Rate** - Data throughput analysis
7. **LDEV Response Time** - Latency analysis vs processor usage
8. **LDEV Read Hit** - Cache hit analysis for read-heavy workloads

Charts are generated with:
- **High DPI output** (150 DPI) for publication quality
- **Proper margins** to ensure all elements including legends are visible
- **Dual-axis plotting** when comparing different metrics
- **Automatic legend placement** to avoid clipping or overlapping elements

---

## PDF Report Generation

After running all visualization cells, a professional PDF report can be generated:

1. **Navigate to Section 7: PDF Report Generation**
2. **Run the PDF generation cell** - This will:
   - Combine all 8 chart images with analysis text
   - Create a formatted title page with report metadata
   - Generate a multi-page PDF report (`VSP5600_Performance_Report_Professional.pdf`)
   - Display status messages showing which charts were included

The generated PDF includes:
- **Page 1**: Title page with report header, date, and system information
- **Pages 2-9**: Eight analysis sections, each with:
  - Chart title and section number
  - Full-resolution chart image
  - Analysis text explaining the metrics and findings

**Note**: The PDF generation requires `reportlab` library. The notebook will automatically install it if not present.

---

## Troubleshooting

### "No ZIP file or data folder found"

- Ensure the ZIP file is in the `ROOT_DIR` directory
- Verify `DATA_FOLDER_NAME` matches your ZIP file name exactly (without `.zip`)

### Import errors

- Make sure you've activated the virtual environment
- Run `pip install pandas matplotlib numpy`

### Kernel not found (VS Code)

- Click on the kernel selector (top right)
- Select "Python Environments" → Choose `.venv`

### Permission denied (macOS/Linux)

- Ensure the virtual environment is activated: `source .venv/bin/activate`

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.

This means you are free to:

- ✅ Use this software for any purpose
- ✅ Study and modify the source code
- ✅ Distribute copies of the original software
- ✅ Distribute your modified versions

Under the following conditions:

- 📋 You must include the original copyright and license notice
- 📋 You must disclose the source code when distributing
- 📋 Modified versions must also be licensed under GPL-3.0
- 📋 Changes made to the code must be documented

See the [LICENSE](LICENSE) file for the full license text.

## Author

Performance Analysis Team
