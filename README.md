# people-reid
使用colab训练people reid全过程：



1，在谷歌云盘上创建colab的notebook

先把谷歌云盘关联上colab

点击 New -> More -> Connect more apps， 找到Google Colaboratory，关联上。

新建colab的notebook

点击 New -> More ->Google Colaboratory

![image](https://user-images.githubusercontent.com/88146336/129576954-70215a9c-3643-4a7b-b4d7-dc72decf3ef6.png)

![image](https://user-images.githubusercontent.com/88146336/129577113-8c1b8f4f-13a7-4690-bbe0-f5c7afa8e343.png)

2，使用免费GPU

Edit-> Notebook settings ,选择GPU

3， 执行命令（按alt+enter快捷执行）

colab这个相当于jupyter notebook，可以直接运行python 代码，

![image](https://user-images.githubusercontent.com/88146336/129577344-0b2017e2-ee98-4324-8452-872842727716.png)

这个notebook又可以执行linux下的一些命令，因为这其实是一台linux的虚拟机，只不过执行linux命令的时候前面要加!，比如：!ls , !pwd.

4，由于项目需要,这里需要安装pytorch，进行相关的配置，在colab中输入如下代码：

!pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

!pip install torchvision

!python -m pip install matplotlib

! pip install  pretrainedmodels

! pip install timm


5，把colab挂在谷歌云盘drive上，这样就可以把结果存入谷歌云盘

from google.colab import drive

drive.mount('/content/drive/')

6，进入路径

path = "/content/drive/My Drive/people"

import os

from google.colab import drive

os.chdir(path)

os.listdir(path)

7，解压谷歌云盘上的程序到colab

!unzip '/content/drive/MyDrive/people/person reid.zip' -d '/content/drive/MyDrive/people/person'

前面是压缩包路径，后面是解压后的路径。

也可以直接从GitHub上下载代码：

!git clone https://github.com/layumi/Person_reID_baseline_pytorch.git

8，进入运行目录，运行程序。（需要先更改,prapare.py train.py和test.py中的相应路径）

%cd /content/drive/MyDrive/people/person/person\ reid

数据准备：! python prepare.py

训练：! python train.py

测试：! python test.py

评估：!python evaluate_gpu.py

可视化：!python demo.py --query_index 750（0-3367）

9，如果想把文件下载到本地，运行如下代码，（先压缩，再下载到本地）

import os, tarfile

import os

from google.colab import files

def make_targz_one_by_one(output_filename, source_dir):

  tar = tarfile.open(output_filename,"w")
  
  for root,dir_name,files_list in os.walk(source_dir):
  
    for file in files_list:
    
      pathfile = os.path.join(root, file)
      
      tar.add(pathfile)
      
  tar.close()
 
  files.download(output_filename)
 
make_targz_one_by_one('peo', '/content/drive/MyDrive/people/person/person reid')

peo为压缩后文件名字，可以随意。/content/drive/MyDrive/people/person/person reid，是要下载的文件名。

10,把模型保存至谷歌drive：

#connect to self drive

from google.colab import drive

drive.mount('/content/drive')

import os

os.chdir('/content/drive/My Drive')

import torch

torch.save(model, './model.pt')。


