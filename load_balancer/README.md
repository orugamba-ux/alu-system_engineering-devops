#!/usr/bin/env bash
# Installs and configures HAProxy load balancer with roundrobin to web-01 and web-02

# Update and install HAProxy
apt-get update -y
apt-get install -y haproxy

# Enable HAProxy to be started by init script
sed -i 's/ENABLED=0/ENABLED=1/' /etc/default/haproxy

# Create HAProxy configuration
cat > /etc/haproxy/haproxy.cfg << 'EOC'
global
    log 127.0.0.1 local0 notice
    maxconn 2000
    user haproxy
    group haproxy
    daemon

defaults
    log global
    mode http
    option httplog
    option dontlognull
    option forwardfor
    timeout connect 5000
    timeout client  50000
    timeout server  50000

frontend http_front
    bind *:80
    default_backend web_servers

backend web_servers
    balance roundrobin
    server web-01 3.80.194.42:80
    server web-02 52.70.163.162:80
EOC

# Validate configuration
haproxy -c -f /etc/haproxy/haproxy.cfg

# Restart HAProxy
service haproxy restart

echo "HAProxy installed and configured successfully with round-robin load balancing."