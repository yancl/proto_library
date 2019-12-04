load("@rules_cc//cc:defs.bzl", "cc_library")
load("@rules_java//java:defs.bzl", "java_library")
load("@io_bazel_rules_go//proto:def.bzl", "go_proto_library")
load("@rules_proto//proto:defs.bzl", "proto_library")
load("@com_github_grpc_grpc//bazel:cc_grpc_library.bzl", "cc_grpc_library")
load("@com_github_grpc_grpc//bazel:python_rules.bzl", "py_proto_library", "py_grpc_library")
load("@io_grpc_grpc_java//:java_grpc_library.bzl", "java_grpc_library")

# Convention:
# A java_proto_library that wraps a proto_library named foo_proto
# should be called foo_java_proto.
#
# Note that you only need a java_proto_library for the protos
# you directly use in your code - a java_proto_library converts
# an entire proto graph.
java_proto_library(
    name = "person_java_proto",
    deps = [":person_proto"],
)

# Convention:
# A java_lite_proto_library that wraps a proto_library named foo_proto
# should be called foo_java_proto_lite.
java_lite_proto_library(
    name = "person_java_proto_lite",
    deps = [":person_proto"],
)

java_grpc_library(
    name = "person_java_grpc",
    srcs = [":person_proto"],
    deps = [":person_java_proto"],
)

# Convention:
# A cc_proto_library that wraps a proto_library named foo_proto
# should be called foo_cc_proto.
cc_proto_library(
    name = "person_cc_proto",
    deps = [":person_proto"],
)

cc_grpc_library(
    name = "person_cc_grpc",
    srcs = [":person_proto"],
    grpc_only = True,
    deps = [":person_cc_proto"],
)

# Convention:
# A py_proto_library that wraps a proto_library named foo_proto
# should be called foo_py_proto.
py_proto_library(
    name = "person_py_proto",
    deps = [":person_proto"],
)

py_grpc_library(
    name = "person_py_grpc",
    srcs = [":person_proto"],
    deps = [":person_py_proto"],
)

# Convention:
# A go_proto_library that wraps a proto_library named foo_proto
# should be called foo_go_proto.
go_proto_library(
    name = "zip_code_go_proto",
    proto = ":zip_code_proto",
    importpath = "github.com/yancl/proto_library/src/zip_code",
    visibility = ["//visibility:public"],
)

go_proto_library(
    name = "address_go_proto",
    proto = ":address_proto",
    deps = [
    	":zip_code_go_proto",
    ],
    # each file.go should use different importpath
    # see: https://github.com/bazelbuild/rules_go/issues/1841
    importpath = "github.com/yancl/proto_library/src/address",
    visibility = ["//visibility:public"],
)

go_proto_library(
    name = "person_go_proto",
    compilers = ["@io_bazel_rules_go//proto:go_grpc"],
    proto = ":person_proto",
    importpath = "github.com/yancl/proto_library/src/person",
    visibility = ["//visibility:public"],
    deps = [
        ":address_go_proto",
        "@go_googleapis//google/api:annotations_go_proto",
    ]
)


# Conventions:
# 1. One proto_library rule per .proto file.
# 2. A file named foo.proto will be in a rule named foo_proto.
proto_library(
    name = "person_proto",
    srcs = ["person.proto"],
    deps = [
        ":address_proto",
        # Well known protos should be included as deps in the
        # proto_library rules of the source files importing them.
        # A list of all @com_google_protobuf well known protos can
        # seen with:
        # `bazel query 'kind(proto_library, @com_google_protobuf//:all)'`
        "@com_google_protobuf//:any_proto",
        "@go_googleapis//google/api:annotations_proto",
    ],
)

proto_library(
    name = "address_proto",
    srcs = ["address.proto"],
    deps = [":zip_code_proto"],
)

proto_library(
    name = "zip_code_proto",
    srcs = ["zip_code.proto"],
)


# one library and one proto
proto_library(
    name = "all_proto",
    srcs = ["person.proto", "zip_code.proto", "address.proto"],
    deps = [
        # Well known protos should be included as deps in the
        # proto_library rules of the source files importing them.
        # A list of all @com_google_protobuf well known protos can
        # seen with:
        # `bazel query 'kind(proto_library, @com_google_protobuf//:all)'`
        "@com_google_protobuf//:any_proto",
        "@go_googleapis//google/api:annotations_proto",
    ],
)

go_proto_library(
    name = "all_go_proto",
    compilers = ["@io_bazel_rules_go//proto:go_grpc"],
    proto = ":all_proto",
    importpath = "github.com/yancl/proto_library/src",
    visibility = ["//visibility:public"],
    deps = [
        "@go_googleapis//google/api:annotations_go_proto",
    ]
)
