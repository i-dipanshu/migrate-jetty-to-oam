# Project Title: Migrating Jetty Server to Open Application Model (OAM)

## Overview:

The goal of this project is to migrate a Jetty server to Open Application Model (OAM) so that it can be deployed on the Napptive platform. Napptive is a cloud-native application platform that provides an integrated solution for deploying applications in modern infrastructures. The migration to OAM will enable the Jetty server to be deployed and managed more efficiently on the Napptive platform. OAM provides a modular and consistent API for modeling application deployments, which can simplify and standardize the deployment process for Jetty.

## What is Jetty ?
Jetty is a Java-based web server and servlet container that can run on a variety of technology stacks. 

## Project Scope:

The project scope includes the following tasks:

- Analyze the existing Jetty server and its deployment architecture.

- Identify the components of the Jetty server that need to be migrated to OAM.

- Design the OAM-based deployment architecture for the Jetty server, including defining the server's components, dependencies, and resource requirements.

- Develop and test the OAM-based deployment configuration for the Jetty server.

- Migrate the Jetty server from its current deployment architecture to the OAM-based architecture.

- Validate the functionality and performance of the migrated Jetty server on the Napptive platform.

## Deliverables:

The following deliverables are expected at the end of the project:

- The OAM-based deployment configuration for the Jetty server, including all necessary manifests and configuration files.

- A working version of the migrated Jetty server running on the Napptive platform.

## Migrating Jetty to Open Application Model (OAM) can have several potential impacts:

- Improved deployment efficiency: OAM provides a higher-level yet consistent API for modeling application deployments, which can simplify and standardize the deployment process for Jetty. This can lead to faster and more efficient deployment of Jetty servers on the Napptive platform.

- Better scalability and portability: OAM provides a modular and extensible design for modeling application deployments, which can make it easier to scale and move Jetty servers across different environments, such as Kubernetes, cloud, or even IoT devices. This can enable Jetty to be more easily deployed and managed in a variety of scenarios.

- Increased developer productivity: OAM's modular and consistent API can simplify the development and deployment process for Jetty, making it easier for developers to focus on application development rather than deployment details. This can improve developer productivity and reduce the time and effort required to deploy and manage Jetty servers.

- Better integration with Napptive platform: Migrating Jetty to OAM can enable it to integrate more seamlessly with the Napptive platform, which can provide additional benefits such as easier management and monitoring of Jetty servers.

In summary, migrating Jetty to Open Application Model can improve deployment efficiency, scalability, developer productivity, and platform integration, which can lead to significant benefits for the organization.

## The jetty.app.yaml
```yaml
apiVersion: core.oam.dev/v1beta1
kind: Application
metadata:
  name: jetty
  annotations:
    version: "9.4.51-jre8-alpine"
    description: "Jetty Web Server"
spec:
  components:
    - name: jetty
      type: webservice
      properties:
        image: jetty:9.4.51-jre8-alpine
        ports:
          - port: 8080
            expose: true
        env:
          - name: JETTY_HOME
            value: "/usr/local/jetty"
          - name: JETTY_BASE
            value: "/var/lib/jetty"
          - name: TMPDIR
            value: "/tmp/jetty"
      traits:
        - type: napptive-ingress
          properties:
            name: jetty
            port: 8080
            path: /
```