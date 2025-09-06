## 5 Docker Security Best Practices.

1. ### Ensure container processes run as a non-root user

By default, Docker containers run as the root user (UID 0), which increases security risks if the container is compromised. Best practice is to run as a non-root user.

* Option 1: Create a User in the Dockerfile

You can define a dedicated user inside the image and switch to it with the USER instruction.
Example from the provided Dockerfile:

Create an unprivileged user with UID/GID 10001
`USER 10001:10001`

This ensures that whenever the container starts, the process runs as an unprivileged user by default.
If you want a human-readable username (e.g., postgres or appuser), you can add it during the build with:

``` 
RUN groupadd -r appuser && useradd --no-log-init -r -g appuser appuser
USER appuser
```

* Option 2: Override at Runtime with --user

Alternatively, you can leave the image unchanged and specify the user when running the container:

```
docker run --user=1000 example-image:latest
```

Here, 1000 is the UID of the first non-root user on most Linux systems. It’s commonly used because:

UID 0 = root (full privileges)

UIDs 1–999 = reserved for system/service accounts

UID 1000 = first “regular” user account (e.g., the one created when the system was installed)

Running with `--user=1000` forces the container process to execute with a non-root identity, reducing the risk of privilege escalation.

Why This Matters

Prevents an attacker from gaining root privileges on the host if the container is compromised.

Limits access to files, system calls, and mounted volumes.

Aligns with security best practices for Docker and Kubernetes deployments.

2. ### Use minimal, trusted base images and pin versions/digests

Only select trusted base images for the FROM instructions in your Dockerfiles. You can easily find these images by filtering using the “Docker Official Image” and “Verified Publisher” options on Docker Hub. An image that’s published by an unknown author or which has few downloads might not contain the content you expect.

It’s also advisable to use minimal images (such as Alpine-based variants) where possible. These will have smaller download sizes and should contain fewer OS packages, which reduces your attack surface.

3. ### Don't expose unnecessary ports
Exposing container ports unnecessarily (using the -p or --port flag for docker run) can increase your attack surface by allowing external processes to probe inside the container. Only ports which are actually needed by the containerized application (typically those listed as Dockerfile EXPOSE instructions) should be opened.

4. ### Drop capabilities when you start containers
Even the default set of Linux capabilities granted by Docker can be too permissive for production use. They include the ability to change file UIDs and GIDs, kill processes, and bypass file read, write, and execute permission checks.

It’s good practice to drop capabilities that your container doesn’t need. The docker run command’s --cap-drop and --cap-add flags allow you to remove and grant them. The following example drops every capability, then adds back CHOWN to permit file ownership changes:

```
$ docker run --cap-drop=ALL --cap-add=CHOWN example-image:latest
```

5. ### Don't start containers in privileged mode
Using privileged mode (--privileged) is a security risk that should be avoided unless you’re certain it’s required. Containers that run in privileged mode are granted all available Linux capabilities and have some cgroups restrictions lifted. This allows them to achieve almost anything that the host machine can.

Containerized apps very rarely require privileged mode. It’s typically only useful when you’re running an application that needs full access to your host or the ability to manage other Docker containers.

 ***Dockerfile With best practices***

 ```
FROM nginx:1.27-alpine
WORKDIR /usr/share/nginx/html
COPY index.html .
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN addgroup -S web \
    && adduser -S web -G web \
    && chown -R web:web /var/cache/nginx /var/run /var/log/nginx \
    && chown -R web:web /usr/share/nginx/html
USER web
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
 ```