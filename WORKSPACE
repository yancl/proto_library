workspace(name = "com_github_cgrushko_proto_library")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# rules_cc defines rules for generating C++ code from Protocol Buffers.
http_archive(
    name = "rules_cc",
    sha256 = "35f2fb4ea0b3e61ad64a369de284e4fbbdcdba71836a5555abb5e194cf119509",
    strip_prefix = "rules_cc-624b5d59dfb45672d4239422fa1e3de1822ee110",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_cc/archive/624b5d59dfb45672d4239422fa1e3de1822ee110.tar.gz",
        "https://github.com/bazelbuild/rules_cc/archive/624b5d59dfb45672d4239422fa1e3de1822ee110.tar.gz",
    ],
)

# rules_java defines rules for generating Java code from Protocol Buffers.
http_archive(
    name = "rules_java",
    sha256 = "ccf00372878d141f7d5568cedc4c42ad4811ba367ea3e26bc7c43445bbc52895",
    strip_prefix = "rules_java-d7bf804c8731edd232cb061cb2a9fe003a85d8ee",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_java/archive/d7bf804c8731edd232cb061cb2a9fe003a85d8ee.tar.gz",
        "https://github.com/bazelbuild/rules_java/archive/d7bf804c8731edd232cb061cb2a9fe003a85d8ee.tar.gz",
    ],
)

# java_lite_proto_library rules implicitly depend on @com_google_protobuf_javalite//:javalite_toolchain,
# which is the JavaLite proto runtime (base classes and common utilities).
http_archive(
    name = "com_google_protobuf_javalite",
    sha256 = "a8cb9b8db16aff743a4bc8193abec96cf6ac0b0bc027121366b43ae8870f6fd3",
    strip_prefix = "protobuf-fa08222434bc58d743e8c2cc716bc219c3d0f44e",
    urls = [
        "https://github.com/google/protobuf/archive/fa08222434bc58d743e8c2cc716bc219c3d0f44e.zip",
    ],
)

# rules_go defines rules for generating Go code from Protocol Buffers
http_archive(
    name = "io_bazel_rules_go",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.20.2/rules_go-v0.20.2.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.20.2/rules_go-v0.20.2.tar.gz",
    ],
    sha256 = "b9aa86ec08a292b97ec4591cf578e020b35f98e12173bbd4a921f84f583aebd9",
)

# rules_proto defines abstract rules for building Protocol Buffers.
http_archive(
    name = "rules_proto",
    sha256 = "57001a3b33ec690a175cdf0698243431ef27233017b9bed23f96d44b9c98242f",
    strip_prefix = "rules_proto-9cd4f8f1ede19d81c6d48910429fe96776e567b1",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/9cd4f8f1ede19d81c6d48910429fe96776e567b1.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/9cd4f8f1ede19d81c6d48910429fe96776e567b1.tar.gz",
    ],
)

# cpp grpc related
http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "ae0be9dcee70a25b38dfd2a0fe22839ea9beb5a2c3f180b0c5b4174fa37f3e93",
    strip_prefix = "grpc-5817f6287d758ead304668ea6e7819fd9a4c3dcb",
    urls = [
        "https://github.com/grpc/grpc/archive/5817f6287d758ead304668ea6e7819fd9a4c3dcb.tar.gz",
    ],
)


# gazelle 
http_archive(
    name = "bazel_gazelle",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/bazel-gazelle/releases/download/v0.19.1/bazel-gazelle-v0.19.1.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.19.1/bazel-gazelle-v0.19.1.tar.gz",
    ],
    sha256 = "86c6d481b3f7aedc1d60c1c211c6f76da282ae197c3b3160f54bd3a8f847896f",
)

load("@rules_cc//cc:repositories.bzl", "rules_cc_dependencies")
rules_cc_dependencies()

load("@rules_java//java:repositories.bzl", "rules_java_dependencies", "rules_java_toolchains")
rules_java_dependencies()
rules_java_toolchains()

load("@io_bazel_rules_go//go:deps.bzl", "go_rules_dependencies", "go_register_toolchains")
go_rules_dependencies()
go_register_toolchains()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()

# go grpc deps
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")
gazelle_dependencies()

go_repository(
    name = "org_golang_google_grpc",
    build_file_proto_mode = "disable",
    importpath = "google.golang.org/grpc",
    sum = "h1:J0UbZOIrCAl+fpTOf8YLs4dJo8L/owV4LYVtAXQoPkw=",
    version = "v1.22.0",
)

go_repository(
    name = "org_golang_x_net",
    importpath = "golang.org/x/net",
    sum = "h1:oWX7TPOiFAMXLq8o0ikBYfCJVlRHBcsciT5bXOrH628=",
    version = "v0.0.0-20190311183353-d8887717615a",
)

go_repository(
    name = "org_golang_x_text",
    importpath = "golang.org/x/text",
    sum = "h1:g61tztE5qeGQ89tm6NTjjM9VPIm088od1l6aSorWRWg=",
    version = "v0.3.0",
)

# cpp grpc deps
load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()

load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")
grpc_extra_deps()

#load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")
#protobuf_deps()

#load("@io_bazel_rules_python//python:pip.bzl", "pip_import", "pip_repositories")
#pip_import(
#    name = "grpc_python_dependencies",
#    requirements = "@com_github_grpc_grpc//:requirements.bazel.txt",
#)
#load("@grpc_python_dependencies//:requirements.bzl", "pip_install")
#pip_repositories()
#pip_install()
