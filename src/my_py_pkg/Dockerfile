# Step 1: Use the official ROS2 Jazzy base image
FROM osrf/ros:jazzy-desktop

# Step 2: Set shell to bash for sourcing capabilities
SHELL ["/bin/bash", "-c"]

# Step 3: Create and set the workspace directory inside the container
WORKDIR /ros2_ws

# Step 4: Copy your custom package source code into the workspace
COPY . ./src/my_py_pkg

# Step 5: Install any missing system dependencies defined in package.xml
RUN apt-get update && rosdep update && \
    rosdep install --from-paths src --ignore-src -y && \
    rm -rf /var/lib/apt/lists/*

# Step 6: Build the Python package using colcon
RUN source /opt/ros/jazzy/setup.bash && \
    colcon build --packages-select my_py_pkg

# Step 7: Automatically source the built workspace for interactive shells
RUN echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc && \
    echo "source /ros2_ws/install/setup.bash" >> ~/.bashrc

# Step 8: Execution command to launch your node when the container starts
CMD ["bash", "-c", "source /ros2_ws/install/setup.bash && ros2 run my_py_pkg my_node"]
