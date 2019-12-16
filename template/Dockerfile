FROM azul/zulu-openjdk-alpine:7u232

ARG LABEL_BUILD_DATE
ARG LABEL_NAME
ARG LABEL_VCS_REF
ARG LABEL_VERSION

COPY scripts/* /usr/local/bin/

RUN adduser -D -h /home/liferay liferay && addgroup liferay liferay

COPY --chown=liferay:liferay home/.bashrc /home/liferay/
COPY --chown=liferay:liferay liferay /opt/liferay

COPY --chown=liferay:liferay ./mysql-connector-java-5.1.48.jar /opt/liferay/tomcat-7.0.62/lib/ext/
COPY --chown=liferay:liferay ./portal-ext.properties /opt/liferay/
COPY --chown=liferay:liferay ./ROOT.xml /opt/liferay/tomcat-7.0.62/conf/Catalina/localhost/

ENTRYPOINT /usr/local/bin/liferay_entrypoint.sh

ENV LIFERAY_HOME=/opt/liferay
ENV LIFERAY_JPDA_ENABLED=false
ENV LIFERAY_JVM_OPTS=
ENV LIFERAY_PRODUCT_NAME="${LABEL_NAME}"

ENV LIFERAY_SETUP_PERIOD_WIZARD_PERIOD_ADD_PERIOD_SAMPLE_PERIOD_DATA=false
ENV LIFERAY_SETUP_PERIOD_WIZARD_PERIOD_ENABLED=false
ENV LIFERAY_TERMS_PERIOD_OF_PERIOD_USE_PERIOD_REQUIRED=false
ENV LIFERAY_USERS_PERIOD_REMINDER_PERIOD_QUERIES_PERIOD_ENABLE=false
#ENV HTTP_PROXY "http://proxy.reply.it:8080"
#ENV HTTPS_PROXY "http://proxy.reply.it:8080"

EXPOSE 8000 8009 8080 11311

HEALTHCHECK \
	--interval=1m \
	--start-period=1m \
	--timeout=1m \
	CMD curl -fsS "http://localhost:8080/c/portal/layout" || exit 1

LABEL org.label-schema.build-date="${LABEL_BUILD_DATE}"
LABEL org.label-schema.name="${LABEL_NAME}"
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.vcs-ref="${LABEL_VCS_REF}"
LABEL org.label-schema.vcs-url="https://github.com/liferay/liferay-docker"
LABEL org.label-schema.vendor="Liferay, Inc."
LABEL org.label-schema.version="${LABEL_VERSION}"

RUN apk add bash curl nss tomcat-native tree ttf-dejavu

USER liferay:liferay

WORKDIR /opt/liferay