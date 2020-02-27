FROM debian:10
RUN apt update -y && \
	apt upgrade -y && \
	apt install -y wget openssh-server && \
	useradd -p miikka vpn && \
	usermod -aG sudo vpn && \
	wget -P ~/ https://github.com/OpenVPN/easy-rsa/releases/download/v3.0.6/EasyRSA-unix-v3.0.6.tgz && \
	cd ~ && \
	mkdir volume && \
	tar xvf ~/EasyRSA-unix-v3.0.6.tgz && \
	cd ~/EasyRSA-v3.0.6 && \
	cp vars.example vars && \
	sed -i 's/#set_var EASYRSA_REQ_COUNTRY/set_var EASYRSA_REQ_COUNTRY/' ~/EasyRSA-v3.0.6/vars && \
	sed -i 's/#set_var EASYRSA_REQ_PROVINCE/set_var EASYRSA_REQ_PROVINCE/' ~/EasyRSA-v3.0.6/vars && \
	sed -i 's/#set_var EASYRSA_REQ_CITY/set_var EASYRSA_REQ_CITY/' ~/EasyRSA-v3.0.6/vars && \
	sed -i 's/#set_var EASYRSA_REQ_ORG/set_var EASYRSA_REQ_ORG/' ~/EasyRSA-v3.0.6/vars && \
	sed -i 's/#set_var EASYRSA_REQ_EMAIL/set_var EASYRSA_REQ_EMAIL/' ~/EasyRSA-v3.0.6/vars && \
	sed -i 's/#set_var EASYRSA_REQ_OU/set_var EASYRSA_REQ_OU/' ~/EasyRSA-v3.0.6/vars
CMD cd ~/EasyRSA-v3.0.6 && \
	./easyrsa init-pki && \
	echo -en "\n" | ./easyrsa build-ca nopass && \
	./easyrsa import-req ~/volume/server.req server && \
	echo -en "yes\n" | ./easyrsa sign-req server server && \
	tail -f /dev/null
# docker run -d --name ca-cert -v vpn:~/volume ca-cert 
