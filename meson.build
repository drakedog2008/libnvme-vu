project(
    'libnvme-vu',
    'cpp',
    default_options: [
        'warning_level=3',
        'werror=true',
        'cpp_std=c++20'
    ],
    version: '0.1',
    meson_version: '>=0.57.0',
)

sdbusplus = dependency('sdbusplus', required : false, include_type: 'system')
if not sdbusplus.found()
  sdbusplus_proj = subproject('sdbusplus', required: true)
  sdbusplus = sdbusplus_proj.get_variable('sdbusplus_dep')
  sdbusplus = sdbusplus.as_system('system')
  sdbusplusplus_prog = sdbusplus_proj.get_variable('sdbusplusplus_prog')
else
  sdbusplusplus_prog = find_program('sdbus++', native: true)
endif

pdi = dependency(
  'phosphor-dbus-interfaces',
  fallback: ['phosphor-dbus-interfaces', 'phosphor_dbus_interfaces_dep']
)

inc = include_directories('.')
if_root = meson.current_source_dir()

subdir('xyz/openbmc_project/NVMe/NVMeAdmin')
