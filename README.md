Dockdiffy
==========

Example of how to use twitter diffy (https://github.com/twitter/diffy) running on docker containers

Running
--------

To run it you will need docker and docker-compose installed. Read more about it here: https://www.docker.com/toolbox

Clone this repository:

      $ git clone git@github.com:camiloribeiro/dockdiffy.git
      $ cd dockdiffy

Run docker compose up command:
      
      $ docker-compose up

Now you will see the logs for all the four services: the twitter diffy proxy, the candidate service, the primary and secondary services. 
You will be able to access the web console for diffy on http://localhost:8888/

Now you can curl to check the differences:

      $ curl http://localhost:31900/endpoint

In the web console you will be able to see the diffs. 

To change the services the only thing you need to do is to change the three flavor files, candidate, primary and secondary. Whatever you change there will change when you restart the docker-compose.

ps: If you are running on mac or windows, remember to use the docker-machine/boot2docker/whateveryourundockeron instead of localhost or port forward it to localhost :)

Have fun!

Digging a bit more
------------

there are some other resources running in the same containers. You can play with it with the following curls:

      $ curl --header "Canonical-Resource: /endpoint" http://localhost:31900/endpoint
      $ curl --header "Canonical-Resource: /endpoint/foo" http://localhost:31900/endpoint/foo
      $ curl --header "Canonical-Resource: /endpoint/meh" http://localhst:31900/endpoint/meh

Applying to your own service
--------------

As you can see in the docker-compose.yml, you can replace the container with two different versions of your service and expose the ports in a way to keep the same configuratio in both services. For example:
       
       candidate:
         image: mycompany/my_service:new_version
         ports:
           - "8080"
       
       primary:
         image: mycompany/my_service:stable_version
         ports:
           - "8080"

       secondary:
         image: mycompany/my_service:stable_version
         ports:
           - "8080"

What is the service being tested here?
-----

It is a rest-shifter service. Easy way to create simple service mocks and prototypes. 
Read more: https://github.com/camiloribeiro/restshifter

LICENSE
--------

Copyright 2015 Camilo Ribeiro camilo@camiloribeiro.com

This file is part of Dockdiffy.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
