# prophesee metavision SDK installation
Guide for installing Prophesee Metavision SDK on ubuntu

## Step1: Pull the Docker image on the Coder server and create a workspace 
(if installing directly on a local machine, ensure you are using Ubuntu 22.04):

```docker pull ghcr.io/chjz1024/cuda:12.4.1-cudnn-runtime-ubuntu22.04 ```


## Step 2: Add the APT repository:
```echo "deb [arch=amd64 trusted=yes] https://apt.prophesee.ai/dists/public/baiTh5si/ubuntu jammy sdk" | sudo tee /etc/apt/sources.list.d/prophesee-sdk.list```

**Note**: If the above repository becomes invalid, please contact YuliangWu.
If you have an account, get the repository by yourself:(https://support.prophesee.ai/portal/en/kb/articles/download-metavision-sdk-4-6)




## Step3: Install the Metavision SDK:
```
sudo apt update
sudo apt -y install metavision-sdk
```

## Step4: Create a Conda environment (requires Python 3.10):
```
conda create -n metavision python=3.10 -y 
conda activate metavision
```


## Step5: Make the Conda environment "see" the Metavision module installed on the system:

```
PY_DIST=/usr/lib/python3/dist-packages
SITE=$(python -c "import site; print(site.getsitepackages()[0])")
echo "$PY_DIST" > "$SITE/metavision.pth"
```

## Step6: Verify the installation:
```python -c "from metavision_core.event_io import EventsIterator; print('OK')"```


If the output is `OK`, the installation was successful.



