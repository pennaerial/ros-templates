## Create a Python Package
To create a new python package, follow the steps below. For these steps to work, you must have a python file called `main.py` with a function `run()`. This `run` function will be called when executing the node. Instructions to change this default behavior is in another section. 

1. Copy the template_python package to the desired location
2. Open `CMakeLists` and update line 2 with your desired package name
3. Open `package.xml` and update the package name on line 3 with your desired package name
4. Open `setup.py` and replace `template_python` with your package name
5. Rename the template_python root package to the desired package name
6. Rename src/template_python to the same name
7. Remove src/PACKAGE_NAME/main.py and add your python source files here
8. Open `bin/main` and replace any instance of `template_python` with your package name (lines 3 and 6)
9. Run `cd ~/catkin_ws && catkin build`. You should see your package be built.
10. Test your package by first launching `roscore` in one terminal and running `rosrun PACKAGE_NAME main` in another.

## Add dependencies
For certain projects, the default dependencies (`geometry_msgs`, `roscpp`, `rospy`, and `std_msgs`) may not be enough. The steps below will walk you through adding additional dependencies. 

1. Open `CMakeLists.txt` in your favorite editor. 
2. Add the dependency to the `find_package` list (around line 7).
3. Open `package.xml` in your favorite editor.
4. Add the dependency to the `build_depend` and `run_depend` list (around line 45)

## Add additional executables to the package
This also applies if you do not wish to use the default `main.py` and `run` function.

1. Copy the existing `main` file in `bin/main` and rename to the filename in `src/` that you want to be called. For example, if I had a file `hello.py` in my `src/` folder, I would copy main and name it `hello`. 
2. Open the new file you copied
3. Replace the `import` line with `import <PACKAGE_NAME>.<FILE_NAME>`
4. Replace the function call (line 6) with `<PACKAGE_NAME>.<FILE_NAME>.<FUNCTION_NAME>()`
5.  Add the following lines to `CMakeLists.txt`, replacing BIN_FILE_NAME with the name of the bin file created in step one.

        catkin_install_python(PROGRAMS bin/BIN_FILE_NAME
            DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

## Rather do this from scratch?
Detailed instructions to build a ROS Python pacckage can be found here: http://wiki.ros.org/rospy_tutorials/Tutorials/Makefile
