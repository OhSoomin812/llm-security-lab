# 보안 공지 요약 봇 — 실행 결과

실행 시각: 2026-10-13 11:05:12

## 모델별 정확도 (각 10점 만점)

| 모델 | 형식 | 제품 | 조치 | 오류 |
| --- | --- | --- | --- | --- |
| gpt-4.1-mini | 10 | 10 | 10 | 0 |
| gpt-4.1-nano | 10 | 10 | 7 | 0 |
| qwen2.5:3b | 10 | 10 | 8 | 0 |
| llama3.2 | 10 | 10 | 7 | 0 |

## 모델별 토큰 · 시간 · 잘림

| 모델 | 입력토큰 | 출력토큰 | 총토큰 | 시간(초) | 잘림 | 오류 |
| --- | --- | --- | --- | --- | --- | --- |
| gpt-4.1-mini | 5521 | 622 | 6143 | 10.7 | 0 | 0 |
| gpt-4.1-nano | 5521 | 537 | 6058 | 8.3 | 0 | 0 |
| qwen2.5:3b | 5849 | 790 | 6639 | 82.2 | 0 | 0 |
| llama3.2 | 5726 | 611 | 6337 | 68.8 | 0 | 0 |

## 모델별 전체 답변

### CVE-2021-44228

**gpt-4.1-mini**

```
제품: Apache Log4j 2.x (2.14.1 이하 및 2.15.0 이전 버전)
영향: 공격자가 LDAP JNDI 파서를 통해 원격 코드 실행을 할 수 있다.
조치: 2.16.0 이상으로 업데이트
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Log4j 버전 2.14.1 이하
영향: 원격 코드 실행(RCE) 취약점이 있어 공격자가 임의의 코드를 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Apache Log4j 2.0
영향: 로그 메시지나 파라미터에 사용자 또는 불안정한 데이터를 로깅할 경우 로그 메시지가 로그 서버를 통해 실행될 수 있는 Remote Code Execution(RCE)을 유발할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
# 제품: Log4j
#영향: attacker-controlled LDAP와 JNDI 관련 엔드포인트를 사용하여 원격 코드 실행을 possible로 만든다.
#조치: Log4j 2.16.0
#긴급도: 높음
```

### CVE-2022-22965

**gpt-4.1-mini**

```
제품: Spring Framework 5.2.20 미만 및 5.3.18 미만  
영향: 원격에서 코드 실행이 가능하다.  
조치: 5.3.18 이상 또는 5.2.20 이상으로 업그레이드  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Spring Framework 버전 5.2.19 이하, 5.3.17 이하
영향: 원격 코드 실행(RCE) 공격이 가능하다
조치: 5.2.20, 5.3.18
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Spring Framework prior to versions 5.2.20 and 5.3.18
영향: Spring MVC 또는 Spring WebFlux 애플리케이션은 JDK 9 이상에서 Tomcat 컨테이너를 사용하여 WAR 배포로 실행되는 애플리케이션에 대해 데이터 바인딩을 통해 레이어 4 Shell 공격을 통해 레거시 코드 실행을 수행할 수 있습니다.
조치: Spring Framework [5.3.18](https://github.com/spring-projects/spring-framework/releases/tag/v5.3.18) and [5.2.20](https://github.com/spring-projects/spring-framework/releases/tag/v5.2.20.RELEASE)
긴급도: 높음
```

**llama3.2**

```
제품: Spring Framework prior to versions 5.2.20 and 5.3.18
영향: Tomcat Servlet container 위에 WAR 패키지에 `spring-webmvc` 또는 `spring-webflux` 의존성이 있는 Spring MVC 또는 Spring WebFlux 애플리케이션에 RCE가 발생할 수 있다.
조치: Spring Framework [5.3.18]와 [5.2.20], Spring Boot [2.6.6]와 [2.5.12]
긴급도: 높음
```

### CVE-2017-5638

**gpt-4.1-mini**

```
제품: Apache Struts 2 2.3.x (2.3.32 이전), 2.5.x (2.5.10.1 이전)  
영향: 원격 공격자가 조작된 HTTP 헤더를 통해 임의 명령을 실행할 수 있음  
조치: 2.3.32 이상, 2.5.10.1 이상으로 업그레이드  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Apache Struts 2 2.3.x 이전 2.3.32 및 2.5.x 이전 2.5.10.1
영향: 원격 공격자가 조작된 HTTP 헤더를 통해 임의의 명령을 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Apache Struts 2 2.3.x, 2.5.x
영향: 공격자는 HTTP 헤더를 사용해 원격에서 명령을 실행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: Apache Struts 2 2.3.x, 2.5.x
영향: Content-Type, Content-Disposition, Content-Length HTTP header를 crafted하여 원격 attacker가 원하는 명령을 실행할 수 있다.
조치: 공지에 없음
긴급도: 보통
```

### CVE-2014-6271

**gpt-4.1-mini**

```
제품: GNU Bash 4.3 이하  
영향: 원격 공격자가 임의의 코드를 실행할 수 있다  
조치: 공지에 없음  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Bash 4.3 이하
영향: 원격 공격자가 임의의 코드를 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**qwen2.5:3b**

```
제품: GNU Bash 4.3
영향: 공격자는 시스템을 통해 임의 코드를 실행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: GNU Bash 4.3
영향: 원격 공격자가 shell 명령을 실행할 수 있다.
조치: GNU Bash 4.4
긴급도: 높음
```

### CVE-2023-49105

**gpt-4.1-mini**

```
제품: ownCloud owncloud/core 10.6.0부터 10.13.0까지  
영향: 공격자가 인증 없이 파일을 접근, 수정, 삭제할 수 있다  
조치: 10.13.1  
긴급도: 높음
```

**gpt-4.1-nano**

```
제품: ownCloud core 이전 버전(최초 10.6.0)  
영향: 공격자가 인증 없이 파일에 접근, 수정 또는 삭제 가능  
조치: 공지에 없음  
긴급도: 높음
```

**qwen2.5:3b**

```
제품: ownCloud owncloud/core before 10.13.1
영향: 파일을 접근, 수정, 삭제할 수 있는 악용 가능성이 발생
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: ownCloud owncloud/core
영향: 공격자가 특정 사용자 이름을 biết고, 사용자 이름이-configured signing-key가 없는 사용자에게 파일을 수정하거나 삭제할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

### CVE-2026-48710

**gpt-4.1-mini**

```
제품: Starlette 1.0.1 미만 버전  
영향: 조작된 HTTP Host 헤더로 request.url.path가 실제 요청 경로와 달라져 보안 제한 우회 가능  
조치: 1.0.1 이상 버전으로 업그레이드  
긴급도: 보통
```

**gpt-4.1-nano**

```
제품: Starlette 버전 1.0.0 이하
영향: 공격자가 malformed한 Host 헤더를 통해 request.url.path를 조작하여 보안 제한을 우회할 수 있다.
조치: 1.0.1 이상
긴급도: 보통
```

**qwen2.5:3b**

```
제품: Starlette 1.0.0 이전 버전
영향: 중앙 서버에 대한 악용을 방지하지 못하고, 요청 경로에 대한 보안 제한을 무시할 수 있는 취약점이 존재한다.
조치: 1.0.1 이상
긴급도: 높음
```

**llama3.2**

```
제품: Starlette 1.0.1
영향: maliciously crafted HTTP `Host` request header를 사용하여 request.url.path와 canonical ASGI request path (scope["path"])의 차이를 만들 수 있다.
조치: Starlette 1.0.1
긴급도: 보통
```

### CVE-2026-59822

**gpt-4.1-mini**

```
제품: LiteLLM 1.84.0 이전 버전  
영향: 인증 없이 조작된 Authorization 헤더로 MCP 도구에 무단 접근 가능  
조치: 1.84.0  
긴급도: 높음
```

**gpt-4.1-nano**

```
제품: LiteLLM 버전 1.84.0 이전
영향: 인증되지 않은 공격자가 무단으로 MCP 도구에 접근할 수 있음
조치: 1.84.0
긴급도: 높음
```

**qwen2.5:3b**

```
제품: LiteLLM (영향받는 버전: 1.84.0 이후)
영향: MCP Streamable HTTP endpoint를 통해 악용자에게 인증되지 않은 악용자가 LiteLLM 키 검증을 통과시키고 MCP 툴링에 대한 요청을 처리할 수 있게 됩니다.
조치: 1.84.0
긴급도: 높음
```

**llama3.2**

```
제품: LiteLLM 1.83.0
영향: LiteLLM proxy server의 MCP Streamable HTTP 엔드포인트를 사용하여 OAuth2 passthrough fallback path를 bypass할 수 있다.
조치: LiteLLM 1.84.0
긴급도: 높은
```

### CVE-2026-75650

**gpt-4.1-mini**

```
제품: Adobe Commerce  
영향: 공격자가 임의의 코드를 실행할 수 있음  
조치: 공지에 없음  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Adobe Commerce
영향: 공격자가 임의의 코드를 실행할 수 있다
조치: 공지에 없음
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Adobe Commerce
영향: 공격자는 현재 사용자의 컨텍스트에서 임의 코드를 실행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: Adobe Commerce
영향: 공격자가 현재 사용자 contexto에서 arbitrar리 코드를 실행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

### CVE-2026-49869

**gpt-4.1-mini**

```
제품: Kestra OSS 1.0.45 이전 및 1.3.21 이전 버전  
영향: 인증 없이 임의 워크플로우 생성 및 실행, 원격 코드 실행 가능  
조치: 1.0.45 및 1.3.21 이상으로 업데이트  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Kestra 버전 이전 1.0.45 및 1.3.21  
영향: 인증 없이 임의의 워크플로우 생성 및 실행, 원격 코드 실행 가능  
조치: 1.0.45 및 1.3.21  
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Kestra 1.0.45, 1.3.21
영향: 공격자는 API 경로의 마지막 부분이 configs인 경우를 확인하는 AuthenticationFilter를 통해 인증 없이 리모트 코드 실행을 수행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: Kestra OSS
영향: unauthenticated Remote Code Execution as root inside the Kestra worker container
조치: 1.0.45
긴급도: 높음
```

### CVE-2026-73570

**gpt-4.1-mini**

```
제품: Zimbra Collaboration (ZCS) 10.1.20 이전 버전, zimbra-snmp 패키지 설치 및 SNMP 알림 활성화 시  
영향: 인증되지 않은 공격자가 임의의 운영 체제 명령을 실행할 수 있음  
조치: 10.1.20  
긴급도: 긴급
```

**gpt-4.1-nano**

```
제품: Zimbra Collaboration 이전 버전
영향: 인증되지 않은 공격자가 임의의 운영체제 명령을 실행할 수 있음
조치: 공지에 없음
긴급도: 높음
```

**qwen2.5:3b**

```
제품: Zimbra Collaboration (ZCS) before 10.1.20
영향: 공격자는 Zimbra 사용자 권한으로서 임의 운영 체제 명령을 실행할 수 있다.
조치: 공지에 없음
긴급도: 높음
```

**llama3.2**

```
제품: Zimbra Collaboration (ZCS) before 10.1.20
영향: unauthenticated attacker가 arbitrary operating system commands를 실행할 수 있다.
조치: zimbra-snmp 패치
긴급도: 높음
```

