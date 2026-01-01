cmake_minimum_required(VERSION 3.11)
project(SuperMarioBros LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include(FetchContent)

# Fetch SFML 2.5.1 (fixes GLX typedef conflicts and provides Keyboard::Enter)
FetchContent_Declare(
  sfml
  GIT_REPOSITORY https://github.com/SFML/SFML.git
  GIT_TAG        2.5.1
)

set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build shared libraries" FORCE)

FetchContent_MakeAvailable(sfml)

# Collect source files
file(GLOB SOURCE_FILES "Source/*.cpp")

# Create executable
add_executable(mario ${SOURCE_FILES})

# Include directories
target_include_directories(mario PRIVATE "Source/Headers")
target_include_directories(mario PRIVATE ${sfml_SOURCE_DIR}/include)

# Link SFML libraries
target_link_libraries(mario sfml-graphics sfml-window sfml-system)

# Copy resources to build directory (optional)
file(COPY "Source/Resources" DESTINATION ${CMAKE_BINARY_DIR})