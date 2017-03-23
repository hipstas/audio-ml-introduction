# Workshop: Audio Machine Learning Introduction

### Setup

- Before the workshop, follow the steps in [README.md](https://github.com/hipstas/audio-ml-introduction/blob/master/README.md) to install the software you will need.
- Download the workshop guide and Audio Tagging Toolkit from GitHub and unzip them. Move the **audio-ml-introduction-master** and **audio-tagging-toolkit-master** folders to the desktop.
  - [Download this workshop guide](https://github.com/hipstas/audio-ml-introduction/archive/master.zip)
  - [Download Audio Tagging Toolkit](https://github.com/hipstas/audio-tagging-toolkit/archive/master.zip)
- Download five or ten historical NBC radio recordings from Archive.org and place them in a new folder called **NBC_Radio** on your desktop.
  - [https://archive.org/details/NBCCompleteBroadcastDDay/](https://archive.org/details/NBCCompleteBroadcastDDay/)
  - [Bundled file set](https://www.dropbox.com/s/xz05iyk0y0mkwpg/NBC_Radio.zip?dl=1)
- Create folders on your desktop called **NBC_Chimes** and **NBC_Not_Chimes**.

### Tagging Chimes

- Open one of the recordings in Sonic Visualiser. In the toolbar, select "Pane > Add Spectrogram > [filename]: All Channels Mixed." A spectral representation of your audio will appear at the bottom of the window.

![](img/img01.png)

- To adjust zoom, use the up and down arrows or scroll using your mouse. To the right of the spectrogram, in the second dropdown menu next to "Bins," change the option "Linear" to "Log."

- To move through the recording, use your left and right arrow keys or scroll sideways with your mouse. Here is a typical example of speech audio.

![](img/img02.png)

- Scroll to the end of the file and see if you can identify the NBC chime sequence by eye. It should look something like this.

![](img/img03.png)

- Next we'll apply a tag that identifies this segment of audio. In the toolbar, choose "Layer > Add New Regions Layer."
- The Draw tool in the upper right should be highlighted automatically. To make it easier to see our work, click the dropdown menu next to "Plot Type" and choose "Segmentation."
- Click and drag in the waveform at the top of the window to select just the chime segment.

![](img/img04.png)

- In the toolbar, select "File > Export Annotation Layer" and enter a name for your annotation file. For convenience, I recommend using the name of the audio file, using the extension ".csv" instead of ".mp3."
- Open the CSV file in a text editor. It should look something like this: one line with three values separated by commas. The first number is the starting time of our tagged segment, in seconds. The last number is the duration of our tag. The second value, "1," is a numeric class identifier; more on this later.

![](img/img05.png)

- Repeat this process, collecting tags for five or ten chime sequences. Quit Sonic Visualiser after working on each file.


### Extracting Chime Audio

- Next we'll extract these segments as new audio files. Open Terminal, located under "Utilities" in your "Applications" folder.

- Open a new terminal window and `cd` to the toolkit's directory.

```
cd ~/Desktop/audio-tagging-toolkit-master/
```

- To run a script, we will execute it using Python along with a series of options. Here is the basic format.

```
python ExcerptClass.py -i /path/to/audio.mp3 -t /path/to/tags.csv -e 1 -o /path/to/output/directory
```

- The "-i" option is the pathname for our audio file. The "-t" option points to a CSV tag file from Sonic Visualiser. The "-e" option indicates we want to extract audio for class 1, which we saw in the CSV file above.

- To get a file's pathname, drag its icon from a Finder window into a terminal window.

- Create a folder called "NBC_Chimes" on your desktop, which we will use as our output folder. Construct a command for each of the files you tagged. Here is an example for a file called "CBD-440606_NBC1945-HVKaltenborn.mp3":

```
cd ~/Desktop/audio-tagging-toolkit-master/

python ExcerptClass.py -i ~/Desktop/NBC_Radio/CBD-440606_NBC1945-HVKaltenborn.mp3 -t ~/Desktop/NBC_Radio/CBD-440606_NBC1945-HVKaltenborn.csv -e 1 -o ~/Desktop/NBC_Chimes/
```


### Extracting Non-Chime Audio

- We also need examples of non-chime audio in order to train our classifier, so let's choose some clips at random. The `RandomTags.py` script in Audio Tagging Toolkit will handle the details.

```
python RandomTags.py -n 5 -s 3 -e -i /path/to/example.mp3 -o /path/to/output_dir/
```
- The example above will extract five clips from example.mp3, each three seconds long. It will then export them as WAV files to a specified output directory.

- Create a folder on your desktop called "NBC_Not_Chimes." Try entering a command like the one above to see if it works.

- If you don't want to enter a new `RandomTags.py` command for each file, you can loop through your audio files using a short bash script:

```
cd ~/Desktop/audio-tagging-toolkit-master/

for filename in ~/Desktop/NBC_Radio/*.mp3; do
python RandomTags.py -n 5 -s 3 -e -i $filename -o ~/Desktop/NBC_Not_Chimes/ ;
done
```

- Once you've generated a set of random audio segments, you'll need to make sure they don't include any chime audio by mistake. Open VLC Media Player and drag your random files into the playlist window. Now listen to the set; if a clip contains chimes, locate it in the Finder and delete it.

### Training Classifier Model

- Enter the following command in the terminal to launch the Python shell:

```
python
```

- Now enter the following to import packages and set ourworking directory to the desktop.

```python
from pyAudioAnalysis import audioTrainTest as aT
import os
os.chdir(os.path.expanduser('~/Desktop/'))
```

- If the desktop contains directories called "NBC_Chimes" and "NBC_Not_Chimes," the following command will use any WAV audio files they contain to train a support vector machine (SVM) classifier. *Note: You may have to press return twice when entering this command.*

```python
aT.featureAndTrain(['NBC_Not_Chimes','NBC_Chimes'], 1.0, 1.0, aT.shortTermWindow, aT.shortTermStep, "svm", "audio-ml-introduction-master/model/svm_chimes", False)
```

- This will output a model file called "svm_chimes" in the "model" directory within the audio-ml-introduction-master directory, along with two supporting files.

![](img/img06.png)

### Classifying Audio

- Open a new terminal window and enter the following commands to launch the included Jupyter notebook.

```
cd ~/Desktop/audio-ml-introduction-master/
jupyter notebook "02 Find and Play NBC Chimes.ipynb"
```
