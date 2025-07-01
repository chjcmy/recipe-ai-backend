# 🚀 Recipe AI - TypeScript Backend

NestJS 기반 AI 레시피 추천 시스템 백엔드

## 📋 프로젝트 개요

**기술 스택**: NestJS + TypeScript + MongoDB + Redis + Elasticsearch + LangChain + Ollama
**핵심 기능**: 실시간 AI 채팅, 개인화 레시피 추천, 알레르기 필터링, WebSocket 통신

## 🏗 아키텍처

```
WebSocket Gateway ←→ LangChain Service ←→ Redis Memory
        ↓                    ↓                ↓
   실시간 채팅        AI 개인화 응답      대화 기록 저장
        ↓                    ↓                ↓
   Auth Service      Elasticsearch     MongoDB
   (사용자 관리)        (레시피 검색)    (사용자 데이터)
```

## 🚀 주요 기능

### 1. **실시간 AI 채팅 시스템**
- WebSocket 기반 실시간 통신
- LangChain ConversationChain 활용
- 스트리밍 응답으로 UX 최적화

### 2. **개인화 AI 서비스**
- 사용자별 알레르기 정보 자동 필터링
- 요리 실력별 맞춤 레시피 추천
- Redis 기반 대화 컨텍스트 유지

### 3. **안전한 레시피 검색**
- Elasticsearch 기반 고성능 검색
- 알레르기 위험도 점수 계산
- 다중 필드 검색 (이름, 재료, 설명)

### 4. **사용자 인증 & 관리**
- JWT 기반 보안 인증
- bcrypt 비밀번호 해싱
- 사용자별 프로필 관리

## 🔧 주요 모듈

### **AuthModule** - 사용자 인증
```typescript
POST /api/auth/register     # 회원가입
POST /api/auth/login        # 로그인  
GET  /api/auth/profile      # 프로필 조회
PUT  /api/auth/allergies    # 알레르기 정보 업데이트
```

### **WebSocketModule** - 실시간 채팅
```typescript
'send-personal-message'     # 메시지 전송
'join-personal-chat'        # 채팅방 입장
'clear-chat-history'        # 대화 기록 삭제
```

### **LangChainModule** - AI 서비스
```typescript
- RAG 기반 레시피 검색
- 개인화 컨텍스트 적용
- Redis 메모리 관리
```

## 🛠 기술적 특징

### **1. Redis 기반 커스텀 메모리**
```typescript
class RedisConversationMemory extends BaseMemory {
  // LangChain과 완벽 연동
  // 사용자별 독립 메모리 공간
  // 최근 20개 메시지 유지
}
```

### **2. 알레르기 안전 필터링**
```typescript
async searchSafeRecipes(query, options) {
  // Elasticsearch 검색 + 알레르기 필터
  // 위험도 점수 계산
  // 안전한 레시피만 반환
}
```

### **3. 스트리밍 AI 응답**
```typescript
async *streamResponse() {
  // 실시간 청크별 전송
  // WebSocket을 통한 즉시 응답
  // 사용자 경험 최적화
}
```

## 🐳 Docker 배포

### **로컬 개발 환경**
```bash
npm run start:dev
```

### **Docker 배포**
```bash
docker-compose up -d
```

## 📊 API 문서

서버 실행 후 접속: `http://localhost:8081/api/docs`

## 🔗 연동 서비스

- **MongoDB**: 사용자 데이터, 설정
- **Redis**: 대화 기록, 캐시  
- **Elasticsearch**: 레시피 검색
- **Ollama**: AI 모델 (Gemma3)

## 🎯 핵심 차별점

1. **완전한 개인화**: 사용자별 알레르기/선호도 고려
2. **실시간 스트리밍**: WebSocket + LangChain 연동
3. **안전성 우선**: 알레르기 필터링 시스템
4. **확장 가능한 구조**: 모듈형 아키텍처

---

**📧 Contact**: 바카티오 Backend Engineer 지원용 포트폴리오
**🚀 Status**: 프로덕션 배포 준비 완료
