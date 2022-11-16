workspace(name = "reproduce")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# == Protobuf dependencies

_protobuf_version = "3.19.4"

http_archive(
    name = "com_google_protobuf",
    sha256 = "3bd7828aa5af4b13b99c191e8b1e884ebfa9ad371b0ce264605d347f135d2568",
    strip_prefix = "protobuf-{}".format(_protobuf_version),
    urls = [
        "https://mirror.bazel.build/github.com/protocolbuffers/protobuf/archive/v{}.tar.gz".format(_protobuf_version),
        "https://github.com/protocolbuffers/protobuf/archive/v{}.tar.gz".format(_protobuf_version),
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# == Dev dependencies

# Buildifier requires io_bazel_rules_go

_bazel_rules_go_version = "0.29.0"

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "2b1641428dff9018f9e85c0384f03ec6c10660d935b750e3fa1492a281a53b0f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v{version}/rules_go-v{version}.zip".format(version=_bazel_rules_go_version),
        "https://github.com/bazelbuild/rules_go/releases/download/v{version}/rules_go-v{version}.zip".format(version=_bazel_rules_go_version),
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.17.2")

_bazel_buildtools_version = "4.2.2"

http_archive(
    name = "com_github_bazelbuild_buildtools",
    sha256 = "ae34c344514e08c23e90da0e2d6cb700fcd28e80c02e23e4d5715dddcb42f7b3",
    strip_prefix = "buildtools-{}".format(_bazel_buildtools_version),
    url = "https://github.com/bazelbuild/buildtools/archive/refs/tags/{}.tar.gz".format(_bazel_buildtools_version),
)

# == Kubeflow Pipelines dependencies

# googleapis requires grpc

_grpc_version = "1.47.0"

http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "edf25f4db6c841853b7a29d61b0980b516dc31a1b6cdc399bcf24c1446a4a249",
    strip_prefix = "grpc-%s" % _grpc_version,
    urls = ["https://github.com/grpc/grpc/archive/v%s.zip" % _grpc_version],
)

# kubeflow/pipelines requires googleapis

_googleapis_version = "2f9af297c84c55c8b871ba4495e01ade42476c92"

http_archive(
    name = "com_google_googleapis",
    patch_args = ["-p1"],
    patches = ["//third_party/googleapis:rpc.patch"],
    sha256 = "5bb6b0253ccf64b53d6c7249625a7e3f6c3bc6402abd52d3778bfa48258703a0",
    strip_prefix = "googleapis-%s" % _googleapis_version,
    urls = [
        "https://storage.googleapis.com/grpc-bazel-mirror/github.com/googleapis/googleapis/archive/%s.tar.gz" % _googleapis_version,
        "https://github.com/googleapis/googleapis/archive/%s.tar.gz" % _googleapis_version,
    ],
)

load("@com_google_googleapis//:repository_rules.bzl", "switched_rules_by_language")

switched_rules_by_language(
    name = "com_google_googleapis_imports",
    python = True,
)

_kfp_version = "1.8.14"

http_archive(
    name = "com_github_kubeflow_pipelines",
    build_file = "//third_party/pipelines:kfp.BUILD",
    sha256 = "84d6ea9cfba09b29e5180b306823b0ff140487a05479463edb1e2c415a5b3043",
    strip_prefix = "pipelines-%s" % _kfp_version,
    url = "https://github.com/kubeflow/pipelines/archive/refs/tags/%s.zip" % _kfp_version,
)
