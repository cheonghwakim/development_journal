### Docker Compose란?

여러 개의 컨테이너(container)로 구성된 애플리케이션을 하나의 파일에 정의해놓고 한 번에 올리거나 내릴 수 있다. 편리함 때문에 Docker Compose는 특히 로컬 개발 환경이나 테스트 자동화 환경에서 간단한 컨테이너 오케스트레이션(Container Orchestration) 도구로 많이 사용되고 있다. 

##### Docker Compose 설정에 사용되는 `docker-compose.yml`을 작성하는 방법

1. **파일 위치 / 기본 구조** 

   Docker Compose는 기본적으로 `docker-compose.yml` 파일을 설정 파일로 사용하는데 일반적으로 프로젝트의 최상위 디렉토리에 위치시킨다. 그러면 프로젝트에 디렉토리에 들어오자 마자 손쉽게 애플리케이션을 올릴 수 있다.

   `docker-compose.yml` 파일은 대략적으로 다음과 같은 구조를 가진다.

   ```
   version: "3.5"
   services:
     web:
       # 웹 애플리케이션 설정
     db:
       # 데이터베이스 설정
   networks:
     # 네트워크 설정
   volumes:
     # 볼륨 설정
   ```

   ​