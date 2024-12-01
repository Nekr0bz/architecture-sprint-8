FROM python:3.11.9-slim as python-stage
ENV PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_ROOT_USER_ACTION=ignore \
    PYTHONPYCACHEPREFIX=/tmp/

FROM python-stage as requirements-stage
WORKDIR /tmp/
COPY req.txt /tmp/

FROM python-stage as base-stage
WORKDIR /code/API/
ENV PYTHONPATH=$PYTHONPATH:/code/API/src/
COPY --from=requirements-stage /tmp/req.txt req.txt
RUN pip install --no-cache-dir --upgrade -r req.txt
COPY src ./src/

FROM base-stage as api-stage