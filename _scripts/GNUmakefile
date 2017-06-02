
GURU_DIR ?= guru
WATT_DIR ?= watt
VOLTA_DIR ?= volta
DIODE_DIR ?= diode
METAL_DIR ?= metal
CHARGE_DIR ?= charge
OUTPUT_DIR ?= $(GURU_DIR)/_output

DIODE ?= $(shell which diode)
VOLTA ?= $(shell which volt)

BASE_FLAGS=--no-backend -jo $@ \
	--lib-I $(VOLTA_DIR)/rt/src \
	--lib-I $(WATT_DIR)/src

VDOC_GURU_FILES=$(shell find watt/src volta/rt/src/core -type f)
VDOC_VOLTA_FILES=$(VOLTA_DIR)/src/main.d
VDOC_METAL_FILES=$(shell find $(METAL_DIR)/src -type f -name "*.volt")
VDOC_DIODE_FILES=$(shell find $(DIODE_DIR)/src -type f -name "*.volt")
VDOC_CHARGE_FILES=$(shell find $(CHARGE_DIR)/src -type f -name "*.volt")

GURU_FLAGS = $(BASE_FLAGS) $(VDOC_GURU_FILES)
VOLTA_FLAGS = $(BASE_FLAGS) $(VDOC_VOLTA_FILES) --internal-d --src-I $(VOLTA_DIR)/src
METAL_FLAGS = $(BASE_FLAGS) $(VDOC_METAL_FILES)
DIODE_FLAGS = $(BASE_FLAGS) $(VDOC_DIODE_FILES) -J $(DIODE_DIR)/res
CHARGE_FLAGS = $(BASE_FLAGS) $(VDOC_CHARGE_FILES) -J $(CHARGE_DIR)/res


GURU_JSON = $(GURU_DIR)/_tmp/guru.json
VOLTA_JSON = $(GURU_DIR)/_tmp/volta.json
DIODE_JSON = $(GURU_DIR)/_tmp/diode.json
METAL_JSON = $(GURU_DIR)/_tmp/metal.json
CHARGE_JSON = $(GURU_DIR)/_tmp/charge.json

VDOC_JSON = $(GURU_JSON) $(DIODE_JSON) $(METAL_JSON) $(VOLTA_JSON) $(CHARGE_JSON)


#
# Rules start here.
#

all: docu

$(GURU_JSON): $(VOLTA) $(VDOC_GURU_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(GURU_FLAGS)

$(VOLTA_JSON): $(VOLTA) $(VDOC_VOLTA_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(VOLTA_FLAGS)

$(METAL_JSON): $(VOLTA) $(VDOC_METAL_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(METAL_FLAGS)

$(DIODE_JSON): $(VOLTA) $(VDOC_DIODE_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(DIODE_FLAGS)

$(CHARGE_JSON): $(VOLTA) $(VDOC_CHARGE_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(CHARGE_FLAGS)

docu: $(VDOC_JSON)
	@echo "  DIODE    site"
	@rm -rf $(OUTPUT_DIR)
	@cp -r $(GURU_DIR)/_site $(OUTPUT_DIR)
	@$(DIODE) \
		-s $(GURU_DIR) -d $(OUTPUT_DIR) \
		--baseurl "http://volt.guru" \
		$(GURU_JSON)
	@$(DIODE) \
		-s $(METAL_DIR)/doc -d $(OUTPUT_DIR)/metal \
		--baseurl "http://volt.guru/metal" \
		$(METAL_JSON)
	@$(DIODE) \
		-s $(DIODE_DIR)/doc -d $(OUTPUT_DIR)/diode \
		--baseurl "http://volt.guru/diode" \
		$(DIODE_JSON)
	@$(DIODE) \
		-s $(VOLTA_DIR)/doc -d $(OUTPUT_DIR)/volta \
		--baseurl "http://volt.guru/volta" \
		$(VOLTA_JSON)
	@$(DIODE) \
		-s $(CHARGE_DIR)/doc -d $(OUTPUT_DIR)/charge \
		--baseurl "http://volt.guru/charge" \
		$(CHARGE_JSON)

.PHONY: all guru