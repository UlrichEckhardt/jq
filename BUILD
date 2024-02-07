load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")


# TODO: generate "src/config.h"
# TODO: generate "src/builtin.inc"


cc_library(
    name = "jqlib",
    deps = [],
    srcs = glob(
        ["src/*.c", "src/*.h", "src/*.inc"],
        ["src/main.c", "src/config.h"]
    ),
    defines = [
        "_GNU_SOURCE",
        "IEEE_8087",
        'JQ_VERSION=\\"unknown\\"',
        'JQ_CONFIG=\\"(unknown)\\"',
    ],
)

cc_binary(
    name = "jq",
    deps = [
        ":jqlib",
    ],
    srcs = [
        "src/main.c",
        "src/config.h",
    ],
    visibility = ["//visibility:public"],
)
