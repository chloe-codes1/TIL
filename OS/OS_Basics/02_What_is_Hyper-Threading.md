# What is Hyper-Threading?
>
> Hyper Threading에 대하여 알아봅시다앙~
>
> Reference: [Intel Docs](https://www.intel.com/content/www/us/en/gaming/resources/hyper-threading.html)

<br>

이 글에서는 `single-threaded` 그리고 `multithreaded` application의 차이와 `Hyper-Thrading`이 무엇인지, 그리고 `multithreading`과 어떤 점이 다른지 설명한다

<br>

### What Is `Multithreading`?

- Multithreading이란 **동시 처리**를 위한 **병렬** 또는 **분할** 작업의 한 형태이다
- Thread program은 single core에 대량의 workload를 제공하는 대신, 작업을 여러 개의 software thread로 분할한다
- 이러한 Thread는 시간 절약을 위해 서로 다른 CPU core에 의해 병렬 처리된다

<br>

### What Is `Hyper-Threading`?

- Intel이 만든 동시 multithreading 기술로, 물리적 실행 장치 한 개에 가상 실행 장치 두 개를 할당해 성능을 높인다
- Core 한 개당 thread가 두 개씩 추가되므로, 운영체제는 physical core 수 * 2로 core 수를 인식한다
  - 즉, 하나의 **physical core**가 다른 software thread를 처리할 수 있는 두 개의 **logical core** 처럼 작동한다는 것을 의미한다
- 두 개의 **logical core**는 기존의 single thread core 보다 더 효율적으로 작업을 수행할 수 있다
  - Intel의 `Hyper-Threading` 기술은 core가 이전의 다른 작업이 완료되기를 기다리는 유휴 시간을 이용하여 CPU 처리량을 개선한다

<br>

### What Benefits Will I See from `Hyper-Threading`?

- CPU `Hyper-Threading`이 있다면, PC는 더 적은 시간에 더 많은 정보를 처리할 수 있고, 더 많은 배경 작업을 중단 없이 실행할 수 있다
- 올바른 환경에서 이 기술은 CPU core가 한 번에 두 가지 작업을 효과적으로 수행할 수 있도록 한다

<br>

### See if Mac OS has enabled `Hyper-Threading`

`sysctl` 명령어를 통해 physical processor와 logical processor 수의 차이를 알아볼 수 있다

```sh
sysctl hw.physicalcpu hw.logicalcpu
```

<br>

나는 Intel Core i7 processor가 탑재된 MacBook을 사용중이라서, 아래와 같이 `Hyper-Threading`이 활성화된 것을 확인할 수 있다

<p align="center">
  <img src="../images/physical-and-logical-cpu.png" width="300">
</p>

<br>
<br>

*끝!*
