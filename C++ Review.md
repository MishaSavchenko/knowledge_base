Dynamic memory Allocation

* Allows the request specific amount memory to be allocated on the heap. Since the memory isn't allocated on the stack frame it is not freed when the function returns.   
*   
* Stack: static memory allocation, heap: dynamic memory allocation, both stored in RAM  
  * Stack:   
    * allocated variables are directly stored to the memory   
    * access to this memory is very fast  
    * Allocation is dealt when the program is compiled  
    * Reserved in LIFO order (most recent reservation is freed first)  
    * “Freeing a block from the stack is nothing more than adjusting one pointer”  
    * Thread specific   
  * Heap:  
    * Allocated at run time (changes sizes)  
    * Accessing memory is a bit slower  
    * Heap size is only limited by the virtual memory size  
    * No dependency between element and random access   
    * Application specific  
    * The memory allocation library manages the free memory in the heap and when the allocation cannot be done, the allocation library increases the boundary of the heap allowing it to grow  
* C: \#include \<stdlib.h\>  
  * Malloc  
    * Allocates memory  

| void \* malloc\[size\_t size\] |
| :---- |

    * Return pointer to the allocated memory   
    * Portability and maintainability are the reason why inputting specific number of bytes isnt good  
    * Portability influences the amount of bytes a type may need  
    * sizeof   
      * operator determines the amount of bytes a type requires   
      * Evaluated during compile time 

| Int \* myArray \= malloc( 6 \* sizeof(\*myArray)) |
| :---- |

        * The sizeof(\*myArray) will be determined during compile time and will allow to change the myArray type without changing the sizeof() input   
    * May return NULL if the heap is out of space  
    * Shallow vs deep copying   
      * Copying pointer without allocating memory for the copied information   
* Free  
	* Frees memory 
	   ``` void free(void * ptr);```
		* Memory associated with the stack is automatically removed as soon as the function returns   
		* Memory on the heap must be explicitly freed   
		* Only frees the memory block it points to   
	* Memory Leaks 
		* Losing all the references to a block of memory while it is still allocated
		* Valgrind detects memory leaks
		* Double freeing ( trying to free the same black of memory more than once )  
		* May segfault   
	* Malloc may crash   
		* Corrupted bookkeeping structures of the memory allocation library   
		* Freeing stack memory may segfault  
  * Realloc  
    * Allocate a new block of memory, copy the contents to the new and free the old one   
    * Void \* realloc(void \* ptr, size\_t size);  
    * Pointer to new area, or NULL if failure  
    * New pointer location may not be anywhere near original location   
    * If realloc fails it may cause a memory leak    
  * Calloc   
    * If malloc just allocates memory, calloc zeros out memory   
  * Getline (\#include \<stdio.h\> )  
    * fgets ( reads string into buffer is limited by the amount of space you allocate for it) 

| size\_t getline(char \*\*inep, size\_t \*lineacapp, FILE \*stream) |
| :---- |

    * Reads characters until encountering ‘\\n’ copying the characters into the buffer in memory  
    * Places ‘\\0’ after reading new line char which indicates the end of the string   
    * Allocates space for the string as needed  
* C++:  
  * Section E6  
  * “The only difference between a class and a struct is the default access control of its members”  
    * Struct: default access is public   
    * Class: default access is private  
  * Access Control  
    * Public: can be accessed  
    * Private: only accessed by code in the class  
    * Protected: Chapter 18  
  * Encapsulation: combining into a single logical unit  
  * const Methods  
    * Wanting to specify this argument as a const pointer 

| int getX() const{    return x;} |
| :---- |

    * Cannot modify anything in the object it points at   
  * Static Members   
    * Field or method that acts on no particular instance of that class  
    * Static means that its shared by all instances of the class

| class MyClass{   Static unsigned long MyField;   ...};unsigned long MyClass::MyField \= 0; |
| :---- |

    * :: scope resolution operator   
      * Allows for the specification of name inside another scope  
    * Static methods cannot access non-static member of the class since they do not have the implicit this pointer passed to them   
    * Restricts the visibility to compilation unit it is declared in   
    * May not be used by another compilation unit   
  * Namespaces  
    * Named scopes

| namespace dataAnalysis {   class DataPoint { ... };   class DataSet { ... };   DataSet combineDataSets(DataSet \* array, int n);} |
| :---- |

    * 2 way to reference a name declared inside of a namespace  
      * Use the scope resolution operator ::  
      * Open the namespace with **using** keyword    
  * Name Mangling  
    * **extern “C”**  
      * Allows for explicit statement for which functions should be complied with C compiler   
    * Adjusting the function names to encode the parameter type information as well as what class and namespace the function resides in by the compiler   
    * This is done to make the function names unique   
    * C does not mangle names   
    *   
  * References  
    * Like a pointer provides access to a “box”   
    * But   
      * Once reference is initialized it cannot be changed  
      * Automatically dereferenced whereas pointers need to be explicitly dereferenced  
      * Must be initialized when its declared  
      * Cannot have a NULL reference   
      * Cannot have a reference to a reference (int &\&x)  
      * Cannot have a pointer to a reference  (int &\* x)  
      * Can have a reference to a pointer ( int \*& x)   
      * Cannot reference arithmetic   
      *   
  * New / object construction   
    * Malloc cannot be used for classes because it does not call the proper constructor and has no idea how much space to actually allocate  
    * Allocates memory for the specified class   
    * Can also allocate space for an array

| BankAccount \* accountArray \= new BankAccount\[42\](); |
| :---- |

      * Creating an array of objects can only be done using their default constructors  
      * Instead create an array of pointers 

| BankAccount \*\* accountPointerArray \= new BankAccount\*\[42\](); |
| :---- |

    * Value and Default Initialization  
      * Value initialization, a class with a default constructor is initialized by its default constructor  
        * Class without any constructor has every field value initialized   
        * Non-class types are zero initialized   
        * Arrays have elements value initialized  
      * Default initialization, non-POD types are initialized by their default constructors and POD types are left uninitialized   
        * Arrays has their elements default initialized  
    * Initialization lists:  
      * Initialization are different from assignments   
      * C++ ensures all fields have some form of initialization before the open constructor goes into function   
      * Initialization for POD types leaves them with unspecified values   
      * Assignments do not specify initialization values   
      * Assignments instead of initialization may result in unwanted or slower behaviours   
      * References cannot be assigned to   
      * Const fields must be initialized in the initializer list  
      * Order by which the field are initialized is the order with which they are declared in the class  
    * new\[\] does not have realloc analog as its becomes a much different problem when non-POD is involved   
  * Delete / object destruction   
    * Destructors may not be overloaded, and cannot take any parameters  
    * Destructors are mostly useful when there is some dynamically allocated memory in the class   
    * New \-\> delete, new\[\] \-\> delete\[\] (the only correct form)   
      * Mixing may result in memory leaks or segfaults   
    * Destructors are invoked when there is either   
      * Dynamic deallocation through delete  
      * Local variable going out of scope  
      * By one object that contains another being destroyed   
    * Deallocation for array with delete\[\]  
      * Elements of the array have heir destructors invoked in decreasing order of index (opposite of the construction order)  
    * Order of destruction is generally the opposite of order of construction  
    * Local variable must invoke destructors before the scope is exited is destroyed   
    * Trivial destructors \-\> Default destructor, no manually written destructors   
    * Nontrivial destructors \-\> Any type of explicitly written destructors  
      * Any class with nontrivial destructor is not-POD type  
  * Copy constructors   
    * Copying during initialization occurs when a new object is created as a copy of an old one   
      * Objects are passed to functions by value (instead of reference or pointer)  
      * Objects are returned from a function by value   
      * Explicitly   
    * Named the same as the class, has no return type   
    * Takes a reference (usually const) to its own type   
      * Reference points at the original object rather than a copy 

| class Polygon{   point \* points;   size\_t numPoints;public:   Polygon(size\_t n): points(new Point\[n\], numPoints(n) {}   //Copy constructor   Polygon(const Polygon & rhs) : points(new Point\[rhs.numPoints\]), numPoints(rhs.numPoints){      for (size\_t i=0; i \< numPoints; i++){         points\[i\] \= rhs.points\[i\];      }   }   //Assignment operator   Polygon & operator\=(const Polygon & rhs){      if (this \!= \&rhs){         Point \* temp \= new Point\[rhs.numPoints\];         for (size\_t i \= 0; i \< rhs.numPoints; i++){            Temp\[i\] \= rhs.points\[i\];         }         delete\[\] points;         numPoints \= rhs.numPoints;         points \= temp;      }      return \*this;    \~Polygon(){      delete\[\] points;   } }; |
| :---- |

    * Implicit copy constructors are provided   
      * Provided copy constructor performs as if it contains an initializer list that initializes every field the corresponding field in the argument  
    * May be trivial or non trivial   
  * Assignment Operator  
    * Form of copying that occurs during assignment  
    * To an already exciting and initialized object  
    * Three differences  
      * Assignment operator returns a value   
      * Operator begins by checking this \!= \&rhs (pointer comparison)  
      * Assignment operator must cleanup existing object before have new values copied into it  
  * Unnamed temporaries: values that are created as the result of an expression but given  a name   
  * Parameter Passing: passing an unnamed temporaries as a function parameter  
    * Compiler is allowed to optimize away the copy   
    * Generally preferable to take in const references rather than a copy of an object 

| int someFunction( const MyClass & something ) {...} |
| :---- |

    * No copying is involved  
    * Since its a const reference we can pass unnamed temporaries   
      * If the param is not const we would not be able to pass an unnamed temporary   
  * Return values  
    * Return value optimization   
      *   
  * Implicit Conversions  
    * In C++ any constructor that takes one argument is considered as a way to implicitly convert from its argument type to the type of class it resides in, unless that constructor is declared ***explicit***

| int someFunction(const MyClass & something){...}someFunction(MyClass(42));someFunction(42); //kindda fucking weird but it works //unless your class is like this  class MyClass{ // public:    explicit MyClass(int x) : someField(x) { … }    MyClass(const MyClass & rhs) : someField(rhs.someField){ … }    //other stuff here… }; |
| :---- |

    *   
* Virtual Memory  
  * Memory management capability that allows temporarily transferring data from RAM to disk   
  * Virtual address space is increased using active memory in RAM and inactive memory in hard disk   
  *    
* Static data(?)  
* Runtime vs Compile  
  * Phase distinction [**(\*)**](https://stackoverflow.com/questions/846103/runtime-vs-compile-time)   
    * Property of programming languages that observe a strict division between types and tems  
    * Most statically typed languages conform to the principle of phase distinction   
  * Different types of errors  
  * Compile-time   
    * Written code converted to executable  
    * Errors: syntax, type checking, compiler crashes   
  * Run-time  
    * Executable code being ran  
    * Errors: Division by zero, dereferencing a null pointer, running out of memory  
  * Static: anything that is created during compile time and stays fixed during runtime  
  * Dynamic: created and change during runtime  
  *   
  * *Compilers*  
    * *Check program statements for errors and report them*   
    * *Generate the machine instructions that carry out the instructions of the program*   
    * Declaration  
      * “program text” that provides information to the compiler  
      * *Allow for executable generation and error finding*  
    * *Executable statements*   
      *   Program statements that meant to specify operation to carry during runtime   
    * *Housekeeping **(\*)***  
      * *The procedure performed as you perform memory freeing actions*   
      * *Standard entry*   
      * *Exit routine*    
* Statically typed languages  
* [Smart Pointers](https://www.boost.org/doc/libs/1_62_0/libs/smart_ptr/smart_ptr.htm)  
  * Objects which store pointers to dynamically allocated (heap) objects   
  * Automatically delete the object pointed to at the appropriate time   
  * Useful for exceptions   
  * Keep track of dynamically allocated objects shared by multiple owners   
  * unique\_ptr   
    * Unique object ownership semantics  
    *   
  * shared\_ptr  
    * Shared object ownership semantics  
  * weak\_ptr  
    * Weak reference to an object managed by shared\_ptr  
  * 

# Pointer vs Reference

* Both  
  * Used to provide one variable provide access to another  
* Pointers   
  * Variable that holds memory address of another variable   
  * Needs to be dereferenced with \* operator to access the memory location it points to  
  * Pointer can be reassigned   
  * Pointer has it own memory address and size on the stack  
  * Can be assigned null values  
  * Can have pointers to pointers  
  * Pointers support arithmetic operations  
* References  
  * Alias, another name for an existing variable   
  * Stores the address of an object  
  * Constant pointer that automatically dereferenced   
  * Reference cannot be re-assigned and must be assigned at initialization  
  * Reference shares the same memory address but also takes up some space on the stack  
    * cout \<\< &(\&r); // to get the reference’s true address  
  * Cannot be assigned null values  
  * Offered a single level of indirection  
  * Reference arithmetic do not exist  
* When to use  
  * References  
    *  in function parameters and return types  
    * Referred over pointers whenever we dont need researing  
    *   
  * Pointers  
    * Pointer arithmetic or passing NULL pointer is needed   
    * Implementing data structures like linked lists, tree, etc 

# Scope

* Scope of a variable determines which region of a program can access it and also the lifespan of the variable   
* Scope resolution operator (::) is used to access the global variable if local and global variables are declared with the same name  
* Global variables  
  * Program scope: can be accessed everywhere and they are freed only when program execution ends  
  * Initialized automatically  
    * Variables of type int, float, or double is initialized to 0  
    * Char type variable is initialized to ‘\\0’   
    * Pointer types initialized to NULL   
* Local variables   
  * Accessed within the function only   
  * Destroyed as soon as the function ends  
  * function/block scope   
  * Not initialized by the system 

# Memory Segments

Refs: [1](https://www.learncpp.com/cpp-tutorial/79-the-stack-and-the-heap/), [2](https://www.geeksforgeeks.org/memory-layout-of-c-program/), [3](https://stackoverflow.com/questions/14588767/where-in-memory-are-my-variables-stored-in-c)

* Code Segment (text segment)   
  * Segment where the compiled program is located   
  * Typically read only   
* Bss segment (uninitialized data segment)   
  * Stands for (Basic Service Set)  
  * Where zero-initialized global and static variables are stored  
* Data segment (initialized data segment)   
  * Initialized global and static variables are stored  
* Heap   
  * Dynamically allocated variables are allocated from  
* Stack  
  * Function parameters, local variables, other function related information are stored

# Storage Classes

Refs: [tutorialspoint](https://www.tutorialspoint.com/cplusplus/cpp_storage_classes.htm), [geeksforgeeks](https://www.geeksforgeeks.org/c-mutable-keyword/)

* Storage class defines the scope and life-time of variables/functions   
* Five classes:   
  * Auto  
    * Default storage class for all local variable  
    * Can only be used within functions   
  * Register  
    * Local variables that should be stored in register instead of RAM  
    * Maximum size equal to reister size   
    * Cant have the unary & operator   
      * Does Not have memory location   
    * Should only be used for variables that require quick access (counter)   
  * Static   
    * Instructs compiler to keep a local variable in existence during the life-time of the program instead of creating and destroying  
    * Can be applied to global variables as well, allowing for the scope to be the entire file of declaration    
    * Stored in the data segment of the memory   
  * Extern  
    * Used to give reference of a global variable that is visible to ALL program files   
    * Cannot be initialized as all it does is point the variable name at a storage location previously defined  
    * Used in another file to give reference of defined variable or function  
    * Used to declare a global variable or function in another file   
  * Mutable  
    * Applied only to class object   
    * When it is required to modify one or more data members of class/struct through const function even though you don't the function to update other members of class/struct  
    * Used to allow a particular data member of const object to be modified   
    * Adding mutable to a variable allows a const pointer to change members   
    * When most members should const but some should be changed   
    * Data members declared as mutable can be changed even if they are a part of a const object    
    * Cannot use mutable with names declared as static const, or reference

# Namespaces

Refs: [microsoft](https://docs.microsoft.com/en-us/cpp/cpp/namespaces-cpp?view=vs-2019)

* Namespace is declarative region that provides a scope to the identifiers inside it  
* Used to organize code into logical groups and to prevent name collision when working with multiple libraries  
* All identifiers at namespace sope are visible to one another without qualification   
* Identifiers outside the namespace can access the members by using fully qualified name for each identifier (i.e, std::vector\<std::string\> vec;)  
  * Or using declaration for a single identifier (using std::string)  
  * Or using directive for all the identifiers in the namespace (using namespace std;)

| //namespace declarationnamespace ContosoData {   class ObjectManager {    public:         Void DoSomething(){}   };   void Func(ObjectManager){}}// fully qualified nameContosoData::ObjectManager mgr;mgr.DoSomething();ContosoData::Func(mgr);// using declaration to bring one identifier into scopeusing ContosoData::ObjectManager;ObjectManager mgr;mgr.DoSomething();// using directive to bring everything in the namespace into scope Using namespace ContosoData;ObjectManager mgr;mgr.DoSomething();Func(mgr); |
| :---- |

* using directives  
  * Allows all the names in a namespace to be used without the namespace-name as explicit qualifier   
  * Only bring the identifiers that you are using into the scope instead of all identifiers   
  * If local variable has the same namespace as namespace variable, the namespace variable is hidden   
  * It is an error to have a namespace variable with the same name as a global variable  
  * 

# Constants

Ref: [cplusplus](http://www.cplusplus.com/doc/tutorial/constants/)

* Variables with a fixed value  
* Literals  
  * Express particular values within the source code of a program.   
  * integer , floating-point, characters, strigns, boolean, pointers, and user-defined literals   
* Integer Numerals  
  * Numerical constants the identify integer values   
  * 

# Operators

Refs: [geeksforgeeks](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/), 

* Unary operator  
* Binary Operator   
  * Compound Assignment Operators  
  * Arithmetic Operators  
  * Relational Operator   
  * Logical Operator   
  * Bitwise Operators   
    * & (AND)  
      * Take two numbers as operands and does AND on every bit of two numbers   
      * Results is 1 if both bits are 1   
    * | (OR)  
      * Result is 1 if any of the two bits is 1   
    * ^ (XOR)  
      * Result is 1 if the two bits are different   
    * \<\< (left shift)  
      * Left shifts the bits of the first operand, the second operand decides the number of places to shift   
    * \>\> (right shift)  
      * Right shifts the bits of the first operand, the second operand decides the number of places to shift  
    * \~ (NOT)  
      * Inverts all bits of it   
* Ternary Operator  
* Pre and Post Increment/ Decrement Operations

# Input/Output Operators Overloading in C++

Refs: [tutorialspoint](https://www.tutorialspoint.com/cplusplus/input_output_operators_overloading.htm), [geeksforgeeks](https://www.geeksforgeeks.org/overloading-stream-insertion-operators-c/)

* Input and output built in data types using the stream extraction operator \>\>, stram insertion operator  
* \<\< and \>\> could be overloaded to perform iput and output for user defined types like an object  
*    
* streams  
  * cout object of ostream class   
  * cin object of istream class  
  * Must be overloaded as a global function   
  * To allow them to access private data members of class we must make the overload a friend

# Functions

* As the program executes the function call instruction the CPU stores the memory address of the instruction following the function call, copies the arguments of the function on the stack and finally transfers control to the specified function   
* CPU executes the function code store the function return value in a predefined memory location/register and returns control to the calling function   
* This becomes an overhead if function execution time is less than the switching time from the caller function to called function (callee)  

## Parameters

Refs: [stackoverflow\_default params](https://stackoverflow.com/questions/12903724/default-arguments-have-to-be-bound-at-compiled-time-why)

* Default parameter

## Inline function

Refs: [geeksforgeeks](https://www.geeksforgeeks.org/inline-functions-cpp/), [isocpp](https://isocpp.org/wiki/faq/inline-functions)

* Inline function reduce the function call overhead  
* Function that is expanded in line when it is called   
* As it is called the whole code is inserted at the point of the function call  
* Substitution is done at compile time, and this may increase the efficiency if it is small

| inline return\-type function-name(parameters){  //function code} |
| :---- |

* Inline is only a request to the compiler not a command  
  * Compilers may ignore the call when   
    * Function contains a loop   
    * Function contains static variables   
    * Function is recursive   
    * Function return type is other than void, and the return statement does not exist in function body   
    * Function contains switch or goto statement  
* Advantages  
  * No function call overhead  
  * Saves the overhead of push/pop variables on stack when the function is called  
  * Saves overhead of return call from a function   
  * May allow for context specific optimization on the body of the function   
  * May be useful for embedded systems because inline can yield less code than function call preamble and return  
* Disadvantages  
  * Consumes additional registers  
  * Grows the executable file, due to duplication of the same code   
  * Reduces instruction cache hit rate, reducing instruction fetch from cache memory to that of primary memory   
  * Increase compile time   
  * May not be useful for many embedded systems where size is more important than speed   
  * Might cause thrashing, via increasing size of the binary executable file causing the performace of the computer to degrade 

## Return 

### Void Return Type

Refs: [geeksforgeeks](https://www.geeksforgeeks.org/return-void-functions-c/), [**fsu**](http://www.cs.fsu.edu/~cop3014p/lectures/ch7/index.html)

* Void functions technically supposed to not return anything   
* However void function can   
  * just do return; (this is considered a good practice)  
  * return another void function 

| \#include \<iostream\> Using namespace std; void work(){    cout \<\< "the void function has returned a void () \\n";}void test(){    return work();}Int main(){    test();    return 0;}  |
| :---- |

  * Return a vod value ( return (void);  
  * 

# Classes

## Friend Class

Refs: [geeksforgeeks](https://www.geeksforgeeks.org/friend-class-function-cpp/)

* A friend class can access private and protected members of other classes in which it is declared as friend   
* 

# Inheritance

Refs: [programiz](https://www.programiz.com/cpp-programming/inheritance), [tutorialspoint](https://www.tutorialspoint.com/cplusplus/cpp_inheritance.htm)

* Allows users to create a derived class from a base class, such that the derived class inherits all the features from the base class and can have additional features   
* Lets you avoid a lot of code duplication  
* “Is a” statement: Derived class **is a** Base Class  
* Derived classes can be defined in the following way 

| //single class inheritance class derived-class: access-specifier base{};   // multiple inheritance class derived-class: access-specifier baseA, access-specifier baseB{}; //multilevel inheritance  class derived-derived-class: access-specifier derived-class{}; |
| :---- |

  * The access specifier is by default private but can be specified to be protected or public as well   
* Access Control and Inheritance   
  * Derived class can access all the non-private members of its base class   
    * Members of the base class that shouldnt be accessed by the parent class should be declared private   
  * Acess types can be summarized accoriding to who can acccess them   
    * Public   
      * Same class, derived class, outside classes   
    * Protected   
      * Same class, derived classes  
    * Private	  
      * Same class only   
  * Derived class inherits all base class methods unless they are	  
    * Constructors, destructors, and coy constructors of the base class  
    * Overloaded operators of the base class   
    * Friend functions of the base class   
* Types of Inheritance  
  * Public inheritance   
    * Public members of the base class become public member of the derive class, protected members remain proteced, private members are never accessible directly, but can be accessed through public and protected memebers   
  * Protected Inheritance  
    * Pbulic and protected members of the base class become protected members  
  * Private Inheritance  
    * Public and protected members of the base class become private members of the derived class   
* Multiple Inheritance   
  * A class can inherit from more than one class   
  *   
* Multilevel Inheritance  
  *    
* Hierarchical Inheritance

# Concurrency

* Multi-Threading  
  * Each thread has its own independent stack but all threads share heap   
* Process  
  * Running instance of a program   
  * Each process has its own stack heap, data segment, and code   
  * While it is possible to setup communication between processes usually processes do not influence each other states  
    * Via setting up shared memory spaces using explicit system calls   
  * Unique Process ID (PID) for each process   
  * Using multiple processes isnt a direct multiplier  
    * Load imbalance  
      * Spending some time waiting for the last few task to run while have no other task to be run   
    * Parallel task may contend for hardware resources   
      * Makes each task take longer   
  * **fork**   
    * System call that creates new processes  
    * Creates child process of the original process  
      * Child processes return 0 and child’s PID in the parent  
      * New processes id   
      * Resets some OS-level resource accounting  
    * Memory and file descriptors are copied   
      * Which is why child process cannot access parent’s process  
    * Can use fork to create multiple images without using execve to run them 

| while(\!exiting){  Request \* r \= getIncomingRequest();  pid\_t fork\_result \= fork(); // creates a two independent programs  if ( fork\_resut \== \-1 ){	//handle the error  }  else if {	handleRequest(r); // child process calls handleRequest	exit(EXIT\_SUCCESS); // then exits  }  else{	// do whatever else the parent needs to do       // these tasks are accomplished in parallel with the child 	// ....  }} |
| :---- |

    *   
  * **execve**  
    * System call that executes the appropriate task   
    * Replaces the program in the current running process with a newly loaded program  
    * Calling execve right after forking   
      * Second copy of the parent’s memory is destroyed and replaced with a memory image loaded from the requested binary   
  * **waitpid**  
    * System call that waits for the other processes to finish   
    * Allows for parent process to wait for one or more of its children to terminate   
* Threads   
  * When a parallel task needs to communicate a non-trivial amount they have   
  * Have separate stack and execution arrows but have the same heap, code segment and global data segment    
  * Share address space   
    * One thread can access data in other’s stack via pointers   
  * Process can have one or more threads within it   
  * pthreads : POSIX thread library   
    * \#include\<pthread.h\>  
    * To link \-lpthread at the end of the compilation command   
    * Must specify a function where new thread should start   
    * When the specified function returns the thread exits   
    * Function must have type void\* (\*) (void \*)  
      * Pointer to a function that takes void \* and returns void \*  
      *    
    * The fourth argument of pthread\_create takes in what to pass into this function as its argument when that function is called on the newly spawned thread  
  * Calling pthread\_create   
    * New stack is created that is independent from caller’s stack   
    * New stack is created with frames from the pthread library and a frame for the requested function  
    * Second arrow is created at the start of the function   
      * Making a system call to spawn a new thread   
  * Parallel Execution   
    * Multi threaded programs are non deterministic  
    *    
  * Thread Exit   
    * Returning  from the starting function or by calling pthread\_exit stops the run of the thread   
    * Return value must be available for another thread to retrieve   
    * pthread\_join   
      * Inputs:   
        * Pthread\_t: to identify the thread to wait for   
        * Pointer to void\* to fill in with the return value   
          * If you want the thread to just wait you can pass in NULL   
      * Waiting for threads to complete is called *joining*  
      * The execution arrow is blocked from advancing  until the joining thread terminates		  
      * Allows for thread resources to be release   
    * pthread\_detach   
      * Tells the pthread lib that the thread will never join any other thread and all the resources are released immediately   
    * Main thread is different from other threads and when it exits all of the threads inside it are terminated   
      * main thread is not called by the pthread lib  
  * Synchronization  
    * Most of the time threads must wait before performing specific operations   
    * Data Races   
      * Multiple threads are accessing the same data and the specific order in which they advance effects the results   
    * Critical section   
      * Region  of program that must be executed by one thread at a time  
    * Mutexes (Locks) (mutual exclusion lock)  
      * Guards critical sections   
      * Two states: lock(acquire) and unlock(release)  
      * Locking an already locked mutex block the execution until the mutex is unlocked by another thread  
      * Unlocked mutex is locked   
      * A thread can unlock the mutex it locks   
      * One mutex per one piece of data  
      * pthread mutex t \= ptherad\_mutex\_intit (...);  
        * Pointer to the mutex variable and attribute of the mutex (or NULL for default)  
        * Initialized to unlocked state  
      * pthread\_mutex\_lock & pthread\_mutex\_unlock  
        * Take pointer to the mutex  
      * pthread\_mutex\_destroy to clean up mutex 

| pthreard\_mutex\_tvoid \* incrThread(void \* varg){	Int \* arg \= varg;	for (int i \= 0; i \< 5000; i++){		pthread\_mutex\_lock(\&lock);		Int temp \= \*arg;		temp++;		\*arg \= temp;		pthread\_mutex\_unlock(\&lock);}return NULL;}int main(void){	int x \= 0;	pthread\_t thr;	pthread\_mutex\_init(\&lock, NULL);	pthread\_create(\&thr, NULL, incrThread, \&x);	incrThread(\&x);	pthread\_join(thr, NULL);	pthread\_mutex\_destroy(\&lock);	printf("%d\\n",x);	return EXIT\_SUCCESS;} |
| :---- |

      * Mutex have high overhead   
        * May require mutex data from the other core and wait for it to be sent   
      * Contended mutexs are the ones that many threads are trying to acquire at once  
    * **Locking Granularity**   
      * Size of the data protected by a single lock  
    * Reader/Writer Locks  
      * Special kind of mutex that a thread can lock for reading or lock for writing   
      * Multiple thread can access the data to read it but only on thread is able to write to it   
    * Deadlocks  
      * One or more threads are waiting for a mutex that will never be unlocked   
      * What helps:  
        * Acquiring locks in the same order  
        * Usual practice to acquire lock in ascending order /  
    * Condition Variables   
      * A synchronization construct that supports the operations wait, signal, and broadcast  
      * Help to avoid deadlocks  
      * **Wait:** blocks the thread until some other thread does **signal/broadcast**  
        * Releases the mutex in such a way that there is no race with the thread starting to wait   
      * **Signal:** unblocks the one thread that is waiting   
      * **Broadcast:** unblocks all threads that are waiting 

| WorkItem \* getWorkd(Queue \* myQueue){   pthread\_mutex\_lock(\&myQueue-\>lock); //locks mutex   while(myQueue-\>isEmpty()){      pthread\_cond\_wait(\&myQueue-\>cv, \&myQueue-\>lock); // waits for the signal, checking every loop   }   WorkItem \* answer \= myQueue-\>dequeue(); //does its operation    pthread\_mutex\_unlock(\&myQueue-\>lock); // unlocks mutex   Return answer;} Void addWork(Queue \* myQueue, WorkItem \* w){    pthread\_mutex\_lock(\&myQueue-\>lock); //locks mutex    myQueue-\>enqueue(w); // does operation    pthread\_cond\_signal (\&myQueue-\>cv); //sends signal     pthread\_mutex\_unlock(\&myQueue-\>lock); //unlocks mutex } |
| :---- |
| pthread\_mutex\_broadcast(\&myQueue-\>cv); //broadcasting instead of signal  |

      *  Must wrap the wait operation in a while loop that rechecks the condition   
    * Barriers  
      * Synchronization construct  
      * Requires a certain number of threads to reach it before proceeds  
      * pthread\_barrrier\_init  
        * Identifies how many threads will participate  
      * pthread\_barrier\_wait  
        * After the the threads perform some computation they must wait on the barrier   
        * Returns a value that distinguishes one thread from all of the others  
  * Atomic Primitives  
    * Reading and writing data atomically   
      * In a way that the hardware guarantees that there are no races between read and write   
    * Test-and-set (TAS)  
      * Atomically tests the value in a memory location and set it to 1 

| int test\_and\_set(int \* ptr){ // essentially what TAS does but it guarantees that the following two lines are atomic    int x \= \*ptr;      \*ptr \= 1;   return x; } |
| :---- |

      * Test-and-set-and-set  
        * Test the lock with a non-atomic operation  
        * Use the atomic operator only when there is a possibility of acquiring the lock   
    * Compare-and-Swap (CAS)  
      * Compares the value in a memory location to an expected value  
      * If the memory matches the value is updated with new value  
        * If it doesn't the update isn't made  
    * Load-linked/Store-conditional  
      * “Instruction sets based on the idea of having only simple operations”  
      * Load-linked and store-conditional combined together to create atomically behaved operations  
      * LL instruction reads a value from memory and asks the hardware to watch that memory address  
        * If another thread uses that memory location the hardware will remember   
      * Store-conditional instruction writes to that memory location only if it has not been changed (store-conditional succeeds)  
    * Atomic Increment  
      * Atomically reads a value from memory, adds 1 and stores it back to the same memory location   
      * Much more efficient if only for element incementation   
  * Lock Free Data Structure **(\*)**  
    * Data structures that are capable of operating correctly when multiple threads access them at the same time and do not require locks to do so   
    * Rely on atomic primitives (CAS mostly)   
    * HOWEVER   
      * New operator most likely implemented with lock internally   
        * When allocating memory it locks the free blocks of the heap   
      * Some pool friendly allocation libraries allow for no lock allocation by keeping blocks of heap memory allocated for each heap   
  * Parallel Programming Idioms  
    * Common ways in which data is parallized  
    * Data Parallelism  
      * Different data elements accessed in an independent fashion  
      * Can be exploited with vector instructions  
        * Instruction that are performed on multiple pieces of data at the same time  
    * Pipeline parallelism  
      * Divide the program into a series of tasks which are carried out in an assembly line like fashion   
      * Different threads for each stage of the pipeline  
      * Pipeline must be balanced to ensure that the throughput throughout is the same  
    * Task Parallelism  
      * Task spawn more task and wait for their child tasks’ results  
      * Divide and conquer algorithms   
        * Divide spawns tasks   
        * Conquer waits for children to finish   
      * Load balancing   
        * Making sure that one thread does not finish its work first and sit idle   
        * Work stealing   
          * A thread with an empty queue steals from a thread with a bigger queue   
    * Amdahl’s Law  
      * Considering how much of the program is serial and how much parallel  
      * Formula for maximum theoretical speedup of a task given a certain amount of threads   
      * S, time for serial portion, P time for parallel portion, N number of threads  
      * Speedup(N) \= ( S \+ P ) / ( S \+ P/N )  
      * Make the common case fast   
    *   
  * Std::thread	  
  * Memory Consistency Model (atomic primitives)

# Templates

Refs: [All of Programming](https://play.google.com/books/reader?id=-zViCgAAQBAJ&pg=GBS.PA318), [Effective C++](https://doc.lagout.org/programmation/C/Addison.Wesley.Effective.CPP.3rd.Edition.May.2005.pdf) 

* Similar operations on different data types in a similar fashion  
* Parametric Polymorphism   
  * C++ but not C  
  * Ability to operate on multiple types reduces code duplication by allowing the same piece of code to be resued acroos different types  
* Templated Functions   
  * **template \<typename T\>**   
    * \<\>: template parameters  
    * As the scope of the entire function  
    * Template \<typename T, typename S, int N\>   
      * Allows for multiple parameters, as well as normal type parameters  
  * Templated function itself is not actually a function, and must be instantiated with the template to create an actual function   
  * Calling a function and instantiating a template are different 

int \* m1 \= arrMax\<int\>(myIntArray, nIntElements);  
string \* m2 \= arrMax\<string\>(myStringArray, nStringElements);  
int x \= someFunction\<int \*, double, 42\>(m1, 3.14); 

* As the template is instantiated the copiler creates a **template specialization**   
  * Function derived from template for particular vales of its parameters  
* Templated Classes  
  * Has template parameters which can be either types or values  
  * Scope is the entire class declaration

template\<typename T\>  
class Array{  
private:  
	T \* data;  
	Size\_t size;  
public:  
	array(): data(NULL), size(0){}  
	…  
}; 

* Whenever the templated class is instantiated the compiler creates a specialization of the template   
  * Different instantiation with different parameters are different classes  
    * And are not interchangeble  
* Templates as Template Parameters  
  *  

template\<typename T, template\<typename\> class Container\>  
class Something{  
private:  
Container\<T\> data;  
// other code in the rest of the class...  
 \];

* Another level of abstraction  
* Template Rules  
  * Template Definitions must be “Visible at Instantiations  
    * Implementation of templated function or class must be visible to the compiler at the point where the template is instantiated   
      * Compiler cannot just generate a call to it an find it an object file  
    * Templated function/class are not actually those things, just a reciepy to create specialization when the template is instantiated   
    * Compiler needs a definition in order to create the actual specialization   
  * Template Arguments Must Be Compile-Time Constatnts  
    * Compile-time constants   
      * Compiler must be able to directly evaluate the expression to a constant   
    * Compiler must create a specialization for the argument values fgiven, when the compiler cannot figure out the exact value of the parameter then it has no idea what specializations of the template it should create and this cannot compile the code  
  * Templates are only type check when specialized   
    * You can write a template that can only legaly be instantiated with some types but not others   
    * When the compiler specializes the function  
      * The first time the function encounter an instatniation of the templated function with a particular set of arguments it type checks the function  
    * For a class   
      * Whenever  an instance of the class is created the compiler specializes the part of the class definition that is required to make the object;s in memory representation   
        * The fields as well as virtual methods   
      * The normal methods do not actually affect the in-memory representation of an instance of the object as they are not placed in the object but rather the code segmentt (\*)  
      * The non virtual method of a teplated class are only specialized when corresponding cmethod is sed although this piece by piece specialization may seem a bit odd it actually proves useful in the way the C++ templates are used  
  * Multiple Close Brackets Must be seperated by whitespace  
    * Error otherwise 

std::vector\<strd::pair\<int, std::string\> \> myVector; 

* Dependent Type names require keyword typename  
  * T::x, Something\<T\>::x   
    * X is a dependent name  
    * Whenever a dependent name for a type is used typename keyword must be explicitly provided 

 template\<typename T\>  
class Something{   
private:   
	typename T::t oneField;  
	typename anotherTempate\<T\>::x twoField;  
public:   
	typename T::t someFunction(typename T::t x){  
		Typename T::t someVar;  
		//some code  
	}  
};

* You can provide an explicit specialization  
  * Providing secific behavior for particular values of the template arguments  
    * More efficient implementation of the exact same behavior as the primary template   
    * Explicit specialization may be either partial or complete  
      * Partial specalization with respect to some of the parametres leaving the resulting specalization parameterized over the others  
      * Complete specialize all of the parameters  
  * Template Parameters for Function (But not classes) may be inferred   
    * Using templated function you may omit angle brackets and template arguments in cases where the compiler can infer them  
      * Not recommended   
        * Readability is decreased   
        * Compiler may infer different from the expected  
* The Standard Template Library  
  * std::vector\<typename T\>   
    * \#include \<vector\>  
  * std::pair\<typename T, typename S\>  
  * Iterators   
    * Container class (classes that hold other data)  
    * Resolves the conflict between good abstraction and high preformance   
    * Class that encapsuulates the state of the internal traversal while privding an implementation-independent interface to external code  
      * Tracks where the traversal is in whatever fashion is efficie for the data structure it belongs to but gives a simple interface to other code   
    *  Postfix increment requires the operator to make a copy of the original object, perform the increment then return the copy of the object   
      * Prefix increment avoids the unncessary copies and destructions   
    * Container should be const as we do not modify its elements (.)  
    * T::const\_iterator for provides const reference  
    * Whenever a modification occurs an iterator may be invalidated by that modfication   
  * Algorithms from the STL  
*  Understanding implicit interfaces and compile time polymorphism   
  * Explicit interface: one explicitly visible in the source code   
    * Consists of function signatures:   
      * Names  
      * Parameter types   
      * Return types   
  * Implicit interface: set of expressions that must be valid in ordewer for the template to compile   
    * Not based on function signiture but on the valid expressions   
  * Since templates are instantiated at compile time they are compile time polymorphism   
  * Both explicit and implicit interfaces are checked during compilation time   
  *  Classes vs Templates   
    * classes : explicit interfaces, centered on function signitures, polymorphism occusrs at runtime  through bvirtual functionas   
    * templates: implicit interfaces, centered on valid expressions, polymorphism occurs at compilation through template instantiation and function overloading resolution   
* Two types of typename 

template\<class T\> class Widget;  
template\<typename T\> class Widget; 

* From C++ point of view class and typename mean exactly the same thing when declaring a template parameter   
  * C++ doesnt alwayus view **class** and **typename** as equivalent   
  * Dependent names   
    * Names in a template that are dependent on a template parameter   
    * Nested dependent names are those inside a class   
  * Non-dependent names  
    * Names that do not depend on any template parameter  
  * C++ has a rule to resolve ambiguity when it comes to differentiating between, for example, static data members and types   
    * If a praser encounters a nested dependent name in a template it assumes that the name is not a type unless you tell it otherwise 

template\<typename C\>  
void print2nd(const C& container){  
	C::const\_iterator iter(container.begin()); //invalid code   
	…  
}  
template\<typename C\>  
void print2nd(const C& container){  
	typename C::const\_iterator iter(container.begin()); //invalid code   
	…  
}

* Typename should be used to identify only nested dependent type names  
  * Exception to this rule is that typename must not precede nested dependet type names in a list of base classes   
  * Typedef can be used to shorten the typename typing  
    * Common convention is for the typedef name to be the smae as the traits member names, so such a local typedef 

template void workWithIterator(IterT iter) {  
typedef typename std::iterator\_traits::value\_type value\_type;  
 value\_type temp(\*iter);  
 ...   
}

* When delcaring template parameters class and typename are interchangeable   
  * Use typename to identify nested dependent type names except in base class list or as base class identifier in a member initialization list   
* How to access names in templetized base classes

# Smart Pointer

Refs: Effective Modern C++ (book)  

* Regular pointer problems  
  *  Declaration doesnt specify single object or array   
  * Declaration doesnt specify the destruction that needs to occur  
  * No information on how to destroy the object  
    * Undefined results if you try to use delete vs delete\[\]   
  * May be difficult to ensure a single destruction of the object  
    * Different paths may not destroy the object creating memory leaks or destroy it more than once, leading to undefined behaviour   
  * No way to determine if the pointer is dangling   
* Smart are wrappers around raw pointers that act much like raw pointers, but avoid many pitfalls   
  * Far fewer opportunities for errors  
* 4 types of smart pointers help manage the life times of dynamically allocated objects  
  * Avoid resource memory leaks by ensuring that such objects are destroyed in an appropriate manner at the appropriate time   
  * Including in the event of exceptions  
* **std::auto\_ptr**  
  * Depreciated from C++98   
  * Late on became **std::unique\_ptr** in C++11  
  * Couldnt utilize move semantics  **(\*)**  
  * Employed copy operators for moves which led to surprising code  
    * Copying **std::auto\_ptr** sets it to null  
  *  and weird usage restrictions  
    * Cannot store the **std::auto\_ptr** in containers   
* **std::unique\_ptr**   
  * Does everything that **std::auto\_ptr** does \+ some other stuff  
  * May not compile with C++98 compilers  
  * Exclusive owenrship resource managment  
    * A non-null **std::unique\_ptr** always own what it points to  
    * Moving **std::unique\_ptr** transfers ownership from the source pointer to destintion pointer and setting the source pointer to null   
    * Copying **std::unique\_ptr** isnt allowed, because this would essentially break the exclusive ownership semantic   
    * Move-only type   
    * Upon destruction non-null **std::unique\_ptr** destroys its resource   
      * Applying delete to the raw pointer inside the **std::unique\_ptr**  
  * Same size asa raw pointers  
  * For more operation, as well as dereferencing, they execute exactly the same instructions   
  * Common use   
    * Factory function return type for objects in a heirarchy   
  * During exception occurances the **std::unique\_ptr** and their managed resources are destroyed  
    * By default the destructors is **delete**  
    * **std::unique\_ptr** can be configure to use custom deletes

| auto delInvmt \= \[\](Investment\* pInvestment) // custom                { // deleter                   makeLogEntry(pInvestment); // (a lambda                  delete  pInvestment; // expression)               };template\<typename... Ts\> // revisedstd::unique\_ptr\<Investment, decltype(delInvmt)\> // return typemakeInvestment(Ts&&... params){std::unique\_ptr\<Investment, decltype(delInvmt)\> // ptr to bepInv(nullptr, delInvmt); // returned |
| :---- |

  *   
* **std::shared\_ptr**  
  *   
* **std::weak\_ptr**   
* 