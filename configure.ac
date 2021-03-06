AC_PREREQ(2.59)

GENERIC_LIBRARY_NAME=usf

dnl Increment if backward compatibility with previous releases is not granted
m4_define(usf_version_major, 0)
dnl Increment if backward compatibility with previous releases is granted, 
dnl but something changed in the implementation of the Component. 
dnl (ie it methods could have been added)
m4_define(usf_version_minor, 2)
dnl Increment if the changes are small forward compatible bug fixes or 
dnl documentation modifications
m4_define(usf_version_micro, 0)

AC_INIT([usf],[usf_version_major.usf_version_minor.usf_version_micro], [andreas.sandberg@it.uu.se])

USF_VERSION_MAJOR=usf_version_major()
USF_VERSION_MINOR=usf_version_minor()
USF_VERSION_MICRO=usf_version_micro()
AC_SUBST(USF_VERSION_MAJOR)
AC_SUBST(USF_VERSION_MINOR)
AC_SUBST(USF_VERSION_MICRO)

AC_CONFIG_AUX_DIR([.])
AM_INIT_AUTOMAKE([foreign])

AC_CONFIG_MACRO_DIR([m4])

AC_PROG_CC
AC_PROG_CXX

AC_PROG_CC_STDC

AC_PROG_LIBTOOL

AM_PATH_PYTHON([2.4])
AX_PYTHON_DEVEL(>= '2.4')
AX_PKG_SWIG(1.3.17, 
	    [ have_swig=true ], 
	    [ AC_MSG_ERROR([SWIG is required to build bindings.]) ])
AX_SWIG_ENABLE_CXX
AX_SWIG_PYTHON

AM_CONDITIONAL([HAVE_SWIG], [ test x$have_swig = xtrue ])

AC_CHECK_HEADERS([argp.h], 
  [ have_argp=true ], [
    AC_MSG_WARN([GNU Argp not found, some tools will be disabled.])
    have_argp=false
  ])
AM_CONDITIONAL([HAVE_ARGP], [ test x$have_argp = xtrue ])

AC_CHECK_FUNCS([strndup strnlen])
AC_CHECK_LIB([bz2], [BZ2_bzReadOpen])

AC_ARG_ENABLE([debug-log],
  AS_HELP_STRING([--enable-debug-log],
    [Enable debug logging (default: disabled)]),
  [
    AC_DEFINE([ENABLE_DEBUG_LOG], [1], [Enable debug logging.])
  ])

AC_ARG_ENABLE([strict],
  AS_HELP_STRING([--disable-strict],
    [Disable strict compile time checks.]),
  [
    true
  ], [
    CFLAGS="-Werror ${CFLAGS}"
  ])

AC_MSG_CHECKING([for PIN])
AC_ARG_VAR([PIN_HOME], [ Path to PIN toolkit ])
if [ test "$PIN_HOME" != "" ] && \
   [ test -e ${PIN_HOME}/source/tools/makefile.gnu.config ]; then

  have_pin=true
  AC_MSG_RESULT([ yes ($PIN_HOME) ])
else
  AC_MSG_RESULT([no])
fi
AM_CONDITIONAL([HAVE_PIN], [ test x$have_pin = xtrue ])

AC_CONFIG_HEADERS([config.h])

AC_CONFIG_FILES([
	Makefile

	include/Makefile
	include/uart/Makefile

	lib/Makefile

	tools/Makefile

	pin/Makefile

	test/Makefile

	swig/Makefile
])

AC_OUTPUT
