# MIT License
#
# Copyright (c) 2018 char-lie
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
add_library(image image.cpp)
add_library(pgm_io pgm_io.cpp)
add_library(disparity_graph disparity_graph.cpp)
target_include_directories(
    image PUBLIC
    ${STEREO_PARALLEL_MAIN_INCLUDE_DIR}
)
target_include_directories(
    pgm_io PUBLIC
    ${STEREO_PARALLEL_MAIN_INCLUDE_DIR}
)
target_include_directories(
    disparity_graph PUBLIC
    ${STEREO_PARALLEL_MAIN_INCLUDE_DIR}
)
target_link_libraries(
    pgm_io
    image
)
target_link_libraries(
    disparity_graph
    image
)

find_package(Boost 1.54 REQUIRED COMPONENTS program_options)
add_executable(stereo_parallel main.cpp)
target_include_directories(
    stereo_parallel
    PRIVATE
    ${BOOST_INCLUDE_DIRS}
)
target_link_libraries(
    stereo_parallel
    image
    pgm_io
    ${Boost_PROGRAM_OPTIONS_LIBRARY}
)