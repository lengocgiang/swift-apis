add_library(CTensorFlow INTERFACE)
if(NOT USE_BUNDLED_CTENSORFLOW)
  target_include_directories(CTensorFlow INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR})
endif()
target_link_libraries(CTensorFlow INTERFACE
  tensorflow)

install(FILES module.modulemap CTensorFlow.h
  DESTINATION lib/swift/tensorflow)
install(DIRECTORY $<TARGET_PROPERTY:tensorflow,INTERFACE_INCLUDE_DIRECTORIES>/tensorflow/c
  DESTINATION lib/swift/tensorflow
  FILES_MATCHING
    PATTERN c_api.h
    PATTERN c_api_experimental.h
    PATTERN tf_attrtype.h
    PATTERN tf_datatype.h
    PATTERN tf_status.h
    PATTERN tf_tensor.h
    PATTERN eager/c_api.h)
