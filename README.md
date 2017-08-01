<h1 align="center"><br><img src="https://user-images.githubusercontent.com/904724/28823994-706e5628-76c0-11e7-937c-3ae6cc83b305.png" alt="Imperium Logo"/><br><br></h1>

> Imperium is a node.js module to control your user's authorizations (ACL).

## Installation

```
npm install --save imperium
```

## Usage

```js
const Imperium = require('imperium')

const imperium = Imperium(/* options */)

// User roles
imperium.addRoles([
  'admin',
  'user'
])

// List of user actions
imperium.addActions([
  'manageUser',
  'seeUser'
])

// Define user permissions
imperium.role('user').can([
  // '@' means itself
  { action: 'manageUser', user: '@' },
  { action: 'seeUser', user: '@' }
])

// Define admin permissions
imperium.role('admin').is('user', { user: '*' })
// '*' means all, so admin will be able to manage and see all users

// Use imperium.check(...) to secure the route
app.put('/users/:id', imperium.check([{ action: 'manageUser', user: ':id' }]), updateUser)
```

## API

### Imperium(options)
