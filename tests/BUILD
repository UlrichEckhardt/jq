sh_library(
    name = "testscripts",
    deps = [],
    srcs = [
        "setup"
    ],
)

# TODO: Avoid duplication of `env = {"NO_VALGRIND": "1"}`
# TODO: Integrate Valgrind
# TODO: The scripts here are just small shell scripts that invoke `jq --run-tests`
#       with different test files. It should be possible to use `cc_test` instead
#       and set up the necessary environment variables there instead.

sh_test(
    name = "base64",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "base64test"
    ],
    data = [
        "//:jq",
        "base64.test",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
    size = "small",
)

sh_test(
    name = "jq",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "jqtest"
    ],
    data = [
        "//:jq",
        "jq.test",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
)

sh_test(
    name = "man",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "mantest",
    ],
    data = [
        "//:jq",
        "man.test",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
)

sh_test(
    name = "onig",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "onigtest"
    ],
    data = [
        "//:jq",
        "onig.test",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
)

sh_test(
    name = "optional",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "optionaltest"
    ],
    data = [
        "//:jq",
        "optional.test",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
)

sh_test(
    name = "sh",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "shtest"
    ],
    data = [
        "//:jq",
        "jq-f-test.sh",
        "torture/input0.json",
        "no-main-program.jq",
        "yes-main-program.jq",
        "modules/data.json",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
)

sh_test(
    name = "utf8",
    deps = [
        ":testscripts",
    ],
    srcs = [
        "utf8test"
    ],
    data = [
        "//:jq",
        "utf8-truncate.jq",
    ],
    env = {
        "NO_VALGRIND": "1",
        "LC_ALL": "C",
    },
    size = "small",
)

test_suite(
    name = "all",
    tests = [
        ":base64",
        ":jq",
        ":man",
        ":onig",
        ":optional",
        ":sh",
        ":utf8",
    ],
)