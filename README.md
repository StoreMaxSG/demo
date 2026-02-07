# StoreMax

A modern warehouse management system designed to optimize storage, streamline operations, and enhance overall warehouse efficiency. StoreMax provides a comprehensive solution for managing warehouse operations with a focus on simplicity and functionality.

## Project Overview

StoreMax offers a seamless experience for warehouse management, including:

- Optimized storage allocation
- Efficient cargo handling
- Real-time monitoring of warehouse operations
- Streamlined workflow management
- User-friendly interface for warehouse personnel

## Features

### Warehouse Optimization

- Intelligent storage allocation algorithms
- Space utilization analysis
- Cargo categorization and organization

### Real-time Monitoring

- Live tracking of warehouse operations
- Agent status monitoring
- Performance metrics and insights

### User Interface

- Responsive design for various devices
- Intuitive dashboard for warehouse management
- Real-time updates and notifications

### Integration Capabilities

- Modular architecture for easy integration
- Standardized communication protocols
- Extensible plugin system

## Technologies Used

### Frontend

- Framework: React
- Language: JavaScript/TypeScript
- Build Tool: Vite
- Styling: Tailwind CSS
- Hosting: Cloudflare Pages

### Backend

- Language: Python
- Architecture: Agent-based system
- Platform: AgentField
- Serverless Platform: Cloudflare Workers, Cloudflare Containers, KV, Durable Objects, R2
- Service Bindings: Cloudflare Pages to Workers integration
- Container Runtime: Cloudflare Containers for Python agents

### Development Tools

- Version Control: Git
- Package Management: npm, pip
- Deployment: Vite, Cloudflare Workers

## Project Structure

```
opensource/
├── README.md          # Main documentation
├── LICENSE            # MIT License
└── docs/              # Additional documentation
    ├── architecture-overview.md   # System architecture
    ├── cloudflare-workers.md      # Cloudflare Workers implementation
    ├── agentfield-implementation.md # AgentField implementation guide
    └── getting-started.md         # Getting started guide
```

## System Architecture

StoreMax employs a modular, agent-based architecture designed for scalability and flexibility. The system consists of multiple components working together to provide a comprehensive warehouse management solution.

### Key Components

- **Frontend Application**: User interface for warehouse operations and monitoring
- **Agent System**: Modular agents handling specific warehouse functions
- **Integration Layer**: Connects various system components
- **Monitoring System**: Tracks performance and provides insights

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- Python (v3.10 or higher)
- npm or yarn
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd StoreMax
   ```

2. **Install frontend dependencies**
   ```bash
   cd frontend
   npm install
   ```

3. **Install backend dependencies**
   ```bash
   cd ../agents
   pip install -r requirements.txt
   ```

### Running the Application

1. **Start the frontend development server**
   ```bash
   cd frontend
   npm run dev
   ```

2. **Start the backend agents**
   ```bash
   # In separate terminals
   python agents/optimizer/main.py
   python agents/sync_agent/main.py
   python agents/warehouse_manager/main.py
   ```

3. **Access the application**
   Open your browser and navigate to `http://localhost:5173`

## License

StoreMax is open source software licensed under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- Built with modern web technologies and best practices
- Inspired by the need for efficient warehouse management solutions
- Developed as part of the AgentField Hackathon
