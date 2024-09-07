# Game-Performance-Profiler
Just a Profiler for CPP Games and software

#How to use examples

1 : Use one of these example or you can use both 

# Example 1
This first version will probably use more RAM because each call to `PROFILE_SCOPED` creates an object, but it will be more precise.
```cpp
#include <game_performance_profiler.hpp>

void createSemaphores() {
    PROFILE_SCOPED(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
    VkSemaphoreCreateInfo semaphoreInfo = {};
    semaphoreInfo.sType = VK_STRUCTURE_TYPE_SEMAPHORE_CREATE_INFO;
    if (vkCreateSemaphore(VulkanGlobals::device, &semaphoreInfo, nullptr, &VulkanGlobals::imageAvailableSemaphore) != VK_SUCCESS ||
        vkCreateSemaphore(VulkanGlobals::device, &semaphoreInfo, nullptr, &VulkanGlobals::renderFinishedSemaphore) != VK_SUCCESS) {
        LOGGER_THREAD(LogLevel::ERRORING, "Failed to create semaphores!")
        exit(EXIT_FAILURE);
    }
}
```

# Example 2
This second version will probably use less ram than version one, but will be less precise
```cpp
#include <game_performance_profiler.hpp>

void createSemaphores() {
    PROFILE_START(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
    VkSemaphoreCreateInfo semaphoreInfo = {};
    semaphoreInfo.sType = VK_STRUCTURE_TYPE_SEMAPHORE_CREATE_INFO;
    if (vkCreateSemaphore(VulkanGlobals::device, &semaphoreInfo, nullptr, &VulkanGlobals::imageAvailableSemaphore) != VK_SUCCESS ||
        vkCreateSemaphore(VulkanGlobals::device, &semaphoreInfo, nullptr, &VulkanGlobals::renderFinishedSemaphore) != VK_SUCCESS) {
        LOGGER_THREAD(LogLevel::ERRORING, "Failed to create semaphores!")
        exit(EXIT_FAILURE);
    }
    PROFILE_STOP(std::string("Catz-Voxel-Engine:") + ":" + __FUNCTION__)
}
```

2 : call this when you exit your game if you use ThreadedLoggerForCpp "https://github.com/quentin452/ThreadedLoggerForCPP" , it will copy the print in the LoggerGlobals::LogFilePath
```cpp
#include <game_performance_profiler.hpp>

// Call this in your exit game method
gamePerformanceProfiler.printWithLogMessageAsync();

```
or this if you don't use ThreadedLoggerForCpp and he will copy the print in the path you written in the first argument of  printWithoutLogMessageAsyn
```cpp
#include <game_performance_profiler.hpp>

// Call this in your exit game method
gamePerformanceProfiler.printWithoutLogMessageAsync("game_performance_profiler.log");
```