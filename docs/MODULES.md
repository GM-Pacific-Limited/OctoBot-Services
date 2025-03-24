# OctoBot-Services Modules

## Services
The `services` module provides the core service system:
- `AbstractService`: Base class for all services
- `ServiceFactory`: Creates and manages service instances

## Notification
The `notification` module handles the notification system:
- `AbstractNotifier`: Base class for sending notifications
- Various notification implementations for different events

## Interfaces
The `interfaces` module manages user interfaces:
- `AbstractInterface`: Base class for all interfaces
- `AbstractBotInterface`: For command-based interactions
- `AbstractWebInterface`: For web-based interactions

## Service Feeds
The `service_feeds` module handles external data sources:
- `AbstractServiceFeed`: Base class for service feeds
- `ServiceFeedFactory`: Creates service feed instances

## Managers
The `managers` module provides component lifecycle management:
- `ServiceManager`: Manages service lifecycle
- `InterfaceManager`: Manages interface lifecycle
- `ServiceFeedManager`: Manages service feed lifecycle

## Channels
The `channel` module implements the communication system:
- `UserCommandsChannel`: For user command distribution
- `NotificationChannel`: For notification distribution
