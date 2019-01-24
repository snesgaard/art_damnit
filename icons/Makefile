ims=$(wildcard image/*.png)
sprites=$(wildcard image/*.aseprite)
jsons=$(addprefix ./build/, $(notdir $(sprites:.aseprite=.json)))
atlas=./atlas.png
info=./index.lua
aseprite=~/.steam/steam/steamapps/common/Aseprite/aseprite
texatlas_script=/repos/artwork_n_stuff/texatlas.py

all: create_build_dirs $(atlas)

debug:
	@echo $(ims)

$(atlas): $(jsons) $(ims)
	@python $(texatlas_script) $^ -i $(info) -s $(atlas)

build/%.json: image/%.aseprite
	@$(aseprite) -b $< --sheet $(@:.json=.png) --data $@ \
	           --list-slices  --trim --inner-padding 1 --format json-array\
	           --list-tags

create_build_dirs:
	@mkdir -p build

clean:
	@rm -rf build
	@rm -f $(info)
	@rm -f $(atlas)
