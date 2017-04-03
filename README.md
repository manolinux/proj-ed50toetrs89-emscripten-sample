Quick and not very detailed instructions
========================================

* Follow the instructions to install Emscripten, install Proj from http://proj4.org/ invoking
   emconfigure, emmake

* Link and generate javascript: 
 - Including filesystem for Proj data
 - Exporting required functions (pj_transform, pj_init_plus)

emcc .libs/libproj.so.12.0.0 cs2cs.o -o <HTML_DIR>/cs2cs.js --preload-file usr -s EXPORTED_FUNCTIONS="['_pj_transform','_pj_init_plus']"

* Generate fake filesystem emulating /usr/local/share/proj(*)

 - mkdir usr/local/share/proj under a temp working dir
 - cp /usr/local/share/proj/epsg to TMP_DIR/usr/local/share/proj
 - cp /usr/local/share/proj/proj_def.data TMP_DIR/usr/local/share/proj
 - cp nadgrid (PENR2009.gsb) to TMP_DIR/usr/local/share/proj
 - modify required epsg codes in temp dir, epsg file to deal with nadgrid
   <23030> +proj=utm +zone=30 +ellps=intl +nadgrids=PENR2009.gsb +units=m +no_defs  <>

This packages usr under working dir:
 cd TMP_DIR
 python <EMSCRIPTEN_DIR>/master/tools/file_packager.py <HTML_DIR>/cs2cs.data --preload usr/share/proj
(js output can be discarded, creates <HTML_DIR> cs2cs.data, which in fact it is called in previously generated cs2cs.js)

(*) /usr/local/share/proj might be /usr/share/proj, depending on configure step of proj


...Detailed instructions as far as I can clear my mind and remember what I did exactly, stay tuned :D ...

Regards,
Manuel.


