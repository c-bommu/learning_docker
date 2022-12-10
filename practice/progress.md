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
          * There are two main types of volumes: named volumes & anonymous volumes.
               * I began with first learning about named volumes.
     * To persist data...
          * Learned that with my database being in a single file, if we can persist that file on the host and make it available to the next container, it should be able to pick up where the last one left off.
          * By creating a volume and attaching (often called “mounting”) it to the directory the data is stored in, we can persist the data. As my container writes to my database file, it would persist to the host in the volume.
          * Learned how to use a **named volume**.
               * Learned that a named volume can be thought of as simply a bucket of data. Docker maintains the physical location on the disk and I would only need to remember the name of the volume. So, every time I use the volume, Docker would make sure that the correct data is provided.
                    * Learned to use the `docker volume create` command to create a volume
               * The `docker volume inspect` command tells me where Docker is *actually* storing my data when I use a named volume.
                    * Specifically, the `Mountpoint` that is presented after running this command displays the actual location on the disk where the data is stored. It would be important to note that on most machines, I would need to have root access in order to access this directory from the host.
