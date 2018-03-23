
# One-shot Learning for Semantic Segmentation (OSLSM)

By Amirreza Shaban, Shray Bansal, Zhen Liu, Irfan Essa and Byron Boots

### Paper

You can find our paper at https://arxiv.org/abs/1709.03410


### Citation

If you find OSLSM useful in your research, please consider to cite:

 @inproceedings{shaban2017one,
	  title={One-Shot Learning for Semantic Segmentation},
	  author={Shaban, Amirreza and Bansal, Shray and Liu, Zhen and Essa, Irfan and Boots, Byron},
	  journal={arXiv preprint arXiv:1709.03410},
	  year={2017}
 }


### Instructions for Testing (tested on Ubuntu 16.04)
We assume you have downloaded the repository into ${OSLSM_HOME} path.

1. Install Caffe prerequisites and build the Caffe code (with PyCaffe). See http://caffe.berkeleyvision.org/installation.html for more details

```shell 
cd ${OSLSM_HOME}
mkdir build
cd build
cmake ..
make all -j8
```

If you prefer Make, set BLAS to your desired one in Makefile.config. Then run:

```shell
cd ${OSLSM_HOME}
make all -j8
make pycaffe
```

2. Update the `$PYTHONPATH`: 

```shell
export PYTHONPATH=${OSLSM_HOME}/OSLSM/code:${OSLSM_HOME}/python:$PYTHONPATH
```

3. Download PASCAL VOC dataset: http://host.robots.ox.ac.uk/pascal/VOC/voc2012/

4. Download trained models from: https://gtvault-my.sharepoint.com/:u:/g/personal/ashaban6_gatech_edu/EXS5Cj8nrL9CnIJjv5YkhEgBQt9WAcIabDQv22AERZEeUQ

5. Set `CAFFE_PATH=${OSLSM_HOME}` and `PASCAL_PATH` in `${OSLSM_HOME}/OSLSM/code/db_path.py` file

6. Run the following to test the models in one-shot setting:

```shell
cd ${OSLSM_HOME}/OSLSM/os_semantic_segmentation
python test.py deploy_1shot.prototxt ${TRAINED_MODEL} ${RESULTS_PATH} 1000 fold${FOLD_ID}_1shot_test
```

Where ${FOLD_ID} can be 0,1,2, or 3 and ${TRAIN_MODEL} is the path to the trained caffe model. Please note that we have included different caffe models for each ${FOLD_ID}.

Simillarly, run the following to test the models in 5-shot setting:

```shell
cd ${OSLSM_HOME}/OSLSM/os_semantic_segmentation
python test.py deploy_5shot.prototxt ${TRAINED_MODEL} ${RESULTS_PATH} 1000 fold${FOLD_ID}_5shot_test
```

7. For training your own models, we have included all prototxts in `${OSLSM_HOME}/OSLSM/os_semantic_segmentation/training` directory and the vgg pre-trained model can be found in `snapshots/os_pretrained.caffemodel`.

You will also need to

1) Download/Prepare SBD dataset (http://home.bharathh.info/pubs/codes/SBD/download.html).

2) Set `SBD_PATH` in `${OSLSM_HOME}/OSLSM/code/db_path.py`

3) Set the profile to `fold${FOLD_ID}\_train` for our data layer (check the prototxt files and `${OSLSM_HOME}/OSLSM/code/ss_datalayer.py`) to work.



## my result

python test.py deploy_1shot.prototxt training/snapshots/fold0/ss_os_fc_iter_60000.caffemodel 1shot_fold0_test 1000 fold0_1shot_test

mIOU=34.6

python test.py deploy_5shot.prototxt training/snapshots/fold0/ss_os_fc_iter_60000.caffemodel 5shot_fold0_test 1000 fold0_5shot_test

mIoU = 39.9




