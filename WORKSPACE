workspace(name = "com_google_pybind11_protobuf")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.1.1/bazel-skylib-1.1.1.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.1.1/bazel-skylib-1.1.1.tar.gz",
    ],
    sha256 = "c6966ec828da198c5d9adbaa94c05e3a1c7f21bd012a0b29ba8ddbccb2c93b0d",
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()


http_archive(
    name = "com_google_absl",
    sha256 = "dcf71b9cba8dc0ca9940c4b316a0c796be8fab42b070bb6b7cab62b48f0e66c4",  # SHARED_ABSL_SHA
    strip_prefix = "abseil-cpp-20211102.0",
    urls = [
        "https://github.com/abseil/abseil-cpp/archive/refs/tags/20211102.0.tar.gz",
    ],
)

http_archive(
    name = "com_google_absl_py",
    repo_mapping = {"@six_archive": "@six"},
    sha256 = "0be59b82d65dfa1f995365dcfea2cc57989297b065fda696ef13f30fcc6c8e5b",
    strip_prefix = "abseil-py-pypi-v0.15.0",
    urls = [
        "https://github.com/abseil/abseil-py/archive/refs/tags/pypi-v0.15.0.tar.gz",
    ],
)

# Six is a dependency of com_google_absl_py
http_archive(
    name = "six_archive",
    urls = [
        "http://mirror.bazel.build/pypi.python.org/packages/source/s/six/six-1.10.0.tar.gz",
        "https://pypi.python.org/packages/source/s/six/six-1.10.0.tar.gz",
    ],
    sha256 = "105f8d68616f8248e24bf0e9372ef04d3cc10104f1980f54d57b2ce73a5ad56a",
    strip_prefix = "six-1.10.0",
    build_file = "@com_google_absl_py//third_party:six.BUILD",
)

## `pybind11_bazel`
# See https://github.com/pybind/pybind11_bazel
http_archive(
  name = "pybind11_bazel",
  strip_prefix = "pybind11_bazel-72cbbf1fbc830e487e3012862b7b720001b70672",
  sha256 = "516c1b3a10d87740d2b7de6f121f8e19dde2c372ecbfe59aef44cd1872c10395",
  urls = ["https://github.com/pybind/pybind11_bazel/archive/72cbbf1fbc830e487e3012862b7b720001b70672.tar.gz"],
)

# We still require the pybind library.
http_archive(
  name = "pybind11",
  build_file = "@pybind11_bazel//:pybind11.BUILD",
  strip_prefix = "pybind11-master",
  urls = ["https://github.com/pybind/pybind11/archive/refs/heads/master.tar.gz"],
)

load("@pybind11_bazel//:python_configure.bzl", "python_configure")
python_configure(name = "local_config_python")

# proto_library, cc_proto_library, and java_proto_library rules implicitly
# depend on @com_google_protobuf for protoc and proto runtimes.
# This statement defines the @com_google_protobuf repo.
http_archive(
    name = "com_google_protobuf",
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz"],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")
protobuf_deps()

# GRPC v1.42, for proto rules.
# For a related discussion of the pro/cons of various open-source py proto rule
# repositories, see b/189457935.
http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "9f387689b7fdf6c003fd90ef55853107f89a2121792146770df5486f0199f400",
    strip_prefix = "grpc-1.42.0",
    urls = ["https://github.com/grpc/grpc/archive/v1.42.0.zip"],
)

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()

bind(
    name = "python_headers",
    actual = "@local_config_python//:python_headers",
)
