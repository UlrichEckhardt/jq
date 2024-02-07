load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

# TODO: generate "src/version.h", "src/config_opts.inc", "src/builtin.inc"


cc_library(
    name = "jqlib",
    deps = [],
    srcs = glob(
        ["src/*.c", "src/*.h", "src/*.inc"],
        ["src/main.c", "src/version.h", "src/config_opts.inc"]
    ),
    defines = [
        "_GNU_SOURCE",
        "IEEE_8087",
    ],
)

cc_binary(
    name = "jq",
    deps = [
        ":jqlib",
    ],
    srcs = [
        "src/main.c",
        "src/version.h",
        "src/config_opts.inc",
    ],
    visibility = ["//visibility:public"],
)
