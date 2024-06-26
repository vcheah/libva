# Copyright (c) 2007 Intel Corporation. All Rights Reserved.
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the
# "Software"), to deal in the Software without restriction, including
# without limitation the rights to use, copy, modify, merge, publish,
# distribute, sub license, and/or sell copies of the Software, and to
# permit persons to whom the Software is furnished to do so, subject to
# the following conditions:
# 
# The above copyright notice and this permission notice (including the
# next paragraph) shall be included in all copies or substantial portions
# of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
# OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT.
# IN NO EVENT SHALL PRECISION INSIGHT AND/OR ITS SUPPLIERS BE LIABLE FOR
# ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
# TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
# SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

SUBDIRS =

AM_CPPFLAGS = \
	-I$(top_srcdir) \
	-DSYSCONFDIR='"$(sysconfdir)"' \
	-DVA_DRIVERS_PATH="\"$(LIBVA_DRIVERS_PATH)\""

LDADD = \
	$(LIBVA_LT_LDFLAGS)

libva_source_c = \
	va.c			\
	va_compat.c		\
	va_str.c		\
	va_trace.c		\
	$(NULL)

libva_source_h = \
	va.h			\
	va_backend.h		\
	va_backend_prot.h	\
	va_backend_vpp.h	\
	va_compat.h		\
	va_dec_av1.h		\
	va_dec_hevc.h		\
	va_dec_jpeg.h		\
	va_dec_vp8.h		\
	va_dec_vp9.h		\
	va_dec_vvc.h		\
	va_drmcommon.h		\
	va_egl.h		\
	va_enc_hevc.h		\
	va_enc_h264.h		\
	va_enc_jpeg.h		\
	va_enc_vp8.h		\
	va_fei.h    		\
	va_fei_h264.h		\
	va_enc_mpeg2.h		\
	va_fei_hevc.h 		\
	va_enc_vp9.h            \
	va_enc_av1.h            \
	va_str.h		\
	va_tpi.h		\
	va_version.h		\
	va_prot.h		\
	va_vpp.h		\
	$(NULL)

libva_source_h_priv = \
	sysdeps.h		\
	va_internal.h		\
	va_trace.h		\
	$(NULL)

libva_ldflags = \
	$(LDADD) -no-undefined	\
	-Wl,-version-script,${srcdir}/libva.syms \
	$(NULL)

libva_cflags = \
	-Wall			\
	$(NULL)

libva_cflags += $(SSP_CC_FLAG)

lib_LTLIBRARIES			= libva.la
libvaincludedir			= ${includedir}/va
libvainclude_HEADERS		= $(libva_source_h)
noinst_HEADERS			= $(libva_source_h_priv)
libva_la_SOURCES		= $(libva_source_c)
libva_la_CFLAGS			= $(libva_cflags)
libva_la_LDFLAGS		= $(libva_ldflags)
libva_la_DEPENDENCIES		= libva.syms
libva_la_LIBADD			= $(LIBVA_LIBS)

if USE_DRM
SUBDIRS				+= drm
lib_LTLIBRARIES			+= libva-drm.la
libva_drm_la_SOURCES		=
libva_drm_la_CFLAGS		= $(libva_cflags)
libva_drm_la_LDFLAGS		= $(LDADD)
libva_drm_la_DEPENDENCIES	= libva.la drm/libva_drm.la
libva_drm_la_LIBADD		= libva.la drm/libva_drm.la \
	$(LIBVA_LIBS) $(DRM_LIBS)
endif

if USE_X11
SUBDIRS				+= x11
lib_LTLIBRARIES			+= libva-x11.la
libva_source_h			+= va_x11.h
libva_x11_la_SOURCES		= 
libva_x11_la_CFLAGS		= $(libva_cflags)
libva_x11_la_LDFLAGS		= $(LDADD)
libva_x11_la_DEPENDENCIES	= libva.la x11/libva_x11.la
libva_x11_la_LIBADD		= libva.la x11/libva_x11.la \
	$(LIBVA_LIBS) $(X11_LIBS) $(XEXT_LIBS) $(XFIXES_LIBS) $(DRM_LIBS)
endif

if USE_GLX
SUBDIRS				+= glx
lib_LTLIBRARIES			+= libva-glx.la
libva_glx_la_SOURCES		=
libva_glx_la_CFLAGS		= $(libva_cflags)
libva_glx_la_LDFLAGS		= $(LDADD)
libva_glx_la_DEPENDENCIES	= libva.la glx/libva_glx.la libva-x11.la
libva_glx_la_LIBADD		= libva.la glx/libva_glx.la libva-x11.la \
	$(GLX_LIBS)
endif

if USE_WAYLAND
SUBDIRS				+= wayland
lib_LTLIBRARIES			+= libva-wayland.la
libva_wayland_la_SOURCES	=
libva_wayland_la_CFLAGS		= $(libva_cflags)
libva_wayland_la_LDFLAGS	= $(LDADD)
libva_wayland_la_DEPENDENCIES	= libva.la wayland/libva_wayland.la
libva_wayland_la_LIBADD		= libva.la wayland/libva_wayland.la \
	$(WAYLAND_LIBS) $(DRM_LIBS)
endif

DIST_SUBDIRS = x11 glx drm wayland

DISTCLEANFILES = \
	va_version.h		\
	$(NULL)

EXTRA_DIST = \
	libva.syms		\
	va_version.h.in		\
	meson.build		\
        libva.def               \
	$(NULL)
