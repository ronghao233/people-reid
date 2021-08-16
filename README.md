# people-reid
使用colab训练people reid全过程：



1，在谷歌云盘上创建colab的notebook

先把谷歌云盘关联上colab
点击 New -> More -> Connect more apps， 找到Google Colaboratory，关联上。

新建colab的notebook
点击 New -> More ->Google Colaboratory

![image](https://user-images.githubusercontent.com/88146336/129576954-70215a9c-3643-4a7b-b4d7-dc72decf3ef6.png)







1，首先，需要进行相关的配置，在colab中输入如下代码：

!pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

! pip install torchvision

!python -m pip install matplotlib

! pip install  pretrainedmodels

! pip install timm

2，把colab挂在谷歌云盘上，这样就可以把结果存入谷歌云盘：

from google.colab import drive

drive.mount('/content/drive/')
3，进入路径：
path = "/content/drive/My Drive/people"
import os
from google.colab import drive
os.chdir(path)
os.listdir(path)

4，把谷歌云盘上的代码压缩包解压到colab上
!unzip '/content/drive/MyDrive/people/person reid.zip' -d '/content/drive/MyDrive/people/person'

前面是压缩包路径，后面是解压后的路径。

也可以直接从GitHub上下载代码
5，进入运行目录，运行程序。（需要先更改train.py和test.py中的相应路径）
%cd /content/drive/MyDrive/people/person/person\ reid

训练：! python train.py

测试：! python test.py

评估：!python evaluate_gpu.py

可视化：!python demo.py --query_index 750（1-）

6，如果想把文件下载到本地，运行如下代码，（先压缩，再下载到本地）
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

