cmake_minimum_required(VERSION 3.26.4)

project(IconFontCppHeaders)

add_library(IconFontCppHeaders INTERFACE)
target_sources(IconFontCppHeaders PRIVATE
	"IconsFontAwesome6Pro.h"
	"IconsFontAwesome6ProBrands.h"
)
target_include_directories(IconFontCppHeaders INTERFACE .)