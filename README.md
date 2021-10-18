# nuxt-firebase

## Command

1. Register  
   Registering a dummy user
2. Login  
   Login a dummy user, must be register first
3. Logout  
   Logout a dummy user
4. Current User  
   Display current user if register and login success
5. Clear Screen  
   Just clean up output response
6. Verify Email  
   Send verification email of current user
7. Delete User  
   Delete current user from firebase auth

## Configuration

add .env to your configuration, and fill information from your console firebase auth

```env
apiKey=xxx
authDomain=xxx
projectId=xxx
storageBucket=xxx
messagingSenderId=xxx
ppId=xxx
measurementId=xxx
```

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
