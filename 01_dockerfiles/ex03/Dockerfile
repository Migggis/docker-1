FROM debian
RUN	apt update -y && \
	apt upgrade -y && \
	apt install -y tzdata && \
	apt install -y curl openssh-server openssl ca-certificates && \
	apt install -y postfix && \
	sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	echo 'root:hive' | chpasswd && \
	curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install gitlab-ce && \
	rm -rf script.deb.sh && \
	mkdir -p /etc/gitlab/ssl && \
	chmod 700 /etc/gitlab/ssl && \
	openssl req -x509 -nodes -days 365 -newkey rsa:4096 \
	-subj /C=FI/ST=./L=Helsinki/O=./OU=./CN=192.168.99.100/emailAddress=mkarkaus@student.hive.fi \
	-keyout /etc/gitlab/ssl/selfsigned.key -out /etc/gitlab/ssl/selfsigned.crt && \
	echo "external_url \"https://192.168.99.100\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/selfsigned.crt\"" >> /etc/gitlab/gitlab.rb && \
	echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/selfsigned.key\"" >> /etc/gitlab/gitlab.rb && \
	echo "gitlab_rails['gitlab_shell_ssh_port'] = 8022" >> /etc/gitlab/gitlab.rb
EXPOSE 22 80 443
ENTRYPOINT  service ssh start && \
			(/opt/gitlab/embedded/bin/runsvdir-start &) && \
			gitlab-ctl reconfigure && \
			tail -f /dev/null
# docker run -it --privileged -p 80:80 -p 8022:22 -p 443:443 --name gitlab gitlab
# passphrase of the rsa key is 'miikka'
# GIT_SSL_NO_VERIFY=true git clone https://192.168.99.100/root/projekti.git
