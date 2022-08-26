# Salesforce Connected App Configuration

In order to access data hosted by Salesforce from an external app, you need to create a "Connected App".

To configure a connected app, go to Setup by clicking the cog icon (⚙️) at the top right of the Salesforce app.

In the Lightning Experience, you create a a "Connected App" in "App Manager", not "Connected Apps" setup item.

Once a Connected App is created, you can see a list of them in "Manage Connected Apps" setup item. Unfortunately, clicking on "Edit" for a list item on this page, takes you to a view that typically is not what you want.

In order to get back to the powerful settings page of a Connected APP, especially if you're configuring for Oauth, go to `App Manager` and click the **drop-down button at the far right** of your app entry. Here, you should click `Edit` in the context menu. (Instead, if you select "Manage" and then "Edit Policies", you will again find yourself in the "Manage Connected Apps" view for that app).

Make sure to:

1. Check `Enable OAuth Settings`
2. Add your `redirect_uri` (the localhost endpoint for your CLI) in `Callback URL` one line at a time.
3. Add needed scopes from the `Selected OAuth Scopes` list. For test purpose, select "Full Scope".

In addition, you may want to:

1. Check `Enable for Device Flow`
2. Uncheck `Require Secret for Web Server Flow`
3. Uncheck `Require Secret for Refresh Token Flow`

In the management page for your connected app, under `OAuth Policies` you may want to:

1. Set `Permitted Users` to `All users may self-authorize`
2. Set `IP Relaxation` to `Relax IP restrictions`

The access token timeout is configured in the `timeout` in `Session Settings` page, but the refresh token is configured in the management page. 