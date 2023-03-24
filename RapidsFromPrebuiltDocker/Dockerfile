# Prebuilt Docker image for Rapids
# https://github.com/databricks/containers/tree/master/ubuntu/gpu/cuda-11/rapids
FROM databricksruntime/gpu-rapids:cuda11

# installing build essential and gcc compiler for building libraries(hdbscan,PyMetis,etc)
# installing git for mlflow
# installing libnuma-dev for dask_cuda
RUN apt-get update \
    && apt-get upgrade -y\
    && apt-get install -y git\
    && apt-get install python-dev gcc -y\
    && apt-get install build-essential -y\
    && apt-get install libnuma-dev -y

# update llvmlite package for numba dependency
RUN /databricks/conda/envs/rapids/bin/pip install llvmlite==0.39.1 --ignore-installed

# install additionally req packages within rapids conda environment
WORKDIR /je_env
COPY requirements.txt /je_env/requirements.txt
RUN /databricks/conda/envs/rapids/bin/pip install -r requirements.txt

# download required nltk packages
RUN /databricks/conda/envs/rapids/bin/python3 -c "import nltk; nltk.download(['punkt', 'stopwords', 'wordnet', 'omw-1.4'])"

# Set environment variables required in Databricks
ENV MLFLOW_TRACKING_URI=databricks
ENV DEFAULT_DATABRICKS_ROOT_CONDA_ENV=rapids
ENV PYSPARK_PYTHON=/databricks/conda/envs/rapids/bin/python3
ENV LD_LIBRARY_PATH=/usr/local/cuda-11.0/compat