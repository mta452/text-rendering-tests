cmake_minimum_required(VERSION 3.0)

project(fribidi)

add_library(fribidi STATIC
    fribidi/charset/fribidi-char-sets-cap-rtl.c
    fribidi/charset/fribidi-char-sets-cp1255.c
    fribidi/charset/fribidi-char-sets-cp1256.c
    fribidi/charset/fribidi-char-sets-iso8859-6.c
    fribidi/charset/fribidi-char-sets-iso8859-8.c
    fribidi/charset/fribidi-char-sets-utf8.c
    fribidi/charset/fribidi-char-sets.c
    fribidi/lib/fribidi-arabic.c
    fribidi/lib/fribidi-bidi-types.c
    fribidi/lib/fribidi-bidi.c
    fribidi/lib/fribidi-brackets.c
    fribidi/lib/fribidi-deprecated.c
    fribidi/lib/fribidi-joining-types.c
    fribidi/lib/fribidi-joining.c
    fribidi/lib/fribidi-mirroring.c
    fribidi/lib/fribidi-run.c
    fribidi/lib/fribidi-shape.c
    fribidi/lib/fribidi.c
)

include(CheckIncludeFile)
check_include_file(stdlib.h HAVE_STDLIB_H)
check_include_file(string.h HAVE_STRING_H)
check_include_file(strings.h HAVE_STRINGS_H)
check_include_file(wchar.h HAVE_WCHAR_H)
check_include_file(sys/times.h HAVE_SYS_TIMES_H)

include(CheckTypeSize)
check_type_size(int SIZEOF_INT)
check_type_size(wchar_t SIZEOF_WCHAR_T)

target_compile_definitions(fribidi
    PRIVATE HAVE_STRINGIZE
        $<IF:${HAVE_STDLIB_H},HAVE_STDLIB_H,>
        $<IF:${HAVE_STRING_H},HAVE_STRING_H,>
        $<IF:${HAVE_STRINGS_H},HAVE_STRINGS_H,>
        $<IF:${HAVE_WCHAR_H},HAVE_WCHAR_H,>
        $<IF:${HAVE_SYS_TIMES_H},HAVE_SYS_TIMES_H,>
)

target_include_directories(fribidi SYSTEM
    PUBLIC fribidi/lib
    PUBLIC generated
    PUBLIC include
    PUBLIC fribidi/charset
)
