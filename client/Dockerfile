FROM amazonlinux

# Workspace directory
WORKDIR /home/workspace

# Install some dependencies
RUN yum install -y gcc-c++ cmake git gcc

# Clone the vsomeip repository
RUN git clone https://github.com/COVESA/vsomeip.git

# Install Boost libraries
RUN yum install -y boost-devel

# Build the vsomeip library
RUN cd vsomeip && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    make install

# Set the environment variable
ENV LD_LIBRARY_PATH /usr/local/lib

RUN rm -rf vsomeip

RUN yum install -y net-tools iputils

# Copy the source code
COPY . .

# Build the client
RUN mkdir build && \
    cd build && \
    cmake .. && \
    make 

# Set the environment variable for configuration file
ENV VSOMEIP_CONFIGURATION /home/workspace/config_file.json
ENV VSOMEIP_APPLICATION_NAME=hello_world_client 

# Set the entrypoint
CMD ["build/hello_world_client"]

