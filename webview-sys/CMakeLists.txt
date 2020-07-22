cmake_minimum_required(VERSION 3.17)

# This is a hack
# set(CMAKE_OSX_SYSROOT /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/)
set(CMAKE_OSX_DEPLOYMENT_TARGET 10.15)

project(webview-sys)

set(CMAKE_C_STANDARD 11)

# The Objective-C dispatch interfaces changed in macOS 10.15 so we need `OBJC_OLD_DISPATCH_PROTOTYPES` for backwards compat
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DOBJC_OLD_DISPATCH_PROTOTYPES")

find_library(COCOA_LIBRARY Cocoa)

add_library(Webview_cocoa webview_cocoa.c)

target_include_directories(Webview_cocoa SYSTEM PRIVATE ${CMAKE_OSX_SYSROOT}/usr/include)
target_include_directories(Webview_cocoa PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

