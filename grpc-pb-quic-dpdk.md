# gRPC - Protocol Buffers - QUIC - DPDK

**目录**

一、Protocol Buffers简介

二、Protocol Buffers相比JSON有哪些优势

三、Protocol Buffers定义、序列化、反序列化C++示例

四、gRPC (gRPC Remote Procedure Call) 简介

五、gRPC四种通信模式

六、gRPC一元请求示例

七、gRPC客户端流示例

八、gRPC服务流示例

九、gRPC双向流示例

十、gRPC使用HTTP/2作为传输协议，将支持HTTP/3和QUIC

十一、gRPC架构

十二、QUIC协议介绍

十三、QUIC Server/Client示例

十四、QUIC相比TCP有哪些优势

十五、QUIC相比UDP有哪些优势

十六、DPDK介绍

十七、DPDK通信伪码示例

十八、使用DPDK-ANS库实现tcp client server通信

十九、DPDK-ANS架构

# 一、Protocol Buffers简介

Protocol Buffers（简称ProtoBuf）是一种轻量级、高效的数据序列化格式，由Google开发并开源。它用于在不同应用程序和平台之间进行数据交换，尤其适用于网络通信和持久化存储。以下是关于Protocol Buffers的介绍：

### 1. 数据序列化和反序列化

Protocol Buffers 定义了一种结构化的数据格式，通过使用 `.proto` 文件来描述数据的结构。然后，可以使用 Protocol Buffers 编译器将 `.proto` 文件编译成各种编程语言的源代码，用于序列化和反序列化数据。

*   **序列化**: 序列化是将数据对象转换为 Protocol Buffers 格式的过程，以便将其传输到其他应用程序或进行持久化存储。
    
*   **反序列化**: 反序列化是将 Protocol Buffers 格式的数据还原为数据对象的过程，以便在应用程序中使用。
    

### 2. 特点和优势

Protocol Buffers 具有以下特点和优势：

*   **高效性**: Protocol Buffers 使用二进制编码，因此数据大小较小，序列化和反序列化速度快。
    
*   **跨语言**: Protocol Buffers 支持多种编程语言，因此您可以使用不同语言的应用程序进行通信，而无需手动编写序列化和反序列化代码。
    
*   **可扩展性**: 您可以轻松向现有 `.proto` 文件添加新字段或消息类型，而不会破坏向后兼容性。
    
*   **自描述性**: `.proto` 文件包含数据结构的定义，因此可以轻松理解数据的结构，这有助于文档和版本控制。
    
*   **适用于多种用途**: Protocol Buffers 不仅适用于网络通信，还可用于持久化存储、配置文件、日志记录等场景。
    

### 3. 如何使用 Protocol Buffers

使用 Protocol Buffers 的基本步骤包括：

1.  **定义数据结构**: 创建一个 `.proto` 文件，定义数据的结构，包括消息类型、字段和字段类型。
    
2.  **编译 .proto 文件**: 使用 Protocol Buffers 编译器将 `.proto` 文件编译成目标编程语言的源代码。
    
3.  **使用生成的代码**: 在应用程序中使用生成的代码进行数据的序列化和反序列化操作。
    
4.  **通信或存储**: 将序列化后的数据发送到其他应用程序，或将其持久化存储到文件或数据库中。
    

### 4. 学习资源

要深入学习 Protocol Buffers，您可以查阅以下资源：

*   [Protocol Buffers 官方网站](https://developers.google.com/protocol-buffers): 包含了 Protocol Buffers 的详细文档、教程和工具。
    
*   [Protocol Buffers GitHub 仓库](https://github.com/protocolbuffers/protobuf): 您可以在 GitHub 上找到 Protocol Buffers 的源代码和其他资源。
    
*   [ProtoBuf 编程指南](https://developers.google.com/protocol-buffers/docs/overview): 详细的编程指南，介绍如何使用 Protocol Buffers。
    
*   [ProtoBuf 示例](https://developers.google.com/protocol-buffers/docs/tutorials): 官方提供的示例和教程，帮助您入门。
    
*   [ProtoBuf 社区](https://groups.google.com/g/protobuf): Protocol Buffers 的官方论坛，您可以在这里提问和参与讨论。
    

Protocol Buffers 是一种强大的数据序列化格式，广泛用于各种应用程序和场景中，以提高数据的效率和可扩展性。

# 二、Protocol Buffers相比JSON有哪些优势

Protocol Buffers（ProtoBuf）和 JSON 是两种不同的数据序列化格式，它们在序列化和反序列化性能以及数据大小方面有一些重要的区别。

### 1. 性能比较

一般来说，Protocol Buffers 在性能方面通常优于 JSON。这是因为 Protocol Buffers 使用二进制编码，而 JSON 使用文本编码。以下是性能方面的比较：

*   **序列化性能**：Protocol Buffers通常比JSON更快，因为二进制数据的编码速度比文本数据快。这在高吞吐量的应用中特别有优势。
    
*   **反序列化性能**：同样，Protocol Buffers 通常比 JSON 反序列化更快，因为解析二进制数据比解析文本数据快。
    

### 2. 数据大小比较

Protocol Buffers 通常产生更小的数据量，这对于网络通信和持久化存储都是有利的。以下是数据大小方面的比较：

*   **数据大小**：由于 Protocol Buffers 使用紧凑的二进制编码，通常会生成比 JSON 更小的数据。数据大小的减小程度取决于数据的内容和结构，但通常情况下，Protocol Buffers 数据可以比 JSON 数据小 20% 到 80% 或更多。
    
*   **网络带宽**：较小的数据量意味着在网络上传输时需要更少的带宽，这对于大规模应用程序和移动设备非常重要。
    
*   **存储空间**：Protocol Buffers 生成的数据在持久化存储中占用更少的磁盘空间，这对于数据库和日志文件等数据存储方案也是有益的。
    

需要注意的是，性能和数据大小的差异取决于具体的数据和使用情况。对于小型数据或低要求性能的应用程序，JSON 可能足够好。但对于高性能和高效数据传输至关重要的应用程序，Protocol Buffers 是一个更好的选择。

最佳选择通常取决于您的特定用例和需求。在某些情况下，可以考虑使用两者的混合策略，例如使用 Protocol Buffers 进行高性能的内部通信和持久化存储，然后将数据转换为 JSON 以供外部 API 使用。这样可以充分利用 Protocol Buffers 的性能和 JSON 的人类可读性。

我们来看一个序列化结果示例，假如我要传输100个ascii字符串类型(长度依次从10到1000)，10个int型类(范围分别是int8, int16, int32, int64)，100个bytes类型(长度依次从100到10000)。

要计算准确的protobuf和json序列化结果的字节数，需要考虑以下因素：

1.  **ASCII字符串：** 你有100个ASCII字符串，长度从10到1000不等。protobuf序列化的大小将取决于字段的标签、字符串长度以及具体的编码方式。假设每个字符串占用4字节用于长度编码，再加上字符串的实际长度。protobuf的编码规则会更加紧凑，所以以下是protobuf和json序列化的估算：
    

*   protobuf：假设每个字符串平均长度为500字符，那么4字节长度编码 + 500字节数据 = 504字节/字符串。总共100个字符串，所以protobuf序列化结果约为：100 \* 504 = 50,400字节。
    
*   JSON：JSON的文本编码会导致更大的开销。假设每个字符串平均长度为500字符，再考虑JSON的标签和引号等开销，估计每个字符串需要600字节。总共100个字符串，所以JSON序列化结果约为：100 \* 600 = 60,000字节。
    

1.  **整数：** 你有10个整数，范围从int8到int64。整数的大小取决于类型，这里我们假设每个整数占用相应的字节数：
    

*   int8：1字节
    
*   int16：2字节
    
*   int32：4字节
    
*   int64：8字节
    

所以protobuf序列化结果的总字节数为：1 \* 10 + 2 \* 10 + 4 \* 10 + 8 \* 10 = 150字节。

JSON序列化结果通常会更大，因为它需要将整数表示为文本。

3.  **字节数据：** 你有100个字节数据，长度从100到10000不等。protobuf序列化的大小将取决于字段的标签、字节数据的长度以及编码方式。假设每个字节数据占用4字节用于长度编码，再加上字节数据的实际长度。以下是protobuf和json序列化的估算：
    

*   protobuf：假设每个字节数据平均长度为500字节，那么4字节长度编码 + 500字节数据 = 504字节/字节数据。总共100个字节数据，所以protobuf序列化结果约为：100 \* 504 = 50,400字节。
    
*   JSON：JSON的文本编码会导致更大的开销。假设每个字节数据平均长度为500字节，再考虑JSON的标签和引号等开销，估计每个字节数据需要600字节。总共100个字节数据，所以JSON序列化结果约为：100 \* 600 = 60,000字节。
    

**综合以上计算，protobuf序列化结果总字节数约为：50,400 (字符串) + 150 (整数) + 50,400 (字节数据) = 101,950字节。**

**JSON序列化结果总字节数约为：60,000 (字符串) + 大约更多的字节用于整数 + 60,000 (字节数据) = 总字节数会更大，但具体的字节数取决于JSON编码的细节。**

请注意，这些数字仅为估算，实际的序列化结果可能会因不同的编码库、选项和优化而有所不同。如果需要准确的字节大小，请使用具体的序列化库来进行测试。

# 三、Protocol Buffers定义、序列化、反序列化C++示例

下面是一个示例 Protocol Buffers `.proto` 文件定义一个 `Person` 结构，包括 `name` 和 `age` 两个属性：

    syntax = "proto3";
    
    message Person {
      string name = 1;
      int32 age = 2;
    }

在这个示例中，我们使用 Protocol Buffers 的 proto3 语法定义了一个名为 `Person` 的消息类型，它有两个字段：`name` 和 `age`，分别是字符串类型和整数类型。

接下来，您可以使用 Protocol Buffers 编译器生成 C++ 绑定代码。以下是生成 C++ 代码的命令：

    protoc --cpp_out=. your_proto_file.proto

请将 `your\_proto\_file.proto` 替换为包含上述 `Person` 定义的实际文件名。运行此命令后，它将在当前目录中生成一个名为 `your\_proto\_file.pb.cc` 和 `your\_proto\_file.pb.h` 的文件，其中包含了 C++ 绑定代码。

然后，您可以在您的 C++ 项目中包含生成的头文件 `your\_proto\_file.pb.h`，并使用 `Person` 结构进行操作。以下是一个示例 C++ 代码，用于创建和使用 `Person` 对象：

    #include <iostream>
    #include "your_proto_file.pb.h"
    
    int main() {
        // 创建一个 Person 对象
        Person person;
        person.set_name("John");
        person.set_age(30);
    
        // 序列化到字符串
        std::string serialized_person;
        person.SerializeToString(&serialized_person);
    
        // 反序列化
        Person deserialized_person;
        deserialized_person.ParseFromString(serialized_person);
    
        // 访问属性
        std::cout << "Name: " << deserialized_person.name() << std::endl;
        std::cout << "Age: " << deserialized_person.age() << std::endl;
    
        return 0;
    }

在这个示例中，我们首先创建一个 `Person` 对象，设置其属性，然后将其序列化为字符串。接着，我们反序列化该字符串以获取一个新的 `Person` 对象，并访问其属性。

确保根据您的实际项目配置编译器和链接器，以便正确使用 Protocol Buffers 的 C++ 绑定代码。

# 四、gRPC (gRPC Remote Procedure Call) 简介

gRPC (gRPC Remote Procedure Call) 是一个高性能、跨语言的开源远程过程调用（RPC）框架，最初由Google开发。它允许客户端和服务器之间通过定义一组方法来进行通信，就像调用本地函数一样。以下是关于gRPC的介绍文档：

### 1. gRPC 简介

gRPC 是一个现代的、高效的RPC框架，具有以下特点：

*   **跨语言**: gRPC 支持多种编程语言，包括Rust, C++, Java, Python, Go, Node.js, Ruby, C#, Objective-C等。这意味着您可以使用不同语言的客户端和服务器进行通信，而不需要编写大量的代码来处理通信细节。
    
*   **IDL (Interface Definition Language)**: gRPC 使用 Protocol Buffers（简称ProtoBuf）作为接口定义语言，用于定义服务和消息格式。这使得服务的定义非常清晰，同时自动生成客户端和服务器端的代码。
    
*   **高性能**: gRPC 使用HTTP/2协议进行通信，它具有多路复用、头部压缩等特性，可以显著提高性能。此外，gRPC还支持流式RPC，允许双向流动的数据通信。
    
*   **支持多种序列化格式**: 虽然 gRPC 默认使用 Protocol Buffers，但也支持其他序列化格式，如JSON。
    

### 2. gRPC 架构

gRPC 的架构通常包括以下组件：

*   **服务定义**: 使用 Protocol Buffers 定义 gRPC 服务的接口、方法和消息类型。
    
*   **客户端**: 客户端生成从服务定义生成的代码，以便远程调用服务器上的方法。
    
*   **服务器**: 服务器实现了由服务定义指定的方法，并在特定端口上监听客户端请求。
    
*   **传输**: gRPC 使用HTTP/2作为底层传输协议，支持多路复用、头部压缩等特性。
    

### 3. gRPC 使用场景

gRPC 在各种应用场景中都得到广泛使用，包括：

*   **微服务架构**: gRPC 适用于构建微服务架构，允许不同服务之间进行高性能的远程调用。
    
*   **分布式系统**: gRPC 可用于构建分布式系统，用于在不同节点之间进行通信。
    
*   **移动应用**: gRPC 提供了适用于移动应用的轻量级客户端库，可用于与后端服务器进行通信。
    
*   **IoT（物联网）**: gRPC 的高性能和跨语言特性使其成为连接IoT设备和云服务的理想选择。
    

### 4. gRPC 生态系统

gRPC 生态系统包括：

*   **gRPC Tools**: 提供了用于生成 gRPC 代码的工具，包括 Protocol Buffers 编译器和 gRPC 插件。
    
*   **gRPC Gateway**: 允许将 gRPC 服务转换为 HTTP/JSON API，以便与非-gRPC 客户端进行通信。
    
*   **gRPC 插件**: 各种编程语言和框架提供了 gRPC 的插件和扩展，以简化开发和集成。
    
*   **gRPC 生态库**: 有许多与 gRPC 配合使用的开源库，用于处理认证、负载均衡、日志记录等功能。
    

### 5. 学习资源

要深入学习 gRPC，您可以查阅官方文档和教程，以及在线资源，如示例代码和社区支持。以下是一些学习 gRPC 的资源：

*   [gRPC 官方网站](https://grpc.io/): 包含了 gRPC 的详细文档、示例代码和工具。
    
*   [gRPC GitHub 仓库](https://github.com/grpc/grpc): 您可以在 GitHub 上找到 gRPC 的源代码和其他资源。
    
*   [gRPC 教程](https://grpc.io/docs/languages/): 官方提供了各种语言的入门教程和示例代码。
    
*   [Protocol Buffers 官方网站](https://developers.google.com/protocol-buffers): 学习如何使用 Protocol Buffers 来定义 gRPC 服务的接口。
    
*   在线社区和论坛: 加入 gRPC 社区，参与讨论和寻求帮助，例如 Stack Overflow 上的 [gRPC 标签](https://stackoverflow.com/questions/tagged/grpc)。
    

gRPC 是一个功能强大且灵活的远程调用框架，适用于各种应用程序和场景，可以提供高性能和跨语言的通信能力。

# 五、gRPC四种通信模式

gRPC 支持多种通信模式，以下是四种主要的通信模式：

### 1. 单项 RPC（Unary RPC）

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/0864c1a1-66f3-43db-9461-be8ec617b5a1.png)

这是最常见的 RPC 类型，客户端发送一个请求到服务器，从服务器获取一个响应，就像常规的函数调用。

**.proto 定义示例**:

    service MyService {
      rpc SimpleMethod(Request) returns (Response);
    }

**客户端伪代码**:

    Request request;
    Response response;
    response = client.SimpleMethod(request);

### 2. 服务器流 RPC（Server streaming RPC）

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/d7ad594f-f919-42b5-b8bb-f8357cf75ff1.png)

客户端发送一个请求到服务器，获取一个流以读取一系列消息。客户端从返回的流中读取，直到没有更多消息为止。

**.proto 定义示例**:

    service MyService {
      rpc ServerStreamingMethod(Request) returns (stream Response);
    }

**客户端伪代码**:

    Request request;
    Response response;
    auto stream = client.ServerStreamingMethod(request);
    while (stream >> response) {
      // 处理响应
    }

### 3. 客户端流 RPC（Client streaming RPC）

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/a51aedce-4e50-40fc-88a9-7b6765aec08d.png)

客户端写入一系列消息并发送到服务器，使用提供的流。一旦客户端完成消息写入，它等待服务器读取这些消息并返回响应。

**.proto 定义示例**:

    service MyService {
      rpc ClientStreamingMethod(stream Request) returns (Response);
    }

**客户端伪代码**:

    Request request1, request2;
    Response response;
    auto stream = client.ClientStreamingMethod();
    
    // 写入消息到流中
    stream << request1;
    stream << request2;
    
    stream.Close();
    response = stream.Receive();

### 4. 双向流 RPC（Bidirectional streaming RPC）

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/61a42477-5eeb-4f76-b160-7e59ca2e2993.png)

客户端和服务器都可以读写并且交换消息使用他们的流。这两个流操作独立，所以客户端和服务器能够按照他们喜欢的任意顺序读写，例如，服务器可以等待所有客户端消息，之后再发送出去。

**.proto 定义示例**:

    service MyService {
      rpc BiDirectionalStreamingMethod(stream Request) returns (stream Response);
    }

**客户端伪代码**:

    Request request1, request2;
    Response response;
    auto stream = client.BiDirectionalStreamingMethod();
    
    // 写入消息到流中
    stream << request1;
    stream << request2;
    
    // 从流中读取响应
    while (stream >> response) {
      // 处理响应
    }
    
    stream.Close();

这四种模式为 gRPC 提供了强大的通信灵活性，使其可以满足各种应用程序和系统的需求。

# 六、gRPC一元请求示例

以下是一个使用 gRPC C++ 的一元请求示例，其中客户端调用一个名为 "Hello" 的服务，服务器返回 "World"。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `HelloService` 的服务，其中包含一个名为 `SayHello` 的方法：

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

接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

### gRPC 服务器示例：

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

### gRPC 客户端示例：

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

请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。这个示例中的服务器接收客户端的名字，并返回包含 "Hello, " 加上名字的消息。

# 七、gRPC客户端流示例

以下是一个使用 gRPC C++ 的客户端流示例，客户端不停地发送当前日期时间给服务器。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `DateTimeService` 的服务，其中包含一个名为 `StreamDateTime` 的方法：

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

接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

### gRPC 服务器示例：

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

### gRPC 客户端示例：

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

请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。在此示例中，服务器会不断地向客户端发送当前日期时间，客户端会接收并打印这些时间信息。客户端和服务器之间使用流来实现数据的持续传输。

# 八、gRPC服务流示例

以下是一个使用 gRPC C++ 的服务端流示例，服务器不停地向客户端发送当前日期时间。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `DateTimeService` 的服务，其中包含一个名为 `StreamDateTime` 的方法：

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

接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

### gRPC 服务器示例：

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

### gRPC 客户端示例：

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

请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。在此示例中，服务器会不断地向客户端发送当前日期时间，客户端会接收并打印这些时间信息。服务器和客户端之间使用流来实现数据的持续传输，这是服务端流 gRPC 的工作方式。

# 九、gRPC双向流示例

以下是一个使用 gRPC C++ 的双向流示例，双方不停地交换自身的计算机名称和当前日期时间。

首先，您需要创建一个 `.proto` 文件来定义服务和消息类型。在这个示例中，我们将创建一个名为 `ComputerInfoService` 的服务，其中包含一个名为 `ExchangeInfo` 的方法：

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

接下来，使用 Protocol Buffers 编译器生成 C++ 代码：

    protoc --grpc_out=. --cpp_out=. your_proto_file.proto

然后，您可以编写客户端和服务器的代码。

### gRPC 服务器示例：

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

### gRPC 客户端示例：

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

请确保将 `your\_proto\_file.proto` 替换为您自己的 `.proto` 文件名称，然后使用上述步骤编译和运行服务器和客户端代码。在此示例中，客户端和服务器之间建立了一个双向流，它们不停地交换计算机名称和当前日期时间。每个消息都包含计算机名称和日期时间信息。

# 十、gRPC使用HTTP/2作为传输协议，将支持HTTP/3和QUIC

gRPC 使用 HTTP/2 作为传输协议的主要原因有以下几点：

1.  **多路复用（Multiplexing）**：HTTP/2 允许在单个连接上同时传输多个请求和响应。这意味着多个 gRPC 请求可以共享相同的网络连接，而不需要为每个请求创建新的连接。这提高了效率，减少了资源消耗。
    
2.  **头部压缩（Header Compression）**：HTTP/2 引入了头部压缩机制，可以减小请求和响应的头部大小。在 gRPC 中，这对于传输大量的元数据（例如 gRPC 的请求头和响应头）非常有用，减少了网络带宽的占用。
    
3.  **流量控制（Flow Control）**：HTTP/2 支持流量控制，可以防止一个请求的数据过多地压倒接收方。这对于处理大量的并发请求非常重要，可以保持系统的稳定性和可靠性。
    
4.  **双向流（Bidirectional Streams）**：HTTP/2 支持双向流，这是 gRPC 的核心特性之一。双向流允许客户端和服务器同时发送请求和响应，而不需要等待对方完成。这种能力对于实现实时通信、流式数据传输等场景非常有用。
    
5.  **优化的二进制帧格式**：HTTP/2 使用二进制帧格式来传输数据，相对于 HTTP/1.x 的文本格式，这更加高效。这使得 gRPC 能够更有效地处理数据的序列化和反序列化。
    
6.  **连接复用（Connection Reuse）**：HTTP/2 允许长连接，这意味着客户端和服务器之间的连接可以被重复使用，而不是在每个请求之后都关闭。这减少了建立和关闭连接的开销。
    
7.  **安全性**：HTTP/2 提供了对数据的加密和认证支持，这与 gRPC 的安全性要求相符。gRPC 默认使用 TLS/SSL 来加密通信，确保数据的机密性和完整性。
    

总之，HTTP/2 提供了许多现代网络应用程序所需的性能和功能特性，使其成为 gRPC 的理想传输协议。它能够满足 gRPC 处理高效、实时和复杂通信的需求，同时减少了网络资源的消耗。因此，gRPC 选择使用 HTTP/2 作为其默认传输协议。

gRPC团队正在考虑在将来支持HTTP/3和QUIC传输协议。HTTP/3是HTTP/2的后继版本，它在传输层使用QUIC（Quick UDP Internet Connections）协议。HTTP/3和QUIC的主要目标是提高性能、减少延迟、增强安全性，以及更好地处理不稳定的网络环境。

以下是一些关于gRPC支持HTTP/3和QUIC的情况：

1.  **gRPC Web 和 HTTP/3**：目前，gRPC Web 是支持在浏览器中使用gRPC的一个项目，它通常基于HTTP/2。然而，gRPC团队正在研究如何将gRPC Web迁移到HTTP/3，以充分利用HTTP/3的性能和安全性优势。
    
2.  **QUIC和gRPC**：QUIC是一个基于UDP的传输协议，旨在提供更快的连接建立和更可靠的数据传输。gRPC团队正在研究如何在QUIC上实现gRPC，以便在需要高性能和低延迟的情况下使用。
    
3.  **Protocol Buffers 4和HTTP/3支持**：Protocol Buffers 4（protobuf 4）正在开发中，它有望提供更好的HTTP/3支持。这将有助于gRPC更紧密地集成HTTP/3和QUIC。
    

需要注意的是，gRPC是一个活跃的开源项目，不断进行演进和改进。随着HTTP/3和QUIC的逐渐普及，gRPC团队可能会加速对这些协议的支持。如果您有特定的需求或关注HTTP/3和QUIC的使用，建议随时查看gRPC的官方文档和GitHub存储库以获取最新的更新和信息。

# 十一、gRPC架构

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/758cb70d-b30d-4bcb-adaf-f68b1ce111a1.png)

gRPC Stub 是 gRPC 客户端用于与 gRPC 服务通信的代理类，它具有多种功能，使客户端能够调用远程服务的方法。以下是 gRPC Stub 的主要功能：

1.  **远程方法调用**：gRPC Stub 允许客户端调用远程服务的方法。这些方法是由 gRPC 服务定义的，客户端可以像调用本地方法一样调用它们，而无需关心底层的网络通信细节。
    
2.  **请求和响应类型映射**：gRPC Stub 负责将客户端的请求数据序列化为字节流，并将来自服务端的响应字节流反序列化为相应的数据类型。这个过程是由 Protocol Buffers 自动生成的代码完成的。
    
3.  **异步调用**：gRPC Stub 支持异步调用，客户端可以使用异步方法来发起远程调用并等待响应，而不会阻塞主线程。
    
4.  **流式调用**：gRPC Stub 支持流式调用，客户端和服务端可以在单个调用中交换多个请求和响应，实现双向流量。这对于实现实时通信和流式数据传输非常有用。
    
5.  **超时和重试**：gRPC Stub 允许客户端设置调用的超时时间，并支持在出现错误时进行重试，以增加调用的可靠性。
    
6.  **元数据传递**：gRPC Stub 允许客户端和服务端在请求和响应中传递元数据，例如身份验证凭证、请求标头等。
    
7.  **中间件（拦截器）**：gRPC Stub 支持中间件（拦截器），客户端可以通过拦截器在调用前后执行自定义逻辑，例如添加身份验证令牌、记录日志等。
    
8.  **流量控制**：gRPC Stub 支持流量控制，客户端可以控制同时进行的并发调用数量，以避免对服务端造成过大的压力。
    
9.  **连接管理**：gRPC Stub 管理与 gRPC 服务的连接，可以自动管理连接的建立和维护，以提高性能和效率。
    

gRPC 由多个关键组件构成，每个组件都扮演着不同的角色并负责不同的功能。以下是 gRPC 的主要组件以及它们的角色和功能：

1.  **Service Definition（服务定义）**：
    
    *   **角色和功能**：
        
        *   服务定义是 gRPC 的核心，它是使用 Protocol Buffers（protobuf）编写的接口描述文件（.proto 文件）。
            
        *   服务定义定义了 gRPC 服务的方法，包括方法名称、输入参数类型和输出参数类型。
            
        *   服务定义还可以包含有关服务的元数据，如身份验证要求、服务版本等。
            
2.  **Code Generation（代码生成器）**：
    
    *   **角色和功能**：
        
        *   代码生成器将服务定义文件编译成各种编程语言的客户端和服务器代码。
            
        *   生成的客户端和服务器代码包括用于远程调用的 Stub 和服务实现。
            
        *   这些生成的代码隐藏了网络通信的底层细节，使开发人员可以更容易地与 gRPC 服务交互。
            
3.  **Stub（客户端代理）**：
    
    *   **角色和功能**：
        
        *   Stub 是 gRPC 客户端用于与 gRPC 服务通信的代理类。
            
        *   Stub 提供了远程方法调用的接口，允许客户端像调用本地方法一样调用 gRPC 服务的方法。
            
        *   Stub 处理请求和响应的序列化和反序列化，以及与服务器的通信细节，如连接管理、超时和重试。
            
4.  **Server Implementation（服务端实现）**：
    
    *   **角色和功能**：
        
        *   服务端实现是 gRPC 服务的实际实现，它包含了服务定义中定义的方法的具体逻辑。
            
        *   服务端实现通常由开发人员编写，用于处理客户端的请求并生成响应。
            
        *   服务端实现通过实现服务定义中的接口来提供服务。
            
5.  **Transport Layer（传输层）**：
    
    *   **角色和功能**：
        
        *   传输层负责处理客户端和服务端之间的实际数据传输。
            
        *   gRPC 默认使用 HTTP/2 作为传输协议，提供了多路复用、头部压缩、流量控制等特性。
            
        *   传输层还处理连接的建立和维护，确保安全的通信。
            
6.  **Serialization and Deserialization（序列化和反序列化）**：
    
    *   **角色和功能**：
        
        *   序列化负责将请求和响应的数据结构转换为字节流，以便在网络上传输。
            
        *   反序列化负责将接收到的字节流转换回数据结构，以便服务端或客户端能够理解和处理数据。
            
        *   gRPC 使用 Protocol Buffers（protobuf）作为默认的序列化协议，但也支持其他序列化方式。
            
7.  **Middleware and Interceptors（中间件和拦截器）**：
    
    *   **角色和功能**：
        
        *   中间件和拦截器允许在请求和响应的处理过程中插入自定义逻辑。
            
        *   拦截器可以用于添加身份验证、日志记录、跟踪、错误处理等功能。
            
        *   这些中间件和拦截器可以通过 gRPC 提供的接口来定义和注册。
            
8.  **Load Balancing（负载均衡）**：
    
    *   **角色和功能**：
        
        *   在微服务架构中，负载均衡非常重要，以确保请求分布到多个服务实例中。
            
        *   gRPC 提供了负载均衡的支持，可以与服务发现工具集成，动态地发现和选择可用的服务实例。
            

# 十二、QUIC协议介绍

QUIC（Quick UDP Internet Connections）是一种用于传输数据的网络传输协议，最初由Google开发，旨在提供更快且更安全的网络连接。QUIC的主要特点包括：

1.  **基于UDP：** QUIC是建立在UDP（User Datagram Protocol）之上的，而不是TCP（Transmission Control Protocol）。这使得QUIC具备更低的连接建立和关闭延迟，因为它不需要像TCP那样的三次握手和四次挥手。
    
2.  **多路复用：** QUIC支持多路复用，允许在单个连接上同时传输多个数据流。这意味着可以并行发送和接收多个数据流，提高了网络效率。
    
3.  **流控制：** QUIC具有内置的流控制机制，可根据网络条件动态调整传输速率，以防止拥塞和丢包。
    
4.  **错误纠正：** QUIC包括错误纠正机制，能够自动恢复丢失的数据包，而无需等待TCP的重传机制。
    
5.  **0-RTT握手：** QUIC支持0-RTT（Zero Round-Trip Time）握手，这意味着在某些情况下，客户端可以在连接上发送数据，而不需要等待握手完成，从而降低延迟。
    
6.  **安全性：** QUIC内置了TLS（Transport Layer Security）协议，确保数据在传输过程中得到加密和认证，提供了更高的安全性。
    
7.  **动态变化：** QUIC的设计允许协议的改进和更新，而无需修改操作系统内核，因此更容易进行协议升级。
    
8.  **NAT穿越：** QUIC通过使用随机化的连接ID和0-RTT握手，有助于穿越NAT设备，从而改善了对等连接的建立。
    

QUIC已经被广泛部署，并且逐渐成为Web应用程序和服务的首选协议，特别是对于支持HTTP/3的Web服务器。HTTP/3是基于QUIC的协议，用于更快地传输Web内容。它的主要目标是提供更低的延迟、更高的性能和更好的安全性，以改善用户体验。

需要注意的是，QUIC是一个快速发展的协议，其规范可能会有所变化，因此在实际使用时需要关注最新的协议规范和实施细节。

# 十三、QUIC Server/Client示例

在C++中编写QUIC协议的完整示例是一个相对复杂的任务，因为QUIC是一个底层协议，需要使用专门的库来实现。一个常用的QUIC库是Google的QUIC库，也有其他一些库可供选择。下面是一个简化的示例，使用QUIC库（基于Google QUIC的实现）来创建一个QUIC协议的服务器和客户端，它们互相发送日期时间和递增ID。

请注意，这个示例假定你已经安装了适当的QUIC库（例如，quiche库），并且你的编译环境已经设置好。

**QUIC服务器示例：**

    #include <quiche/quiche.h>
    
    int main() {
        // 创建QUIC监听套接字
        int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
        if (sockfd < 0) {
            perror("socket");
            return -1;
        }
    
        struct sockaddr_in server_addr;
        memset(&server_addr, 0, sizeof(server_addr));
        server_addr.sin_family = AF_INET;
        server_addr.sin_addr.s_addr = INADDR_ANY;
        server_addr.sin_port = htons(12345); // 替换为你想要使用的端口号
    
        if (bind(sockfd, (struct sockaddr*)&server_addr, sizeof(server_addr)) < 0) {
            perror("bind");
            close(sockfd);
            return -1;
        }
    
        quiche_config *config = quiche_config_new();
        quiche_config_set_application_protos(config, (uint8_t *)QUICHE_H3_APPLICATION_PROTOCOL, sizeof(QUICHE_H3_APPLICATION_PROTOCOL) - 1);
        
        // 创建QUIC连接
        quiche_conn *conn = quiche_accept(NULL, sockfd, &server_addr, sizeof(server_addr), config);
    
        uint8_t buf[65535];
        ssize_t recv_len;
        
        while (1) {
            recv_len = recv(sockfd, buf, sizeof(buf), 0);
            if (recv_len < 0) {
                perror("recv");
                break;
            }
    
            quiche_recv(conn, buf, recv_len);
    
            // 处理接收到的数据，这里可以解析日期时间和递增ID，并回复数据
            // ...
        }
    
        quiche_conn_free(conn);
        quiche_config_free(config);
        close(sockfd);
    
        return 0;
    }

**QUIC客户端示例：**

    #include <quiche/quiche.h>
    
    int main() {
        // 创建QUIC套接字
        int sockfd = socket(AF_INET, SOCK_DGRAM, 0);
        if (sockfd < 0) {
            perror("socket");
            return -1;
        }
    
        quiche_config *config = quiche_config_new();
        
        // 创建QUIC连接
        quiche_conn *conn = quiche_connect("127.0.0.1", 12345, config);
    
        uint8_t buf[65535];
        ssize_t recv_len;
    
        while (1) {
            // 创建日期时间和递增ID数据，将其发送给服务器
            // ...
            
            quiche_send(conn, buf, send_len);
    
            ssize_t send_len = quiche_send(conn, buf, sizeof(buf));
            if (send_len < 0) {
                perror("quiche_send");
                break;
            }
    
            recv_len = recv(sockfd, buf, sizeof(buf), 0);
            if (recv_len < 0) {
                perror("recv");
                break;
            }
    
            quiche_recv(conn, buf, recv_len);
    
            // 处理接收到的数据，这里可以解析服务器发送的日期时间和递增ID
            // ...
        }
    
        quiche_conn_free(conn);
        quiche_config_free(config);
        close(sockfd);
    
        return 0;
    }

请注意，上述示例是一个简化版本，真实的QUIC应用程序可能需要更多的配置和错误处理。你需要根据你的需求来编写完整的服务器和客户端代码，并确保使用正确的QUIC库。同时，你还需要实现日期时间和递增ID的生成和解析逻辑，以便在数据交换中使用。

# 十四、QUIC相比TCP有哪些优势

QUIC（Quick UDP Internet Connections）的诞生背景和与TCP比较的优势可以总结如下：

**背景：**

1.  **网络性能需求提升：** 在现代互联网中，用户对网络性能的要求越来越高，特别是在移动设备和高延迟网络上。传统的TCP协议存在一些性能瓶颈，例如握手延迟和拥塞控制算法可能不够灵活，因此需要更快速、更灵活的协议来满足这些需求。
    
2.  **HTTPS加密：** 为了保护用户数据的隐私和安全，大部分网站都使用了HTTPS协议来进行加密通信。然而，建立TLS（Transport Layer Security）连接需要多次往返，这增加了延迟，因此需要一种更快速的方式来处理加密通信。
    
3.  **HTTP/2和HTTP/3的发展：** HTTP/2和HTTP/3是基于TCP的协议，它们引入了多路复用和头部压缩等特性，但仍然受限于TCP的一些局限性，例如队头阻塞（Head-of-Line Blocking）问题。因此，需要一种底层协议来进一步优化HTTP/2和HTTP/3的性能。
    

**与TCP比较的优势：**

1.  **连接建立速度：** QUIC使用0-RTT握手，可以实现更快的连接建立，因为它可以在第一次通信时就携带数据，而无需等待握手完成。
    
2.  **多路复用：** QUIC支持多路复用，允许在单个连接上同时传输多个数据流，从而提高了网络效率。TCP在多个数据流之间可能存在队头阻塞问题，而QUIC能够减轻这个问题。
    
3.  **拥塞控制：** QUIC具有自适应拥塞控制机制，可以更快地适应网络条件的变化，从而降低了拥塞的可能性。
    
4.  **流量控制：** QUIC内置了流量控制机制，可以更精确地管理每个数据流的传输速率，防止过度消耗网络带宽。
    
5.  **容错性：** QUIC具有错误纠正机制，可以自动恢复丢失的数据包，而无需等待TCP的重传机制。
    
6.  **安全性：** QUIC内置了TLS加密，提供了更高的安全性，同时避免了TLS握手的多次往返延迟。
    
7.  **灵活性：** QUIC的设计允许协议的改进和更新，而无需修改操作系统内核，因此更容易进行协议升级。
    

总的来说，QUIC通过减少握手延迟、支持多路复用、改进拥塞控制和提供更好的安全性等特性，使其在性能和用户体验方面相对于传统TCP有明显的优势。这使得QUIC成为越来越多应用程序和服务的首选协议，特别是在需要高性能和安全性的情况下。

# 十五、QUIC相比UDP有哪些优势

QUIC（Quick UDP Internet Connections）与UDP（User Datagram Protocol）相比具有以下优势：

1.  **可靠性：** QUIC内置了可靠性机制，包括错误纠正和重传，以确保数据的可靠传输。UDP本身是不可靠的传输协议，不提供数据包的重传和错误处理功能，因此在需要可靠性的应用场景下，QUIC更适合。
    
2.  **安全性：** QUIC集成了TLS（Transport Layer Security）协议，提供端到端的加密和身份验证，确保数据在传输过程中的保密性和完整性。UDP不提供内置的加密和身份验证，因此需要额外的安全层，如DTLS（Datagram Transport Layer Security）来提供类似的保护。
    
3.  **多路复用：** QUIC支持多路复用，允许在单个连接上同时传输多个数据流，提高了网络效率。UDP只能将数据包按原始顺序传输，没有多路复用功能。
    
4.  **流量控制：** QUIC内置了流量控制机制，可以根据网络条件动态调整传输速率，以防止拥塞和丢包。UDP不提供流量控制功能，需要应用程序自行实现。
    
5.  **连接管理：** QUIC具有连接管理机制，允许创建和管理多个连接，这对于支持多个并发会话的应用程序非常有用。UDP是一种无连接协议，不具备连接管理能力。
    
6.  **NAT穿越：** QUIC使用随机化的连接ID和0-RTT握手等技术，有助于穿越NAT设备，从而改善对等连接的建立。UDP通常需要特殊的NAT穿越技术，如STUN（Session Traversal Utilities for NAT）或TURN（Traversal Using Relays around NAT）来实现。
    
7.  **升级和改进：** QUIC的设计允许协议的改进和更新，而无需修改操作系统内核，因此更容易进行协议升级。UDP是一个固定的协议，不支持动态升级。
    

总之，QUIC在可靠性、安全性、多路复用、流量控制、连接管理、NAT穿越以及协议升级等方面具有明显的优势，使其成为越来越多应用程序和服务的首选协议，特别是在需要高性能、可靠性和安全性的情况下。但需要注意的是，UDP仍然在某些特定用途下有其价值，例如实时音视频传输等，因为它的低延迟特性可能对这些应用更为重要。

# 十六、DPDK介绍

DPDK（Data Plane Development Kit）是一个开源的、高性能的数据平面开发工具集，旨在加速数据包处理和数据平面应用程序的开发。以下是有关DPDK的背景、它解决的问题以及它的优势的一些关键信息：

**背景：**

在网络领域，数据平面通常指的是处理网络数据包的部分，它需要处理大量的数据包，要求低延迟和高吞吐量。传统的网络堆栈和操作系统内核网络协议栈通常无法满足这些要求，因为它们包含了大量的通用代码和复杂的数据包处理路径，导致性能受限。DPDK应运而生，旨在解决这些性能问题。

**解决的痛点：**

1.  **高性能要求：** 一些应用程序，如网络路由、防火墙、负载均衡、虚拟化、SDN（Software Defined Networking）等，需要在高速网络上实现低延迟和高吞吐量的数据包处理。传统网络协议栈和内核网络堆栈的性能不能满足这些要求。
    
2.  **通用性能瓶颈：** 通用操作系统内核网络协议栈包含了大量适用于各种应用的通用代码，这增加了数据包处理的复杂性和延迟。许多应用需要更精简的、专用的数据平面来获得更好的性能。
    
3.  **硬件加速：** 现代网络接口卡（NIC）通常具有硬件加速功能，如SR-IOV（Single Root I/O Virtualization）和RDMA（Remote Direct Memory Access），传统网络协议栈难以充分利用这些硬件加速功能。
    

**DPDK的提升：**

DPDK通过以下方式提升了数据包处理的性能和效率：

1.  **用户态驱动：** DPDK允许网络应用程序在用户态下运行，而不是在内核态下，从而避免了内核态和用户态之间的上下文切换开销，提高了性能。
    
2.  **零拷贝：** DPDK支持零拷贝技术，允许数据包在内存中的移动而无需复制，减少了数据包处理的复杂性和延迟。
    
3.  **硬件加速：** DPDK充分利用现代NIC的硬件加速功能，例如数据包分类、分流、分发等，以提高吞吐量。
    
4.  **优化的数据结构：** DPDK使用高效的数据结构和算法来加速数据包处理，例如环形缓冲区、位图、散列表等。
    
5.  **多核支持：** DPDK可以有效地利用多核处理器，允许并行处理多个数据包，从而提高整体性能。
    
6.  **高性能驱动程序：** DPDK包括了一系列高性能的驱动程序，与常见的NIC硬件兼容，以获得最佳性能。
    
7.  **应用库和工具：** DPDK提供了一系列的库和工具，用于快速开发高性能的数据平面应用程序，包括包括Open vSwitch（OvS）、Suricata、Snort等。
    

总的来说，DPDK是一个强大的工具集，解决了在高性能数据包处理场景中遇到的许多问题，使网络应用程序能够获得更低的延迟、更高的吞吐量和更好的性能。它在云计算、网络功能虚拟化、边缘计算等领域得到广泛应用。

# 十七、DPDK通信伪码示例

对不起，我之前的回答确实没有涉及DPDK。为了使用DPDK与QUIC协议一起工作，您需要将QUIC与DPDK集成在一起。以下是一个概念示例，展示如何使用DPDK与QUIC一起创建服务器和客户端，它们分别发送日期时间和递增ID给对方。

首先，确保您已经安装和配置了DPDK，并正确初始化了DPDK环境。然后，您可以创建一个基于DPDK的网络应用程序，其中包括QUIC协议。

请注意，以下示例仅用于概念演示，实际实现可能需要更多的细节和错误处理。

    #include <iostream>
    #include <thread>
    #include <rte_eal.h>
    #include <rte_ethdev.h>
    
    // DPDK初始化
    void dpdk_initialize(int argc, char** argv) {
        rte_eal_init(argc, argv);
        // 初始化DPDK的其他配置，如网卡绑定、内存配置等
    }
    
    // DPDK服务器
    void run_dpdk_server() {
        // 初始化DPDK
        int argc = 2; // 替换为实际参数数量
    
        char* argv[ ] = {"dpdk_server", "-c", "0x01"}; // 替换为实际参数
    
        dpdk_initialize(argc, argv);
    
        // 创建DPDK端口和配置
        uint16_t port_id = 0; // 替换为实际的网卡端口号
        struct rte_eth_conf port_conf = {0};
        rte_eth_dev_configure(port_id, 1, 1, &port_conf);
    
        // 启动DPDK端口
        rte_eth_dev_start(port_id);
    
        // 等待DPDK线程
        while (true) {
            rte_eal_mp_wait_lcore();
        }
    }
    
    // DPDK客户端
    void run_dpdk_client() {
        // 初始化DPDK
        int argc = 2; // 替换为实际参数数量
    
        char* argv[ ] = {"dpdk_client", "-c", "0x02"}; // 替换为实际参数
    
        dpdk_initialize(argc, argv);
    
        // 创建DPDK端口和配置
        uint16_t port_id = 0; // 替换为实际的网卡端口号
        struct rte_eth_conf port_conf = {0};
        rte_eth_dev_configure(port_id, 1, 1, &port_conf);
    
        // 启动DPDK端口
        rte_eth_dev_start(port_id);
    
        // 创建QUIC连接并发送数据
        // ...
    
        // 等待DPDK线程
        while (true) {
            rte_eal_mp_wait_lcore();
        }
    }
    
    int main() {
        // 启动DPDK服务器和客户端
        std::thread server_thread(run_dpdk_server);
        std::thread client_thread(run_dpdk_client);
    
        // 等待线程结束
        server_thread.join();
        client_thread.join();
    
        return 0;
    }

在这个示例中，我们首先初始化了DPDK环境，并创建了DPDK端口。然后，在服务器和客户端中，您可以使用DPDK来处理网络数据包，并在QUIC连接上发送日期时间和递增ID。请注意，这只是一个概念示例，实际的实现可能会更加复杂，具体的QUIC库和数据包处理逻辑需要根据您的需求进行选择和开发。

# 十八、使用DPDK-ANS库实现tcp client server通信

DPDK-ANS（DPDK Accelerated Network Stack）的库，它是一个用于实现高性能网络应用的开源项目。以下是使用DPDK-ANS来创建TCP客户端和服务器的一般步骤：

1.  **准备DPDK环境**：
    
    *   配置和初始化DPDK环境，包括绑定网络接口和分配大页内存等。
        
2.  **下载和构建DPDK-ANS**：
    
    *   下载 DPDK-ANS 的源代码。
        
    *   使用 DPDK 提供的工具来构建 DPDK-ANS。
        
3.  **编写客户端和服务器代码**：
    
    *   创建一个客户端程序和一个服务器程序。
        
    *   在你的程序中，包含 DPDK-ANS 的头文件并使用其API来实现TCP通信逻辑。
        
4.  **初始化DPDK-ANS**：
    
    *   在程序中初始化 DPDK-ANS，并配置网络接口。
        
5.  **实现TCP客户端和服务器逻辑**：
    
    *   在客户端程序中，创建套接字、连接到服务器、发送和接收数据。
        
    *   在服务器程序中，创建套接字、绑定地址、监听连接请求、接受连接、处理客户端请求、发送和接收数据。
        
6.  **编译和链接**：
    
    *   使用 DPDK 的编译工具来编译和链接你的客户端和服务器程序，确保链接 DPDK-ANS 库。
        
7.  **运行应用程序**：
    
    *   在DPDK环境中运行你的客户端和服务器程序。
        

请注意，具体的代码实现和配置会根据你的应用程序需求而有所不同。DPDK-ANS 提供了一些示例代码和文档，可以帮助你入门。

DPDK-ANS 项目的 GitHub 页面可能包含了详细的文档和示例代码，以帮助你开始。在实际实施之前，建议详细研究DPDK-ANS的文档和示例，以确保你的TCP客户端和服务器满足你的性能和功能需求。此外，也可以查找其他类似的开源DPDK TCP库，以找到适合你的项目的最佳解决方案。

    #include <rte_eal.h>
    #include <rte_ethdev.h>
    #include <rte_mbuf.h>
    #include <dpdk_ans.h>
    
    #define CLIENT_IP   "127.0.0.1"
    #define SERVER_IP   "127.0.0.1"
    #define CLIENT_PORT 12345
    #define SERVER_PORT 54321
    
    #define MAX_PACKET_SIZE 1500
    
    // 初始化DPDK
    static void init_dpdk(int argc, char *argv[]) {
        rte_eal_init(argc, argv);
        // 初始化DPDK-ANS
        ans_init();
    }
    
    // 客户端逻辑
    static void run_client() {
        struct ans_socket *sock;
        sock = ans_socket(AF_INET, SOCK_STREAM, 0);
    
        struct sockaddr_in server_addr;
        server_addr.sin_family = AF_INET;
        server_addr.sin_port = SERVER_PORT;
        server_addr.sin_addr.s_addr = inet_addr(SERVER_IP);
    
        ans_connect(sock, (struct sockaddr *)&server_addr, sizeof(server_addr));
    
        char send_buffer[MAX_PACKET_SIZE];
        char recv_buffer[MAX_PACKET_SIZE];
    
        // 发送数据
        strcpy(send_buffer, "Hello, server!");
        ans_send(sock, send_buffer, strlen(send_buffer), 0);
    
        // 接收数据
        int recv_size = ans_recv(sock, recv_buffer, sizeof(recv_buffer), 0);
        if (recv_size > 0) {
            recv_buffer[recv_size] = '\0';
            printf("Received from server: %s\n", recv_buffer);
        }
    
        ans_close(sock);
    }
    
    // 服务器逻辑
    static void run_server() {
        struct ans_socket *sock;
        sock = ans_socket(AF_INET, SOCK_STREAM, 0);
    
        struct sockaddr_in server_addr;
        server_addr.sin_family = AF_INET;
        server_addr.sin_port = SERVER_PORT;
        server_addr.sin_addr.s_addr = INADDR_ANY;
    
        ans_bind(sock, (struct sockaddr *)&server_addr, sizeof(server_addr));
        ans_listen(sock, 5);
    
        while (1) {
            struct ans_socket *client_sock;
            client_sock = ans_accept(sock, NULL, NULL);
    
            char recv_buffer[MAX_PACKET_SIZE];
    
            // 接收数据
            int recv_size = ans_recv(client_sock, recv_buffer, sizeof(recv_buffer), 0);
            if (recv_size > 0) {
                recv_buffer[recv_size] = '\0';
                printf("Received from client: %s\n", recv_buffer);
            }
    
            // 发送数据
            char send_buffer[MAX_PACKET_SIZE];
            strcpy(send_buffer, "Hello, client!");
            ans_send(client_sock, send_buffer, strlen(send_buffer), 0);
    
            ans_close(client_sock);
        }
    
        ans_close(sock);
    }
    
    int main(int argc, char *argv[]) {
        init_dpdk(argc, argv);
    
        // 根据命令行参数选择运行客户端或服务器
        if (argc == 2 && strcmp(argv[1], "client") == 0) {
            run_client();
        } else if (argc == 2 && strcmp(argv[1], "server") == 0) {
            run_server();
        } else {
            printf("Usage: %s <client/server>\n", argv[0]);
            return -1;
        }
    
        return 0;
    }

# 十九、DPDK-ANS架构

librte\_ans：TCP/IP 堆栈静态库。ANS 使用 dpdk mbuf、ring、memzone、mempool、timer、spinlock。所以在 dpdk 和 ANS 之间零拷贝 mbuf。 librte\_anssock：应用程序的 ANS 套接字库，ANS 和应用程序之间的零复制。 librte\_anscli：用于路由/ip/neigh/link 配置的 ANS cli 库。 cli：用于配置 ANS tcp/ip 堆栈的命令。 示例：ANS 应用示例。 测试：带有 ANS 的示例应用程序，用于测试 ANS tcp/ip 堆栈

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/f0b4c048-5960-4356-9c42-ecd0f3b972f9.png)

![image](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/54Lq3e4WkbWRl7Ed/img/01ca70e1-759e-44e1-87a0-3c1e350b1733.png)

支持环境

EAL 基于 dpdk-18.11； linux 版本： 4.4.0-45-generic (Ubuntu 16.04.1 LTS)。 gcc 版本： gcc 版本 5.4.0 20160609。 支持功能：

ANS 初始化； ANS 在容器中运行； Ether，NIC 和 ANS TCP/IP 堆栈之间的零复制； ARP，ARP超时； IP层，IP分片和重组； 高性能路由； ICMP; 访问控制列表； 绕过流量到linux内核； 从 linux 内核同步 IP/路由； 支持动态路由（OSPF/BGP…）； 支持DHCP客户端； 命令行界面：

添加、删除、显示IP地址； 添加、删除、显示静态路由； 显示邻居表； 显示界面和统计信息； 显示 IP 统计信息； 添加、删除、显示ACL； 添加、删除、显示绕过规则； 显示端口队列 lcore 映射； 添加、删除、显示流量过滤规则； UDP协议； 套接字层； Socket API兼容BSD，APP可以基于开关选择ANS socket或linux socket。 socket/bind/connect/listen/close/send/recv/epoll/writev/readv/shutdown…; 支持openssl； TCP协议； 支持可靠传输； 支持基于dupack的重传，基于超时的重传； 支持流量控制； 支持拥塞控制：newreno/cubic/vegas…； 支持最大段大小； 支持选择性确认； 支持窗口缩放； 支持TCP时间戳； 支持TCP ECN； 支持保持活力； 支持SO\_REUSEPORT，多个应用可以监听同一个端口； 支持多核tcp堆栈，每个lcore每个tcp堆栈； 支持TSO。 路由器； 支持虚拟主机； 支持虚拟用户； 支撑刀； 支持敲击； 硬件;

x86：broadwell、haswell、ivybridge、knl、sandybridge、westmere 等。 arm：arm64 SoC 和边缘计算机；

    #define _GNU_SOURCE
    #include <stdio.h>
    #include <stdlib.h>
    #include <sched.h>
    #include <unistd.h>
    #include <sys/times.h>
    
    #include <stdint.h>
    #include <string.h>
    #include <stdarg.h>
    #include <errno.h>
    #include <netinet/in.h>
    #include <termios.h>
    #include <sys/epoll.h>
    
    #include <sys/types.h>
    #include <sys/socket.h>
    #include <arpa/inet.h>
    
    #ifndef __linux__
    #ifdef __FreeBSD__
    #include <sys/socket.h>
    #else
    #include <net/socket.h>
    #endif
    #endif
    
    #include <sys/time.h>
    #include "anssock_intf.h"
    #include "ans_errno.h"
    
    
    #define BUFFER_SIZE 5000
    #define MAX_EVENTS 512
    #define MAX_CPUS 8
    
    char *http_200 = "HTTP/1.0 200 OK\r\n"
                     "Cache-Control: no-cache\r\n"
                     "Connection: close\r\n"
                     "Content-Type: text/html\r\n"
                     "\r\n"
                     "<html><body><h1>200 OK</h1>\nHello world.\n</body></html>\n";
    
    static int HandleReadEvent(int epoll_fd, struct epoll_event ev)
    {
        int rd;
        int i;
        int len;
        int sent;
        char recv_buf[BUFFER_SIZE];
        int sockid = ev.data.fd;
        /* HTTP request handling */
        rd = anssock_recvfrom(sockid, recv_buf, BUFFER_SIZE, 0, NULL, NULL);
    
        if (rd <= 0) {
            return rd;
        }
        /* just response http 200*/
        len = strlen(http_200);
        sent = anssock_send(ev.data.fd, http_200, len, 0);
    
        ev.events = EPOLLIN | EPOLLOUT;
        anssock_epoll_ctl(epoll_fd, EPOLL_CTL_DEL, sockid, NULL);
    //    printf("read and close sockid:%d\n", sockid); //test purpose
        return rd;
    }
    
    
    int RunServerThread()
    {
        int ret;
        int server_sockfd;
        int client_sockfd;
        struct sockaddr_in my_addr;
        struct sockaddr_in remote_addr;
        int sin_size;
        int do_accept;
        int opt_val = 1;
    
        ret = anssock_init(NULL);
        if (ret != 0)
            printf("init sock failed \n");
    
        // end initialized
        memset(&my_addr, 0, sizeof(my_addr));
        my_addr.sin_family = AF_INET;
        my_addr.sin_addr.s_addr = INADDR_ANY;
        my_addr.sin_port = htons(8089);
    
        if ((server_sockfd = anssock_socket(AF_INET, SOCK_STREAM, 0)) < 0)
        {
            printf("socket error \n");
            return 1;
        }
    
        if(anssock_setsockopt(server_sockfd, SOL_SOCKET, SO_REUSEPORT, &opt_val, sizeof(int)) < 0)
        {
            printf("set socket option failed \n");
        }
    
        if (anssock_bind(server_sockfd, (struct sockaddr *)&my_addr, sizeof(struct sockaddr)) < 0)
        {
            printf("bind error \n");
            return 1;
        }
    
        if (anssock_listen(server_sockfd, 2048) < 0)
        {
            printf("listen error \n");
            return 1;
        }
    
        sin_size = sizeof(struct sockaddr_in);
        /* wait for incoming accept events */
        /* create epoll descriptor */
        int epoll_fd;
        epoll_fd = anssock_epoll_create(MAX_EVENTS);
        if (epoll_fd == -1)
        {
            printf("epoll_create failed \n");
            return 1;
        }
    
        struct epoll_event ev;
        struct epoll_event events[MAX_EVENTS];
        ev.events = EPOLLIN | EPOLLET;
        ev.data.fd = server_sockfd;
    
        if (anssock_epoll_ctl(epoll_fd, EPOLL_CTL_ADD, server_sockfd, &ev) == -1)
        {
            printf("epll_ctl:server_sockfd register failed");
            anssock_close(server_sockfd);
            anssock_close(epoll_fd);
            return 1;
        }
    
        int nfds;
        struct sockaddr_in* pV4Addr = (struct sockaddr_in*)&my_addr;
        int ipAddr = pV4Addr->sin_addr.s_addr;
        char ipstr[INET_ADDRSTRLEN];
        inet_ntop( AF_INET, &ipAddr, ipstr, INET_ADDRSTRLEN );
        printf("open socket on ip:%s  port: %d\n", ipstr, ntohs(my_addr.sin_port));
    
        while (1)
        {
            nfds = anssock_epoll_wait(epoll_fd, events, MAX_EVENTS, -1);
            if (nfds == -1)  {
                printf("start epoll_wait failed");
                anssock_close(server_sockfd);
                anssock_close(epoll_fd);
                return 1;
            }
    
            int i;
            do_accept = 0;
            for (i = 0; i < nfds; i++)
            {
                int sockid = events[i].data.fd;
                if (sockid == server_sockfd) { //accept case
                    do_accept = 1;
                }
                else
                {
                    if (events[i].events & EPOLLERR) { //epoll error event
                        int err;
                        socklen_t len = sizeof(err);
    
                        /* error on the connection */
                        anssock_epoll_ctl(epoll_fd, EPOLL_CTL_DEL, sockid, NULL);
                        anssock_close(sockid);
                    }
                    if (events[i].events == EPOLLIN) { //epollin  read and write
                        int ret = HandleReadEvent(epoll_fd, events[i]);
                        anssock_close(sockid);
                    }
                    if (events[i].events == EPOLLOUT) { //epollout write
                        int LEN = strlen(http_200);
                        anssock_send(sockid, http_200, LEN, 0);
                        anssock_epoll_ctl(epoll_fd, EPOLL_CTL_DEL, sockid, NULL);
                        anssock_close(sockid);
                    }
                    if (events[i].events == EPOLLHUP) { //remote close the socket
                        anssock_epoll_ctl(epoll_fd, EPOLL_CTL_DEL, sockid, NULL);
                        anssock_close(sockid);
                    }
                }
            }
            if (do_accept) {
                while (1) {
                    int c = anssock_accept(server_sockfd, NULL, NULL);
                    if (c >= 0) {
                        struct epoll_event ev;
                        //accept connection and wait EPOLLIN EVENT
                        ev.events = EPOLLIN | EPOLLET;
                        ev.data.fd = c;
                        anssock_epoll_ctl(epoll_fd, EPOLL_CTL_ADD, c, &ev);
                        //      printf("Socket %d registered.\n", c);
                    } else {  //c<0
                        /*     printf("mtcp_accept() error %s\n",
                                   strerror(errno));*/
                        break;
                    }
                }
            }//end if
        }
        anssock_close(server_sockfd);
    
        return 0;
    }
    
    
    int main(int argc, char *argv[])
    {
        int core =0;
    
        if(argc >= 2)
        {
            core = atoi(argv[1]);
            printf("affinity to core %d \n", core);
        }
        else
        {
            printf("affinity to 0 core by default \n");
        }
    
          /*initialize thread bind cpu*/
        cpu_set_t cpus;
    
        CPU_ZERO(&cpus);
        CPU_SET((unsigned)core, &cpus);
        sched_setaffinity(0, sizeof(cpus), &cpus);
    
        RunServerThread();
    }
    

    #define _GNU_SOURCE
    #include <stdio.h>
    #include <stdlib.h>
    #include <sched.h>
    #include <unistd.h>
    #include <string.h>
    #include <arpa/inet.h>
    #include "anssock_intf.h"
    
    #define SERVER_IP "127.0.0.1"
    #define SERVER_PORT 8089
    #define BUFFER_SIZE 5000
    
    int main(int argc, char *argv[])
    {
        int core = 0;
    
        if (argc >= 2)
        {
            core = atoi(argv[1]);
            printf("affinity to core %d \n", core);
        }
        else
        {
            printf("affinity to 0 core by default \n");
        }
    
        /* Initialize thread bind CPU */
        cpu_set_t cpus;
    
        CPU_ZERO(&cpus);
        CPU_SET((unsigned)core, &cpus);
        sched_setaffinity(0, sizeof(cpus), &cpus);
    
        int client_sockfd;
        struct sockaddr_in server_addr;
        int ret;
    
        ret = anssock_init(NULL);
        if (ret != 0)
        {
            printf("init sock failed \n");
            return 1;
        }
    
        client_sockfd = anssock_socket(AF_INET, SOCK_STREAM, 0);
        if (client_sockfd < 0)
        {
            printf("socket error \n");
            return 1;
        }
    
        memset(&server_addr, 0, sizeof(server_addr));
        server_addr.sin_family = AF_INET;
        server_addr.sin_port = htons(SERVER_PORT);
        inet_pton(AF_INET, SERVER_IP, &(server_addr.sin_addr));
    
        ret = anssock_connect(client_sockfd, (struct sockaddr *)&server_addr, sizeof(server_addr));
        if (ret < 0)
        {
            printf("connect error \n");
            return 1;
        }
    
        char request[] = "GET / HTTP/1.1\r\nHost: 127.0.0.1:8089\r\n\r\n";
        anssock_send(client_sockfd, request, strlen(request), 0);
    
        char response[BUFFER_SIZE];
        memset(response, 0, sizeof(response));
        int recv_len = anssock_recv(client_sockfd, response, BUFFER_SIZE, 0);
    
        if (recv_len > 0)
        {
            printf("Received response from server:\n");
            printf("%s\n", response);
        }
        else
        {
            printf("Failed to receive response from server.\n");
        }
    
        anssock_close(client_sockfd);
        return 0;
    }
