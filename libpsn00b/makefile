# Run using make (Linux) or gmake (BSD)
# Part of the PSn00bSDK Project
# 2019 Lameguy64 / Meido-Tek Productions

TOPTARGETS	= all clean

LIBDIRS 	= lzp psxgpu psxgte psxapi psxetc psxspu psxsio psxcd


$(TOPTARGETS): $(LIBDIRS)
$(LIBDIRS):
	@$(MAKE) -C $@ $(MAKECMDGOALS)

clean: $(LIBDIRS)

.PHONY: $(TOPTARGETS) $(LIBDIRS)
