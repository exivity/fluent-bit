set(src
  pgsql.c
  pgsql_connections.c
  )

find_package(PostgreSQL REQUIRED)
if (PostgreSQL_FOUND)
    FLB_PLUGIN(out_pgsql "${src}" "")
    # This line adds both include paths and libraries for Postgres
    target_link_libraries(flb-plugin-out_pgsql PRIVATE PostgreSQL::PostgreSQL)

    # target_include_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_INCLUDE_DIRS})
    # if (FLB_SYSTEM_WINDOWS)    
    #     target_link_libraries(flb-plugin-out_pgsql ${PostgreSQL_LIBRARY_DIRS}/libpq.lib)
    # else ()
    #     target_link_libraries(flb-plugin-out_pgsql -lpq)
    # endif()
endif()
