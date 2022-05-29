AC_INIT(Leafpad, 0.8.17le, tarot@sdf.lonestar.org)
AM_INIT_AUTOMAKE($PACKAGE_TARNAME, $PACKAGE_VERSION)
AM_CONFIG_HEADER(config.h)

AC_PROG_INTLTOOL(, no-xml)	# require >= 0.31 for autoreconf
AC_PROG_CC
if test "$GCC" = "yes"; then
	CFLAGS="$CFLAGS -Wall"
fi
AM_PROG_CC_C_O
AC_PROG_CXX
AC_PROG_RANLIB

PKG_CHECK_MODULES(GTK, gtk+-2.0)

AC_ARG_ENABLE(chardetect,
	AC_HELP_STRING([--disable-chardetect], [force to disable universalchardet feature]))
if test "$enable_chardetect" != "no"; then
	AC_DEFINE(ENABLE_CHARDETECT, 1, [Define if universalchardet is enabled.])
fi

AC_ARG_ENABLE(shiftenter,
	AC_HELP_STRING([--disable-shiftenter], [force to disable Shift+Enter key-binding]))
if test "$enable_shiftenter" != "no"; then
	AC_DEFINE(ENABLE_SHIFTENTER, 1, [Define if Shift+Enter is enabled.])
fi

AC_ARG_ENABLE(chooser,
	AC_HELP_STRING([--disable-chooser], [force to use GtkFileSelector]))
if test "$enable_chooser" != "no"; then
	PKG_CHECK_EXISTS(gtk+-2.0 >= 2.4.0,
		AC_DEFINE(ENABLE_CHOOSER, 1, [Define if GtkFileChooser is enabled.]))
fi

AC_ARG_ENABLE(findhistory,
	AC_HELP_STRING([--disable-findhistory], [force to use simple text entry for search and replace]))
if test "$enable_findhistory" != "no"; then
   AC_DEFINE(SEARCH_HISTORY, 1, [Define if search/replace history is enabled.])
fi

AC_ARG_ENABLE(print,
	AC_HELP_STRING([--disable-print], [force to disable print feature]))
if test "$enable_print" != "no"; then
	PKG_CHECK_EXISTS(gtk+-2.0 >= 2.10.0, have_print=yes, [
		PKG_CHECK_MODULES(GNOMEPRINT, libgnomeprintui-2.2,
			have_print=yes, have_print=no)])
	if test "$have_print" = "yes"; then
		AC_DEFINE(ENABLE_PRINT, 1, [Define if print feature is enabled.])
	fi
fi

AC_ARG_ENABLE(emacs,
	AC_HELP_STRING([--enable-emacs], [implement Emacs key theme (experimental)]),
	AC_DEFINE(ENABLE_EMACS, 1, [Define if Emacs key theme is enabled.])
)

dnl ========== Check for Hildon Libraries
PKG_CHECK_MODULES(HILDON,
  hildon-libs hildon-fm libosso,
  HAVE_HILDON=yes, HAVE_HILDON=no)

if test "x$HAVE_HILDON" = "xyes"; then
  AC_DEFINE(USE_HILDON, 1, [build with hildon libs])
fi

AM_CONDITIONAL(USE_HILDON, test "x$HAVE_HILDON" = "xyes")

dnl make HILDON_CFLAGS and HILDON_LIBS available
AC_SUBST(HILDON_CFLAGS)
AC_SUBST(HILDON_LIBS)

GETTEXT_PACKAGE="$PACKAGE"
AC_SUBST(GETTEXT_PACKAGE)
AM_GLIB_GNU_GETTEXT
AM_GLIB_DEFINE_LOCALEDIR(LOCALEDIR)

AC_CONFIG_FILES([
	Makefile
	src/Makefile
	src/charset-detector/Makefile
	src/charset-detector/include/Makefile
	src/charset-detector/src/Makefile
	src/charset-detector/src/entry/Makefile
	src/charset-detector/src/tables/Makefile
	src/charset-detector/test/Makefile
	data/Makefile
	data/icons/Makefile
	data/icons/16x16/Makefile
	data/icons/22x22/Makefile
	data/icons/24x24/Makefile
	data/icons/32x32/Makefile
	data/icons/scalable/Makefile
	po/Makefile.in
])
AC_OUTPUT

