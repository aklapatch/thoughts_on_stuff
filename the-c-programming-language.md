# My thoughts on the C programming language
I use C at work, and it's the language I'm the most familiar with.
- C was a great language, but it's age is apparent, and I doubt C will improve much since it's development is being driven by a committee. I've seen what a committee is doing to C++ (making it very complex), and I'm not a fan.
- Header files are a hack, but also a really good idea.
    - Why they're a hack
        - You could have had a proper import syntax, instead of including the file directly. I'm fairly sure this existed in programming languages before C came around.
        - IMO, it would be better to store the function declaration in the object file instead of having to duplicate the work of declaring the function again. That would make linking much more complex, but that's why it's a hack. It was an easy way to avoid making linking more complicated.
    - Why they're a good idea.
        - You can use header files to replace object files, since they are just included directly.
        - That means you could not event have a separate linking step. You can omit object files from the command link invocation altogether.
        - I wish header-only libraries were the only type of libraries, while source code obfuscation is useful, the build process becomes so much simpler if the library only needs an include statement. Builds could be faster, optimizations could be better.

- Assuming a function's return type is an `int` is a really bad idea. I'm usually using `stdint.h`, and I almost never return `int` from a function anymore. C should just error out instead of assuming a return type.

- C's greatest virtue is letting you see the memory layout of your data. Structs obey your wishes, and the language does nothing you don't tell it to, and hides nothing from you (e.g. virtual functions, operator overloading).

- Function pointers are underappreciated in C. You can get pretty far using them, and you still get some compile time safety from them. The syntax is really difficult to get the hang of though.
- Gotos are actually pretty useful when you don't have a native `defer` statement.
- `stdint.h` is great. I understand that having a `int` that is not connected to a specific size makes sense when you don't want to re-write code, but guaranteeing the size of a size of memory is far more important IMO.

- `NULL` is a big mistake. We all know that. AFAIK, the real problems with it are that any pointer type can be `NULL`, (so you always have to check if a pointer is valid) and that `NULL` is 0.

- `stdint.h` and `stdbool.h` should be included in the language by default.

- I think C is used so much because it was a simple language. C was well suited to writing low-level components such as kernels, operating systems, and low-level tools. I think it would still be feasible for me to (eventually) write a C compiler in assembly, whereas I don't think I could write a C++ compiler in C, much less assembly.
- C seemed to be the best fit for low-level components when it was made. That may be why it's so prolific. C++ doesn't work super well for embedded programming IMO because of exceptions and poor control of the heap. Rust binaries can be big. Zig is pretty good, but Zig is build on top of the LLVM stack, which means that until they get their self-hosting compiler together (and implement a lot of LLVM's functionality), they won't be able to get away from C++.

- I'm not sure C can be replaced. Anything that relies on C++ inherits C's legacy, and many new languages use LLVM (written in C++) to get up and running. I think to truly replace C, someone may have to write a compiler or interpreter for a new programming language in assembly. IMO, to replace C, you can't depend on it. Once you're up and running on one platform, you can cross-compile to another. You'll still need to retain C compatability to use libraries though.

- C is a victim of it's own success. It is hard to change it for the better because it may break old programs or workflows.
