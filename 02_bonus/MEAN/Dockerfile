FROM ubuntu
RUN apt update -y && \
	apt upgrade -y && \
	apt install -y build-essential systemd url git fontconfig libpng-dev ruby ruby-dev && \
	gem install sass && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
	echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" \
	| tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
	apt install -y mongodb && \
	curl -sL https://deb.nodesource.com/setup_13.x | bash && \
	apt install -y nodejs && \
	npm install -g yarn && \
	npm install -g gulp && \
	git clone https://github.com/meanjs/mean.git && \
	cd mean && \
	npm install && \
	yarn install --allow-root
ENTRYPOINT systemctl start mongod && \
			npm start
