# 가상머신과 컨테이너
---

## Contents
- [Virtual Machines](#virtual-machines)
  - [가상머신이란](#가상머신이란)
  - [하이퍼바이저란](#하이퍼바이저란)
- [Containers](#containers)
  - [컨테이너란](#컨테이너란)
- [VM vs. Container](#virtual-machine-vs-container)
---

### Virtual Machines
#### 가상머신이란
- 물리적 하드웨어 시스템에 구축되어, 물리적 컴퓨터와 동일한 기능을 제공하도록 소프트웨어를 통해 논리적으로 만들어낸 컴퓨터
![image](https://user-images.githubusercontent.com/22542483/128626032-7680fce0-471d-4c87-af99-2fd8fc68c31d.png)

- 하드웨어 수준의 가상화
- 실제 물리적 컴퓨터 (Host) 의 리소스가 Hypervisor 라는 소프트웨어를 통해 Host 위에 설치된 복수의 가상머신들 (Guests) 에 적절히 분배 제공됨
- 대표적인 가상화 소프트웨어로는 Vmware 와 Virtualbox 가 있음

#### 하이퍼바이저란
- 가상머신을 생성하고 구동하는 소프트웨어
- 단일 물리 하드웨어에서 여러 다른 가상 머신을 호스팅할 수 있게 해줌
- Host 의 리소스 (CPU, 메모리, 스토리지 등) 를 가상머신 Guest 에 어떻게 할당할지 등을 관리함
- Host OS 의 존재 여부에 따라서 2가지 타입이 있음

![image](https://user-images.githubusercontent.com/22542483/128638118-f5e46eec-6db4-486f-a854-42c6651eac00.png)

**Type 1**
- Type 1 은 베어메탈 (Bare-metal) 이라 불리는 하이퍼바이저 타입으로, Host OS 없이 곧바로 하드웨어에서 직접 구동되어 게스트 OS를 관리함
- Host OS 를 거치지 않기 때문에 Type 2 보다 성능은 높지만, 설치가 까다로움
- 개인 보다는 엔터프라이즈 데이터 센터 등에서 주로 사용됨
- 대표적인 Type 1 Hypervisor 소프트웨어로는 MS Hyper-V, VMWare vSphere, KVM 등이 있음


**Type 2**
- Host 형 하이퍼바이저 타입으로, Hpyervisor 가 Host OS 위의 다른 App 처럼 구동되어서 사용됨
- Host OS Layer 를 거치므로 Type 1 보다 다소 느리지만 설치가 용이하여 개인이 주로 사용함
- 대표적인 Type 2 Hpyervisor 소프트웨어로는 VirtualBox, VMWare Workstation 등이 있음

----

### Containers
#### 컨테이너란
- 화물 운송에서 컨테이너라는 규격화된 운송장비를 도입하여 화물에 따라 운송 방법을 다르게 처리해야하는 비효율성을 제거한 것 처럼, Software 를 표준화된 방식으로 패키징하여 구동 환경에 종속되어 호환성을 설정해야하는 비효율성을 제거한 패키징 방법
- OS 수준의 가상화

![image](https://user-images.githubusercontent.com/22542483/128638908-29e843fd-829a-40fb-a949-c664f675b2c8.png)

- OS 수준의 가상화를 수행하는 컨테이너 기술은 위 표에서 알 수 있듯이 가장 많이 쓰이는 Docker 이외에도 다양함
- 다양한 컨테이너 기술이 있지만, 기본적으로 Linux Kernel 의 cgroup 과 namespace 를 이용하여 구현됨
  - cgroup (control group) 은 task 단위의 process 그룹에 대한 자원 할당을 제어하는 커널 모듈
  - namespace 는 process 별 리소스 사용을 분리하기 위해 process 별로 격리하는 기능

----

### Virtual Machine vs Container
<img width="567" alt="스크린샷 2021-08-09 오전 1 43 11" src="https://user-images.githubusercontent.com/22542483/128639201-81d4fe3b-9d80-46f8-8b0a-40f1cd7ef9d9.png">

- 가상머신 (VM) 은 하드웨어 수준의 가상화인 반면, 컨테이너는 OS 수준의 가상화
- VM과 달리 Container 는 별도의 Guest OS 를 가지고 있지 않고 격리된 프로세스로 가상화를 구현함
- Hypervisor, Guest OS 등이 패키징되지 않으므로 상당한 경량화 효과
  - 용량: VM은 GB 단위 vs. Container는 MB 단위
  - 생성 소요시간: VM은 10분+ vs. Container는 분단위
  - 시작/종료 소요시간: VM은 분단위 vs. Container는 초단위
- Container 는 OS 커널을 공유하므로, 장애 발생시 각 Container 들이 영향을 받을 수 있지만 VM은 완전히 독립되어 비교적 안정적

