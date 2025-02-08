# **SportsRadar API Proxy** 🏈🏀⚽  

A lightweight proxy for the **[SportsRadar API](https://developer.sportradar.com/getting-started/docs/coverage-information)**, simplifying integration and resolving CORS issues.  

## **Features**  
✅ **Automatic API Key Handling** – Appends API key to all forwarded requests  
✅ **Transparent Responses** – Returns exact results from the SportsRadar API  
✅ **CORS-Friendly** – Enables access from any domain, avoiding browser CORS issues  

Effortless SportsRadar API access, with no headaches! 🚀  

## **Prerequisites**  

Install runtime dependencies using the corresponding script for your OS:  

```bash
sh install-on-mac.sh
```

## **Usage**  

1️⃣ **Set up your API Key:**  

```bash
cp .sample.env .env
# Edit .env to set your API key
```

2️⃣ **Start the proxy using Docker Compose:**  

```bash
docker-compose up -d
```

After startup, access the API locally:  
🔗 **http://localhost:8080/nfl/...** (forwards requests to the SportsRadar API)  

3️⃣ **Check logs, if necessary:**  

```bash
docker-compose logs -f
```

4️⃣ **Stop the service:**

```bash
docker-compose down
```

## **Development & Contribution**  

This project is developed using [Camel JBang](https://camel.apache.org/manual/camel-jbang.html) and [GraalVM](https://www.graalvm.org/). These dependencies should be installed on your local machine to aid further development of the project.

### **Set Up Development Environment**

Install dependencies (JBand & Apache Camel) for development:

```bash
sh setup-4-dev-on-mac.sh
```

For **native image testing**, additionally install GraalVM:

```bash
sdk install java 23.0.2-graal
```

### **Modifying Camel Routes**

Routes are defined in: 📂 `src/main/resources/camel/routing.camel.yaml`  

🔍 **Find available components:** [Camel Components Documentation](https://camel.apache.org/components/4.8.x/index.html)  

### **Testing Adjustments**

Quickly test changes to routes with:  

```bash
camel run camel-jbang.properties ./**/*.camel.yaml
```

You can use and extend the prepared HTML sample file underneath `src/test/resources/sample.html` to check whether your adjustments worked correctly.

### **Build & Run the Application**

Compile the application:

```bash
./mvnw clean package
```

Run the packaged JAR:

```bash
java -jar target/quarkus-app/quarkus-run.jar
```

## **Docker Support**  

### **Create and Run a Docker Container**  

Build the Docker image:  

```bash
docker build -f Dockerfile -t sport-radar-proxy:latest .
```

If you want to build and immediately run the new container version, you can do so by using the prepared `docker-compose.local-jvm.yaml`:

```bash
docker-compose up -d -f docker-compose.local-jvm.yaml
```

### **Build & Run a Native Docker Container**  

For a **smaller, faster** native container run the following:  

```bash
docker build -f Dockerfile.native -t sport-radar-proxy:native-latest .
```

If you want to build and immediately run the new native container version, you can do so by using the prepared `docker-compose.local-native.yaml`:

```bash
docker-compose up -d -f docker-compose.local-native.yaml
```

## **License**  

This project is licensed under the [Apache License 2.0](LICENSE).  