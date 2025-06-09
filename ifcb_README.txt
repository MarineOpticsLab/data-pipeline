Spring 2025 IFCB processing for GNATS cruises
Farley

We are following Ali Chase's pipeline. Read all about it on GitHub: https://github.com/ifcb-utopia/data-pipeline/blob/main/README.md

The current pipeline is collect data for each station and put the station name in the comments section. Conver to PNGs via the McLane software. Then run Ali Chase's Marimo notebook classifier.

Details:

Run McLane's ROI-PNG (IFCB ROI Viewer v2.2) program to generate all the PNG files. This takes in the ifcb folder (inside the cruise folder) that contains each station's ROI, HDR and ADC files.

Output these PNG files into a new folder 'ml'

The Marimo notebook operates in a Python environment that controls the versions of all the packages to ensure cooperation.
To activate this environment, open an Anaconda prompt and change the directory to the GirHub folder ifcb-pipline (the Marine optics branch).
Then type: conda activate ifcb-utopia
	The (base) prefix will be replaced with (ifcb-utopia) followed by the directory.
Then type: marimo edit
This will open the Marimo notebook editor in your browser. Open the create_cnn_dataset_vFWM.py notebook.
Follow the prompts, pointing to the ml folder with your PNG files in it.
It should generate a list of PNG file paths in the correct format. This can take upwards of 8 minutes. May be a way to speed it up.

When you get to the CNN (convoluted Neural Network) part, give it these paths to the CNN files:
	Z:\fmiller\GitHub - storage\data-pipeline\assets\models\model-cnn-v1-b3.json
	Z:\fmiller\GitHub - storage\data-pipeline\assets\models\model-cnn-v1-b3.h5

	Without the ""!!
	More models are available from Ali on GitHub

Run this by clicking Predict Labels. This can take an hour or two, so go do something else or take a walk.

This gives you a CSV with a path to the PNG file, and 10 columns representing the % confidence that the image is of something in each of 10 categories. 
Another column contains the CNNs best guess as to which category the image fits into. The categories are:

	0 Chloro
	1 Ciliate
	2 Crypto
	3 Diatom
 	4 Dictyo
	5 Dinoflagellate
	6 Eugleno
	7 Other (not sure what this means)
	8 Prymnesio
	9 null (Also not sure what this means)

From there we need to create another script that matches these tags with these categories, and also pairs it all with station metadata. Woof.