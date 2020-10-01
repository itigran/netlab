FROM centos:latest
RUN yum install -y openssh-server openssl net-tools tcpdump nc nmap bind-utils
ADD ssh_host_rsa_key /etc/ssh/ssh_host_rsa_key
ADD ssh_host_ecdsa_key /etc/ssh/ssh_host_ecdsa_key
ADD ssh_host_ed25519_key /etc/ssh/ssh_host_ed25519_key

RUN mkdir /var/run/sshd
RUN echo 'root:w34kP@s$' | chpasswd
RUN sed -i 's/#*PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

ENV NOTVISIBLE="in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

CMD ["/usr/sbin/sshd", "-D"]
