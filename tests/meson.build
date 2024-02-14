tests = {
  'rom-kana': 'rom-kana.c',
  'file-dict': 'file-dict.c',
  'cdb-dict': 'cdb-dict.c',
  'skkserv': 'skkserv.c',
  'user-dict': files('user-dict.c', 'common.c'),
  'rule': files('rule.c', 'common.c'),
  'context': files('context.c', 'common.c'),
  'basic': files('basic.c', 'common.c')
}

tests_incdir = include_directories('..')
tests_env = environment({
  'LIBSKK_DATA_PATH': ':'.join([
    meson.global_source_root(),
    meson.current_source_dir()
  ])
})

add_test_setup('default', env: tests_env, is_default: true)

valgrind = find_program('valgrind', required: false)
if valgrind.found()
  add_test_setup(
    'valgrind',
    env: tests_env,
    exe_wrapper: [
      valgrind,
      '--show-reachable=no',
      '--gen-suppressions=all',
      '--num-callers=20',
      '--error-exitcode=0',
      '--log-file=valgrind.log.%p'
    ]
  )
endif

tests_file_dict = meson.current_source_dir() / 'file-dict.dat'
tests_cdb_dict = meson.current_source_dir() / 'cdb-dict.dat'

foreach t_name, t_sources: tests
  t_exe = executable(t_name, t_sources,
                     dependencies: libskk_deps,
                     link_with: libskk,
                     include_directories: tests_incdir,
                     c_args: [
                       '-DLIBSKK_FILE_DICT="@0@"'.format(tests_file_dict),
                       '-DLIBSKK_CDB_DICT="@0@"'.format(tests_cdb_dict)
                     ])
  # Don't set is_parallel=true to avoid file modification conflict
  test(t_name, t_exe, is_parallel: false)
endforeach
