# Subs AI
Subtitles generation tool (Web-UI + CLI + Python package) powered by OpenAI's Whisper and its variants.

<br/>
<p align="center">
  <img src="./assets/demo/demo.gif">
</p>

# Features
* Supported Models
  * [x] [openai/whisper](https://github.com/openai/whisper)
  * [x] [linto-ai/whisper-timestamped](https://github.com/linto-ai/whisper-timestamped)
  * [ ] [ggerganov/whisper.cpp](https://github.com/ggerganov/whisper.cpp) (Soon)
  
* Web UI
  * Fully offline, no third party services 
  * Works on Linux, Mac and Windows
  * Intuitive and easy to use
  * Supports subtitle modification
  * Integrated tools:
    * Translation using [xhluca/dl-translate](https://github.com/xhluca/dl-translate):
      * Supported models:
        * [x] [facebook/m2m100_418M](https://huggingface.co/facebook/m2m100_418M)
        * [x] [facebook/m2m100_1.2B](https://huggingface.co/facebook/m2m100_1.2B)
        * [x] [facebook/mbart-large-50-many-to-many-mmt](https://huggingface.co/facebook/mbart-large-50-many-to-many-mmt)
    * Auto-sync using [smacke/ffsubsync](https://github.com/smacke/ffsubsync)
* Command Line Interface
  * For simple or batch processing
* Python package
  * Easy API in case you want to develop your own UI
* Supports different subtitles formats thanks to [tkarabela/pysubs2](https://github.com/tkarabela/pysubs2/)
  * [x] SubRip
  * [x] WebVTT
  * [x] substation alpha
  * [x] MicroDVD
  * [x] MPL2
  * [x] TMP
* Supports audio and video files
# Installation 
```shell
pip install subsai
```
# Usage
* Web UI

To use the web UI, run the following command on the terminal
```shell
subsai-webui
```

And a web page will open on your default browser.

* CLI

```shell
usage: subsai [-h] [--version] [-m MODEL] [-mc MODEL_CONFIGS] [-f FORMAT] [-df DESTINATION_FOLDER] [-tm TRANSLATION_MODEL]
              [-tc TRANSLATION_CONFIGS] [-tsl TRANSLATION_SOURCE_LANG] [-ttl TRANSLATION_TARGET_LANG]
              media_file [media_file ...]

positional arguments:
  media_file            The path of the media file, a list of files, or a text file containing paths for batch processing.

options:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  -m MODEL, --model MODEL
                        The transcription AI models. Available models: ['openai/whisper', 'linto-ai/whisper-timestamped']
  -mc MODEL_CONFIGS, --model-configs MODEL_CONFIGS
                        JSON configuration (path to a json file or a direct string)
  -f FORMAT, --format FORMAT, --subtitles-format FORMAT
                        Output subtitles format, available formats ['.srt', '.ass', '.ssa', '.sub', '.json', '.txt', '.vtt']
  -df DESTINATION_FOLDER, --destination-folder DESTINATION_FOLDER
                        The directory where the subtitles will be stored, default to the same folder where the media file(s) is stored.
  -tm TRANSLATION_MODEL, --translation-model TRANSLATION_MODEL
                        Translate subtitles using AI models, available models: ['facebook/m2m100_418M', 'facebook/m2m100_1.2B',
                        'facebook/mbart-large-50-many-to-many-mmt']
  -tc TRANSLATION_CONFIGS, --translation-configs TRANSLATION_CONFIGS
                        JSON configuration (path to a json file or a direct string)
  -tsl TRANSLATION_SOURCE_LANG, --translation-source-lang TRANSLATION_SOURCE_LANG
                        Source language of the subtitles
  -ttl TRANSLATION_TARGET_LANG, --translation-target-lang TRANSLATION_TARGET_LANG
                        Target language of the subtitles


```

Example of simple usage
```shell
subsai ./assets/test1.mp4 --model openai/whisper --format srt
```

You can also provide a simple text file for batch processing 
_(Every line should contain the absolute path to a single media file)_

```shell
subsai /home/user/media.txt --model openai/whisper --format srt
```

* From Python

```python
from subsai import SubsAI

file = './assets/test1.mp4'
subs_ai = SubsAI()
model = subs_ai.create_model('openai/whisper', {'model_type': 'base'})
subs = subs_ai.transcribe(file, model)
subs.save('test1.srt')
```
Read the documentation for advanced usage.

# Contributing
If you find a bug, have a suggestion or feedback, please open an issue for discussion.


# License

This project is licensed under the GNU General Licence version 3 or later. You can modify or redistribute it under the conditions
of these licences (See [LICENSE](./LICENSE) for more information).
