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

>    `sudo chown $(whoami):admin /usr/local && sudo chown -R $(whoami):admin /usr/local`

Python is installed by default in OS X, but we’ll want to install a fresh copy through Homebrew. This install includes the **`pip`** package manager and a few other tools Apple left out.

    brew install python

Now install ffmpeg, a command-line tool for audio/video encoding.

     brew install ffmpeg --with-fdk-aac --with-ffplay --with-freetype --with-gpl --with-libass --with-libfdk-aac --with-libfreetype --with-libmp3lame --with-libopus --with-libquvi --with-libvorbis --with-libvpx --with-libx264 --with-libx265 --with-nonfree --with-opus --with-x265

Before we install our Python dependencies, let’s update pip. The **`-U`** option upgrades related components to their most recent versions.

    pip install -U pip

Enter the following command to install the required packages in Python.

    pip install -U jupyter numpy scipy matplotlib pandas sklearn pydub tqdm requests
    pip install pyAudioAnalysis

Now open Jupyter by entering the following two commands. The first navigates to the desktop and the second launches Jupyter's local notebook server.

    cd ~/Desktop
    jupyter notebook

Leave this terminal window open as long as you're using Jupyter. You might want to minimize it.

The Jupyter interface should appear in a new browser window, displaying the files on your desktop. If not, point your browser to **`http://localhost:8888`**

Create a new Jupyter notebook via the dropdown menu at the upper left: **`File > New Noteboook > Python 2`**
