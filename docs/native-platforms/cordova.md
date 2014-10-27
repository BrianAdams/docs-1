---
lodash: true
---

## Cordova Tutorial

<% if (configuration.api && configuration.thirdParty) { %>

<div class="package" style="text-align: center;">
  <blockquote>
    <a href="@@base_url@@/auth0-cordova/master/create-package?path=examples/basic-sample&type=js&filePath=examples/basic-sample/www/js@@account.clientParam@@" class="btn btn-lg btn-success btn-package" style="text-transform: uppercase; color: white">
      <span style="display: block">Download a Seed project</span>
      <% if (account.userName) { %>
      <span class="smaller" style="display:block; font-size: 11px">with your Auth0 API Keys already set and configured</span>
      <% } %>
    </a>
  </blockquote>
</div>

<% } else  { %>

<div class="package" style="text-align: center;">
  <blockquote>
    <a href="@@base_url@@/auth0-cordova/master/create-package?path=examples/basic-sample&type=js&filePath=examples/basic-sample/www/js@@account.clientParam@@" class="btn btn-lg btn-success btn-package" style="text-transform: uppercase; color: white">
      <span style="display: block">Download a Seed project</span>
      <% if (account.userName) { %>
      <span class="smaller" style="display:block; font-size: 11px">with your Auth0 API Keys already set and configured</span>
      <% } %>
    </a>
  </blockquote>
</div>

<% } %>

**Otherwise, if you already have an existing application, please follow the steps below.**

### 0. Setting up the callback URL in Auth0

<div class="setup-callback">
<p>Go to the <a href="@@uiAppSettingsURL@@" target="_new">Application Settings</a> section on Auth0 Admin app and make sure that <b>App Callbacks URLs</b> has the following value:</p>

<pre><code>https://@@account.namespace@@/mobile</pre></code>

<p>If you'd also want to test your application with Ionic Serve, then add your localhost url as another <b>App Callback URL<b></p>
</div>

### 1. Add `InAppBrowser` plugin

You must install the `InAppBrowser` plugin from Cordova to be able to show the Login popup. For that, just run the following command:

````bash
cordova plugin add org.apache.cordova.inappbrowser
```

and then add the following configuration to the `config.xml` file:

````xml
<feature name="InAppBrowser">
  <param name="ios-package" value="CDVInAppBrowser" />
  <param name="android-package" value="org.apache.cordova.inappbrowser.InAppBrowser" />
</feature>
```

### 2. Follow the guide specific to the FrontEnd technology you're using

Now, you can just follow the tutorial for the FrontEnd technology that you're using. We currently support applications using [jQuery](@@base_url@@/new/client-platforms/jquery), [AngularJS](@@base_url@@/new/client-platforms/angularjs) and [Vanilla JS](@@base_url@@/new/client-platforms/vanillajs).

> **Warning**: Cordova doesn't support getting dependencies from a CDN, so you're going to have to download the JS and CSS dependencies locally and then point to the downloaded files.

> **Warning**: You must use `popup` mode when configuring an application with Cordova. (All available guides currently do that by default)

### 3. Sit back and relax

Now it's time to sit back, relax and open a beer. You've implemented Login and Signup with Auth0 and Cordova.

### Troubleshooting 

#### Command failed with exit code 65 when running ionic build

This means that the `InAppBrowser` plugin wasn't installed successfully by Cordova. Try any of the followings to fix this.

* Reinstall the `InAppBrowser` plugin

````bash
ionic plugin remove org.apache.cordova.inappbrowser
ionic plugin add org.apache.cordova.inappbrowser
```
* Remove the platform and re add it

````bash
ionic platform remove ios
ionic platform add ios
```

* Copy the contents from the plugin to the platform plugins

````bash
cp plugins/org.apache.cordova.inappbrowser/src/ios/* platforms/ios/[yourAppName]/Plugins/org.apache.cordova.inappbrowser/
```

#### Get a blank page with an OK after signin

This means that the `InAppBrowser` plugin wasn't installed successfully by Cordova. See the previous section to learn how to solve this.
