# docker
Puppet master docker file will be creating puppet master container, Please use below command to run puppetmaster docker container:
    docker run --name puppermaster -h puppet -d -t -i puppetmaster:image
    
Puppet agent docker file will be creating puppet agent container, Please use below command to run puppetmaster docker container:
    docker run --name pupperagent1 -h puppetagent1 --add-host=puppet:172.17.0.2 -d -t -i puppetagent:image
    
    
    
    https://github.com/SonarOpenCommunity/sonar-cxx/releases
