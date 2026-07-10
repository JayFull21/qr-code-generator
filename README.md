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
