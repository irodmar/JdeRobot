SET (ARDRONE_INTERFACES_DIR ${CMAKE_CURRENT_SOURCE_DIR}/interfaces)

PKG_CHECK_MODULES(libxmlpp REQUIRED libxml++-2.6)
include_directories(${libxmlpp_INCLUDE_DIRS})
link_directories(${libxmlpp_LIBRARY_DIRS})

#find_package(OpenCV REQUIRED)

include_directories(
    ${ARDRONE_INTERFACES_DIR}
	${GAZEBO_INCLUDE_DIRS}
    ${INTERFACES_CPP_DIR}
    ${LIBS_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}
)

link_directories(${GAZEBO_LIBRARY_DIRS}
    ${INTERFACES_CPP_DIR}/jderobot
	${LIBS_DIR}/visionlib/colorspaces
    )

add_library(quadrotorplugin SHARED quadrotorplugin.cc
                quadrotor_remote_config.cc
                quadrotor_parser.cpp
                quadrotor_config.cpp
                interfaces/navdatai.cpp
                ${ARDRONE_INTERFACES_DIR}/remoteConfig.cpp
                ${ARDRONE_INTERFACES_DIR}/navdata.cpp
                ${ARDRONE_INTERFACES_DIR}/cmdvel.cpp
                ${ARDRONE_INTERFACES_DIR}/ardroneextra.cpp)
target_link_libraries(quadrotorplugin 
	${OpenCV_LIBS}
	Ice
	IceUtil
	${libxmlpp_LIBRARIES}
    JderobotInterfaces
	${GAZEBO_libraries} 
)

add_library(imuplugin SHARED imuplugin.cc)
target_link_libraries(imuplugin 
	Ice
	IceUtil
	JderobotInterfaces
	${GAZEBO_libraries} 
	${ZeroCIce_LIBRARIES}
    ${PROTOBUF_LIBRARIES}
)

add_library(poseplugin SHARED poseplugin.cc)
target_link_libraries(poseplugin 
	${GAZEBO_libraries} 
)

add_library(togglecamplugin SHARED togglecamplugin.cc)
target_link_libraries(togglecamplugin
    ${OpenCV_LIBS}
	CameraPlugin
    colorspacesmm
	${GAZEBO_libraries}
    ${PROTOBUF_LIBRARIES}
)
