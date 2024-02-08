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

# TODO: Implement this meaningfully.
# With autotools, `config.status --config` gives you the flags given
# to `configure`.
genrule(
    name = "config_opts_header",
    srcs = [],
    outs = [
        "src/config_opts.inc"
    ],
    cmd_bash = "echo '#define JQ_CONFIG \"(unknown)\"' > $@",
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
    deps = [],
    srcs = glob(
        ["src/*.c", "src/*.h", "src/*.inc"],
        ["src/main.c", "src/version.h", "src/config_opts.inc"]
    ),
    hdrs =[
        "src/builtin.inc",
    ],
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
