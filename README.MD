# About

Steps to create a docker containter with **mirth-connect-3.5.1** from an already existing image.


# Create container

To create a mirth-connect container with v3.5.1, run

        docker run -d -P --name mirth marlycormar/mirth-connect-3.5.1

It will create a container from [this](https://hub.docker.com/r/marlycormar/mirth-connect-3.5.1/) already existing image found on Docker Hub. 


## Create container with custom configurations

You can apply custom configurations before running the mirth image:

1. Download a template configuration file from: `https://github.com/marlycormar/mirth-connect-3.5.1/blob/master/mirth.properties.example`

1. Rename the configuration file to `mirth.properties`:

        mv mirth.properties.example mirth.properties 

1. Make the necessary changes to the configuration file, e.g., add db credentials.

1. Run Mirth Connect with this configuration:
        
        docker run -d -P -v <absolute_path>/mirth.properties:/opt/mirth-connect/conf/mirth.properties marlycormar/mirth-connect-3.5.1


# Usage

After the container is created, follow the steps below to open Mirth Connect:

1. Check the ports on which the server is running:

        docker ps

1. Download mirth connect admin by going to:

        127.0.0.1:<8080_PORT>/webstart.jnlp
e.g.,
        127.0.0.1:32771/webstart.jnlp

1. When prompted, provide the following configuration:

        host: https://localhost:<8443_PORT>
        username: admin
        password: admin
        

# Notes

If you would like to run Mirth Shell, first copy the image name from `docker ps` and then run:

        docker run -it --link <image_name>:mirth-connect marlycormar/mirth-connect-3.5.1 java -jar mirth-cli-launcher.jar -a https://mirth-connect:8443 -u admin -p admin