---
title: 오브젝트
weight: 22
---

쿠버네티스 오브젝트 는 쿠버네티스 시스템에서 영속성을 가지는 개체이다. 쿠버네티스는 클러스터의 상태를 나타내기 위해 이 개체를 이용한다. 구체적으로 말하자면, 다음을 기술할 수 있다.

* 어떤 컨테이너화된 애플리케이션이 동작 중인지 (그리고 어느 노드에서 동작 중인지)
* 그 애플리케이션이 이용할 수 있는 리소스
* 그 애플리케이션이 어떻게 재구동 정책, 업그레이드, 그리고 내고장성과 같은 것에 동작해야 하는지에 대한 정책

#### 오브젝트 명세(spec)와 상태(status)

`spec`을 가진 오브젝트는 오브젝트를 생성할 때 리소스에 원하는 특징(의도한 상태)에 대한 설명을 제공해서 설정한다.

`status`는 오브젝트의 현재 상태 를 기술하고, 쿠버네티스 컴포넌트에 의해 제공되고 업데이트 된다.

쿠버네티스 컨트롤 플레인은 모든 오브젝트의 실제 상태를 사용자가 의도한 상태와 일치시키기 위해 끊임없이 그리고 능동적으로 관리한다.

#### 쿠버네티스 오브젝트 기술하기

쿠버네티스 디플로이먼트를 위한 요청 필드와 오브젝트 spec을 보여주는 `.yaml` 파일 예시이다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

디플로이먼트를 생성하기 위해 다음의 명령을 실행한다.

```bash
kubectl apply -f https://k8s.io/examples/application/deployment.yaml --record
```

#### 요구되는 필드

* `apiVersion` - 이 오브젝트를 생성하기 위해 사용하고 있는 쿠버네티스 API 버전이 어떤 것인지
* `kind` - 어떤 종류의 오브젝트를 생성하고자 하는지
* `metadata` - 이름 문자열, UID, 그리고 선택적인 네임스페이스를 포함하여 오브젝트를 유일하게 구분지어 줄 데이터
* `spec` - 오브젝트에 대해 어떤 상태를 의도하는지

오브젝트 `spec`에 대한 정확한 포맷은 모든 쿠버네티스 오브젝트마다 다르고, 그 오브젝트 특유의 중첩된 필드를 포함한다. [Kubernetes API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/) 는 쿠버네티스를 이용하여 생성할 수 있는 오브젝트에 대한 모든 spec 포맷을 살펴볼 수 있도록 해준다.
