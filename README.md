### Environment

*  KFP version: 1.8.13
<!-- For more information, see an overview of KFP installation options: https://www.kubeflow.org/docs/pipelines/installation/overview/. -->
*  All dependencies version:
  * kfp==1.8.13
  * kfp-pipeline-spec==0.1.16
  * kfp-server-api==1.8.4
<!-- Specify the output of the following shell command: $pip list | grep kfp -->


### Steps to reproduce

Based on [kfp-pipeline-repro-codes-8459](https://github.com/Writtic/kfp-pipeline-repro-codes-8459)

```bash
bazel run //tools:gen_proto
python main.py
```

### Expected result

Using `py_proto_library()` from com_google_protobuf, I hope to use the part of pipeline_spec.proto on [kubeflow/pipelines](https://github.com/kubeflow/pipelines) for reusability and integrity.
However, [kubeflow/pipelines](https://github.com/kubeflow/pipelines) has different package path from protobuf path, so I can't use as it is.

Due to this, I add the dependancy of [kubeflow/pipelines](https://github.com/kubeflow/pipelines) and bazel patches, build file for [kubeflow/pipelines](https://github.com/kubeflow/pipelines).

As a result, I can get [pipeline_config_pb2.py](reproduce/proto/pipeline_config_pb2.py) with gen_proto.sh which is simply copy `*_pb2.py` file from bazel runtime environment.

But `pipeline_config_pb2.py` refers to `kfp.pipeline_spec` which is in `kfp-pipeline-spec` python package in python runtime eventually.
And even the protobuf file of `kfp.pipeline_spec` has no subpackage path.

This bring some problem like below.
- Protobuf file, [pipeline_config.proto](reproduce/proto/pipeline_config.proto), should use `import "pipeline_spec.proto";`
- `pb2.py` file, [pipeline_config_pb2.py](reproduce/proto/pipeline_config_pb2.py), should use `from kfp.pipeline_spec import pipeline_spec` because of `kfp-pipeline-spec`


### Materials and Reference

- Github Repository: [kfp-pipeline-repro-codes-8459](https://github.com/Writtic/kfp-pipeline-repro-codes-8459)

<!-- Help us debug this issue by providing resources such as: sample code, background context, or links to references. -->

---

<!-- Don't delete message below to encourage users to support your issue! -->
Impacted by this bug? Give it a 👍.
