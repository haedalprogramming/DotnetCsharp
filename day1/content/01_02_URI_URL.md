# URI와 URL의 이해

# 목차
- [URI와 URL의 이해](#uri와-url의-이해)
- [목차](#목차)
  - [소개](#소개)
  - [1. URI (Uniform Resource Identifier)](#1-uri-uniform-resource-identifier)
    - [URI의 정의](#uri의-정의)
    - [URI의 구성 요소](#uri의-구성-요소)
    - [URI 예제](#uri-예제)
  - [2. URL (Uniform Resource Locator)](#2-url-uniform-resource-locator)
    - [URL의 정의](#url의-정의)
    - [URL의 구성 요소](#url의-구성-요소)
    - [URL 예제](#url-예제)
  - [3. URI와 URL의 차이점](#3-uri와-url의-차이점)
    - [URI와 URL의 관계](#uri와-url의-관계)
    - [예제 비교](#예제-비교)
  - [4. URI와 URL의 실제 사용 사례](#4-uri와-url의-실제-사용-사례)
    - [웹 브라우저에서의 사용](#웹-브라우저에서의-사용)
    - [API 요청에서의 사용](#api-요청에서의-사용)
  - [결론](#결론)
  - [출처](#출처)
  - [다음](#다음)

## 소개
웹 기술을 이해하는 데 있어 URI와 URL의 개념은 매우 중요합니다. 이 문서에서는 URI와 URL의 정의, 구성 요소, 차이점 및 예제를 살펴보겠습니다.

## 1. URI (Uniform Resource Identifier)

### URI의 정의
- **URI**는 인터넷에서 자원을 식별하는 문자열입니다.
- 모든 URL은 URI의 한 종류입니다, 하지만 모든 URI가 URL은 아닙니다.

### URI의 구성 요소
URI는 여러 구성 요소로 이루어질 수 있으며, 이들은 각기 다른 방식으로 자원을 식별합니다.
- **스킴 (Scheme)**: 자원에 접근하는 방법을 정의합니다. (예: `http`, `https`, `ftp`)
- **권한 (Authority)**: 자원의 호스트 정보를 포함합니다. (예: `example.com`)
- **경로 (Path)**: 자원의 위치를 나타냅니다. (예: `/path/to/resource`)
- **쿼리 (Query)**: 자원에 대한 추가 매개변수를 제공합니다. (예: `?key1=value1&key2=value2`)
- **프래그먼트 (Fragment)**: 자원의 일부를 참조합니다. (예: `#section1`)

### URI 예제
```text
http://example.com/path/to/resource?key1=value1&key2=value2#section1
```
- **스킴**: `http`
- **권한**: `example.com`
- **경로**: `/path/to/resource`
- **쿼리**: `key1=value1&key2=value2`
- **프래그먼트**: `#section1`

## 2. URL (Uniform Resource Locator)

### URL의 정의
- **URL**은 인터넷 상의 자원의 위치를 나타내는 URI의 한 형태입니다.
- URL은 자원에 접근하기 위한 방법과 자원의 위치를 포함합니다.

### URL의 구성 요소
URL은 URI와 유사한 구성 요소를 가지고 있으며, 자원에 접근하는 데 필요한 정보를 제공합니다.
- **스킴 (Scheme)**: 자원에 접근하는 프로토콜을 정의합니다. (예: `http`, `https`, `ftp`)
- **사용자 정보 (User Info)**: (선택 사항) 사용자 이름과 비밀번호를 포함할 수 있습니다. (예: `user:pass@`)
- **호스트 (Host)**: 자원의 호스트 정보를 포함합니다. (예: `example.com`)
- **포트 (Port)**: (선택 사항) 호스트와 연결할 포트를 지정합니다. (예: `:80`)
- **경로 (Path)**: 자원의 위치를 나타냅니다. (예: `/path/to/resource`)
- **쿼리 (Query)**: 자원에 대한 추가 매개변수를 제공합니다. (예: `?key1=value1&key2=value2`)
- **프래그먼트 (Fragment)**: 자원의 일부를 참조합니다. (예: `#section1`)

### URL 예제
```text
http://user:pass@example.com:80/path/to/resource?key1=value1&key2=value2#section1
```
- **스킴**: `http`
- **사용자 정보**: `user:pass@`
- **호스트**: `example.com`
- **포트**: `:80`
- **경로**: `/path/to/resource`
- **쿼리**: `key1=value1&key2=value2`
- **프래그먼트**: `#section1`

## 3. URI와 URL의 차이점

### URI와 URL의 관계
- **URI**는 자원을 식별하는 모든 방식을 포함하는 개념입니다.
- **URL**은 URI의 하위 개념으로, 자원의 위치를 구체적으로 명시합니다.

### 예제 비교
1. **URI**: `mailto:example@example.com`
   - 스킴: `mailto`
   - 이 URI는 이메일 주소를 식별합니다.
2. **URL**: `http://example.com/path/to/resource`
   - 스킴: `http`
   - 호스트: `example.com`
   - 경로: `/path/to/resource`
   - 이 URL은 웹 자원의 위치를 명시합니다.

## 4. URI와 URL의 실제 사용 사례

### 웹 브라우저에서의 사용
- **URL 입력**: 사용자가 브라우저 주소창에 URL을 입력하여 웹 페이지를 요청합니다.
- **링크**: 웹 페이지 내의 하이퍼링크는 다른 웹 페이지의 URL을 포함하여 클릭 시 해당 자원으로 이동합니다.

### API 요청에서의 사용
- **엔드포인트**: API 요청은 특정 자원의 위치를 나타내는 URL을 사용하여 서버와 통신합니다.
```text
GET https://api.example.com/users?id=123
```

## 결론
URI와 URL은 웹 상의 자원을 식별하고 접근하는 데 필수적인 개념입니다. URI는 자원을 식별하는 일반적인 방식이며, URL은 자원의 위치를 구체적으로 명시하는 URI의 한 형태입니다. 이러한 개념을 이해함으로써 웹 기술에 대한 전반적인 이해를 높일 수 있습니다.

## 출처
- [MDN Web Docs - URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)
- [Wikipedia - Uniform Resource Identifier](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)
- [W3C - URI/URL/URN 공식 문서](https://www.w3.org/Addressing/URL/uri-spec.html)

---
## [다음](./02_Backend_소개.md)

