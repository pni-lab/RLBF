Towards generative AI-based fMRI paradigms: reinforcement learning via real-time brain feedback
========

Giuseppe Gallitto<sup>1,2</sup>, Robert Englert<sup>2,3</sup>, Balint Kincses<sup>1,2</sup>, Raviteja Kotikalapudi<sup>1,2</sup>, Jialin Li<sup>1,2,4</sup>, Kevin Hoffschlag<sup>1,2</sup>, Sulin Ali<sup>1,2</sup>, Ulrike Bingel<sup>1,2</sup>, Tamas Spisak<sup>2,3</sup><br>

<sup>1</sup> Department of Neurology, University Medicine Essen, Germany<br>
<sup>2</sup> Center for Translational Neuro- and Behavioral Sciences (C-TNBS), University Medicine Essen, Germany<br>
<sup>3</sup> Department of Diagnostic and Interventional Radiology and Neuroradiology, University Medicine Essen, Germany<br>
<sup>4</sup> Max Planck School of Cognition, Leipzig, Germany<br>

### Software
**N.B.** Our real-time fMRI software is still in an early stage of development, and it is not suitable for general use.
The current version has been tested on one single scanner **and works only** with a very specific setup.

<b> ** Tested with Siemens Magnetom Vida 3T **</b>

### Features
The current version of the program consists in:

- A controller that manages incoming volumes from Siemens' real-time export function.
It handles preprocessing and reinforcement learning with a minimum TR of 1 sec.
- A custom RL environment made in [Raylib 5.0](https://www.raylib.com/) with a flickering
checkerboard that changes in contrast and frequency.
- A custom RL Soft-Q-Learning algorithm based on the work of 
[Haarnoja et al., 2017](https://proceedings.mlr.press/v70/haarnoja17a.html?ref=https://githubhelp.com).
- A Dashboard made in [Streamlit](https://streamlit.io/), to visualize the progress of real-time processing.


### Dependencies
The program has been tested in Ubuntu 20.04.

- Developed using Python 3.11.7.
- Preprocessing strongly depends on [ANTsPy](https://antspyx.readthedocs.io/en/latest/),
except for motion correction that is done using [FSL mcflirt](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/MCFLIRT).
- The environment runs using the [python version](https://electronstudio.github.io/raylib-python-cffi/README.html#installation) 
of Raylib.
- The Dashboard runs on Streamlit 1.30.0.


### Requirements
1. To avoid slowdowns that hinder the correct rendering of visual stimuli presented to participants a
dedicated graphic card is required to run the Raylib environment.

2. Also you should set up a "/mnt/fmritemp" folder to store temporary data. Ideally the folder
should be a ram disk of at least 1GB size.

### Run the program

Remember to **change the paths** on the "rtfmri_dashboard/controller.py" and "rtfmri_dashboard/envs/render.py" scripts before running.

Run the controller script to start the main program. The environment will spawn by itself
after the reference volume has been preprocessed.
```
python ./rtfmri_dashboard/controller.py
```

Run the Dashboard. The Dashboard is only for visualization purposes and doesn't need to be
run for the controller to work properly.
```
streamlit run ./rtfmri_dashboard/real_time/dashboard.py
```
