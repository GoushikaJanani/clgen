# This is an implementation of the OpenCL benchmark generator from:
#
#     ﻿Cummins, C., Petoumenos, P., Zang, W., & Leather, H. (2017). Synthesizing
#     Benchmarks for Predictive Modeling. In CGO. IEEE.
#
# Copyright 2017-2020 Chris Cummins <chrisc.101@gmail.com>.
#
# This file is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.

load("@com_github_chriscummins_rules_bats//:bats.bzl", "bats_test")

py_binary(
    name = "generative_model",
    srcs = ["generative_model.py"],
    data = ["//deeplearning/clgen/corpuses:token_lists"],
    visibility = ["//visibility:public"],
    deps = [
        "//deeplearning/clgen",
        "//deeplearning/clgen/proto:clgen_pb_py",
        "//labm8/py:app",
        "//labm8/py:bazelutil",
        "//labm8/py:pbutil",
    ],
)

py_test(
    name = "generative_model_test",
    srcs = ["generative_model_test.py"],
    deps = [
        ":generative_model",
        "//labm8/py:app",
        "//labm8/py:fs",
        "//labm8/py:test",
    ],
)

bats_test(
    name = "generative_model_smoke_test",
    srcs = ["generative_model_smoke_test.bats"],
    data = [
        ":generative_model",
        "//labm8/sh:test",
    ],
)

py_library(
    name = "opencl_kernel_driver",
    srcs = ["opencl_kernel_driver.py"],
    visibility = ["//visibility:public"],
    deps = [
        "//compilers/llvm:clang",
        "//deeplearning/deepsmith/harnesses:cldrive",
        "//deeplearning/deepsmith/proto:deepsmith_pb_py_grpc",
        "//gpu/cldrive/legacy:env",
        "//gpu/libcecl:libcecl_compile",
        "//gpu/libcecl:libcecl_rewriter",
        "//gpu/libcecl:libcecl_runtime",
        "//gpu/libcecl/proto:libcecl_pb_py",
        "//labm8/py:app",
    ],
)

py_test(
    name = "opencl_kernel_driver_test",
    srcs = ["opencl_kernel_driver_test.py"],
    deps = [
        ":opencl_kernel_driver",
        "//gpu/cldrive/legacy:env",
        "//labm8/py:test",
        "//third_party/py/pytest",
    ],
)
