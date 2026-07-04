cmake_minimum_required(VERSION 4.2)
project(CppServer)

set(CMAKE_CXX_STANDARD 20)

add_executable(CppServer main.cpp
        ServerCore/Utils/pch.cpp
        ServerCore/Utils/pch.h
        ServerCore/Utils/CorePch.cpp
        ServerCore/Utils/CorePch.h
        ServerCore/Utils/Types.h)
