# Basic Firebase set-up

## Firebase Install

$ npm install angularfire2@4.0.0-rc.0 firebase@^3.6.6 --save
          -or-
  yarn add angularfire2@4.0.0-rc.0 firebase@^3.6.6 --save

==============================

## make api call##

**src/app/api-keys.ts**

export const masterFirebaseConfig = {
    apiKey: "xxxx",
    authDomain: "xxxx.firebaseapp.com",
    databaseURL: "https://xxxx.firebaseio.com",
    storageBucket: "xxxx.appspot.com",
    messagingSenderId: "xxxx"
  };

==============================
## add to git ignore*

**.gitignore**

...
## Firebase credentials
/src/app/api-keys.ts

==============================

## import to app.module

**src/app/app.module.ts**

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

==============================

## adjust rules

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

==============================

# DEPLOYMENT!!

$ ng build --env=prod

==============================

$ npm install -g firebase-tools

or 

yarn global add firebase-tools

==============================

$ firebase login

$ firebase init

You're about to initialize a Firebase project in this directory:

  /Users/student/Desktop/your-project-directory-name

? What Firebase CLI features do you want to setup for this folder?
❯◉ Database: Deploy Firebase Realtime Database Rules
 ◉ Hosting: Configure and deploy Firebase Hosting sites

 ...

==============================

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

? What Firebase project do you want to associate as default? (Use arrow keys)
your-firebase-project-names-here


Your current Firebase projects will be listed. Using the arrow keys to navigate, select the one that corresponds to the project you're deploying. If this project doesn't have a Firebase a database, select the project you created a moment ago. If it does, select the project containing its database.

==============================

## Next, create a file in the top-level of your project directory named database.rules.json. Insert the following into it:

**database.rules.json**
{
  "rules": {
    ".read": true,
    ".write": true
  }
}

==============================

**firebase.json**
{
  "database": {
    "rules": "database.rules.json"
  },
  "hosting": {
    "public": "dist"
  }
}

==============================

$ firebase deploy

:fire: :fire: :fire: