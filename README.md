# SportRadar API Proxy 🏈🏀⚽

A lightweight proxy for the **SportsRadar API**, making integration seamless and hassle-free.  

## Features:

✅ **Automatic API Key Handling** – Forwards all requests while appending your API key.  
✅ **Transparent Responses** – Returns results exactly as received from SportsRadar.  
✅ **CORS-Friendly** – Enables access from any domain, avoiding browser CORS issues.  

Effortless SportsRadar API access, with no headaches! 🚀

## Pre-requisits

Install runtime dependencies with the corresponding script for your OS (`install-on-<os>.sh`), for example:

```bash
sh install-on-mac.sh
```

## Using the proxy

Provide you API Key in a `.env` file:

```bash
cp .sample.env .env

# set the API key in the .env file
```

Run the image with Docker Compose like this:

```bash
# Start the service
docker-compose up -d

# Check logs
docker-compose logs -f

# Stop the service
docker-compose down
```

After a few seconds you will see output similar to the following in the terminal window:

```
2025-02-05 23:11:21.897  INFO 72056 --- [           main] e.camel.impl.engine.AbstractCamelContext : Apache Camel 4.9.0 (sport-radar-proxy) is starting
2025-02-05 23:11:21.982  INFO 72056 --- [           main] vertx.core.spi.resolver.ResolverProvider : Using the default address resolver as the dns resolver could not be loaded
2025-02-05 23:11:22.035  INFO 72056 --- [ntloop-thread-0] tform.http.vertx.VertxPlatformHttpServer : Vert.x HttpServer started on 0.0.0.0:8080
2025-02-05 23:11:22.122  INFO 72056 --- [           main] e.camel.impl.engine.AbstractCamelContext : Routes startup (total:2)
2025-02-05 23:11:22.123  INFO 72056 --- [           main] e.camel.impl.engine.AbstractCamelContext :     Started health-check (platform-http:///health)
2025-02-05 23:11:22.123  INFO 72056 --- [           main] e.camel.impl.engine.AbstractCamelContext :     Started sportradar-proxy (platform-http:///nfl/)
2025-02-05 23:11:22.123  INFO 72056 --- [           main] e.camel.impl.engine.AbstractCamelContext : Apache Camel 4.9.0 (sport-radar-proxy) started in 225ms (build:0ms init:0ms start:225ms boot:5s677ms)
2025-02-05 23:11:22.124  INFO 72056 --- [           main] ponent.platform.http.main.MainHttpServer : HTTP endpoints summary
2025-02-05 23:11:22.124  INFO 72056 --- [           main] ponent.platform.http.main.MainHttpServer :     http://0.0.0.0:8080/health             
2025-02-05 23:11:22.124  INFO 72056 --- [           main] ponent.platform.http.main.MainHttpServer :     http://0.0.0.0:8080/nfl/  
```

As soon as this happens, the local API is accessible underneath: http://localhost:8080/nfl/... and forwards all requests to the remote Sportsradar API

## Contributing

This project was generated using [Camel Jbang](https://camel.apache.org/manual/camel-jbang.html). Please, refer the the online documentation for learning more about how to configure the export of a Camel application.

### Prepare Environment

Install development dependencies with the corresponding script for your OS (`setup-4-dev-on-<os>.sh`), for example:

```bash
sh setup-4-dev-on-mac.sh
```

Optional: If you want to test the native image build locally, install GraalVM (e. g. with SDK man) as well:

```bash
sdk install java 23.0.2-graal
```

### Extending Camel routes

Camel routes are defined as YAML in the file `src/main/resources/camel/routing.camel.yaml`
Components that can be used for integration can be looked up at the [ Camel documentation website](https://camel.apache.org/components/4.8.x/index.html)

### Testing adjustments

Run the following command from a terminal window you can quickly run an test your adjusted camel routes:

```bash
camel run camel-jbang.properties ./**/*.camel.yaml
```

### Building the application artifact

```bash
./mvnw clean package
```

The application could now immediately run:

```bash
java -jar target/quarkus-app/quarkus-run.jar
```

## Creating a Docker container

Build the image with:

```bash
docker build -f Dockerfile -t sport-radar-proxy:latest .
```

Then run the container using:

```bash
docker run -it --rm -p 8080:8080 sport-radar-proxy:latest
```

### Creating a Native Docker container

Build the image with:

```bash
docker build -f Dockerfile.native -t sport-radar-proxy:native-latest .
```

Then run the container using:

```bash
docker run -it --rm -p 8080:8080 sport-radar-proxy:native-latest
```