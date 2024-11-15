# Node.js Setup Guide

This guide will walk you through the process of setting up Node.js on your machine.

## Prerequisites
Basic familiarity with command-line operations.
Administrator permissions on your machine.

<br>

---

<br>

### 1. Download and Install Node.js
Visit the Node.js website:
Go to https://nodejs.org and download the latest stable version (LTS) of Node.js for your operating system.

Install Node.js:
- Linux: You can use a package manager.
  
#### For Ubuntu/Debian:
```javascript
sudo apt update
sudo apt install nodejs npm
```

#### Verify the Installation:
After installing, verify by running the following commands in your terminal:

```javascript
node -v
npm -v
```
This should display the installed versions of Node.js and npm.

<br>

---

<br>

### 2. Update npm (Optional)
After installing, it’s recommended to update npm to the latest version:

```javascript
npm install -g npm@latest
```

<br>

---

<br>

### 3. Install a Code Editor 
While Node.js can be used from any text editor, using a dedicated code editor can be helpful:

- download Visual Studio Code (recommended)

<br>

---

<br>

### 4. Create Your First Node.js App
To verify everything works, create a simple "Hello World" app:

Create a new directory for your project in the terminal (ctrl+shift+T):
```javascript
mkdir my-node-app
cd my-node-app
```

Initialize npm to create a package.json file:

```javascript
npm init -y
```

Create an index.js file with the following content:

```javascript
console.log("Hello, Node.js!");
```

Run the app in the terminal with the following command:

```javascript
node index.js
```

You should see Hello, Node.js! in the console.

<br>

---

<br>

### 5. Nodemon & Script

Nodemon is a tool that helps automatically restart your Node.js server whenever changes are detected in your code. This is very useful during development.

#### Install Nodemon

To install Nodemon , use the following command in the Terminal:

```bash
npm install -g nodemon
```

#### Update package.json with a Nodemon Script

After installing Nodemon, you can add a script in your package.json file to run your app with Nodemon:

1. Open package.json.
2. Under the "scripts" section, add a new script:

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js"
}
```

- start: Runs your app normally using Node.js.
- dev: Runs your app with Nodemon for automatic restarts on changes.

Now run the app with Nodemon
To run your app with Nodemon, use the following command:

```bash
npm run dev
```

Now, Nodemon will automatically restart your app whenever changes are made to your files. So everytime you save your file (Shortkut: ctrl + S) your app will restart automatically.

<br>

---

<br>

### 6. Additional Resources
Node.js Documentation: https://nodejs.org/docs/latest/api/
npm Documentation: https://docs.npmjs.com/

# Happy coding!
