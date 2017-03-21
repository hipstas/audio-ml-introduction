# Workshop: Audio Machine Learning Introduction

## Audio Software

Install the following programs for audio visualization and playback (available for macOS, Windows, and Linux).

- Sonic Visualiser: http://www.sonicvisualiser.org/download.html

- VLC media player: http://www.videolan.org


## Text Editor

Install a plaintext editor if you don't have one already.

- TextWrangler: http://www.barebones.com/products/textwrangler/

- Geany: https://www.geany.org/Download/Releases


## Command Line Setup (Mac)

Launch **`Terminal`** in macOS, located at **`/Applications/Utilities/Terminal.app`**

> If your current account doesn't have admin privileges, switch users by entering the following command (substituting the username of the admin account). Press return and enter your password at the prompt.
>
>    `su your_admin_name`
>
> If you don't remember your admin username, the following command will list the users on your system.
>
>    `ls /Users/`

To install a bundle of command-line tools provided by Apple, paste the following line into the terminal window and press return. When prompted, click "Install," then "Agree."

    xcode-select --install

Run the following command to install the **`Homebrew`** package manager. Enter your password at the prompt to proceed.

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Next, enter this command to update Homebrew.

    brew update

> If Homebrew returns an error, enter the following command to give it the permissions it expects.
>
>    `sudo chown $(whoami):admin /usr/local && sudo chown -R $(whoami):admin /usr/local`

Python is installed by default in macOS, but we’ll want to install a fresh copy through Homebrew. This version includes the **`pip`** package manager and a few other tools Apple left out.

```
brew install python

brew link --overwrite python
```

Before we install our Python dependencies, let’s update pip. The **`-U`** option upgrades related components to their most recent versions.

```
pip install -U pip
```

Enter the following commands to install several required Python packages.

```
pip install -U jupyter numpy scipy matplotlib pandas sklearn pydub tqdm requests

pip install pyAudioAnalysis
```


Now install **`ffmpeg`**, a command-line tool for audio/video encoding. First we will install several media codecs, then we will download ffmpeg's source code and compile it before installing. Although it is faster to install ffmpeg through Homebrew, that version can't read or write MP3 files.

Enter the following commands one at a time; note that the first and fourth lines are very long. After the last command you will be prompted to enter your password.

```
brew install automake fdk-aac git lame libass libtool libvorbis libvpx opus sdl shtool texi2html theora wget x264 xvid yasm

git clone http://source.ffmpeg.org/git/ffmpeg.git ffmpeg

cd ffmpeg

./configure  --prefix=/usr/local --enable-gpl --enable-nonfree --enable-libass --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libxvid

make && sudo make install
```

While you wait for ffmpeg to compile (which may take 5 or 10 minutes), let's create a Jupyter notebook. Open a new terminal window by pressing  ⌘+N or selecting "Shell > New Window > New Window with Settings - Novel" in the toolbar.

Now launch Jupyter by entering the following two commands. The first navigates to the desktop and the second launches Jupyter's local notebook server.

```
cd ~/Desktop

jupyter notebook
```

Leave this terminal window open as long as you're using Jupyter. You might want to minimize it.

The Jupyter interface should appear in a new browser window, displaying the files on your desktop. If it doesn't launch automatically, enter **`http://localhost:8888`** in your browser's URL box.

Create a new Jupyter notebook via the dropdown menu at the upper left: **`File > New Noteboook > Python 2`**

If you've made it this far, you're done for now. We'll talk more about Jupyter during the workshop.
