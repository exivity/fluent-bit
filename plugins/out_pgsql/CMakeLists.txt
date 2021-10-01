set(src
  pgsql.c
  pgsql_connections.c
  )

if (PostgreSQL_FOUND)
    FLB_PLUGIN(out_pgsql "${src}" "")
    target_include_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_INCLUDE_DIRS})
    if (FLB_SYSTEM_WINDOWS)    
        target_link_libraries(flb-plugin-out_pgsql ${PostgreSQL_LIBRARY_DIRS}/libpq.lib)
    else ()
        target_link_libraries(flb-plugin-out_pgsql -lpq)
    endif()
endif()
