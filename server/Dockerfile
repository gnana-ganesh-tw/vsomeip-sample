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

# Copy the source code
COPY . .

# Build the client
RUN mkdir build && \
    cd build && \
    cmake .. && \
    make


RUN yum install -y net-tools iputils 
RUN yum install -y net-tools iputils 

# Set the environment variable for configuration file
ENV VSOMEIP_CONFIGURATION /home/workspace/config_file.json
ENV VSOMEIP_APPLICATION_NAME=hello_world_service

# Set the entrypoint
ENTRYPOINT ["build/hello_world_service"]

# // "enable" : "true",
#         // "multicast" : "224.224.224.245",
#         // "port" : "30490",
#         // "protocol" : "udp",
#         // "initial_delay_min" : "10",
#         // "initial_delay_max" : "100",
#         // "repetitions_base_delay" : "200",
#         // "repetitions_max" : "3",
#         // "ttl" : "3",
#         // "cyclic_offer_delay" : "2000",
#         // "request_response_delay" : "1500"