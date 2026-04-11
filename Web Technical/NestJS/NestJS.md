---
Created: 2025-03-15T14:32
Class: Personal-project
Type: Back-end
Materials:
  - https://youtu.be/sFnAHC9lLaw
  - https://docs.nestjs.com/
Reviewed: false
Edited: 2025-05-10T14:47
---
# Introduce

> [!info] Documentation | NestJS - A progressive Node.js framework  
> Nest is a framework for building efficient, scalable Node.  
> [https://docs.nestjs.com/](https://docs.nestjs.com/)  

> **NestJS** is a framework for building [[NodeJS]] server-side applications.

Using progressive [[JavaScript]] with fully [[TypeScript]] supports and combines of **OOP** _(Object Oriented Programming)_ and **FP** _(Functional Programming)_

# Decorator

[[What is a Decorator, Really]]

---

# Nest CLI

**Nest** provides rich **CLI** commands to create module

```Shell
npx nest g module [name] 
```

```Shell
npx nest g controller [name]
```

Or create a full CRUD resource

```Shell
npx nest g resource [name]
```

  

![[Web Technical/NestJS/attachments/image.png|image.png]]

Example of “resume” resource

1. class `cl`
2. controller `co`
3. decorator `d`
4. exception `e`
5. filter `f`
6. gateway `ga`
7. guard `gu`
8. interceptor `i`
9. middleware `mi`
10. module `mo`
11. pipe `pi`
12. provider `pr`
13. service `s`

---

# Controllers

Controllers in Nest are responsible for handling incoming requests and returning responses to the client.

```TypeScript
@Controller('songs')
export class SongController {}
```

With the decorator `@Controller` , it’s basically creating a “songs” route.

---

# Provider

Providers in Nest are used to create services, factories, helpers and more that can be inject into a

```TypeScript
@Injectable()
export class SongProvider {
	constructor(private readonly songService: SongService) {}
}
```

More will be mentioned in .

---

# Module

A Nest application is organized to modules. The module syntax are similar with modules in ==**Angular**==.

A module in Nest is a class with a `@Module()` decorator.

The `@Module()` decorator takes a single of object parameter that describe the module using these properties:

|Property|Description|
|---|---|
|`components`|The components to be instantiated that my be shared across this mod to be available to other modules|
|`controllers`|The controllers that created by this modules|
|`imports`|The list of modules to import that export components that are required|
|`exports`|The list of components from this module that can be available for other modules|

An example application, the root Module is named `AppModule` and the application is split up into a number of sub-modules that handle the major parts of the application.

```TypeScript
@Module({
	components: [],
	controllers: [],
	imports: [
		DatabaseModule,
		AuthenticationModule.forRoot('jwt'),
		UserModule,
		EntryModule,
		CommentModule,
		UserGatewayModule,
		CommentGatewayModule
	],
	exports: [],
})
export class AppModule implements NestModule {}
```

The root module in the application doesn’t need to have any exports since no other modules import it.

The root module also doesn’t have any components or controllers, as these are all organized within the sub-modules they are related to.

```TypeScript
@Module({
	components: [entryProvider, EntryService],
	controllers: [EntryController],
	imports: [],
	exports: [EntryService],
})
export class EntryModule implements NestModule {}
```

> [!important] Modules in **Nest** are ==singletons== by default

  

---

# Dependency injection

**Dependency injection (DI)** is a technique of supplying dependent object, such as a ==module== or ==component==, with a dependency like a ==service==. It is when an object **receives** the instances of other objects it depends on, rather than **creating them itself**

> [!important] Don’t create your dependency, let’s someone give it to you.

```TypeScript
class Service {
  private db = new Database(); // tightly coupled
}

// ❌ This class directly creates an instance of Database

// ❌ Hard to test with a mock

// ❌ Hard to replace Database with something else
```

```TypeScript
class Service {
  constructor(private db: Database) {} // dependency is injected
}

// ✅ You pass the Database instance from outside

// ✅ Easy to mock or replace with another implementation

// ✅ Encourages interfaces, not concrete classes
```

Here is an example of injecting a **UsersRepository** into the constructor of **UsersService**, thereby ==providing access== to “Users Database” repository from inside **UsersService.**

```TypeScript
@Injectable()
export class UserService implements IUserService {
	constructor(@Inject('UserRepository') private readonly UserRepository: typeof User) { }
}
```

In turn this **UsersService** will be injected into the **UsersController** in the `src/users/users.controller.ts` file, which will provide access to the **UsersService** from the routes that point to this controller.

---

# Authentication

Authentication is one of the most important aspect of developing. As a developer, we always want to make sure that users can only access to the resource in their permission.

[[Keycloak]]

---

# ORM

**Object-Relational Mapping** is one of the most important concepts when dealing with communication between server and database.

It provides a mapping between object in memory (class) with record in a relational database.

This allow to create a **Data Transfer Object (DTO)** that knows how to write objects stored in memory to the database, and also read the record results from **SQL** or another query language.

## Related

- [[NodeJS]]
- [[TypeScript]]
- [[Express framework]]