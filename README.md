# audio-to-text-
1. Sign Up for a Free Tier Account
Google Cloud offers a Free Tier plan, which will be used in this tutorial. An account is required to get an API key.

2. Generate an API Key
Follow these steps to generate an API key:

Sign-in to Google Cloud Console
Click “APIs & Services”
Click “Credentials”
Click “Create Credentials”
Select “Service Account Key”
Under “Service Account” select “New service account”
Name service (whatever you’d like)
Select Role: “Project” -> “Owner”
Leave “JSON” option selected
Click “Create”
Save generated API key file
Rename file to api-key.json
Make sure to move the key into speech-to-text cloned repo, if you plan to test this code.

3. Convert Audio File to Wav format
I ran into issues when trying to convert my audio file via a command line tools. Instead, I used Audacity (an open source audio editing tool) to convert my file to wav format. Audacity is great and I highly recommended it.

The steps to convert:

Open file in Audacity
Click “File” menu
Click “Save other”
Click “Export as Wav”
Export it with default setting
4. Break up audio file into smaller parts
Google Cloud Speech API only accepts files no longer than 60 seconds. To be on the safe side, I broke my files in 30-second chunks. To do that I used an open source command line library called ffmpeg. It can be download from its site. On Mac, I installed it with Homebrew via brew install ffmpeg.

Here is the command I used to break up my file:

# Clean out old parts if needed via rm -rf parts/*
ffmpeg -i source/genevieve.wav -f segment -segment_time 30 -c copy parts/out%09d.wav
Code language: PHP (php)
Where, source/genevieve.wav is the name of the input file, and parts/out%09d.wav is the format for output files. %09d indicated that the file number will be padded with 9 zeros (i.e. out000000001.wav), allowing files to be sorted alphabetically. This way ls command returns files sorted in the right order.

5. Install required Python modules
I added requirements.txt in example repo with all needed libraries. It can be used to install all via:

pip3 install -r requirements.txt
Code language: CSS (css)
The real hero on this list is the SpeechRecognition. It does most of the heavy lifting.

The rest of the libraries came with the official google-api-python-client package.

I also used tqdm module to show progress in the slower version of the script.

6. Running the Code
Finally, we can run the Python script to get the transcript. For example python3 fast.py.
