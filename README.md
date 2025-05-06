## 🐳 Step-by-Step: Set Up Docker with Node.js in VS Code

### 📝 Prerequisites:

1. **Docker installed**
- Download Docker Desktop: https://www.docker.com/products/docker-desktop/
2. **VS Code** installed with the **Docker extension** (optional but recommended for convenience):

   * Install the **Docker extension** from the VS Code Extensions Marketplace.

---

### 🔹 1. Create a Node.js Project in VS Code

1. **Open VS Code** and create a new folder for your project (e.g., `node-docker-app`).

2. Open the terminal (`Ctrl + backtick`) in VS Code and navigate to the project folder.

3. **Initialize a new Node.js app**:

   ```bash
   npm init -y
   ```

4. Install the required dependencies. For example, let's install `express`:

   ```bash
   npm install express
   ```

---

### 🔹 2. Create a Simple Node.js App

Create a file called **`app.js`** in your project folder and add the following code:

```js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello, Dockerized Node.js!');
});

app.listen(port, () => {
  console.log(`App listening at http://localhost:${port}`);
});
```

---

### 🔹 3. Create a `Dockerfile`

In the same folder, create a file called **`Dockerfile`** (no file extension) and add the following code:

```Dockerfile
# Use the official Node.js image as the base image
FROM node:16

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json to the container
COPY package*.json ./

# Install the app dependencies
RUN npm install

# Copy the rest of the app's code into the container
COPY . .

# Expose the app's port
EXPOSE 3000

# Command to run the app inside the container
CMD ["node", "app.js"]
```

---

### 🔹 4. Create a `.dockerignore` File

Create a `.dockerignore` file to avoid unnecessary files being copied into the container, similar to `.gitignore`. Example content for `.dockerignore`:

```text
node_modules
npm-debug.log
```

---

### 🔹 5. Build the Docker Image

Now, in the **VS Code terminal**, build your Docker image using the following command:

```bash
docker build -t node-docker-app .
```

This will create a Docker image with the tag `node-docker-app`.

---

### 🔹 6. Run the Docker Container

Once the image is built, run the container using:

```bash
docker run -p 3000:3000 -d node-docker-app
```

Explanation:

* `-p 3000:3000`: Maps port 3000 on your machine to port 3000 in the container (since the app is listening on port 3000).
* `-d`: Runs the container in detached mode (in the background).

You should see the container running. To check if it's running:

```bash
docker ps
```

---

### 🔹 7. Access Your Node.js App

* Open your browser and go to `http://localhost:3000`.
* You should see **"Hello, Dockerized Node.js!"**.

---

### 🔹 8. (Optional) Using VS Code's Docker Extension

If you installed the Docker extension for VS Code, you can:

* **View images** and **containers** directly in VS Code.
* **Build, run, and manage** Docker containers easily from the Docker panel in VS Code.

---

### ✅ Done!

Your **Node.js app** is now running in a **Docker container** using VS Code.
