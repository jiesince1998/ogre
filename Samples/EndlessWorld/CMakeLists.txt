# Configure EndlessWorld demo build

set(HEADER_FILES
	include/EndlessWorld.h
	include/PerlinNoiseTerrainGenerator.h)
set(SOURCE_FILES
	src/EndlessWorld.cpp
	src/PerlinNoiseTerrainGenerator.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
ogre_add_component_include_dir(Terrain)
ogre_add_component_include_dir(Paging)

ogre_add_library_to_folder(Samples Sample_EndlessWorld ${OGRE_LIB_TYPE} ${SOURCE_FILES} ${HEADER_FILES})

target_link_libraries(Sample_EndlessWorld ${OGRE_LIBRARIES} ${SDL2_LIBRARY} ${OGRE_Terrain_LIBRARIES} ${OGRE_Paging_LIBRARIES})
ogre_config_sample_lib(Sample_EndlessWorld)

if (APPLE AND NOT APPLE_IOS)
	# Set the INSTALL_PATH so that Samples can be installed in the application package
	set_target_properties(Sample_EndlessWorld
		PROPERTIES BUILD_WITH_INSTALL_RPATH 1
		INSTALL_NAME_DIR "@executable_path/../Plugins"
	)
endif()

