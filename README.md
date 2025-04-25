# cs-6210-project-3-solved



**<span style='color:red'>TO GET THIS SOLUTION VISIT:</span>** https://www.ankitcodinghub.com/product/cs-6210-project-3-solved/

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;129503&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS-6210 Project-3 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">
            
<div class="kksr-stars">
    
<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
    
<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">
            

<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>
                

<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
In this project you will implement a simple distributed service using gRPC. This service will simulate an online store which connects customer queries for items with vendors that offer those items.

To get started, review the README located in the attached project3-master.zip. Follow the instructions provided to create a working implementation of the online store. When you’re submitting the project on Gradescope, please make sure you adhere to the directory structure mentioned in the README.&nbsp;Refer to this&nbsp;<a href="https://help.gradescope.com/article/m5qz2xsnjy-student-add-group-members">link</a>&nbsp;on how to create a group submission on Gradescope.

### Big Picture

– In this project, you are going to implement major chunks of a simple distributed service using [grpc](http://www.grpc.io).

– Learnings from this project will also help you in the next project as you will become familiar with grpc and multithreading with threadpool.

### Overview

– You are going to build a store (You can think of Amazon Store!), which receives requests from different users, querying the prices offered by the different registered vendors.

– Your store will be provided with a file of &lt;ip address:port&gt; of vendor servers. On each product query, your store is supposed to request all of these vendor servers for their bid on the queried product.

– Once your store has responses from all the vendors, it is supposed to collate the (bid, vendor_id) from the vendors and send it back to the requesting client.

### Learning outcomes

– Synchronous and Asynchronous RPC packages

– Building a multi-threaded store in a distributed service

## Environment Setup

To set up your environment, you can choose one of the following methods:

– Option 1: Follow this [link](https://grpc.io/docs/languages/cpp/quickstart/) for a cmake based setup on your host machine

– Option 2: Using Docker

### Option 2: Setting Up the Docker Environment (Skip the whole option 2 section if you choose option 1)

If you prefer to use a Docker environment for Project 3, you can either use the pre-build docker image or build and run your own image.

#### Option 2.1: Pre-build Docker image

“`

docker pull dcchico/aos_project3

docker run -it dcchico/aos_project3

“`

#### Option 2.2: Build and Run your own image the following Dockerfile (Skip this step if you use Option 2.1: the pre-build docker image)

Copy the code below into a file and name it “Dockerfile”.

“`dockerfile

FROM ubuntu:22.04

ENV MY_INSTALL_DIR /.local

ENV PATH $MY_INSTALL_DIR/bin:$PATH

RUN apt update &amp;&amp; \

apt install -y cmake build-essential autoconf libtool pkg-config git zip unzip &amp;&amp; \

git clone –recurse-submodules -b v1.58.0 –depth 1 –shallow-submodules https://github.com/grpc/grpc /grpc &amp;&amp; \

mkdir -p $MY_INSTALL_DIR

WORKDIR /grpc/cmake/build

RUN cmake -DgRPC_INSTALL=ON -DgRPC_BUILD_TESTS=OFF -DCMAKE_INSTALL_PREFIX=$MY_INSTALL_DIR ../.. &amp;&amp; \

make -j 4 &amp;&amp; \

make install

WORKDIR /project3

COPY ./project3-template /project3

CMD /bin/bash

“`

Building and Running the Docker Image

Build the Docker image:

“`docker build -t project3-docker .“`

Run the Docker container:

“`docker run -it project3-docker“`

#### Troubleshooting Undefined Reference to grpc::Status::OK

If you see errors like undefined reference to grpc::Status::OK while running make, add gRPC::grpc++_reflection to the linked libraries list for run_tests in /tests/CMakeLists.txt. Lines 10 to 17 should look like this:

“`

add_executable(run_tests client.cc run_tests.cc product_queries_util.h)

target_link_libraries(run_tests

Threads::Threads

gRPC::grpc++

gRPC::grpc++_reflection

p3protolib)

add_dependencies(run_tests p3protolib)

“`

## How You Are Going to Implement It ( Step-by-step )

1. Make sure you understand how GRPC- synchronous and asynchronous calls work. Understand the given helloworld [example](https://github.com/grpc/grpc/tree/master/examples/cpp/helloworld). You will be building your store with asynchronous mechanisms ONLY.

2. Establish asynchronous GRPC communication between –

– Your store and user client.

– Your store and the vendors.

3. Create your thread pool and use it. Where will you use it and for what?

Upon receiving a client request, you store will assign a thread from the thread pool to the incoming request for processing.

– The thread will make async RPC calls to the vendors

– The thread will await for all results to come back

– The thread will collate the results

– The thread will reply to the store client with the results of the call

– Having completed the work, the thread will return to the thread pool

4. Do you have your user client request reaching to the vendors now? And can you see the bids from the different vendors at your user client end? Congratulations you almost got it! Now use the test harness to test if your server can serve multiple clients concurrently and make sure that your thread handling is correct.

## Keep In Mind

1. Your Server has to handle

– Multiple concurrent requests from clients

– Be stateless so far as client requests are concerned (once the client request is serviced it can forget the client)

– Manage the connections to the client requests and the requests it makes to the 3rd party vendors.

2. Server will get the vendor addresses from a file with line separated strings &lt;ip:port&gt;

3. Your server should be able to accept `command line input` of the vendor addresses file, `address` on which it is going to expose its service and `maximum number of threads` its threadpool should have.

4. The format of the invocation is:

./store &lt;filepath for vendor addresses&gt; \

&lt;ip address:port to listen on for clients&gt; \

&lt;maximum number of threads in threadpool&gt;

5. Remember to add references to all the resources you have used while working on the project.

## Given to You

1. run_tests.cc – This will simulate real world users sending concurrent product queries. This will be released soon to you.

2. client.cc – This will be providing ability to connect to the store as a user.

3. vendor.cc – This wil act as the server providing bids for different products. Multiple instances of it will be run listening on different ip address and port.

4. `Two .proto files`

– store.proto – Comm. protocol between user(client) and store(server)

– vendor.proto -Comm. protocol between store(client) and vendor(server)

## How to run the test setup

– Go to project3 directory and build the program.

– Three binaries would be created in the bin folder – `store`,`run_tests` and `run_vendors`. (Note that the location of bin folder depends on how you build the program.)

– First run the command `./run_vendors vendor_addresses.txt &amp;` to start a process which will run multiple servers on different threads listening to (ip_address:ports) from the file given as command line argument.

– Then start up your store which will read the same address file to know vendors’ listening addresses. Also, your store should start listening on a port(for clients to connect to) given as command line argument.

– Then finally run the command `./run_tests $IP_and_port_on_which_store_is_listening $max_num_concurrent_client_requests` to start a process which will simulate real world clients sending requests at the same time.

– This process read the queries from the file `product_query_list.txt`

– It will send some queries and print back the results, which you can use to verify your whole system’s flow.

## Grading

This project is not performance oriented, we will only test the functionality and correctness.

Below is the rubric:

**Total Possible Score:** 12

| Score | Reason |

| —– | —— |

| +2 | Code compiles |

| +4 | Query output is correct |

| +3 | Threadpool management |

| +1 | `store-server` operates in `async` fashion |

| +1 | `store-client` operates in `async` fashion |

| +1 | Readme |

## Deliverables

Please follow the instructions carefully. The folder you hand in must contain the following:

– `Readme.txt` – text file containing a brief description of both your threadpool implementation and the communicaiton pipelines you have built in the store (also include anything about the project that you want to tell the TAs).

– `CMakeLists.txt` – You might need to change it if you add more source files.

– `Store source files` – store.cc(must) containing the source code for store management

– `Threadpool source files` – threadpool.h(must), containing the source code for threadpool management

– You can add supporting files too(in addition to above two), if you need to keep your code more structured, clean etc.

**Submission Directory Structure:**

Readme.txt

src/CMakeLists.txt

src/store.cc

src/threadpool.h

src/any_additional_supporting_files.*

You must use the collect_submission.py to create the submission zip file. Submit the zip file in gradescope. You can verify your submission using the autograder in gradescope.

# FAQ

FAQ can be found [here](faq.md).

&nbsp;
