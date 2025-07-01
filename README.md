
# 🚀 Deploying a React (Vite) App to AWS EC2

## A Step-by-Step Guide

### 📘 Introduction
This guide provides a comprehensive, step-by-step walkthrough of the process for deploying a modern React application (built with Vite) to a live AWS EC2 server. We will cover everything from creating the app locally to making it accessible to the world.

---

## ✅ Prerequisites
Before you begin, ensure you have the following ready:

- An active AWS Account.
- Node.js and npm installed on your local machine.
- Git and a GitHub account.
- A code editor like Visual Studio Code.

---

## 🧱 Step 1: Create a Local React Application

1. Open your terminal and navigate to your project directory:
   ```bash
   cd Desktop
````

2. Create a new React project using Vite:

   ```bash
   npm create vite@latest
   ```

   * Project name: `react-project`
   * Framework: `React`
   * Variant: `JavaScript`

3. Navigate into your new project and install dependencies:

   ```bash
   cd react-project
   npm install
   ```

---

## ✏️ Step 2: Customize and Test the App Locally

1. Open your project in VS Code:

   ```bash
   code .
   ```

2. Modify `src/App.jsx`:

   ```jsx
   import './App.css'

   function App() {
     return (
       <>
         <h1>hello world</h1>
         <h2>my first react app on AWS EC2</h2>
         <h3>deployed by Anjali Singh</h3>
       </>
     )
   }

   export default App
   ```

3. Update `vite.config.js` to expose the dev server:

   ```javascript
   import { defineConfig } from 'vite'
   import react from '@vitejs/plugin-react'

   export default defineConfig({
     plugins: [react()],
     server: {
       port: 3000,
       host: true // Exposes the server to the network
     }
   })
   ```

4. Run the app locally:

   ```bash
   npm run dev
   ```

   ✅ Your app should be live at `http://localhost:3000`.

---

## 📤 Step 3: Push Your Project to GitHub

1. Create a new empty repository on GitHub.

2. Initialize Git and push your project:

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <YOUR_GITHUB_REPO_URL>
   git push -u origin main
   ```

---

## ☁️ Step 4: Launch and Connect to an AWS EC2 Instance

1. In AWS Console, go to EC2 → Launch Instance:

   * AMI: **Amazon Linux 2023**
   * Instance Type: `t2.micro` (Free Tier eligible)
   * Create & download a `.pem` key pair

2. Once the instance is running, click **Connect** and copy the SSH command.

3. In terminal (where your `.pem` is stored), run:

   ```bash
   ssh -i "your-key.pem" ec2-user@<your-ec2-public-ip>
   ```

---

## ⚙️ Step 5: Prepare the Server Environment

1. Switch to root:

   ```bash
   sudo su
   ```

2. Install Git and Node.js:

   ```bash
   yum install git -y
   yum install nodejs -y
   ```

3. (Optional but recommended) Use NVM for Node.js:

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   source ~/.bashrc
   nvm install 20
   node -v
   ```

---

## 📦 Step 6: Deploy and Run the Application

1. Clone your GitHub repo:

   ```bash
   git clone <YOUR_GITHUB_REPO_URL>
   ```

2. Navigate and install dependencies:

   ```bash
   cd <your-repo-name>
   npm install
   ```

3. Run the app:

   ```bash
   npm run dev
   ```

   🚀 The server will run on port 3000.

---

## 🔐 Step 7: Configure AWS Security Group (Crucial!)

1. In EC2 Console → Your instance → **Security → Security Group**

2. Click **Edit inbound rules** → **Add Rule**:

   * **Type**: Custom TCP
   * **Port Range**: 3000
   * **Source**: Anywhere (0.0.0.0/0)

3. Click **Save Rules**

> ⚠️ **Security Note**: 0.0.0.0/0 is open to the internet. Restrict for production use.

---

## 🌐 Step 8: Access Your Deployed App

Open a browser and go to:

```
http://<Your-EC2-Public-IP-Address>:3000
```

---

## 🎉 Congratulations!

You have successfully deployed your React (Vite) app on AWS EC2 using only terminal and GitHub.

