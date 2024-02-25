# Custom Script and Shared Object

## <mark style="color:red;">Write your custom script:</mark>&#x20;

Create your custom script (e.g., a shell script) that contains the functionality you want to encapsulate:

```bash
#!/bin/bash

echo "Running custom script..."
echo "Hello, world!"
```

## <mark style="color:red;">Create a C wrapper function:</mark>&#x20;

Write a C function that will serve as a wrapper for executing your script. \
This function will use the system() function from the C standard library to execute the script. \
Create a C source file (e.g., wrapper.c) with the following content:

```bash
// wrapper.c

#include <stdlib.h>

void run_custom_script() {
    system("./custom_script.sh");
}
```

## <mark style="color:red;">Compile the source code:</mark>

Use GCC to compile the source code into a shared object. \
Use the <mark style="color:yellow;">`-shared`</mark> flag to specify that you want to create a shared object, and <mark style="color:yellow;">`-fPIC`</mark> to generate position-independent code, which is required for shared objects. \
This command compiles wrapper.c into a shared object named libcustom.so.:\
<mark style="color:yellow;">`gcc -shared -fPIC -o libcustom.so wrapper.c`</mark>

## <mark style="color:red;">Use the shared object:</mark>&#x20;

Once you've created the shared object, you can use it in other programs to execute your custom script. \
You can link it with other programs or dynamically load it at runtime using tools like dlopen in your C/C++ programs. \
For example, you can create a simple C program that uses the shared object:

{% code lineNumbers="true" %}
```bash
// main.c

#include <stdio.h>
#include <dlfcn.h>

int main() {
    void *handle = dlopen("./libcustom.so", RTLD_LAZY);
    if (!handle) {
        fprintf(stderr, "Error: %s\n", dlerror());
        return 1;
    }

    void (*run_custom_script)() = dlsym(handle, "run_custom_script");
    if (!run_custom_script) {
        fprintf(stderr, "Error: %s\n", dlerror());
        dlclose(handle);
        return 1;
    }

    run_custom_script();

    dlclose(handle);
    return 0;
}
```
{% endcode %}

Compile main.c and link it with libcustom.so:

<mark style="color:yellow;">`gcc -o main main.c -ldl`</mark>

Now, when you run the main program, it will execute the custom script encapsulated within the shared object libcustom.so.
