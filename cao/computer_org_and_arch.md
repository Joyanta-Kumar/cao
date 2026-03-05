# Org. Vs Arch.

| Feature | Computer Architecture | Computer Organization |
| ------- | --------------------- | --------------------- |
| Definition | Logical design and functional behaviour of a computer | Physical implementation of the architectural specification |
| Focus | What the system does | How the system does it |
| Concerned with | Instruction St Architecture (ISA), addressing modes, data types, registers | ALU design, control singnals, memory interfaces, bus structure |
| Visibility | Visible to programmer | Transparent (hidden) to the programmer |
| Examples | Instruction formats, number of registers, IO mechanism | Use of carry look-ahead adder, pipeline stages, cache memory |
| Nature | Abstruct / Conceptual | Concrete / Physical |
| Changes with | New ISA design (x86 vs arm) | Technology improvements (faster transistor) |
| Goal | Define what operations are supported | Efficiently execute those operations |
| Design level | High level (logical design) | Low level (physical hardware) |
