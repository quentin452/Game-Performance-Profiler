# Game-Performance-Profiler

Just a Profiler for CPP Games and software

# How to use

1 : Use one of these example or you can use both

# Example 1

This first version will probably use more RAM because each call to `PROFILE_SCOPED` creates an object, but it will be more precise.

```cpp
#include <game_performance_profiler.hpp>

void ExampleMethod() {
    PROFILE_SCOPED(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
    VkSemaphoreCreateInfo semaphoreInfo = {};
    // YOUR CODE
}
```

# Example 2

This second version will probably use less ram than version one, but will be less precise

```cpp
#include <game_performance_profiler.hpp>

void ExampleMethod() {
    PROFILE_START(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
    // YOUR CODE
    PROFILE_STOP(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
}
```

2 : call this when you exit your game if you use ThreadedLoggerForCpp "https://github.com/quentin452/ThreadedLoggerForCPP" , it will copy the print in the LoggerGlobals::LogFilePath

```cpp
#include <game_performance_profiler.hpp>

// Call this in your exit game method
gamePerformanceProfiler.printWithLogMessageAsync();

```

or this if you don't use ThreadedLoggerForCpp and he will copy the print in the path you written in the first argument of printWithoutLogMessageAsyn

```cpp
#include <game_performance_profiler.hpp>

// Call this in your exit game method
gamePerformanceProfiler.printWithoutLogMessageAsync("game_performance_profiler.log");
```
