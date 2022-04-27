cmake_minimum_required(VERSION 3.10.2)

project(pybind11_protobuf)

set(CMAKE_CXX_STANDARD 14)

set(ABSL_PROPAGATE_CXX_STD ON)

find_package(Python3 REQUIRED COMPONENTS Development Interpreter)

add_subdirectory(third_party/abseil-cpp)
add_subdirectory(third_party/protobuf)
add_subdirectory(third_party/pybind11)

add_library(pybind11_protobuf
  pybind11_protobuf/enum_type_caster.h
  pybind11_protobuf/native_proto_caster.cc
  pybind11_protobuf/proto.cc
  pybind11_protobuf/proto_cast_util.cc
  pybind11_protobuf/proto_caster_impl.h
  pybind11_protobuf/proto_utils.cc
  pybind11_protobuf/proto_utils.h
  pybind11_protobuf/wrapped_proto_caster.h
  )

target_link_libraries(pybind11_protobuf PUBLIC
  absl::flat_hash_map
  absl::flat_hash_set
  absl::hash
  absl::strings
  absl::optional
  protobuf::libprotobuf
  pybind11::pybind11
  )

target_include_directories(pybind11_protobuf PUBLIC
  ${PROJECT_SOURCE_DIR}
  ${PROJECT_SOURCE_DIR}/third_party/protobuf
  )
