FROM alpine:3.16 as builder

RUN mkdir /opt/bin

WORKDIR /opt/bin

RUN apk update && apk add curl

RUN ARCH="$(apk --print-arch)"; \
	case "$ARCH" in \
		aarch64) export ARCH='arm64' ;; \
	esac; \
echo $ARCH; \
curl -LJ https://github.com/containernetworking/plugins/releases/download/v0.8.7/cni-plugins-linux-$ARCH-v0.8.7.tgz \
| tar zxv

FROM scratch

COPY --from=builder /opt/bin /opt/bin

