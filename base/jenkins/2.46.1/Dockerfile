FROM openjdk:8-jdk

LABEL maintainer="phithon <root@leavesongs.com>"

RUN apt-get update \
    && apt-get install --no-install-recommends -y git curl wget ca-certificates \
    && rm -rf /var/lib/apt/lists/*

ENV JENKINS_HOME /var/jenkins_home
ENV COPY_REFERENCE_FILE_LOG $JENKINS_HOME/copy_reference_file.log

RUN groupadd -g 1000 jenkins \
    && useradd -d "$JENKINS_HOME" -u 1000 -g 1000 -m -s /bin/bash jenkins

ENV JENKINS_VERSION 2.46.1
RUN set -ex \
    && [ -e /usr/share/jenkins ] || mkdir -p /usr/share/jenkins \
    && [ -e /usr/share/jenkins/ref ] || mkdir -p /usr/share/jenkins/ref \
    && curl -#SL http://mirrors.jenkins.io/war-stable/${JENKINS_VERSION}/jenkins.war -o /usr/share/jenkins/jenkins.war \
    && chown -R jenkins "$JENKINS_HOME" /usr/share/jenkins/ref

EXPOSE 8080
EXPOSE 50000

COPY jenkins.sh /usr/local/bin/jenkins.sh

RUN chmod +x /usr/local/bin/jenkins.sh

USER jenkins

CMD ["/usr/local/bin/jenkins.sh"]