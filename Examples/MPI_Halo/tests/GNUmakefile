.PHONY: clean tests
ifneq ($(BASEMK_INCLUDED),YES)
include $(PFUNIT)/include/base.mk
endif

SRCS = $(wildcard *.pf)
OBJS = $(SRCS:.pf=$(OBJ_EXT))

tests: $(OBJS)

testSuites.inc: $(SRCS)

FFLAGS += -I$(SRC_DIR) -I$(PFUNIT)/mod

ifndef SKIP_INTENTIONALLY_BROKEN
  FFLAGS += -DINCLUDE_INTENTIONALLY_BROKEN
endif

%.F90: %.pf
	$(PFUNIT)/bin/funitproc $<  $@

%$(OBJ_EXT): %.F90
	$(MPIF90) -c $(FFLAGS) $<

clean: local-E1-clean

local-E1-clean:
	$(RM) *$(OBJ_EXT) *.mod
