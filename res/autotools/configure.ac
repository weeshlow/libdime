# Note that this has not been extensively tested with various autoconf
# versions.  TODO - determine the minimum autoconf version we will support
AC_PREREQ([2.63])

AC_INIT([libdime], [0.1], [support@lavabit.com], [libdime], [https://lavabit.com])

# Look for macros in the m4 directory
AC_CONFIG_MACRO_DIR([m4])

# The X509_check_host() function was added to OpenSSL in v1.0.2. So you need
# that version or you need to apply the patch to OpenSSL v1.0.1.
PKG_CHECK_MODULES([OPENSSL], [openssl >= 1.0.2])

# Sanity check to make sure the specified srcdir actually contains the source
AC_CONFIG_SRCDIR([include/dime/signet/signet.h])

# Auxiliary autotools files go here
AC_CONFIG_AUX_DIR([build-aux])

# Initialize Automake
#
# The foreign option prevents automake from requiring the GNU-specific project
# files like AUTHORS, COPYING, etc.
#
# The subdir-objects option allows source files in subdirectories.
#
# nostdinc disables including srcdir (-I.)
AM_INIT_AUTOMAKE([foreign subdir-objects nostdinc])

# Instruct configure to create Makefile using Makefile.am
AC_CONFIG_FILES([Makefile])

# Find and probe C compiler (use "current" standard)
#AC_PROG_CC_STDC

# Set the C compiler
AC_PROG_CC_C99

# Find and probe C++ compiler
AC_PROG_CXX

# Set common system defines for POSIX extensions, such as _GNU_SOURCE Must be
# called before any macros that run the compiler (like AC_PROG_LIBTOOL) to
# avoid autoconf errors.
AC_USE_SYSTEM_EXTENSIONS

# Find libtool
AC_PROG_LIBTOOL

# Find awk
AC_PROG_AWK

# Check which version of strerror_r the system has
AC_FUNC_STRERROR_R

# Handle pthreads
AX_PTHREAD(
    [AC_SUBST(GTEST_HAS_PTHREAD, [1])],
    [AC_SUBST(GTEST_HAS_PTHREAD, [0])])

#AC_DEFINE([HAVE_NS_TYPE])

# These flags are applied everywhere
WARNINGS="-Wfatal-errors "
WARNINGS+="-Werror "
WARNINGS+="-Wall "
WARNINGS+="-Wextra "
WARNINGS+="-Wformat=2 "
WARNINGS+="-Wwrite-strings "
WARNINGS+="-Wno-format-nonliteral "
#WARNINGS += "-Wstrict-overflow=5"

# These flags are C only
CWARNINGS="-Wstrict-prototypes "
CWARNINGS+="-Wmissing-prototypes "
CWARNINGS+="-Wno-pointer-sign "

if `$CC -v 2>&1 | grep 'clang version' > /dev/null 2>&1`; then
    # Clang-specific flags

    WARNINGS+="-Wno-cast-align "
    WARNINGS+="-Wno-conditional-uninitialized "
    WARNINGS+="-Wno-conversion "
    WARNINGS+="-Wno-covered-switch-default "
    WARNINGS+="-Wno-disabled-macro-expansion "
    WARNINGS+="-Wno-documentation "
    WARNINGS+="-Wno-documentation-unknown-command "
    WARNINGS+="-Wno-float-equal "
    WARNINGS+="-Wno-gnu-designator "
    WARNINGS+="-Wno-packed "
    WARNINGS+="-Wno-padded "
    WARNINGS+="-Wno-pedantic "
    WARNINGS+="-Wno-shorten-64-to-32 "
    WARNINGS+="-Wno-sign-conversion "
    WARNINGS+="-Wno-switch-enum "
    WARNINGS+="-Wno-unreachable-code "
    WARNINGS+="-Wno-cast-qual "
    WARNINGS+="-Wno-class-varargs "
    WARNINGS+="-Wno-unreachable-code-break "
    WARNINGS+="-Wno-assign-enum "

    CWARNINGS+="-ferror-limit=5 "
    CWARNINGS+="-Weverything "
    CWARNINGS+="-Wno-bad-function-cast "
fi

AC_SUBST(WARNINGS)
AC_SUBST(CWARNINGS)

# Set the C++ standard
AC_DEFUN([CHECK_CXX0X],[
          AC_LANG_PUSH([C++])
          AX_CHECK_COMPILE_FLAG([-std=c++0x],[
                                 CXX="$CXX -std=c++0x"])
          AC_LANG_POP([C++])
          ])
CHECK_CXX0X

AC_DEFUN([AM_SET_DEPDIR],
[AC_REQUIRE([AM_SET_LEADING_DOT])
AC_SUBST([DEPDIR], ["${am__leading_dot}deps"])
])
AM_SET_DEPDIR

AC_DEFUN([AM_SET_OBJDIR],
[AC_REQUIRE([AM_SET_LEADING_DOT])
AC_SUBST([OBJDIR], ["${am__leading_dot}objs"])
])
AM_SET_OBJDIR

AS_IF([test "x${ac_cv_prog_cc_c99}" == "xno"],[AC_MSG_ERROR([No c99 compatible compiler found])])


AC_OUTPUT
