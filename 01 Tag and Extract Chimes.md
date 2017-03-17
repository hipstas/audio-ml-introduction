# Workshop: Audio Machine Learning Introduction

- Download five or ten historical NBC radio recordings from Archive.org and place them in a folder called "NBC_Radio" on your desktop.
  - https://archive.org/details/NBCCompleteBroadcastDDay/
  - easy download: https://www.dropbox.com/sh/zd0pxk2gcq079xh/AAC-JYAO3JP5MeTMa1F0K6F3a?dl=0


- Open one of the recordings in Sonic Visualiser. In the toolbar, select "Pane > Add Spectrogram > [filename]: All Channels Mixed." A spectral representation of your audio will appear at the bottom of the window.


![](img/img01.png)



- Use the up and down arrows (or scroll using your mouse) to zoom. To the right of the spectrogram, in the second dropdown menu next to "Bins," change the option "Linear" to "Log."


- Use your left and right arrow keys (or scroll sideways using mouse) to examine the recording. Here is a typical example of speech audio.



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



- Repeat this process, collecting tags for five or ten chime sequences. Note: you can close the Sonic Visualiser window before opening a new file

- Next we'll extract these segments as new audio files. If you haven't already, download Audio Tagging Toolkit.

  - https://github.com/hipstas/audio-tagging-toolkit

- Open a new terminal window and `cd` to the toolkit's directory.

```
cd /path/to/audio-tagging-toolkit/
```



- To run a script, we will execute it using Python along with a series of options. Here is the basic format.

```
python ExcerptClass.py -i /path/to/audio.mp3 -t /path/to/tags.csv -e 1 -o /path/to/output/directory
```

- The "-i" option is the pathname for our audio file. The "-t" option points to a CSV tag file from Sonic Visualiser. The "-e" option indicates we want to extract audio for class 1, which we saw in the CSV file above. 

- To get a file's pathname, drag its icon from a Finder window into a terminal window. 

- Create a folder called "NBC_Chimes" on your desktop, which we will use as our output folder. 

```
python ExcerptClass.py -i ~/Desktop/NBC_Radio/CBD-440606_NBC1945-HVKaltenborn.mp3 -t ~/Desktop/NBC_Radio/CBD-440606_NBC1945-HVKaltenborn.csv -e 1 -o ~/Desktop/NBC_Chimes/
```

- 


### Extracting non-
- 





![](img/img06.png)
![](img/img07.png)

![](img/img08.png)

![](img/img09.png)

![](img/img10.png)

![](img/img11.png)

![](img/img12.png)