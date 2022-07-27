# cat_vs_dog
Building image classification models using little data.

---
## Download data


    python3 -m venv .env
    source .env/bin/activate
    pip install -r requirements.txt
    dvc init
    dvc get https://github.com/iterative/dataset-registry \
            tutorials/versioning/data.zip
    unzip -q data.zip
    rm -f data.zip
    dvc add data
    dvc stage add -n featurize -d src/featurization.py -d data \
        -p featurize.img_width,featurize.img_height,featurize.nb_validation_samples, featurize.batch_size \
        -o bottleneck_features_train.npy \
        -o bottleneck_features_validation.npy \
        python src/featurization.py data/
          
    dvc run -n train -d train_tensorflow.py -d src/train_tensorflow.py \
        -p train.epochs, featurize.nb_validation_samples, featurize.batch_size
        -o model.h5 -M evaluation.json \
        python src/train_tensorflow.py features/


**dvc get** can download any file or directory tracked in a DVC repository (and stored remotely). It's like wget, but for DVC or Git repos.


https://dvc.org/doc/use-cases/versioning-data-and-model-files/tutorial
https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html