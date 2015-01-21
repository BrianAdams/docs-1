# High availability

The connector is a very important component, therefore we recommend a highly available deployment through redundancy: installing multiple instances of it.

If one of the instances fails either because of a network issue or hardware issue, Auth0 will redirect the login transactions to the other connector.

Having a highly available deployment also allows updating the connector with zero downtime.

## Instructions

1. Install the connector as explained [here](@@env.BASE_URL@@/connector/install).
2. Make sure all steps are complete and the connector is up and running.
3. Copy **config.json**, **lib/profileMapper.js** and everything under the **certs** folder from:
  -  Windows: `C:\Program Files (x86)\Auth0\AD LDAP Connector\`
  -  Linux: `/opt/auth0/ad-ldap`

4. Install the connector on a second server follwing the same instructions as above. When prompted for the __Ticket URL__ close the dialog
5. On the **second server**, overwrite the default files, `config.json`, `lib/profileMapper.js` and the files in `certs` directory, with the versions of those files from the **first server** that were copied/saved in step 3 above.
6. Restart the service on the second server.

You should see now 2 connectors on the dashboard.