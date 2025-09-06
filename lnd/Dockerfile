FROM golang:1.24.6 as builder

# LND ソースを取得
RUN git clone https://github.com/lightningnetwork/lnd.git /src/lnd
WORKDIR /src/lnd

# ビルド
RUN make && make install

# 実行ステージ
FROM debian:bookworm-slim
COPY --from=builder /go/bin/* /usr/local/bin/
ENTRYPOINT ["lnd"]