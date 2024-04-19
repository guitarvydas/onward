projectdir=.
0D=0d/python
das2jsondir=0D/das2json/
STD=${0D}/std

0Dsrc = ${0D}/gensym.py \
    ${0D}/datum.py \
    ${0D}/message.py \
    ${0D}/dynrouting.py \
    ${0D}/container.py \
    ${0D}/registry.py \
    ${0D}/process.py \
    ${0D}/0d.py \
    ${STD}/std.py \
    ${STD}/lib.py \
    ${STD}/fakepipe.py \
    ${STD}/stock.py \
    ${STD}/run.py

all : clear _.py helloworld0d.drawio.json
	python3 _.py ${projectdir} ${0D} "0D was here" main helloworld0d.drawio.json

clear:
	clear

clean:
	rm -f _.py

_.py: ${0Dsrc}
	cat ${0Dsrc} ./main.py > _.py

helloworld0d.draw.json : helloworld0d.drawio
	${das2jsondir}/das2json helloworld0d.drawio


install:
	./makedas2json.bash ${das2jsondir}

