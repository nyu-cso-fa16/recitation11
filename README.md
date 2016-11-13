Computer Systems Organization: Recitation 11
==========

Exercise -- Symbol Table
-----

Consider the following version of the swap.c function that counts the number of times it has been called:

```
	extern int buf[];

	int* bufp0 = &buf[0];
	static int* bufp1;

	static void incr()
	{
		static int count = 0;
		count++;
	}

	void swap()
	{
		int temp;

		incr();
		bufp1 = &buf[1];
		temp = *bufp0;

		*bufp0 = *bufp1;
		*bufp1 = temp
	}

```

For each symbol that is defined and referenced in swap.o, indicate if it will have a symbol table entry in the .symtab section in module swap.o. If so, indicate the module that defines the symbol (swap.o or main.o), the symbol type (local, global, or extern) and the section (.text, .data, or .bss) it occupies in that module.


|     Symbol    | swap.o.symtab entry? | Symbol type | Module where defined | Section |
| :-----------: | :------------------: | :----------:| :------------------: | :-----: |
| buf           | 					   | 			 | 						|		  |
| bufp0         | 					   | 			 | 						|		  |
| bufp1         |					   | 			 | 						|		  |
| swap          | 					   | 			 | 						|		  |
| temp          | 					   | 			 | 						|		  |
| incr          | 					   | 			 | 						|		  |
| count         | 					   | 			 | 						|		  |

Fill the table above.

Exercise 2: Linking
-----

The `list.c` file in this directory implements a simple linked list. Compile this file into an object file and don't forget to include `-std=gnu99` flag (see Tutorial 8 for a review on compiling). Explain the errors produced. Fix them to produce the object file `list.o`.

Compile the `main.c` file included in this directory (also with the `-std=gnu99` flag) into an object file. Explain the errors produced. Fix them to produce the object file `main.o`.

Then, link the two object files into an executable (using `gcc`) to create the binary executable `linkedlist` (that you can run by typing `./linkedlist`).

Among the collection of names in `list.c` (as shown below), which are linker symbols and which are not? Which linker symbols are defined in `list.c` and which ones are not?
* `head`
* `n_inserts`
* `n_deletes`
* `insert`
* `prev`
* `curr`
* `malloc`
* `delete`
* `free`
* `find`

After you've answered the above question using sheer brainpower, let's find out the actual answer using the UNIX tool called `nm`. Run `nm list.o`. Read the man pages of `nm` (type `man nm`). And explain the nm output.  What are the symbols defined? What are the ones undefined? Then, run `nm main.o` and explain its output as well.

Lastly, run `nm ./linkedlist`. Which previously undefined symbols have now become defined? What are the remaining undefined symbols? What do these remaining undefined symbols correspond to?

### Linker and Shared library

We can examine the shared library (as in, the library that you included with `#include <stdlib.h>`) to be loaded with `./linkedlist` using the UNIX tool `ldd` (do `man ldd`). Type `ldd ./linkedlist` and find out the pathname of the shared library file that correspond to C standard library.

Now, let's examine the symbols defined in the C library to see if the remaining undefined symbols of  `./linkedlist` can indeed be found there. Type `nm -D <filename>` to list dynamic symbols. Did you find what you are looking for?

### Programming errors in the linking process

Now let's turn our attention to the actual output of `./linkedlist`. The program inserts 100 linked list nodes and then deletes half of them. Explain why the output statistics are so out of whack. Fix the errors.