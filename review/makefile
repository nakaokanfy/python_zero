RE=introduction.re about.re install.re hello.re basic.re scope.re list.re string.re file.re recursion.re class.re numpy.re howtowork.re dp.re random.re simulation.re ml.re answer.re references.re
MD=$(RE:.re=.md)
DIRS=$(RE:.re=)
TARGET=python_zero.pdf

.PHONY: clean imgcopy

all: $(TARGET)


dir:
	echo $(DIRS)

%.md:
	cp ../$*/README.md $@

imgcopy:
	for dir in $(DIRS);\
		do mkdir -p images/$$dir;\
		cp ../$$dir/fig/*.png images/$$dir 2>/dev/null;\
		done

%.re: %.md
	ruby md2re.rb $^ > $*.re

$(TARGET): catalog.yml config.yml $(RE) imgcopy
	docker run --rm -v `pwd`/:/work kauplan/review2.5 /bin/bash -c "cd /work; rake pdf"

wsl: catalog.yml config.yml $(RE) imgcopy
	#docker run --rm -v c:\\Users\\watanabe\\Desktop\\github\\python_zero\\review:/work kauplan/review2.5 /bin/bash -c "cp -r work work2;cd /work2; rake pdf;cp python_zero.pdf /work"
	docker run --rm -v c:\\Users\\watanabe\\Desktop\\github\\python_zero\\review:/work kauplan/review2.5 /bin/bash -c "cd /work; rake pdf"

clean:
	rm -f $(TARGET) *.post *.pre $(RE) $(MD)
