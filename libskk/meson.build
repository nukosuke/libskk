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

libskk = static_library(
  'skk',
  sources: libskk_sources,
  dependencies: libskk_deps,
  vala_header: 'libskk.h',
  vala_vapi: 'libskk-1.0.vapi',
  include_directories: include_directories('..'), # for config.h
  install: true,
  install_dir: get_option('libdir') / 'libskk-1.0'
)

pkgconfig.generate(
  libskk,
  name: 'libskk',
  description: 'a library to deal with Japanese kana-to-kanji conversion method'
)
