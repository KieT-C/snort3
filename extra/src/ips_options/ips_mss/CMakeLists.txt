cmake_minimum_required ( VERSION 2.8.11 )
project ( ips_mss CXX )

if ( APPLE )
    set ( CMAKE_MACOSX_RPATH OFF )
endif ( APPLE )

include ( FindPkgConfig )
pkg_search_module ( SNORT3 REQUIRED snort>=3 )

add_library (
    ips_mss MODULE
    ips_mss.cc
)

if ( APPLE )
    set_target_properties (
        ips_mss
        PROPERTIES
            LINK_FLAGS "-undefined dynamic_lookup"
    )
endif ( APPLE )

set_target_properties (
    ips_mss
    PROPERTIES
        PREFIX ""
)

set ( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11" )

target_include_directories (
    ips_mss PUBLIC
    ${SNORT3_INCLUDE_DIRS}
)

install (
    TARGETS ips_mss
    LIBRARY
        DESTINATION "lib/${CMAKE_PROJECT_NAME}/ips_options"
)
