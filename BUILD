load("@rules_cc//cc:defs.bzl", "cc_binary")

cc_binary(
    name = "jq",
    deps = [],
    srcs = glob(["src/*.c", "src/*.h"]) + [
        "src/builtin.inc", "src/config_opts.inc"
    ],
    defines = [
        "_GNU_SOURCE",
        "IEEE_8087=1",
    ],
    visibility = ["//visibility:public"],
)
