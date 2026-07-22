## Reverse Proxy Configuration

### Nginx Proxy Manager

- Connected Nginx Proxy Manager to the `single-node_default` Docker network.
- Configured proxy to use the Wazuh Dashboard container.
- Verified connectivity using the container hostname.

### Homepage Integration

Homepage is configured to access Wazuh through:

http://wazuh.home.lab

### Troubleshooting

Issue:
Homepage continued opening `https://wazuh.home.lab`, which failed.

Cause:
Homepage container was mounted to:

/home/malcolm/projects/homelab/docker/homepage/config

An older configuration existed at:

/home/malcolm/docker/homepage/config

Edits were being made to the wrong configuration directory.

Resolution:
Verified the active bind mount using:

docker inspect homepage --format='{{range .Mounts}}{{println .Source "->" .Destination}}{{end}}'

Updated the active Homepage configuration and restarted the Homepage container.

Lesson Learned:
Always verify Docker bind mounts before editing configuration files.
