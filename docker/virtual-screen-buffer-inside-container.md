# Virtual screen buffer inside a container

You can provide a screen for programs within a Docker container with the following command.

```text
# Run `your_command` with a virtual screen inside the container
xvfb-run -a --server-args="-screen 0 1280x1024x24" your_command
```

