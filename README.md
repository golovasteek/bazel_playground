# Example of bazel-rust workspace

Currentl problem is that the optional dependencies are not fetched.
These depenedencies neither are provided by `all_crate_deps` nor
can be specified manually.

The `//rust/gui:gui_bin` target can be built in two versions:
 1. defaul one, no extra features. No optional dependencies needed.
 2. debug one, it is enabled by "sdl2" cargo feature. This requires extra dependencies
 the bazel switches between the features by `--//rust/gui:use_sdl` flag.
