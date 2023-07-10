# Docker inheritance 
# this is a ubuntu image with R, Rstudio and bioC
FROM bioconductor/bioconductor_docker:RELEASE_3_17

# Update apt-get
RUN apt-get update \
	&& apt-get install -y nano git \
 	## Install the python package magic wormhole to send files
	&& pip install magic-wormhole \
 	## Remove packages in '/var/cache/' and 'var/lib' 
        ## to remove side-effects of apt-get update
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# Install required CRAN packages
RUN R -e 'install.packages(c("kableExtra","gplots","eulerr"))'  

# Install required Bioconductor package
RUN R -e 'BiocManager::install(c("DESeq2","fgsea","clusterProfiler"))'

# Clone the repository that contains the research code and execute it
RUN git clone https://github.com/markziemann/set7kd.git

# Copy in the reactome gene set file
COPY ReactomePathways_2023-06-30.gmt  /set7kd

# Set the container working directory
ENV DIRPATH set7kd
WORKDIR $DIRPATH
