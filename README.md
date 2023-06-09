# A stable depth fusion framework for monocular 3D object detection
The configuration file will be made public soon.
## Abstract
Monocular 3D object detection heavily relies on accurate
depth prediction. While previous methods have improved
depth accuracy through geometry priors, they typically
combine multiple depth estimates by averaging or taking
a weighted average to obtain the final depth. In this paper,
we propose a novel depth fusion framework that processes
depth estimates from different methods using a unified process. Our framework uses a powerful depth fusion module
and a loss function based on prior knowledge to improve the
accuracy and training stability of the baseline. Our method
outperforms the baseline by 4.09%, 1.94%, and 1.54% on
the KITTI 3D detection benchmark for Simple, Moderate,
and Hard settings, respectively. Our results demonstrate
the effectiveness of the proposed depth fusion framework.
<div align="center">
</div>

## Main Results

<table>
    <tr>
        <td rowspan="2",div align="center">Models</td>
        <td colspan="3",div align="center">Val, AP<sub>3D|R40</sub></td>   
    </tr>
    <tr>
        <td div align="center">Easy</td> 
        <td div align="center">Mod.</td> 
        <td div align="center">Hard</td> 
    </tr>
    <tr>
        <td rowspan="1",div align="center">MonoDETR</td>
        <td div align="center">28.84%</td> 
        <td div align="center">20.61%</td> 
        <td div align="center">16.38%</td> 
    </tr>  
    <tr>
        <td rowspan="1",div align="center">Ours</td>
        <td div align="center">30.48%</td> 
        <td div align="center">21.47%</td> 
        <td div align="center">17.76%</td> 
    </tr>  
</table>

We use the training configuration of MonoDETR (since the image enhancement methods of test set for its model has not been published) on *test* set from official [KITTI benckmark](http://www.cvlibs.net/datasets/kitti/eval_object_detail.php?&result=22a0e176d4f7794e7c142c93f4f8891749aa738f) for the car category:
<table>
    <tr>
        <td rowspan="2",div align="center">Models</td>
        <td colspan="3",div align="center">Test, AP<sub>3D|R40</sub></td>   
    </tr>
    <tr>
        <td div align="center">Easy</td> 
        <td div align="center">Mod.</td> 
        <td div align="center">Hard</td> 
    </tr>
    <tr>
        <td rowspan="1",div align="center">MonoDETR</td>
        <td div align="center">20.94%</td> 
        <td div align="center">13.67%</td> 
        <td div align="center">11.54%</td> 
    </tr>  
    <tr>
		<td rowspan="1",div align="center">Ours</td>
        <td div align="center">22.98%</td> 
        <td div align="center">14.86%</td> 
        <td div align="center">12.11%</td> 
    </tr>  
    
</table>


## Installation
1. Clone this project and create a conda environment:
    ```
    conda create -n sdf python=3.8
    conda activate sdf
    ```
    
2. Install pytorch and torchvision matching your CUDA version:
    ```
    conda install pytorch torchvision cudatoolkit
    ```
    
3. Install requirements and compile the deformable attention:
    ```
    pip install -r requirements.txt

    cd lib/models/monodetr/ops/
    bash make.sh
    
    cd ../../../..
    ```
    
4. Make dictionary for saving training losses:
    ```
    mkdir logs
    ```
 
5. Download [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=3d) datasets and prepare the directory structure as:
    ```
    │SDF/
    ├──...
    ├──data/KITTIDataset/
    │   ├──ImageSets/
    │   ├──training/
    │   ├──testing/
    ├──...
    ```
    You can also change the data path at "dataset/root_dir" in `configs/monodetr.yaml`.
    
## Get Started

### Train
You can modify the settings of models and training in `configs/monodetr.yaml` and appoint the GPU in `train.sh`:

    bash train.sh configs/monodetr.yaml > logs/monodetr.log
   
### Test
The best checkpoint will be evaluated as default. You can change it at "tester/checkpoint" in `configs/monodetr.yaml`:

    bash test.sh configs/monodetr.yaml


## Acknowlegment
This repo benefits from the excellent [MonoDETR](https://github.com/ZrrSkywalker/MonoDETR).
