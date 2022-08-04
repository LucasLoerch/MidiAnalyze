# MidiAnalyze
Python algorithm to assess the accuracy of the performance of notated musical melodies on Midi instruments

Author: Lucas Lörch; lucasloerch@posteo.de; ORCID https://orcid.org/0000-0002-5665-3313 
License:	Creative Commons Attribution-NonCommercial 3.0 Unported License (CC BY-NC 3.0)
Cite:	Lörch, L. (2021). MidiAnalyze. A Python Package for the Analysis of Musical Performance Midi Data. https://doi.org/10.17605/OSF.IO/FKW4B
Manual: [MidiAnalyze v1-0 Manual.pdf](https://github.com/LucasLoerch/MidiAnalyze/files/9260162/MidiAnalyze.v1-0.Manual.pdf)

# General idea and purpose
MidiAnalyze is a Python software package to analyze musical performances on Midi instruments. It has been developed for usage in the context of scientific experiments. The program uses two kinds of Midi files: stimulus melodies, i.e. Midi files that hold the notes that participants were asked to perform, and performances, i.e. Midi files that hold what the participants played. The functions of the program compare the performances with the stimulus melodies and store the resulting accuracy measures in a spreadsheet.

# Technical specifications
MidiAnalyze was developed and tested with Python 3.7.1 on Spyder IDE 4.0.0b7 under Windows 10. It has not yet been tested on other operating systems or with other versions of Python. It requires the Python packages music21, sys, os, glob and pandas.

# Workflow
1. Install dependables
Install Python and the packages music 21, sys, os, glob and pandas. These packages are needed by MidiAnalyze


2. Run the MidiAnalyze Code
Open the file MidiAnalyze v1-0.py in Python and run the whole code. Now the functions of MidiAnalyze can be used.


3. Prepare your data
To use MidiAnalyze, prepare your data as follows:

3.1 create one folder that contains Midi files of all the original melodies, i.e. of the melodies participants had
to perform during your experiment. These Midi files need to be named according to the item name.
For example, if one melody constitutes the first item of condition 1, you could name the file condition1_item1.mid
When choosing a name, consider the number of conditions and items. If you would have, for example, more than
10 conditions and more than 10 items, you should name your files condition01_item01.mid

3.2 create one folder that contains all the experimental data, i.e. the Midi files that you collected during 
participants' performances. These midi files need to be named according to the participant identifier and the item name.
For example, if participant 15 performed item 1 of condition 1, you could name the file participant15_condition1_item1.mid
It is very important that the item names of the original melodies and the item names of the experimental performances are congruent.
Only if this is the case, the original melodies can be assigned correctly to the experimental performances.
In the example above, if you would name your experimental file participant15_condition_1_item_1.mid, the program
would not be able to assign the original melody condition1_item1.mid to it, as the item identifier differs.
Moreover, it is important that your Midi files contain only one performance and that this performance is aligned with the beat.
In some experiments, one might just let the recording running during the whole experiment, comprising the performance of
multiple melodies. If this is the case, it is necessary to use some software that is able to edit Midi and to extract 
the single melodies and export them as Midi files.


4. import all Midi files to MidiAnalyze
Enter the command getyourMidiFiles(performanceDataPath, solutionDataPath, startItemName, endItemName, startSubjectName, endSubjectName)
As perfromanceDataPath, enter the path to the folder with the performance data as created under 3.2 in quotation marks.
Note that Python requires double-backslashes in filepaths under Windows. For example, if your performance data is in a folder "Experiment"
on the desktop, the path would be "C:\\Users\\YourName\\Desktop\\Experiment\\"

As solutionDataPath enter the path to the folder with the original melodies as created under 3.1 in quotation marks.

As startItemName and endItemName, enter the position at which the item identifier starts and ends
in the filenames of your performance files as named under 3.2.
Note that in Python, the first position is indicated by 0. For example if your file name would be participant15_condition1_item1.mid,
the item identifier (which is condition1_item1) starts at the 14th position (at the c) so startItemName would be 14.
The identifier ends at the 30th position (at the .) so endItemName would be 30

As startSubjectName and endSubjectName enter the position at which the participant identifier starts and ends
in the filenames of your performance files as named under 3.2.
Note that in Python, the first position is indicated by 0. For example if your file name would be participant15_condition1_item1.mid,
the participant identifier (which is participant15) starts at the first position (at the p) and hence startSubjectName would be 0.
The identifier ends at the 13th position (at the _) so endSubjectName would be 13.


5. Quantize if requested
If needed, all Midi files can be quantized with the command quantizeMidi(noteValue, quantizeOffsets, quantizeDurations)
As noteValue, indicate on which note value the quantization should be based (1=quarter, 2=eighth, 4=sixteenth, 0.5=half, 0.25=whole, 3=eighth triplets)
in square brackets.
If quantizeOffsets is set to TRUE, the beginning of each note is quantized.
If quantizeDurations is set to TRUE, the end of each note is quantized.
The quantization moves the offset and/or the duration of each note to the closest note with the value specified.
For example if the specified note value is eighth note and quantizeOffsets and quantize Durations is set to TRUE, 
both the beginning and the end of each note is moved to the closest eighth note.


6. Analyze the performances
Run the command analyzeMidi(). MidiAnalyze calculates the accuracy measures and descriptive statistics for all performance files.


7. Export the results
Run the command exportResults(resultsFileName)
As resultsFileName, indicate how you want to name the file that will be generated. MidiAnalyze then creates all results as a .csv
table in the folder with the original melodies as created under 3.1
