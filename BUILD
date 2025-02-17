# Copyright 2019 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@com_github_grpc_grpc//bazel:grpc_build_system.bzl", "grpc_proto_library")

grpc_proto_library(
    name = "match_proto",
    srcs = ["match.proto"],
)

cc_library(
    name = "client_lib",
    srcs = ["client_lib.cc"],
    hdrs = ["client_lib.h"],
    deps = [
        ":match_proto",
        "//crypto:bn_util",
        "//crypto:ec_commutative_cipher",
        "//crypto:paillier",
        "//util:status",
        "//util:status_includes",
        "@com_google_absl//absl/memory",
    ],
)

cc_library(
    name = "server_lib",
    srcs = ["server_lib.cc"],
    hdrs = ["server_lib.h"],
    deps = [
        ":match_proto",
        "//crypto:bn_util",
        "//crypto:ec_commutative_cipher",
        "//crypto:paillier",
        "//util:status",
        "//util:status_includes",
        "@com_google_absl//absl/memory",
    ],
)

cc_library(
    name = "data_util",
    srcs = ["data_util.cc"],
    hdrs = ["data_util.h"],
    deps = [
        ":match_proto",
        "//crypto:bn_util",
        "//util:status",
        "//util:status_includes",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/strings",
    ],
)

cc_binary(
    name = "generate_dummy_data",
    srcs = ["generate_dummy_data.cc"],
    deps = [
        ":data_util",
        "@com_github_gflags_gflags//:gflags",
        "@com_github_glog_glog//:glog",
        "@com_google_absl//absl/base",
    ],
)
cc_library(
    name = "private_join_and_compute_rpc_impl",

    srcs = ["private_join_and_compute_rpc_impl.cc"],
    hdrs = ["private_join_and_compute_rpc_impl.h"],
    deps = [
        ":match_proto",
        ":server_lib",
        "//util:status_includes",
        "@com_github_grpc_grpc//:grpc++",
    ],
)

cc_binary(
    name = "server",
    srcs = ["server.cc"],
    deps = [
        ":data_util",
        ":match_proto",
        ":private_join_and_compute_rpc_impl",
        ":server_lib",
        "@com_github_gflags_gflags//:gflags",
        "@com_github_glog_glog//:glog",
        "@com_github_grpc_grpc//:grpc",
        "@com_github_grpc_grpc//:grpc++",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/memory",
    ],
)

cc_binary(
    name = "client",
    srcs = ["client.cc"],
    deps = [
        ":client_lib",
        ":data_util",
        ":match_proto",
        "@com_github_gflags_gflags//:gflags",
        "@com_github_glog_glog//:glog",
        "@com_github_grpc_grpc//:grpc",
        "@com_github_grpc_grpc//:grpc++",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/memory",
    ],
)
