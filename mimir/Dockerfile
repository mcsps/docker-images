FROM busybox:uclibc as builder

FROM grafana/mimir:r350-d2a17f27
COPY --from=builder /bin/sh /bin/sh
COPY --from=builder /bin/busybox /bin/busybox
RUN ["/bin/busybox", "--install", "/bin"]
CMD ["/bin/sh"]
