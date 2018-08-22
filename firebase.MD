#Basic Firebase set-up

##Firebase Install

$ npm install angularfire2@4.0.0-rc.0 firebase@^3.6.6 --save
          -or-
  yarn add angularfire2@4.0.0-rc.0 firebase@^3.6.6 --save

—-

##make api call##

src/app/api-keys.ts

export const masterFirebaseConfig = {
    apiKey: "xxxx",
    authDomain: "xxxx.firebaseapp.com",
    databaseURL: "https://xxxx.firebaseio.com",
    storageBucket: "xxxx.appspot.com",
    messagingSenderId: "xxxx"
  };

—
##add to git ignore*

.gitignore

...
##Firebase credentials
/src/app/api-keys.ts

—-

##import to app.module

src/app/app.module.ts

…

import { masterFirebaseConfig } from './api-keys';
import { AngularFireModule } from 'angularfire2';
import { AngularFireDatabaseModule } from 'angularfire2/database';

export const firebaseConfig = {
  apiKey: masterFirebaseConfig.apiKey,
  authDomain: masterFirebaseConfig.authDomain,
  databaseURL: masterFirebaseConfig.databaseURL,
  storageBucket: masterFirebaseConfig.storageBucket
};

@NgModule({
  declarations: [
    AppComponent,
    WelcomeComponent,
    AboutComponent,
    MarketplaceComponent,
    AlbumDetailComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule,
    routing,
    AngularFireModule.initializeApp(firebaseConfig),
    AngularFireDatabaseModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

—

##adjust rules

Finally, we just need to tell our Firebase database that we'd like to allow outside applications to read and write to it.
* We'll visit our Firebase Console once more, and select our project's name from the list.
* Then, we'll visit the Database area by selecting the Database option from the navbar on the left-hand side.
* Near the top of the page, there should be a blue navbar reading Realtime Database. Below this, select the option that reads RULES.
* Change both the ".read", and ".write" properties here to "true", as seen below, then click Publish:
{
  "rules": {
    ".read": "true",
    ".write": "true"
  }
}
