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
    python train_tensorflow.py
    dvc add model.h5


**dvc get** can download any file or directory tracked in a DVC repository (and stored remotely). It's like wget, but for DVC or Git repos.


https://dvc.org/doc/use-cases/versioning-data-and-model-files/tutorial
https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html