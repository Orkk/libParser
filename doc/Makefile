SUBDIRS	= gtkdoc
TARGETS	= gtkdoc/libParser.types gtkdoc/tmpl.stamp gtkdoc/sgml.stamp gtkdoc/html.stamp
PREFIX	= /usr/local
DESTDIR	=
RM	= rm -f
LN	= ln -f
MKDIR	= mkdir -m 0755 -p
INSTALL	= install


all: subdirs $(TARGETS)

subdirs:
	@for i in $(SUBDIRS); do (cd "$$i" && $(MAKE)) || exit; done

gtkdoc/libParser.types:
	./gtkdoc.sh -P "$(PREFIX)" -- "gtkdoc/libParser.types"

gtkdoc/tmpl.stamp: gtkdoc/libParser.types
	./gtkdoc.sh -P "$(PREFIX)" -- "gtkdoc/tmpl.stamp"

gtkdoc/sgml.stamp: gtkdoc/tmpl.stamp
	./gtkdoc.sh -P "$(PREFIX)" -- "gtkdoc/sgml.stamp"

gtkdoc/html.stamp: gtkdoc/libParser-docs.xml gtkdoc/sgml.stamp
	./gtkdoc.sh -P "$(PREFIX)" -- "gtkdoc/html.stamp"

clean:
	@for i in $(SUBDIRS); do (cd "$$i" && $(MAKE) clean) || exit; done
	$(RM) -- $(gtkdoc/libParser.types_OBJS) $(gtkdoc/tmpl.stamp_OBJS) $(gtkdoc/sgml.stamp_OBJS) $(gtkdoc/html.stamp_OBJS)
	./gtkdoc.sh -c -P "$(PREFIX)" -- "gtkdoc/html.stamp"

distclean:
	@for i in $(SUBDIRS); do (cd "$$i" && $(MAKE) distclean) || exit; done
	$(RM) -- $(gtkdoc/libParser.types_OBJS) $(gtkdoc/tmpl.stamp_OBJS) $(gtkdoc/sgml.stamp_OBJS) $(gtkdoc/html.stamp_OBJS)
	./gtkdoc.sh -c -P "$(PREFIX)" -- "gtkdoc/html.stamp"
	$(RM) -- $(TARGETS)

install: $(TARGETS)
	@for i in $(SUBDIRS); do (cd "$$i" && $(MAKE) install) || exit; done
	./gtkdoc.sh -P "$(DESTDIR)$(PREFIX)" -i -- "gtkdoc/html.stamp"

uninstall:
	@for i in $(SUBDIRS); do (cd "$$i" && $(MAKE) uninstall) || exit; done
	./gtkdoc.sh -P "$(DESTDIR)$(PREFIX)" -u -- "gtkdoc/html.stamp"

.PHONY: all subdirs clean distclean install uninstall
