# cuda enabled conda docker image
# https://github.com/databricks/containers/blob/master/ubuntu/gpu/cuda-11/conda/Dockerfile
FROM databricksruntime/gpu-conda:cuda11

# Copy rapids specifications file into temp location
COPY rapids-spec_v23.02_cuda11.4_py3.8.txt /tmp/spec.txt

# Create a conda env "rapids" using the spec file and remove it after done
RUN conda create --name rapids --file /tmp/spec.txt && \
  rm -f /tmp/spec.txt

# installing build essential and gcc compiler for building libraries(hdbscan,PyMetis,etc)
# installing git for mlflow
# installing libnuma-dev for dask_cuda
RUN apt-get update \
  && apt-get upgrade -y\
  && apt-get install -y git\
  && apt-get install python-dev gcc -y\
  && apt-get install build-essential -y\
  && apt-get install libnuma-dev -y

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