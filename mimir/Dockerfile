FROM busybox:uclibc as builder
FROM grafana/mimirtool:3.0.3 as mimirtool
FROM grafana/mimir:3.0.0
COPY --from=builder /bin/sh /bin/sh
COPY --from=builder /bin/busybox /bin/busybox
COPY --from=mimirtool  /bin/mimirtool  /bin/mimirtool
RUN ["/bin/busybox", "--install", "/bin"]
CMD ["/bin/sh"]
