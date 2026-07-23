# ServerCore: 다른 모듈들이 링크해서 사용하는 정적 라이브러리
# 이 폴더 안의 모든 .cpp/.h 를 자동으로 수집한다.
file(GLOB_RECURSE SERVERCORE_SOURCES
        CONFIGURE_DEPENDS
        ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/*.h
)

add_library(ServerCore STATIC ${SERVERCORE_SOURCES})

# 사용자(링크하는 쪽)가 "Utils/pch.h" 처럼 include 할 수 있도록 ServerCore 폴더를 공개한다.
target_include_directories(ServerCore PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
)

# 필요 시 여기서 컴파일 옵션/정의 추가 (예: WIN32 매크로 등)
if(WIN32)
    target_compile_definitions(ServerCore PUBLIC WIN32_LEAN_AND_MEAN)
endif()