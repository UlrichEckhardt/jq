load("@rules_cc//cc:defs.bzl", "cc_binary")

cc_binary(
    name = "jq",
    deps = [],
    srcs = glob(["src/*.c", "src/*.h"]) + [
        "src/builtin.inc"
    ],
    defines = [
        "_GNU_SOURCE",
        "IEEE_8087",
        'JQ_VERSION=\\"unknown\\"',
        'JQ_CONFIG=\\"(unknown)\\"',
    ],
    visibility = ["//visibility:public"],
)
