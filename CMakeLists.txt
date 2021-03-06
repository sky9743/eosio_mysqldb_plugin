# if(BUILD_MYSQL_DB_PLUGIN)
    file(GLOB HEADERS "include/eosio/mysql_db_plugin/*.hpp")
    include_directories(${CMAKE_CURRENT_SOURCE_DIR} include db mysqlconn /usr/include/mysql)
    link_directories(/usr/local/lib /usr/lib)
    
    add_library( mysql_db_plugin
                mysqlconn/mysqlconn.cpp
                db/connection_pool.cpp
                db/accounts_table.cpp
                db/transactions_table.cpp
                db/blocks_table.cpp
                db/actions_table.cpp
                mysql_db_plugin.cpp
                ${HEADERS} )

    target_link_libraries( mysql_db_plugin 
        PUBLIC chain_plugin eosio_chain appbase
        mysqlclient z
    )
    target_include_directories( mysql_db_plugin PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include" )
    eosio_additional_plugin(mysql_db_plugin)
# else()
#    message("mysql_db_plugin not selected and will be omitted.")
# endif()