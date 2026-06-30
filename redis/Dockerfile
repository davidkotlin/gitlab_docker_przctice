# 使用你指定的穩定版基底
FROM ubuntu:22.04

# 避免安裝過程卡在時區選擇
ARG DEBIAN_FRONTEND=noninteractive

# 更新並安裝 Redis 伺服器，然後清空 apt 快取瘦身
RUN apt-get update && apt-get install -y redis-server && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# 把剛剛寫好的自訂設定檔，複製到容器內的標準目錄，並覆蓋原本的預設檔
COPY gitlab_redis.conf /etc/redis/redis.conf

# 宣告對外開放的標準 Port (Redis 預設是 6379)
EXPOSE 6379

# 容器啟動時執行的指令：啟動 Redis 並明確指定吃我們剛放進去的設定檔
CMD ["redis-server", "/etc/redis/redis.conf"]
