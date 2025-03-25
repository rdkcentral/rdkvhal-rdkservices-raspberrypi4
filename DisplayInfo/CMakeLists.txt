# If not stated otherwise in this file or this component's LICENSE file the
# following copyright and licenses apply:
#
# Copyright 2025 RDK Management
#
# Licensed under the Apache License, Version 2.0 (the "LICENSE");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.3)

list(APPEND CMAKE_MODULE_PATH
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake/")

# Set the source files
set(SoC_SOURCES SoC_abstraction.cpp kms.c)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBDRM REQUIRED libdrm)

add_library(displayinfo-soc SHARED ${SoC_SOURCES})

target_include_directories(displayinfo-soc PUBLIC ${LIBDRM_INCLUDE_DIRS})
target_link_libraries(displayinfo-soc PUBLIC ${LIBDRM_LIBRARIES})

install(TARGETS displayinfo-soc LIBRARY DESTINATION lib)
install(FILES kms.h DESTINATION include)
