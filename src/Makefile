CXX=c++
DEFS=
INC=

#recommended if supported by your GCC
#DEFS+=-fsanitize=address

# Cygwin was reported to require this:
#DEFS+=-U__STRICT_ANSI__


# this worked for me on OSX
#INC+=-I/usr/local/ssl/include
#LIBS+=-L/usr/local/ssl/lib
#LIBS+=-Wl,--rpath=/usr/local/ssl/lib


# LibreSSL setups, define your paths here
#INC+=-I/usr/local/libressl/include
#LIBS+=-L/usr/local/libressl/lib64
#LIBS+=-Wl,--rpath=/usr/local/libressl/lib64
#DEFS+=-DHAVE_BN_GENCB_NEW=0
#DEFS+=-DHAVE_LIBRESSL


# BoringSSL. Be warned, BoringSSL creates incompatible
# PEM files. So this is not recommended and just for
# testing.
#BSSL=/opt/boringssl
#INC+=-I$(BSSL)/include
#LIBS+=-L$(BSSL)/build/crypto -Wl,--rpath=$(BSSL)/build/crypto
#DEFS+=-DHAVE_BN_GENCB_NEW=0
#DEFS+=-DHAVE_BORINGSSL


# Enable chacha20-poly1305 if avail
#DEFS+=-DCHACHA20

CXXFLAGS=-Wall -O2 -pedantic -std=c++11 $(INC) $(DEFS)

LD=c++
LDFLAGS=
LIBS+=-lcrypto


all: opmsg

contrib: opmux opcoin

opmsg: keystore.o opmsg.o misc.o config.o message.o marker.o base64.o deleters.o missing.o
	$(LD) keystore.o opmsg.o misc.o config.o message.o marker.o base64.o deleters.o missing.o $(LDFLAGS) $(LIBS) -o $@

opcoin: keystore.o opcoin.o config.o deleters.o base58.o misc.o marker.o deleters.o missing.o
	$(LD) keystore.o opcoin.o config.o base58.o misc.o marker.o deleters.o missing.o $(LDFLAGS) $(LIBS) -o $@

opmux: keystore.o opmux.o misc.o marker.o config.o deleters.o missing.o
	$(LD) keystore.o opmux.o misc.o marker.o config.o deleters.o missing.o $(LDFLAGS) $(LIBS) -o $@

opmux.o: contrib/opmux.cc
	$(CXX) -I . -I .. $(CXXFLAGS) -c $<

opcoin.o: contrib/opcoin.cc
	$(CXX) -I . -I .. $(CXXFLAGS) -c $<

base58.o: contrib/base58.cc
	$(CXX) -I . -I .. $(CXXFLAGS) -c $<

opmsg.o: opmsg.cc
	$(CXX) $(CXXFLAGS) -c $<

marker.o: marker.cc marker.h
	$(CXX) $(CXXFLAGS) -c $<

keystore.o: keystore.cc keystore.h
	$(CXX) $(CXXFLAGS) -c $<

base64.o: base64.cc base64.h
	$(CXX) $(CXXFLAGS) -c $<

misc.o: misc.cc misc.h
	$(CXX) $(CXXFLAGS) -c $<

config.o: config.cc config.h numbers.h
	$(CXX) $(CXXFLAGS) -c $<

message.o: message.cc message.h numbers.h
	$(CXX) $(CXXFLAGS) -c $<

deleters.o: deleters.cc
	$(CXX) $(CXXFLAGS) -c $<

missing.o: missing.cc missing.h
	$(CXX) $(CXXFLAGS) -c $<

clean:
	rm -rf *.o opmsg


