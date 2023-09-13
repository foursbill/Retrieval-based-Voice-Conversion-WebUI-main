<div align="center">

<h1>Retrieval-based-Voice-Conversion-WebUI</h1>
Kerangka transformasi suara (pengubah suara) yang sederhana dan mudah digunakan berdasarkan VITS<br><br>

[![madewithlove](https://forthebadge.com/images/badges/built-with-love.svg)](https://github.com/foursbill/Retrieval-based-Voice-Conversion-WebUI-main)

<img src="https://counter.seku.su/cmoe?name=rvc&theme=r34" /><br>

[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/github/liujing04/Retrieval-based-Voice-Conversion-WebUI/blob/main/Retrieval_based_Voice_Conversion_WebUI.ipynb)
[![Licence](https://img.shields.io/github/license/liujing04/Retrieval-based-Voice-Conversion-WebUI?style=for-the-badge)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI/blob/main/%E4%BD%BF%E7%94%A8%E9%9C%80%E9%81%B5%E5%AE%88%E7%9A%84%E5%8D%8F%E8%AE%AE-LICENSE.txt)
[![Huggingface](https://img.shields.io/badge/🤗%20-Spaces-yellow.svg?style=for-the-badge)](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

</div>

------

[**memperbarui log**](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI/blob/main/Changelog_CN.md) | [**Pertanyaan yang Sering Diajukan**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E7%AD%94) | [**AutoDL·5 sen untuk melatih penyanyi AI**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B) | [**Catatan Eksperimen Kontrol**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%AF%B9%E7%85%A7%E5%AE%9E%E9%AA%8C%C2%B7%E5%AE%9E%E9%AA%8C%E8%AE%B0%E5%BD%95))

[**English**](./docs/README.en.md) | [**Simplified Chinese**](./README.md) | [**Japanese**](./docs/README.ja.md) | [**korean**](./docs/README.ko.md) ([**South Korea**](./docs/README.ko.han.md))


> Klik di sini untuk melihat [Video Demo] kami(https://www.bilibili.com/video/BV1pm4y1z7Gm/) !

> Real-time voice conversion using RVC: [w-okada/voice-changer](https://github.com/w-okada/voice-changer)

> Model bawah dilatih dengan hampir 50 jam set pelatihan VCTK open source berkualitas tinggi, tidak ada masalah hak cipta, jangan ragu untuk menggunakannya

> Di masa mendatang, set pelatihan menyanyi resmi berkualitas tinggi akan ditambahkan ke model pelatihan

## Introduction
This warehouse has the following characteristics
+ Use top1 to retrieve and replace input source features with training set features to prevent timbre leakage
+ fast training even on relatively poor graphics cards
+ Using a small amount of data for training can also get better results (it is recommended to collect at least 10 minutes of low-noise speech data)
+ Ability to change timbres by model fusion (with ckpt-merge in the ckpt processing tab)
+ easy-to-use web interface
+ UVR5 model can be called to quickly separate vocals and accompaniment

## Environment configuration
Poetr is recommended
```bash
# Install Pytorch and its core dependencies, skip if already installed
# Referenced from: https://pytorch.org/get-started/locally/
pip install torch torchvision torchaudio

#If it is a win system+Nvidia Ampere Architecture(RTX30xx)，according to #21 Experience, you need to specify the cuda version corresponding to pytorch
#pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117

# Install the Poetry dependency management tool, skip if already installed
# Referenced from: https://python-poetry.org/docs/#installation
curl -sSL https://install.python-poetry.org | python3 -

# Install dependencies through poetry
poetry install
```

You can also install dependencies via pip:

**Notice**: `MacOS`下`faiss 1.7.2`The version will cause a segment error to be thrown. Please use the command `pip install faiss-cpu==1.7.0` to specify the version `1.7.0` during manual installation
 `MacOS`You can install `Swig` through `brew`

 ```bash
 brew install swig
 ```

```bash
pip install -r requirements.txt
```

## Other pre-model preparation
RVC requires some other pre-models for inference and training.

You can download these models from our [Hugging Face space](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/).

Below is a list with the names of all pre-models and other files required by RVC:
```bash
hubert_base.pt

./pretrained 

./uvr5_weights

#If you are using Windows, you may need this file, skip if ffmpeg and ffprobe are already installed; ubuntu/debian users can install these 2 libraries through apt install ffmpeg
./ffmpeg

./ffprobe
```
Then use the following command to start the WebUI:
```bash
python infer-web.py
```
If you are using Windows, you can directly download and unzip `RVC-beta.7z`, run `go-web.bat` to start WebUI.

There is also a `Xiaobai Simple Tutorial.doc` in the warehouse for reference.

## reference project
+ [ContentVec](https://github.com/auspicious3000/contentvec/)
+ [VITS](https://github.com/jaywalnut310/vits)
+ [HIFIGAN](https://github.com/jik876/hifi-gan)
+ [Gradio](https://github.com/gradio-app/gradio)
+ [FFmpeg](https://github.com/FFmpeg/FFmpeg)
+ [Ultimate Vocal Remover](https://github.com/Anjok07/ultimatevocalremovergui)
+ [audio-slicer](https://github.com/openvpi/audio-slicer)

## Thanks to all contributors for their efforts
<a href="https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI/graphs/contributors" target="_blank">
  <img src="https://contrib.rocks/image?repo=liujing04/Retrieval-based-Voice-Conversion-WebUI" />
</a>
