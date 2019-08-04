filegroup(
    name = "headers",
    srcs = glob(
        [
            "include/**/*.h",
            "include/**/*.inl",
        ],
        exclude = ["acconfig.h"],
    ),
)

defines = [
    "GEOS_INLINE",
    "USE_UNSTABLE_GEOS_CPP_API",
    "geos_EXPORTS",
]

# Bazels's optimized compile mode builds with -O2, but libgeos is built with -O3
# by default. We're specifying -O3 here which will override the -O2 bazel sets
copts = [
    "-O3",
    "--std=c++11",
]

includes = ["include"]

# algorithm
algorithmPaths = [
    "distance",
    "locate",
]

[cc_library(
    name = "algorithm/" + path,
    srcs = glob(["src/algorithm/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in algorithmPaths]

cc_library(
    name = "algorithm",
    srcs = glob(["src/algorithm/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":algorithm/" + path for path in algorithmPaths],
)

# geom
geomPaths = [
    "prep",
    "util",
]

[cc_library(
    name = "geom/" + path,
    srcs = glob(["src/geom/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in geomPaths]

cc_library(
    name = "geom",
    srcs = glob(["src/geom/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":geom/" + path for path in geomPaths],
)

# geomgraph
geomGraphPaths = ["index"]

[cc_library(
    name = "geomgraph/" + path,
    srcs = glob(["src/geomgraph/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in geomGraphPaths]

cc_library(
    name = "geomgraph",
    srcs = glob(["src/geomgraph/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":geomgraph/" + path for path in geomGraphPaths],
)

# index
indexPaths = [
    "bintree",
    "chain",
    "intervaltree",
    "quadtree",
    "strtree",
    "sweepline",
]

[cc_library(
    name = "index/" + path,
    srcs = glob(["src/index/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in indexPaths]

cc_library(
    name = "index",
    srcs = glob(["src/index/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":index/" + path for path in indexPaths],
)

# io
cc_library(
    name = "io",
    srcs = glob(["src/io/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# linearref
cc_library(
    name = "linearref",
    srcs = glob(["src/linearref/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# noding
nodingPaths = ["snapround"]

[cc_library(
    name = "noding/" + path,
    srcs = glob(["src/noding/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in nodingPaths]

cc_library(
    name = "noding",
    srcs = glob(["src/noding/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":noding/" + path for path in nodingPaths],
)

# operation
operationPaths = [
    "buffer",
    "distance",
    "intersection",
    "overlay",
    "polygonize",
    "predicate",
    "relate",
    "sharedpaths",
    "union",
    "valid",
]

[cc_library(
    name = "operation/" + path,
    srcs = glob([
        "src/operation/" + path + "/**/*.cpp",
        "src/operation/" + path + "/**/*.h",
    ]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in operationPaths]

cc_library(
    name = "operation",
    srcs = glob(["src/operation/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":operation/" + path for path in operationPaths],
)

# planargrpah
cc_library(
    name = "planargraph",
    srcs = glob(["src/planargraph/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# precision
cc_library(
    name = "precision",
    srcs = glob(["src/precision/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# simplify
cc_library(
    name = "simplify",
    srcs = glob(["src/simplify/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# triangulate
triangulatePaths = ["quadedge"]

[cc_library(
    name = "triangulate/" + path,
    srcs = glob(["src/triangulate/" + path + "/**/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
) for path in triangulatePaths]

cc_library(
    name = "triangulate",
    srcs = glob(["src/triangulate/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [":triangulate/" + path for path in triangulatePaths],
)

# util
cc_library(
    name = "util",
    srcs = glob(["src/util/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
)

# libgeos
cc_library(
    name = "geos",
    srcs = glob(["src/*.cpp"]) + [":headers"],
    copts = copts,
    defines = defines,
    includes = includes,
    deps = [
        ":algorithm",
        ":geom",
        ":geomgraph",
        ":index",
        ":io",
        ":linearref",
        ":noding",
        ":operation",
        ":planargraph",
        ":precision",
        ":simplify",
        ":triangulate",
        ":util",
    ],
)

# capi
genrule(
   name = "capi_header",
   srcs = ["capi/geos_c.h.in"],
   outs = ["capi/geos_c.h"],
   cmd = "cp $< $@",
)

cc_library(
    name = "geos_c",
    srcs = glob(["capi/*.cpp"]) + [":headers", ":capi/geos_c.h"],
    copts = copts,
    defines = defines,
    hdrs = [":capi/geos_c.h"],
    includes = includes + ["capi"],
    deps = [
        ":geos",
    ],
)
