# Nginx 기반의 간단한 웹 서버 이미지

# 1. 기반 이미지
FROM nginx:latest

# 2. (선택 사항) 메타데이터
LABEL maintainer="your_email@example.com"

# 3. (선택 사항) 작업 디렉토리 (Nginx는 기본적으로 /usr/share/nginx/html 사용)
# WORKDIR /usr/share/nginx/html

# 4. 정적 HTML 파일 복사
COPY index.html /usr/share/nginx/html/

# 5. (선택 사항) 포트 노출
EXPOSE 80

# 6. (선택 사항) 기본 명령어 (Nginx는 이미 기본 명령어 설정되어 있음)
# CMD ["nginx", "-g", "daemon off;"]
