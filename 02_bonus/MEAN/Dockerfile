FROM ubuntu
ADD . /app
WORKDIR /app
RUN apt update -y && \
	apt upgrade -y && \
	apt install -y build-essential curl npm systemd git libpng-dev ruby ruby-dev && \
	gem install sass && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
	echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" \
	| tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
	apt install -y mongodb && \
	curl -sL https://deb.nodesource.com/setup_13.x | bash && \
	apt install -y nodejs && \
	npm install && \
	npm install -g bower && \
	npm install -g gulp && \
	git clone https://github.com/meanjs/mean.git && \
	cd mean && \
	bower install --allow-root && \
	npm install -g nodemon && \
	rm -rf node_modules && \
	npm install -g npm@latest && \
	npm i core-util-is
EXPOSE 3000
CMD	cd mean && \
	service mongodb start && \
	nodemon server.js
# docker build . -t mean
# docker run -it --name means -p 3000:3000 mean
