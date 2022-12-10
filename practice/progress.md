# Building a simple todo list manager:

1. Began the tutorial through Docker Labs’ Docker Playground.
2. Learned the very basics about building a container image and created a Dockerfile to do so. Once I built an image, I started the container and saw the running todo list app.
3. Made a modification to the app and learned how to update my running application with a new image. During this process, I learned other useful commands such as `docker ps` to get container IDs, `docker stop` to stop containers using the previously obtained IDs, and `docker rm` to remove stopped containers.
4. Learned about tags and how to share images with others using Docker Hub
     * “Tagging” an image basically means giving it another name
     * Learned commands `docker login`, `docker tag`, and `docker push`
5. After having built an image that had been pushed into a registry, I learned how to run an image on a brand new instance that had never seen this container and was able to run the freshly pushed image.
6. Learned how to see code updates without needing to rebuild and start a new container every time I make a change (persistence across restarts)
     * Regarding a container’s file system...
          * Learned how to start an `ubuntu` container
          * Learned how to use the `docker exec` command
          * Learned that containers are effectively read-only. While containers can create, update, and delete files, those changes are lost when the container is removed and are isolated to that container. Volumes can change this.
     * Regarding container volumes...
          * Learned that volumes provide the ability to connect specific filesystem paths of the container back to the host machine. If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.
          * There are two main types of volumes: named volumes & bind mounts.
               * I began with first learning about named volumes.
     * To persist data...
          * Learned that with my database being in a single file, if we can persist that file on the host and make it available to the next container, it should be able to pick up where the last one left off.
          * By creating a volume and attaching (often called “mounting”) it to the directory the data is stored in, we can persist the data. As my container writes to my database file, it would persist to the host in the volume.
          * Learned how to use a **named volume**.
               * Learned that a named volume can be thought of as simply a bucket of data. Docker maintains the physical location on the disk and I would only need to remember the name of the volume. So, every time I use the volume, Docker would make sure that the correct data is provided.
                    * Learned to use the `docker volume create` command to create a volume
               * The `docker volume inspect` command tells me where Docker is *actually* storing my data when I use a named volume.
                    * Specifically, the `Mountpoint` that is presented after running this command displays the actual location on the disk where the data is stored. It would be important to note that on most machines, I would need to have root access in order to access this directory from the host.
               * Named volumes are great if we simply want to store data, since we would not have to worry about *where* it is stored.
7. Learned that **bind mounts** serve as a better way of making changes since rebuilding images for every change takes quite a bit of time.
     * They allowed me to control the exact mountpoint on the host.
          * While we can use this to persist data (like I practiced earlier), it is often used to provide additional data into containers.
          * I was able to use a bind mount to mount my source code into the container to let it see code changes, respond, and allow me to see changes immediately.
     * For Node-based applications, [nodemon](https://www.npmjs.com/package/nodemon) is a useful tool used to watch for file changes and then restart the application.
8. Learned how to start a dev-mode container
     * First, I had to mount my source code into the container after ensuring that I had no previous associated Docker containers running
          * Learned that I need to choose a base image (in my case, `node:10-alpine`) to use for my app from the Dockerfile
     * Next, I installed all dependencies, including the “dev” dependencies
          * Used `yarn install` and `yarn run dev` for my application
     * Lastly, I started nodemon to watch for any filesystem changes
          * This was done in the same command that I had run in the previous step, since the `dev` script within the `package.json` file starts `nodemon`.
9. Figured out how to watch logs using the `docker logs` command
     * After watching logs, I was able to make a change to my app and then simply refresh/reopen the localhost page to see the change reflected almost immediately.
          * I should mention that after all of the desired changes have been made, it is important to stop the container and then build a new image so that these changes will be saved.

