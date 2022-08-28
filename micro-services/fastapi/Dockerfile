# Dockerfile to build fastapi application as a docker image
# 
# Author: sreejith.naarakathil@gmail.com
#
# $ docker run --network="host" -ti --rm fastapi-srv:1.0.1
ARG DISTRO_VERSION=3.10.6-alpine3.16
FROM python:${DISTRO_VERSION} AS base

# Create separate targets for each phase, this allows us to cache intermediate
# stages and makes the final deployment stage
# small as it contains only what is needed.
FROM base AS devtools

# Install the typical development tools and some additions:
RUN apk update && \
    apk add \
	py3-pip

# Copy the source code to /app and compile it.
FROM devtools AS build
# Build additional app components any in this environment
WORKDIR /app
COPY . /app
# RUN pip install fastapi
# RUN pip install uvicorn

# Create the final deployment image, using `alpine`as the starting point.
FROM python:${DISTRO_VERSION} AS final
RUN apk update && \
    apk add \
	py3-pip
RUN pip install fastapi
RUN pip install uvicorn

# Copy the program and shared libraries from the previously created stage and make it the entry point.
WORKDIR /app
COPY --from=build /app /app

ENTRYPOINT ["python3"]
CMD ["-m", "uvicorn", "--host", "0.0.0.0", "--port", "8080", "main:app"]

