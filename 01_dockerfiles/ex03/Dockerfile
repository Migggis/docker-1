FROM debian
RUN	apt update -y && \
	apt upgrade -y && \
	apt install -y tzdata && \
	apt install -y curl openssh-server ca-certificates && \
	apt install -y postfix && \
	curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
	apt-get install gitlab-ce && \
	rm -rf script.deb.sh
EXPOSE 22 80 443 
ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null
# docker run -it --privileged -p 8080:80 -p 8022:22 -p 8443:443 --name gitlab gitlab
