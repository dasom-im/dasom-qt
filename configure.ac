dnl Process this file with autoconf to produce a configure script.

AC_INIT(dasom-qt, 1.2.2, https://github.com/dasom-im/dasom-qt/issues)

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([-Wall -Werror])
AM_MAINTAINER_MODE([disable])
AM_SILENT_RULES([yes])

AM_PROG_AR
AC_PROG_CXX

LT_INIT([disable-static])

PKG_CHECK_MODULES(DASOM, [dasom])
PKG_CHECK_MODULES(QT4_GUI, [QtGui])
PKG_CHECK_MODULES(QT5_WIDGETS, [Qt5Widgets])
PKG_CHECK_MODULES(QT5_PLATFORM_SUPPORT, [Qt5PlatformSupport])

AC_PATH_PROGS([QT5_MOC], [moc-qt5 moc], [no],
              [`pkg-config --variable=host_bins Qt5Core`])
if test "x$QT5_MOC" = "xno"; then
  AC_MSG_ERROR([moc for qt5 not found])
fi

QT5_LIB_DIR=`pkg-config --variable=libdir Qt5PlatformSupport`

case `pkg-config --variable=host_bins Qt5Core` in
  */qt5/*)
    QT5_IM_MODULE_DIR=$QT5_LIB_DIR/qt5/plugins/platforminputcontexts
    ;;
  */qt/*)
    QT5_IM_MODULE_DIR=$QT5_LIB_DIR/qt/plugins/platforminputcontexts
    ;;
  *)
    AC_MSG_ERROR(Can not determine Qt5 plugins/platforminputcontexts directory)
    ;;
esac

AC_SUBST(QT5_IM_MODULE_DIR)

AC_OUTPUT([
  Makefile
  qt4/Makefile
  qt5/Makefile
])
