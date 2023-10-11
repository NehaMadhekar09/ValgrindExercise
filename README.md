# Valgrind Exercise

## Standard install via command-line
```bash
# Configure the project and generate a native build system:
  # Must re-run this command whenever any CMakeLists.txt file has been changed.
  cmake -S ./ -B build/
# Compile and build the project:
  # rebuild only files that are modified since the last build
  cmake --build build/
  # or rebuild everything from scracth
  cmake --build build/ --clean-first
  # to see verbose output, do:
  cmake --build build/ --verbose
# Run program:
  ./build/app/shell-app
# Clean
  cmake --build build/ --target clean
# Clean and start over:
  rm -rf build/
```

## Command to run
valgrind --leak-check=full --track-origins=yes -s ./build/app/shell-app &> valgrind_output.txt


## Bugs Found
1. Uninitialized variable 'terminator' in main.cpp
Solution: Initialized it as true 

2. Memory was allocated on heap using std::vector<int> *readings. However, it was not freed/deleted, producing memory leaks.
Solution: Delete the pointer readings and set to nullptr. 
  Alternatively, the code can be implemented without allocating memory on the heap. 


## Valgrind Outputs before and after the fix
Valgrind output before fix: valgrind_output_before_fix.txt
Valgrind output after fix: valgrind_output_after_fix.txt


