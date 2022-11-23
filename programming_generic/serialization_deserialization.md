### What is serialization and de-serialization?
The method of converting a programming language objects to a format that can be used to store or transport over network is called serialization and the process of converting back this formatted data to objects is called deserialization. 

For example:   
If we have to store int 1 and send it over network, this can be done without any special process. As 1 can be written to a file and the file can be send. But what if we need to send a nested object containing different object types. For this purpose we would need an add-on.

Json being the universal file format that most of the languages understand and widely used. Though, json is limited to data certain data types and also don't support user defined objects like, a class build in python. For python pickle is the default serialization format. 