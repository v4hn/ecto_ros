macro(pytest pyfile)
  string(REPLACE ";" " " args "${ARGN}")
  add_test(ros_${pyfile}
    ${CMAKE_CURRENT_SOURCE_DIR}/run_test.sh  ${CATKIN_DEVEL_PREFIX}/setup.sh ${CMAKE_CURRENT_SOURCE_DIR}/${pyfile}.py ${args}
    )
endmacro()

if (CATKIN_ENABLE_TESTING)
  catkin_download_test_data(
    ${PROJECT_NAME}_t01.bag
    http://vault.willowgarage.com/wgdata1/vol1/ecto_data/t01.bag
    DESTINATION ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}/tests
  )
  set(T01 ${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}/tests/t01.bag)
  pytest(test_bag ${T01})
#pytest(test_sync_sub ${T01} ) 
#pytest(test_image_sub ${T01} )
#pytest(test_image_sub_threadpool ${T01} )
#pytest(test_reinit ${T01} )
#pytest(test_reinit_threadpool ${T01} )
endif()
