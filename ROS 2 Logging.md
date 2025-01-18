- [Logging in ROS 2 Humble](https://docs.ros.org/en/humble/Tutorials/Demos/Logging-and-logger-configuration.html)
- [Logging Concepts](https://docs.ros.org/en/humble/Concepts/Intermediate/About-Logging.html)
* [rclcpp/logging api](https://docs.ros2.org/latest/api/rclcpp/logging_8hpp.html)

Logger levels follow hierarchy based on their names and the logging levels of their parents UNLESS explicitly set

It probably pretty important to know that logging in ROS 2 has a number of environment variables that it uses to configure the outputs

- ROS_LOG_DIR/ROS_HOME -> directory logging configuration
- RCUTILS_CONSOLE_OUTPUT_FORMAT -> format
- RCUTILS_COLORIZED_OUTPUT -> color control
- RCUTILS_LOGGING_BUFFERED_STREAM -> buffer of the output
- RCUTILS_LOGGING_USE_STDOUT -> stdcou vs stderr output 


The rclcpp library has a couple of nifty functions that are not outward advertised
* RCLCPP_INFO(logger, ...)
* RCLCPP_INFO_ONCE(logger, ...)
* RCLCPP_INFO_EXPRESSION(logger, expression, ...)
* RCLCPP_INFO_FUNCTION(logger, function, ...)
	* specifically these two are pretty interesting, you dont need to write code embeds logic around you logging, but just have the logging do that for you 
* RCLCPP_INFO_SKIPFIRST(logger, ...)
* RCLCPP_INFO_THROTTLE(logger, clock, duration, ...)
* RCLCPP_INFO_SKIPFIRST_THROTTLE(logger, clock, duration, ...)
  



---
[[Standard Streams]]