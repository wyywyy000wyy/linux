cmake_minimum_required(VERSION 3.1)
file(GLOB_RECURSE AllFile *)

file(RELATIVE_PATH RelativePath ${CMAKE_CURRENT_SOURCE_DIR}/.. ${CMAKE_CURRENT_SOURCE_DIR})

project(${RelativePath})

function(AllFilesLoad CurPath CurGroup)
file(GLOB Cur_Files ${CurPath}/*)
source_group(${CurGroup}  FILES ${Cur_Files})
file(GLOB files ${CurPath}/*)	
foreach(var ${files})
if(IS_DIRECTORY ${var})
file(RELATIVE_PATH RelativePath ${CurPath} ${var})
set(childGroup ${CurGroup}\\${RelativePath})
AllFilesLoad(${var} ${childGroup})
endif()
endforeach()	
endfunction(AllFilesLoad)

ADD_DEFINITIONS(-D__GXX_EXPERIMENTAL_CXX0X__)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_library(${PROJECT_NAME} ${AllFile})

AllFilesLoad(${CMAKE_CURRENT_SOURCE_DIR} ${PROJECT_NAME})


#target_link_libraries(Test libprotobuf)


