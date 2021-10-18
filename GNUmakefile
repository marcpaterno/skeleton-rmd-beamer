####################################
# Global Variables.

# Things we want to know how to build.
PRODUCTS = skeleton-talk.pdf \
 skeleton-talk-notes.pdf

IMAGES = d1a-1.png \
         equations.png \
         example_pipeline.png \
         galaxy-cluster.jpg \
         qplot-1.png \
		 repositories.png

# All PDFs should be made portable, with subsetted fonts.
PORTABLE_PDF = 1

# Show the command lines used.
# VERBOSE = 1

# Don't show command output or error.
QUIET = 2
####################################

####################################
# Use doc.mk to produce our documents.
ifneq (,$(SSDDOC_INC))
  ddir = $(SSDDOC_INC)
else
  ddir = ../cet-is/ssddoc/include
endif

include $(ddir)/doc.mk

# Check we have the version we need of doc.mk.
verified_doc_mk_version := $(call require_doc_mk_version,0.2.0)
####################################

####################################
# LaTeX-specific environment variables.

# LaTeXMK looks in TEXINPUTS for e.g. .bst files, but doesn't know how
# to look in recursive paths (//), so we add the specific directory for
# woc.bst to the front of TEXINPUTS.
export TEXINPUTS = $(DOC_MK_DIR)web-conf/:$(DOC_MK_DIR)/:
export BSTINPUTS = $(DOC_MK_DIR)web-conf/:
####################################

####################################
# Target-specific variables and additive overrides.
skeleton-talk.pdf: $(IMAGES)
skeleton-talk-notes.pdf: $(IMAGES)

# See doc.mk for a description of targets_with and friends.

our_beamer_targets = $(call targets_with,-talk)

# Re-do when we edit GNUmakefile.
$(our_beamer_targets): GNUmakefile

# Override some defaults.
$(our_beamer_targets): override PANDOC_BEAMER = 1

# Regenerate and clean up .bbl files.
override LATEXMK_EXTRA_OPTS += -bibtex

# Make Pandoc more verbose.
# override PANDOC_EXTRA_OPTS += --verbose
####################################
