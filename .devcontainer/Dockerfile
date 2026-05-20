FROM eclipse-temurin:24-jdk-noble

RUN apt-get update && apt-get install -y curl unzip git && rm -rf /var/lib/apt/lists/*

# Install latest Gradle
# RUN GRADLE_VERSION=$(curl -s https://services.gradle.org/versions/current \
#         | grep -o '"version":"[^"]*"' \
#         | cut -d'"' -f4) && \
#     curl -fsSL "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" -o /tmp/gradle.zip && \
#     unzip -q /tmp/gradle.zip -d /opt && \
#     ln -s /opt/gradle-${GRADLE_VERSION}/bin/gradle /usr/local/bin/gradle && \
#     rm /tmp/gradle.zip

# Pre-warm the Gradle dependency cache into the image layer.
# The build context is the project root, so these files are available.
# This means switching codespace instances won't re-download your entire dependency tree.
WORKDIR /tmp/project
COPY build.gradle.kts gradlew ./
COPY gradle/ gradle/
COPY settings.gradle* ./
RUN chmod +x gradlew && ./gradlew dependencies --no-daemon --quiet 2>/dev/null || true

WORKDIR /workspaces
