ARG BUILD_FROM
FROM rust:1-bookworm AS builder
RUN git clone --branch feat/local-hexa-segments --depth 1 https://github.com/pixelowaty/govee2mqtt.git /src
WORKDIR /src
RUN cargo build --release

FROM $BUILD_FROM
COPY run.sh /run.sh
COPY --from=builder /src/target/release/govee /app/govee
COPY --from=builder /src/assets /app/assets/
COPY --from=builder /src/AmazonRootCA1.pem /app/
CMD [ "/run.sh" ]
