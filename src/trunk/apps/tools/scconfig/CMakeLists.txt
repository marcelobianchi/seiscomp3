IF (SC_GLOBAL_GUI)
	FIND_PACKAGE(Qt4 REQUIRED)

	SET(NEWCONFIG_TARGET scconfig)

	SET(
		NEWCONFIG_MOC_HEADERS
			gui.h
			fancyview.h
			wizard.h
			editor.h
			panels/inspector.h
			panels/bindings.h
			panels/information.h
			panels/inventory.h
			panels/modules.h
			panels/system.h
			panels/help.h
	)

	SET(
		NEWCONFIG_RESOURCES
			icons.qrc
	)

	SET(
		NEWCONFIG_UI
			panels/inspector.ui
	)

	IF (NEWCONFIG_MOC_HEADERS)
		QT4_WRAP_CPP(NEWCONFIG_MOC_SOURCES ${NEWCONFIG_MOC_HEADERS} OPTIONS -DBOOST_TT_HAS_OPERATOR_HPP_INCLUDED)
	ENDIF (NEWCONFIG_MOC_HEADERS)

	IF (NEWCONFIG_UI)
		QT4_WRAP_UI(NEWCONFIG_UI_HEADERS ${NEWCONFIG_UI})
		INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})
		INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})
	ENDIF (NEWCONFIG_UI)

	IF (NEWCONFIG_RESOURCES)
		QT4_ADD_RESOURCES(NEWCONFIG_RESOURCE_SOURCES ${NEWCONFIG_RESOURCES})
	ENDIF (NEWCONFIG_RESOURCES)

	SET(
		NEWCONFIG_SOURCES
			main.cpp
			gui.cpp
			flowlayout.cpp
			fancyview.cpp
			wizard.cpp
			editor.cpp
			panels/inspector.cpp
			panels/bindings.cpp
			panels/information.cpp
			panels/inventory.cpp
			panels/modules.cpp
			panels/system.cpp
			panels/help.cpp
			${NEWCONFIG_MOC_SOURCES}
			${NEWCONFIG_RESOURCE_SOURCES}
			${NEWCONFIG_UI_HEADERS}
	)


	INCLUDE(${QT_USE_FILE})

	SC_ADD_EXECUTABLE(NEWCONFIG ${NEWCONFIG_TARGET})
	SC_LINK_LIBRARIES_INTERNAL(${NEWCONFIG_TARGET} core)
	SC_LINK_LIBRARIES(${NEWCONFIG_TARGET} ${QT_LIBRARIES})

	INSTALL(FILES data/README DESTINATION ${SC3_PACKAGE_APP_CONFIG_DIR}/inventory)
ENDIF (SC_GLOBAL_GUI)
