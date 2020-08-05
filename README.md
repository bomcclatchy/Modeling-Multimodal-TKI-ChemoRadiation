# Modeling-Multimodal-TKI-ChemoRadiation
 
Read Me file for the python code accompanying "Modeling Resistance and Recurrence Patterns of Combined Targeted - Chemoradiotherapy Predicts Benefit of Shorter Induction Period" by McClatchy et al.

This code was developed for research purposes by David "Bo" McClatchy, Changran Geng, Clemens Grassberger, and Harald Paganetti. This code is not to be used for clinical use.  

_________Description of Files_________

_FirstCalibrate.ipynb: This script calibrates various model parameters, with most initial parameters values taken from Changran et al. "Prediction of Treatment Response for Combined Chemo- and Radiation Therapy for Non-Small Cell Lung Cancer Patients Using a Bio-Mathematical Model".  Data can be generated and saved in the ModelCalibration folder or data can be loaded from the Paper Calibration folder to recreate the plots in the paper. Note that this script can take very long to re-generate the calibration data (~100hr for n_sample = 1024), but should only be a few minutes to do the analysis and plotting.

_SecondModel.ipynb: This script takes the calibrated model parameters determined in _FirstCalibrate and creates simulated patient populations (e.g. EGFR mutant and WT). Then it runs various multimodal treatment regimens (each treatment regimen is its own function) for each patient and saves the results. Note that this script can take very long to re-generate the model output data for all treatment regimens (~60hr for n_sample = 1024), but the outputs from the manuscript are located in the PaperOutputs folder.

_ThirdPlot.ipynb: This script takes in data generated from _Second Model (either from ModelOutputs or PapersOutputs) and does model validation against literature data (data found in the LiteratureData folder), and also recreates all of the other analyses plots seen in the manuscript.

Dynamic_resistancelib.ipynb: This module contains all of the TKI treatment, growth, and mutation functions, the chemo-radiation functions, and truncated normal and truncate log-normal sampling functions.

_________Other comments_________

- The following python (v3.7) packages are needed to run this code package
	- lifelines v0.24.1 (note: alpha can refer to opacity of plot or 1 minus confidence level)
	- seaborn v0.9.0
	- numpy v1.17.2
	- scipy v1.3.1

- The following scripts used to created and sample truncated normal and truncated log-normal distributions were downloaded from the following repository and are distributed under the GNU LGPL license https://people.sc.fsu.edu/~jburkardt/py_src/py_src.html
	- r8poly_value_horner.ipynb
	- r8_uniform_ab.ipynb
	- normal_01.ipynb
	- normal.ipynb
	- log_normal_truncated_ab.ipynb
	- log_normal.ipynb

- Csv tabulated data in the "Literature Data" folder were acquired using the WebPlotDigitzer V4.2 program (https://automeris.io/WebPlotDigitizer/)

- The function calcHazardRatio(patResA,patResB) in _ThirdPlot.ipynb calculates Hazard Ratios between two treatment arms using the Mantel Haneszel approach described in "Estimation of the Proportional Hazard in "Two-Treatment-Group Clinical Trials" by Bernstein et al. Biometrics 1981 and further described at https://www.graphpad.com/support/faq/hazard-ratio-from-survival-analysis/

- In _FirstCalibrate.ipynb and _ThirdPlot.ipynb, plots seen in the paper can be recreated by loading the PaperCailbration and PaperModel Folders. However, many plots randomly subsample data as described in the paper, and therefore, the plot will be slightly different each time the code is run. 
