libnixf_deps = [ ]

libnixf_inc = include_directories('include')

libnixf = library(
    'nixf',
    'src/Basic/Diagnostic.cpp',
    'src/Parse/Lexer.cpp',
    'src/Parse/Parser.cpp',
    include_directories: libnixf_inc,
    dependencies: libnixf_deps,
    install: true,
    cpp_args: [ '-Werror=implicit-fallthrough' ]
)

pkgconfig.generate(
    name: 'libnixf',
    version: 'nightly',
    description: 'libnixf',
    libraries: libnixf
)

nixf = declare_dependency(
    include_directories: libnixf_inc,
    link_with: libnixf,
    dependencies: libnixf_deps
)

test('unit/libnixf/Basic',
    executable('unit-libnixf-basic',
        'test/Basic/Diagnostic.cpp',
        dependencies: [ nixf, gtest_main ],
    )
)

test('unit/libnixf/Parse',
    executable('unit-libnixf-parse',
        'test/Parse/Lexer.cpp',
        'test/Parse/Parser.cpp',
        dependencies: [ nixf, gtest_main ],
        include_directories: [ 'src/Parse' ] # Private headers
    )
)


install_subdir('include/nixf', install_dir: 'include')
