# GameServer: 실행 파일. ServerCore 라이브러리를 링크한다.
file(GLOB_RECURSE GAMESERVER_SOURCES
        CONFIGURE_DEPENDS
        ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/*.h
)

add_executable(GameServer ${GAMESERVER_SOURCES})

target_link_libraries(GameServer PRIVATE ServerCore)