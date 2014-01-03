FROM centos:latest

RUN rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -iUvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN yum -y update

RUN yum -y install openssh-server supervisor

RUN echo 'root:p4ssw0rd' | chpasswd

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#Use PAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN /usr/bin/ssh-keygen -q -t rsa1 -f /etc/ssh/ssh_host_key -C '' -N '' >& /dev/null
RUN chmod 600 /etc/ssh/ssh_host_key
RUN chmod 644 /etc/ssh/ssh_host_key.pub

RUN /usr/bin/ssh-keygen -q -t rsa -f /etc/ssh/ssh_host_rsa_key -C '' -N '' >& /dev/null
RUN chmod 600 /etc/ssh/ssh_host_rsa_key
RUN chmod 644 /etc/ssh/ssh_host_rsa_key.pub

RUN /usr/bin/ssh-keygen -q -t dsa -f /etc/ssh/ssh_host_dsa_key -C '' -N '' >& /dev/null
RUN chmod 600 /etc/ssh/ssh_host_dsa_key
RUN chmod 644 /etc/ssh/ssh_host_dsa_key.pub

EXPOSE 22

ADD supervisord.conf /etc/supervisor/supervisord.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
