FROM busybox:uclibc as builder
FROM grafana/mimirtool:r365-00292cd4 as mimirtool
FROM grafana/mimir:r365-00292cd4
COPY --from=builder /bin/sh /bin/sh
COPY --from=builder /bin/busybox /bin/busybox
COPY --from=mimirtool  /bin/mimirtool  /bin/mimirtool
RUN ["/bin/busybox", "--install", "/bin"]
CMD ["/bin/sh"]
