# Argo CD Architecture

Hello everyone. In this section, we will take a deep dive into the Argo CD architecture.

Without further delay, let us get started at its core.

Argo CD operates as a Kubernetes controller designed to enforce the principle of GitOps. It continuously monitors the state of applications running in the cluster and compares it with the desired state defined in a Git repository.

When disparities arise, the application is marked as out of sync, signaling that the live state no longer aligns with the intended configuration. Argo CD provides detailed insights into these differences and offers both manual and automated capabilities to synchronize the state by continuously reconciling the live state with the desired state.

Argo CD ensures that any changes made in the Git repository are propagated to the cluster. This guarantees consistency across environments and eliminates the risk associated with manual updates.

Argo CD is designed with a component-based architecture to separate responsibilities into distinct deployable units.

Now let us explore these logical layers.

## Four Logical Layers

Argo CD architecture is organized into four logical layers that define responsibilities and manage dependencies.

Let us go through each one.

### 1. UI Layer

The UI layer provides the user interface for interacting with Argo CD, including both graphical and command-line options.

#### Components

- Web App: The web app provides a graphical user interface for managing applications, monitoring health, viewing logs, and triggering synchronization.
- CLI: The command-line interface allows users to interact with Argo CD programmatically. It offers similar functionality to the web app, including application deployment, synchronization, and monitoring, but is better suited for automation and scripting.

### 2. Application Layer

The application layer supports the UI layer and handles requests between users and the backend components.

This layer is responsible for translating user actions into application operations and coordinating communication with the rest of the system.

### 3. Repository and Sync Layer

This layer is where Argo CD reads the desired state from Git and compares it with the live state in the cluster. It is the core of the GitOps workflow.

When a repository change is detected, Argo CD evaluates the difference and determines whether the cluster needs to be synchronized.

### 4. Cluster/Runtime Layer

The cluster layer represents the target environment where the application is deployed and running.

Argo CD monitors the actual state of resources in the cluster and compares them against the desired configuration. If there is drift, the application is marked as out of sync and can be reconciled.

## Summary

Argo CD follows a clean separation of concerns:

- UI layer for user interaction
- Application layer for request handling
- Repository layer for desired state definition
- Cluster layer for live state monitoring and reconciliation

This architecture enables Argo CD to continuously maintain the cluster in the desired state, ensuring consistency, visibility, and easier automation.
