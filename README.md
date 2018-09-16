# Simple File System

Algorithms and Data Structures - Politecnico di Milano, 2017

## Overview

A simple simulated file system structure that works totally in RAM.  
It uses a tree structure to store directory contents, maintaining the file system structure.  
    
Tree nodes (resources) con be files or directories.  
Both have a name. Files can only be inserted as tree leaves, directories can also appear as intermediate nodes.  
Only files con contain data, represented as a string with a maximum length of 255 characters.  
The root of the tree is the root directory and each directory can have a maximum of 1024 sons.  
Resources paths follow the Unix syntax: the path is a sequence of names of resources, from the root to the requested file or directory. Each name is separed with `/` (es: `/dir/dir2/file0`).  
Resources names are alphanumeric strings with a maximum length of 255 characters and the maximum tree height (and so the maximum path length) is 255 too.

## Input and Output
The file system structure can distinguish among 8 different commands:
- `create <path>`: creates an empty file, without any associated data. The output will be `ok` if the creation succedes, `no` otherwise (es: if already exists a file with the same name in the specified path).
- `create_dir <path>`: creates an empty directory, without any son. The file system answers with `ok` if the directory has been correctly created, `no` otherwise.
- `read <path>`: reads the content of a file printing the word `contenuto` and the actual file content. The word `no` will be printed if the file doesn't exist.
- `write <path> <content>`: writes the string in the specified file printing `ok` followed by the number of bytes written. If the file doesn't exist, the output will be `no`.
- `delete <path>`: deletes a resource giving `ok` as output. A resource can be deleted only if it hasn't any son. The output will be `no` if trying to delete a non-existing resource or a directory containing at least one resource.
- `delete_r <path>`: recursively deletes a resource and all its descendants. It will print `no` if the specified resource doesn't exist, `ok` otherwise.
- `find <name>`: searches every resource having the specified name in the file system. The path of all the resources that the function encounters will be printed out, in lexicographic order. The output will be `no` if no resource with the specified name has been found.
- `exit`: ends the file system execution.

## Temporal Complexity
The project required a maximum complexity to execute each input command given to the file system structure.  
Indicating with `L` the length of a path, with `D` the total number if resources in the file system, with `Dpath` the number of sons of the specified resource, with `f` the number of resources found by the `find` command and with `contentLength` the length in bytes of the content of the specified file, required complexities are:  

|   command  |       complexity        |  
|------------|-------------------------|
| create     |  *O*(L)                 |
| create_dir |  *O*(L)                 |
| read       |  *O*(L + contentLength) |
| write      |  *O*(L + contentLength) |
| delete     |  *O*(L)                 |
| delete_r   |  *O*(Dpath)             |
| find       |  *O*(D + f<sup>2</sup>) |
