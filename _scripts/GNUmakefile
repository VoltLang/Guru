
AMP_DIR ?= amp
GURU_DIR ?= guru
WATT_DIR ?= watt
VOLTA_DIR ?= volta
DIODE_DIR ?= diode
TESLA_DIR ?= tesla
METAL_DIR ?= metal
PARSEC_DIR ?= parsec
CHARGE_DIR ?= charge
BATTERY_DIR ?= battery

JSON_DIR ?= $(GURU_DIR)/_tmp
OUTPUT_DIR ?= $(GURU_DIR)/_output

DIODE ?= $(shell which diode)
VOLTA ?= $(shell which volt)

BASE_FLAGS=--no-backend -jo $@ \
	--lib-I $(VOLTA_DIR)/rt/src \
	--lib-I $(WATT_DIR)/src

VDOC_AMP_FILES=$(shell find $(AMP_DIR)/src -type f -name "*.volt")
VDOC_VRT_FILES=$(shell find $(VOLTA_DIR)/rt/src/vrt -type f -name "*.volt")
VDOC_GURU_FILES=$(shell find $(WATT_DIR)/src $(VOLTA_DIR)/rt/src/core -type f -name "*.volt")
VDOC_VOLTA_FILES=$(VOLTA_DIR)/src/main.d
VDOC_DIODE_FILES=$(shell find $(DIODE_DIR)/src -type f -name "*.volt")
VDOC_TESLA_FILES=$(shell find $(TESLA_DIR)/src -type f -name "*.volt")
VDOC_METAL_FILES=$(shell find $(METAL_DIR)/src -type f -name "*.volt")
VDOC_PARSEC_FILES=$(shell find $(PARSEC_DIR)/src -type f -name "*.volt")
VDOC_CHARGE_FILES=$(shell find $(CHARGE_DIR)/src -type f -name "*.volt")
VDOC_BATTERY_FILES=$(shell find $(BATTERY_DIR)/src -type f -name "*.volt")

AMP_FLAGS = $(BASE_FLAGS) $(VDOC_AMP_FILES)
VRT_FLAGS = $(BASE_FLAGS) $(VDOC_VRT_FILES)
GURU_FLAGS = $(BASE_FLAGS) $(VDOC_GURU_FILES)
VOLTA_FLAGS = $(BASE_FLAGS) $(VDOC_VOLTA_FILES) --internal-d --src-I $(VOLTA_DIR)/src
DIODE_FLAGS = $(BASE_FLAGS) $(VDOC_DIODE_FILES) -J $(DIODE_DIR)/res
TESLA_FLAGS = $(BASE_FLAGS) $(VDOC_TESLA_FILES)
METAL_FLAGS = $(BASE_FLAGS) $(VDOC_METAL_FILES)
PARSEC_FLAGS = $(BASE_FLAGS) $(VDOC_PARSEC_FILES)
CHARGE_FLAGS = $(BASE_FLAGS) $(VDOC_CHARGE_FILES) -J $(CHARGE_DIR)/res
BATTERY_FLAGS = $(BASE_FLAGS) $(VDOC_BATTERY_FILES)


AMP_JSON = $(JSON_DIR)/amp.json
VRT_JSON = $(JSON_DIR)/vrt.json
GURU_JSON = $(JSON_DIR)/guru.json
VOLTA_JSON = $(JSON_DIR)/volta.json
DIODE_JSON = $(JSON_DIR)/diode.json
TESLA_JSON = $(JSON_DIR)/tesla.json
METAL_JSON = $(JSON_DIR)/metal.json
PARSEC_JSON = $(JSON_DIR)/parsec.json
CHARGE_JSON = $(JSON_DIR)/charge.json
BATTERY_JSON = $(JSON_DIR)/battery.json

VDOC_JSON = \
	$(AMP_JSON) \
	$(VRT_JSON) \
	$(GURU_JSON) \
	$(VOLTA_JSON) \
	$(DIODE_JSON) \
	$(TESLA_JSON) \
	$(METAL_JSON) \
	$(PARSEC_JSON) \
	$(CHARGE_JSON) \
	$(BATTERY_JSON)


#
# Rules start here.
#

all: docu

$(AMP_JSON): $(VOLTA) $(VDOC_AMP_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(AMP_FLAGS)

$(VRT_JSON): $(VOLTA) $(VDOC_VRT_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(VRT_FLAGS)

$(GURU_JSON): $(VOLTA) $(VDOC_GURU_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(GURU_FLAGS)

$(VOLTA_JSON): $(VOLTA) $(VDOC_VOLTA_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(VOLTA_FLAGS)

$(DIODE_JSON): $(VOLTA) $(VDOC_DIODE_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(DIODE_FLAGS)

$(TESLA_JSON): $(VOLTA) $(VDOC_TESLA_FILES)
	@echo "  VOLTA    $@"
	@$(VOLTA) $(TESLA_FLAGS)

$(METAL_JSON): $(VOLTA) $(VDOC_METAL_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(METAL_FLAGS)

$(PARSEC_JSON): $(VOLTA) $(VDOC_PARSEC_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(PARSEC_FLAGS)

$(CHARGE_JSON): $(VOLTA) $(VDOC_CHARGE_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(CHARGE_FLAGS)

$(BATTERY_JSON): $(VOLTA) $(VDOC_CHARGE_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(BATTERY_FLAGS)

docu: $(VDOC_JSON) $(DIODE)
	@echo "  DIODE    site"
	@rm -rf $(OUTPUT_DIR)
	@cp -r $(GURU_DIR)/_site $(OUTPUT_DIR)
	@$(DIODE) \
		-s $(GURU_DIR) -d $(OUTPUT_DIR) \
		--baseurl "http://volt.guru" \
		$(GURU_JSON)
	@$(DIODE) \
		-s $(AMP_DIR)/doc -d $(OUTPUT_DIR)/amp \
		--baseurl "http://volt.guru/amp" \
		$(AMP_JSON)
	@$(DIODE) \
		-s $(VOLTA_DIR)/rt/doc -d $(OUTPUT_DIR)/vrt \
		--baseurl "http://volt.guru/vrt" \
		$(VRT_JSON)
	@$(DIODE) \
		-s $(VOLTA_DIR)/doc -d $(OUTPUT_DIR)/volta \
		--baseurl "http://volt.guru/volta" \
		$(VOLTA_JSON)
	@$(DIODE) \
		-s $(DIODE_DIR)/doc -d $(OUTPUT_DIR)/diode \
		--baseurl "http://volt.guru/diode" \
		$(DIODE_JSON)
	@$(DIODE) \
		-s $(TESLA_DIR)/doc -d $(OUTPUT_DIR)/tesla \
		--baseurl "http://volt.guru/tesla" \
		$(TESLA_JSON)
	@$(DIODE) \
		-s $(METAL_DIR)/doc -d $(OUTPUT_DIR)/metal \
		--baseurl "http://volt.guru/metal" \
		$(METAL_JSON)
	@$(DIODE) \
		-s $(PARSEC_DIR)/doc -d $(OUTPUT_DIR)/parsec \
		--baseurl "http://volt.guru/parsec" \
		$(PARSEC_JSON)
	@$(DIODE) \
		-s $(CHARGE_DIR)/doc -d $(OUTPUT_DIR)/charge \
		--baseurl "http://volt.guru/charge" \
		$(CHARGE_JSON)
	@$(DIODE) \
		-s $(BATTERY_DIR)/doc -d $(OUTPUT_DIR)/battery \
		--baseurl "http://volt.guru/battery" \
		$(BATTERY_JSON)


.PHONY: all guru
