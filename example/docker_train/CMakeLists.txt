cmake_minimum_required(VERSION 3.9)
add_executable(train main.cpp)
add_definitions(-std=c++1z)
install(TARGETS train RUNTIME DESTINATION bin)
