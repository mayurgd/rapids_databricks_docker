# Failed Trials

----
>rapidsai-core:23.02-cuda11.8-runtime-ubuntu20.04-py3.10
----
- build succeeded

**for dbx_runtime 10.4LTS and 11.4LTS**
- cluster startup failed

```python
cannot import name 'Iterable' from 'collections' (/databricks/python/lib/python3.10/collections/init.py)
```
collections script udpated in py3.10, databricks not in sync with py3.10

----
>rapidsai-core:23.02-cuda11.8-runtime-ubuntu20.04-py3.8
----
- build succeeded

**for dbx_runtime 10.4LTS**
- cluster startup succeeded
- code run fails

```python
LinkerError: [222] Call to cuLinkAddData results in UNKNOWN_CUDA_ERROR
ptxas application ptx input, line 9; fatal   : Unsupported .version 7.8; current version is '7.4'
```
maybe not compatible with cuda11.8 ?


**for dbx_runtime 11.4LTS**
- cluster startup fails

```
Spark error: Driver down cause: driver state change
```

