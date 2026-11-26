# Hindsight

A local Docker Compose setup for [Hindsight](https://github.com/vectorize-io/hindsight), an AI memory service. The official all-in-one image provides the Hindsight API, control plane, and embedded PostgreSQL.

## Features

- Runs the Hindsight API and control plane in one container.
- Connects to an LLM provider; the Compose defaults use Ollama on the host.
- Persists data in a Docker-managed volume across container restarts.
- Binds the API (`8888`) and control plane (`9999`) to localhost.

## Run

Requires Docker with the Compose plugin. For the default configuration, run Ollama on the host and make the configured model available there.

```sh
docker compose up -d
```

The API and control plane are available at `http://localhost:8888` and `http://localhost:9999`, respectively. To inspect the service logs:

```sh
docker compose logs -f hindsight
```

## Configuration

`compose.yaml` defaults to the Ollama endpoint `http://host.docker.internal:11434/v1` and model `minicpm5-2b:latest`. Override these values in your shell or in a local `.env` file. `.env.example` contains configuration notes and examples; uncomment only the settings you need and replace example credentials with your own.

The Compose ports are bound to localhost. The API does not have authentication enabled by default; configure authentication before exposing it beyond your local machine. The `hindsight-data` volume stores persistent data.
