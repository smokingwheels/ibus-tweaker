project(
  'gnome-shell-extension-ibus-tweaker',
  license: 'GPL3+',
  version: '44.beta',
)

NAME = 'IBus Tweaker'
INFO = 'Tweaker of IBus for orientation, theme, font, input mode and clipboard history'
EID = meson.project_name().replace('gnome-shell-extension-', '')
UUID = EID + '@tuberry.github.com'
EGO = 'EGO=2820' / EID

GETTEXT = meson.project_name()
SCHEMAS = 'org.gnome.shell.extensions.' + EID
VERSION = (get_option('version') != 0) ? get_option('version') : run_command('cli/get-version.sh', check: true, env: [EGO]).stdout().strip()

fs = import('fs')
i18n = import('i18n')
gnome = import('gnome')

TARGET = get_option('target')
if(TARGET == 'system') 
  LOCALE_DIR = get_option('localedir')
  SCHEMA_DIR = get_option('datadir') / 'glib-2.0' / 'schemas'
  TARGET_DIR = get_option('datadir') / 'gnome-shell' / 'extensions' / UUID
else
  TARGET_ROOT = (TARGET == 'local') ? fs.expanduser('~/.local/share/gnome-shell/extensions/') : meson.project_build_root()
  TARGET_DIR = TARGET_ROOT / UUID
  LOCALE_DIR = TARGET_DIR / 'locale'
  SCHEMA_DIR = TARGET_DIR / 'schemas'
endif

if(TARGET == 'zip')
  ZIP_DIR = get_option('desktop') ? fs.expanduser('~/Desktop') : TARGET_ROOT 
  meson.add_install_script(
    find_program('7z'),
    'a',
    ZIP_DIR / '@0@_v@1@.zip'.format(GETTEXT, VERSION),
    TARGET_DIR / '*'
    )
endif

subdir('po')
subdir('res')
install_subdir('src', install_dir: TARGET_DIR, strip_directory: true)

