# Kubernetes MongoDB and Mongo Express Deployment

This project demonstrates the deployment of a MongoDB database along with a Mongo Express web interface within a Kubernetes cluster. The setup includes creating necessary services, ConfigMaps, and Secrets to ensure secure and seamless communication between components.

## Steps Performed

### 1. Created a MongoDB Pod

- **Objective:** Deploy a MongoDB instance in a Kubernetes pod.
- **Service Creation:** An internal service was created to allow communication with the MongoDB pod. This service restricts access to internal cluster components only, ensuring no external requests are allowed.

### 2. Created a Mongo Express Deployment

- **Objective:** Set up Mongo Express for managing the MongoDB instance via a web interface.
- **Configuration:**
  - **Database URL:** Required for Mongo Express to connect to the MongoDB instance.
  - **Credentials:** Required for authentication (username and password).
- **Implementation:**
  - **ConfigMap:** Created to store the MongoDB URL.
  - **Secret:** Created to store the MongoDB credentials (username and password).
  - **Deployment YAML:** Referenced the ConfigMap and Secret in the Mongo Express deployment file using environment variables.

### 3. Exposed Mongo Express Externally

- **Objective:** Make Mongo Express accessible through a web browser.
- **Service Creation:** An external service was created to allow external requests to communicate with the Mongo Express pod.
  - **URL Format:** The external service can be accessed via `http://<Node-IP>:<External-Service-Port>`.

### 4. Configured Request Flow

- **Request Handling:**
  1. **Browser Request:** Initiated from a browser to the Mongo Express external service.
  2. **Forwarding:** The external service forwards the request to the Mongo Express pod.
  3. **Internal Connection:** The Mongo Express pod connects to the internal service of the MongoDB instance.
  4. **Authentication:** The MongoDB pod authenticates the request using the provided credentials.
