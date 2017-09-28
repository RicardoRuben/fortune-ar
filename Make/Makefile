
COOKIES= argentina.fortunes
STRFILE=/usr/bin/strfile

.PHONY: all cookies o-cookies w-cookies install clean

all: cookies o-cookies w-cookies

cookies: cookies-stamp

o-cookies:
	if [ $(OFFENSIVE) = 1 ] ; then \
	    cd ofensivas && $(MAKE) OCOOKIEDIR=$(OCOOKIEDIR) ; fi

w-cookies:
	if [ $(WEB) = 1 ] ; then \
	    cd html && $(MAKE) WCOOKIEDIR=$(WCOOKIEDIR); fi

cookies-stamp:
	rm -f *.dat
	for i in $(COOKIES) ; do $(STRFILE) $$i || exit $? ; done
	touch cookies-stamp

cookies-utf8-stamp:
	touch cookies-utf8-stamp

install: cookies-stamp
	install -m 0755 -d $(COOKIEDIR)
	if [ $(OFFENSIVE) = 1 ] ; then cd ofensivas && $(MAKE) install ; fi
	if [ $(WEB) = 1 ] ; then cd html && $(MAKE) install ; fi
	for i in $(COOKIES) ; do \
		install -m 0644 $$i $$i.dat $(COOKIEDIR) || exit $? ; done

install-utf8: cookies-utf8-stamp
	install -m 0755 -d $(COOKIEDIR)
	if [ $(OFFENSIVE) = 1 ] ; then cd ofensivas && $(MAKE) install-utf8 ; fi
	if [ $(WEB) = 1 ] ; then cd html && $(MAKE) install ; fi
	for i in $(COOKIES) ; do \
		install -m 0644 $$i $(COOKIEDIR) || exit $? ;   \
		recode latin1..u8 $(COOKIEDIR)/$$i;  \
		ln -s $$i $(COOKIEDIR)/$$i.u8; \
		strfile -s $(COOKIEDIR)/$$i; \
		done

clean:
	rm -f cookies-stamp cookies-utf8-stamp *.dat
	cd ofensivas && $(MAKE) clean
	cd html && $(MAKE) clean
