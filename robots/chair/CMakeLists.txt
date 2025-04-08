cmake_minimum_required(VERSION 3.10)

project(chair VERSION 1.0.0)

if(NOT TARGET mc_mujoco)
  find_package(mc_mujoco REQUIRED)
endif()

option(SRC_MODE "Use files in the repository instead of installed files" OFF)

set(CHAIR_XML_MODEL_PATH "xml/chair.xml")

if(SRC_MODE)
  set(CHAIR_XML_MODEL_PATH "${CMAKE_CURRENT_SOURCE_DIR}/${CHAIR_XML_MODEL_PATH}")
else()
  set(CHAIR_XML_MODEL_PATH "${MC_MUJOCO_SHARE_DESTINATION}/CHAIR/${CHAIR_XML_MODEL_PATH}")
endif()

configure_file(mc_mujoco/chair.in.yaml "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/chair.yaml")
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/chair.yaml" DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}")

install(DIRECTORY meshes DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/CHAIR" FILES_MATCHING PATTERN "*.stl")
install(DIRECTORY xml DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/CHAIR" FILES_MATCHING PATTERN "*.xml")
