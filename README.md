# DEV flow
Spring Boot프로젝트를 빌드할 시 톰캣이 내장된 .jar파일이 나오게 되는데 
이 때 여기 안에 프론트 프로젝트를 추가하여 함께 빌드하는 방법

1. SpringBoot프로젝트 생성(의존성 Spring Web 추가)
2. pom.xml(devtools, oracle, mybatis설정)
3. 백엔드 로직 작성
4. Vue CLI프로젝트 생성
5. vue.config.js -> module.exports(outputDir, indexPath, proxy설정)
6. 프론트엔드 빌드 ($ npm run build)
7. Maven Update
8. 8080포트 백엔드 서버 Run
9. 8081포트 프론트엔드 개발서버 Run
10. 프론트엔드 로직 작성
