# --------------------------------------------------------
#  Copyright (C) 2004-2017 by EMGU Corporation. All rights reserved.
# --------------------------------------------------------

IF(HAVE_WINDESKTOP_X86 OR HAVE_WINDESKTOP_X64)  

#MESSAGE(STATUS "MSBUILD_EXECUTABLE_40: ${MSBUILD_EXECUTABLE_40}")
SET(MSBUILD_EXECUTABLE ${MSBUILD_EXECUTABLE_40})

IF(NOT ("${MSBUILD_EXECUTABLE}" STREQUAL ""))
#MESSAGE(STATUS "MSBUILD_EXECUTABLE: ${MSBUILD_EXECUTABLE}")
PROJECT(Emgu.TF.Document.Html)
ADD_CUSTOM_TARGET(
   ${PROJECT_NAME}
   COMMAND ${MSBUILD_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/Emgu.TF.html.shfbproj
   SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/Emgu.TF.html.shfbproj
)
ADD_DEPENDENCIES(${PROJECT_NAME} Emgu.TF.World)

PROJECT(Emgu.TF.Documentation.chm)
ADD_CUSTOM_TARGET(
   ${PROJECT_NAME} ALL
   COMMAND ${MSBUILD_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/Emgu.TF.html.shfbproj /property:OutputPath=. /property:HelpFileFormat=HtmlHelp1
   SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/Emgu.TF.html.shfbproj
)
ADD_DEPENDENCIES(${PROJECT_NAME} Emgu.TF.World)

INSTALL(
  FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/Emgu.TF.Documentation.chm"
  DESTINATION ./
  COMPONENT emgutf_document
  )

ELSE()
MESSAGE(STATUS "MSBUILD_EXECUTABLE: NOT FOUND")
ENDIF()

ENDIF()
