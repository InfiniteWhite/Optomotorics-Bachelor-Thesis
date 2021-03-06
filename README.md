# Optomotorics-Bachelor-Thesis

This project is part of my Bachelor Thesis in Biology. The Opt_Moto code runs a machine designed to test optomotoric walking behavior in fruit flies. Data is being acquired through an Analog/Digital-Converter which receives a signal from a sensor controlled by the fly and another signal from the arena turning around the fly. 
For further information on the topic see my Bachelor Thesis "Establishing An Optomotor Experiment For Drosophila" (LINK)

3 primary programs:
1. Opt_Moto.py: 
- modified version of the ULAIO01.py program from the mcculw library
- succeeds in writing some of the input directly to a text document called "rawtext.txt" in real time, which can be used by the following program for live real-time plotting
- writes a more accurate list of the collected data at the end of one run to "KHZtext.txt" and then to a user-specified XML document
- The UI allows the user to control the experiment and specify the metadata to then create an XML file which can be used for further examination

2. live_graph.py:
- takes data from rawdata.txt, stores it and shows at most 150 data points from the fly position and at most 500 data points from the arena position
- uses that data to plot the before mentioned live graph
- can be called by pressing a button on the Opt_Moto.py UI

3. easy_plot.R:
- early version of data evaluation
- used for experimentation with the data to find plots that should be implemented in the main evaluation program (https://github.com/brembslab/DTSevaluations.git)

INSTALLATION
1. Install the “MCC Universal Library Python API for Windows” from Github (https://github.com/mccdaq/mcculw.git) and follow the installation instructions in the readme file. Please follow the instructions for Python 2.7.
2. Download the files from this repository (the easy_plot programs are optional).
3. Save them all in the same folder (important!) and in the same drive as the Universal Library from MCC and Python.
4. Use the pip install command in the Windows command center to install all the packages needed in the programs: tkinter, etree, os, winsoud, shutil, datetime, sys, tkMessageBox, matplotlib, pycompile
5. To be able to call the live graph, live_graph.py first has to be compiled. Just run setup.py and this should be resolved.

UI DOCUMENTATION

Analog Input:
- Low Channel Number represents the first channel of the A/D converter that should be taken into account. In the existing setup, Channel 0 is the fly’s signal.
- High Channel Number represents the last channel of the A/D converter that should be taken into account. In the existing setup, Channel 1 is the arena position signal. If Channel 2 would be added, the arena speed should be measured additionally.
- Period Duration defines the timespan of one period in seconds
- Number of Periods defines the quantity of periods that should be measured. By multiplying “Period Duration” with “Number of Periods” the experiment duration can be derived.
- Write to TXT and plot live graph starts the live plotting (“live_graph.py”) of all channels that are measured.
- Start Analog Input starts the actual experiment.
- Status can be either “idle” or “running".
- Period depicts which period has been reached in the time series.
- Index depicts the number of data points that have been acquired so far.
- Count depicts the number of data points that have been acquired so far.

Metadata:
- First name of the experimenter
- Lastname of the experimenter
- Orcid ID of the experimenter
- Flytype
- Flyname. An identifier string. Lowercase characters with ., _, - and / are allowed. This is ideally a url-usable and human-readable name.
- Flydescription of the fly strain
- Experimenttype with the type of “joystick”
- Date and Time is being generated automatically but can be changed manually.
- File Name is the name for the XML file that will be generated.
- Samplingrate(HZ) shows the frequency at which data is being acquired.
- Pattern(number) is a documentation field for the used pattern. For the pattern classification see "https://docs.google.com/document/d/1AN1AaDx_QCwTGT3eXNvgVLIGefST_Jaa31iktVDaSc0/edit?ts=5bc70f33"

PROGRAM OPERATION

1.    Start the Opt_Moto.py program and check the parameters (see Attachment 2)
2.    Plug in the lamp for the arena
3.    Retract and position the arm responsible for holding the fly in a way that makes it easily accessible
4.    Attach a fly to the clamp on the arm and make sure it is perfectly horizontal
5.    Use the 3D manipulator to lower the fly to the desired position (standard: central tip of the platform, facing away from the          platform suspension)
6.    Switch all light sources except the arena light in the room off
7.    Switch the motor control unit on and press the “Start Analog Input” button in the program at the same time if possible
8.    Once the program is completed check the metadata and press the button “Transfer data to XML (only when idle)”
9.    To run another test click the “Quit” button, restart the program and begin from step 1, only disregarding the motor control switch in step 7 

DATA EVALUATION

The programs from "https://github.com/brembslab/DTSevaluations.git" are able to evaluate the data generated by Opt_moto.py if certain conditions are met. All the XML files generated for one experiment group have to be documented manually in the yml file with the format given in the example. For more precise instructions read the section "Software" in the earlier mentioned Bachelor Thesis.
