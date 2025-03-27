# MuseTalk

MuseTalk: Real-Time High Quality Lip Synchronization with Latent Space Inpainting
</br>
Yue Zhang <sup>\*</sup>,
Minhao Liu<sup>\*</sup>,
Zhaokang Chen,
Bin Wu<sup>†</sup>,
Yubin Zeng, 
Chao Zhan,
Yingjie He,
Junxin Huang,
Wenjiang Zhou
(<sup>*</sup>Equal Contribution, <sup>†</sup>Corresponding Author, benbinwu@tencent.com)

Lyra Lab, Tencent Music Entertainment

**[github](https://github.com/TMElyralab/MuseTalk)**    **[huggingface](https://huggingface.co/TMElyralab/MuseTalk)**    **[space](https://huggingface.co/spaces/TMElyralab/MuseTalk)**    **[Technical report](https://arxiv.org/abs/2410.10122)**

We introduce `MuseTalk`, a **real-time high quality** lip-syncing model (30fps+ on an NVIDIA Tesla V100). MuseTalk can be applied with input videos, e.g., generated by [MuseV](https://github.com/TMElyralab/MuseV), as a complete virtual human solution.

:new: Update: We are thrilled to announce that [MusePose](https://github.com/TMElyralab/MusePose/) has been released. MusePose is an image-to-video generation framework for virtual human under control signal like pose. Together with MuseV and MuseTalk, we hope the community can join us and march towards the vision where a virtual human can be generated end2end with native ability of full body movement and interaction.

# Overview
`MuseTalk` is a real-time high quality audio-driven lip-syncing model trained in the latent space of `ft-mse-vae`, which

1. modifies an unseen face according to the input audio, with a size of face region of `256 x 256`.
1. supports audio in various languages, such as Chinese, English, and Japanese.
1. supports real-time inference with 30fps+ on an NVIDIA Tesla V100.
1. supports modification of the center point of the face region proposes, which **SIGNIFICANTLY** affects generation results. 
1. checkpoint available trained on the HDTF dataset.
1. training codes (comming soon).

# News
- [04/02/2024] Release MuseTalk project and pretrained models.
- [04/16/2024] Release Gradio [demo](https://huggingface.co/spaces/TMElyralab/MuseTalk) on HuggingFace Spaces (thanks to HF team for their community grant)
- [04/17/2024] : We release a pipeline that utilizes MuseTalk for real-time inference.
- [10/18/2024] :mega: We release the [technical report](https://arxiv.org/abs/2410.10122). Our report details a superior model to the open-source L1 loss version. It includes GAN and perceptual losses for improved clarity, and sync loss for enhanced performance.

## Model
![Model Structure](assets/figs/musetalk_arc.jpg)
MuseTalk was trained in latent spaces, where the images were encoded by a freezed VAE. The audio was encoded by a freezed `whisper-tiny` model. The architecture of the generation network was borrowed from the UNet of the `stable-diffusion-v1-4`, where the audio embeddings were fused to the image embeddings by cross-attention. 

Note that although we use a very similar architecture as Stable Diffusion, MuseTalk is distinct in that it is **NOT** a diffusion model. Instead, MuseTalk operates by inpainting in the latent space with a single step.

## Cases
<table>
<tr>
<td width="33%">

### Input Video
---
https://github.com/TMElyralab/MuseTalk/assets/163980830/37a3a666-7b90-4244-8d3a-058cb0e44107

---
https://github.com/user-attachments/assets/89f2697d-582d-4c7f-9808-4473410d60f4

---
https://github.com/user-attachments/assets/fa3b13a1-ae26-4d1d-899e-87435f8d22b3

---
https://github.com/user-attachments/assets/15800692-39d1-4f4c-99f2-aef044dc3251

---
https://github.com/user-attachments/assets/8a09ae73-20fa-40ac-9191-3ad816594314

---
https://github.com/user-attachments/assets/3f50e939-f794-4c5c-a814-1d878c6df7c7

</td>
<td width="33%">

### MuseTalk 1.0
---
https://github.com/user-attachments/assets/c04f3cd5-9f77-40e9-aafd-61978380d0ef

---
https://github.com/user-attachments/assets/feeb9ba9-6787-4192-b731-d7bdd63b64a9

---
https://github.com/user-attachments/assets/b5f56f71-5cdc-4e2e-a519-454242000d32

---
https://github.com/user-attachments/assets/a5843835-04ab-4c31-989f-0995cfc22f34

---
https://github.com/user-attachments/assets/3dc7f1d7-8747-4733-bbdd-97874af0c028

---
https://github.com/user-attachments/assets/3c78064e-faad-4637-83ae-28452a22b09a

</td>
<td width="33%">

### MuseTalk 1.5
---
https://github.com/user-attachments/assets/999a6f5b-61dd-48e1-b902-bb3f9cbc7247

---
https://github.com/user-attachments/assets/b6cf57d7-2aa5-4e8a-9dd3-72c79cc6b0bc

---
https://github.com/user-attachments/assets/471290d7-b157-4cf6-8a6d-7e899afa302c

---
https://github.com/user-attachments/assets/1ee77c4c-8c70-4add-b6db-583a12faa7dc

---
https://github.com/user-attachments/assets/370510ea-624c-43b7-bbb0-ab5333e0fcc4

---
https://github.com/user-attachments/assets/b011ece9-a332-4bc1-b8b7-ef6e383d7bde

</td>
</tr>
</table>


* The character of the last two rows, `Xinying Sun`, is a supermodel KOL. You can follow her on [douyin](https://www.douyin.com/user/MS4wLjABAAAAWDThbMPN_6Xmm_JgXexbOii1K-httbu2APdG8DvDyM8).

## Video dubbing
<table class="center">
  <tr style="font-weight: bolder;text-align:center;">
        <td width="70%">MuseTalk</td>
        <td width="30%">Original videos</td>
  </tr>
  <tr>
    <td>
      <video src=https://github.com/TMElyralab/MuseTalk/assets/163980830/4d7c5fa1-3550-4d52-8ed2-52f158150f24 controls preload></video>
    </td>
    <td>
      <a href="//www.bilibili.com/video/BV1wT411b7HU">Link</a>
      <href src=""></href>
    </td>
  </tr>
</table>

* For video dubbing, we applied a self-developed tool which can identify the talking person. 

## Some interesting videos!
<table class="center">
  <tr style="font-weight: bolder;text-align:center;">
        <td width="50%">Image</td>
        <td width="50%">MuseV + MuseTalk</td>
  </tr>
  <tr>
    <td>
      <img src=assets/demo/video1/video1.png width="95%">
    </td>
    <td>
      <video src=https://github.com/TMElyralab/MuseTalk/assets/163980830/1f02f9c6-8b98-475e-86b8-82ebee82fe0d controls preload></video>
    </td>
  </tr>
</table>

# TODO:
- [x] trained models and inference codes.
- [x] Huggingface Gradio [demo](https://huggingface.co/spaces/TMElyralab/MuseTalk).
- [x] codes for real-time inference.
- [ ] technical report.
- [ ] training codes.
- [ ] a better model (may take longer).


# Getting Started
We provide a detailed tutorial about the installation and the basic usage of MuseTalk for new users:

## Third party integration
Thanks for the third-party integration, which makes installation and use more convenient for everyone.
We also hope you note that we have not verified, maintained, or updated third-party. Please refer to this project for specific results.

### [ComfyUI](https://github.com/chaojie/ComfyUI-MuseTalk)

## Installation
To prepare the Python environment and install additional packages such as opencv, diffusers, mmcv, etc., please follow the steps below:
### Build environment

We recommend a python version >=3.10 and cuda version =11.7. Then build environment as follows:

```shell
pip install -r requirements.txt
```

### mmlab packages
```bash
pip install --no-cache-dir -U openmim 
mim install mmengine 
mim install "mmcv>=2.0.1" 
mim install "mmdet>=3.1.0" 
mim install "mmpose>=1.1.0" 
```

### Download ffmpeg-static
Download the ffmpeg-static and
```
export FFMPEG_PATH=/path/to/ffmpeg
```
for example:
```
export FFMPEG_PATH=/musetalk/ffmpeg-4.4-amd64-static
```
### Download weights
You can download weights manually as follows:

1. Download our trained [weights](https://huggingface.co/TMElyralab/MuseTalk).

2. Download the weights of other components:
   - [sd-vae-ft-mse](https://huggingface.co/stabilityai/sd-vae-ft-mse)
   - [whisper](https://openaipublic.azureedge.net/main/whisper/models/65147644a518d12f04e32d6f3b26facc3f8dd46e5390956a9424a650c0ce22b9/tiny.pt)
   - [dwpose](https://huggingface.co/yzd-v/DWPose/tree/main)
   - [face-parse-bisent](https://github.com/zllrunning/face-parsing.PyTorch)
   - [resnet18](https://download.pytorch.org/models/resnet18-5c106cde.pth)


Finally, these weights should be organized in `models` as follows:
```
./models/
├── musetalk
│   └── musetalk.json
│   └── pytorch_model.bin
├── dwpose
│   └── dw-ll_ucoco_384.pth
├── face-parse-bisent
│   ├── 79999_iter.pth
│   └── resnet18-5c106cde.pth
├── sd-vae-ft-mse
│   ├── config.json
│   └── diffusion_pytorch_model.bin
└── whisper
    └── tiny.pt
```
## Quickstart

### Inference
Here, we provide the inference script. 
```
python -m scripts.inference --inference_config configs/inference/test.yaml 
```
configs/inference/test.yaml is the path to the inference configuration file, including video_path and audio_path.
The video_path should be either a video file, an image file or a directory of images. 

You are recommended to input video with `25fps`, the same fps used when training the model. If your video is far less than 25fps, you are recommended to apply frame interpolation or directly convert the video to 25fps using ffmpeg.

#### Use of bbox_shift to have adjustable results
:mag_right: We have found that upper-bound of the mask has an important impact on mouth openness. Thus, to control the mask region, we suggest using the `bbox_shift` parameter. Positive values (moving towards the lower half) increase mouth openness, while negative values (moving towards the upper half) decrease mouth openness.

You can start by running with the default configuration to obtain the adjustable value range, and then re-run the script within this range. 

For example, in the case of `Xinying Sun`, after running the default configuration, it shows that the adjustable value rage is [-9, 9]. Then, to decrease the mouth openness, we set the value to be `-7`. 
```
python -m scripts.inference --inference_config configs/inference/test.yaml --bbox_shift -7 
```
:pushpin: More technical details can be found in [bbox_shift](assets/BBOX_SHIFT.md).

#### Combining MuseV and MuseTalk

As a complete solution to virtual human generation, you are suggested to first apply [MuseV](https://github.com/TMElyralab/MuseV) to generate a video (text-to-video, image-to-video or pose-to-video) by referring [this](https://github.com/TMElyralab/MuseV?tab=readme-ov-file#text2video). Frame interpolation is suggested to increase frame rate. Then, you can use `MuseTalk` to generate a lip-sync video by referring [this](https://github.com/TMElyralab/MuseTalk?tab=readme-ov-file#inference).

#### :new: Real-time inference

Here, we provide the inference script. This script first applies necessary pre-processing such as face detection, face parsing and VAE encode in advance. During inference, only UNet and the VAE decoder are involved, which makes MuseTalk real-time.

```
python -m scripts.realtime_inference --inference_config configs/inference/realtime.yaml --batch_size 4
```
configs/inference/realtime.yaml is the path to the real-time inference configuration file, including `preparation`, `video_path` , `bbox_shift` and `audio_clips`. 

1. Set `preparation` to `True` in `realtime.yaml` to prepare the materials for a new `avatar`. (If the `bbox_shift` has changed, you also need to re-prepare the materials.)
1. After that, the `avatar` will use an audio clip selected from `audio_clips` to generate video.
    ```
    Inferring using: data/audio/yongen.wav
    ```
1. While MuseTalk is inferring, sub-threads can simultaneously stream the results to the users. The generation process can achieve 30fps+ on an NVIDIA Tesla V100.
1. Set `preparation` to `False` and run this script if you want to genrate more videos using the same avatar.

##### Note for Real-time inference
1. If you want to generate multiple videos using the same avatar/video, you can also use this script to **SIGNIFICANTLY** expedite the generation process.
1. In the previous script, the generation time is also limited by I/O (e.g. saving images). If you just want to test the generation speed without saving the images, you can run
```
python -m scripts.realtime_inference --inference_config configs/inference/realtime.yaml --skip_save_images
```

# Acknowledgement
1. We thank open-source components like [whisper](https://github.com/openai/whisper), [dwpose](https://github.com/IDEA-Research/DWPose), [face-alignment](https://github.com/1adrianb/face-alignment), [face-parsing](https://github.com/zllrunning/face-parsing.PyTorch), [S3FD](https://github.com/yxlijun/S3FD.pytorch). 
1. MuseTalk has referred much to [diffusers](https://github.com/huggingface/diffusers) and [isaacOnline/whisper](https://github.com/isaacOnline/whisper/tree/extract-embeddings).
1. MuseTalk has been built on [HDTF](https://github.com/MRzzm/HDTF) datasets.

Thanks for open-sourcing!

# Limitations
- Resolution: Though MuseTalk uses a face region size of 256 x 256, which make it better than other open-source methods, it has not yet reached the theoretical resolution bound. We will continue to deal with this problem.  
If you need higher resolution, you could apply super resolution models such as [GFPGAN](https://github.com/TencentARC/GFPGAN) in combination with MuseTalk.

- Identity preservation: Some details of the original face are not well preserved, such as mustache, lip shape and color.

- Jitter: There exists some jitter as the current pipeline adopts single-frame generation.

# Citation
```bib
@article{musetalk,
  title={MuseTalk: Real-Time High Quality Lip Synchorization with Latent Space Inpainting},
  author={Zhang, Yue and Liu, Minhao and Chen, Zhaokang and Wu, Bin and Zeng, Yubin and Zhan, Chao and He, Yingjie and Huang, Junxin and Zhou, Wenjiang},
  journal={arxiv},
  year={2024}
}
```
# Disclaimer/License
1. `code`: The code of MuseTalk is released under the MIT License. There is no limitation for both academic and commercial usage.
1. `model`: The trained model are available for any purpose, even commercially.
1. `other opensource model`: Other open-source models used must comply with their license, such as `whisper`, `ft-mse-vae`, `dwpose`, `S3FD`, etc..
1. The testdata are collected from internet, which are available for non-commercial research purposes only.
1. `AIGC`: This project strives to impact the domain of AI-driven video generation positively. Users are granted the freedom to create videos using this tool, but they are expected to comply with local laws and utilize it responsibly. The developers do not assume any responsibility for potential misuse by users.
