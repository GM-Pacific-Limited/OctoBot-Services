# OctoBot-Services Documentation

## Overview
OctoBot-Services is a Python package that provides integration between OctoBot's core trading functionalities and various external services, communication channels, and user interfaces. It serves as the bridge between the trading bot and the outside world.

The package enables OctoBot users to:
- Receive notifications about trades, orders, and market conditions
- Interact with the trading system through command-based interfaces (e.g., Telegram)
- Use web interfaces for managing and monitoring the trading system
- Connect to external data sources and platforms
- Configure various services for enhanced functionality

## Core Architecture
The architecture of OctoBot-Services is based on several key abstractions:

### Services System
- `AbstractService`: Base class for all services that defines the interface and common behaviors
- `ServiceFactory`: Creates and manages service instances, ensuring singleton instances
- `AbstractServiceUser`: Base class for components that require services

### Notification System
- `AbstractNotifier`: Base class for sending notifications
- Various notification types for different events (orders, trades, etc.)
- `NotificationChannel`: Channel for distributing notifications to subscribers

### Interface System
- `AbstractInterface`: Base class for all interfaces
- `AbstractBotInterface`: Interface for command-based interaction
- `AbstractWebInterface`: Interface for web-based interaction

### Service Feed System
- `AbstractServiceFeed`: Base class for service feeds receiving data from external sources
- `ServiceFeedFactory`: Creates service feed instances
- `ServiceFeedManager`: Manages service feed lifecycle

## Directory Structure
```
octobot_services/
├── api/                  # API functions for external interaction
├── channel/              # Communication channels
├── interfaces/           # Interface implementations
│   ├── bots/             # Bot interfaces
│   ├── web/              # Web interfaces
│   └── util/             # Interface utilities
├── managers/             # Component managers
├── notifier/             # Notification system
├── notification/         # Notification implementations
├── services/             # Service implementations
├── service_feeds/        # Service feed implementations
└── util/                 # Utility functions
```

## Key Components

### Services
Services provide specific functionalities through standard interfaces. Some examples include:
- Telegram service for communication
- Web service for browser-based dashboards
- Webhook service for external signals

### Notifiers
Notifiers send information to users through various channels:
- Email notifications
- Telegram messages
- Discord alerts
- Custom notification channels

### Interfaces
Interfaces allow users to interact with the OctoBot system:
- Command-line interfaces
- Bot-based interfaces (Telegram, Discord)
- Web interfaces

### Service Feeds
Service feeds bring external data into the OctoBot ecosystem:
- TradingView signals
- Social media feeds
- Custom data sources

## Usage Examples

### Creating a Service
```python
class MyCustomService(AbstractService):
    def get_type(self):
        return "my_service"
        
    def get_endpoint(self):
        return "https://my-service-endpoint.com"
        
    async def prepare(self):
        # Service initialization code
        pass
        
    def has_required_configuration(self):
        return all(key in self.config for key in self.get_required_config())
        
    def get_successful_startup_message(self):
        return "My custom service successfully started!", True
```

### Using a Service
```python
class MyServiceUser(AbstractServiceUser):
    REQUIRED_SERVICES = [MyCustomService]
    
    def __init__(self, config):
        super().__init__(config)
        # Initialization code
```

## Configuration
Services are configured through the OctoBot configuration system. Each service can specify:
- Required configuration fields
- Default values
- Field descriptions
- Read-only information
```
services:
  my_service:
    enabled: true
    api_key: "your-api-key-here"
    secret: "your-secret-here"
```
