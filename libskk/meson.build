pkgconfig = import('pkgconfig')

libskk_sources = files(
  'rom-kana.vala',
  'encoding.vala',
  'dict.vala',
  'file-dict.vala',
  'cdb-dict.vala',
  'user-dict.vala',
  'skkserv.vala',
  'key-event.vala',
  'key-event-filter.vala',
  'keymap.vala',
  'rule.vala',
  'map-file.vala',
  'state.vala',
  'context.vala',
  'candidate.vala',
  'candidate-list.vala',
  'nicola.vala',
  'expr.vala',
  'util.vala',
  'keysyms.vala'
)

libskk = library(
  'skk',
  version: '1.0.5',
  soversion: '1',
  sources: libskk_sources,
  dependencies: libskk_deps,
  vala_header: 'libskk.h',
  vala_vapi: 'skk-1.0.vapi',
  vala_gir: 'Skk-1.0.gir',
  include_directories: include_directories('..'), # for config.h
  install: true,
  install_dir: [true, true, true, true]
)

gir_compiler = find_program('g-ir-compiler')
custom_target(
  'libskk typelib',
  command: [gir_compiler, '--output', '@OUTPUT@', meson.current_build_dir() / 'Skk-1.0.gir'],
  output: 'Skk-1.0.typelib',
  depends: libskk,
  install: true,
  install_dir: get_option('libdir') / 'girepository-1.0'
)

pkgconfig.generate(
  libskk,
  name: 'libskk',
  description: 'a library to deal with Japanese kana-to-kanji conversion method'
)
