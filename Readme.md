The plugin is still in an experimental state. 
It is not very user friendly (lack of good error messages) and still contains bugs. 
But is useable enough to "translate" a large chunck of standard library. 

Compilation 
===========

The plugin currently works on a branch of coq (hopefully, in the future, it will also work on a stable official release). 
The easy (and long) way to test the plugin is to follow the following steps:
* Create a fresh directory and move into it:
    mkdir testplugin && cd testplugin 

* Retrieve my branch of coq and compile it (and go take a coffee, or may be 5 coffees):
    git clone https://github.com/mlasson/coq.git
    cd coq
    ./configure -local 
    make -j 4 
    cd ..

* Retrieve the plugin and compile it:
    git clone https://github.com/mlasson/paramcoq.git
    cd paramcoq 
    make

To test the plugin:
    cd test-suite
    make ide

It will compile Parametricity.vo which loads the plugin and contains a translation of the initial modules. 
Then, it launches coq-ide with some simple examples. 

Available commands
==================

The default arity is 2. 
The default name is automatically generated when translating a constant (otherwise you need to provide it). 

- Translate *term* [as *name*] [arity *n*]. 

Define a new constant named *name* obtained by computing the parametricity translation of *term*. 

- Translate Inductive *inductive* [as *name*] [arity *n*].

Declare a new inductive type named *name* from the translation of *inductive*. 

- Translate Module *modulepath*.

Recursively translate everything in a module. 

- Realizer *constant or variable* [as *name*] [arity *n*] := *term*.

Declare *term* to be the translation of a constant. 
Useful to translate terms containing section variables, or axioms. 

Note that all that both translating a term or module may lead to proof obligations (for some fixpoints and opaque terms if you did not import ProofIrrelevence).  