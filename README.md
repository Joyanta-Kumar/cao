# Top-level view of computer system

## Definition**  
A computer is an electronic system that process data and instructions. At top level, it consists of:  

| module | work |
| ------ | ---- |
| CPU    | Executes instructions |
| Memory | Stores data and programs |
| IO Unit | Communicates with the outside world |

### CPU Components

| module | work |
| ------ | ---- |
| CU    | Coordinates operations, fetches and decodes instructions |
| ALU | Performs arithmetic and logic operations |
| REG | Very fast storage for operands and intermediate results |

### CPU Buses
- Connect CPU, Memory and IO.  
- Types:
  - Address Bus
  - Data Bus
  - Control Bus

## Diagram  
```graphql
            ┌───────────┐
            │   Input   │
            └─────┬─────┘
                  │
        ┌─────────▼─────────┐
        │       Memory      │
        └─────────┬─────────┘
                  │
        ┌─────────▼─────────┐
        │        CPU        │
        │  CU | ALU | REG   │
        └─────────┬─────────┘
                  │
            ┌─────▼─────┐
            │   Output  │
            └───────────┘

```

## Summary  
A computer consists of CPU, Memory, and IO interconnected by System Buses, where the CPU executes instructions using its ALU, Control Unit, and Registers.  

---

# Bus Functional Structure

## Definition  
A bus is a set of parallel lines used for communication between CPU, Memory, and IO. Functionally, it is divided into three types:  

1. Address Bus  
  - Purpose: Selects the Memory or IO location for READ / WRITE.
  - Direction: Unidirectional (CPU -> Memory, IO).
  - Notes: Width determines maximum addressable memory. 
2. Data Bus
  - Purpose: Transfer actual data or instructions.  
  - Direction: Bidirectional.
  - Notes: Width determines word size and throughput.
3. Control Bus 
  - Purpose: Carries Control and Timing signals.
  - Signals include: READ, WRITE, CLOCK, RESET, INTERRUPT, BUS REQUEST / GRANT. 
  - Direction: Both directions.  
  - Notes: Ensures correct operation and synchronization.  

## Memory READ operation flow
1. CPU places address on `Address Bus`.
2. CPU asserts READ on `Control Bus`.
3. Memory places data on `Data Bus`.
4. CPU reads data.

## Summary  
The system bus consists of the address bus for specifying locations, the data bus for transferring information, and the control bus for coordinating operations between CPU, memory, and IO devices.  

---

# Bus Structure  

## Definition  
Bus structure describes how buses are organized in a computer system to connect CPU, memory, and IO. It affects performance, scalability, and cost. 

1. Single bus structure
  - Concept: One bus connects CPU, Memory, and all IO devices.  
  - Characteristics: Only one transfer at a time, simple design.
  - Advantage: Low cost, easy to implement. 
  - Disadvantage: Low performance, bus contention, poor scalability.  
  - Use Case: Small systems, micro-controllers.

**Diagram**
```mathematica
CPU ────────────── Memory
  │
  ├────────────── I/O Device 1
  └────────────── I/O Device 2
```

2. Multiple bus structure
  - Concept: Separate buses for `CPU <-> Memory` and `CPU <-> IO`.
  - Characteristics: Parallel transfer possible, reduced contention.
  - Advantages: Higher performance, scalable.
  - Disadvantages: More complex, higher cost, arbitration needed.
  - Use Case: General-purpose computers.  
  
  **Diagram**
```mathematica
        Memory Bus
CPU ────────────── Memory

        I/O Bus
CPU ────────────── I/O Devices
```

3. Mezzanine (Hierarchical) bus structure
  - Concept: Buses arranged in layers: high-speed local bus near CPU, slower peripheral buses.  
  - Characteristics: Optimized for speed, reduces electrical load, scalable.  
  - Advantages: High performance, supports multiple levels of devices.  
  - Disadvantages: Complex design, bridges / controller needed.  
  - Use Case: Modern computers (PCIe, chip-set buses, memory channels).  

**Diagram**  

```mathematica
CPU
 │
High-speed Local Bus
 │
Bridge
 │
Peripheral Bus
 │
I/O Devices
```

## Summary  
Bus structures range from single-bus(simple, low-performance) to multiple and mezzanine buses(higher performance and scalability through separation and hierarchy).  

---

# CPU Registers

## Definition  
Registers are high-speed storage locations inside the CPU used to hold operands, instructions, addresses, or intermediate results during instruction execution.  

### Types of Registers
#### General Purpose Registers (GPRs)
  - Hold operands, results, and temporary data.  
  - Directly accessible by instructions.  
  - Examples: `R0->R31` (ARM / RISC-V), `EAX / EBX` (x86).  
  - Help reduce memory access -> improves performance.  
#### Special Purpose Registers  

| Register | Purpose |
| -------- | ------- |
| Program Counter | Holds address of next instruction |
| Instruction Register | Holds current instruction |
| Stack Pointer | Points to top of stack |
| Flag Register | Holds condition flags (zero, carry, overflow) |
| Control Register | Configure CPU modes, interrupt |

#### Memory Access Registers
Interface CPU with Memory.  

| Register | Purpose |
| -------- | ------- |
| Memory Address Register | Holds memory location to READ / WRITE |
| Memory Buffer Register | Holds data being transferred to / from memory |

## How Register fit in Fetch-Execute cycle  
- MAR & MBR -> Move data to / from memory.  
- IR & PC -> Fetch and sequence instructions.  
- GPTs & ALU -> Performs computations.  

## Summary
Registers are the CPU's fastest storage, classified as general-purpose, special-purpose, and memory-access, and they directly support instruction fetch, execution, and memory operations.  

---

# Instruction Format (Opcode & Operands)  

## Definition
And instruction is a binary pattern that tell the CPU what operation to perform and on what data.

It has two main elements:

### Opcode
- Specifies the operation to perform.  
- Examples: `ADD`, `SUB`, `LOAD`, `STORE`, `JMP`.  
- Decoded by the control unit to generate control signals.  

### Operands
- Specify the data or the location of the data.  
- Can be:
  - Registers.  
  - Memory addresses.  
  - Immediate values.  
  - IO locations.  
- Number of operands varies: 0, 1, 2, or 3.  

## Example instructions  

 | Instruction | Opcode | Operands | Meaning |  
 | ----------- | ------ | -------- | ------- |
 | ADD R1, R2, R3 | `ADD` | `R1`,`R2`,`R3` | R1<-R2+R3 |
 | LOAD R1, 0x1000 | `LOAD` | `R1`, `0x1000` | R1 ← Memory[0x1000] |

 ## Summary
 An instruction consists of an opcode, which specifies the operation, and operands which specify the data or location involved in the operation.  

 ---

 