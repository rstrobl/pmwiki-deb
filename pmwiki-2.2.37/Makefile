DESTDIR = $(CURDIR)/debian/pmwiki
TARGET_DIR = $(DESTDIR)/usr/share/pmwiki/
DOC_DIR = $(DESTDIR)/usr/share/doc/pmwiki/
CONF_DIR = $(DESTDIR)/etc/
WIKI_DIR = $(DESTDIR)/var/lib/pmwiki/

install:
	install -d $(TARGET_DIR)
	install -d $(DOC_DIR)
	install -d $(WIKI_DIR)
	install -d $(CONF_DIR)
	install -m622 ./pmwiki.php $(TARGET_DIR)
	install -m622 ./index.php $(TARGET_DIR)
	cp -rf ./pub/ $(TARGET_DIR)
	cp -rf ./scripts/ $(TARGET_DIR)
	cp -a `ls -1d ./docs/* |grep -v COPYING.txt | grep -v INSTALL.txt` $(DOC_DIR)
	cp -rf ./local/ $(CONF_DIR)/pmwiki
	cp -rf ./wikilib.d/ $(TARGET_DIR)
	cp -rf ./cookbook/ $(TARGET_DIR)
