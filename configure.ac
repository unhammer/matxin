#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT([matxin], [1.4.0-beta])
AC_CONFIG_SRCDIR([src/analyser.cc])
AC_CONFIG_AUX_DIR([build-aux])
PACKAGE=matxin

GENERIC_MAJOR_VERSION=1
GENERIC_MINOR_VERSION=4
GENERIC_MICRO_VERSION=0
GENERIC_EXTRA_VERSION=beta

GENERIC_RELEASE=$GENERIC_MAJOR_VERSION.$GENERIC_MINOR_VERSION
GENERIC_RELEASE=$GENERIC_MAJOR_VERSION.$GENERIC_MINOR_VERSION.$GENERIC_MICRO_VERSION-$GENERIC_EXTRA_VERSION
AC_SUBST(GENERIC_RELEASE)
AC_SUBST(GENERIC_VERSION)

#
# API version (often = GENERIC_MAJOR_VERSION.GENERIC_MINOR_VERSION)
#
GENERIC_API_VERSION=$GENERIC_MAJOR_VERSION
AC_SUBST(GENERIC_API_VERSION)

AC_SUBST(GENERIC_LIBRARY_NAME, $PACKAGE)

#
# Required library versions
#
m4_define([required_lttoolbox_version], [3.2.0])
m4_define([required_libxml_version], [2.6.17])
m4_define([required_libpcre_version], [6.4])

#
# Our configure script should create Makefiles
#
AM_INIT_AUTOMAKE([-Wall -Werror foreign])
#AM_INIT_AUTOMAKE
AM_CONFIG_HEADER([config.h])

#
# Determine default prefix and look in common locations for libraries
#
test "x$prefix" = "xNONE" && prefix="$ac_default_prefix"

CPPFLAGS="$CPPFLAGS -I$prefix/include -I$prefix/include/lttoolbox-3.2"
LDFLAGS="$LDFLAGS -L$prefix/lib"
if test "x$prefix" != "x/usr/local"; then
  CPPFLAGS="$CPPFLAGS -I/usr/local/include -I/usr/local/include/lttoolbox-3.2"
  LDFLAGS="$LDFLAGS -L/usr/local/lib"
fi
if test "x$prefix" != "x/usr"; then
  CPPFLAGS="$CPPFLAGS -I/usr/include -I/usr/include/lttoolbox-3.2"
  LDFLAGS="$LDFLAGS -L/usr/lib"
fi

#
# Set default paths for PKG_CONFIG_PATH in case it's not defined
#
if ! test $PKG_CONFIG_PATH ; then
  PKG_CONFIG_PATH="/usr/lib/pkgconfig:/usr/local/lib/pkgconfig"
fi

#
# Check for libxml2 usability.
#
AC_CHECK_PROG(HAVE_XML2_CONFIG, xml2-config, yes)
if test "x$HAVE_XML2_CONFIG" = "xyes"; then
  CPPFLAGS="$CPPFLAGS `xml2-config --cflags`"
else
  CPPFLAGS="$CPPFLAGS -I/usr/include/libxml2"
fi


#
# Define include/libs options
#
AC_ARG_WITH(boost,
            [AS_HELP_STRING([--with-boost=DIR],
                            [Look for boost include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="-I$withval/include $CPPFLAGS"
                 LDFLAGS="-L$withval/lib $LDFLAGS"
                 ;;
              esac ])

AC_ARG_WITH(foma,
            [AS_HELP_STRING([--with-foma=DIR],
                            [Look for foma include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="-I$withval/include $CPPFLAGS"
                 LDFLAGS="-L$withval/lib $LDFLAGS"
                 ;;
              esac ])

AC_ARG_WITH(freeling,
            [AS_HELP_STRING([--with-freeling=DIR],
                            [Look for freeling include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="-I$withval/include $CPPFLAGS"
                 LDFLAGS="-L$withval/lib $LDFLAGS"
                 ;;
              esac ])

AC_ARG_WITH(lttoolbox,
            [AS_HELP_STRING([--with-lttoolbox=DIR],
                            [Look for lttoolbox include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="-I$withval/include/lttoolbox-3.2 $CPPFLAGS"
                 LDFLAGS="-L$withval/lib $LDFLAGS"
		 PKG_CONFIG_PATH=$withval/lib/pkgconfig
                 ;;
              esac ])

AC_ARG_WITH(libxml2,
            [AS_HELP_STRING([--with-libxml2=DIR],
                            [Look for libxml2 include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="$CPPFLAGS -I$withval/include/libxml2"
                 LDFLAGS="$LDFLAGS -L$withval/lib"
                 ;;
              esac ])

AC_ARG_WITH(pcre,
            [AS_HELP_STRING([--with-pcre=DIR],
                            [Look for pcre include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="$CPPFLAGS -I$withval/include"
                 LDFLAGS="$LDFLAGS -L$withval/lib"
                 ;;
              esac ])

AC_ARG_WITH(berkeley,
            [AS_HELP_STRING([--with-berkeley=DIR],
                            [Look for Berkeley db_cxx include/libs in DIR])],
            [ case "$withval" in
               no)
                 ;;
               *)
                 CPPFLAGS="$CPPFLAGS -I$withval/include"
                 LDFLAGS="$LDFLAGS -L$withval/lib"
                 ;;
              esac ])


#
# Checks for programs.
#
AC_PROG_CXX
AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_RANLIB
AC_LANG([C++])

# This is the right thing to use
#AX_CXX_COMPILE_STDCXX_11

CXXFLAGS="$CXXFLAGS -std=gnu++11"


#
# Arch & OS checks
#
AC_MSG_CHECKING([Compilation architecture: PPC, i686, Other])
    if test x$(which arch) = x
    then ARCH=$($(which uname) -m)
else ARCH=$($(which arch))
    fi
    if test x$ARCH = xppc
    then
AC_MSG_RESULT([PowerPC])
    CFLAGS="$CFLAGS -ansi -mpowerpc -maltivec -fno-pic -fomit-frame-pointer"
    CXXFLAGS="$CXXFLAGS -ansi -mpowerpc -maltivec -fno-pic -fomit-frame-pointer"
    else
    if test x$ARCH = xi686
    then
AC_MSG_RESULT([i686])
    CFLAGS="$CFLAGS -ansi -march=i686 -O3 -fno-pic -fomit-frame-pointer"
    CXXFLAGS="$CXXFLAGS -ansi -march=i686 -O3 -fno-pic \
              -fomit-frame-pointer"
    else
AC_MSG_RESULT([Other])
    CFLAGS="$CFLAGS -ansi -O3"
    CXXFLAGS="$CXXFLAGS -ansi -O3"
    fi
    fi

AC_MSG_CHECKING([Operating System])
OSTYPE=$($(which uname) -s)
AC_MSG_RESULT([$OSTYPE])
AC_SUBST(OSTYPE)

# We need this to determine whether we use zcat or gzcat
AM_CONDITIONAL(OS_IS_SOLARIS, [test x"$OSTYPE" = xSunOS])
AM_CONDITIONAL(OS_IS_DARWIN, [test x"$OSTYPE" = xDarwin])

#
# These programs are required during the make process so we
# must test they're available on the current system
#
if test x$ARCH = xppc
then
  AC_PATH_PROG(XSLTPROC, sabcmd, no)
  if test x$ac_cv_path_XSLTPROC = x
  then
    AC_MSG_ERROR([sablotron not found. You may want to adjust your PATH.])
  fi
  if test x$ac_cv_path_XSLTPROC = xno
  then
    AC_MSG_ERROR([sablotron not found. You may want to adjust your PATH.])
  fi
else
  AC_PATH_PROG(XSLTPROC, xsltproc, no)
  if test x$ac_cv_path_XSLTPROC = x
  then
    AC_MSG_ERROR([xsltproc not found. You may want to adjust your PATH.])
  fi
  if test x$ac_cv_path_XSLTPROC = xno
  then
    AC_MSG_ERROR([xsltproc not found. You may want to adjust your PATH.])
  fi
fi

AC_PATH_PROG(FLEX, flex, no)
if test x$ac_cv_path_FLEX = x
then
  AC_MSG_ERROR([flex not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_FLEX = xno
then
  AC_MSG_ERROR([flex not found. You may want to adjust your PATH.])
fi

AC_PATH_PROG(PERL, perl, no)
if test x$ac_cv_path_PERL = x
then
  AC_MSG_ERROR([perl not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_PERL = xno
then
  AC_MSG_ERROR([perl not found. You may want to adjust your PATH.])
fi

AC_PATH_PROG(BASH, bash, no)
if test x$ac_cv_path_BASH = x
then
  AC_MSG_ERROR([bash not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_BASH = xno
then
  AC_MSG_ERROR([bash not found. You may want to adjust your PATH.])
fi

AC_PATH_PROG(LT_COMP, lt-comp, no)
if test x$ac_cv_path_LT_COMP = x
then
  AC_MSG_ERROR([lt-comp not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_LT_COMP = xno
then
  AC_MSG_ERROR([lt-comp not found. You may want to adjust your PATH.])
fi

AC_PATH_PROG(DICC2PHON, dicc2phon, no)
if test x$ac_cv_path_DICC2PHON = x
then
  AC_MSG_ERROR([dicc2phon not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_DICC2PHON = xno
then
  AC_MSG_ERROR([dicc2phon not found. You may want to adjust your PATH.])
fi

dnl AC_PATH_PROG(CONVERTDICT, convertdict, no)
dnl if test x$ac_cv_path_CONVERTDICT = x
dnl then
dnl   AC_MSG_ERROR([convertdict not found. You may want to adjust your PATH.])
dnl fi
dnl if test x$ac_cv_path_CONVERTDICT = xno
dnl then
dnl   AC_MSG_ERROR([convertdict not found. You may want to adjust your PATH.])
dnl fi

#AC_PATH_PROG(COMPILEKB, compile_kb, no)
#if test x$ac_cv_path_COMPILEKB = x
#then
#  AC_MSG_ERROR([compile_kb not found. You may want to adjust your PATH.])
#fi
#if test x$ac_cv_path_COMPILEKB = xno
#then
#  AC_MSG_ERROR([compile_kb not found. You may want to adjust your PATH.])
#fi

AC_PATH_PROG(FOMA, foma, no)
if test x$ac_cv_path_FOMA = x
then
  AC_MSG_ERROR([foma not found. You may want to adjust your PATH.])
fi
if test x$ac_cv_path_FOMA = xno
then
  AC_MSG_ERROR([foma not found. You may want to adjust your PATH.])
fi


#
# Checks for libraries.
#
AC_CHECK_LIB(boost_system, main, [true],AC_MSG_ERROR([boost_system found]))
AC_CHECK_LIB(foma, main, [true],AC_MSG_ERROR([foma found]))

PKG_CHECK_MODULES(MATXIN, [dnl
 lttoolbox >= required_lttoolbox_version dnl
 libxml-2.0 >= required_libxml_version dnl
 libpcre >= required_libpcre_version], CPPFLAGS="$CPPFLAGS $MATXIN_CPPFLAGS $MATXIN_CFLAGS"; LIBS="$LIBS $MATXIN_LIBS")

#
# Checks for header files.
#
AC_HEADER_STDC
AC_CHECK_HEADERS([string.h sys/socket.h])


#
# Checks for typedefs, structures, and compiler characteristics.
#
AC_HEADER_STDBOOL
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T

#
# Checks for library functions.
#
AC_FUNC_ERROR_AT_LINE
AC_CHECK_FUNCS([socket])


#
# Generate these files
#
AC_CONFIG_FILES([matxin.pc
                 Makefile
                 src/Makefile])
AC_OUTPUT

#
# Print summary for the selected configuration
#
echo
echo "**  $PACKAGE_NAME $PACKAGE_VERSION - selected build configuration  **"
echo
echo "Install prefix ................... : $prefix"
echo
echo "Build architecture ............... : $ARCH"
echo "Operating System ................. : $OSTYPE"
echo
echo "Now type 'make', followed by 'make install' as root."
echo "If there are any problems, read the INSTALL file."
echo

