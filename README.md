# Image-to-SPICE Netlist Generation for Analog Circuits

Course project for Directed Research in AI, Peking University.

This project explores automatic generation of SPICE-style netlists from images of analog circuit diagrams, focusing on circuits extracted from Razavi's analog circuit textbook. It builds on the AMSNet-style template matching and graph traversal pipeline, then adds preprocessing and template-matching improvements for noisier textbook figures.

## Project Summary

The pipeline converts circuit figures into netlists through four main stages:

1. Preprocess circuit images and remove non-topological noise such as text labels, annotations, and dashed guide lines.
2. Detect components, junctions, and special symbols with OpenCV template matching.
3. Traverse wire connections with BFS and assign component pins.
4. Postprocess intersections and equivalent nodes to generate a netlist.

Main improvements implemented in this project include:

- Multi-scale template matching for components whose printed sizes differ slightly from the template library.
- Noise removal before component detection, while preserving isolated symbol parts such as ground symbols, voltage/current sources, and OPAMPs.
- Component-specific matching thresholds for VDD symbols, current arrows, nodes, junctions, and other devices.
- Explicit OPAMP template support and pin ordering.

In the course report, the improved pipeline achieved an average component detection rate of about 70% on printed-book images and about 84% on higher-quality PDF-extracted images.

## Repository Structure

```text
.
|-- README.md
|-- .gitignore
|-- report/
|   |-- main.tex              # LaTeX source of the project report
|   |-- reference.bib
|   |-- template22.sty
|   |-- config.tex
|   |-- figures/
|   `-- main.pdf              # Compiled report, if present locally
`-- 提交/
    |-- Netlist_for_pdf.ipynb # Main notebook for PDF-image netlist generation
    |-- convert_pdf/          # Submitted outputs and intermediate result folders
    `-- 张孟尧-2300011424-唐希源.pdf
```

Large raw data folders, third-party source trees, local model weights, videos, LaTeX build files, and duplicate archives are intentionally excluded by `.gitignore`.

## Environment

The main notebook is Python/Jupyter based. The observed dependencies are:

- Python 3
- Jupyter Notebook or JupyterLab
- NumPy
- OpenCV (`opencv-python`)
- Pillow
- Matplotlib
- SciPy
- natsort
- scikit-learn, for the exploratory clustering notebook if used locally

Example setup:

```bash
pip install notebook numpy opencv-python pillow matplotlib scipy natsort scikit-learn
```

## Usage

Open the main submitted notebook:

```bash
jupyter notebook "提交/Netlist_for_pdf.ipynb"
```

Run the notebook cells in order. The notebook expects the submitted `提交/convert_pdf/` folder structure to be available, including page images, binary images, templates, page data, and generated netlist outputs.

To build the report from source:

```bash
cd report
latexmk -pdf main.tex
```

If `latexmk` is not installed, compile with your preferred LaTeX toolchain.

## Notes

- This is a course project prototype rather than a packaged Python library.
- Some paths inside notebooks may be relative to the project root or to the notebook location; adjust the working directory if running from another folder.
- The ignored raw folders can remain on your machine without being pushed to GitHub.
- No license is declared yet. Add one before public reuse if you want others to copy or modify the code under clear terms.
