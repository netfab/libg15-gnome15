#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(libg15, 1.3.1, https://github.com/netfab/libg15/issues)
AC_PREFIX_DEFAULT(/usr)
AC_CONFIG_AUX_DIR(config)
AC_CONFIG_MACRO_DIR([m4])
AC_CANONICAL_TARGET()

AM_INIT_AUTOMAKE()
AC_CONFIG_SRCDIR([src/libg15.c])
AC_CONFIG_HEADER([config.h])

# Checks for programs.
AC_PROG_CC
AC_PROG_LIBTOOL

case $host_os in
	*linux*) 
	  AC_DEFINE([OSTYPE_LINUX], [1],[Target OS is Linux])
	  ;;
	*darwin*)
	  AC_DEFINE([OSTYPE_DARWIN], [1],[Target OS is Darwin])
	  ;;
        *solaris*)
          AC_DEFINE([OSTYPE_SOLARIS], [1],[Target OS is Solaris])
	  AC_SEARCH_LIBS([nanosleep],rt,[],[],[])
          AC_DEFINE(SUN_LIBUSB, 1, [Define to 1 for Sun version of libusb.])
	  libusb_blocks=true	  
	  ;;
esac

# Checks for libraries.
AC_SEARCH_LIBS([usb_init], [usb], [], [
	AC_MSG_ERROR([libusb not found. please install it])
])

dnl Some versions of libusb do not honour timeout and block. Suns' version is one of them.
if test "x$libusb_blocks" == "xtrue"; then
      AC_DEFINE([LIBUSB_BLOCKS], [1],[Define if libusb implementation blocks on read or write])
fi

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([string.h])
AC_CHECK_HEADERS([usb.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_CHECK_FUNCS([memset])

AC_CONFIG_FILES([
	libg15.pc
	src/Makefile
	Makefile
])
AC_OUTPUT
