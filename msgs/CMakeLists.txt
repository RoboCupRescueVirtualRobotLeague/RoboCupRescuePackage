find_package(Protobuf REQUIRED)

set(PROTOBUF_IMPORT_DIRS)
foreach(ITR ${GAZEBO_INCLUDE_DIRS})
  if(ITR MATCHES ".*gazebo-[0-9.]+$")
    set(PROTOBUF_IMPORT_DIRS "${ITR}/gazebo/msgs/proto")
  endif()
endforeach()

set (msgs
  flipper_control.proto encoder.proto
)
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS ${msgs})
add_library(flipper_control_msgs SHARED ${PROTO_SRCS})
target_link_libraries(flipper_control_msgs ${PROTOBUF_LIBRARY})
add_library(encoder_msgs SHARED ${PROTO_SRCS})
target_link_libraries(encoder_msgs ${PROTOBUF_LIBRARY})

