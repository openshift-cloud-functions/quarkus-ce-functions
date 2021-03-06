# Quarkus Cloud Functions

[![CircleCI](https://circleci.com/gh/boson-project/quarkus-ce-functions.svg?style=svg)](https://circleci.com/gh/boson-project/quarkus-ce-functions)

The Quarkus Cloud Functions stack is designed to provide a foundation for building and running Java functions on Quarkus, invoked with Cloud Events using Knative.

This stack is based on the `Quarkus 1.0.0.Final` runtime. It allows you to write Java functions that run on Quarkus and can be turned into a native executable for a low memory footprint and near instantaneous (< 10ms) start times.

## What is Quarkus?

See: https://quarkus.io/

> Kubernetes Native Java stack tailored for GraalVM & OpenJDK HotSpot, crafted from the best of breed Java libraries and standards

## Templates

Templates are used to create your local project and start your development. When initializing your project you will be provided with the default template project. This template provides a simple Quarkus application with a "Hello World!" API example.

## Getting Started

To use this stack, you'll need to work with it locally. That means, cloning this repository and running a few commands before you can get started.

```sh
    git clone https://github.com/boson-project/quarkus-ce-functions.git
    cd quarkus-ce-functions
    make
```

Once you have done this, the stack image will be available in the docker repository on your local machine. Then, follow the instructions below.

1. Create a new folder in your local directory and initialize it using the Appsody CLI, e.g.:

    ```bash
    mkdir my-project
    cd my-project
    appsody init dev.local/quarkus-functions
    ```
    This will initialize a Quarkus project using the default template.

1. After your project has been initialized you can then run your application using the following command:

    ```bash
    appsody run
    ```

    This launches a Docker container with Quarkus running in developer mode. Changes to your code (on your local disk) will automatically be detected by Quarkus (running in the container) and will be live reloaded. It also exposes port 8080, for accessing the example REST API and welcome page.

    You can continue to edit the application in your preferred IDE/editor and your changes will be reflected in the running container instantly.

3. You can try your application by visiting http://0.0.0.0:8080/ and observing the welcome page. You can also visit http://0.0.0.0:8080/hello/greeting/paul to try the REST API.

4. To try out the live reload:

    - Edit ./src/main/resources/META-INF/resources/index.html
    - Make a change to the HTML
    - Hit save in your IDE/editor
    - Refresh the page at http://0.0.0.0:8080/

You can also edit `/src/main/java/org/acme/quickstart/GreetingResource.java` and save, the REST API will be live-reloaded on the next invocation.

## Building a Production Image
Running `appsody build` will create a production image that typically boots in under 10ms. Quarkus achieves this fast boot time by using ahead of time compilation of Java into a native executable using [GraalVM](https://www.graalvm.org/). The `appsody build` process can take around 5 minutes due to the amount of time required to build a native executable.

To try this, run:

```bash
appsody build
docker run -i --rm -p 8080:8080 <my-project>:latest
```

Running the production container should give you an output similar to:

```bash
2019-07-16 12:43:21,918 INFO  [io.quarkus] (main) Quarkus 1.0.0.Final started in 0.006s. Listening on: http://0.0.0.0:8080
2019-07-16 12:43:21,918 INFO  [io.quarkus] (main) Installed features: [cdi, resteasy]
```

You can verify that this worked by visiting http://0.0.0.0:8080/ and observing the welcome page. You can also visit http://0.0.0.0:8080/hello/greeting/paul to try the REST API.

## Known Issue:

- Currently there is no configuration or documentation on `appsody debug`.

## License

This stack is licensed under the [Apache 2.0](./image/LICENSE) license
