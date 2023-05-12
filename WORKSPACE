load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_rust",
    sha256 = "25209daff2ba21e818801c7b2dab0274c43808982d6aea9f796d899db6319146",
    urls = ["https://github.com/bazelbuild/rules_rust/releases/download/0.21.1/rules_rust-v0.21.1.tar.gz"],
)

# local_repository(
#     name = "rules_rust",
#     path = "../rules_rust",
# )

load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(
    edition="2021",
    extra_target_triples = [
        "x86_64-unknown-linux-musl"
    ]
)

load("@rules_rust//crate_universe:repositories.bzl", "crate_universe_dependencies")

crate_universe_dependencies(bootstrap = True)

load("@rules_rust//crate_universe:defs.bzl", "crates_repository", "crate")

crates_repository(
    name = "crate_index",
    cargo_lockfile = "//rust:Cargo.lock",
    isolated = False,
    manifests = [
      "//rust/gui:Cargo.toml",
    ],
    generator = "@cargo_bazel_bootstrap//:cargo-bazel",
)

load("@crate_index//:defs.bzl", "crate_repositories")

crate_repositories()

HERMETIC_CC_TOOLCHAIN_VERSION = "v2.0.0-rc1"

http_archive(
    name = "hermetic_cc_toolchain",
    sha256 = "43a1b398f08109c4f03b9ba2b3914bd43d1fec0425f71b71f802bf3f78cee0c2",
    urls = [
        "https://mirror.bazel.build/github.com/uber/hermetic_cc_toolchain/releases/download/{0}/hermetic_cc_toolchain-{0}.tar.gz".format(HERMETIC_CC_TOOLCHAIN_VERSION),
        "https://github.com/uber/hermetic_cc_toolchain/releases/download/{0}/hermetic_cc_toolchain-{0}.tar.gz".format(HERMETIC_CC_TOOLCHAIN_VERSION),
    ],
)

load("@hermetic_cc_toolchain//toolchain:defs.bzl", zig_toolchains = "toolchains")

zig_toolchains()

register_toolchains(
    "@zig_sdk//toolchain:linux_amd64_gnu.2.17",
)
