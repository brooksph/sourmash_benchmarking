#To build this container yourself do the following

#Make directory for dockerfile 

	mkdir "path"/make_sourmash
	cd "path"/make_sourmash
	
#Make docker file 

	cat <<EOF > Dockerfile
	FROM ubuntu:15.10
	RUN apt-get update && apt-get install -y git \
		python2.7-dev \
		python-pip \
		gcc \
   		g++
	RUN cd /home
	RUN git clone https://github.com/dib-lab/khmer.git && \
		cd khmer && \
		python setup.py install 
	EOF
	
#Check it out 

	cat Dockerfile

#Build docker image 

	docker build -t khmer_ctr .

#Test it 

	docker run -it sourmash_ctr sourmash compute 
	
#Move into directory for assembly
	
	cd "path to data"

#Link data to docker image and run 

	docker run -it sourmash_ctr sourmash compute -h