# For development or CI, build from local Dockerfile (.travis.yml will update base before tests)
# For production, download prebuilt image
FROM monogramm/docker-frappe:13-debian

COPY docker_test.sh /docker_test.sh

RUN set -ex; \
    test 'debian' = 'debian-slim' && sudo apt-get update && sudo apt-get install -y --allow-unauthenticated iputils-ping; \
    sudo chmod 755 /docker_test.sh; \
    sudo pip install coverage==4.5.4; \
    sudo pip install python-coveralls

# TODO QUnit (JS) Unit tests
EXPOSE 4444

# Default Chrome configuration
ENV DISPLAY=:20.0 \
    SCREEN_GEOMETRY="1440x900x24" \
    CHROMEDRIVER_PORT=4444 \
    CHROMEDRIVER_WHITELISTED_IPS="127.0.0.1" \
    CHROMEDRIVER_URL_BASE='' \
    CHROMEDRIVER_EXTRA_ARGS=''

CMD ["/docker_test.sh"]
