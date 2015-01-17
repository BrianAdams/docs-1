# Installing the AD LDAP Connector on different platforms

1.  [Install node.js v0.10](https://nodejs.org).
2.  Use the GitHub repository to download the package: <a class="download-github" href=""></a> to /tmp. Eg: <pre><code class="curl-example"></code></pre>
3.  Expand the package and install dependencies:

        mkdir /opt/auth0-adldap
        tar -xzf /tmp/adldap.tar.gz -C /opt/auth0-adldap --strip-components=1
        cd /opt/auth0-adldap

4.  Run `node server.js` and follow the steps to finish the process.
5.  Once the connector is running you will need to daemonize the connector using a tool like upstart, systemd, init.d, etc.

<script src="https://code.jquery.com/jquery-1.11.2.min.js"></script>
<script type="text/javascript">
  $.getJSON('https://cdn.auth0.com/connector/windows/latest.json', function (data) {
    // https://github.com/auth0/ad-ldap-connector/archive/v2.10.4.tar.gz
    $('.download-github')
        .attr('href', 'https://github.com/auth0/ad-ldap-connector/releases/tag/v' + data.version)
        .text('adldap-' + data.version);

    $('.curl-example')
      .text('curl -Lo /tmp/adldap.tar.gz \\\n    https://github.com/auth0/ad-ldap-connector/archive/' + data.version + '.tar.gz');
  })
</script>