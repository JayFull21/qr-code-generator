# QR Code Generator

A command-line tool that generates a QR code image from a URL, built to be run either directly with Python or inside a Docker container.

## Features

- Generates a QR code PNG from any valid URL
- Timestamped output filenames (`QRCode_<timestamp>.png`)
- Configurable output directory and colors via environment variables
- URL validation before generation
- Runs as a non-root user inside its Docker container for security

## Local Setup (without Docker)

```bash
python3 -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python main.py --url https://github.com/kaw393939
```

The QR code will be saved to `qr_codes/`.

### Configuration

Copy `.env.example` to `.env` to customize behavior:

```bash
cp .env.example .env
```

| Variable | Description | Default |
|---|---|---|
| `QR_CODE_DIR` | Directory where QR codes are saved | `qr_codes` |
| `FILL_COLOR` | QR code foreground color | `red` |
| `BACK_COLOR` | QR code background color | `white` |

## Running with Docker

### Build the image

```bash
docker build -t qr-code-generator-app .
```

### Run the container

```bash
docker run -d --name qr-generator qr-code-generator-app
```

To use a custom URL and persist the generated QR code on your host machine:

```bash
docker run -d --name qr-generator \
  -v $(pwd)/qr_codes:/app/qr_codes \
  qr-code-generator-app --url http://www.njit.edu
```

### Check the logs

```bash
docker logs qr-generator
```

### Clean up

```bash
docker stop qr-generator
docker rm qr-generator
```

## Pushing to DockerHub

```bash
docker login
docker tag qr-code-generator-app your-dockerhub-username/qr-code-generator-app
docker push your-dockerhub-username/qr-code-generator-app
```

Replace `your-dockerhub-username` with your actual DockerHub username.

## Continuous Integration

A GitHub Actions workflow (`.github/workflows/docker-build.yml`) runs on every push and pull request to `main`. It builds the Docker image to verify it compiles cleanly, and on pushes to `main` it also logs in to DockerHub and pushes the image automatically.

To enable the automated push, add these two repository secrets under **Settings → Secrets and variables → Actions**:

- `DOCKERHUB_USERNAME` — your DockerHub username
- `DOCKERHUB_TOKEN` — a DockerHub access token (create one under DockerHub → Account Settings → Security → New Access Token)

## Project Structure

```
qr-code-generator/
├── main.py                          # QR code generation script
├── requirements.txt                 # Python dependencies
├── Dockerfile                       # Container build instructions
├── .dockerignore                    # Files excluded from the Docker build context
├── .env.example                     # Configuration template
├── .github/workflows/
│   └── docker-build.yml             # CI: builds and pushes the Docker image
├── qr_codes/                        # Generated QR code images (gitignored)
└── logs/                            # Application logs (gitignored)
```
