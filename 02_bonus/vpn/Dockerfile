FROM debian:10
WORKDIR ~/
RUN apt update -y && \
	apt upgrade -y && \
	apt install -y openssh-server openvpn && \
	mkdir volume && \
	useradd -p miikka vpn && \
	usermod -aG sudo vpn && \
	wget -P ~/ https://github.com/OpenVPN/easy-rsa/releases/download/v3.0.6/EasyRSA-unix-v3.0.6.tgz && \
	tar xvf EasyRSA-unix-v3.0.6.tgz && \

CMD	cd EasyRSA-v3.0.6/ && \
	./easyrsa init-pki && \
	./easyrsa gen-req server nopass && \
	cp ~/EasyRSA-v3.0.6/pki/private/server.key /etc/openvpn/ && \
	cp ~/EasyRSA-v3.0.6/pki/reqs/server.req ~/volume && \


# docker build . -t vpn
# docker run -d --name vpn -v vpn:~/volume -e vpn
