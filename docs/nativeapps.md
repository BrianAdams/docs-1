# Calling APIs from Native Devices

Once the user has logged in using one of our SDKs as part of the response, you will get a [JSON Web Token](jwt) signed with the secret of that application. 

For instance, in iOS:

    [client loginAsync:self withCompletionHandler:^(BOOL authenticated) {
      // client.auth0User.IdToken <--- this is the JWT

Or using Xamarin:

    var user = await auth0.LoginAsync(this);
    // user.IdToken <--- this is the JWT

Or in Windows Phone:

    var user = await auth0.LoginAsync();
    // user.IdToken <--- this is the JWT

For other examples, look under the [Native Mobile App](/#!/native-mobile) section.