# TODO:
# - some of the source files are excluded, determine when they are needed
# - adjust visibility so that this is only visible from this workspace
cc_library(
    name = "decnum",
    srcs = [
        "decContext.c",
        "decDouble.c",
        "decimal32.c",
        "decimal64.c",
        "decimal128.c",
        "decNumber.c",
        "decPacked.c",
        "decQuad.c",
        "decSingle.c",
    ],
    hdrs = glob(
        ["*.h"]
    ) + [
        "decBasic.c",
        "decCommon.c",
    ],
    visibility = ["//visibility:public"],
    include_prefix = "decNumber",
)

cc_binary(
    name = "example1",
    deps = [":decnum"],
    srcs = ["example1.c"],
)

cc_binary(
    name = "example2",
    deps = [":decnum"],
    srcs = ["example2.c"],
)

cc_binary(
    name = "example3",
    deps = [":decnum"],
    srcs = ["example3.c"],
)

cc_binary(
    name = "example4",
    deps = [":decnum"],
    srcs = ["example4.c"],
)

cc_binary(
    name = "example5",
    deps = [":decnum"],
    srcs = ["example5.c"],
)

cc_binary(
    name = "example6",
    deps = [":decnum"],
    srcs = ["example6.c"],
)

cc_binary(
    name = "example7",
    deps = [":decnum"],
    srcs = ["example7.c"],
)

cc_binary(
    name = "example8",
    deps = [":decnum"],
    srcs = ["example8.c"],
)

filegroup(
    name = "all_examples",
    srcs = [
        ":example1",
        ":example2",
        ":example3",
        ":example4",
        ":example5",
        ":example6",
        ":example7",
        ":example8",
    ],
)
