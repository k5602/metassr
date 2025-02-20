# Build image
FROM debian:bookworm-slim AS builder

# Image descriptor
LABEL copyright.name="Vicente Eduardo Ferrer Garcia" \
	copyright.address="vic798@gmail.com" \
	maintainer.name="Vicente Eduardo Ferrer Garcia" \
	maintainer.address="vic798@gmail.com" \
	vendor="MetaCall Inc." \
	version="0.1"

# Install wrk dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
	build-essential \
	libssl-dev \
	git \
	zlib1g-dev \
	ca-certificates

# Build wrk2
RUN git clone https://github.com/giltene/wrk2.git \
	&& cd wrk2 && make -j$(grep -c processor /proc/cpuinfo)

# Client image
FROM debian:bookworm-slim AS client

# Install wrk dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
	libssl3 \
	ca-certificates

# Copy wrk executable
COPY --from=builder /wrk2/wrk /usr/bin

# Raise the limits to successfully run benchmarks
RUN ulimit -c -m -s -t unlimited

# Copy wrk scripts
COPY scripts /usr/bin

# Entry point
ENTRYPOINT ["/usr/bin/wrk"]
