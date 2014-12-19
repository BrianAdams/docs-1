# Connecting Active Directory with Auth0

Auth0 integrates with Active Directory/LDAP through the __Active Directory/LDAP Connector__ that you install in your network.

The __AD/LDAP Connector (1)__, is a bridge between your __Active Directory (2)__  and the __Auth0 Service (3)__. This bridge is necessary because AD is typically locked down to your internal network, and Auth0 is a cloud service running on a completely different context.

<img src="https://docs.google.com/drawings/d/1X30jQAsatQTibLXgxKgDanbCH1RJ9ZAfoDmHV33jdBY/pub?w=630&amp;h=526">

You can install multiple instances of the connector for high availability and load balancing. Also, all connections are out-bound: from the connector to the Auth0 Server, so in general no changes to the firewall need to be applied.

Configuring an AD/LDAP connection in Auth0 requires two simple steps:

###1. Creating an AD/LDAP Connection in Auth0

The first step is creating a new Connection on the dashboard:

__Connections > Enterprise > AD/LDAP__

![](https://cdn.auth0.com/docs/img/ldap-create.png)

Name the connection and check whether you want `Kerberos` enabled for this connection. If you enable this, you need to enter the range of IP addresses from where `Kerberos` authentication will be enabled. These would typically be the intranet where `Kerberos` would work.

In addition, the `Email domains` field, whitelists email suffixes that will be recognized before redirecting users to this particular AD/LDAP connection.

![](https://cdn.auth0.com/docs/img/ldap-create-2.png)

__Save__ the configuration. You are done on the Auth0 side! You will then be prompted to download the __AD/LDAP Connector__ to your machine.

![](https://cdn.auth0.com/docs/img/ldap-create-3.png)

> We ship different versions of the Connector to install it on multiple platforms: Windows, Linux and OS X

Keep the __TICKET URL__ at hand as you will need it later.

###2. Installing the AD/LDAP Connector

#### Auth0 AD LDAP Connector Setup (Windows Agent)
On Windows, the Connector is packaged as a standard installer file (__MSI__). Run it on the machine you want to install it on and follow the installation wizard:

![](https://s3.amazonaws.com/blog.auth0.com/adldap_01.PNG)

![](https://s3.amazonaws.com/blog.auth0.com/adldap_02.PNG)

> The __AD/LDAP Connector__ in Windows is installed as a Service: ![](https://s3.amazonaws.com/blog.auth0.com/adldap_06.PNG)

Once the installation is complete, you will see the following screen in a browser (notice that the browser is opening a page on the local machine).

Enter the __TICKET URL__ that was generated in __Step 1__.

The __Ticket URL__ uniquely identifies this connector in Auth0. Don't share it with anyone. The Connector will use this to communicate with Auth0 Server and automatically complete the configuration.

![](https://s3.amazonaws.com/blog.auth0.com/adldap_03.PNG)

If successful, the next screen will allow you to enter your __Active Directory__ connection parameters. Namely:

* The __LDAP Connection String__ (this is the network location of the server)
* The __Base DN__
* A __Username__ and a __Password__

These are credentials used by the __AD/LDAP Connector__ to authenticate itself with AD.

![](https://s3.amazonaws.com/blog.auth0.com/adldap_04.PNG)


##3. Testing your new Active Directory/LDAP connection

Go back to your Auth0 Dashboard and you should see a green dot next to your Connection definition:

![](https://s3.amazonaws.com/blog.auth0.com/adldap_07.png)

This signals that the __AD/LDAP Connector__ is online and working. Click on __Try__ to test the entire flow. If you configured `Kerberos` and are testing this inside your network, your login will happen automatically.

If you didn't configure `Kerberos` or you are outside your intranet you will be prompted for credentials. After successful authentication you should see the test screen showing the user profile:

![](https://s3.amazonaws.com/blog.auth0.com/adldap_08.png)

> Notice the __User profile__ includes the __Groups__ a user belongs to in AD. This will include any nested groups (flattened list).

##4. Kerberos mode

This mode is only available if you deploy the connector on a Windows machine. It allows Integrated Windows Authentication (i.e. a user plugged into a domain-joined network wouldn't have to enter the password at all). Notice that when enabling this you would have to enter the IP address ranges that will be using Kerberos. These are the IP addresses of the proxy your company is connecting through to Auth0.

##5. High availability

High availability is achieved through multiple instances of the connector running simultaneously. You need to simply install the connector on another machine. On Windows, just run the __MSI__ again. When the browser opens and requests you to enter the __Ticket URL__, close the window. Open File Explorer in the location the Connector is installed on (e.g. "\Program Files\ADLDAP Connector") and copy the `certs` folder and `config.json` from a previously configured connector instance here, overwriting any content that exists.
