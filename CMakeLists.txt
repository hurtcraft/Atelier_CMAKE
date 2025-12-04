cmake_minimum_required(VERSION 3.5)
project(calculator C)
add_subdirectory(include)
add_subdirectory(src)
include_directories(include)
enable_testing()
add_test(t1 src/calculator add 2 3)
add_test(t2 src/calculator sub 3 -2)
add_test(t3 src/calculator mul 5 5)
add_test(t4 src/calculator div 1 5)
add_test(t5 src/calculator square 2)

Test_Add:
runs-on: ubuntu-latest
needs: Compilation
steps:
    - name: Test fonction add
    run: |
        last_directory=$(basename ${{ runner.workspace }})
        git clone https://github.com/${{ github.repository }}.git
        cd ./$last_directory
        mkdir build
        cd build
        cmake ..
        make
        ./src/calculator add 10 5