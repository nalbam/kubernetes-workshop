---
title: Kubernetes
weight: 2
---

쿠버네티스(K8S)는 컨테이너화된 애플리케이션을 자동으로 배포, 스케일링 및 관리해주는 오픈소스 시스템입니다.

* 컨테이너 작업을 자동화하는 오픈소스 플랫폼
* Container Orchestration
* Cluster 는 Master 와 Nodes 로 구성

![Container Evolution](./images/container_evolution.png)

#### 전통적인 배포

어플리케이션을 물리서버에서 실행했다. 하나의 물리서버에서 여러 어플리케이션 구동시 각 어플리케이션의 리소스 사용량을 정의하고 통제할 방법이 없었다. 같은 서버의 하나의 어플리케이션에 문제가 발생하면 다른 어플리케이션에 영향을 줄 수 있었다. 그래서 어플리케이션 만큼 물리서버를 분리 하였으나, 리소스를 효율적으로 사용 할 수 없었다.

#### 가상화된 배포

위의 해결책으로 가상화가 도입 되었다. 단일 물리서버의 CPU, Memory를 여러 VM(가살 머신)에 할당하여 어플리케이션의 리소스 사용량을 통제 하였다. 리소스를 좀더 효율적으로 사용 할수 있게 되었고, 어플리케이션을 추가하거나 업데이트가 쉬워졌다.

하지만, VM도 머신이므로 OS가 존재하고 부팅 시간이 필요하였다.

#### 컨테이너 배포

컨테이너는 VM과 유사하지만, OS를 공유한다. 따라서 좀더 가볍고 어플리케이션의 시작 속도가 더 빨라졌다.

다음은 컨테이너가 제공하는 혜택이다.

* 기민한 애플리케이션 생성과 배포: VM 이미지를 사용하는 것에 비해 컨테이너 이미지 생성이 보다 쉽고 효율적임.
* 지속적인 개발, 통합 및 배포: 안정적이고 주기적으로 컨테이너 이미지를 빌드해서 배포할 수 있고 (이미지의 불변성 덕에) 빠르고 쉽게 롤백할 수 있다.
* 개발과 운영의 관심사 분리: 배포 시점이 아닌 빌드/릴리스 시점에 애플리케이션 컨테이너 이미지를 만들기 때문에, 애플리케이션이 인프라스트럭처에서 분리된다.
* 가시성은 OS 수준의 정보와 메트릭에 머무르지 않고, 애플리케이션의 헬스와 그 밖의 시그널을 볼 수 있다.
* 개발, 테스팅 및 운영 환경에 걸친 일관성: 랩탑에서도 클라우드에서와 동일하게 구동된다.
* 클라우드 및 OS 배포판 간 이식성: Ubuntu, RHEL, CoreOS, 온-프레미스, 주요 퍼블릭 클라우드와 어디에서든 구동된다.
* 애플리케이션 중심 관리: 가상 하드웨어 상에서 OS를 실행하는 수준에서 논리적인 리소스를 사용하는 OS 상에서 애플리케이션을 실행하는 수준으로 추상화 수준이 높아진다.
* 느슨하게 커플되고, 분산되고, 유연하며, 자유로운 마이크로서비스: 애플리케이션은 단일 목적의 머신에서 모놀리식 스택으로 구동되지 않고 보다 작고 독립적인 단위로 쪼개져서 동적으로 배포되고 관리될 수 있다.
* 리소스 격리: 애플리케이션 성능을 예측할 수 있다.
* 자원 사용량: 리소스 사용량: 고효율 고집적.

### 쿠버네티스

쿠버네티스는 분산 시스템을 탄력적으로 실행하기 위한 프레임 워크를 제공한다. 애플리케이션의 확장과 장애 조치를 처리하고, 배포 패턴 등을 제공한다.

* `서비스 디스커버리와 로드 밸런싱` 쿠버네티스는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다. 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱하고 배포하여 배포가 안정적으로 이루어질 수 있다.
* `스토리지 오케스트레이션` 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재 할 수 있다.
* `자동화된 롤아웃과 롤백` 쿠버네티스를 사용하여 배포된 컨테이너의 원하는 상태를 서술할 수 있으며 현재 상태를 원하는 상태로 설정한 속도에 따라 변경할 수 있다. 예를 들어 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고, 모든 리소스를 새 컨테이너에 적용할 수 있다.
* `자동화된 빈 패킹(bin packing)` 컨테이너화된 작업을 실행하는데 사용할 수 있는 쿠버네티스 클러스터 노드를 제공한다. 각 컨테이너가 필요로 하는 CPU와 메모리(RAM)를 쿠버네티스에게 지시한다. 쿠버네티스는 컨테이너를 노드에 맞추어서 리소스를 가장 잘 사용할 수 있도록 해준다.
* `자동화된 복구(self-healing)` 쿠버네티스는 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, ‘사용자 정의 상태 검사’에 응답하지 않는 컨테이너를 죽이고, 서비스 준비가 끝날 때까지 그러한 과정을 클라이언트에 보여주지 않는다.
* `시크릿과 구성 관리` 쿠버네티스를 사용하면 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리 할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 시크릿을 노출하지 않고도 시크릿 및 애플리케이션 구성을 배포 및 업데이트 할 수 있다.

{{% children %}}
