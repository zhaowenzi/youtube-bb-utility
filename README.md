
**Forked from mbuckler/youtube-bb. Thank you for the original work!**

# YouTube BoundingBox

This repo contains helpful scripts for using the [YouTube BoundingBoxes](
https://research.google.com/youtube-bb/index.html) 
dataset released by Google Research. The only current hosting method 
provided for the dataset is [annotations in csv
form](https://research.google.com/youtube-bb/download.html). The csv files contain links to the videos on YouTube, but it's up to you to download the video files themselves. For this
reason, these scripts are provided for downloading, cutting, and decoding
the videos into a usable form.

This script only downloads the frames that have been labelled for object detection.
Labels are available for 380,000 video segments of about 19s each.
Bounding box information is only available every second, so that is about 19 JPG images
per segment. However, the videos are encoded
at various framerates (I've found 24fps, 29.99fps, 30fps, ...).
That is why this script uses OpenCV to extract frames from the closest timestamps that have been labelled. 
*You can uncomment lines 90 to 96 if you want to print the bounding boxes on the downloaded images.
I used that to verify that my calculations were ok.*

This script was originally written by Mark Buckler.
The YouTube BoundingBoxes dataset was created and curated by Esteban Real,
Jonathon Shlens, Stefano Mazzocchi, Xin Pan, and Vincent Vanhoucke.
The dataset web page is [here](https://research.google.com/youtube-bb/index.html) and the
accompanying whitepaper is [here](https://arxiv.org/abs/1702.00824).
*This fork was written by Mehdi Shibahara*


## Installing the dependencies

1. Clone this repository.

2. Install majority of dependencies by running 
  + `pip install -r requirements.txt` in this repo's directory.
  + Install opencv: using conda or build from source

3. Install wget, and [youtube-dl](https://github.com/rg3/youtube-dl)
through your package manager.
For most platforms this should be straightforward, but for 
Ubuntu 14.04 users you will need to update your apt-get repository 
before being able to install ffmpeg as [shown
here](https://www.faqforge.com/linux/how-to-install-ffmpeg-on-ubuntu-14-04/).

Some small tweaks may be needed for different software environments.
These scripts were developed and tested on Ubuntu 16.04.

## Running the scripts

Note: This script was developed with Python 2.7.

### Download and decode

The `download_detection.py` script is provided for users who are interested in
downloading and decoding the videos which accompany the provided annotations. It also
cuts these videos down to the range in which they have been
annotated, then extract only the frames with label.
Parallel video downloads are supported so that you can
saturate your download bandwith even though YouTube throttles per-video.

Run `python download_detection.py [VIDEO_DIR] [NUM_THREADS]` to download the dataset into the specified
directory.
