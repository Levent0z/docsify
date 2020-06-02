npm i oidc-client --save


import { enableProdMode } from '@angular/core';
enableProdMode(); // if production


## Silent Redirect
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/oidc-client/1.5.1/oidc-client.min.js"></script>
<script>
  var config = {
    userStore: new Oidc.WebStorageStateStore({ store: window.localStorage })
  };
  new Oidc.UserManager(config).signinSilentCallback()
    .catch((err) => {
        console.log(err);
    });
</script>
```

## OIDC Login Redirect
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/oidc-client/1.4.1/oidc-client.min.js"></script>
<script>
  var config = {
    userStore: new Oidc.WebStorageStateStore({ store: window.localStorage })
  };
  new Oidc.UserManager(config).signinRedirectCallback().then(() => {
    window.history.replaceState({}, window.document.title, window.location.origin);
    window.location = "/";
  }, error => {
    console.error(error);
  });
</script>
```

## APP.COMPONENT.TS
```typescript
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { AuthService } from './core/auth.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: []
})
export class AppComponent implements OnInit {  
  constructor(    
    private authService: AuthService,
    private router: Router
  ) {}

  ngOnInit() {
    if (window.location.href.indexOf('?postLogout=true') > 0) {
      this.authService.signoutRedirectCallback().then(() => {
        const url: string = this.router.url.substring(0, this.router.url.indexOf('?'));
        this.router.navigateByUrl(url);
      });
    }
  }

  login() {
    this.authService.login();
  }

  logout() {
    this.authService.logout();
  }

  isLoggedIn() {
    return this.authService.isLoggedIn();
  }

  isAdmin() {
    return this.authService.authContext && 
           this.authService.authContext.claims && 
           (this.authService.authContext.claims.find(c => c.type === 'http://schemas.microsoft.com/ws/2008/06/identity/claims/role' && c.value === 'Admin'));
  }
}
```

## AUTH.SERVICE.TS
```TypeScript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { UserManager, User, WebStorageStateStore, Log } from 'oidc-client';
import { Constants } from '../constants';
import { AuthContext } from '../model/auth-context';

@Injectable()
export class AuthService {
  private userManager: UserManager;
  private user: User;
  authContext: AuthContext;

  constructor(private httpClient: HttpClient) {
    Log.logger = console;
    const config = {
      authority: Constants.stsAuthority,
      client_id: Constants.clientId,
      redirect_uri: `${Constants.clientRoot}assets/oidc-login-redirect.html`,
      scope: 'openid projects-api profile',
      response_type: 'id_token token',
      post_logout_redirect_uri: `${Constants.clientRoot}?postLogout=true`,
      userStore: new WebStorageStateStore({ store: window.localStorage }),
      automaticSilentRenew: true,
      silent_redirect_uri: `${Constants.clientRoot}assets/silent-redirect.html`
    };
    this.userManager = new UserManager(config);

    const setUser = (user) => {
      if (user && !user.expired) {
        this.user = user;
        this.loadSecurityContext();
      }
    }
    this.userManager.getUser().then(setUser);

    this.userManager.events.addUserLoaded(args => {
      this.userManager.getUser().then(setUser);
    });
  }

  login(): Promise<any> {
    return this.userManager.signinRedirect();
  }

  logout(): Promise<any> {
    return this.userManager.signoutRedirect();
  }

  isLoggedIn(): boolean {
    return this.user && this.user.access_token && !this.user.expired;
  }

  getAccessToken(): string {
    return this.user ? this.user.access_token : '';
  }

  signoutRedirectCallback(): Promise<any> {
    return this.userManager.signoutRedirectCallback();
  }

  loadSecurityContext() {
    this.httpClient.get<AuthContext>(`${Constants.apiRoot}Account/AuthContext`).subscribe(context => {
      this.authContext = context;
    }, error => console.error(error));
  }
}
```


## STS Project

### References
IdentityModel
IdentityServer4
IdentityServer4.AspNetIdentity
Microsoft.AspNetCore.All
Microsoft.AspNetCore.AUthentication.OpenIdConnect
Microsoft.EntityFrameworkCore.Tools
Microsoft.NETCore.App
Microsoft.VisualStudio.Web.CodeGeneration.Design
Serilog
Serilog.Extensions.Logging
Serilog.Sinks.Console
Serilog.Sinks.File


