# Spring Security FilterChain 순서 (주요 필터 기준)

| 순서 | 필터 클래스                                    | 역할                                                          |
| -- | ----------------------------------------- | ----------------------------------------------------------- |
| 1  | `SecurityContextPersistenceFilter`        | 이전 요청에서 저장된 `SecurityContext` 복원 또는 새로 생성                   |
| 2  | `HeaderWriterFilter`                      | 보안 헤더(`X-Frame-Options`, `X-Content-Type-Options` 등) 추가     |
| 3  | `CsrfFilter`                              | CSRF 토큰 검사                                                  |
| 4  | **`JwtFilter`** (커스텀)                     | `Authorization` 헤더에서 JWT 추출 및 검증 후 인증 설정                    |
| 5  | `UsernamePasswordAuthenticationFilter`    | **폼 로그인 처리 필터** (`/login`에서 ID/PW 인증 수행)                    |
| 6  | `BasicAuthenticationFilter`               | HTTP Basic 인증 처리                                            |
| 7  | `RequestCacheAwareFilter`                 | 인증 후 원래 요청했던 URL 저장 및 복원 처리                                 |
| 8  | `SecurityContextHolderAwareRequestFilter` | `HttpServletRequest`에 인증 관련 메서드 (`getUserPrincipal()` 등) 추가 |
| 9  | `AnonymousAuthenticationFilter`           | 인증되지 않은 사용자를 **익명 사용자**로 설정                                 |
| 10 | `SessionManagementFilter`                 | 세션 생성, 유효성 검사, 세션 고정 보호 설정 등                                |
| 11 | `ExceptionTranslationFilter`              | 인증/인가 실패 예외 처리 → `AuthenticationEntryPoint` 등 호출            |
| 12 | `FilterSecurityInterceptor`               | 최종 권한 검사 (인가 처리) – `@PreAuthorize`나 `hasRole()` 등의 정책 적용    |
| 13 | `SwitchUserFilter` (선택적)                  | 관리자 전환 로그인 기능 지원                                            |
