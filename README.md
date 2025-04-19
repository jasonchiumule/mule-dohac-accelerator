# DoHAC Accelerator

This is a MuleSoft application designed to act as a simple API facade or accelerator for backend services, specifically interacting with endpoints hosted at `dohac-apis.fly.dev`.

## Overview

The application exposes several HTTP endpoints that proxy requests to corresponding endpoints on the backend service (`https://dohac-apis.fly.dev`). It primarily handles GET requests for various resources and one POST request for `QuestionnaireResponse`.

For each request proxied to the backend, a static `Authorization: Bearer mock_blahblah` header is added.

## Features

The application exposes the following endpoints on port `8081` (by default):

*   `GET /api/Provider`: Proxies a GET request to `https://dohac-apis.fly.dev/api/Provider`.
*   `GET /api/Questionnaire`: Proxies a GET request to `https://dohac-apis.fly.dev/api/Questionnaire`.
*   `GET /api/RegisteredNurseAttendance`: Proxies a GET request to `https://dohac-apis.fly.dev/api/RegisteredNurseAttendance?service=SVC-54321&summary=false`. (Note: Query parameters are hardcoded).
*   `GET /api/HealthcareService`: Proxies a GET request to `https://dohac-apis.fly.dev/api/HealthcareService?organization=PRV-12345`. (Note: Query parameter is hardcoded).
*   `POST /api/QuestionnaireResponse`: Generates a static JSON payload and POSTs it to `https://dohac-apis.fly.dev/api/QuestionnaireResponse`.

CORS is configured to allow requests from any origin (`<http:public-resource />`).

## Prerequisites

*   [Apache Maven](https://maven.apache.org/download.cgi)
*   [Anypoint Studio](https://www.mulesoft.com/platform/studio) (Recommended for development and local testing) or a compatible Mule Runtime (Version specified in `pom.xml`).
*   JDK compatible with the specified Mule Runtime.

## Building

To build the application package, navigate to the project's root directory (`dohac-accelerator`) and run:

```bash
mvn clean package
```

This will generate a deployable Mule application archive (`.jar`) in the `target/` directory.

## Running

### Locally using Anypoint Studio

1.  Import the project into Anypoint Studio (`File -> Import -> Anypoint Studio -> Anypoint Studio project from File System`).
2.  Right-click on the project in the Package Explorer.
3.  Select `Run As -> Mule Application`.

### Using Mule Standalone Runtime

1.  Build the project using `mvn clean package`.
2.  Copy the generated JAR file from the `target/` directory to the `apps/` directory of your Mule Standalone Runtime installation.
3.  Start the Mule Runtime.

## Configuration

*   **HTTP Listener Port:** Configured in `src/main/mule/dohac-accelerator.xml` within the `HTTP_Listener_config`. Default is `8081`.
*   **Backend Service Host:** Configured in `src/main/mule/dohac-accelerator.xml` within the `req-dohac-apis.fly.dev` config. Default is `dohac-apis.fly.dev` (HTTPS).
*   **Backend Authentication:** A **hardcoded** bearer token (`Bearer mock_blahblah`) is used for all requests to the backend service. This is defined within each `http:request` component's headers. **Note:** For production or secure environments, this should be externalized and managed securely (e.g., using properties, Mule Secure Configuration Properties, or secrets management).
*   **Backend Query Parameters:** Some flows (`api-registerednurse`, `api-healthcareService`) have hardcoded query parameters in the `http:request` path.

## Backend Service Dependency

This application relies on the availability of the backend service at `https://dohac-apis.fly.dev`.
