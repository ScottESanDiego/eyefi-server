FROM ubuntu:18.04

WORKDIR /root

RUN apt update \
	&& apt install -y wget build-essential python-dev python-pyexiv2 python-setuptools \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget https://launchpad.net/eyefi/trunk/0.2/+download/eyefi-0.2.tar.gz \
	&& tar xf eyefi-0.2.tar.gz \
	&& rm eyefi-0.2.tar.gz

WORKDIR /root/eyefi-0.2

RUN sed -i s/\"Twisted-Web\"\,\ \"Twisted-Core\"\,/\"twisted\"\,/ setup.py \
	&& sed -i s/\"flickrapi\",// setup.py \
	&& sed -i s/"from eyefi.twisted_flickrapi"/"#from eyefi.twisted_flickrapi"/ eyefi/actions.py \
	&& sed -i s/\"Sphinx\",/\"sphinx==1.8.5\",/ setup.py \
	&& python setup.py install

CMD ["twistd", "-n", "eyefi"]
