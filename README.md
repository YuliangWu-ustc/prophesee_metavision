# prophesee_metavision
Guide for installing Prophesee Metavision SDK on ubuntu

Step1: coder服务器输入镜像并创建workspace，（如果是直接在本机安装需要保证ubuntu22.04）：

```docker pull ghcr.io/chjz1024/cuda:12.4.1-cudnn-runtime-ubuntu22.04 ```


Step2: 添加apt源：
```echo "deb [arch=amd64 trusted=yes] https://apt.prophesee.ai/dists/public/baiTh5si/ubuntu jammy sdk" | sudo tee /etc/apt/sources.list.d/prophesee-sdk.list```

p.s. 以上apt源的来源，如果失效请联系wyl：https://support.prophesee.ai/portal/en/kb/articles/download-metavision-sdk-4-6



Step3: 安装metavision sdk：
```
sudo apt update
sudo apt -y install metavision-sdk
```

Step4: 创建conda环境(需要python3.10)：
```
conda create -n metavision python=3.10 -y 
conda activate metavision
```


Step5: 让这个 conda 环境“看到”系统里的 Metavision 模块：

```
PY_DIST=/usr/lib/python3/dist-packages
SITE=$(python -c "import site; print(site.getsitepackages()[0])")
echo "$PY_DIST" > "$SITE/metavision.pth"
```

Step6: 测试是否成功：
```python -c "from metavision_core.event_io import EventsIterator; print('OK')"```

输出OK则成功


