# TinyRabbit

TinyRabbit Initial Access Agent

## What is?

TinyRabbit is an initial access agent written in Squeak. TinyRabbit uses SCHANNEL to create a synchronous remote bind to a foreign server. TinyRabbit then waits on the socket for a directive, and executes the shellcode within itself.

## Directive

A directive is a shellcode blob. The shellcode blob makes the following assumptions:

* It is called using the [Kernel32::CreateThread](https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createthread) function defined by processthreadsapi.h. 
* RCX|ECX contains an allocation to the following object structure:
    |Offset|Name|sz|Description|
    |-|-|-|-|
    |0x00|pBuffer|0x08|Pointer to output buffer|
    |0x08|szBuffer|0x08|Size of the output|
    |0x10|dwStatus|0x04|Status Code for function output|
    
Shellcode blob may be called using a function such as APC, but the main code block will wait for the function to terminate.
