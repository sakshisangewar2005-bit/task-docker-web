# Docker Web Server — Internship Task 4

A complete, small web application demonstrating Docker containerization. It
serves a responsive status page, exposes JSON health/runtime endpoints, runs as
the unprivileged `node` user, and includes a Docker health check and Compose
restart policy. It uses only Node.js built-ins, so there are no npm packages to
install.

## Requirements

- Docker Desktop on Windows/macOS, or Docker Engine with the Docker Compose
  plugin on Linux
- Node.js 20+ only if you want to run the test suite or run the server outside
  Docker

## Run it with Docker Compose

1. Extract the ZIP file.
2. Open a terminal in the `task-docker-web` folder.
3. Confirm Docker is running:

   ```sh
   docker --version
   docker compose version
   ```

4. Build the image and start the container:

   ```sh
   docker compose up --build -d
   ```

5. Confirm it is running and wait for the health status:

   ```sh
   docker compose ps
   ```

6. Open **http://localhost:3000** in a browser. The page displays live runtime
   information.
7. Check the JSON endpoints:

   - `http://localhost:3000/health` — used by Docker's health check
   - `http://localhost:3000/api/status` — runtime and Node.js details

8. View logs:

   ```sh
   docker compose logs -f web
   ```

   Press `Ctrl+C` to stop following the logs; the container keeps running.

9. Stop and remove the container/network:

   ```sh
   docker compose down
   ```

The same commands are collected in `COMMANDS.txt`, `commands.sh` (macOS/Linux),
and `commands.ps1` (Windows PowerShell).

## Run the automated tests

With Node.js 20 or later installed, from this folder run:

```sh
npm test
```

No `npm install` is needed. The tests start the server on a temporary local port
and check the home page, health endpoint, status endpoint, 404 handling, and
unsupported HTTP methods.

## Run without Docker (optional)

macOS/Linux:

```sh
PORT=3000 npm start
```

Windows PowerShell:

```powershell
$env:PORT = "3000"
npm start
```

Visit `http://localhost:3000`, then press `Ctrl+C` to stop the server.

## Useful Docker commands

```sh
docker compose ps                 # status and health
docker compose logs -f web        # follow app logs
docker compose restart web        # restart the service
docker compose up --build -d      # rebuild and start after code changes
docker compose down               # stop and remove the container/network
```

If port `3000` is already in use, change the host-side port in `compose.yaml`
from `"3000:3000"` to `"3001:3000"`, then rebuild/start and visit
`http://localhost:3001`.

## What this demonstrates

- **Containerization:** a `Dockerfile` builds the web server image.
- **Web server in a container:** Docker maps host port 3000 to container port
  3000.
- **Lifecycle and health:** Docker checks `/health`; Compose restarts the
  service unless it is intentionally stopped.
- **Operational troubleshooting:** view status and logs with Docker Compose.
- **Safer image defaults:** Alpine-based Node image, limited build context, and
  a non-root runtime user.

## Internship submission note

This ZIP completes the **Task 4: Web Server using Docker** option shown in the
provided task sheet. The sheet says participants must complete at least **two
or three** listed tasks for certificate eligibility, so this one task by itself
does not meet that minimum. Run and verify the project, then follow the
organizer's submission form and repository naming instructions.
