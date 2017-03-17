# Workshop: Audio Machine Learning Introduction

- Download five or ten historical NBC radio recordings from Archive.org.
  - https://archive.org/details/NBCCompleteBroadcastDDay/




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



- Repeat this process, collecting tags for five or ten chime sequences.

- Next we'll extract these segments as new audio files. If you haven't already, download Audio Tagging Toolkit.

  - https://github.com/hipstas/audio-tagging-toolkit

- Open a new terminal window and `cd` to the toolkit's directory.

```
cd /path/to/audio-tagging-toolkit/
```







![](img/img06.png)
![](img/img07.png)

![](img/img08.png)

![](img/img09.png)

![](img/img10.png)

![](img/img11.png)

![](img/img12.png)