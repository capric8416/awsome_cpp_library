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

### 11. gstreamer
Open-source multimedia framework
You can find tutorials and documentation on the official GStreamer website: [GStreamer Documentation](https://gstreamer.freedesktop.org/documentation/)

[GitHub Repo](https://github.com/GStreamer/gstreamer)

### 12. mpv
Command-line video player (library)
Usage examples and documentation can be found on the mpv website: [mpv Documentation](https://mpv.io/manual/stable/)

[GitHub Repo](https://github.com/mpv-player/mpv)
[Build mpv for Windows](https://github.com/shinchiro/mpv-winbuild-cmake)

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

### 15. nvJPEG
GPU-accelerated JPEG decoder, encoder, and transcoder
Documentation for NVIDIA nvJPEG can be found on the NVIDIA website: [NVIDIA nvJPEG Documentation](https://developer.nvidia.com/nvjpeg)

[Library Documentation](https://developer.nvidia.com/nvjpeg)

### 16. absl
Abseil Common Libraries (C++)
Documentation for Abseil can be found on the Abseil website: [Abseil Documentation](https://abseil.io/docs/cpp/)

[GitHub Repo](https://github.com/abseil



### 17. modp-base64
SIMD base64 encoder and decoder
Example code and usage instructions can be found in the GitHub repository's README: [modp_b64 GitHub Repository](https://github.com/Piasy/modp_b64)

[GitHub Repo](https://github.com/Piasy/modp_b64)

### 18. folly
An open-source C++ library developed and used at Facebook
Example code and documentation can be found on the folly GitHub repository: [folly GitHub Repository](https://github.com/facebook/folly)

[GitHub Repo](https://github.com/facebook/folly)

### 19. boost
Free peer-reviewed portable C++ source libraries
Example code and extensive documentation can be found on the Boost website: [Boost Documentation](https://www.boost.org/doc/libs/)

[Library Documentation](https://www.boost.org/doc/libs/)

### 20. libuv
Cross-platform asynchronous I/O
Example code and documentation can be found on the libuv GitHub repository: [libuv GitHub Repository](https://github.com/libuv/libuv)

[GitHub Repo](https://github.com/libuv/libuv)

### 21. openssl
TLS/SSL and crypto library
Example code and documentation can be found on the OpenSSL GitHub repository: [OpenSSL GitHub Repository](https://github.com/openssl/openssl)

[GitHub Repo](https://github.com/openssl/openssl)

### 22. imgui
Dear ImGui: Bloat-free Graphical User Interface for C++ with minimal dependencies
Example code and documentation can be found on the Dear ImGui GitHub repository: [Dear ImGui GitHub Repository](https://github.com/ocornut/imgui)

[GitHub Repo](https://github.com/ocornut/imgui)

### 23. bgfx
Cross-platform, graphics API-agnostic rendering library
Example code and documentation can be found on the bgfx GitHub repository: [bgfx GitHub Repository](https://github.com/bkaradzic/bgfx)

[GitHub Repo](https://github.com/bkaradzic/bgfx)

### 24. libplacebo
libplacebo is, in a nutshell, the core rendering algorithms and ideas of mpv rewritten as an independent library
Example code and documentation can be found on the libplacebo GitHub repository: [libplacebo GitHub Repository](https://github.com/haasn/libplacebo)

[GitHub Repo](https://github.com/haasn/libplacebo)

### 25. SPIRV-Cross
SPIRV-Cross is a practical tool and library for performing reflection on SPIR-V and disassembling SPIR-V back to high-level languages
Example code and documentation can be found on the SPIRV-Cross GitHub repository: [SPIRV-Cross GitHub Repository](https://github.com/KhronosGroup/SPIRV-Cross)

[GitHub Repo](https://github.com/KhronosGroup/SPIRV-Cross)

### 26. asl
A compact C++ cross-platform library including JSON, XML, HTTP, Sockets, WebSockets, threads, processes, logs, file system, CSV, INI files, etc
Example code and documentation can be found on the asl GitHub repository: [asl GitHub Repository](https://github.com/aslze/asl)

[GitHub Repo](https://github.com/aslze/asl)

### 27. stxxl
STXXL: Standard Template Library for Extra Large Data Sets
Example code and documentation can be found on the stxxl GitHub repository: [stxxl GitHub Repository](https://github.com/stxxl/stxxl)

[GitHub Repo](https://github.com/stxxl/stxxl)


[goto github repo](https://github.com/stxxl/stxxl)
