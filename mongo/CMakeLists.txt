IF(MONGO)
	find_package (MongoDB)

	IF(MongoDB_FOUND)
		LOCATE_LIBRARY(LIBMONGOCLIENT "dbclient.h" "mongoclient" "mongo" "mongo/client")

		ADD_LIBRARY(mongodb MODULE
		    mongo)

		TARGET_LINK_LIBRARIES(mongodb
		    cocaine-common
		    boost_thread-mt
		    mongoclient)

		SET_TARGET_PROPERTIES(mongodb PROPERTIES
		    PREFIX ""
		    SUFFIX ".cocaine-plugin")

		INSTALL(TARGETS mongodb
		    LIBRARY DESTINATION lib/cocaine
		    COMPONENT runtime)
	ENDIF(MongoDB_FOUND)
ENDIF(MONGO)
