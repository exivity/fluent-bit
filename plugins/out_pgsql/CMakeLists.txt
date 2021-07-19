set(src
  pgsql.c
  pgsql_connections.c
  )

FLB_PLUGIN(out_pgsql "${src}" "")
target_include_directories(flb-plugin-out_pgsql PRIVATE ${PostgreSQL_INCLUDE_DIRS})
target_link_libraries(flb-plugin-out_pgsql -lpq)

# Include and link libpq on Windows.
if (FLB_SYSTEM_WINDOWS)
  # find PG include, have to specify full path because AppVeyor install several versions of PG and none of them is in the PATH
  execute_process(COMMAND "c:/Program Files/PostgreSQL/9.6/bin/pg_config.exe" --includedir OUTPUT_VARIABLE PG_INCLUDE)
  execute_process(COMMAND "c:/Program Files/PostgreSQL/9.6/bin/pg_config.exe" --libdir OUTPUT_VARIABLE PG_LIB)
  message(STATUS "PG include is in ${PG_INCLUDE}, PG lib is ${PG_LIB}")
  string(STRIP ${PG_INCLUDE} PG_INCLUDE)
  string(STRIP ${PG_LIB} PG_LIB)
  message(STATUS "PG include is in ${PG_INCLUDE}, PG lib is ${PG_LIB}")
  # Include directories 
  include_directories(${PG_INCLUDE})
  link_directories(${PG_LIB})
endif()
