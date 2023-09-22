# Linux Kernel

> LInux Kernel에 대해 알아보아요

<br>

<br>

### Linux Kernel 이란?

- System에 존재하는 자원을 효율적으로 관리하는 **자원 관리자**로, 아래와 같은 주요 기능을 가진다

  1. **Processor 관리**
     - 처리 속도를 향상시키기 위해 여러 Process를 **병렬**로 연결하여 사용한다
     - system에서 동작하는 process도 kernel에서는 관리해야 할 자원이고, OS의 처리 요구에 맞춰 동작할 수 있도록 각 process에 필요한 processor를 효율적으로 **할당**하고 **수행**하도록 관리한다

  2. **Process 관리**
     - OS에는 최소한 하나 이상의 process가 동작한다
       - Process는 다른 말로 **task**라고도 하며, 주어진 일을 수행하는 기본 단위이다
     - Kernel은 **scheduler**를 이요하여 여러 process가 동작할 수 있도록 각 process를 **생성**하고 **제거**하며 외부 환경과 process를 **연결**하고 **관리**한다
  3. **Memory 관리**
     - 각각의 Process가 독립적인 공간에서 수행할 수 있도록 **가상의 주소 공간**을 제공한다
     - `가상 메모리`를 바타응로 물리적인 한계를 극복할 수 있는 기능을 제공한다

- 이외에도 **File System 관리**, **Device 제어**, **Network 관리** 등의 기능을 한다

<br>

- Linux Kernel은 OS에서 가장 중요한 부분이다
  - Processor와 System memory에 상주하면서 device나 memory 같은 hardware 자원을 관리하고,
  - Process의 schedule을 관리하여 **다중 process**를 구현하고,
  - System에 연결된 I/O를 처리하는 OS의 핵심 역할을 수행한다!
