Deploying a React (Vite) App to AWS EC2
A Step-by-Step Guide
Introduction
This guide provides a comprehensive, step-by-step walkthrough of the process for deploying a modern React application (built with Vite) to a live AWS EC2 server. We will cover everything from creating the app locally to making it accessible to the world.
Prerequisites
Before you begin, ensure you have the following ready:
An active AWS Account.
Node.js and npm installed on your local machine.
Git and a GitHub account.
A code editor like Visual Studio Code.
Step 1: Create a Local React Application
First, we'll set up a simple React project on our local computer.
Open your terminal and navigate to your project directory.
Generated bash
cd Desktop
Use code with caution.
Bash
Create a new React project using Vite. Follow the on-screen prompts.
Generated bash
npm create vite@latest
Use code with caution.
Bash
Project name: react-project
Framework: React
Variant: JavaScript
Navigate into the new project folder and install the dependencies.
Generated bash
cd react-project
npm install
Use code with caution.
Bash
Step 2: Customize and Test the App Locally
Let's modify the default app and ensure it runs correctly.
Open the project in your code editor (code .).
Modify src/App.jsx with your own simple code.
Generated jsx
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
Use code with caution.
Jsx
Modify vite.config.js to allow network access, which is crucial for EC2.
Generated javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    host: true // Exposes the server to the network
  }
})
Use code with caution.
JavaScript
Run the app locally to test it.
Generated bash
npm run dev
Use code with caution.
Bash
✅ Your app should be live at http://localhost:3000.
Step 3: Push Your Project to GitHub
To get our code onto the server, we need to put it in a central repository.
Create a new, empty repository on GitHub.
In your local terminal, initialize Git and push your code.
Generated bash
git init
git add .
git commit -m "Initial commit"
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
Use code with caution.
Bash
Step 4: Launch and Connect to an AWS EC2 Instance
Now, let's set up our server in the cloud.
In the AWS Console, navigate to the EC2 service and launch a new instance.
AMI: Amazon Linux 2023
Instance Type: t2.micro (Free Tier eligible)
Create and download a new key pair (.pem file). Keep it safe!
Once the instance is running, select it, click "Connect", and copy the SSH command.
In a new local terminal, navigate to where you saved the .pem file and paste the command to connect.
Generated bash
# Example command
ssh -i "your-key.pem" ec2-user@<your-ec2-public-ip>
Use code with caution.
Bash
Step 5: Prepare the Server Environment
Once connected to your EC2 instance, install the necessary tools.
Switch to the root user.
Generated bash
sudo su
Use code with caution.
Bash
Install Git and Node.js.
Generated bash
yum install git -y
yum install nodejs -y
Use code with caution.
Bash
(Recommended) Install and use NVM (Node Version Manager) for better control.
Generated bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
node -v
Use code with caution.
Bash
✅ You should now be running a modern version of Node.js.
Step 6: Deploy and Run the Application
Let's pull our code from GitHub and run it on the server.
Clone your GitHub repository.
Generated bash
git clone <YOUR_GITHUB_REPO_URL>
Use code with caution.
Bash
Navigate into your project directory and install the dependencies.
Generated bash
cd <your-repo-name>
npm install
Use code with caution.
Bash
Run the application!
Generated bash
npm run dev
Use code with caution.
Bash
🚀 The terminal will show the app is running on port 3000.
Step 7: Configure AWS Security Group (Crucial Final Step!)
By default, the EC2 firewall blocks incoming traffic. We must open the port.
In the EC2 Console, go to your instance's "Security" tab and click on its Security Group.
Click "Edit inbound rules".
Click "Add rule" and configure it as follows:
Type: Custom TCP
Port Range: 3000
Source: Anywhere-IPv4 (0.0.0.0/0)
Click "Save rules".
⚠️ Security Note: Setting the source to 0.0.0.0/0 allows traffic from any IP address. This is fine for public demos but should be restricted for production applications.
Step 8: Access Your Deployed App!
Open your browser and navigate to your app using your EC2 instance's Public IP address.
URL: http://<Your-EC2-Public-IP-Address>:3000
Congratulations!
You have successfully deployed your React application on an AWS EC2 instance.
