# Chapter 1: Introduction

```text
An operating system is software that manages a computer’s hardware.
It also provides a basis for application programs and acts as an intermediary between the computer user and the computer hardware.
```

### Operating system is one program
- the operating system is the one program running at all times on the computer—usually called the kernel. Along with the kernel, there are two other types of programs: `system programs`, which are associated with the operating system but are not neces- sarily part of the kernel, and `application programs`, which include all programs not associated with the operation of the system.


### Middleware in Mobile

- Today, if we look at operating systems for mobile devices, we see that once again the number of features constituting the operating system is increasing. Mobile operating systems often include `not only a core kernel` but also `middleware` a set of software frameworks that provide additional services to application developers like databases, multimedia, and graphics 

### Computer-System Organization
```text
How does hardware communicate with itself?
```
- A modern general-purpose computer system consists of one or more CPUs and a number of device controllers connected through a common `bus` that provides access between components and `shared memory (RAM)`
- Operating systems have a `device driver` for each device controller for manage 

## Interrupts
```text 
Alert the CPU to events that require attention.
```
- Used with device controller
- Some issue 

## Interrupt Life Cycle
- The CPU hardware has a wire called the `interrupt-request line` that the CPU senses after executing every instruction.
- When the CPU detects that a controller has asserted a signal on the interrupt-request line, it reads the interrupt number and jumps to the `interrupt-handler routine` by using that interrupt number as an index into the `interrupt vector`(interrupt vector is table of ISR).
- It then starts execution at the address associated with that index.
- The interrupt handler saves any state it will be changing during its operation, determines the cause of the interrupt, performs the necessary processing, performs a state restore, and executes a return from interrupt instruction to return the CPU to the execution state prior to the interrupt.

![alt text](https://github.com/ammarelriyali/Operating-System-Concepts/blob/main/notes/Chapter1/Interrupt%20I%3AO%20cycle.png?raw=true)

## Isuue With Interrupt System

- Ability to defer interrupt handling during critical processing.
- Efficient way to dispatch to the proper interrupt handler for
a device.
- Multilevel interrupts, so that the operating system can distin- guish between high- and low-priority interrupts and can respond with the appropriate degree of urgency.

## Sloveing The Problem 
- Most CPUs have two interrupt request lines
    - One is the `nonmaskable` interrupt, which is reserved for events such as unrecoverable memory errors.
    - The second interrupt line is `maskable`: it can be turned off by the CPU before the execution of critical instruction sequences that must not be interrupted. 
- Each element in the interrupt vector points to the head of a list of interrupt handlers. When an interrupt is raised, the handlers on the corresponding list are called one by one, until one is found that can service the request.this technique called `interrupt chaining` 
- `interrupt priority levels`. These levels enable the CPU to defer the handling of low-priority inter-rupts without masking all interrupts and makes it possible for a high-priority interrupt to preempt the execution of a low-priority interrupt.

## Interrupts Summary 
- interrupts are used throughout modern operating systems to handle asynchronous events (and for other purposes we will discuss through- out the text).
- Device controllers and hardware faults raise interrupts. To enable the most urgent work to be done first, modern computers use a system of interrupt priorities. Because interrupts are used so heavily for time-sensitive processing, efficient interrupt handling is required for good system performance.

## Storage Structure
```text
The CPU can load instructions only from memory, so any programs must first be loaded into memory to run. General purpose computers run most of their programs from rewritable memory, called main memory (also called random access memory, or RAM).
```

- the first program to run on computer poweron is a `bootstrap program`, which then loads the operating system.
- Since RAM is volatile loses its content when power is turned off or otherwise lost we cannot trust it to hold the bootstrap program. Instead, for this and some other purposes, the computer uses `electrically erasable programmable read-only memory (EEPROM)` and other forms of firmwar storage that is infrequently written to and is nonvolatile. 
 - typical instruction – execution cycle, as executed on a system with a `von Neumann architecture`, first fetches an instruction from memory and stores that instruction in the instruction register.
 - The instruction is then decoded and may cause operands to be fetched from memory and stored in some internal register.
 - After the instruction on the operands has been executed, the result may be stored back in memory. 

![alt text](https://github.com/ammarelriyali/Operating-System-Concepts/blob/main/notes/Chapter1/Storage-device%20hierarchy.png?raw=true)

