FROM alpine:3
LABEL maintainer "Jacob Boomgaarden jake@pomeloproductions.com"

# Environment
ENV AWS_DEFAULT_REGION=us-east-1

# Install packages
RUN apk add --no-cache python3 py-pip py-setuptools ca-certificates git bash findutils groff less tini inotify-tools

RUN pip install python-magic \
  && git clone https://github.com/s3tools/s3cmd.git /tmp/s3cmd \
  && cd /tmp/s3cmd \
  && python3 /tmp/s3cmd/setup.py install \
  && cd / \
  && rm -rf /tmp/s3cmd \
  && apk del py-pip git

# Entrypoint
COPY entrypoint.sh /
ENTRYPOINT ["/sbin/tini", "--", "/entrypoint.sh"]
