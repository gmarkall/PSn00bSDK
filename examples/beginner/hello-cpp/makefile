include ../../sdk-common.mk

# Project target name
TARGET		= hello.elf

# Searches for C, C++ and S (assembler) files in local directory
CFILES		= $(notdir $(wildcard *.c))
CPPFILES 	= $(notdir $(wildcard *.cpp))
AFILES		= $(notdir $(wildcard *.s))

# Determine object files
OFILES		= $(addprefix build/,$(CFILES:.c=.o)) \
			$(addprefix build/,$(CPPFILES:.cpp=.o)) \
			$(addprefix build/,$(AFILES:.s=.o))

# Project specific include and library directories
# (use -I for include dirs, -L for library dirs)
INCLUDE	 	+=
LIBDIRS		+=

# Libraries to link
LIBS		= -lpsxetc -lpsxgpu -lpsxgte -lpsxspu -lpsxapi -lpsxsys \
		  -lstdc++ -lc -Wl,--start-group -lgcc -lc -lpsxsys -Wl,--end-group

# C compiler flags
CFLAGS		= -g -O2 -fno-builtin -fdata-sections -ffunction-sections

# C++ compiler flags
CPPFLAGS	= $(CFLAGS) -fno-exceptions

# Assembler flags
AFLAGS		= -g -msoft-float

# Linker flags
LDFLAGS		=  -g -Wl,-gc-sections \
			-Wl,-T,psx.ld -Wl,-Map,main.map

# Toolchain programs
CC			= $(PREFIX)gcc
CXX			= $(PREFIX)g++
AS			= $(PREFIX)as
LD			= $(PREFIX)g++

all: $(OFILES)
	$(LD) $(LDFLAGS) $(LIBDIRS) $(OFILES) $(LIBS) -o $(TARGET)
	elf2x -q $(TARGET)
	
build/%.o: %.c
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@
	
build/%.o: %.cpp
	@mkdir -p $(dir $@)
	$(CXX) $(CPPFLAGS) $(INCLUDE) -c $< -o $@
	
build/%.o: %.s
	@mkdir -p $(dir $@)
	$(CC) $(AFLAGS) $(INCLUDE) -c $< -o $@
	
clean:
	rm -rf build $(TARGET) $(TARGET:.elf=.exe)
