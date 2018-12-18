FROM jenkins/jenkins:lts

# Install Jenkins plugins
COPY jenkins-plugins.txt /usr/share/jenkins/ref/jenkins-plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/jenkins-plugins.txt


# if we want to install via apt
USER root

RUN apt-get update && apt-get install -y ruby ruby-dev gcc g++ make
RUN gem install bundler jekyll

# Prep for html-sites volume
RUN mkdir -p /mnt/html-sites && chown jenkins:jenkins -R /mnt/html-sites

# Update permissions on Ruby gems folder to allow builds to install new plugins
RUN chown -R root:jenkins /usr/lib/ruby/gems && chmod 770 -R /usr/lib/ruby/gems
RUN chown -R root:jenkins /var/lib/gems && chmod 770 -R /var/lib/gems


# drop back to the regular jenkins user - good practice
USER jenkins