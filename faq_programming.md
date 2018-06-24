# Solutions for the problems encountered when programming.

### (1) Problem: compile error "memcpy, not declared" in GCC 4.4

Solution: add the header file <cstring>. this only happens in gcc 4.4, older version doesn't have this problem.

### (2) Problem: compile using openmp error, 

​         undefined reference to `GOMP_parallel_end'
         undefined reference to `omp_get_num_threads'
         undefined reference to `GOMP_parallel_start'
         undefined reference to `omp_get_thread_num'
Solution: have to add "-fopenmp" in both compile and link time. CXXFLAGS += -fopenmp, LDFLAGS += -fopenmp. This happens only in gcc 4.4, the older version of gcc doesn't have this problem. 
Reference: http://gcc.gnu.org/ml/gcc-bugs/2008-12/msg01409.html

### (3) Problem: when make, having error "no rule to make target ..."

Solution: This may because there is some file that doesn't exist, the "make" can not find this file. (for example, I use gbr/*.h, but should be mlsvm/*.h). Try to use the "make -d" to print some debug information to find the error reasons.

### (4) Problem: svclassifier.cpp:(.text+0x197a): undefined reference to `svm_predict', when linking to the static library "liblibsvm.a".

Solution: The trick here is to put the library AFTER the module you are compiling. The problem is a reference thing. The linker resolves references in order, so when the library is BEFORE the module being compiled, the linker gets confused and does not think that any of the functions in the library are needed. By putting the library AFTER the module, the references to the library in the module are resolved by the linker.
Reference: http://stackoverflow.com/questions/1517138/trying-to-include-a-library-but-keep-getting-undefined-reference-to-messages

### (5) Problem: opencv 1.1pre1 can not compile, the error is "../../cxcore/include/cxmisc.h:133:6: error: #elif with no expression"

Solution: 
because the new gcc has changed the pre-processing scheme, and make the "#elif" with no experssion not correct. So just change #elif
to #else work solve the problem.

ref: http://ubuntuforums.org/showthread.php?t=1346876
cite others' saying:
Apparently a newer version of GCC changes the pre-processor, so this command elif without any expression will result in a compilation error.

http://gcc.gnu.org/gcc-4.4/porting_to.html

So, to fix this change the elif to else, and it compiles functionally.

### (6) Question: In VS2017, the compiler error: Undeclared (it's in stdint.h) INTMAX_MAX 

Tag: visual studio, vs, compiler error

Answer:

Add `__STDC_LIMIT_MACROS` and `__STDC_CONSTANT_MACROS`  in the macro defines. For QtCreator, in *.pro file, it is `DEFINES += __STDC_LIMIT_MACROS __STDC_CONSTANT_MACROS `. In the visual studio, it is ``

Ref: https://social.msdn.microsoft.com/Forums/vstudio/en-US/3a3dc941-af59-4788-b75e-74e585a25f3e/compile-issue-vs2015-undeclared-its-in-stdinth-intmaxmax?forum=vcgeneral

Done.

