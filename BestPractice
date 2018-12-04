# Docker Best Practice<br>
This page introduces some best practices for developers to make the developing process easier and more effective. Both general docker development best practices and best practices for writing dockerfiles will be covered below. For detailed information, please visit https://docs.docker.com/develop/dev-best-practices/. <br>


## Best practices for Docker Development <br>

### Keep images small</b>.###
Small images are easier to be transfered over internet and usually take less time to be loaded. Some useful tips for making image small are:
* <b>Choose a suitable base image</b>. Use only what you need. Avoid loading a generic image and adding components you need.
* <b>Use multistage builds</b>. Only keep the artifacts and the environment needed by your program in the final image.
  * If you need to use a version of Docker that does not include multistage builds, try to reduce the number of layers in your image by minimizing the number of separate 'RUN' commands in your Dockerfile. You can do this by consolidating multiple commands into a single RUN line and using your shell’s mechanisms to combine them together. Consider the following two fragments. The first creates two layers in the image, while the second only creates one.
  '''RUN apt-get -y update
     RUN apt-get install -y python
  '''
  '''RUN apt-get -y update && apt-get install -y python
  '''
* <b>Put common components in your own base image</b>. If multiple images have many common components, create your own base image that contains these shared components to avoid unnecessary load times. By doing so, the loading process will be more quickly and efficiently. 
* <b>Use the production image as the base image for the debug image</b>
* <b>Tag your image with useful tags!</b> Tag images wich codify version information, intended destination, stability, etc. Do not rely on automatically created latest tag

### Persist application data ###
* <b>Avoid storing application data in your container’s writable layer using storage drivers</b>. This increases the size of your container and is less efficient from an I/O perspective than using volumes or bind mounts. Using volumes to stode data!
* <b>Use secrets to store sensitive data and use configs for non-sensitive data</b>.

### Use swarm services when possible! ###
Even if you only need to run a single instance of your application, swarm services provide several advantages over standalone containers. A service’s configuration is declarative, and Docker is always working to keep the desired and actual state in sync.

### Use CI/CD for testing and deployment ###
* <b>Use Docker cloud or other CI/CI pipeline to automatically build and tag Docer image and test it</b>
* <b>Use Docer EE before deploying images into production to ensure it is tested and signed off by development, quality, and security teams.</b>

### Differences in development and production environments ###
<table>
  <thead>
    <tr>
      <th style="text-align: left">Development</th>
      <th style="text-align: left">Production</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: left">Use bind mounts to give your container access to your source  code.</td>
      <td style="text-align: left">Use volumes to store container data.</td>
    </tr>
    <tr>
      <td style="text-align: left">Use Docker for Mac or Docker for Windows.</td>
      <td style="text-align: left">Use Docker EE if possible, with <a href="/engine/security/userns-remap.md">userns mapping</a> for greater isolation of Docker processes from host processes.</td>
    </tr>
    <tr>
      <td style="text-align: left">Don’t worry about time drift.</td>
      <td style="text-align: left">Always run an NTP client on the Docker host and within each container process and sync them all to the same NTP server. If you use swarm services, also ensure that each Docker node syncs its clocks to the same time source as the containers.</td>
    </tr>
  </tbody>
</table>

Reference for the content above: Docker development best practices - https://docs.docker.com/develop/dev-best-practices/
