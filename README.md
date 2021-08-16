The whole process of using colab to train Person_reID
=====
## 1,Create a colab notebook on Google Cloud Disk
First associate Google Cloud Disk with colab  
Click New -> More -> Connect more apps, find Google Colaboratory, and connect.  
Create a new colab notebook   
Click New -> More ->Google Colaboratory  
## 2. Use free GPU  
Edit-> Notebook settings, select GPU   
## 3. Execute the command (press alt+enter to execute quickly)

colab is equivalent to jupyter notebook, you can run python code directly,

This notebook can also execute some commands under linux, because this is actually a linux virtual machine, but when you execute linux commands, you must add! In front of it, such as:
``` 
!ls, !pwd.
```
#4. Due to the needs of the project, pytorch needs to be installed here and related configuration is performed. Enter the following code in colab:
---
```
!pip install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html

!pip install torchvision

!python -m pip install matplotlib

! pip install  pretrainedmodels

! pip install timm
```
#5. Hang colab on Google Cloud Disk Drive, so that you can save the results to Google Cloud Disk:
---
```
from google.colab import drive

drive.mount('/content/drive/')
```
#6. Enter the path
---
```
path = "/content/drive/My Drive/people"

import os

from google.colab import drive

os.chdir(path)

os.listdir(path)
```
#7. Unzip the program on Google Cloud Disk to colab:
---
```
!unzip '/content/drive/MyDrive/people/person reid.zip' -d '/content/drive/MyDrive/people/person'
```
The front is the path of the compressed package, and the back is the path after decompression.

You can also download the code directly from GitHub:
```
!git clone https://github.com/layumi/Person_reID_baseline_pytorch.git
```
#8. Enter the operating directory and run the program.
---
(Need to change first, the corresponding path in prapare.py ,train.py ,and test.py)
```
%cd /content/drive/MyDrive/people/person/person\ reid
```
Data preparation:
```
python prepare.py
```
Training:
```
! python train.py
```
Test:
```
! Python test.py
```
Evaluation: 
```
!python evaluate_gpu.py
```
Visualization: 
```
!python demo.py --query_index 750 (0-3367)
```
#9. If you want to download the file to the local, run the following code
---
(compress first, then download to the local)
```
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
```
peo is the name of the compressed file, which can be anything you want. /content/drive/MyDrive/people/person/person reid is the name of the file to be downloaded.




