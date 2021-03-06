====
Portainer (With ECR support)
====

(Taken from https://github.com/portainer/portainer/issues/1533#issuecomment-689927288)

----
Usage
----

.. code-block:: bash

  $ ./build.sh
  $ docker swarm init --advertise-addr=<your-public-or-private-ip>
  $ docker stack deploy -c ecr-portainer-agent-stack.yml portainer


----
Caveats
----

* In case you want to test it out, attach a new console to the container. In Portainer go to Containers > Click the 'portainer' container > Attach:

.. code-block:: bash

  / # ./docker pull <ECR Repo/image>

* You will not be able to pull images from the Portainer UI, however, you can use ECR repository images in Stacks inside Portainer, like so:

.. code-block:: yml

  version: "3.3"
  services:
    my-awesome-service:
      image: <registy-id>.dkr.ecr.<aws-region>.amazonaws.com/<repository-name>:<image-tag>

* When calling Service Webhooks to update images the hook will fail when trying to find the latest image. To fetch the latest image you need to SSH into the server and pull the image like shown above