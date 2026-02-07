---
title: DevOps 기술 고르는 기준과 쿠버네티스 엔지니어가 해야할 것들
date: 2026-02-07 10:00:00 
categories: [DevOps, 쿠버네티스]
tags: [쿠버네티스]
---

쿠버네티스 환경을 설정하기 위한 다양한 기술 스택에 대한 경험이 있어야 한다.     
그렇지만 너무나 다양한 기술이 있는데...     
다양한 기술들 속에서 집중적으로 공부할만한 기술을 고르는 기준은 다음과 같다.

## 수많은 DevOps 기술 중에서 고르는 기준
### 1️⃣ CNCF 프로젝트일 때
CNCF란 클라우드 네이티브 기술 관련 단체이다. 여기서 인정한 기술들은 꽤나 안정적이라고 생각하고 사용할 수 있을만큼 공신력이 있다고 한다.    

<br>

CNCF 프로젝트 중에서도 Graduated Projects, Incubating Projects, Sandbox Projects, Archived Projects로 나뉘는데,     

우리가 공부할만한 기술을 찾을 때는 **Graduated Projects와 Incubating Projects**을 참고하는 게 좋다.    

(Graduated에서도 깃허브 Stars가 낮다면 제외하고, Incubating에서도 깃허브 Stars가 높으면 공부 대상에 추가하기)


<br>

### 2️⃣ CNCF 프로젝트가 아닐 때
보통은 깃허브 Stars를 기준으로 판단한다고 한다.

<br>

---

<br>

## 쿠버네티스 엔지니어가 해야할 것들
### 1️⃣ 전체 흐름을 완성해보기
> 최소한의 도구와 기능을 선택하고 사용해서 전체적인 흐름을 만들어보기

| 분류                  | 상세              | 기술                |
| --------------------- | ----------------- | ------------------- |
| 개발                  | 빌드도구          | Gradle, Docker      |
|                       | CI/CD             | GitLab, Jenkins     |
| 오케스트레이션/매니징 | 오케스트레이션    | Kubernetes          |
|                       | 서비스 검색       | etcd, CoreDNS       |
|                       | 원격호출          | gRPC                |
|                       | 서비스 프록시     | NGINX               |
| 런타임                | 네이티브 스토리지 | LONGHORN            |
|                       | 컨테이너 런타임   | containerd, runc    |
|                       | 네트워크          | CALICO              |
| 플랫폼                | 설치              | kubeadm             |
| 분석                  | 모니터링          | Grafana, Prometheus |
|                       | 로깅              | Grafana loki        |


<br>

### 2️⃣ 전문 분야 공부하기
- 배포
- 클라우드
- 서비스 매시

| 분류                  | 상세                | 기술                                         |
| --------------------- | ------------------- | -------------------------------------------- |
| 개발                  | CI/CD               | argo, HELM                                   |
| 오케스트레이션/매니징 | 서비스 프록시       | envoy                                        |
|                       | API 게이트웨이      | Kong                                         |
|                       | 서비스 매시         | lstio                                        |
| 플랫폼                | 호스팅              | NCP, AWS, MS Azure, Google Kubernetes Engine |
|                       | 설치                | kops                                         |
| 분석                  | 트레이싱            | JAEGER, JIPKIN                               |
| 프로비저닝            | 자동화              | ANSIBLE, Terraform                           |
|                       | 컨테이너 레지스트리 | Docker Registry                              |


<br>

### 3️⃣ 상황별 공부하기
- 마음에 드는 도구가 있을 때
- 프로젝트를 하는 상황일 때

| 분류       | 상세                | 기술                                                                       |
| ---------- | ------------------- | -------------------------------------------------------------------------- |
| 개발       | 데이터베이스        | redis, cassandra, PostgreSQL                                               |
|            | 메세징              | kafka                                                                      |  |
| 플랫폼     | 관리형              | Red Hat OpenShift, RANCHER, K3S                                            |
| 분석       | 모니터링            | Thanos, cortex                                                             |
| 프로비저닝 | 컨테이너 레지스트리 | HARBOR                                                                     |
|            | 보안                | Open Policy Agent, CERT MANAGER, trivy, clair, Falco, KEYCLOAK, kube-bench |
|            | 키 관리             | Vault                                                                      |


<br>


---

### 느낀점
일하면서 들어본 기술도 있고, 너무 생소해보이는 기술도 많은데... 어느정도 선별 기준이 있다는게 그래도 다행인 것 같다. 

<br>

출처: 인프런 일프로 님 - [쿠버네티스 어나더 클래스-Spring 1, 2](https://www.inflearn.com/course/%EC%BF%A0%EB%B2%84%EB%84%A4%ED%8B%B0%EC%8A%A4-%EC%96%B4%EB%82%98%EB%8D%94-%ED%81%B4%EB%9E%98%EC%8A%A4-%EC%A7%80%EC%83%81%ED%8E%B8-sprint1?cid=330869)


