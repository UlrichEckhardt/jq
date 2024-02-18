workspace(name = "jqlang_jq")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# TODO: Oniguruma is included as git submodule, too, so why not compile it from there?
http_archive(
    name = "oniguruma",
    urls = ["https://github.com/kkos/oniguruma/archive/d2f1a14ced5d5d461acac0da0d477ab240a7ab5f.tar.gz"],
    integrity = "sha256-9RULMMXGRIVGhYtoD2Ti3Lw5HgrK3vjDBDCfGOvC4PI=",
    build_file = "//:oniguruma.BUILD",
    workspace_file = "//:oniguruma.WORKSPACE",
    strip_prefix = "oniguruma-d2f1a14ced5d5d461acac0da0d477ab240a7ab5f",
)
