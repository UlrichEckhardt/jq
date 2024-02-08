load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")


# TODO: generate "src/config.h"


genrule(
    name = "builtins_header",
    srcs = [
        "src/builtin.jq"
    ],
    outs = [
        "src/builtin.inc"
    ],
    cmd_bash = """
        cat src/builtin.jq \\
        | od -v -A n -t o1 \\
        | sed -e 's/$$/ /' \\
            -e 's/\\([0123456789]\\) /\\1, /g' \\
            -e 's/ $$//' \\
            -e 's/ 0/  0/g' \\
            -e 's/ \\([123456789]\\)/ 0\\1/g' \\
        > $@
    """,
)


cc_library(
    name = "jqlib",
    deps = [],
    srcs = glob(
        ["src/*.c", "src/*.h"],
        ["src/main.c", "src/config.h"]
    ),
    hdrs = [
        "src/builtin.inc",
    ],
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
