# --- 1단계: 소스 클론 + 빌드 ---
FROM node:18-alpine AS builder
ARG GIT_URL="https://github.com/gorisanson/pikachu-volleyball.git"
WORKDIR /build
RUN apk add --no-cache git
RUN git clone --depth=1 "$GIT_URL" app
WORKDIR /build/app
# lock 파일이 있으면 ci, 없으면 install
RUN npm ci || npm install
# JS 번들 생성 (dist/)
RUN npm run build

# --- 2단계: 런타임 (Nginx) ---
FROM nginx:alpine
# 빌드 산출물만 복사 → 가볍고 빠름
COPY --from=builder /build/app/dist/ /usr/share/nginx/html/
EXPOSE 80
# nginx 기본 CMD 사용
