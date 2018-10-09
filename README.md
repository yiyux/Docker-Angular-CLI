# Docker-Angular-CLI
Docker Compose configuration for Angular CLI


So to get what you want with docker-compose run, use publish to publish the ports. As run doesn't use the mappings from your docker-compose.yml, it ignores them. So use it like this:

docker-compose run --publish 80:4200 node bash

Then create the angular app and start it up as you were doing. I am adding the steps for anyone else looking into this answer in the future:

cd tmp (or any writable folder)

ng new myProject

cd myProject

ng serve --host 0.0.0.0 (--host 0.0.0.0 to listen to all the interfaces from the container)

Then in your browser, go to localhost and you should see the angular welcome page now as the port 4200 is published and bound to the host port 80 through the publish command as I showed above.

Everytime you have port forwarding issues, if you open a new terminal keeping the other terminal where you executed the original run command and run docker ps you will see this in the Ports column:

0.0.0.0:80->4200/tcp which means that your host on port 80 is forwarding to your container in port 4200 successfully.

If you see something like 4200/tcp and not the -> part, that means there is no mappings or ports published.
