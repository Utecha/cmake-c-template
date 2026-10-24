# Add the library/executable target(s).
add_executable(${EXAMPLE})

# Add source files to the target.
target_sources(
    ${EXAMPLE} PRIVATE
    main.c
)

# Set the output directory for the target.
set_target_properties(
    ${EXAMPLE} PROPERTIES
    C_STANDARD 99
    C_STANDARD_REQUIRED OFF
    C_EXTENSIONS OFF
    ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY}
    LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY}
    RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY}
)

# Add any necessary include directories.
# target_include_directories(
#     ${EXAMPLE} PRIVATE
# )

# Add compiler flags by compiler toolchain.
target_compile_options(
    ${EXAMPLE} PRIVATE
    $<$<C_COMPILER_ID:Clang,GNU>:
        -Wall
        -Wextra
        -Wpedantic
    >
    $<$<C_COMPILER_ID:GNU>:
        $<$<NOT:$<PLATFORM_ID:Windows>>:
            $<$<CONFIG:Debug>:-ggdb>
        >
    >
    $<$<C_COMPILER_ID:Clang>:
        $<$<NOT:$<PLATFORM_ID:Windows>>:
            $<$<CONFIG:Debug>:-glldb>
        >
    >
    $<$<C_COMPILER_ID:MSVC>:
        /W3
        $<$<CONFIG:Debug>:/Zi>
    >
)

# Add definitions to the compiler flags. These are macros which can be used from
# code to control features or compile code conditionally.
target_compile_definitions(
    ${EXAMPLE} PRIVATE
    $<$<CONFIG:Debug>:DEBUG>
)
