CMAKE_MINIMUM_REQUIRED(VERSION 2.6)


FIND_PACKAGE(Qt REQUIRED)

QT4_WRAP_CPP(QtProject_HEADERS_MOC GuiCSV.h)
QT4_WRAP_UI(UI_FILES guicsv.ui)

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
#####################

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/GuiCSV.cxx.in ${CMAKE_CURRENT_BINARY_DIR}/GuiCSV.cxx)
############
SET(RTsources RodentThickness.cxx GuiCSV.h ${CMAKE_CURRENT_BINARY_DIR}/GuiCSV.cxx ScriptRunner.h ScriptRunner.cxx StatisticalpartRunner.h StatisticalpartRunner.cxx ${QtProject_HEADERS_MOC} ${UI_FILES}) # define the variable "sources" that contains the names of files
GENERATECLP(RTsources RodentThickness.xml)
ADD_EXECUTABLE(RodentThickness ${RTsources})  # add the files contained by "sources" to the project

TARGET_LINK_LIBRARIES(RodentThickness ${QT_LIBRARIES} ${ITK_LIBRARIES} ${BatchMake_LIBRARIES})




# Testing for 
#set(TestingSRCdirectory ${CMAKE_CURRENT_SOURCE_DIR}/Testing)
#set(TestingBINdirectory ${CMAKE_CURRENT_BINARY_DIR}/Testing)
#set(TestDataFolder ${TestingSRCdirectory}/Data)
#add_library(RodentThicknessLib STATIC ${RTsources}) # STATIC is also the default
#set_target_properties(RodentThicknessLib PROPERTIES COMPILE_FLAGS "-Dmain=ModuleEntryPoint")
#target_link_libraries(RodentThicknessLib ${QT_LIBRARIES} ${ITK_LIBRARIES} ${BatchMake_LIBRARIES})
#set_target_properties(RodentThicknessLib PROPERTIES LABELS RodentThickness)


#add_executable(testrun testrun.cpp)
#target_link_libraries(testrun  ${ITK_LIBRARIES} ${BatchMake_LIBRARIES})



# Create Tests
#include(CTest)
#add_subdirectory( ${TestingSRCdirectory} ) # contains a CMakeLists.txt
# include_directories( ${TestingSRCdirectory} ) # contains a CMakeLists.txt


SET (PythonScripts system.py run.py shapeworks.py)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/shapeworks.py ${Executablebin}/shapeworks.py)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/system.py ${Executablebin}/system.py)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/boxplot.py ${Executablebin}/boxplot.py)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/run.py ${Executablebin}/run.py)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/rodentThicknessStats.r ${Executablebin}/rodentThicknessStats.r)


