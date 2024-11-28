# Copyright 2016 The Cartographer Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.2)

project(cartographer)


include(CMakeParseArguments)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake/)

# 查找 Python
find_package(Python3 REQUIRED)

# 查找 Sphinx
execute_process(
    COMMAND ${Python3_EXECUTABLE} -c "import sphinx; print(sphinx.__file__)"
    OUTPUT_VARIABLE SPHINX_MODULE_PATH
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

# Only build the documentation if we can find Sphinx.
find_package(Sphinx)
if(SPHINX_FOUND)
  add_subdirectory("docs")
endif()
