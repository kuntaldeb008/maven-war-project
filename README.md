# Project Description :-

1.) Open [http://devserverpublicip:8080/ansibledockerapp-1.0/hello](http://devserverpublicip:8080/ansibledockerapp-1.0/hello) in your browser.

2.) Git Repository :- https://github.com/kuntaldeb008/maven-war-project

3.) If we push / check-in any changes to git repository , then Jenkins Job running in Jenkins Master Machine will auto build and run the declarative pipeline as Poll SCM is configured for every minute.

4.) Jenkins Job will perform following actions :-
    a.) Clone the git project and build the war of maven git project.
    b.) Will build the docker image “kuntaldeb008/javapp”.
    c.) Will then push the docker image to mine own docker hub repository - https://hub.docker.com/repository/docker/kuntaldeb008/javaapp
    d.) Will then invoke the ansible playbook command defined in declarative pipeline in Jenkins Job [Note ansible is installed in Jenkins machine]
    e.) It will then install python-pip , docker in dev server .
    f.) It will then start and enable the docker service in dev-server.
    g.) It will then pull the docker image docker/kuntaldeb008/javaapp will then finally start and run the docker container in dev-server.
