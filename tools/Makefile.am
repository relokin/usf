if HAVE_ARGP
PROG_NEED_ARGP=usfdump usf2usf
endif

bin_PROGRAMS = usfsort usfcat usfstats usf2trace \
               usfresampler usfdiff usfsplit usfgentrace \
		$(PROG_NEED_ARGP)

CPPFLAGS = -I $(top_srcdir)/include

# XXX -lm is only needed by usfresampler
LDFLAGS += -lm -lusf 
LIBS += -L$(top_srcdir)/lib


usfdump_SOURCES = usfdump.c
usf2usf_SOURCES = usf2usf.c
usfsort_SOURCES = usfsort.cc
usfcat_SOURCES = usfcat.c
usfstats_SOURCES = usfstats.c
usf2trace_SOURCES = usf2trace.c
usfresampler_SOURCES = usfresampler.c
usfdiff_SOURCES = usfdiff.c
usfsplit_SOURCES = usfsplit.c
usfgentrace_SOURCES = usfgentrace.c
