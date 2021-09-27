set(src
  pgsql.c
  pgsql_connections.c
  )

FLB_PLUGIN(out_pgsql "${src}" "")

if (PostgreSQL_FOUND)
    if (FLB_SYSTEM_WINDOWS)
        target_include_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_INCLUDE_DIRS})
        target_link_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_LIBRARY_DIRS})
        target_link_libraries(flb-plugin-out_pgsql ${PostgreSQL_LIBRARY_DIRS}/libpq.lib)
    else ()
        target_include_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_INCLUDE_DIRS})
        target_link_libraries(flb-plugin-out_pgsql -lpq)
    endif()
endif()
