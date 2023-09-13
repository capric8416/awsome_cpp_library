# awsome c/c++ package manager
C++ Library Manager for Windows, Linux, and MacOS

[GitHub Repo](https://github.com/microsoft/vcpkg)


# awsome_cpp_library

Sure, I can help you add examples for each of the libraries you've listed. Here are the libraries along with some example code or usage instructions where applicable:

### 01. argparse
Argument Parser for Modern C++
```cpp
#include "argparse/argparse.hpp"

int main(int argc, const char** argv) {
    argparse::ArgumentParser parser;
    parser.add_argument("input_file").help("Input file path");
    parser.add_argument("-o", "--output").default_value("output.txt").help("Output file path");
    
    auto args = parser.parse_args(argc, argv);
    
    std::string input_file = args.get<std::string>("input_file");
    std::string output_file = args.get<std::string>("output");
    
    // Your code to process input and output files
    // ...
    
    return 0;
}
```
[GitHub Repo](https://github.com/p-ranav/argparse)

### 02. fmt
A modern formatting library
```cpp
#include <fmt/format.h>

int main() {
    std::string name = "John";
    int age = 30;
    
    std::string formatted = fmt::format("Name: {}, Age: {}", name, age);
    fmt::print("{}\n", formatted);
    
    return 0;
}
```
[GitHub Repo](https://github.com/fmtlib/fmt)

### 03. spdlog
Fast C++ logging library
```cpp
#include <spdlog/spdlog.h>

int main() {
    // Create a logger
    auto logger = spdlog::stdout_logger_mt("console");

    // Log messages
    logger->info("This is an info message.");
    logger->error("This is an error message.");

    return 0;
}
```
[GitHub Repo](https://github.com/gabime/spdlog)

### 04. cpr
C++ Requests: Curl for People, a spiritual port of Python Requests
```cpp
#include <cpr/cpr.h>

int main() {
    cpr::Response response = cpr::Get(cpr::Url{"https://example.com"});
    
    if (response.status_code == 200) {
        std::cout << response.text << std::endl;
    } else {
        std::cerr << "Request failed with status code: " << response.status_code << std::endl;
    }
    
    return 0;
}
```
[GitHub Repo](https://github.com/libcpr/cpr)

### 05. nlohmann-json
JSON for Modern C++
```cpp
#include <nlohmann/json.hpp>

int main() {
    nlohmann::json data = {
        {"name", "John"},
        {"age", 30}
    };
    
    std::string json_str = data.dump();
    
    // Parse JSON
    auto parsed_data = nlohmann::json::parse(json_str);
    
    std::cout << "Name: " << parsed_data["name"] << ", Age: " << parsed_data["age"] << std::endl;
    
    return 0;
}
```
[GitHub Repo](https://github.com/nlohmann/json)

### 06. uWebSockets
Simple, secure & standards-compliant web server for demanding applications
```cpp
#include <uWS/uWS.h>

int main() {
    uWS::Hub hub;

    hub.onMessage([](uWS::WebSocket<uWS::SERVER> *ws, char *message, size_t length, uWS::OpCode opCode) {
        std::string msg(message, length);
        ws->send(msg, opCode);
    });

    if (hub.listen(3000)) {
        std::cout << "Server listening on port 3000" << std::endl;
        hub.run();
    }

    return 0;
}
```
[GitHub Repo](https://github.com/FFmpeg/FFmpeg)

### 08. protobuf
Protocol Buffers - Google's data interchange format
Example code for Protocol Buffers can be found in the official documentation: [Protocol Buffers - C++ Tutorial](https://developers.google.com/protocol-buffers/docs/cpptutorial)

[GitHub Repo](https://github.com/protocolbuffers/protobuf)

Certainly! Protocol Buffers (protobuf) is a popular serialization format developed by Google. Below are examples of how to serialize and deserialize data using protobuf in C++.

##### Step 1: Define a Protocol Buffer Message
First, you need to define your data structure in a `.proto` file. For example, let's create a simple message for a person's information:

```protobuf
// person.proto
syntax = "proto3";

message Person {
  string name = 1;
  int32 age = 2;
}
```

##### Step 2: Compile the `.proto` File
You'll need to use the Protocol Buffers compiler (`protoc`) to compile your `.proto` file into C++ code. Run the following command to generate the C++ files:

```bash
protoc --cpp_out=. person.proto
```

This command will generate `person.pb.h` and `person.pb.cc`.

##### Step 3: Serialize Data
Now, you can use the generated C++ classes to create and serialize a `Person` message:

```cpp
#include "person.pb.h"
#include <iostream>
#include <fstream>

int main() {
    // Create a Person message
    Person person;
    person.set_name("John");
    person.set_age(30);

    // Serialize the Person message to a binary format
    std::string serializedData;
    person.SerializeToString(&serializedData);

    // Save the serialized data to a file
    std::ofstream output("person.dat", std::ios::binary);
    output.write(serializedData.c_str(), serializedData.size());
    output.close();

    std::cout << "Serialized data saved to 'person.dat'" << std::endl;

    return 0;
}
```

##### Step 4: Deserialize Data
To deserialize the data, you can read the binary data from the file and parse it:

```cpp
#include "person.pb.h"
#include <iostream>
#include <fstream>

int main() {
    // Read the serialized data from a file
    std::ifstream input("person.dat", std::ios::binary);
    std::string serializedData((std::istreambuf_iterator<char>(input)), (std::istreambuf_iterator<char>()));
    input.close();

    // Parse the serialized data into a Person message
    Person person;
    if (!person.ParseFromString(serializedData)) {
        std::cerr << "Failed to parse serialized data." << std::endl;
        return 1;
    }

    // Access the deserialized data
    std::cout << "Name: " << person.name() << ", Age: " << person.age() << std::endl;

    return 0;
}
```

Compile and run the serialization and deserialization code. Make sure you have the `person.dat` file in the same directory, which was created in the serialization step. This code will read the serialized data, parse it back into a `Person` message, and print the person's name and age.

Remember to include error handling in your code to handle cases where deserialization may fail due to data corruption or other issues.

### 09. grpc
The C-based gRPC (C++, Python, Ruby, Objective-C, PHP, C#)
Example code for gRPC can be found in the official documentation: [gRPC C++ Quick Start](https://grpc.io/docs/languages/cpp/quickstart/)

[GitHub Repo](https://github.com/grpc/grpc)

###### gRPC一元请求示例

以下是一个使用 gRPC C++ 的一元请求示例，其中客户端调用一个名为 "Hello" 的服务，服务器返回 "World"。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `HelloService` 的服务，其中包含一个名为 `SayHello` 的方法：
```proto
    syntax = "proto3";
    
    service HelloService {
      rpc SayHello(HelloRequest) returns (HelloResponse);
    }
    
    message HelloRequest {
      string name = 1;
    }
    
    message HelloResponse {
      string message = 1;
    }
```
接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

###### gRPC 服务器示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include "your_proto_file.grpc.pb.h"
    
    class HelloServiceImpl final : public HelloService::Service {
    public:
        grpc::Status SayHello(grpc::ServerContext* context, const HelloRequest* request, HelloResponse* response) override {
            std::string name = request->name();
            response->set_message("Hello, " + name + "!");
            return grpc::Status::OK;
        }
    };
    
    int main() {
        std::string server_address("0.0.0.0:50051");
        HelloServiceImpl service;
    
        grpc::ServerBuilder builder;
        builder.AddListeningPort(server_address, grpc::InsecureServerCredentials());
        builder.RegisterService(&service);
    
        std::unique_ptr<grpc::Server> server(builder.BuildAndStart());
        std::cout << "Server listening on " << server_address << std::endl;
        server->Wait();
    
        return 0;
    }
```
###### gRPC 客户端示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include "your_proto_file.grpc.pb.h"
    
    int main() {
        std::string server_address("localhost:50051");
        grpc::ChannelArguments channel_args;
        channel_args.SetMaxReceiveMessageSize(INT_MAX);
        channel_args.SetMaxSendMessageSize(INT_MAX);
        grpc::Channel channel = grpc::CreateCustomChannel(server_address, grpc::InsecureChannelCredentials(), channel_args);
        std::unique_ptr<HelloService::Stub> stub = HelloService::NewStub(channel);
    
        HelloRequest request;
        request.set_name("World");
        HelloResponse response;
    
        grpc::ClientContext context;
        grpc::Status status = stub->SayHello(&context, request, &response);
    
        if (status.ok()) {
            std::cout << "Server says: " << response.message() << std::endl;
        } else {
            std::cerr << "RPC failed: " << status.error_message() << std::endl;
        }
    
        return 0;
    }
```
请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。这个示例中的服务器接收客户端的名字，并返回包含 "Hello, " 加上名字的消息。

###### gRPC客户端流示例

以下是一个使用 gRPC C++ 的客户端流示例，客户端不停地发送当前日期时间给服务器。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `DateTimeService` 的服务，其中包含一个名为 `StreamDateTime` 的方法：
```proto
    syntax = "proto3";
    
    service DateTimeService {
      rpc StreamDateTime(stream DateTimeRequest) returns (DateTimeResponse);
    }
    
    message DateTimeRequest {
      // 空消息，用于客户端发送时间请求
    }
    
    message DateTimeResponse {
      string datetime = 1;
    }
```
接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

###### gRPC 服务器示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include <chrono>
    #include <thread>
    #include "your_proto_file.grpc.pb.h"
    
    class DateTimeServiceImpl final : public DateTimeService::Service {
    public:
        grpc::Status StreamDateTime(grpc::ServerContext* context, grpc::ServerReaderWriter<DateTimeResponse, DateTimeRequest>* stream) override {
            while (true) {
                DateTimeResponse response;
                std::time_t now = std::time(nullptr);
                response.set_datetime(std::ctime(&now));
                
                grpc::WriteOptions options;
                if (!stream->Write(response, options)) {
                    break;
                }
    
                // 暂停一秒钟再发送下一个时间
                std::this_thread::sleep_for(std::chrono::seconds(1));
            }
            return grpc::Status::OK;
        }
    };
    
    int main() {
        std::string server_address("0.0.0.0:50051");
        DateTimeServiceImpl service;
    
        grpc::ServerBuilder builder;
        builder.AddListeningPort(server_address, grpc::InsecureServerCredentials());
        builder.RegisterService(&service);
    
        std::unique_ptr<grpc::Server> server(builder.BuildAndStart());
        std::cout << "Server listening on " << server_address << std::endl;
        server->Wait();
    
        return 0;
    }
```
###### gRPC 客户端示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include "your_proto_file.grpc.pb.h"
    
    int main() {
        std::string server_address("localhost:50051");
        grpc::ChannelArguments channel_args;
        channel_args.SetMaxReceiveMessageSize(INT_MAX);
        channel_args.SetMaxSendMessageSize(INT_MAX);
        grpc::Channel channel = grpc::CreateCustomChannel(server_address, grpc::InsecureChannelCredentials(), channel_args);
        std::unique_ptr<DateTimeService::Stub> stub = DateTimeService::NewStub(channel);
    
        grpc::ClientContext context;
        std::shared_ptr<grpc::ClientReader<DateTimeResponse>> reader = stub->StreamDateTime(&context, grpc::ClientContext::CompletionQueue());
    
        DateTimeResponse response;
        while (reader->Read(&response)) {
            std::cout << "Server says: " << response.datetime() << std::endl;
        }
    
        grpc::Status status = reader->Finish();
        if (status.ok()) {
            std::cout << "Server stream finished successfully." << std::endl;
        } else {
            std::cerr << "RPC failed: " << status.error_message() << std::endl;
        }
    
        return 0;
    }
```
请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。在此示例中，服务器会不断地向客户端发送当前日期时间，客户端会接收并打印这些时间信息。客户端和服务器之间使用流来实现数据的持续传输。

###### gRPC服务流示例

以下是一个使用 gRPC C++ 的服务端流示例，服务器不停地向客户端发送当前日期时间。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `DateTimeService` 的服务，其中包含一个名为 `StreamDateTime` 的方法：
```proto
    syntax = "proto3";
    
    service DateTimeService {
      rpc StreamDateTime(DateTimeRequest) returns (stream DateTimeResponse);
    }
    
    message DateTimeRequest {
      // 空消息，用于客户端发送请求
    }
    
    message DateTimeResponse {
      string datetime = 1;
    }
```
接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

###### gRPC 服务器示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include <chrono>
    #include <thread>
    #include "your_proto_file.grpc.pb.h"
    
    class DateTimeServiceImpl final : public DateTimeService::Service {
    public:
        grpc::Status StreamDateTime(grpc::ServerContext* context, const DateTimeRequest* request, grpc::ServerWriter<DateTimeResponse>* writer) override {
            while (true) {
                DateTimeResponse response;
                std::time_t now = std::time(nullptr);
                response.set_datetime(std::ctime(&now));
    
                grpc::WriteOptions options;
                if (!writer->Write(response, options)) {
                    break;
                }
    
                // 暂停一秒钟再发送下一个时间
                std::this_thread::sleep_for(std::chrono::seconds(1));
            }
            return grpc::Status::OK;
        }
    };
    
    int main() {
        std::string server_address("0.0.0.0:50051");
        DateTimeServiceImpl service;
    
        grpc::ServerBuilder builder;
        builder.AddListeningPort(server_address, grpc::InsecureServerCredentials());
        builder.RegisterService(&service);
    
        std::unique_ptr<grpc::Server> server(builder.BuildAndStart());
        std::cout << "Server listening on " << server_address << std::endl;
        server->Wait();
    
        return 0;
    }
```
###### gRPC 客户端示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include "your_proto_file.grpc.pb.h"
    
    int main() {
        std::string server_address("localhost:50051");
        grpc::ChannelArguments channel_args;
        channel_args.SetMaxReceiveMessageSize(INT_MAX);
        channel_args.SetMaxSendMessageSize(INT_MAX);
        grpc::Channel channel = grpc::CreateCustomChannel(server_address, grpc::InsecureChannelCredentials(), channel_args);
        std::unique_ptr<DateTimeService::Stub> stub = DateTimeService::NewStub(channel);
    
        DateTimeRequest request;
        std::shared_ptr<grpc::ClientReader<DateTimeResponse>> reader = stub->StreamDateTime(&request, grpc::ClientContext::CompletionQueue());
    
        DateTimeResponse response;
        while (reader->Read(&response)) {
            std::cout << "Server says: " << response.datetime() << std::endl;
        }
    
        grpc::Status status = reader->Finish();
        if (status.ok()) {
            std::cout << "Server stream finished successfully." << std::endl;
        } else {
            std::cerr << "RPC failed: " << status.error_message() << std::endl;
        }
    
        return 0;
    }
```
请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。在此示例中，服务器会不断地向客户端发送当前日期时间，客户端会接收并打印这些时间信息。服务器和客户端之间使用流来实现数据的持续传输，这是服务端流 gRPC 的工作方式。

###### gRPC双向流示例

以下是一个使用 gRPC C++ 的双向流示例，双方不停地交换自身的计算机名称和当前日期时间。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `ComputerInfoService` 的服务，其中包含一个名为 `ExchangeInfo` 的方法：
```proto
    syntax = "proto3";
    
    service ComputerInfoService {
      rpc ExchangeInfo(stream ComputerInfoRequest) returns (stream ComputerInfoResponse);
    }
    
    message ComputerInfoRequest {
      string computer_name = 1;
    }
    
    message ComputerInfoResponse {
      string computer_name = 1;
      string datetime = 2;
    }
```
接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

###### gRPC 服务器示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include <chrono>
    #include <thread>
    #include <sstream>
    #include "your_proto_file.grpc.pb.h"
    
    class ComputerInfoServiceImpl final : public ComputerInfoService::Service {
    public:
        grpc::Status ExchangeInfo(grpc::ServerContext* context, grpc::ServerReaderWriter<ComputerInfoResponse, ComputerInfoRequest>* stream) override {
            while (true) {
                ComputerInfoRequest request;
                if (!stream->Read(&request)) {
                    break;
                }
    
                std::string computer_name = request.computer_name();
    
                ComputerInfoResponse response;
                response.set_computer_name(computer_name);
    
                std::time_t now = std::time(nullptr);
                response.set_datetime(std::ctime(&now));
    
                grpc::WriteOptions options;
                if (!stream->Write(response, options)) {
                    break;
                }
    
                // 暂停一秒钟再发送下一个信息
                std::this_thread::sleep_for(std::chrono::seconds(1));
            }
            return grpc::Status::OK;
        }
    };
    
    int main() {
        std::string server_address("0.0.0.0:50051");
        ComputerInfoServiceImpl service;
    
        grpc::ServerBuilder builder;
        builder.AddListeningPort(server_address, grpc::InsecureServerCredentials());
        builder.RegisterService(&service);
    
        std::unique_ptr<grpc::Server> server(builder.BuildAndStart());
        std::cout << "Server listening on " << server_address << std::endl;
        server->Wait();
    
        return 0;
    }
```
###### gRPC 客户端示例：
```cpp
    #include <iostream>
    #include <grpcpp/grpcpp.h>
    #include <thread>
    #include "your_proto_file.grpc.pb.h"
    
    class ComputerInfoClient {
    public:
        ComputerInfoClient(std::shared_ptr<grpc::Channel> channel)
            : stub_(ComputerInfoService::NewStub(channel)) {}
    
        void ExchangeInfo() {
            grpc::ClientContext context;
            std::shared_ptr<grpc::ClientReaderWriter<ComputerInfoResponse, ComputerInfoRequest>> stream = stub_->ExchangeInfo(&context);
    
            std::string computer_name = "Client";
            while (true) {
                ComputerInfoRequest request;
                request.set_computer_name(computer_name);
    
                grpc::WriteOptions options;
                if (!stream->Write(request, options)) {
                    break;
                }
    
                ComputerInfoResponse response;
                if (!stream->Read(&response)) {
                    break;
                }
    
                std::cout << "Server says: " << response.computer_name() << " - " << response.datetime() << std::endl;
    
                // 暂停一秒钟再发送下一个信息
                std::this_thread::sleep_for(std::chrono::seconds(1));
            }
    
            stream->WritesDone();
            grpc::Status status = stream->Finish();
            if (status.ok()) {
                std::cout << "Server stream finished successfully." << std::endl;
            } else {
                std::cerr << "RPC failed: " << status.error_message() << std::endl;
            }
        }
    
    private:
        std::unique_ptr<ComputerInfoService::Stub> stub_;
    };
    
    int main() {
        std::string server_address("localhost:50051");
        grpc::ChannelArguments channel_args;
        channel_args.SetMaxReceiveMessageSize(INT_MAX);
        channel_args.SetMaxSendMessageSize(INT_MAX);
        grpc::Channel channel = grpc::CreateCustomChannel(server_address, grpc::InsecureChannelCredentials(), channel_args);
    
        ComputerInfoClient client(channel);
        client.ExchangeInfo();
    
        return 0;
    }
```


### 10. FFmpeg
A complete, cross-platform solution for audio and video
You can find FFmpeg usage examples in its documentation: [FFmpeg Documentation](https://www.ffmpeg.org/documentation.html)

[GitHub Repo](https://github.com/FFmpeg/FFmpeg)
[Build FFmpeg for Windows](https://github.com/ShiftMediaProject/FFmpeg)

编码H.265
```cpp
#include <iostream>
#include <string>
#include <stdexcept>

extern "C" {
#include <libavcodec/avcodec.h>
#include <libavformat/avformat.h>
#include <libavutil/opt.h>
}

int main() {
    // Initialize FFmpeg libraries
    av_register_all();
    avcodec_register_all();

    // Input settings
    std::string inputFileName = "input.mp4";  // Replace with your input video file name
    std::string outputFileName = "output.h265";  // Output file in H.265 format

    // Open the input file
    AVFormatContext* formatContext = nullptr;
    if (avformat_open_input(&formatContext, inputFileName.c_str(), nullptr, nullptr) != 0) {
        std::cerr << "Error opening input file." << std::endl;
        return 1;
    }

    if (avformat_find_stream_info(formatContext, nullptr) < 0) {
        std::cerr << "Error finding stream information." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Find the video stream
    int videoStreamIndex = -1;
    for (unsigned int i = 0; i < formatContext->nb_streams; i++) {
        if (formatContext->streams[i]->codecpar->codec_type == AVMEDIA_TYPE_VIDEO) {
            videoStreamIndex = i;
            break;
        }
    }

    if (videoStreamIndex == -1) {
        std::cerr << "Error: No video stream found." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Find the codec for H.265/HEVC
    AVCodec* codec = avcodec_find_encoder_by_name("libx265");
    if (!codec) {
        std::cerr << "Error: libx265 not found." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Create a codec context and set parameters
    AVCodecContext* codecContext = avcodec_alloc_context3(codec);
    if (!codecContext) {
        std::cerr << "Error allocating codec context." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    codecContext->width = formatContext->streams[videoStreamIndex]->codecpar->width;
    codecContext->height = formatContext->streams[videoStreamIndex]->codecpar->height;
    codecContext->bit_rate = 2000000; // Adjust the bit rate as needed
    codecContext->time_base = {1, 25}; // Adjust the frame rate as needed

    // Set H.265 specific options
    av_opt_set(codecContext->priv_data, "preset", "medium", 0); // Encoding preset (e.g., medium, slow, fast)
    av_opt_set(codecContext->priv_data, "x265-params", "keyint=30:min-keyint=30:scenecut=0", 0); // x265 parameters

    // Open the codec
    if (avcodec_open2(codecContext, codec, nullptr) < 0) {
        std::cerr << "Error opening codec." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Open the output file
    AVFormatContext* outputFormatContext = nullptr;
    if (avformat_alloc_output_context2(&outputFormatContext, nullptr, nullptr, outputFileName.c_str()) < 0) {
        std::cerr << "Error creating output format context." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    if (avio_open(&outputFormatContext->pb, outputFileName.c_str(), AVIO_FLAG_WRITE) < 0) {
        std::cerr << "Error opening output file." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    AVStream* outputVideoStream = avformat_new_stream(outputFormatContext, codec);
    if (!outputVideoStream) {
        std::cerr << "Error creating output video stream." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Copy the codec parameters from the input stream to the output stream
    avcodec_parameters_copy(outputVideoStream->codecpar, formatContext->streams[videoStreamIndex]->codecpar);
    outputVideoStream->codecpar->codec_id = AV_CODEC_ID_HEVC; // Set codec to H.265/HEVC

    // Write the output format header
    if (avformat_write_header(outputFormatContext, nullptr) < 0) {
        std::cerr << "Error writing output format header." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Encode and write frames
    AVPacket pkt;
    av_init_packet(&pkt);
    pkt.data = nullptr;
    pkt.size = 0;

    AVFrame* frame = av_frame_alloc();
    if (!frame) {
        std::cerr << "Error allocating frame." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    int frameNumber = 0;
    int gotOutput = 0;
    while (av_read_frame(formatContext, &pkt) >= 0) {
        if (pkt.stream_index == videoStreamIndex) {
            // Send the frame for encoding
            avcodec_encode_video2(codecContext, &pkt, frame, &gotOutput);

            if (gotOutput) {
                // Write the encoded frame to the output file
                av_packet_rescale_ts(&pkt, codecContext->time_base, outputVideoStream->time_base);
                pkt.stream_index = outputVideoStream->index;

                av_write_frame(outputFormatContext, &pkt);
            }
        }

        av_packet_unref(&pkt);
        frameNumber++;
    }

    // Flush the encoder
    avcodec_encode_video2(codecContext, &pkt, nullptr, &gotOutput);
    if (gotOutput) {
        av_packet_rescale_ts(&pkt, codecContext->time_base, outputVideoStream->time_base);
        pkt.stream_index = outputVideoStream->index;
        av_write_frame(outputFormatContext, &pkt);
    }

    // Write the trailer
    av_write_trailer(outputFormatContext);

    // Clean up
    avcodec_free_context(&codecContext);
    avformat_free_context(outputFormatContext);
    avformat_close_input(&formatContext);
    av_frame_free(&frame);

    return 0;
}
```

解码H.265
```cpp
#include <iostream>
#include <string>
#include <stdexcept>

extern "C" {
#include <libavcodec/avcodec.h>
#include <libavformat/avformat.h>
#include <libswscale/swscale.h>
}

int main() {
    // Initialize FFmpeg libraries
    av_register_all();
    avcodec_register_all();

    // Input settings
    std::string inputFileName = "input.h265";  // Replace with your input H.265 video file name
    std::string outputFileName = "output.mp4";  // Output file in MP4 format

    // Open the input file
    AVFormatContext* formatContext = nullptr;
    if (avformat_open_input(&formatContext, inputFileName.c_str(), nullptr, nullptr) != 0) {
        std::cerr << "Error opening input file." << std::endl;
        return 1;
    }

    if (avformat_find_stream_info(formatContext, nullptr) < 0) {
        std::cerr << "Error finding stream information." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Find the video stream
    int videoStreamIndex = -1;
    for (unsigned int i = 0; i < formatContext->nb_streams; i++) {
        if (formatContext->streams[i]->codecpar->codec_type == AVMEDIA_TYPE_VIDEO) {
            videoStreamIndex = i;
            break;
        }
    }

    if (videoStreamIndex == -1) {
        std::cerr << "Error: No video stream found." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Find the codec for H.265/HEVC
    AVCodec* codec = avcodec_find_decoder(AV_CODEC_ID_HEVC);
    if (!codec) {
        std::cerr << "Error: H.265/HEVC decoder not found." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    // Create a codec context and set parameters
    AVCodecContext* codecContext = avcodec_alloc_context3(codec);
    if (!codecContext) {
        std::cerr << "Error allocating codec context." << std::endl;
        avformat_close_input(&formatContext);
        return 1;
    }

    if (avcodec_parameters_to_context(codecContext, formatContext->streams[videoStreamIndex]->codecpar) < 0) {
        std::cerr << "Error setting codec parameters." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Open the codec
    if (avcodec_open2(codecContext, codec, nullptr) < 0) {
        std::cerr << "Error opening codec." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Open the output file
    AVFormatContext* outputFormatContext = nullptr;
    if (avformat_alloc_output_context2(&outputFormatContext, nullptr, nullptr, outputFileName.c_str()) < 0) {
        std::cerr << "Error creating output format context." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    if (avio_open(&outputFormatContext->pb, outputFileName.c_str(), AVIO_FLAG_WRITE) < 0) {
        std::cerr << "Error opening output file." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    AVStream* outputVideoStream = avformat_new_stream(outputFormatContext, codec);
    if (!outputVideoStream) {
        std::cerr << "Error creating output video stream." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Copy the codec parameters from the input stream to the output stream
    avcodec_parameters_copy(outputVideoStream->codecpar, formatContext->streams[videoStreamIndex]->codecpar);

    // Write the output format header
    if (avformat_write_header(outputFormatContext, nullptr) < 0) {
        std::cerr << "Error writing output format header." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Initialize the packet and frame
    AVPacket pkt;
    av_init_packet(&pkt);
    pkt.data = nullptr;
    pkt.size = 0;

    AVFrame* frame = av_frame_alloc();
    if (!frame) {
        std::cerr << "Error allocating frame." << std::endl;
        avcodec_free_context(&codecContext);
        avformat_free_context(outputFormatContext);
        avformat_close_input(&formatContext);
        return 1;
    }

    // Initialize the SwsContext for frame conversion if needed
    SwsContext* swsContext = nullptr;

    // Decode and write frames
    while (av_read_frame(formatContext, &pkt) >= 0) {
        if (pkt.stream_index == videoStreamIndex) {
            // Decode the frame
            int ret = avcodec_receive_frame(codecContext, frame);
            if (ret == 0) {
                // Convert the frame if needed
                if (!swsContext) {
                    swsContext = sws_getContext(
                        frame->width, frame->height, (AVPixelFormat)frame->format,
                        frame->width, frame->height, AV_PIX_FMT_YUV420P,
                        SWS_BILINEAR, nullptr, nullptr, nullptr
                    );
                }

                if (swsContext) {
                    AVFrame* convertedFrame = av_frame_alloc();
                    av_image_fill_arrays(
                        convertedFrame->data, convertedFrame->linesize,
                        av_malloc(av_image_get_buffer_size(AV_PIX_FMT_YUV420P, frame->width, frame->height, 1)),
                        AV_PIX_FMT_YUV420P, frame->width, frame->height, 1
                    );
                    sws_scale(swsContext, frame->data, frame->linesize, 0, frame->height, convertedFrame->data, convertedFrame->linesize);
                    av_frame_unref(frame);
                    av_frame_free(&frame);
                    frame = convertedFrame;
                }

                // Encode the frame
                AVPacket encodedPkt;
                av_init_packet(&encodedPkt);
                encodedPkt.data = nullptr;
                encodedPkt.size = 0;
                frame->pts = av_frame_get_best_effort_timestamp(frame);
                avcodec_send_frame(codecContext, frame);
                ret = avcodec_receive_packet(codecContext, &encodedPkt);
                if (ret == 0) {
                    // Write the encoded packet to the output file
                    av_write_frame(outputFormat
```



### 11. gstreamer
Open-source multimedia framework
You can find tutorials and documentation on the official GStreamer website: [GStreamer Documentation](https://gstreamer.freedesktop.org/documentation/)

[GitHub Repo](https://github.com/GStreamer/gstreamer)

H.265基本码流转换成传输流
```cpp
#include <gst/gst.h>

int main(int argc, char *argv[]) {
    // Initialize GStreamer
    gst_init(&argc, &argv);

    // Input H.265 encoded file
    const gchar* input_file = "input.h265";

    // Output H.265 transport stream file
    const gchar* output_file = "output.ts";

    // Create a GStreamer pipeline
    GstElement *pipeline, *filesrc, *h265parse, *mux, *filesink;
    GstBus *bus;
    GstMessage *msg;
    GstStateChangeReturn ret;

    pipeline = gst_pipeline_new("h265-to-ts");
    filesrc = gst_element_factory_make("filesrc", "file-source");
    h265parse = gst_element_factory_make("h265parse", "h265-parser");
    mux = gst_element_factory_make("mpegtsmux", "mpegts-mux");
    filesink = gst_element_factory_make("filesink", "file-sink");

    if (!pipeline || !filesrc || !h265parse || !mux || !filesink) {
        g_printerr("Not all elements could be created.\n");
        return -1;
    }

    // Set input and output file locations
    g_object_set(G_OBJECT(filesrc), "location", input_file, NULL);
    g_object_set(G_OBJECT(filesink), "location", output_file, NULL);

    // Add elements to the pipeline
    gst_bin_add_many(GST_BIN(pipeline), filesrc, h265parse, mux, filesink, NULL);

    // Link elements together
    if (!gst_element_link(filesrc, h265parse) ||
        !gst_element_link(h265parse, mux) ||
        !gst_element_link(mux, filesink)) {
        g_printerr("Elements could not be linked.\n");
        gst_object_unref(pipeline);
        return -1;
    }

    // Set the pipeline to the playing state
    ret = gst_element_set_state(pipeline, GST_STATE_PLAYING);
    if (ret == GST_STATE_CHANGE_FAILURE) {
        g_printerr("Unable to set the pipeline to the playing state.\n");
        gst_object_unref(pipeline);
        return -1;
    }

    // Wait until the conversion is complete
    bus = gst_element_get_bus(pipeline);
    msg = gst_bus_timed_pop_filtered(bus, GST_CLOCK_TIME_NONE,
                                     GST_MESSAGE_ERROR | GST_MESSAGE_EOS);

    // Stop and cleanup
    gst_message_unref(msg);
    gst_object_unref(bus);
    gst_element_set_state(pipeline, GST_STATE_NULL);
    gst_object_unref(pipeline);

    g_print("File %s converted to %s\n", input_file, output_file);

    return 0;
}
```


### 12. mpv
Command-line video player (library)
Usage examples and documentation can be found on the mpv website: [mpv Documentation](https://mpv.io/manual/stable/)

[GitHub Repo](https://github.com/mpv-player/mpv)
[Build mpv for Windows](https://github.com/shinchiro/mpv-winbuild-cmake)

播放自定义流
```cpp
#include <iostream>
#include <mpv/client.h>
#include <mpv/stream_cb.h>

// 自定义数据读取回调函数
ssize_t custom_read_fn(void *user_data, void *buffer, size_t size) {
    // 在这里实现您的自定义数据读取逻辑
    // 将数据写入buffer，并返回实际读取的字节数
    // 如果没有更多数据可用，可以返回0表示结束
    // 如果发生错误，返回-1

    // 示例：假设您有一个自定义数据源，每次读取100字节
    static const char custom_data[] = "Your custom data source content";
    static size_t offset = 0;

    if (offset >= sizeof(custom_data))
        return 0;

    size_t bytes_to_copy = std::min(size, sizeof(custom_data) - offset);
    memcpy(buffer, custom_data + offset, bytes_to_copy);
    offset += bytes_to_copy;

    return bytes_to_copy;
}

int main() {
    mpv_handle *mpv;

    // 初始化mpv实例
    mpv = mpv_create();
    if (!mpv) {
        std::cerr << "Failed to create mpv instance." << std::endl;
        return 1;
    }

    // 设置mpv选项，可以根据需要进行调整
    mpv_set_option_string(mpv, "input-default-bindings", "yes");
    mpv_set_option_string(mpv, "input-vo-keyboard", "yes");
    mpv_set_option_string(mpv, "input-ipc-server", "/tmp/mpvsocket");

    // 打开一个X11窗口，如果需要的话
    mpv_set_option_string(mpv, "wid", "X11 Window ID");

    // 设置自定义数据读取回调函数
    mpv_stream_cb_info stream_cb_info;
    memset(&stream_cb_info, 0, sizeof(stream_cb_info));
    stream_cb_info.read_cb = custom_read_fn;
    
    // 关联自定义数据读取回调函数与mpv实例
    if (mpv_stream_cb_create(mpv, &stream_cb_info) < 0) {
        std::cerr << "Failed to create stream callback." << std::endl;
        mpv_terminate_destroy(mpv);
        return 1;
    }

    // 使用mpv命令播放流
    const char *cmd[] = {
        "loadfile", "stream://", NULL
    };
    if (mpv_command(mpv, cmd) < 0) {
        std::cerr << "Failed to load stream." << std::endl;
        mpv_terminate_destroy(mpv);
        return 1;
    }

    // 等待播放结束
    mpv_event *event;
    while (1) {
        event = mpv_wait_event(mpv, -1);
        if (event->event_id == MPV_EVENT_END_FILE)
            break;
    }

    // 清理和销毁mpv实例
    mpv_terminate_destroy(mpv);

    return 0;
}
```

### 13. bshoshany-thread-pool
BS::thread_pool: a fast, lightweight C++17 thread pool library
```cpp
#include <bshoshany/thread_pool.h>

int main() {
    bshoshany::thread_pool pool(4); // Create a thread pool with 4 worker threads
    
    // Submit tasks to the thread pool
    for (int i = 0; i < 10; ++i) {
        pool.submit([i] {
            std::cout << "Task " << i << " executed by thread " << std::this_thread::get_id() << std::endl;
        });
    }
    
    // Shutdown the thread pool when done
    pool.shutdown();
    
    return 0;
}
```
[GitHub Repo](https://github.com/bshoshany/thread-pool)

### 14. libnpp
NVIDIA 2D Image and Signal Processing Performance Primitives (NPP)
Documentation for NVIDIA NPP can be found on the NVIDIA website: [NVIDIA NPP Documentation](https://docs.nvidia.com/cuda/npp/index.html)

[Library Documentation](https://docs.nvidia.com/cuda/npp/index.html)

pixel_fmt_cuda转换成rgb24
```cpp
#include <iostream>
#include <npp.h>

int main() {
    // 初始化NPP库
    NppStatus nppStatus = nppiInit();
    if (nppStatus != NPP_SUCCESS) {
        std::cerr << "NPP initialization failed: " << nppGetErrorString(nppStatus) << std::endl;
        return 1;
    }

    // 定义输入NV12图像和输出RGB24图像的尺寸
    int width = 1920;  // 替换为您的图像宽度
    int height = 1080; // 替换为您的图像高度

    // 分配和初始化NV12和RGB24图像缓冲区
    Npp8u* pSrcNV12 = static_cast<Npp8u*>(malloc(width * height * 3 / 2)); // NV12格式
    Npp8u* pDstRGB24 = static_cast<Npp8u*>(malloc(width * height * 3));    // RGB24格式

    // 在这里填充pSrcNV12缓冲区，将NV12图像数据加载到内存中

    // 创建NPP图像描述符
    NppiSize oSize = { width, height };
    NppiRect oROI = { 0, 0, width, height };
    NppiSize oSrcStep = { width, width / 2 }; // NV12格式的步长
    NppiSize oDstStep = { width * 3, width * 3 }; // RGB24格式的步长

    // 使用NPP库函数执行NV12到RGB24的转换
    nppStatus = nppiYCbCr420ToBGR_8u_P2C3R(pSrcNV12, oSrcStep, pDstRGB24, oDstStep, oSize, oROI);
    if (nppStatus != NPP_SUCCESS) {
        std::cerr << "NPP conversion failed: " << nppGetErrorString(nppStatus) << std::endl;
        free(pSrcNV12);
        free(pDstRGB24);
        return 1;
    }

    // 现在pDstRGB24缓冲区包含RGB24格式的图像数据，可以进行后续处理或显示

    // 释放内存
    free(pSrcNV12);
    free(pDstRGB24);

    // 关闭NPP库
    nppStatus = nppiFree();
    if (nppStatus != NPP_SUCCESS) {
        std::cerr << "NPP cleanup failed: " << nppGetErrorString(nppStatus) << std::endl;
        return 1;
    }

    return 0;
}
```

### 15. nvJPEG
GPU-accelerated JPEG decoder, encoder, and transcoder
Documentation for NVIDIA nvJPEG can be found on the NVIDIA website: [NVIDIA nvJPEG Documentation](https://developer.nvidia.com/nvjpeg)

[Library Documentation](https://developer.nvidia.com/nvjpeg)

jpeg编码
```cpp
#include <iostream>
#include <npp.h>
#include <nvjpeg.h>

int main() {
    // 1. 使用NPP将图像转换为YUV 420P

    // 假设输入数据为RGB24
    int width = 1920;
    int height = 1080;
    Npp8u *pSrcRGB = nullptr;  // 这是您的原始数据
    Npp8u *pDstYUV = nullptr;  // 这是转换后的YUV数据

    // 分配内存和其他初始化...

    // 使用NPP将RGB转换为YUV420
    // 对于这一部分，您可能需要使用一系列的npp函数调用
    // 注意：以下是一个伪代码调用，并不是一个真实的函数
    // nppConvertRGBToYUV420(pSrcRGB, pDstYUV, width, height);

    // 2. 使用nvJPEG编码YUV 420P为JPEG

    nvjpegHandle_t nvjpegHandle;
    nvjpegEncoderState_t encoderState;
    nvjpegEncoderParams_t encoderParams;
    nvjpegStatus_t nvjpegStatus = nvjpegCreateSimple(&nvjpegHandle);

    // 初始化 nvJPEG 结构和分配内存...

    nvjpegJpegState_t jpegState;
    nvjpegCreateJpegState(nvjpegHandle, &jpegState);
    nvjpegEncoderParamsCreate(nvjpegHandle, &encoderParams, NVJPEG_BACKEND_DEFAULT);

    // 使用默认参数编码
    nvjpegEncoderParamsSetDefaults(nvjpegHandle, encoderParams);

    // 设置图像格式
    nvjpegInputFormat_t inputFormat = NVJPEG_INPUT_YUV420;
    nvjpegEncodeSetInputFormat(encoderParams, inputFormat);

    // 执行编码
    size_t jpegSize;
    nvjpegEncodeImage(nvjpegHandle, encoderState, encoderParams, &jpegState, pDstYUV, &jpegSize);

    // pDstYUV 现在应该包含编码的 JPEG 数据

    // 清理工作：释放内存、销毁NPP和nvJPEG资源...

    return 0;
}
```


### 16. absl
Abseil Common Libraries (C++)
Documentation for Abseil can be found on the Abseil website: [Abseil Documentation](https://abseil.io/docs/cpp/)

[GitHub Repo](https://github.com/abseil/abseil-cpp)

计算文件sha1摘要
```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <absl/strings/string_view.h>
#include <absl/crypto/sha.h>

int main() {
    // 打开文件
    std::ifstream file("your_file.txt", std::ios::binary);
    if (!file.is_open()) {
        std::cerr << "Failed to open file." << std::endl;
        return 1;
    }

    // 创建SHA-1计算器
    absl::crypto::Sha1 sha1;

    // 缓冲区大小（根据需要进行调整）
    constexpr size_t buffer_size = 4096;
    char buffer[buffer_size];

    // 读取文件并更新SHA-1计算
    while (file) {
        file.read(buffer, buffer_size);
        absl::string_view data(buffer, static_cast<size_t>(file.gcount()));
        sha1.Update(data);
    }

    // 获取SHA-1摘要
    std::string sha1_digest = sha1.Hash();

    // 输出SHA-1摘要
    std::cout << "SHA-1 Digest: " << sha1_digest << std::endl;

    // 关闭文件
    file.close();

    return 0;
}
```


### 17. modp-base64
SIMD base64 encoder and decoder
Example code and usage instructions can be found in the GitHub repository's README: [modp_b64 GitHub Repository](https://github.com/Piasy/modp_b64)

[GitHub Repo](https://github.com/Piasy/modp_b64)

base64编码
```cpp
#include <stdio.h>
#include <modp_b64.h>

int main() {
    const char* input_data = "Hello, World!"; // 要编码的数据
    char output_data[128]; // 用于存储编码后的数据

    // 进行Base64编码
    size_t input_len = strlen(input_data);
    size_t output_len = modp_b64_encode(output_data, input_data, input_len);

    // 打印编码后的数据
    printf("Base64 Encoded Data: %s\n", output_data);
    printf("Encoded Data Length: %zu\n", output_len);

    return 0;
}
```

### 18. folly
An open-source C++ library developed and used at Facebook
Example code and documentation can be found on the folly GitHub repository: [folly GitHub Repository](https://github.com/facebook/folly)

[GitHub Repo](https://github.com/facebook/folly)

异步示例
```cpp
#include <iostream>
#include <folly/futures/Future.h>

int main() {
    // 创建一个Promise对象，用于产生Future
    folly::Promise<int> promise;
    folly::Future<int> future = promise.getFuture();

    // 启动一个异步任务
    std::thread asyncTask([&promise]() {
        // 模拟异步操作
        std::this_thread::sleep_for(std::chrono::seconds(2));

        // 异步操作完成后，使用Promise设置Future的值
        promise.setValue(42);
    });

    // 在主线程中等待Future完成
    std::cout << "Waiting for the async task to complete..." << std::endl;
    future.wait();

    // 从Future中获取结果
    int result = future.value();

    // 打印结果
    std::cout << "Async task result: " << result << std::endl;

    // 等待异步任务完成
    asyncTask.join();

    return 0;
}
```

### 19. boost
Free peer-reviewed portable C++ source libraries
Example code and extensive documentation can be found on the Boost website: [Boost Documentation](https://www.boost.org/doc/libs/)

[Library Documentation](https://www.boost.org/doc/libs/)

进程间共享内存通信
```cpp
#include <iostream>
#include <string>
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/allocators/allocator.hpp>
#include <boost/interprocess/containers/vector.hpp>

using namespace boost::interprocess;

int main() {
    // 创建或打开共享内存
    managed_shared_memory segment(open_or_create, "MySharedMemory", 65536);

    // 创建一个可在共享内存中存储std::string的容器
    typedef allocator<char, managed_shared_memory::segment_manager> CharAllocator;
    typedef vector<std::string, CharAllocator> MyVector;

    // 获取或创建vector对象
    MyVector* myvector = segment.find_or_construct<MyVector>("MyVector")(segment.get_segment_manager());

    // 向共享内存中的vector写入数据
    myvector->push_back("Hello, shared memory!");
    myvector->push_back("This is a message from the first process.");

    // 等待一段时间，以便第二个进程有足够的时间来读取数据
    std::this_thread::sleep_for(std::chrono::seconds(3));

    return 0;
}
```

```cpp
#include <iostream>
#include <string>
#include <boost/interprocess/managed_shared_memory.hpp>
#include <boost/interprocess/allocators/allocator.hpp>
#include <boost/interprocess/containers/vector.hpp>

using namespace boost::interprocess;

int main() {
    // 打开共享内存
    managed_shared_memory segment(open_only, "MySharedMemory");

    // 获取共享内存中的vector对象
    typedef allocator<char, managed_shared_memory::segment_manager> CharAllocator;
    typedef vector<std::string, CharAllocator> MyVector;

    MyVector* myvector = segment.find<MyVector>("MyVector").first;

    // 从共享内存中的vector读取数据并打印
    for (const auto& str : *myvector) {
        std::cout << str << std::endl;
    }

    return 0;
}
```

### 20. libuv
Cross-platform asynchronous I/O
Example code and documentation can be found on the libuv GitHub repository: [libuv GitHub Repository](https://github.com/libuv/libuv)

[GitHub Repo](https://github.com/libuv/libuv)

http client server通信
```cpp
#include <uv.h>
#include <stdio.h>

void on_new_connection(uv_stream_t* server, int status) {
    if (status < 0) {
        fprintf(stderr, "New connection error: %s\n", uv_strerror(status));
        return;
    }

    uv_tcp_t* client = (uv_tcp_t*)malloc(sizeof(uv_tcp_t));
    uv_tcp_init(uv_default_loop(), client);

    if (uv_accept(server, (uv_stream_t*)client) == 0) {
        uv_read_start((uv_stream_t*)client,
            [](uv_handle_t* handle, size_t suggested_size, uv_buf_t* buf) {
                buf->base = (char*)malloc(suggested_size);
                buf->len = suggested_size;
            },
            [](uv_stream_t* stream, ssize_t nread, const uv_buf_t* buf) {
                if (nread > 0) {
                    printf("Received data from client: %.*s\n", (int)nread, buf->base);
                }
                else if (nread < 0) {
                    if (nread != UV_EOF) {
                        fprintf(stderr, "Read error: %s\n", uv_strerror(nread));
                    }
                    uv_close((uv_handle_t*)stream, [](uv_handle_t* handle) {
                        free(handle);
                    });
                }
                free(buf->base);
            }
        );
    }
    else {
        uv_close((uv_handle_t*)client, [](uv_handle_t* handle) {
            free(handle);
        });
    }
}

int main() {
    uv_tcp_t server;
    uv_loop_t* loop = uv_default_loop();

    uv_tcp_init(loop, &server);

    struct sockaddr_in bind_addr;
    uv_ip4_addr("0.0.0.0", 8080, &bind_addr);

    uv_tcp_bind(&server, (const struct sockaddr*)&bind_addr, 0);

    int r = uv_listen((uv_stream_t*)&server, 128, on_new_connection);
    if (r) {
        fprintf(stderr, "Listen error: %s\n", uv_strerror(r));
        return 1;
    }

    printf("HTTP server listening on port 8080...\n");

    return uv_run(loop, UV_RUN_DEFAULT);
}

```

```cpp
#include <uv.h>
#include <stdio.h>

void on_connect(uv_connect_t* req, int status) {
    if (status < 0) {
        fprintf(stderr, "Connection error: %s\n", uv_strerror(status));
        return;
    }

    uv_stream_t* stream = req->handle;
    uv_buf_t req_data = uv_buf_init("GET / HTTP/1.1\r\nHost: localhost\r\n\r\n", 29);

    uv_write_t write_req;
    uv_write(&write_req, stream, &req_data, 1, [](uv_write_t* req, int status) {
        if (status < 0) {
            fprintf(stderr, "Write error: %s\n", uv_strerror(status));
            return;
        }

        uv_stream_t* stream = req->handle;

        uv_read_start(stream,
            [](uv_handle_t* handle, size_t suggested_size, uv_buf_t* buf) {
                buf->base = (char*)malloc(suggested_size);
                buf->len = suggested_size;
            },
            [](uv_stream_t* stream, ssize_t nread, const uv_buf_t* buf) {
                if (nread > 0) {
                    printf("Received response: %.*s\n", (int)nread, buf->base);
                }
                else if (nread < 0) {
                    if (nread != UV_EOF) {
                        fprintf(stderr, "Read error: %s\n", uv_strerror(nread));
                    }
                    uv_close((uv_handle_t*)stream, [](uv_handle_t* handle) {
                        free(handle);
                    });
                }
                free(buf->base);
            }
        );
    });
}

int main() {
    uv_loop_t* loop = uv_default_loop();

    uv_tcp_t client;
    uv_tcp_init(loop, &client);

    struct sockaddr_in server_addr;
    uv_ip4_addr("127.0.0.1", 8080, &server_addr);

    uv_connect_t connect_req;
    uv_tcp_connect(&connect_req, &client, (const struct sockaddr*)&server_addr, on_connect);

    printf("HTTP client connecting to localhost:8080...\n");

    return uv_run(loop, UV_RUN_DEFAULT);
}

```

### 21. openssl
TLS/SSL and crypto library
Example code and documentation can be found on the OpenSSL GitHub repository: [OpenSSL GitHub Repository](https://github.com/openssl/openssl)

[GitHub Repo](https://github.com/openssl/openssl)

ecdsa签名和验证
```cpp
#include <stdio.h>
#include <string.h>
#include <openssl/ec.h>
#include <openssl/ecdsa.h>
#include <openssl/obj_mac.h>
#include <openssl/err.h>

int main() {
    // 初始化 OpenSSL 库
    ERR_load_crypto_strings();
    OpenSSL_add_all_algorithms();

    // 创建 EC_KEY 对象
    EC_KEY *ec_key = EC_KEY_new_by_curve_name(NID_secp256k1);
    if (!ec_key) {
        fprintf(stderr, "Error creating EC_KEY\n");
        return 1;
    }

    // 生成 EC_KEY 密钥对
    if (EC_KEY_generate_key(ec_key) != 1) {
        fprintf(stderr, "Error generating EC_KEY key pair\n");
        return 1;
    }

    // 准备要签名的数据
    const char *data_to_sign = "Hello, ECDSA!";
    size_t data_len = strlen(data_to_sign);

    // 计算数据的 SHA-256 哈希值
    unsigned char hash[SHA256_DIGEST_LENGTH];
    SHA256((const unsigned char *)data_to_sign, data_len, hash);

    // 对数据进行签名
    ECDSA_SIG *signature = ECDSA_do_sign(hash, sizeof(hash), ec_key);
    if (!signature) {
        fprintf(stderr, "Error signing data\n");
        return 1;
    }

    // 打印签名结果
    printf("ECDSA Signature:\n");
    printf("R: %s\n", BN_bn2hex(signature->r));
    printf("S: %s\n", BN_bn2hex(signature->s));

    // 验证签名
    int verification_result = ECDSA_do_verify(hash, sizeof(hash), signature, ec_key);
    if (verification_result == 1) {
        printf("Signature verification succeeded!\n");
    } else if (verification_result == 0) {
        printf("Signature verification failed!\n");
    } else {
        fprintf(stderr, "Error verifying signature\n");
    }

    // 释放资源
    EC_KEY_free(ec_key);
    ECDSA_SIG_free(signature);
    ERR_free_strings();

    return 0;
}

```

### 22. imgui
Dear ImGui: Bloat-free Graphical User Interface for C++ with minimal dependencies
Example code and documentation can be found on the Dear ImGui GitHub repository: [Dear ImGui GitHub Repository](https://github.com/ocornut/imgui)

[GitHub Repo](https://github.com/ocornut/imgui)

```cpp
#include "imgui.h"

// 定义一个结构来表示树形节点
struct TreeNode {
    std::string name;
    std::vector<TreeNode> children;
};

// 递归函数来绘制树形节点及其子节点
void DrawTreeNode(const TreeNode& node) {
    bool node_open = ImGui::TreeNode(node.name.c_str());

    // 处理节点的展开/折叠
    if (node_open) {
        for (const TreeNode& child : node.children) {
            DrawTreeNode(child);
        }
        ImGui::TreePop();
    }

    // 处理双击事件
    if (ImGui::IsItemClicked(0) && ImGui::IsMouseDoubleClicked(0)) {
        // 在这里你可以添加双击节点后的操作，比如显示子节点的名称
        // 在这个示例中，我们简单地打印子节点的名称
        for (const TreeNode& child : node.children) {
            ImGui::Text("Double-clicked child node: %s", child.name.c_str());
        }
    }
}

int main() {
    // 初始化 ImGui

    // 创建树形节点数据
    TreeNode root;
    root.name = "Root";

    TreeNode child1;
    child1.name = "Child 1";

    TreeNode child2;
    child2.name = "Child 2";

    TreeNode grandchild1;
    grandchild1.name = "Grandchild 1";

    child1.children.push_back(grandchild1);
    root.children.push_back(child1);
    root.children.push_back(child2);

    // 主循环
    while (!glfwWindowShouldClose(window)) {
        // 开始 ImGui 帧

        // 绘制树形节点
        DrawTreeNode(root);

        // 结束 ImGui 帧

        // 渲染 ImGui 内容
        // ...

        // 处理事件
        // ...
    }

    // 清理 ImGui 资源

    return 0;
}

```

### 23. bgfx
Cross-platform, graphics API-agnostic rendering library
Example code and documentation can be found on the bgfx GitHub repository: [bgfx GitHub Repository](https://github.com/bkaradzic/bgfx)

[GitHub Repo](https://github.com/bkaradzic/bgfx)

绘制旋转立方体
```cpp
#include <bgfx/bgfx.h>
#include <bgfx/platform.h>
#include <bx/timer.h>
#include <bx/math.h>
#include <entry/entry.h>

namespace
{
    const bgfx::VertexLayout PosColorVertex::ms_layout
            = {bgfx::Attrib::Position, 3, bgfx::AttribType::Float, false, bgfx::Attrib::Color0, 4, bgfx::AttribType::Uint8, true};

    bgfx::ProgramHandle loadProgram(const char* _vsName, const char* _fsName)
    {
        bgfx::ShaderHandle vsh = bgfx::createShader(loadShader(_vsName));
        bgfx::ShaderHandle fsh = bgfx::createShader(loadShader(_fsName));

        return bgfx::createProgram(vsh, fsh, true /* destroy shaders when program is destroyed */);
    }

    const bgfx::Memory* loadShader(const char* _name)
    {
        static std::map<std::string, std::unique_ptr<bgfx::Memory>> s_shaders;
        auto it = s_shaders.find(_name);
        if (it != s_shaders.end())
        {
            return it->second.get();
        }

        const std::string filePath = bx::strCat("shaders/", _name);

        void* data = nullptr;
        size_t size = 0;
        bx::CrtFileReader reader;
        bx::CrtFileReaderScope fileScope(&reader);

        if (bx::open(&reader, filePath.c_str()) == 0)
        {
            size = bx::getSize(&reader);
            data = BX_ALLOC(entry::getAllocator(), size);
            bx::read(&reader, data, size);
        }

        bgfx::Memory* mem = bgfx::makeRef(data, (uint32_t)size, nullptr, [](void* _ptr, void* _userData) { BX_FREE(entry::getAllocator(), _ptr); });

        s_shaders[_name] = std::unique_ptr<bgfx::Memory>(mem);

        return mem;
    }

    const bgfx::Memory* s_cubeVertices;
    const bgfx::Memory* s_cubeIndices;

    bgfx::VertexBufferHandle s_vbh;
    bgfx::IndexBufferHandle s_ibh;
    bgfx::ProgramHandle s_program;
    bgfx::UniformHandle s_time;

    const bgfx::Memory* s_embeddedShaders[] = {
        loadShader("vs_cubes.bin"), loadShader("fs_cubes.bin"),
    };
}

int main(int argc, char** argv)
{
    // 初始化 bgfx
    bgfx::Init init;
    init.type = bgfx::RendererType::Count;
    bgfx::init(init);
    bgfx::reset(init.width, init.height, BGFX_RESET_VSYNC);

    bgfx::setDebug(BGFX_DEBUG_TEXT);

    // 创建顶点和索引缓冲区
    s_cubeVertices = bgfx::makeRef(cubeVertices, sizeof(cubeVertices));
    s_cubeIndices = bgfx::makeRef(cubeIndices, sizeof(cubeIndices));

    s_vbh = bgfx::createVertexBuffer(s_cubeVertices, PosColorVertex::ms_layout);
    s_ibh = bgfx::createIndexBuffer(s_cubeIndices);

    // 加载着色器程序
    s_program = loadProgram("vs_cubes", "fs_cubes");

    // 获取时间 uniform 句柄
    s_time = bgfx::createUniform("u_time", bgfx::UniformType::Vec4);

    // 主循环
    while (!entry::processEvents(init.m_width, init.m_height, init.m_debug, init.m_reset, &init.m_exit))
    {
        float time = bx::getHPCounter() / double(bx::getHPFrequency());
        float view[16];
        float proj[16];
        bx::mtxLookAt(view, {0.0f, 0.0f, -35.0f}, {0.0f, 0.0f, 0.0f});
        bx::mtxProj(proj, 60.0f, float(init.m_width) / float(init.m_height), 0.1f, 100.0f, bgfx::getCaps()->homogeneousDepth);

        // 设置渲染状态
        bgfx::setViewRect(0, 0, 0, uint16_t(init.m_width), uint16_t(init.m_height));
        bgfx::setViewTransform(0, view, proj);
        bgfx::setViewClear(0, BGFX_CLEAR_COLOR | BGFX_CLEAR_DEPTH, 0x303030ff, 1.0f, 0);

        // 设置模型矩阵
        float mtx[16];
        bx::mtxRotateXY(mtx, time, time * 0.37f);
        bgfx::setTransform(mtx);

        // 绘制立方体
        bgfx::setVertexBuffer(0, s_vbh);
        bgfx::setIndexBuffer(s_ibh);

        // 传递时间 uniform
        bgfx::setUniform(s_time, &time);

        // 提交绘制命令
        bgfx::submit(0, s_program);

        // 渲染帧
        bgfx::frame();
    }

    // 清理资源
    bgfx::destroy(s_time);
    bgfx::destroy(s_ibh);
    bgfx::destroy(s_vbh);
    bgfx::destroy(s_program);

    // 关闭 bgfx
    bgfx::shutdown();

    return 0;
}
```

### 24. libplacebo
libplacebo is, in a nutshell, the core rendering algorithms and ideas of mpv rewritten as an independent library
Example code and documentation can be found on the libplacebo GitHub repository: [libplacebo GitHub Repository](https://github.com/haasn/libplacebo)

[GitHub Repo](https://github.com/haasn/libplacebo)

颜色空间转换示例
```cpp
#include <libplacebo/colorspace.h>
#include <libplacebo/renderer.h>

int main() {
    // 初始化 libplacebo 上下文
    pl_context *ctx = pl_context_create(NULL);

    // 创建颜色空间转换上下文
    pl_color_space *csp_ctx = pl_color_space_create(ctx, PL_COLOR_SPACE_AUTO);

    // 设置源颜色空间和目标颜色空间
    pl_color_space_params src_params = {PL_COLOR_SPACE_AUTO, PL_TRANSFER_AUTO, PL_PRIMARIES_AUTO};
    pl_color_space_params dst_params = {PL_COLOR_SPACE_RGB, PL_TRANSFER_LINEAR, PL_PRIMARIES_REC709};
    pl_color_space_select(csp_ctx, &src_params, &dst_params);

    // 创建一个示例的 YUV 图像帧
    // 实际情况下，你应该加载或生成你的图像帧数据
    pl_image img = pl_image_create(ctx, PL_FMT_I420, width, height, NULL);

    // 执行颜色空间转换
    pl_color_space_convert(csp_ctx, &img, &img);

    // 在这里你可以使用转换后的图像进行进一步处理或渲染

    // 释放资源
    pl_image_unref(&img);
    pl_color_space_destroy(&csp_ctx);
    pl_context_destroy(&ctx);

    return 0;
}
```


### 25. SPIRV-Cross
SPIRV-Cross is a practical tool and library for performing reflection on SPIR-V and disassembling SPIR-V back to high-level languages
Example code and documentation can be found on the SPIRV-Cross GitHub repository: [SPIRV-Cross GitHub Repository](https://github.com/KhronosGroup/SPIRV-Cross)

[GitHub Repo](https://github.com/KhronosGroup/SPIRV-Cross)

着色器代码转换
```cpp
#include <spirv_cross/spirv_cross.hpp>

int main() {
    // 创建SPIRV-Cross的编译器对象
    spirv_cross::Compiler compiler(spirv_data);

    // 获取meta、D3D11和Vulkan着色器代码
    std::string meta_shader = compiler.compile(spirv_cross::CompilerGLSL::Options());
    std::string d3d11_shader = compiler.compile(spirv_cross::CompilerHLSL::Options());
    std::string vulkan_shader = compiler.compile(spirv_cross::CompilerGLSL::Options());

    // 现在你可以使用生成的着色器代码进行进一步处理或集成到你的应用程序中

    return 0;
}
```

### 26. asl
A compact C++ cross-platform library including JSON, XML, HTTP, Sockets, WebSockets, threads, processes, logs, file system, CSV, INI files, etc
Example code and documentation can be found on the asl GitHub repository: [asl GitHub Repository](https://github.com/aslze/asl)

[GitHub Repo](https://github.com/aslze/asl)


```cpp
CmdArgs args(argc, argv);
int iterations = args["iterations"] | 10;  // default to 10 if no parameter given
```

Read or write a configuration INI file ("config.ini" contains this):

```
[parameters]
threshold=0.25
```

```cpp
IniFile config("config.ini");
float threshold = config["parameters/threshold"] | 0.2;
config["parameters/threshold"] = 0.5;
```

Do HTTP requests (you can post a body or send headers, too):

```cpp
HttpResponse resp = Http::get("https://www.somewhere.com/page.xhtml");
if(resp.code() != 200)
    return -1;
String type = resp.header("Content-Type");
String text = resp.text();
```

Or create HTTP services:

```cpp
struct TimeServer : public HttpServer
{
    void serve(HttpRequest& req, HttpResponse& resp)
    {
        if(req.is("GET", "/time")
        {
            resp.put(Var{{"time", Date::now().toString()}});
        }
        else
        {
            resp.put(Var{{"status", "error"}});
            resp.setCode(500);
        }
    }
};
TimeServer server;
server.bind(80);
server.start();
```

Decode XML:

```cpp
Xml html = Xml::decode( "<html><head><meta charset='utf8'/></head></html>" );
String charset = html("head")("meta")["charset"];   // -> "utf8"
String rootTag = html.tag();                        // -> "html"
```

Read or write a file in one line:

```cpp
String content = TextFile("somefile-uнicoδe.json").text();
```

The path given above can be Unicode UTF8, and the file content can be UTF8 with or wothout BOM,
UTF16-BE or UTF16-LE. And it will be converted to UTF8.

Emulate a simple `wget`:

```cpp
File("image.png").put( Http::get("http://hello.com/image.png").body() );
```

Decode JSON (but you can also directly load/save JSON from a file):

```cpp
Var data = Json::decode(content);
String name = data["name"];
int number = data["age"];
```

Write JSON:

```cpp
Var particle = Var{
    {"name", "proton"},
    {"mass", 1.67e-27},
    {"position", {x, y, z}}
};
String json = Json::encode(particle);
```

Write to the console with colors:

```cpp
Console console;
console.color(Console::BRED);    // bright red text
console.bgcolor(Console::CYAN);  // cyan background
printf("some highlighted text");
```

Create threads (but you can also use lambdas):

```cpp
class MyThread : public Thread
{
    void run() { do_stuff(); }
};

MyThread thread;
thread.start();
```

Send data through a TCP socket (that will try different hosts
if DNS "host" maps to several IPv4 or IPv6 addresses):

```cpp
Socket socket;                  // or TlsSocket for SSL/TLS
socket.connect("host", 9000);
socket << "hello\n";
```

Or a message through a WebSocket:

```cpp
WebSocket socket;
socket.connect("host", 9000); // or "ws://host:9000"
socket.send("hello");
```

Strings are 8 bit, by default assumed to be UTF8, and can be case converted even beyond ASCII:

```cpp
String country = "Ελλάδα";
String upper = country.toUpperCase(); // -> "ΕΛΛΆΔΑ"
```

Strings have some additional handy methods:

```cpp
if(filename.startsWith(prefix) || filename.contains("-"))
```

A string can be split and joined back:

```cpp
String names = "one,two,three";
Array<String> numbers = names.split(",");
String s123 = numbers.join(" "); // -> "one two three"
```

and can be automatically converted to UTF16:

```cpp
String dirname = "newdir";
CreateDirectoryW( dirname ); // autoconverted to UTF16
```

But don't use the above Windows-only function when you can (in UTF8):

```cpp
Directory::create("newdir");
```

or enumerate the contents of a directory:

```cpp
Directory dir("some/dir");
for(File& file : dir.files("*.txt"))
{
    String path = file.path();
    Long size = file.size();
    Date date = file.lastModified();
}
```

Copy, move or delete files:

```cpp
File("letter.doc").copy("/backup/");
File("file.conf").move("file.ini");
File("trash.doc").remove();
Directory::remove("/trash/"); // must be empty
```

Start a subprocess and read its output:

```cpp
Process p = Process::execute("someprogram.exe");
if(p.success())
    output = p.output();
```

Get the parent directory, file name and extension of a path:

```cpp
Path path = "/some/dir/file.txt";
path.directory() // -> "/some/dir/"
path.name()      // -> "file.txt"
path.nameNoExt() // -> "file"
path.extension() // -> "txt"
```

Time an operation with precision (around microseconds) and sleep for some time:

```cpp
double t1 = now();
sleep(0.5);               // 0.5 seconds
double t2 = now();
double elapsed = t2 - t1; // should be around 0.5
```

Log a message to the console and to a file:

```cpp
ASL_LOG_W("Only %i bytes available", bytesAvailable);
```



### 27. stxxl
STXXL: Standard Template Library for Extra Large Data Sets
Example code and documentation can be found on the stxxl GitHub repository: [stxxl GitHub Repository](https://github.com/stxxl/stxxl)

[GitHub Repo](https://github.com/stxxl/stxxl)


[goto github repo](https://github.com/stxxl/stxxl)


操作大于内存的vector
```cpp
#include <iostream>
#include <stxxl/sort>
#include <stxxl/vector>

int main() {
    // Define a vector with external memory support
    stxxl::vector<int> data_vector;

    // Fill the vector with some data (this data may not fit in RAM)
    for (int i = 1000000; i > 0; --i) {
        data_vector.push_back(i);
    }

    // Define a comparator for sorting
    struct IntComparator {
        bool operator()(const int& a, const int& b) const {
            return a < b;
        }
    };

    // Sort the data using external sorting
    stxxl::sort(data_vector.begin(), data_vector.end(), IntComparator(), 1024 * 1024 * 64); // 64MB of RAM for sorting

    // Print the sorted data
    for (const int& value : data_vector) {
        std::cout << value << " ";
    }

    return 0;
}
```

