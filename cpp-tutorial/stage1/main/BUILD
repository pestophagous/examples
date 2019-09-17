load(
    "//main:copy_filegroups.bzl",
    "copy_filegroups_to_this_package",
)

# This command:
#   bazel run //main:hello-world-unwanted-nesting
#
# Will produce this run directory:
#.
#└── main
#    ├── hello-world-unwanted-nesting # "a.out" (the executable)
#    ├── other
#    │   └── deeply
#    │       └── nested
#    │           └── library
#    │               ├── test20.txt
#    │               └── test21.txt
#    ├── test10.txt
#    └── test11.txt
cc_binary(
    name = "hello-world-unwanted-nesting",
    srcs = ["hello-world.cc"],
    data = [
        ":test_files",
        "//main/other/deeply/nested/library:other_test_files",
    ],
)

# This command:
#   bazel run //main:hello-world-flattened-filegroups
#
# Will produce this run directory:
#.
#└── main
#    ├── hello-world-flattened-filegroups # "a.out" (the executable)
#    ├── test10.txt
#    ├── test11.txt
#    ├── test20.txt
#    └── test21.txt
cc_binary(
    name = "hello-world-flattened-filegroups",
    srcs = ["hello-world.cc"],
    data = [
        ":other_files_unnested",
        ":test_files",
    ],
)

filegroup(
    name = "test_files",
    srcs = glob([
        "*.txt",
    ]),
)

copy_filegroups_to_this_package(
    name = "other_files_unnested",
    targeted_filegroups = ["//main/other/deeply/nested/library:other_test_files"],
)
