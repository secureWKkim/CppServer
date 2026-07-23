cmake_minimum_required(VERSION 3.20)
project(CppServer LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# 모든 실행 파일/라이브러리 산출물을 한 곳에 모아 관리 (구성별 하위 폴더)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# 하위 폴더 중 CMakeLists.txt 를 가진 폴더를 자동으로 인식해 빌드 대상에 추가한다.
# 새 폴더(예: DummyClient)를 만들고 그 안에 CMakeLists.txt 만 두면 자동으로 잡힌다.
# ServerCore 는 다른 모듈들이 링크해야 하므로 먼저 등록되도록 우선 처리.
set(_PRIORITY_SUBDIRS ServerCore)

foreach(_dir IN LISTS _PRIORITY_SUBDIRS)
    if(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${_dir}/CMakeLists.txt)
        add_subdirectory(${_dir})
    endif()
endforeach()

file(GLOB _children RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/*)
foreach(_child IN LISTS _children)
    set(_path ${CMAKE_CURRENT_SOURCE_DIR}/${_child})
    if(IS_DIRECTORY ${_path} AND EXISTS ${_path}/CMakeLists.txt)
        if(NOT _child IN_LIST _PRIORITY_SUBDIRS)
            add_subdirectory(${_child})
        endif()
    endif()
endforeach()