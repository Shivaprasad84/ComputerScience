# Typescript Stuff

## Exclusive OR

```typescript
  interface ThingOne {
    shirtColor: string;
    hairColor?: never;
  }

  interface ThingTwo {
    shirtColor?: never;
    hairColor: string;
  }

  type ExclusiveThing = ThingOne | ThingTwo;

  const x: ExclusiveThing; // x can now be assigned an object
  // having either `shirtColor` or `hairColor` and not both.

```

## Tagged Unions & Exhaustive Switch statement

```typescript
  interface NormalUser {
    type: 'normal user';
    name: string;
    age: number;
  }

  interface AdminUser {
    type: 'admin user';
    name: string;
    age: number;
    adminId: string;
  }

  let getNormalUserAccessToken: (normalUser: NormalUser) => string;

  let getAdminUserAccessToken: (adminUser: AdminUser) => string;

  type User = NormalUser | AdminUser;

  function getAccessToken(user: User): string {
    let accessToken = '';
    switch(user.type) {
      case 'normal user':
        accessToken = getNormalUserAccessToken(user);
        break;
      case 'admin user':
        accessToken = getAdminUserAccessToken(user);
        break;
      default:
        // since all possible types have been exhausted
        // `user` here would be of type `never`.
        let notPossible: never = user;
        return notPossible;
    }
    return accessToken;
  }
```

## Same thing with `intersection` type

```typescript
  type User = { name: string; age: number} & ({
    type: 'normal user'
  } | {
    type: 'admin user',
    adminId: string;
  });


  let getNormalUserAccessToken: (normalUser: User) => string;

  let getAdminUserAccessToken: (adminUser: User) => string;

  function getAccessToken(user: User): string {
    let accessToken = '';
    switch(user.type) {
      case 'normal user':
        accessToken = getNormalUserAccessToken(user);
        break;
      case 'admin user':
        accessToken = getAdminUserAccessToken(user);
        break;
      default:
        // since all possible types have been exhausted
        // `user` here would be of type `never`.
        let notPossible: never = user;
        return notPossible;
    }
    return accessToken;
  }
```

### Interfaces are extendable or mergable

```typescript
  interface User {
    name: string;
  }

  interface User {
    age: number;
  }

  const u: User = {
    name: 'Shiva',
    age: 24
  }
```
