This fork aims to implement template argument deduction for non-terminal function parameter packs.

##The changes consist of:
###Amended rules for partial ordering
Before partial ordering is performed, function parameter packs are replaced by N invented template parameters, where N is the size the
pack would have during the function template instantiation

###Amended rules for function parameter packs
Instead of swallowing all the remaining arguments, function parameter packs are only deduced to include the necessary number of 
arguments for the function call to be valid.

## Code that currently compiles is

```cpp
template <class A, class B, class... Cs>
void foo (A a, Cs... cs, B b) {
  cout << "first";
  
template <class A, class B, class... Cs>
void foo (A a, int i, Cs... cs, B b) {
  cout << "second";
}

foo(1, 2, 3); // calls second
```

```cpp
template <class A, class B>
void foo (A a, B b){
  std::cout << "first" << std::endl;
}
template <class A, class... Bs>
void foo (A a, Bs*... bs){
  std::cout << "second" << std::endl;
}

foo (1, (int*)0); //calls second
```
