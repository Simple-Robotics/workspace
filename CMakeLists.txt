cmake_minimum_required(VERSION 3.12)
project(root)
include(CTest)

set(PROJECT_WORKSPACE ON)
set(PROJECT_PACKAGES_IN_WORKSPACE)
set(PROJECT_PYTHON_PACKAGES_IN_WORKSPACE)

macro(add_eigenpy)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE eigenpy)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/eigenpy/python)
  add_subdirectory(eigenpy)
endmacro()
macro(add_hpp_fcl)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE hpp-fcl)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/hpp-fcl/python)
  add_subdirectory(hpp-fcl)
endmacro()
macro(add_pinocchio)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE pinocchio)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/pinocchio/bindings/python)
  add_subdirectory(pinocchio)
endmacro()
macro(add_pycppad)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE pycppad)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/pycppad/python)
  add_subdirectory(pycppad)
endmacro()
macro(add_example_robot_data)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE example-robot-data)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/example-robot-data/python)
  add_subdirectory(example-robot-data)
endmacro()
macro(add_proxsuite)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE proxsuite)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/proxsuite/bindings/python)
  add_subdirectory(proxsuite)
endmacro()
macro(add_proxsuite_nlp)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE proxsuite-nlp)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/proxsuite-nlp/bindings/python)
  add_subdirectory(proxsuite-nlp)
endmacro()
macro(add_aligator)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE aligator)
  list(APPEND PROJECT_PYTHON_PACKAGES_IN_WORKSPACE
       ${PROJECT_BINARY_DIR}/aligator/bindings/python)
  add_subdirectory(aligator)
endmacro()
macro(add_loik)
  list(APPEND PROJECT_PACKAGES_IN_WORKSPACE loik)
  add_subdirectory(LoIK)
endmacro()

# add_eigenpy()

# add_hpp_fcl()

# add_pinocchio()

# add_pycppad()

# add_example_robot_data()

# add_proxsuite()

# add_proxsuite_nlp()

# add_aligator()

# add_loik()
