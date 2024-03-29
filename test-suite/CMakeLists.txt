set(QLXAD_TEST_SOURCES
    americanoption_xad.cpp
    barrieroption_xad.cpp
    batesmodel_xad.cpp
    bermudanswaption_xad.cpp
    bonds_xad.cpp
    creditdefaultswap_xad.cpp
    europeanoption_xad.cpp
    forwardrateagreement_xad.cpp
    hestonmodel_xad.cpp
    swap_xad.cpp
    
    utilities_xad.cpp
    quantlibtestsuite_xad.cpp
)

set(QLXAD_TEST_HEADERS utilities_xad.hpp)

if(QL_BUILD_TEST_SUITE)
    add_executable(quantlib-xad_test_suite ${QLXAD_TEST_SOURCES} ${QLXAD_TEST_HEADERS})
    set_target_properties(quantlib-xad_test_suite PROPERTIES OUTPUT_NAME "quantlib-xad-test-suite")
    if (NOT Boost_USE_STATIC_LIBS)
        target_compile_definitions(quantlib-xad_test_suite PRIVATE BOOST_ALL_DYN_LINK)
    endif()
    target_link_libraries(quantlib-xad_test_suite PRIVATE
        ql_library
        ${QL_THREAD_LIBRARIES})
    if (QL_INSTALL_TEST_SUITE)
        install(TARGETS quantlib-xad_test_suite RUNTIME DESTINATION ${QL_INSTALL_BINDIR})
    endif()
    add_test(NAME quantlib-xad_test_suite COMMAND quantlib-xad_test_suite --log_level=message)
endif()