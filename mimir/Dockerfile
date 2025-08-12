FROM busybox:uclibc as builder
FROM grafana/mimirtool:2.16.1 as mimirtool
FROM grafana/mimir:r350-d2a17f27
COPY --from=builder /bin/sh /bin/sh
COPY --from=builder /bin/busybox /bin/busybox
COPY --from=mimirtool  /bin/mimirtool  /bin/mimirtool
RUN ["/bin/busybox", "--install", "/bin"]
CMD ["/bin/sh"]
