# Red Hat Openshift

Openshift는 Red Hat의 하이브리드 또는 멀티 클라우드를 위한 Kubernetes Container platform입니다. 아래 내용은 Openshift에 대해 이해하기 위해, Red Hat의 자료를 중심으로 정리하였습니다. 

## 주요특징

[Red Hat® OpenShift](https://www.redhat.com/ko/technologies/cloud-computing/openshift)는 오픈 하이브리드 클라우드 전략을 위해 구축된 엔터프라이즈 수준의 쿠버네티스 컨테이너 플랫폼으로서 하이브리드 클라우드, 멀티클라우드 및 엣지 배포를 관리할 수 있는 일관된 애플리케이션 플랫폼을 제공합니다.

- Kubernetes Container Platform
- 하이브리드/멀티 클라우드 및 엣지 배포를 관리 

- [설치된 위치에 상관없이 인터페이스](https://www.redhat.com/ko/technologies/cloud-computing/openshift#developer)는 관리자 및 개발자에게 동일한 상태로 유지되므로 중앙 관리 콘솔에서 여러 팀의 클러스터, 서비스 및 역할을 제어할 수 있습니다.

- [Openshift](https://www.youtube.com/watch?v=S5NTxTtfdg8): Red Hat Enterprise, Prometheus, Tekton, Grafana, Crio-o로 구성됨

![image](https://user-images.githubusercontent.com/52392004/175792246-2f6033bc-85fc-48b3-9f94-b0aab7106613.png)


## 오픈 하이브리드 클라우드

- 어디서든 애플리케이션을 실행하고 관리: 베어 메탈에서 가상 머신(VM), 엣지 컴퓨팅, 프라이빗 클라우드, 퍼블릭 클라우드에 이르는 다양한 환경에서 애플리케이션을 유연하게 실행
- 애플리케이션을 다양하게 결합해 설계, 개발 및 운영하기 위해 Red Hat에서 권장하는 전략
- 디지털 비즈니스 트랜스포메이션에 필요한 속도, 안정성, 규모를 확보하고 진정으로 유연한 클라우드 경험을 제공

## 어디에 배포하든 클라우드와 유사한 경험을 지원하는 엔터프라이즈급 쿠버네티스 플랫폼

- 클라우드, 온프레미스, 엣지 등 위치와 관계없이 일관된 경험을 통해 애플리케이션을 빌드, 배포, 실행할 위치를 선택할 수 있습니다
- 자동화된 풀 스택 운영과 개발자를 위한 셀프 서비스 프로비저닝

## PaaS

[Red Hat OpenShift Platform - PaaS의 정의와 특장점](https://www.youtube.com/watch?v=QdIrGLkatjI)

![image](https://user-images.githubusercontent.com/52392004/175792174-2d401d7b-98c2-433f-8419-3b5de5f2439b.png)

## Red Hat OpenShift 옵션

[선호하는 클라우드 제공업체에 Red Hat OpenShift를 관리형 서비스](https://www.redhat.com/ko/technologies/cloud-computing/openshift#developer)로 배포하고 Azure, AWS, IBM Cloud 또는 Google Cloud에서 원활한 경험을 누릴 수 있습니다.

![image](https://user-images.githubusercontent.com/52392004/175792569-31c6444b-1071-4c88-b255-a2a458afb876.png)


### Red Hat OpenShift Service on AWS

Red Hat OpenShift Service on AWS는 레드햇과 아마존 웹서비스가 협력하여 지원하며, 전체적으로 관리하는 Red Hat OpenShift 서비스입니다.

- AWS에서 기본적으로 실행되는 Red Hat OpenShift로 쿠버네티스 애플리케이션을 구축, 배포 및 관리
- Red Hat OpenShift Service on AWS가 제공하는 전체 관리형 Red Hat OpenShift 서비스를 선택하면 통합 클러스터 생성, 유연한 사용량 기준 요금 청구, Red Hat과 AWS 양사의 공동 지원

[Hands-on demo of Red Hat OpenShift Service on AWS](https://www.youtube.com/watch?v=MFcbuxkP3C4)

[Red Hat OpenShift Service on AWS](https://ap-northeast-2.console.aws.amazon.com/rosa/home?region=ap-northeast-2#/)

<img width="583" alt="image" src="https://user-images.githubusercontent.com/52392004/175792666-6c3acd5c-723b-476d-8457-b1a0f97e4c0b.png">

AWS 비용에 아래의 비용이 추가 됩니다. 

<img width="428" alt="image" src="https://user-images.githubusercontent.com/52392004/175792702-02d76087-21b1-40c1-8f1f-19f1aa193fbc.png">

## [특징](https://www.penta.co.kr/solution/sisw/cloudpalatform/rhpaas.php)

- Docker를 사용하여 구현된 공개SW기반 PaaS
- Docker컨테이너들의 오케스트레이션을 위한 Kubernetes적용
- Bare-Metal, VM(vSphere, Hyper-V, RHEV 등), Public/Private IaaS 제약없이 설치
- 빠르고 쉽게 애플리케이션플랫폼 제공
- Git연동을 통한 소스 maven 컴파일 및 배포 (자동)
- OpenVswitch를 통한 자동 Networking 구성
- 관리 및 모니터링을 위한 Web Console, REST API 및CLI 제공
- 소스버전관리용 Git, Docker이미지버전 관리용 Registry(저장소) 제공
- AutoScaler를 통한 Docker 컨테이너 자동 확장/축소 (Auto-Scaling)
- Router를 통한 자동 부하분산 (Load-Balancing)
- Wildcard entry를 통한 DNS 연계 제공
- JBossEAP를 통한 WAS 클러스터링(Session Clustering) 기능 제공
- H/W 확장시 ANSIBLE을 통한 쉬운 설치/구성


## CI/CD

[컨테이너, 어디까지 왔나? 레드햇과 함께하는 컨테이너 집중 탐구](https://www.youtube.com/watch?v=PsCmswVRTxo)

![image](https://user-images.githubusercontent.com/52392004/175793453-f69580cd-47b5-42a6-94de-6145832a3c9f.png)

![image](https://user-images.githubusercontent.com/52392004/175793548-6da717bf-39dd-47b6-8a51-45c7afb04a89.png)

![image](https://user-images.githubusercontent.com/52392004/175793618-daebff22-876d-449a-96c5-d71fa2fd431c.png)

## Developer Sandbox for Red Hat OpenShift

[샌드박스 빌드](https://developers.redhat.com/developer-sandbox#assembly-field-sections-57831) 환경

![image](https://user-images.githubusercontent.com/52392004/175792275-5cc2f469-f619-4209-ba97-d174f8955c03.png)

The sandbox provides you with a private OpenShift environment in a shared, multi-tenant OpenShift cluster that is pre-configured with a set of developer tools.


The sandbox is your free access to an OpenShift cluster where you can learn and experiment with Kubernetes and OpenShift. Several developer tools are pre-configured for you, and you can build one of our sample applications — or use your own code.

- Provided runtimes (e.g. Python, PHP, Java, and more)
- Database templates (get a SQL database in seconds)
- Helm charts
- Kubernetes objects, such as Deployments

## [오픈시프트 제공 버전](http://www.opennaru.com/redhat/openshift/)

- OpenShift Origin
Origin은 커뮤니티가 지원하는 오픈시프트의 오픈 소스 업스트림 프로젝트입니다. Origin은 CentOS 또는 RHEL(Red Hat Enterprise Linux)에 설치할 수 있습니다.

- OpenShift Container Platform
Container Platform은 Red Hat이 제공하고 지원하는 엔터프라이즈급 사용 버전입니다. 이 버전을 통해 고객은 오픈시프트 컨테이너 플랫폼에 필요한 자격을 구매하고 전체 인프라의 설치 및 관리를 담당합니다.

고객이 전체 플랫폼을 “소유”하기 때문에 온-프레미스 데이터 센터나 공용 클라우드(Azure, AWS, Google 등)에 설치할 수 있습니다.

- OpenShift Online
Online은 Container Platform을 사용하는 Red Hat이 관리하는 멀티 테넌트 오픈시프트입니다. Red Hat이 모든 기본 인프라(예: VM, 오픈시프트 클러스터, 네트워킹, 저장소 등)를 관리합니다.

이 버전을 통해 고객은 컨테이너를 배포하지만 컨테이너가 실행되는 호스트를 제어할 수 없습니다. Online은 다중 테넌트이므로 컨테이너가 다른 고객의 컨테이너와 동일한 VM 호스트에 함께 배치될 수 있습니다. 비용은 컨테이너당 비용이 청구됩니다.

- OpenShift Dedicated
Dedicated는 Container Platform을 사용하는 Red Hat이 관리하는 단일 테넌트 OpenShift입니다. Red Hat이 모든 기본 인프라(VM, OpenShift 클러스터, 네트워킹, 저장소 등)를 관리합니다. 클러스터는 한 고객 전용이며 공용 클라우드(예: AWS, Google, Azure는 2018년 초 출시 예정)에서 실행됩니다. 시작 클러스터에는 연간 $48,000에(선불) 4개의 응용 프로그램 노드가 포함됩니다.
