tools_incdir = include_directories('..', '../libskk')

executable('skk', 'skk.vala',
           dependencies: libskk_deps,
           link_with: libskk,
           include_directories: tools_incdir)

if get_option('fep')
  executable('skkfep-client', 'fep.vala',
             dependencies: libskk_deps,
             link_with: libskk,
             include_directories: tools_incdir)
endif
