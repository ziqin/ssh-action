# SSH GitHub Action

A lightweight GitHub Action for executing remote commands via SSH.

This action is implemented with simple shell commands, featuring minimal
implementation which can be easily reviewed within seconds.

## Usage

### Basic Example

```yaml
name: Deploy to Server
on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Execute remote commands
        uses: ziqin/ssh-action@v0.1.1
        with:
          host: 'your-server.example.com'
          user: 'deploy'
          key: ${{ secrets.SSH_PRIVATE_KEY }}
          known_hosts: ${{ vars.SSH_KNOWN_HOSTS }}
          script: |
            cd /opt/myapp
            docker compose pull
            docker compose up -d
```

## Inputs

| Input         | Description                              | Required | Default |
|---------------|------------------------------------------|----------|---------|
| `host`        | SSH hostname or IP address to connect to | Yes      | -       |
| `port`        | SSH port number                          | No       | 22      |
| `user`        | SSH username for authentication          | Yes      | -       |
| `key`         | SSH private key in PEM format            | Yes      | -       |
| `known_hosts` | SSH `known_hosts` entry for the host     | Yes      | -       |
| `script`      | Commands to execute on the remote host   | Yes      | -       |

## Security Considerations

1. **Always use secrets** for storing SSH key and sensitive information
2. **Verify server identity** by properly configuring `known_hosts`
3. **Use dedicated deployment key** with minimal required permissions

## Common Use Cases

- 🚀 **Application Deployment**: Deploy code to production servers
- 🔄 **Service Management**: Start/stop/restart services
- 📊 **Health Checks**: Run diagnostics on remote servers
- 🔧 **Configuration Management**: Update server configurations

## Error Handling

The action runs scripts with strict error handling (`set -euo pipefail`).
If any command fails, the step will fail.

## License

This action is released under MIT License.  See [LICENSE](LICENSE) file
for details.
