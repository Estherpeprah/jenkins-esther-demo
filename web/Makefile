version = esther-1.1
image = 401413892014.dkr.ecr.us-east-1.amazonaws.com/webapp:$(version)

login:
	aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 401413892014.dkr.ecr.us-east-1.amazonaws.com

build:
	@docker build -t $(image) .

push: login
	@# docker login is not here
	@docker push $(image)

deploy:
	@cat deployment.yaml | sed "s|IMAGEVERSION|$(version)|g;s|NAMSPACE|$(namespace)g" | kubectl apply -f -
