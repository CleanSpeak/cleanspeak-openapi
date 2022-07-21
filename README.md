## CleanSpeak OpenAPI

This is an **experimental** OpenAPI specification for the CleanSpeak API.

The YAML file located in the root directory (cleanspeak-openapi/openapi.yaml) can be used to generate client libraries, track API changes over time and testing. More here: https://openapi.tools/

This file covers the following APIs:

* Moderate Content
* Update Content
* Proxy Moderate Content
* Proxy Update Content
* Filter Content

Use this file to do all your OpenAPI related actions. For additional information and documentation on CleanSpeak refer to [https://cleanspeak.com](https://cleanspeak.com).

To repeat, this is currently **experimental**, and we make no promises about backwards compatibility.


### Generate libraries

Install either Swagger: https://github.com/swagger-api/swagger-codegen/ or openapi: https://github.com/OpenAPITools/openapi-generator

These instructions will be for openapi.

#### Java

```
npx @openapitools/openapi-generator-cli generate -i openapi.yaml  -g java -o java
cd java
mvn package
# use jar
```

#### Ruby

To build the ruby client libraries:

Create a file called `postprocess.sh`. Put this in the file (make sure to update with the correct `sed` path):

```
/path/to/sed -i "" 's/END = "end".freeze/END_ENUM = "end".freeze/' $1
```

Set an environment variable with the full path of this script:

```
export RUBY_POST_PROCESS_FILE=/path/to/postprocess.sh
```

Copy the `openapi.yaml` file to your current directory.

Then generate the library:

```
npx @openapitools/openapi-generator-cli generate  --enable-post-process-file  -i openapi.yaml  -g ruby -o ruby
```

More docs here: https://openapi-generator.tech/docs/generators/ruby

### Test the YAML

```
pip3 install schemathesis # one time
schemathesis run -vvvv --checks not_a_server_error openapi.yaml --base-url http://localhost:9011 -H "Authorization: bf69486b-4733-4470-a592-f1bfce7af580" 
```
## Next steps

We are publishing this to see how useful the CleanSpeak community finds it. We welcome feedback on your usage of this spec. We'll plan to revisit this after we've received some feedback on how useful it is and determine if there are additional features we need to implement.

Please open bugs on this repository. For support in using this, please see the next section.

## Questions and support

If you have a question or support issue regarding this OpenAPI spec, we'd love to hear from you.

## License

The code is available as open source under the terms of the [Apache v2.0 License](https://opensource.org/licenses/Apache-2.0).
