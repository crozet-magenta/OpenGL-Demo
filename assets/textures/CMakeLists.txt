FILE(GLOB Textures
	 RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}
	 ${CMAKE_CURRENT_SOURCE_DIR}/*.png)

ADD_CUSTOM_TARGET (textures
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	DEPENDS ${PROJECT_SOURCE_DIR}/assets/textures.o
	)

ADD_CUSTOM_COMMAND(OUTPUT ${PROJECT_SOURCE_DIR}/assets/textures.o
	COMMENT "Regeneration des textures."
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	COMMAND resgen *.png > textures.res
	COMMAND ld -r -b binary textures.res -o ${PROJECT_SOURCE_DIR}/assets/textures.o
	DEPENDS resgen ${Textures}
	)
