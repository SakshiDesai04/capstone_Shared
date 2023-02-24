app-jee-html5: HTML5 Service Invocation Application
===================================================

Level: Beginner  
Technologies: HTML5, JavaScript  
Summary: HTML5 Service Invocation Application packaged as a WAR  
Target Product: <span>Keycloak</span>, <span>WildFly</span>  
Source: <https://github.com/keycloak/keycloak-quickstarts>

What is it?
-----------

The `app-jee-html5` quickstart demonstrates how to write an application with HTML5 and JavaScript that authenticates
using <span>Keycloak</span>. Once authenticated the application shows how to invoke a service secured with <span>Keycloak</span>.

For simplicity of deploying the application it is packaged as a WAR archive and can be deployed to JBoss EAP.
As the example only contains static html pages the files in `src/main/webapp` can also be hosted on any web server.


System Requirements
-------------------

The quickstart requires that you have the [example services](../service-jee-jaxrs/README.md) running. It assumes the
services are located at `http://localhost:8080/service`. If the services are running elsewhere you need to edit
`app.js` and replace the value of `serviceUrl`.

See the [Getting Started Guide](../docs/getting-started.md) for the minimum requirements and steps to build and run the quickstart.


Configuration in <span>Keycloak</span>
-----------------------

Prior to running the quickstart you need to create a client in <span>Keycloak</span> and download the installation file.

The following steps show how to create the client required for this quickstart:

* Open the <span>Keycloak</span> admin console
* Select `Clients` from the menu
* Click `Create`
* Add the following values:
  * Client ID: You choose (for example `app-html5`)
  * Client Protocol: `openid-connect`
  * Root URL: URL to the application (for example `http://localhost:8080/app-html5`).
* Click `Save`

If you deploy the application somewhere else change the hostname and port of the URLs accordingly.

Once saved you need to change the `Access Type` to `public` and click save.

Finally you need to configure the javascript adapter, this is done by retrieving the adapter configuration file:

* Click on `Installation` in the tab for the client you created
* Select `Keycloak OIDC JSON`
* Click `Download`
* Move the file `keycloak.json` to the `config/` directory in the root of the quickstart

As an alternative you can create the client by importing the file [client-import.json](config/client-import.json) and
copying [config/keycloak-example.json](config/keycloak-example.json) to `config/keycloak.json`.


Build and Deploy the Quickstart
--------------------------------

1. Open a terminal and navigate to the root directory of this quickstart.

2. The following shows the command to deploy the quickstart:

   ````
   mvn clean wildfly:deploy

   ````


Access the Quickstart
---------------------

You can access the application with the following URL: <http://localhost:8080/app-html5>.

The application provides buttons that allows invoking the different endpoints on the service:

* Invoke public - Invokes the public endpoint and doesn't require a user to be logged-in
* Invoke secured - Invokes the secured endpoint and requires a user with the role `user` to be logged-in
* Invoke admin - Invokes the secured endpoint and requires a user with the role `admin` to be logged-in

If you invoke the endpoints without the required permissions an error will be shown.


Undeploy the Quickstart
-----------------------

1. Open a terminal and navigate to the root directory of this quickstart.

2. The following shows the command to undeploy the quickstart:

   ````
   mvn wildfly:undeploy

   ````

Integration test of the Quickstart
----------------------------------

1. Make sure you have a Keycloak server running with an `admin` user with a password `admin` in the `master` realm running on following url `http://localhost:8180/auth` or use the provided docker image
2. You need to have Chrome browser installed and updated to the latest version.
3. Run `mvn clean install -Pwildfly-managed -Denforcer.skip=true`