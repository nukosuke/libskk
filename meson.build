project(
  'libskk', ['c', 'vala'],
  version: '1.0.5',
  license: 'GPL-3.0-or-later',
  meson_version: '>= 0.64.0'
)

vapi_dir = meson.current_source_dir() / 'libskk'
add_project_arguments(['--vapidir', vapi_dir], language: 'vala')
add_project_arguments(['-DGETTEXT_PACKAGE="libskk"'], language: 'c')

libskk_deps = [
  dependency('glib-2.0'),
  dependency('gio-2.0'),
  dependency('gee-0.8'),
  dependency('json-glib-1.0'),
  dependency('libfep-glib', required: get_option('fep')),
  # libs without pkg-config
  meson.get_compiler('vala').find_library('posix'),
  # C packages
  meson.get_compiler('c').find_library('xkbcommon'),
  meson.get_compiler('vala').find_library('xkbcommon', dirs: vapi_dir),
  # local packages
  meson.get_compiler('vala').find_library('config', dirs: vapi_dir)
]

libskk_prefix = get_option('prefix')
libskk_pkgdatadir = join_paths(libskk_prefix, get_option('datadir'))

config_h = configuration_data()
config_h.set_quoted('PACKAGE_NAME', meson.project_name())
config_h.set_quoted('PACKAGE_VERSION', meson.project_version())
config_h.set_quoted('PKGDATADIR', libskk_pkgdatadir)
config_h.set_quoted('DATADIR', join_paths(libskk_prefix, get_option('datadir')))
config_h.set_quoted('LOCALEDIR', join_paths(libskk_prefix, get_option('localedir')))
configure_file(output: 'config.h', configuration: config_h)

subdir('libskk')
subdir('tools')
subdir('po')
subdir('tests')
install_subdir('rules', install_dir: libskk_pkgdatadir)
