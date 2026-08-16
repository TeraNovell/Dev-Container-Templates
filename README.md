# Dev-Container-Templates

## Personal Dev Container Configuration Override

VS Code Dev Containers currently do not support local overrides or inheritance for an existing `devcontainer.json` for personal or machine-specific changes. Personal changes to the Dev Container configuration therefore require a separate configuration file.

To set up a local configuration, create a subdirectory such as `local` inside `.devcontainer` and copy the existing `devcontainer.json` into it. Personal changes can then be made in `.devcontainer/local/devcontainer.json` instead of modifying the shared configuration.

The `local` directory should be added to the `.gitignore` file so that the personal configuration does not affect other users.

### Docker Compose overrides

Docker Compose overrides can be added in a separate Compose file. The local `devcontainer.json` can reference the project's original Compose file together with an additional local override:

```json
{
    "dockerComposeFile": [
        "../docker-compose.yml",
        "./docker-compose.override.yml"
    ]
}
```

To add a Compose override, create a Compose file, for example `docker-compose.override.yml`, in the previously created `local` directory and add your overrides to it. For example, the following adds a local named volume that can be used to persist configuration and share it between Dev Containers:

```yaml
services:
  app:
    volumes:
      - my-local-volume:/some/path

volumes:
  my-local-volume:
    name: my-local-volume
```
