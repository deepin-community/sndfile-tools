EXTRA_DIST = \
	README.md \
	Scripts/calc-hilbert-fir.m

dist_html_DATA = \
	doc/index.html \
	doc/sweep.png \
	doc/wave-example.png \
	doc/wave-sweep.png \
	doc/libsndfile.css

bin_PROGRAMS = \
	bin/sndfile-generate-chirp \
	bin/sndfile-spectrogram \
	bin/sndfile-mix-to-mono \
	bin/sndfile-resample \
	bin/sndfile-waveform

CLEANFILES = src/*~

dist_man_MANS = \
	man/sndfile-generate-chirp.1 \
	man/sndfile-spectrogram.1 \
	man/sndfile-mix-to-mono.1 \
	man/sndfile-jackplay.1 \
	man/sndfile-resample.1

#=========================================================================================
# The bin targets.

bin_sndfile_generate_chirp_SOURCES = \
	src/common.c \
	src/common.h \
	src/generate-chirp.c
bin_sndfile_generate_chirp_CFLAGS = $(SNDFILE_CFLAGS)
bin_sndfile_generate_chirp_LDADD = $(SNDFILE_LIBS)

bin_sndfile_spectrogram_SOURCES = \
	src/common.c \
	src/common.h \
	src/spectrogram.c \
	src/spectrum.c \
	src/spectrum.h \
	src/window.c \
	src/window.h
bin_sndfile_spectrogram_CFLAGS = $(SNDFILE_CFLAGS) $(FFTW3_CFLAGS) $(CAIRO_CFLAGS)
bin_sndfile_spectrogram_LDADD = $(SNDFILE_LIBS) $(FFTW3_LIBS) $(CAIRO_LIBS)

bin_sndfile_mix_to_mono_SOURCES = \
	src/common.c \
	src/common.h \
	src/mix-to-mono.c
bin_sndfile_mix_to_mono_CFLAGS = $(SNDFILE_CFLAGS)
bin_sndfile_mix_to_mono_LDADD = $(SNDFILE_LIBS)

bin_sndfile_waveform_SOURCES = \
	src/common.c \
	src/common.h \
	src/waveform.c
bin_sndfile_waveform_CFLAGS = $(SNDFILE_CFLAGS) $(CAIRO_CFLAGS)
bin_sndfile_waveform_LDADD = $(SNDFILE_LIBS) $(CAIRO_LIBS)

bin_sndfile_resample_SOURCES = \
	src/common.c \
	src/common.h \
	src/resample.c
bin_sndfile_resample_CFLAGS = $(SNDFILE_CFLAGS) $(SAMPLERATE_CFLAGS)
bin_sndfile_resample_LDADD = $(SNDFILE_LIBS) $(SAMPLERATE_LIBS)

if HAVE_JACK
bin_PROGRAMS += bin/sndfile-jackplay
bin_sndfile_jackplay_SOURCES = src/jackplay.c
bin_sndfile_jackplay_CFLAGS = $(SNDFILE_CFLAGS) $(JACK_CFLAGS)
bin_sndfile_jackplay_LDADD = $(SNDFILE_LIBS) $(JACK_LIBS)
endif

#=========================================================================================
# The make check targets.

# Test programs or programs not yet working.
check_PROGRAMS = \
	tests/common_tests \
	tests/kaiser_window_test

tests_kaiser_window_test_SOURCES = \
	src/window.c \
	src/window.h \
	tests/kaiser_window_test.c

tests_common_tests_SOURCES = \
	src/common.c \
	src/common.h \
	tests/common_tests.c
tests_common_tests_CFLAGS = $(SNDFILE_CFLAGS)
tests_common_tests_LDADD = $(SNDFILE_LIBS)

EXTRA_DIST += tests/test-wrapper.sh
TESTS = \
	$(check_PROGRAMS) \
	tests/test-wrapper.sh

# The 'dist-clean' target on Mac OSX fails without this.
clean-local:
	rm -rf bin/*.dSYM
