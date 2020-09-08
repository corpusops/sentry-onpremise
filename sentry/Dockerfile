ARG SENTRY_IMAGE
FROM ${SENTRY_IMAGE}
## divergences
ENV EXTRA_BUILD_PACKAGES="libsasl2-dev libldap2-dev make build-essential git"
RUN bash -c 'apt-get update -qq && apt-get install -y libldap-2.4-2 libsasl2-2 git $EXTRA_BUILD_PACKAGES'
## end: divergences

COPY . /usr/src/sentry

# Hook for installing additional plugins
RUN if [ -s /usr/src/sentry/requirements.txt ]; then pip install -r /usr/src/sentry/requirements.txt; fi

## divergences
RUN bash -c ' rm -rf /var/lib/apt/lists/* && apt-get clean -qq \
    && apt-get remove --purge -y $EXTRA_BUILD_PACKAGES \
    && apt-get autoremove --purge -y'
## end: divergences
