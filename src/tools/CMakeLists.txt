include_directories(${VISIONWORKBENCH_INCLUDE_DIRS})
include_directories(${Boost_INCLUDE_DIRS})
include_directories(${PROTOBUF_INCLUDE_DIRS})

# Reusable Vision Workbench Patterns
set(VISIONWORKBENCH_BASE_LIBRARIES
  ${VISIONWORKBENCH_CORE_LIBRARY}
  ${VISIONWORKBENCH_MATH_LIBRARY}
  ${VISIONWORKBENCH_IMAGE_LIBRARY}
  ${VISIONWORKBENCH_FILEIO_LIBRARY}
  )

# Executables
set(PHOTK_USED_LIBS PhotometryTK ${VISIONWORKBENCH_CARTOGRAPHY_LIBRARY} ${Boost_LIBRARIES} ${StereoPipeline_LIBRARIES})
add_photk_tool(reconstruct reconstruct.cc)
add_photk_tool(dem_mosaic dem_mosaic.cc)

# The SfS tool. It depends on ISIS.
if (ENABLE_SFS)
   add_isis_tool(sfs sfs.cc)
endif()

# Scripts
install( FILES reconstruct.sh
PERMISSIONS GROUP_EXECUTE OWNER_EXECUTE OWNER_READ GROUP_READ
DESTINATION bin )
