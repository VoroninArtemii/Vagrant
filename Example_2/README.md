This project uses Vagrant to automate the creation and setup of a Docker-based infrastructure with multiple virtual machines. It configures a **Docker Swarm** cluster, which consists of one manager node and two worker nodes. The main components of the project are as follows:

1. **Vagrant Configuration**:
   - It defines three virtual machines: one manager node (`manager1`) and two worker nodes (`worker1`, `worker2`).
   - The manager node is configured to initialize a Docker Swarm and create a join token for the worker nodes to join the swarm.
   - Each VM has a private network and forwarded ports for communication.
   - Docker and Docker Swarm are installed on all nodes via provisioning scripts (`install_docker.sh`), and Docker Swarm is initialized on the manager and joined by the workers.

2. **Docker Services**:
   - **Portainer**: A web-based Docker management tool is deployed using the `portainer/portainer-ce` image. It runs on the manager node and is accessible via port 1102.
   - **Portainer Agent**: Deployed on all nodes to interact with Docker.
   - **Web Service**: A simple Nginx-based web service (`nginxdemos/nginx-hello`) is deployed globally across all nodes.
   - **Nginx Reverse Proxy**: On the manager node, an Nginx reverse proxy is set up to forward traffic from port 1103 to the backend web service.

3. **Networking**:
   - The project uses Docker's **overlay networks** (`agent_network` and `web_network`) to allow communication across the Swarm nodes.
   - The manager node has an Nginx configuration that acts as a reverse proxy for the web service.

4. **Nginx Configuration**:
   - The Nginx configuration sets up a reverse proxy to forward HTTP requests to the `web` service running in the Docker Swarm.
