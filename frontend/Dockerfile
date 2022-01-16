FROM golang AS stage_0
RUN go env -w CGO_ENABLED=0; \
    go env -w GO111MODULE=on; \
    go env -w GOPROXY=https://goproxy.cn,direct; \
    apt-get update && apt-get install -y git; \
    git clone https://github.com/xddxdd/bird-lg-go.git /bird-lg-go
WORKDIR /bird-lg-go/frontend
RUN go build -ldflags "-w -s" -o frontend

FROM scratch AS stage_1
COPY --from=stage_0 /bird-lg-go/frontend/frontend /frontend
ENTRYPOINT [ "/frontend", "--servers=lax1-us,zrh1-ch,noyesix", "--domain=bugsur.xyz", "--proxy-port=7787", "--listen=${PORT}" ]
