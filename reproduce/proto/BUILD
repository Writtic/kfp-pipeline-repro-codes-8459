load("@com_google_protobuf//:protobuf.bzl", "py_proto_library")


package(default_visibility = ["//:__subpackages__"])


py_proto_library(
    name = "pipeline_config_proto_py_pb2",
    srcs = ["pipeline_config.proto"],
    deps = [
        "@com_github_kubeflow_pipelines//:pipeline_spec_proto_py_pb2",
    ],
)

py_library(
    name = "proto",
    data = [
        ":pipeline_config_pb2.py",
    ],
)
