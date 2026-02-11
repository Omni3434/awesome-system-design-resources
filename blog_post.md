# Master Load Balancing: A Core System Design Concept

Today we are diving into one of the most fundamental topics in System Design: **Load Balancing**.

I found some great implementations of load balancing algorithms in our repository and wanted to share them with you.

### What is Load Balancing?
Load balancing is the process of distributing network traffic across multiple servers. This ensures no single server bears too much demand. By spreading the work evenly, load balancing improves application responsiveness and increases availability of applications and websites for users.

### 1. Round Robin Algorithm
The Round Robin algorithm is the simplest method for distributing client requests across a group of servers. It passes each new request to the next server in line.

Here is how it's implemented in Python:

```python
class RoundRobin:
    def __init__(self, servers):
        self.servers = servers
        self.current_index = -1

    def get_next_server(self):
        self.current_index = (self.current_index + 1) % len(self.servers)
        return self.servers[self.current_index]
```

When running this with 3 servers, you get a perfectly even distribution:
- Request 1 -> Server1
- Request 2 -> Server2
- Request 3 -> Server3
- Request 4 -> Server1

### 2. Least Connections Algorithm
While Round Robin is simple, it doesn't take into account the current load on the servers. The **Least Connections** algorithm is smarter: it sends requests to the server with the fewest active connections.

```python
import random

class LeastConnections:
    def __init__(self, servers):
        self.servers = {server: 0 for server in servers}

    def get_next_server(self):
        min_connections = min(self.servers.values())
        least_loaded_servers = [server for server, connections in self.servers.items() if connections == min_connections]
        selected_server = random.choice(least_loaded_servers)
        self.servers[selected_server] += 1
        return selected_server
```

This is particularly useful when requests take varying amounts of time to process, as it prevents overloading a server that is still busy with previous long-running requests.

I hope this helps your study! Happy learning!

Best regards,
Jules
