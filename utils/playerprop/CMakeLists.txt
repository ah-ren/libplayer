OPTION (BUILD_UTILS_PLAYERPROP "Build the playerprop utility" ON)
IF (BUILD_UTILS_PLAYERPROP)
    IF (BUILD_PLAYERCC)
        IF (NOT HAVE_XDR)
            INCLUDE_DIRECTORIES (${PROJECT_SOURCE_DIR}/replace)
        ENDIF (NOT HAVE_XDR)
        IF (NOT HAVE_GETOPT)
            INCLUDE_DIRECTORIES (${PROJECT_SOURCE_DIR}/replace)
            SET (playerreplaceLib playerreplace)
        ENDIF (NOT HAVE_GETOPT)
        INCLUDE_DIRECTORIES (${PROJECT_SOURCE_DIR}/client_libs ${PROJECT_BINARY_DIR}/client_libs)

        LINK_DIRECTORIES (${PLAYERCC_EXTRA_LINK_DIRS})
        PLAYER_ADD_EXECUTABLE (playerprop playerprop.cpp ${getoptSrc})
        TARGET_LINK_LIBRARIES (playerprop playerc++ playerc playerinterface playercommon
                               ${playerreplaceLib} ${PLAYERC_EXTRA_LINK_LIBRARIES}
                               ${PLAYERCC_EXTRA_LINK_LIBRARIES})
        # TARGET_LINK_LIBRARIES (playerprop playerc++ playerc playerinterface playercommon
        #                         ${playerreplaceLib} ${PLAYERC_EXTRA_LINK_LIBRARIES})
    ELSE (BUILD_PLAYERCC)
        MESSAGE (STATUS "playerprop will not be built - playerc++ client library is disabled")
    ENDIF (BUILD_PLAYERCC)
ENDIF (BUILD_UTILS_PLAYERPROP)
