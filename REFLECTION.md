# Reflection: Dockerizing the QR Code Generator

## What I did

I took the provided QR code generator script and containerized it using Docker.
This involved writing a Dockerfile based on a slim Python base image, setting up
a non-root user to run the application securely, and configuring the container
to accept a `--url` argument at runtime. I built the image locally, ran it as a
container, confirmed the QR code generation worked by checking the container
logs and the mounted output volume, and pushed the finished image to DockerHub.
I also set up a GitHub Actions workflow so the image gets built (and pushed to
DockerHub on merges to main) automatically.

## What I learned

- [Fill in: e.g., how COPY ordering + requirements.txt affects Docker's layer
  caching, why a slim base image matters, how USER changes the security
  posture of a container]
- [Fill in: how volume mounts (`-v`) let container output persist on the host
  instead of disappearing when the container is removed]
- [Fill in: anything new about GitHub Actions secrets and how they're used to
  authenticate with DockerHub in CI without hardcoding credentials]

## Challenges I faced

- [Fill in: any build errors you hit and how you fixed them]
- [Fill in: any permission issues from the non-root user, e.g. write access
  to qr_codes/ or logs/ inside the container]
- [Fill in: anything about DockerHub login/push that was confusing]

## What I would do differently

- [Fill in: e.g., healthchecks, multi-stage builds, smaller image size,
  better logging to a file instead of just stdout]
