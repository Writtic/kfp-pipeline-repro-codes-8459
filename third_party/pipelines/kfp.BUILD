load("@com_google_protobuf//:protobuf.bzl", "py_proto_library")

package(default_visibility = ["//visibility:public"])

genrule(
    name = "pipeline_spec_proto",
    srcs = ["api/v2alpha1/pipeline_spec.proto"],
    outs = ["pipeline_spec.proto"],
    cmd = "cp -rp $(SRCS) $(OUTS)",
)

py_proto_library(
    name = "pipeline_spec_proto_py_pb2",
    srcs = ["pipeline_spec.proto"],
    deps = [
        "@com_google_protobuf//:protobuf_python",
        "@com_google_googleapis//google/rpc:status_proto_py_pb2",
    ],
)
