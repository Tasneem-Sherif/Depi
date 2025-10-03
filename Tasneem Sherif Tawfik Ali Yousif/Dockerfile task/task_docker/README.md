  - Why copy manifests first?
Copying package.json and package-lock.json first allows Docker to cache the layer of npm install.
If your code changes but dependencies stay the same, Docker won’t re-run npm install, which saves time.

  - Difference between `npm ci` and `npm install` in Docker 
npm install installs dependencies and updates package-lock.json if needed.
npm ci is faster, installs exactly what’s in package-lock.json.

  - Why run as non-root? 
Running as non-root increases security → even if attacker exploits container, they don’t get root access.
Best practice in production containers.

  - what is healthcheck that you added what's used for 
Healthcheck is a command Docker runs periodically to check if your application is healthy.
Docker sets container status: healthy / unhealthy.

