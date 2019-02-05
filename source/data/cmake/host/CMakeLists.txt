cmake_minimum_required(VERSION 3.10)

option(HUNTER_STATUS_DEBUG "Debug info" ON)

include("${CMAKE_CURRENT_LIST_DIR}/../../../../cmake/HunterGate.cmake")

HunterGate(
    URL "${HUNTER_HOST_URL}"
    SHA1 "${HUNTER_HOST_SHA1}"
)

project(ICUHost)

hunter_add_package(ICU)
