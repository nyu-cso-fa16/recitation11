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


