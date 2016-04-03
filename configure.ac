dnl Process this file with autoconf to produce a configure script.

AC_INIT(dasom-qt, 1.2.5, https://github.com/dasom-im/dasom-qt/issues)

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
PKG_CHECK_MODULES(DASOM_QT5_DEPS, [Qt5Gui Qt5Widgets])

QT5_GUI_VERSION=`pkg-config --modversion Qt5Gui`
QT5_GUI_INCLUDE_DIR=`pkg-config --variable=includedir Qt5Gui`
QT5_GUI_INCLUDE_PATH=$QT5_GUI_INCLUDE_DIR/QtGui/$QT5_GUI_VERSION/QtGui

AC_CHECK_FILES(
   [$QT5_GUI_INCLUDE_PATH/qpa/qplatforminputcontext.h
    $QT5_GUI_INCLUDE_PATH/qpa/qplatforminputcontextplugin_p.h], [],
    AC_MSG_ERROR([Qt 5 base private development files are not found.]))

AC_SUBST(QT5_GUI_INCLUDE_PATH)

AC_PATH_PROGS([QT5_MOC], [moc-qt5 moc], [no],
              [`pkg-config --variable=host_bins Qt5Core`])
if test "x$QT5_MOC" = "xno"; then
  AC_MSG_ERROR([moc for qt5 not found])
fi

QT5_LIB_DIR=`pkg-config --variable=libdir Qt5Core`

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
