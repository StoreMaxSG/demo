# Getting Started Guide

This guide provides step-by-step instructions on how to set up and run the StoreMax system for warehouse management.

## Prerequisites

Before you begin, ensure you have the following software installed on your system:

### Required Software

- **Node.js** (v16 or higher)
  - Download and install from [nodejs.org](https://nodejs.org/)
  - Includes npm (Node Package Manager)

- **Python** (v3.10 or higher)
  - Download and install from [python.org](https://www.python.org/)
  - Includes pip (Python Package Installer)

- **Docker** (v20.10 or higher)
  - Download and install from [docker.com](https://www.docker.com/)
  - Required for building and deploying agent containers

- **Git**
  - Download and install from [git-scm.com](https://git-scm.com/)
  - For version control

- **Wrangler CLI** (latest)
  - Install using: `npm install -g wrangler`
  - Required for deploying to Cloudflare Workers and Containers

### Optional Software

- **Visual Studio Code** (or any preferred code editor)
  - Download from [code.visualstudio.com](https://code.visualstudio.com/)
  - Recommended extensions:
    - ESLint
    - Prettier
    - Python
    - Tailwind CSS IntelliSense

## Installation

### 1. Clone the Repository

```bash
# Clone the repository
git clone <repository-url>

# Navigate to the project directory
cd StoreMax
```

### 2. Install Frontend Dependencies

```bash
# Navigate to the frontend directory
cd frontend

# Install dependencies
npm install
```

### 3. Install Backend Dependencies

```bash
# Navigate to the agents directory
cd ../agents

# Install dependencies
pip install -r requirements.txt
```

## Configuration

### Frontend Configuration

The frontend application uses environment variables for configuration. Create a `.env` file in the `frontend` directory with the following variables:

```env
# Frontend configuration
VITE_API_ENDPOINT=http://localhost:8787
VITE_APP_TITLE=StoreMax
VITE_APP_VERSION=1.0.0
```

### Backend Configuration

The agent system uses configuration files for setting up various parameters. These files are typically located in each agent's directory.

Create a `.env` file in the agents directory with the following variables:

```env
# AgentField configuration
AGENTFIELD_URL=http://localhost:8080

# AI Model configuration
AI_MODEL=openai/gpt-4o-mini

# Cloudflare configuration
CLOUDFLARE_ACCOUNT_ID=your-account-id
CLOUDFLARE_API_TOKEN=your-api-token
```

### Cloudflare Configuration

To deploy to Cloudflare Workers and Containers, you need to configure `wrangler.toml`:

```toml
name = "storemax-api"
main = "worker.js"
compatibility_date = "2024-01-01"

[env.production]
vars = { ENVIRONMENT = "production" }

containers = [
  { binding = "OPTIMIZER_CONTAINER", image = "registry.example.com/storemax/optimizer:latest" },
  { binding = "SYNC_CONTAINER", image = "registry.example.com/storemax/sync:latest" },
  { binding = "WAREHOUSE_MANAGER_CONTAINER", image = "registry.example.com/storemax/warehouse-manager:latest" }
]

kv_namespaces = [
  { binding = "CACHE", id = "xxxxxxxxxxxxxxxx" }
]

durable_objects = { bindings = [
  { name = "WAREHOUSE_STATE", class_name = "WarehouseState" }
]}

r2_buckets = [
  { binding = "STORAGE", bucket_name = "storemax-data" }
]
```

## Building and Deploying Containers

### 1. Build Agent Containers

Build Docker images for each agent:

```bash
# Build optimizer container
cd agents/optimizer
docker build -t storemax/optimizer:latest .

# Build sync container
cd ../sync_agent
docker build -t storemax/sync:latest .

# Build warehouse manager container
cd ../warehouse_manager
docker build -t storemax/warehouse-manager:latest .
```

### 2. Push to Container Registry

Tag and push images to your container registry:

```bash
# Tag images
docker tag storemax/optimizer:latest registry.example.com/storemax/optimizer:latest
docker tag storemax/sync:latest registry.example.com/storemax/sync:latest
docker tag storemax/warehouse-manager:latest registry.example.com/storemax/warehouse-manager:latest

# Push images
docker push registry.example.com/storemax/optimizer:latest
docker push registry.example.com/storemax/sync:latest
docker push registry.example.com/storemax/warehouse-manager:latest
```

### 3. Deploy to Cloudflare

Deploy Workers and Containers using Wrangler:

```bash
# Login to Cloudflare
wrangler login

# Deploy to production
wrangler deploy --env production

# Deploy to development
wrangler deploy --env development
```

## Running the Application

### 1. Start the Frontend Development Server

```bash
# In the frontend directory
npm run dev
```

This will start the development server at `http://localhost:5173` by default.

### 2. Start the Backend Agents

Open separate terminal windows for each agent and run the following commands:

#### Optimizer Agent

```bash
# In the StoreMax directory
PYTHONPATH=. python agents/optimizer/main.py
```

#### Sync Agent

```bash
# In the StoreMax directory
PYTHONPATH=. python agents/sync_agent/main.py
```

#### Warehouse Manager Agent

```bash
# In the StoreMax directory
PYTHONPATH=. python agents/warehouse_manager/main.py
```

### 3. Access the Application

Open your web browser and navigate to `http://localhost:5173` to access the StoreMax application.

## Basic Usage

### Dashboard Overview

Upon accessing the application, you will be presented with the main dashboard, which provides an overview of warehouse operations, including:

- Agent status
- Performance metrics
- Recent activities
- Warehouse statistics

### Managing Warehouse Operations

1. **Monitor Agent Status**: View the current status of all agents in real-time
2. **Track Performance**: Monitor key performance indicators for warehouse operations
3. **View Statistics**: Access detailed statistics about warehouse usage and efficiency
4. **Manage Tasks**: Create and track warehouse tasks through the interface

### Navigation

Use the sidebar menu to navigate between different sections of the application:

- **Dashboard**: Main overview
- **Monitoring**: Real-time monitoring of warehouse operations
- **Analytics**: Performance metrics and insights
- **Settings**: Application configuration

## Troubleshooting

### Common Issues

#### Frontend Issues

- **Development Server Not Starting**
  - Check that Node.js and npm are installed correctly
  - Ensure all dependencies are installed with `npm install`
  - Verify that the port (default: 5173) is not in use by another application

- **API Connection Errors**
  - Ensure all backend agents are running
  - Verify the API endpoint configuration in the `.env` file
  - Check network connectivity between frontend and backend

#### Backend Issues

- **Agent Not Starting**
  - Check that Python is installed correctly
  - Ensure all dependencies are installed with `pip install -r requirements.txt`
  - Verify that the required ports are not in use

- **Import Errors**
  - Ensure the PYTHONPATH is set correctly
  - Check that all required packages are installed
  - Verify that the directory structure is correct

### Debugging

#### Frontend Debugging

- Use the browser's developer tools (F12) to inspect elements and console logs
- Check the terminal running the development server for error messages
- Use `console.log()` statements for debugging

#### Backend Debugging

- Check the terminal output for error messages
- Use `print()` statements for debugging
- Consider using a Python debugger for more complex issues

## Support

If you encounter any issues that are not covered in this guide, please refer to the following resources:

- **Documentation**: Additional documentation can be found in the `docs` directory
- **Community**: Join our community forums for support and discussion
- **GitHub Issues**: Report bugs and feature requests on GitHub

## Next Steps

Once you have the system up and running, you may want to:

1. **Explore the Dashboard**: Familiarize yourself with the main dashboard and its features
2. **Test Agent Functionality**: Verify that all agents are working correctly
3. **Configure Settings**: Adjust application settings to match your warehouse requirements
4. **Learn Advanced Features**: Explore the advanced features of the system

## Conclusion

This getting started guide provides the basic steps to set up and run the StoreMax system. For more detailed information about specific features and functionality, please refer to the other documentation files in the `docs` directory.

We hope you find StoreMax to be a valuable tool for optimizing your warehouse operations!
