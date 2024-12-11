# Multiplayer Paint
## Advanced Javascript project for the 2024/2025 network programming course in FMI

### Overview
Multiplayer Paint is a multiplayer painting platform developed as part of the Network Programming 2024/2025 course at FMI. It allows users to connect over a network, draw collaboratively, and enjoy creative activities in real time.

---

### Prerequisites
1. **Docker:** Ensure Docker is installed on your system. If not, download and install Docker Desktop from the [official website](https://www.docker.com/products/docker-desktop).
2. A system with a terminal/command prompt to run Docker commands.

---

### How to Set Up and Start the Project on the Main Machine
1. Open your terminal or command prompt.
2. Navigate to the directory where the project is saved:
   ```bash
   cd path/to/project
   ```
3. Build the Docker image:
   ```bash
   docker build -t app .
   ```
4. Run the Docker container:
   ```bash
   docker run -p 3000:3000 app
   ```
5. Open your web browser and navigate to http://localhost:3000 to access Multiplayer-Paint.

---

### How to Connect Another Device for Multiplayer
1. Choose a device you want to connect to the main machine.
2. Ensure the device is connected to the same network as the main machine.
3. Find the main machine's local IP address:
   - Open the terminal on the main machine and run:
     ```bash
     ifconfig # On Linux/Mac
     ipconfig # On Windows
     ```
   - Look for an IP address in the format \`10.108.XX.XX\` or \`192.168.XX.XX\`.

4. On the connecting device, open a web browser and enter the following in the address bar:
   ```
   MAIN_MACHINE_LOCAL_IP_ADDRESS:3000
   ```
   Example:
   ```
   10.108.4.25:3000
   ```