FROM ruby
ONBUILD RUN	gem install git && \
	gem install rails && \
	wget https://yarnpkg.com/latest.tar.gz && \
	tar xf latest.tar.gz --directory /usr/local --strip-components 1 && \
	rm -rf latest.tar.gz && \
	wget https://nodejs.org/dist/v12.16.0/node-v12.16.0-linux-x64.tar.gz && \
	tar xf node-v12.16.0-linux-x64.tar.gz --directory /usr/local --strip-components 1 && \
	rm -rf node-v12.16.0-linux-x64.tar.gz && \
	rails new myapp && \
	cp -rf myapp /opt/app && \
	cd myapp && \
	rake db:migrate
ONBUILD WORKDIR /myapp/
#	docker build ex02 -t ft-rails:on-build
#	docker build . -t childdocker
#	docker run -d -p 3000:3000 --name myapp childdocker
