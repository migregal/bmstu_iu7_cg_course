cmake_minimum_required(VERSION 3.16)
project(bmstu_iu7_cg_course)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt5 COMPONENTS
        Core
        Gui
        Widgets
        REQUIRED)

set(QT_GUI
        ui/qt/design.ui
        ui/qt/mainwindow.h
        ui/qt/mainwindow.cpp

        ui/qt/widgets/ColorPicker.h
        ui/qt/widgets/ColorPicker.cpp
        )

set(BOUNDER
        src/bounders/Bounder.h

        src/bounders/aabb/AABB.h
        src/bounders/aabb/AABB.cpp

        src/bounders/sphere/Sphere.h
        src/bounders/sphere/Sphere.cpp
)

set(CAMERA
        src/camera/Camera.h
        src/camera/Camera.cpp

        src/camera/CameraSolution.h
        )

set(DRAWER
        src/drawer/Drawer.h
        src/drawer/Drawer.cpp

        src/drawer/qt/QtDrawer.h
        src/drawer/qt/QtDrawer.cpp
        )

set(ENGINE
        src/engine/Engine.h
        src/engine/Engine.cpp

        src/engine/qt/QtEngine.h
        src/engine/qt/QtEngine.cpp
        )

set(FRACTALS
        src/fractals/Fractal.h
        src/fractals/Fractal.cpp

        src/fractals/mandelbulb/Mandelbulb.h
        src/fractals/mandelbulb/Mandelbulb.cpp

        src/fractals/julia/Julia.h
        src/fractals/julia/Julia.cpp

        # src/fractals/julia/Julia.h
        # src/fractals/julia/Julia.cpp
        )

set(LIGHT
        src/light/Light.h
        src/light/Light.cpp
        )

set(MATERIAL
        src/material/Material.h
        src/material/Material.cpp
        )

set(MATH
        src/math/Matrix.h
        src/math/Vector.h
        )

add_executable(${PROJECT_NAME}
        ${QT_GUI}
        ${BOUNDER}
        ${CAMERA}
        ${DRAWER}
        ${ENGINE}
        ${FRACTALS}
        ${LIGHT}
        ${MATERIAL}
        ${MATH}
        main.cpp
        )

target_link_libraries(${PROJECT_NAME} PRIVATE
        Qt5::Core
        Qt5::Gui
        Qt5::Widgets
        )

find_package(OpenMP)
if(OpenMP_CXX_FOUND)
    target_link_libraries(${PROJECT_NAME} PUBLIC OpenMP::OpenMP_CXX)
endif()

target_include_directories(${PROJECT_NAME} PRIVATE
        ./src/
        ./ui/
        )
