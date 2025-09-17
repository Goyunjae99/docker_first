# 1단계: Git에서 소스 코드 클론
FROM alpine/git AS fetch
ARG GIT_URL="https://github.com/bence-toth/space-drifter.git"
WORKDIR /src
RUN git clone --depth=1 "$GIT_URL" app

# 2단계: Nginx로 정적 파일 서비스
FROM nginx:alpine
# space-drifter 레포의 루트에 index.html이 있으므로 그대로 복사
COPY --from=fetch /src/app/ /usr/share/nginx/html/
EXPOSE 80
