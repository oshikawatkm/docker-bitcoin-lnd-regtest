FROM golang:1.23.2 as builder

RUN git clone https://github.com/btcsuite/btcd.git /src/btcd
WORKDIR /src/btcd

RUN go install . ./cmd/...

FROM debian:bookworm-slim
COPY --from=builder /go/bin/btcd /usr/local/bin/btcd
COPY --from=builder /go/bin/btcctl /usr/local/bin/btcctl
ENTRYPOINT ["btcd"]