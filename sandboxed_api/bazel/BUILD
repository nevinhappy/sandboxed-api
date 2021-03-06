# Copyright 2019 Google LLC. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

licenses(["notice"])  # Apache v2.0

exports_files([
    "proto.bzl",
    "embed_data.bzl",
    "sapi.bzl",
])

load(
    "//sandboxed_api/bazel:embed_data.bzl",
    "sapi_cc_embed_data",
)

# An implicit dependency of all "sapi_cc_embed_data" rules that builds
# embedded data into .cc files.
cc_binary(
    name = "filewrapper",
    srcs = ["filewrapper.cc"],
    visibility = ["//visibility:public"],
    deps = [
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
        "//sandboxed_api/sandbox2/util:fileops",
        "//sandboxed_api/sandbox2/util:strerror",
        "//sandboxed_api/util:raw_logging",
    ],
)

sapi_cc_embed_data(
    name = "filewrapper_embedded",
    srcs = ["testdata/filewrapper_embedded.bin"],
)

cc_test(
    name = "filewrapper_test",
    srcs = ["filewrapper_test.cc"],
    data = ["testdata/filewrapper_embedded.bin"],
    deps = [
        ":filewrapper_embedded",
        "@com_google_googletest//:gtest_main",
        "@com_google_absl//absl/strings",
        "//sandboxed_api/sandbox2:testing",
        "//sandboxed_api/sandbox2/util:file_helpers",
        "//sandboxed_api/util:status_matchers",
    ],
)
