set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DSTATICLIB")

aux_source_directory(. SRC_LIST)

file(GLOB HEADERS "*.h")

add_library(p2p ${SRC_LIST} ${HEADERS})

eth_use(p2p OPTIONAL Miniupnpc)

find_package(Dev)

eth_use(p2p OPTIONAL OpenSSL)

target_include_directories(p2p PRIVATE ..)
target_link_libraries(p2p ${Dev_DEVCORE_LIBRARIES})
target_link_libraries(p2p ${Dev_DEVCRYPTO_LIBRARIES})
target_link_libraries(p2p ${OPENSSL_SSL_LIBRARIE} ${OPENSSL_CRYPTO_LIBRARIE})

install(TARGETS p2p RUNTIME DESTINATION bin ARCHIVE DESTINATION lib LIBRARY DESTINATION lib)