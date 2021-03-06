MACRO(build_dynamic_reporter name)
    IF (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
        SET(CMAKE_SHARED_LINKER_FLAGS "-undefined dynamic_lookup")
    ENDIF()

    ADD_LIBRARY(${name}Reporter SHARED ${name}Reporter.cpp)

    SET_TARGET_PROPERTIES(${name}Reporter
        PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/reporters.dl
				   RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/reporters.dl
        )

    TARGET_LINK_LIBRARIES(${name}Reporter
        OCLintCore
        )
ENDMACRO(build_dynamic_reporter)

BUILD_DYNAMIC_REPORTER(Text)
BUILD_DYNAMIC_REPORTER(HTML)
BUILD_DYNAMIC_REPORTER(XML)
BUILD_DYNAMIC_REPORTER(JSON)
BUILD_DYNAMIC_REPORTER(PMD)
