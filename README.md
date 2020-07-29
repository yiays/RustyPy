# RustyPy
> RustyPy is a codename for this work-in-progress language project.

We intend to create a language that compiles to Rust, abstracting away
some of the complexities of Rust for rapid prototyping by adopting language
features from Python, C# and some original ideas of our own.

RustyPy is designed specifically for writing modern terminal applications,
the standard library will include support for parameters in stdin and
extended libraries will include additional features like grid layout,
padding, and newline spanning.

# Features

## Native stdin and stdout support

> RustyPy supports templating and processing command-line arguments
> within the standard library.

```py
./fib
  -h,--help<bool> "Shows this list."
  -v,--verbose<bool> "Output extra debug information while running."
  file "The file to write fibonacci numbers to."
  n<int>* "The number to find fibonacci numbers for."

# The above lines can be used at the start of the main file to specify the
# schema for stdin.

out.template = "{}\n" # Template for out can be changed

# The schema you've created can be represented as a string, which looks like
# a help doc.
out(str(in.schema))
"""
Usage: fib file

Details:
  Parameter       Type      Description
  =========       ====      ===========
  -h,--help                 Shows this list.
  -v,--verbose    boolean   Output extra debug information while running. Defaults to false.
  file                      The file to write fibonacci numbers to. Required.
"""

if (in.verbose){
  out("Called by command "+str(in)) # in as a str is the entire command
  in.map(param: str){
    out(param)
  }
}
```

## Anonymous callback functions

> In place of lambdas/anonymous functions, RustyPy implements a
> prettier callback syntax, this makes it possible to write functions
> that look like native language features, like `if`, `while` and `for`.

```py
# Defining a custom for function, the callback function is 'callback'.
null for (iterable: iterable) > callback {
  int i = 0;
  while(i < iterable.length){
    callback(iterable[i++]);
  }
}
# Calling this custom for function
for(i in range(15)){
  out('fizz' if(i%3==0) + 'buzz' if(i%5==0) + str(i) if(i%3>0 and i%5>0));
}
```

# Examples

## Fibonacci numbers

```py
int fib (n: int) {
  if (n < 2) {
    return(n);
  }
  else {
    return(fib(n-1)+fib(n-2));
  }
}
```