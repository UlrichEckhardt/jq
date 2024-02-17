load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")
load("@bazel_skylib//rules:common_settings.bzl", "bool_flag")

# build flag whether to use the internal decnum lib or not
bool_flag(
    name = "enable_decnum",
    build_setting_default = False,
    visibility = ["//visibility:public"],
)

config_setting(
    name = "decnum_enabled",
    flag_values = {
        ":enable_decnum": "true",
    },
)


# TODO: Implement this meaningfully.
# With autotools, `config.status --config` gives you the flags given
# to `configure`. This should at least reflect flags given to bazel.
genrule(
    name = "config_header",
    srcs = [],
    outs = [
        "src/config.h"
    ],
    cmd_bash = """
    (
        echo '#define JQ_CONFIG \"(unknown)\"'
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
    deps = select({
        ":decnum_enabled": ["//vendor/decNumber:decnum"],
        "//conditions:default": [],
    }),
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
    ] + select({
        ":decnum_enabled": ["USE_DECNUM"],
        "//conditions:default": [],
    }),
)

cc_binary(
    name = "jq",
    copts = ["--include", "$(location src/config.h)"],
    deps = [
        ":jqlib",
    ],
    srcs = [
        "src/main.c",
        "src/config.h",
    ],
    visibility = ["//visibility:public"],
)
