
BASE_URL ?= http://volt.guru
RT_DIR ?= $(VOLTA_DIR)/rt
AMP_DIR ?= amp
GURU_DIR ?= guru
WATT_DIR ?= watt
DEQP_DIR ?= deqp
VOLTA_DIR ?= volta
DIODE_DIR ?= diode
TESLA_DIR ?= tesla
METAL_DIR ?= metal
CHARGE_DIR ?= charge
BATTERY_DIR ?= battery

JSON_DIR ?= $(GURU_DIR)/_tmp
OUTPUT_DIR ?= $(GURU_DIR)/_output

DIODE ?= $(shell which diode)
VOLTA ?= $(shell which volt)

BASE_FLAGS=--no-backend -jo $@ \
	--lib-I $(VOLTA_DIR)/rt/src \
	--lib-I $(WATT_DIR)/src \
	--lib-I $(WATT_DIR)/http/src \
	--lib-I $(WATT_DIR)/json/src \
	--lib-I $(WATT_DIR)/toml/src \
	--lib-I $(WATT_DIR)/markdown/src

VDOC_RT_FILES=$(shell find $(RT_DIR)/src -type f -name "*.volt")
VDOC_AMP_FILES=$(shell find $(AMP_DIR)/src -type f -name "*.volt")
VDOC_WATT_FILES=$(shell find \
	$(WATT_DIR)/src \
	$(WATT_DIR)/http/src \
	$(WATT_DIR)/json/src \
	$(WATT_DIR)/toml/src \
	$(WATT_DIR)/markdown/src \
	-type f -name "*.volt")
VDOC_DEQP_FILES=$(shell find \
	$(DEQP_DIR)/src \
	-type f -name "*.volt")
VDOC_VOLTA_FILES=$(shell find \
	$(VOLTA_DIR)/src \
	$(VOLTA_DIR)/lib/src \
	-type f -name "*.d")
VDOC_DIODE_FILES=$(shell find \
	$(DIODE_DIR)/src \
	$(DIODE_DIR)/lib/src \
	-type f -name "*.volt")
VDOC_TESLA_FILES=$(shell find $(TESLA_DIR)/src -type f -name "*.volt")
VDOC_METAL_FILES=$(shell find $(METAL_DIR)/src -type f -name "*.volt")
VDOC_CHARGE_FILES=$(shell find \
	$(CHARGE_DIR)/src \
	$(CHARGE_DIR)/lib/src \
	-type f -name "*.volt")
VDOC_BATTERY_FILES=$(shell find \
	$(BATTERY_DIR)/src \
	$(BATTERY_DIR)/lib/src \
	-type f -name "*.volt")

RT_FLAGS = $(BASE_FLAGS) $(VDOC_RT_FILES)
AMP_FLAGS = $(BASE_FLAGS) $(VDOC_AMP_FILES)
WATT_FLAGS = $(BASE_FLAGS) $(VDOC_WATT_FILES)
DEQP_FLAGS = $(BASE_FLAGS) $(VDOC_DEQP_FILES)
VOLTA_FLAGS = $(BASE_FLAGS) $(VOLTA_DIR)/src/main.d --internal-d --src-I $(VOLTA_DIR)/src --src-I $(VOLTA_DIR)/lib/src
DIODE_FLAGS = $(BASE_FLAGS) $(VDOC_DIODE_FILES) -J $(DIODE_DIR)/res
TESLA_FLAGS = $(BASE_FLAGS) $(VDOC_TESLA_FILES)
METAL_FLAGS = $(BASE_FLAGS) $(VDOC_METAL_FILES)
CHARGE_FLAGS = $(BASE_FLAGS) $(VDOC_CHARGE_FILES) -J $(CHARGE_DIR)/res
BATTERY_FLAGS = $(BASE_FLAGS) $(VDOC_BATTERY_FILES)


RT_JSON = $(JSON_DIR)/rt.json
AMP_JSON = $(JSON_DIR)/amp.json
WATT_JSON = $(JSON_DIR)/watt.json
DEQP_JSON = $(JSON_DIR)/deqp.json
VOLTA_JSON = $(JSON_DIR)/volta.json
DIODE_JSON = $(JSON_DIR)/diode.json
TESLA_JSON = $(JSON_DIR)/tesla.json
METAL_JSON = $(JSON_DIR)/metal.json
CHARGE_JSON = $(JSON_DIR)/charge.json
BATTERY_JSON = $(JSON_DIR)/battery.json

VDOC_JSON = \
	$(RT_JSON) \
	$(AMP_JSON) \
	$(WATT_JSON) \
	$(DEQP_JSON) \
	$(VOLTA_JSON) \
	$(DIODE_JSON) \
	$(TESLA_JSON) \
	$(METAL_JSON) \
	$(CHARGE_JSON) \
	$(BATTERY_JSON)


#
# Rules start here.
#

all: docu

$(RT_JSON): $(VOLTA) $(VDOC_RT_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(RT_FLAGS)

$(AMP_JSON): $(VOLTA) $(VDOC_AMP_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(AMP_FLAGS)

$(WATT_JSON): $(VOLTA) $(VDOC_WATT_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(WATT_FLAGS)

$(DEQP_JSON): $(VOLTA) $(VDOC_DEQP_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(DEQP_FLAGS)

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
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(TESLA_FLAGS)

$(METAL_JSON): $(VOLTA) $(VDOC_METAL_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(METAL_FLAGS)

$(CHARGE_JSON): $(VOLTA) $(VDOC_CHARGE_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(CHARGE_FLAGS)

$(BATTERY_JSON): $(VOLTA) $(VDOC_BATTERY_FILES)
	@echo "  VOLTA    $@"
	@mkdir -p "$(dir $@)"
	@$(VOLTA) $(BATTERY_FLAGS)

first: $(WATT_JSON) $(DIODE)
	@rm -rf $(OUTPUT_DIR)
	@cp -r $(GURU_DIR)/_site $(OUTPUT_DIR)
	@echo "  DIODE    guru"
	@$(DIODE) \
		-s $(GURU_DIR) -d $(OUTPUT_DIR) \
		--baseurl "$(BASE_URL)" \
		$(WATT_JSON)

docu-rt: first $(RT_JSON) $(DIODE)
	@echo "  DIODE    rt"
	@$(DIODE) \
		-s $(RT_DIR)/doc -d $(OUTPUT_DIR)/rt \
		--baseurl "$(BASE_URL)/rt" \
		$(RT_JSON)

docu-amp: first $(AMP_JSON) $(DIODE)
	@echo "  DIODE    amp"
	@$(DIODE) \
		-s $(AMP_DIR)/doc -d $(OUTPUT_DIR)/amp \
		--baseurl "$(BASE_URL)/amp" \
		$(AMP_JSON)

docu-watt: first $(WATT_JSON) $(DIODE)
	@echo "  DIODE    watt"
	@$(DIODE) \
		-s $(WATT_DIR)/doc -d $(OUTPUT_DIR)/watt \
		--baseurl "$(BASE_URL)/watt" \
		$(WATT_JSON)

docu-deqp: first $(DEQP_JSON) $(DIODE)
	@echo "  DIODE    deqp"
	@$(DIODE) \
		-s $(DEQP_DIR)/doc -d $(OUTPUT_DIR)/deqp \
		--baseurl "$(BASE_URL)/deqp" \
		$(DEQP_JSON)

docu-volta: first $(VOLTA_JSON) $(DIODE)
	@echo "  DIODE    volta"
	@$(DIODE) \
		-s $(VOLTA_DIR)/doc -d $(OUTPUT_DIR)/volta \
		--baseurl "$(BASE_URL)/volta" \
		$(VOLTA_JSON)

docu-diode: first $(DIODE_JSON) $(DIODE)
	@echo "  DIODE    diode"
	@$(DIODE) \
		-s $(DIODE_DIR)/doc -d $(OUTPUT_DIR)/diode \
		--baseurl "$(BASE_URL)/diode" \
		$(DIODE_JSON)

docu-tesla: first $(TESLA_JSON) $(DIODE)
	@echo "  DIODE    tesla"
	@$(DIODE) \
		-s $(TESLA_DIR)/doc -d $(OUTPUT_DIR)/tesla \
		--baseurl "$(BASE_URL)/tesla" \
		$(TESLA_JSON)

docu-metal: first $(METAL_JSON) $(DIODE)
	@echo "  DIODE    metal"
	@$(DIODE) \
		-s $(METAL_DIR)/doc -d $(OUTPUT_DIR)/metal \
		--baseurl "$(BASE_URL)/metal" \
		$(METAL_JSON)

docu-charge: first $(CHARGE_JSON) $(DIODE)
	@echo "  DIODE    charge"
	@$(DIODE) \
		-s $(CHARGE_DIR)/doc -d $(OUTPUT_DIR)/charge \
		--baseurl "$(BASE_URL)/charge" \
		$(CHARGE_JSON)

docu-battery: first $(BATTERY_JSON) $(DIODE)
	@echo "  DIODE    battery"
	@$(DIODE) \
		-s $(BATTERY_DIR)/doc -d $(OUTPUT_DIR)/battery \
		--baseurl "$(BASE_URL)/battery" \
		$(BATTERY_JSON)

docu: docu-rt docu-amp docu-watt docu-deqp docu-volta docu-diode docu-tesla docu-metal docu-charge docu-battery

.PHONY: all guru first
