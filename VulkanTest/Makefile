CFLAGS = -std=c++17 -O2 -arch arm64
LDFLAGS = -I/opt/homebrew/include -I./libs/tinyobjloader -L/opt/homebrew/Cellar/glfw/3.3.8/lib -lvulkan -lglfw

vertSources = $(shell find ./shaders -type f -name "*.vert")
vertObjFiles = $(patsubst %.vert, %.vert.spv, $(vertSources))
fragSources = $(shell find ./shaders -type f -name "*.frag")
fragObjFiles = $(patsubst %.frag, %.frag.spv, $(fragSources))

TARGET = VulkanTest.out
$(TARGET): $(vertObjFiles) $(fragObjFiles)
$(TARGET): *.cpp *.hpp
	clang++ $(CFLAGS) -o $(TARGET) *.cpp $(LDFLAGS)

%.spv: %
	~/VulkanSDK/1.3.224.1/macOS/bin/glslc $< -o $@

run: *.cpp *.hpp
	clang++ $(CFLAGS) -o VulkanTest.out *.cpp $(LDFLAGS)

.PHONY: test clean

test: VulkanTest
	./VulkanTest.out

clean:
	rm -f VulkanTest.out
	rm -f *.spv