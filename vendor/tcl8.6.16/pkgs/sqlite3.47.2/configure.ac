#!/bin/bash -norc
dnl	This file is an input file used by the GNU "autoconf" program to
dnl	generate the file "configure", which is run during Tcl installation
dnl	to configure the system for the local environment.

#-----------------------------------------------------------------------
# Sample configure.ac for Tcl Extensions.  The only places you should
# need to modify this file are marked by the string __CHANGE__
#-----------------------------------------------------------------------

#-----------------------------------------------------------------------
# __CHANGE__
# Set your package name and version numbers here.
#
# This initializes the environment with PACKAGE_NAME and PACKAGE_VERSION
# set as provided.  These will also be added as -D defs in your Makefile
# so you can encode the package version directly into the source files.
# This will also define a special symbol for Windows (BUILD_<PACKAGE_NAME>
# so that we create the export library with the dll.
#-----------------------------------------------------------------------

AC_INIT([sqlite],[3.47.2])

#--------------------------------------------------------------------
# Call TEA_INIT as the first TEA_ macro to set up initial vars.
# This will define a ${TEA_PLATFORM} variable == "unix" or "windows"
# as well as PKG_LIB_FILE and PKG_STUB_LIB_FILE.
#--------------------------------------------------------------------

TEA_INIT([3.10])

AC_CONFIG_AUX_DIR(tclconfig)

#--------------------------------------------------------------------
# Load the tclConfig.sh file
#--------------------------------------------------------------------

TEA_PATH_TCLCONFIG
TEA_LOAD_TCLCONFIG

#--------------------------------------------------------------------
# Load the tkConfig.sh file if necessary (Tk extension)
#--------------------------------------------------------------------

#TEA_PATH_TKCONFIG
#TEA_LOAD_TKCONFIG

#-----------------------------------------------------------------------
# Handle the --prefix=... option by defaulting to what Tcl gave.
# Must be called after TEA_LOAD_TCLCONFIG and before TEA_SETUP_COMPILER.
#-----------------------------------------------------------------------

TEA_PREFIX

#-----------------------------------------------------------------------
# Standard compiler checks.
# This sets up CC by using the CC env var, or looks for gcc otherwise.
# This also calls AC_PROG_CC, AC_PROG_INSTALL and a few others to create
# the basic setup necessary to compile executables.
#-----------------------------------------------------------------------

TEA_SETUP_COMPILER

#-----------------------------------------------------------------------
# __CHANGE__
# Specify the C source files to compile in TEA_ADD_SOURCES,
# public headers that need to be installed in TEA_ADD_HEADERS,
# stub library C source files to compile in TEA_ADD_STUB_SOURCES,
# and runtime Tcl library files in TEA_ADD_TCL_SOURCES.
# This defines PKG(_STUB)_SOURCES, PKG(_STUB)_OBJECTS, PKG_HEADERS
# and PKG_TCL_SOURCES.
#-----------------------------------------------------------------------

TEA_ADD_SOURCES([tclsqlite3.c])
TEA_ADD_HEADERS([])
TEA_ADD_INCLUDES([-I\"`\${CYGPATH} \${srcdir}/generic`\"])
TEA_ADD_LIBS([])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_DBPAGE_VTAB=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_DBSTAT_VTAB=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_FTS3_PARENTHESIS=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_FTS4=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_FTS5=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_COLUMN_METADATA=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_JSON1=1])
TEA_ADD_CFLAGS([-DSQLITE_3_SUFFIX_ONLY=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_RTREE=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_GEOPOLY=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_STAT4=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_MATH_FUNCTIONS=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_DESERIALIZE=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_DBPAGE_VTAB=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_BYTECODE_VTAB=1])
TEA_ADD_CFLAGS([-DSQLITE_ENABLE_DBSTAT_VTAB=1])
TEA_ADD_CFLAGS([-DSQLITE_LIKE_DOESNT_MATCH_BLOBS=1])
TEA_ADD_CFLAGS([-DSQLITE_UNTESTABLE=1])
TEA_ADD_CFLAGS([-DSQLITE_OMIT_DEPRECATED=1])
TEA_ADD_CFLAGS([-DSQLITE_OMIT_LOOKASIDE=1])
TEA_ADD_CFLAGS([-DSQLITE_SECURE_DELETE=1])
TEA_ADD_CFLAGS([-DSQLITE_SOUNDEX=1])
TEA_ADD_CFLAGS([-DSQLITE_USE_ALLOCA=1])
TEA_ADD_CFLAGS([-DSQLITE_WIN32_NO_ANSI=1])
TEA_ADD_CFLAGS([-DSQLITE_WIN32_GETVERSIONEX=0])
TEA_ADD_STUB_SOURCES([])
TEA_ADD_TCL_SOURCES([])

#--------------------------------------------------------------------
# The --with-system-sqlite causes the TCL bindings to SQLite to use
# the system shared library for SQLite rather than statically linking
# against its own private copy.  This is dangerous and leads to
# undersirable dependences and is not recommended.
# Patchs from rmax.
#--------------------------------------------------------------------
AC_ARG_WITH([system-sqlite],
 [AS_HELP_STRING([--with-system-sqlite],
   [use a system-supplied libsqlite3 instead of the bundled one])],
 [], [with_system_sqlite=no])
if test x$with_system_sqlite != xno; then
 AC_CHECK_HEADER([sqlite3.h],
   [AC_CHECK_LIB([sqlite3],[sqlite3_initialize],
     [AC_DEFINE(USE_SYSTEM_SQLITE)
      LIBS="$LIBS -lsqlite3"])])
else
    TEA_ADD_CFLAGS([-DSQLITE_API=MODULE_SCOPE])
fi

#--------------------------------------------------------------------
# __CHANGE__
#
# You can add more files to clean if your extension creates any extra
# files by extending CLEANFILES.
# Add pkgIndex.tcl if it is generated in the Makefile instead of ./configure
# and change Makefile.in to move it from CONFIG_CLEAN_FILES to BINARIES var.
#
# A few miscellaneous platform-specific items:
# TEA_ADD_* any platform specific compiler/build info here.
#--------------------------------------------------------------------

#CLEANFILES="$CLEANFILES pkgIndex.tcl"
if test "${TEA_PLATFORM}" = "windows" ; then
    # Ensure no empty if clauses
    :
    #TEA_ADD_SOURCES([win/winFile.c])
    #TEA_ADD_INCLUDES([-I\"$(${CYGPATH} ${srcdir}/win)\"])
else
    # Ensure no empty else clauses
    :
    #TEA_ADD_SOURCES([unix/unixFile.c])
    #TEA_ADD_LIBS([-lsuperfly])
fi

#--------------------------------------------------------------------
# __CHANGE__
# Choose which headers you need.  Extension authors should try very
# hard to only rely on the Tcl public header files.  Internal headers
# contain private data structures and are subject to change without
# notice.
# This MUST be called after TEA_LOAD_TCLCONFIG / TEA_LOAD_TKCONFIG
#--------------------------------------------------------------------

TEA_PUBLIC_TCL_HEADERS
#TEA_PRIVATE_TCL_HEADERS

#TEA_PUBLIC_TK_HEADERS
#TEA_PRIVATE_TK_HEADERS
#TEA_PATH_X

#--------------------------------------------------------------------
# Check whether --enable-threads or --disable-threads was given.
# This auto-enables if Tcl was compiled threaded.
#--------------------------------------------------------------------

TEA_ENABLE_THREADS
if test "${TCL_THREADS}" = "1" ; then
    AC_DEFINE(SQLITE_THREADSAFE, 1, [Trigger sqlite threadsafe build])
    # Not automatically added by Tcl because its assumed Tcl links to them,
    # but it may not if it isn't really a threaded build.
    TEA_ADD_LIBS([$THREADS_LIBS])
else
    AC_DEFINE(SQLITE_THREADSAFE, 0, [Trigger sqlite non-threadsafe build])
fi

#--------------------------------------------------------------------
# The statement below defines a collection of symbols related to
# building as a shared library instead of a static library.
#--------------------------------------------------------------------

TEA_ENABLE_SHARED

#--------------------------------------------------------------------
# This macro figures out what flags to use with the compiler/linker
# when building shared/static debug/optimized objects.  This information
# can be taken from the tclConfig.sh file, but this figures it all out.
#--------------------------------------------------------------------

TEA_CONFIG_CFLAGS

#--------------------------------------------------------------------
# Set the default compiler switches based on the --enable-symbols option.
#--------------------------------------------------------------------

TEA_ENABLE_SYMBOLS

#--------------------------------------------------------------------
# Everyone should be linking against the Tcl stub library.  If you
# can't for some reason, remove this definition.  If you aren't using
# stubs, you also need to modify the SHLIB_LD_LIBS setting below to
# link against the non-stubbed Tcl library.  Add Tk too if necessary.
#--------------------------------------------------------------------

AC_DEFINE(USE_TCL_STUBS, 1, [Use Tcl stubs])
#AC_DEFINE(USE_TK_STUBS, 1, [Use Tk stubs])


#--------------------------------------------------------------------
# Redefine fdatasync as fsync on systems that lack fdatasync
#--------------------------------------------------------------------
#
#AC_CHECK_FUNC(fdatasync, , AC_DEFINE(fdatasync, fsync))
AC_CHECK_HEADERS([malloc.h])
# Check for library functions that SQLite can optionally use.
AC_CHECK_FUNCS([fdatasync usleep strchrnul localtime_r gmtime_r localtime_s malloc_usable_size utime flock readlink lstat pread pread64 pwrite pwrite64 rand_s])

AC_FUNC_STRERROR_R


#--------------------------------------------------------------------
# This macro generates a line to use when building a library.  It
# depends on values set by the TEA_ENABLE_SHARED, TEA_ENABLE_SYMBOLS,
# and TEA_LOAD_TCLCONFIG macros above.
#--------------------------------------------------------------------

TEA_MAKE_LIB

#--------------------------------------------------------------------
# Determine the name of the tclsh and/or wish executables in the
# Tcl and Tk build directories or the location they were installed
# into. These paths are used to support running test cases only,
# the Makefile should not be making use of these paths to generate
# a pkgIndex.tcl file or anything else at extension build time.
#--------------------------------------------------------------------

TEA_PROG_TCLSH
#TEA_PROG_WISH

#--------------------------------------------------------------------
# Finally, substitute all of the various values into the Makefile.
# You may alternatively have a special pkgIndex.tcl.in or other files
# which require substituting th AC variables in.  Include these here.
#--------------------------------------------------------------------

AC_CONFIG_FILES([Makefile pkgIndex.tcl])
AC_OUTPUT
