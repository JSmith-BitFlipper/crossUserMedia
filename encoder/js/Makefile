CC = emcc

SOURCES = ../c/encoder.c
TARGET = dist/encoder.js
INSTALL_DIR = ../../frontend/node_modules/pcmencoder

LDFLAGS = -L./dist/lib

LDLIBS = -lm -lavdevice -lavformat -lavfilter -lavcodec -lswresample -lswscale -lavutil

CFLAGS = -v -O2 -g4 \
	-I./dist/include \
	-s ASSERTIONS=1 \
	-s NO_EXIT_RUNTIME=1 \
	-s EXPORTED_FUNCTIONS="['_main', '_init', '_load', '_flush', '_get_output_sample_rate', '_get_output_format', '_get_output_length', '_dispose']" \
	--pre-js pre.js \
	--post-js post.js

# 	-s OUTLINING_LIMIT=100000 \
#  	-s TOTAL_MEMORY=67108864 \
# 	-s USE_PTHREADS=1 \
#   -s BUILD_AS_WORKER=1 \


################################################################

all: program

program: prepare
	$(CC) $(CFLAGS) $(SOURCES) -o $(TARGET) $(LDFLAGS) $(LDLIBS)

prepare:
	mkdir -p dist

install:
	mkdir -p $(INSTALL_DIR)
	cp -f ./.npmignore $(INSTALL_DIR)
	cp -f ./dist/encoder.* $(INSTALL_DIR)
	cp -f ./package.json $(INSTALL_DIR)
	cp -f ./README.md $(INSTALL_DIR)

clean:
	rm -f dist/encoder.*
	rm -Rf $(INSTALL_DIR)
