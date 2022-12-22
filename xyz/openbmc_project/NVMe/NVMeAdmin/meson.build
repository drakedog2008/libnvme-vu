domain = 'xyz.openbmc_project.NVMe.NVMeAdmin'
if_yaml_file = files('../NVMeAdmin.interface.yaml')

nvme_if_server_cpp = custom_target(
  'server.cpp',
  input: if_yaml_file,
  output: 'server.cpp',
  capture: true,
  command: [sdbusplusplus_prog, '-r', if_root, 'interface', 'server-cpp', domain])

nvme_if_server_hpp = custom_target(
  'server.hpp',
  input: if_yaml_file,
  output: 'server.hpp',
  capture: true,
  command: [sdbusplusplus_prog, '-r', if_root, 'interface', 'server-header', domain],
  install: true,
  install_dir: get_option('includedir') / 'xyz/openbmc_project/NVMe/NVMeAdmin'
)

nvme_if_client_hpp = custom_target(
  'client.hpp',
  input: if_yaml_file,
  output: 'client.hpp',
  capture: true,
  command: [sdbusplusplus_prog, '-r', if_root, 'interface', 'client-header', domain],
  install: true,
  install_dir: get_option('includedir') / 'xyz/openbmc_project/NVMe/'
)

libnvme_intf = library(
  'nvme-interface', 
  [
    nvme_if_server_cpp,
    nvme_if_server_hpp
  ], 
  include_directories: [inc],
  dependencies: [
    sdbusplus,
    pdi
  ], 
  version: meson.project_version(),
  install: true,
)

nvme_intf_dep = declare_dependency(
  include_directories: [inc], 
  link_with: libnvme_intf
)
