pkglib_LTLIBRARIES = server-pages.la

factory.cpp:  
	fastcgi3-page-compiler -updateFactory=true -updateMakefile=false *.cpsp

server_pages_la_SOURCES = factory.cpp Login.cpp
server_pages_la_LDFLAGS = -module
server_pages_la_LIBADD = -lfastcgi3-container

AM_CPPFLAGS = -I../config
AM_CXXFLAGS = -pthread
AM_LDFLAGS =  


