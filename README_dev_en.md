# For Developper

## Prerequisites

- ~~Linux(ubuntu, debian) or WSL2, (not tested for other linux distributions and Mac)~~

###### Should now work with all operating systems and all environments by using generic Python infrastructure!<br>
###### Please report if any breakages occur due to this build change.

- Python 3.10 (Broken on 3.11 and above)

## Preparation

1. Clone repository

```bash
$ git clone https://github.com/w-okada/voice-changer.git voice-changer-webserver
```

2. Create a *NORMAL* venv like a *normal* person

```bash
$ cd voice-changer-webserver
$ python3.10 -m venv venv    # This creates a folder venv/ within the repository folder. It's added to .gitignore, so it won't be tracked.
```

3. Activate venv (this is different for every OS, but inspect the venv/bin/ folder to get a general idea for which script you want to run for your OS)

```bash
$ source venv/bin/activate   # You cannot execute this script directly, it MUST be sourced
```
TODO: Add the specific steps from other operating systems as alternative commands
TODO: Clarify/fix for ZSH and other non-Bash shells

## For Server Developer

1. Install requirements

```bash
$ cd server
$ python3.10 -m pip install -U pip setuptools wheel
$ python3.10 -m pip install -r requirements.txt
$ python3.10 -m pip install fairseq pyworld
```
TODO: Look through requirements.txt to see which libraries need to be swapped out for different CPU/GPU configurations, such as NVIDIA, AMD, No GPU, or Apple Silicon

2. Run server

Run server with the below command. You can replace the path to each weight.

```bash
$ python3.10 MMVCServerSIO.py -p 18888 --https true \
    --content_vec_500 pretrain/checkpoint_best_legacy_500.pt  \
    --content_vec_500_onnx pretrain/content_vec_500.onnx \
    --content_vec_500_onnx_on true \
    --hubert_base pretrain/hubert_base.pt \
    --hubert_base_jp pretrain/rinna_hubert_base_jp.pt \
    --hubert_soft pretrain/hubert/hubert-soft-0d54a1f4.pt \
    --nsf_hifigan pretrain/nsf_hifigan/model \
    --crepe_onnx_full pretrain/crepe_onnx_full.onnx \
    --crepe_onnx_tiny pretrain/crepe_onnx_tiny.onnx \
    --rmvpe pretrain/rmvpe.pt \
    --model_dir model_dir \
    --samples samples.json
```

Access with Browser (currently only chrome is supported), then you can see gui.
TODO: Fix this so other browsers can be used? Pipewire integration? Could be a fun adventure

3. Enjoy developing.

### Troubleshoot

1. OSError: PortAudio library not found

If you get the message below, you shold install additional library.

```
OSError: PortAudio library not found
```

You can install the library this command.

```bash
$ sudo apt-get install libportaudio2
$ sudo apt-get install libasound-dev
```

2. It's not starting up! Damn software!

The client will not start automatically. Please launch your browser and access the URL displayed on the console. And watch your words.

3. Could not load library libcudnn_cnn_infer.so.8

When using WSL, you might encounter a message saying `Could not load library libcudnn_cnn_infer.so.8. Error: libcuda.so: cannot open shared object file: No such file or directory`. This often happens because the path hasn't been properly set. Please set the path as shown below. It might be handy to add this to your launch script, such as .bashrc.

```
export LD_LIBRARY_PATH=/usr/lib/wsl/lib:$LD_LIBRARY_PATH
```

- reference
  - https://qiita.com/cacaoMath/items/811146342946cdde5b83
  - https://github.com/microsoft/WSL/issues/8587

### Appendix

1. Win + Anaconda (not supported)

use conda to install pytorch

```
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

Also run these command.

```bash
pip install chardet
pip install numpy==1.24.0
```

## For Client Developer

1. Import modules and initial build

```bash
cd client
cd lib
npm install
npm run build:dev
cd ../demo
npm install
npm run build:dev
```

2. Enjoy developing.
