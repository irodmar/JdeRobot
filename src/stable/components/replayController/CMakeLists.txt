 cmake_minimum_required(VERSION 2.8)


SET( SOURCE_FILES replayController.cpp replayControllerGui.cpp)


add_definitions(-DGLADE_DIR="${gladedir}")

set( CMAKE_CXX_FLAGS "-Wno-deprecated" ) # Opciones para el compilador

include_directories(
    ${INTERFACES_CPP_DIR}
    ${LIBS_DIR}/
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${gtkmm_INCLUDE_DIRS}
    ${libglademm_INCLUDE_DIRS}
    ${gtkglextmm_INCLUDE_DIRS}
)

add_executable (replayController ${SOURCE_FILES})


TARGET_LINK_LIBRARIES(replayController
    ${CMAKE_THREAD_LIBS_INIT} 
    ${GLUT_LIBRARIES}
    ${OpenCV_LIBRARIES}
    ${OpenCVGUI_LIBRARIES}
    ${gtkmm_LIBRARIES}
    ${libglademm_LIBRARIES}
    ${gtkglextmm_LIBRARIES}
    colorspacesmm
    JderobotInterfaces
    jderobotutil
    progeo
    pioneer
    ${ZeroCIce_LIBRARIES}
)
