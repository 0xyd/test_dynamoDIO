cmake_minimum_required(VERSION 3.7)
project(TestMyDummyClinet)

add_library(test_client SHARED test_client.c)
find_package(DynamoRIO)
if (NOT DynamoRIO_FOUND)
  message(FATAL_ERROR "DynamoRIO package required to build")
endif(NOT DynamoRIO_FOUND)
configure_DynamoRIO_client(test_client)
