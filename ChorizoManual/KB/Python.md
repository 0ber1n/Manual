
///////////Floating////////////

~To format the decimal points, this is the syntax for variable myfloat

print('{:.2f}'.format(myFloat))


/////////////////////////////////////

|Compound operator|Expression with compound operator|Equivalent expression|
|---|---|---|
|Addition assignment|`age += 1`|`age = age + 1`|
|Subtraction assignment|`age -= 1`|`age = age - 1`|
|Multiplication assignment|`age *= 1`|`age = age * 1`|
|Division assignment|`age /= 1`|`age = age / 1`|
|Modulo (operator further discussed elsewhere) assignment|`age %= 1`|`age = age % 1`|
//////////////////////////////////////////

|Operation|Description|
|---|---|
|len(list)|Find the length of the list.|
|list1 + list2|Produce a new list by concatenating list2 to the end of list1.|
|min(list)|Find the element in list with the smallest value.|
|max(list)|Find the element in list with the largest value.|
|sum(list)|Find the sum of all elements of a list (numbers only).|
|list.index(val)|Find the index of the first element in list whose value matches val.|
|list.count(val)|Count the number of occurrences of the value val in list.|
///////////////////////////////////////

Recall that `ord()` converts a 1-character string into an integer, and `chr()` converts an integer into a character. Thus, `chr(ord('a') + 1)` results in 'b'.