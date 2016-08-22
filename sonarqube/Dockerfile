FROM redpine42/java8

MAINTAINER Dan Brown <danb@redpine.com>

ENV SONAR_VERSION=6.0 \
    SONARQUBE_HOME=/opt/sonarqube \
    # Database configuration
    # Defaults to using H2
    SONARQUBE_JDBC_USERNAME=sonar \
    SONARQUBE_JDBC_PASSWORD=sonar \
    SONARQUBE_JDBC_URL=

RUN yum install -y wget 

RUN cd /opt && \
    wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-$SONAR_VERSION.zip && \
    unzip sonarqube-$SONAR_VERSION.zip && \
    mv sonarqube-$SONAR_VERSION sonarqube && \
    rm sonarqube-$SONAR_VERSION.zip

RUN wget https://sonarsource.bintray.com/Distribution/sonar-java-plugin/sonar-java-plugin-4.1.jar && \
    mv sonar-java-plugin-4.1.jar $SONARQUBE_HOME/extensions/plugins/

RUN wget https://github.com/SonarQubeCommunity/sonar-findbugs/releases/download/3.4/sonar-findbugs-plugin-3.4.3.jar && \
    mv sonar-findbugs-plugin-3.4.3.jar $SONARQUBE_HOME/extensions/plugins/

RUN wget https://sonarsource.bintray.com/Distribution/sonar-groovy-plugin/sonar-groovy-plugin-1.4.jar && \
    mv sonar-groovy-plugin-1.4.jar $SONARQUBE_HOME/extensions/plugins/

RUN wget http://sonarsource.bintray.com/Distribution/sonar-javascript-plugin/sonar-javascript-plugin-2.15.jar && \
    mv sonar-javascript-plugin-2.15.jar $SONARQUBE_HOME/extensions/plugins/

RUN wget https://sonarsource.bintray.com/Distribution/sonar-web-plugin/sonar-web-plugin-2.4.jar && \
    mv sonar-web-plugin-2.4.jar  $SONARQUBE_HOME/extensions/plugins/


VOLUME ["$SONARQUBE_HOME/data", "$SONARQUBE_HOME/extensions"]

WORKDIR $SONARQUBE_HOME

COPY run.sh $SONARQUBE_HOME/bin/

ADD QualityProfiles $SONARQUBE_HOME/QualityProfiles

ENTRYPOINT ["/opt/sonarqube/bin/run.sh"]