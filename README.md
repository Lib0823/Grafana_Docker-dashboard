# Docker Host & Container Monitoring Dashboard

이 Grafana 대시보드 JSON 파일은 **Docker 환경에서 호스트 서버 및 컨테이너 리소스 사용량**을 한 화면에서 모니터링할 수 있도록 구성되었습니다.  
단일 대시보드에서 **호스트 서버**뿐만 아니라, 각 컨테이너의 **CPU, 메모리, 디스크 사용량**등의 정보를 실시간으로 확인할 수 있습니다.

---

## 주요 기능

- **호스트 서버 리소스 모니터링**
  - CPU 사용률
  - 메모리 사용량
  - 디스크 사용량
  - 네트워크 트래픽
- **Docker 컨테이너 리소스 모니터링**
  - 컨테이너별 CPU 사용률
  - 컨테이너별 메모리 사용량
  - 컨테이너별 디스크 I/O
  - 컨테이너별 네트워크 트래픽
- **단일 대시보드에서 통합 모니터링**
  - 호스트와 모든 컨테이너 상태를 한 화면에서 관리
- **서버 선택 기능**
  - 대시보드 상단 드롭다운에서 서버를 선택하여 특정 서버 데이터만 조회 가능

---

## 아키텍처
![대시보드 예시](https://github.com/Lib0823/Grafana_Docker-dashboard/blob/main/architecture.png)

---

## 사전 준비

1. **Prometheus**와 **Grafana**가 설치 및 실행 중이어야 합니다.
2. Prometheus에 **node_exporter** 및 **cAdvisor** 메트릭이 수집되고 있어야 합니다.
   - `node_exporter` → 호스트 서버 리소스 수집
   - `cAdvisor` → Docker 컨테이너 리소스 수집

---

## 설치 및 사용 방법

1. **대시보드 JSON 가져오기**
   - 이 저장소의 `docker_host_container_dashboard.json` 파일 다운로드

2. **Grafana에 대시보드 가져오기**
   - Grafana 웹 UI 접속
   - `Dashboards` → `Import` 선택
   - JSON 파일 업로드 또는 내용 붙여넣기

3. **변수(Variables) 설정**
   - 대시보드 상단 우측 톱니바퀴(`Dashboard settings`) 클릭
   - **Variables** 메뉴에서 새 변수 추가:
     - **Name**: `server`
     - **Type**: `Query`
     - **Data source**: Prometheus
     - **Query**:
       ```promql
       label_values(up, instance)
       ```
     - **Refresh**: `On Dashboard Load`
     - **Include All option**: 필요 시 활성화
   - 저장 후 대시보드 상단 드롭다운에서 서버를 선택 가능

4. **서버 선택 후 모니터링**
   - 드롭다운에서 특정 서버 선택 → 해당 서버의 호스트/컨테이너 상태만 표시
   - "All" 선택 시 전체 서버 데이터 확인 가능

---

## 예시 화면

![대시보드 예시](https://github.com/Lib0823/Grafana_Docker-dashboard/blob/main/example.png)

