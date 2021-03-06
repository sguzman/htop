
ACLOCAL_AMFLAGS = -I m4
AUTOMAKE_OPTIONS = subdir-objects

bin_PROGRAMS = htop

dist_man_MANS = htop.1
EXTRA_DIST = $(dist_man_MANS) htop.desktop htop.png scripts/MakeHeader.py \
install-sh autogen.sh missing
applicationsdir = $(datadir)/applications
applications_DATA = htop.desktop
pixmapdir = $(datadir)/pixmaps
pixmap_DATA = htop.png

htop_CFLAGS = -pedantic -Wall $(wextra_flag) -std=c99 -rdynamic -D_XOPEN_SOURCE_EXTENDED -DSYSCONFDIR=\"$(sysconfdir)\" -I"$(my_htop_platform)"
AM_CPPFLAGS = -DNDEBUG

myhtopsources = AvailableMetersPanel.c CategoriesPanel.c CheckItem.c \
ClockMeter.c ColorsPanel.c ColumnsPanel.c CPUMeter.c CRT.c \
DisplayOptionsPanel.c FunctionBar.c Hashtable.c Header.c htop.c ListItem.c \
LoadAverageMeter.c MemoryMeter.c Meter.c MetersPanel.c Object.c Panel.c \
BatteryMeter.c Process.c ProcessList.c RichString.c ScreenManager.c Settings.c \
SignalsPanel.c String.c SwapMeter.c TasksMeter.c UptimeMeter.c TraceScreen.c \
UsersTable.c Vector.c AvailableColumnsPanel.c AffinityPanel.c \
HostnameMeter.c OpenFilesScreen.c Affinity.c IncSet.c Action.c

myhtopheaders = AvailableColumnsPanel.h AvailableMetersPanel.h \
CategoriesPanel.h CheckItem.h ClockMeter.h ColorsPanel.h ColumnsPanel.h \
CPUMeter.h CRT.h DisplayOptionsPanel.h FunctionBar.h \
Hashtable.h Header.h htop.h ListItem.h LoadAverageMeter.h MemoryMeter.h \
BatteryMeter.h Meter.h MetersPanel.h Object.h Panel.h ProcessList.h RichString.h \
ScreenManager.h Settings.h SignalsPanel.h String.h SwapMeter.h TasksMeter.h \
UptimeMeter.h TraceScreen.h UsersTable.h Vector.h Process.h AffinityPanel.h \
HostnameMeter.h OpenFilesScreen.h Affinity.h IncSet.h Action.h

if HTOP_LINUX
myhtopplatsources = linux/Platform.c linux/IOPriorityPanel.c linux/IOPriority.c \
linux/LinuxProcess.c linux/LinuxProcessList.c linux/LinuxCRT.c linux/Battery.c

myhtopplatheaders = linux/Platform.h linux/IOPriorityPanel.h linux/IOPriority.h \
linux/LinuxProcess.h linux/LinuxProcessList.h linux/LinuxCRT.h linux/Battery.h
endif

if HTOP_UNSUPPORTED
myhtopplatsources = unsupported/Platform.c \
unsupported/UnsupportedProcess.c unsupported/UnsupportedProcessList.c \
unsupported/UnsupportedCRT.c unsupported/Battery.c

myhtopplatheaders = unsupported/Platform.h \
unsupported/UnsupportedProcess.h unsupported/UnsupportedProcessList.h \
unsupported/UnsupportedCRT.h unsupported/Battery.h
endif

SUFFIXES = .h

BUILT_SOURCES = $(myhtopheaders) $(myhtopplatheaders)
htop_SOURCES  = $(myhtopheaders) $(myhtopplatheaders) $(myhtopsources) $(myhtopplatsources) config.h

target:
	echo $(htop_SOURCES)

profile:
	$(MAKE) all CFLAGS="-pg" AM_CPPFLAGS="-pg -O2 -DNDEBUG"

debug:
	$(MAKE) all CFLAGS="" AM_CPPFLAGS="-ggdb -DDEBUG"

.c.h:
	@srcdir@/scripts/MakeHeader.py $<

cppcheck:
	cppcheck -q -v . --enable=all -DHAVE_CGROUP -DHAVE_OPENVZ -DHAVE_TASKSTATS

