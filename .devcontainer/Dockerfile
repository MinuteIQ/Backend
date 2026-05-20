FROM openjdk:24-ea-oraclelinux9

ARG INSTALL_MAVEN="false"
ARG MAVEN_VERSION=""

ARG INSTALL_GRADLE="true"
ARG GRADLE_VERSION="8.14"

RUN apt-get update && apt-get install -y curl unzip

RUN if [ "${INSTALL_MAVEN}" = "true" ]; then \
        curl -fsSL "https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz" \
        | tar -xz -C /opt && \
        ln -s /opt/apache-maven-${MAVEN_VERSION}/bin/mvn /usr/local/bin/mvn; \
    fi && \
    if [ "${INSTALL_GRADLE}" = "true" ]; then \
        curl -fsSL "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" -o /tmp/gradle.zip && \
        unzip -q /tmp/gradle.zip -d /opt && \
        ln -s /opt/gradle-${GRADLE_VERSION}/bin/gradle /usr/local/bin/gradle && \
        rm /tmp/gradle.zip; \
    fi
