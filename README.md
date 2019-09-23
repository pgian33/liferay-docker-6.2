# liferay-docker-6.2

This is a guide to configure a dockerized Docker of Liferay 6.2.5-CE.
To run your docker instance you have to run the following command:

    > ./build_image.sh https://releases.liferay.com/portal/6.2.5-ga6/liferay-portal-tomcat-6.2-ce-ga6-20160112152609836.zip 
	
Note:

you have to run the build as a root user. Before running the build_image.sh you need to set the JAVA_HOME. 
So, put inside /etc/profile your environment variables of java and the you have to run 
 
    > source /etc/profile
	
Then, cheek your java version:
    > java -version
