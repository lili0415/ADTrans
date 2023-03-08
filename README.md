# ADTrans
## Steps to get started
To setup the environment, we use `conda` to manage our dependencies.

Our developers use `CUDA 10.1` to do experiments.

You can specify the appropriate `cudatoolkit` version to install on your machine in the `environment.yml` file, and then run the following to create the `conda` environment:
```bash
conda env create -f environment.yml
```
You shall manually install the following dependencies.
```bash
# Install mmcv
## CAUTION: The latest versions of mmcv 1.5.3, mmdet 2.25.0 are not well supported, due to bugs in mmdet.
pip install mmcv-full==1.4.3 -f https://download.openmmlab.com/mmcv/dist/cu101/torch1.7.0/index.html

# Install mmdet
pip install openmim
mim install mmdet==2.20.0

# Install coco panopticapi
pip install git+https://github.com/cocodataset/panopticapi.git

# For visualization
conda install -c conda-forge pycocotools
pip install detectron2==0.5 -f \
  https://dl.fbaipublicfiles.com/detectron2/wheels/cu101/torch1.7/index.html

# If you're using wandb for logging
pip install wandb
wandb login

# If you develop and run openpsg directly, install it from source:
pip install -v -e .
# "-v" means verbose, or more output
# "-e" means installing a project in editable mode,
# thus any local modifications made to the code will take effect without reinstallation.
```

Original [Datasets](https://entuedu-my.sharepoint.com/:f:/g/personal/jingkang001_e_ntu_edu_sg/EgQzvsYo3t9BpxgMZ6VHaEMBDAb7v0UgI8iIAExQUJq62Q?e=fIY3zh) and [pretrained models](https://entuedu-my.sharepoint.com/:f:/g/personal/jingkang001_e_ntu_edu_sg/ErQ4stbMxp1NqP8MF8YPFG8BG-mt5geOrrJfAkeitjzASw?e=9taAaU) are provided. Please unzip the files if necessary.

Our codebase accesses the datasets from `./data/` and pretrained models from `./work_dirs/checkpoints/` by default.

Our checkpoint is available at:

https://drive.google.com/file/d/1EWcqu8HHt2ClufKVUMY_fvrSdJjgln3Y/view?usp=sharing

Our new annotation for PSG dataset is available at:

https://drive.google.com/file/d/1X4WSryDo0BE5uEWBSY1v0vrLp2jtPQi5/view?usp=sharing

Users should change the json filename in config/_base_/datasets/psg.py (Line 4-5) to './data/psg/psg.json'.

## Testing
Run the scripts below:
```bash
PYTHONPATH='.':$PYTHONPATH  \
python tools/test.py  \
configs/psgtr/psgtr_r50_psg.py \
work_dirs/PATH_TO_CHECKPOINT \
--eval sgdet
```

