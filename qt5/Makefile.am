qt5_im_moduledir = $(QT5_IM_MODULE_DIR)
qt5_im_module_LTLIBRARIES = libqt5im-dasom.la

BUILT_SOURCES = im-dasom-qt5.moc
libqt5im_dasom_la_SOURCES = im-dasom-qt5.cpp $(BUILT_SOURCES)

libqt5im_dasom_la_CXXFLAGS = \
	-Wall \
	-Werror \
	$(DASOM_CFLAGS) \
	-DG_LOG_DOMAIN=\"dasom\" \
	$(DASOM_QT5_DEPS_CFLAGS) \
	-I$(QT5_GUI_INCLUDE_PATH) \
	-DQT_NO_KEYWORDS

libqt5im_dasom_la_LDFLAGS = -avoid-version -module \
	                          $(DASOM_QT5_DEPS_LIBS) $(DASOM_LIBS)

im-dasom-qt5.moc: im-dasom-qt5.cpp
	$(AM_V_GEN) $(QT5_MOC) -I $(QT5_GUI_INCLUDE_PATH) im-dasom-qt5.cpp \
	                       -o im-dasom-qt5.moc

install-data-hook:
	chmod -x $(DESTDIR)$(qt5_im_moduledir)/libqt5im-dasom.so
	rm -f    $(DESTDIR)$(qt5_im_moduledir)/libqt5im-dasom.la

uninstall-hook:
	 rm    -f $(DESTDIR)$(qt5_im_moduledir)/libqt5im-dasom.so
	-rmdir -p $(DESTDIR)$(qt5_im_moduledir)

DISTCLEANFILES = Makefile.in $(BUILT_SOURCES)
