pkgdatadir = join_paths(get_option('prefix'), get_option('datadir'), meson.project_name())
moduledir = join_paths(pkgdatadir, 'web_scraper')
gnome = import('gnome')

gnome.compile_resources('web-scraper',
  'web_scraper.gresource.xml',
  gresource_bundle: true,
  install: true,
  install_dir: pkgdatadir,
)

desktop_utils = find_program('desktop-file-validate', required: false)
if desktop_utils.found()
  test('Validate desktop file', desktop_utils,
    args: [desktop_file]
  )
endif

python = import('python')

conf = configuration_data()
conf.set('PYTHON', python.find_installation('python3').path())
conf.set('VERSION', meson.project_version())
conf.set('localedir', join_paths(get_option('prefix'), get_option('localedir')))
conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 'web-scraper.in',
  output: 'web-scraper',
  configuration: conf,
  install: true,
  install_dir: get_option('bindir')
)

web_scraper_sources = [
  '__init__.py',
  'main.py',
  'window.py',
]

install_data(web_scraper_sources, install_dir: moduledir)

