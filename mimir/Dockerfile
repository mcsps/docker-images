FROM busybox:uclibc as builder
FROM grafana/mimirtool:2.17.0 as mimirtool
FROM grafana/mimir:2.17.0
COPY --from=builder /bin/sh /bin/sh
COPY --from=builder /bin/busybox /bin/busybox
COPY --from=mimirtool  /bin/mimirtool  /bin/mimirtool
RUN ["/bin/busybox", "--install", "/bin"]
CMD ["/bin/sh"]
