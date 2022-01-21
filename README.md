# @meecode/grpc-server-mock

**Documentation will be improved in the near future**

## Installation

```
npm install -g @meecode/grpc-server-mock
```

## Usage

```
Usage: advanced-grpc-server-mock <command> [options]

Commands:
  advanced-grpc-server-mock start:autowire       Autowires grpc server mock using the mock folder
  advanced-grpc-server-mock start:config         Creates gRPC server mock using given config
  advanced-grpc-server-mock generate:config      Targets autowire folder and generates JSON config from it
```

### Start from auto-wire folder
Starts the server from the given autowire config.
An example can be found in the [examples folder.](./examples/autowire)

```
advanced-grpc-server-mock start:autowire
```
Options:
```
--host     Server host.                                               [default: "127.0.0.1"]
--port     Server port.                                                   [default: "50051"]
--folder   Path to folder with files for autowireing.                         [default: "."]
--silent   If set, noop logger will be used                       [boolean] [default: false]
--delay    Delay in milliseconds before returning response.                   [default: "0"]
--ordered  If set, responses will be ordered instead of random.   [boolean] [default: false]
```

Expected format:
```
|-- <autowire root folder>
|   |-- <arbitrary folder name that contains proto file and responses>
|   |   |-- <service_from_your_proto>
|   |   |   |-- <your_service_method_name1.json>
|   |   |   |-- <your_service_method_name2.json>
|   |   |-- <_otherservice_from_your_proto>
|   |   |   |-- <your_other_service_method_name1.json>
|   |   |   |-- <your_other_service_method_name2.json>
|   |   |   |-- <your_other_service_method_name3.json>
|   |   `-- <your.proto>
|   |-- <another arbitrary folder name that contains proto file and responses>
|   |   |-- <service_from_your_other_proto>
|   |   |   |-- <your_service_method_name1.json>
|   |   |   |-- <your_service_method_name2.json>
|   |   |-- <_otherservice_from_your_other_proto>
|   |   |   |-- <your_other_service_method_name1.json>
|   |   |   |-- <your_other_service_method_name2.json>
|   |   |   |-- <your_other_service_method_name3.json>
|   |   `-- <your_other.proto>
`
```
If your service is defined via multiple proto files, please provide the `root.json` file with the following format:
```json
{
  "root":"<root_proto_name(proto where the service is defined)>.proto"
}
```

Service method json format:
```json
[
  {
    "input": {
      "your_message_field_1": "<value>"
    },
    "output": {
      "your_message_response_field_1": "<value>",
      "your_message_response_field_2": "<value>"
    }
  },
  {
    "input": {
      "your_message_field_2": "<value>",
      "your_message_field_3": "<value>"
    },
    "output": {
      "your_message_response_field_2": "<value>"
    }
  }
]
```

### Start from config
Starts the server from the target config.
```
advanced-grpc-server-mock start:config
```
Options:
```
--folder   Path to file with config.                    [default: "./grpc-server-mock.json"]
--silent   If set, noop logger will be used                       [boolean] [default: false]
```

### GenerateConfigCommand
Generates Config file from target autowire folder.
```
advanced-grpc-server-mock generate:config
```
Options:
```
--host     Server host.                                               [default: "127.0.0.1"]
--port     Server port.                                                   [default: "50051"]
--folder   Path to folder with files for autowireing.                         [default: "."]
--output   Desired path to output file.                 [default: "./grpc-server-mock.json"]
--delay    Delay in milliseconds before returning response.                   [default: "0"]
--ordered  If set, responses will be ordered instead of random.   [boolean] [default: false]
```
