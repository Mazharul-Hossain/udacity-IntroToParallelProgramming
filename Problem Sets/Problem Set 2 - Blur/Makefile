NVCC=nvcc
CC = g++

###################################
# These are the default install   #
# locations on most linux distros #
###################################

OPENCV_LIBPATH=/usr/local/lib
OPENCV_INCLUDEPATH=/usr/local/include/opencv4

###################################################
# On Macs the default install locations are below #
###################################################

#OPENCV_LIBPATH=/usr/local/lib
#OPENCV_INCLUDEPATH=/usr/local/include

OPENCV_LIBS=-lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs
CUDA_INCLUDEPATH=/usr/local/cuda/include

######################################################
# On Macs the default install locations are below    #
# ####################################################

#CUDA_INCLUDEPATH=/usr/local/cuda/include
#CUDA_LIBPATH=/usr/local/cuda/lib

NVCC_OPTS=-O3 -arch=sm_75 -Xcompiler -Wall -Xcompiler -Wextra -m64

GCC_OPTS=-O3 -Wall -Wextra -m64 $(shell pkg-config --cflags opencv4)
LDFLAGS = -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(shell pkg-config --libs opencv4)

student: main.o student_func.o compare.o reference_calc.o Makefile
	$(NVCC) -o HW2 main.o student_func.o compare.o reference_calc.o $(LDFLAGS) $(NVCC_OPTS)

main.o: main.cpp timer.h utils.h reference_calc.cpp compare.cpp HW2.cpp
	g++ -c main.cpp $(GCC_OPTS) -I $(CUDA_INCLUDEPATH) -I $(OPENCV_INCLUDEPATH)

student_func.o: student_func.cu utils.h
	nvcc -c student_func.cu $(NVCC_OPTS)

compare.o: compare.cpp compare.h
	g++ -c compare.cpp -I $(OPENCV_INCLUDEPATH) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

reference_calc.o: reference_calc.cpp reference_calc.h
	g++ -c reference_calc.cpp -I $(OPENCV_INCLUDEPATH) $(GCC_OPTS) -I $(CUDA_INCLUDEPATH)

clean:
	rm -f *.o student
