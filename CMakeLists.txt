#######################################################################################
## ASIO CMake Project File
##

# Version requirement and project info
cmake_minimum_required(VERSION 3.1)
project(asio)

if (NOT TARGET asio)
	# Define asio as header only interface
	add_library(asio INTERFACE)

	# Add header files als interface dependencies
	target_include_directories(asio INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/asio/include)

	# Link to libwinsock on windows
	if(WIN32)
		target_link_libraries(asio INTERFACE wsock32 ws2_32)
	endif()

	# Use ASIO as standalone library
	target_compile_definitions(asio INTERFACE ASIO_STANDALONE=1)

	set(ASIO_LIBRARIES asio CACHE INTERNAL "")
endif()
