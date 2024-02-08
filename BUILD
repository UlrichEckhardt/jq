load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

genrule(
    name = "version_header",
    srcs = [],
    outs = [
        "src/version.h"
    ],
    cmd_bash = """
    (
        VERSION=$$(scripts/version)
        echo -n '#define JQ_VERSION "'
        echo -n "$$VERSION"
        echo '"'
    ) > $@
    """,
    # Note: This target depends on the whole Git repository here,
    # which is why it needs to be executed locally and outside of
    # any sandbox.
    local = True,
    tools = [
        "scripts/version"
    ],
)

# TODO: generate "src/config_opts.inc", "src/builtin.inc"

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
