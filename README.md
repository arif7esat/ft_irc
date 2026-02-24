# ft_irc — High-Performance TCP/IP Chat Server (C++98)

> *⚠️ **Notice on Source Code Availability:** The source codes for this project are currently hosted on the highly restricted internal servers (Vogsphere) of the 42 Network. Full source code migration to this public repository is scheduled and will be completed soon. Below is the architectural documentation and technical constraints of the project.*

## ⚙️ Architecture & First Principles
This project is a custom implementation of an RFC-compliant TCP/IP IRC Server, developed entirely from scratch in **C++98** without relying on modern network libraries (like Boost.Asio). The core objective was to build a robust, non-blocking network architecture capable of handling high concurrency—principles directly applicable to **real-time automotive communication systems and telematic control units.**

### Core Engineering Features
* **I/O Multiplexing:** Utilized `poll()` system calls to manage hundreds of concurrent client connections within a single-threaded event loop, avoiding the heavy context-switching overhead of multi-threaded server designs.
* **Non-blocking I/O:** Configured all sockets (`fcntl`, `O_NONBLOCK`) to ensure deterministic execution times, preventing any single dead client from locking the server resource.
* **Zero-copy Buffer Strategy:** Implemented optimized memory buffers for message distribution, ensuring minimal CPU cycles are wasted copying data between kernel and user space.
* **Strict OOP Hierarchies:** Designed a robust object-oriented architecture in C++98 to handle User Authentication, Channel Routing, and Operator Privilege Management.

## 🛡️ Robustness & Memory Safety
In system-level programming, memory leaks are catastrophic. This server was engineered with strict resource management protocols:
- Complete compliance with C++98 standard (no smart pointers allowed; manual `new`/`delete` management).
- Aggressive error propagation and signal handling (`SIGINT`, `SIGQUIT`) to ensure safe process termination and graceful socket closures.
- Valgrind tested: `All heap blocks were freed -- no leaks are possible.`

---
*Developed as part of the 42 Network Common Core Curriculum.*
