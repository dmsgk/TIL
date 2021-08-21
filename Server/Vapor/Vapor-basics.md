# Vapor

Swift로 사용할 수 있는, 서버사이드 프레임워크

## **Basics- 1. Routing**

**라우팅**([영어](https://ko.wikipedia.org/wiki/영어): routing)은 어떤 [네트워크](https://ko.wikipedia.org/wiki/네트워크) 안에서 통신 데이터를 보낼 때 최적의 경로를 선택하는 과정이다. 최적의 경로는 주어진 데이터를 가장 짧은 거리로 또는 가장 적은 시간 안에 전송할 수 있는 경로다.

### **HTTP Method**

[HTTP Method](https://www.notion.so/fbebe55a743a4ffa9ab1fe2a35701cd1)

### **Router Methods**

Let's take a look at how this request could be handled in Vapor.

```swift
app.get("hello", "vapor") { req in
    return "Hello, vapor!"
}
```

With this route registered, the example HTTP request from above will result in the following HTTP response.

```
HTTP/1.1 200 OK
content-length: 13
content-type: text/plain; charset=utf-8

Hello, vapor!
```

## **Fluent**

- ORM Framework for Swift

## Controllers

Controllers are a great way to organize your code. They are collections of methods that accept a request and return a response.

## Overview

Let's take a look at an example controller.

```swift
import Vapor

struct TodosController: RouteCollection {
    func boot(routes: RoutesBuilder) throws {
        let todos = routes.grouped("todos")
        todos.get(use: index)
        todos.post(use: create)

        todos.group(":id") { todo in
            todo.get(use: show)
            todo.put(use: update)
            todo.delete(use: delete)
        }
    }

    func index(req: Request) throws -> String {
        // ...
    }

    func create(req: Request) throws -> String {
        // ...
    }

    func show(req: Request) throws -> String {
        guard let id = req.parameters.get("id") else {
            throw Abort(.internalServerError)
        }
        // ...
    }

    func update(req: Request) throws -> String {
        guard let id = req.parameters.get("id") else {
            throw Abort(.internalServerError)
        }
        // ...
    }

    func delete(req: Request) throws -> String {
        guard let id = req.parameters.get("id") else {
            throw Abort(.internalServerError)
        }
        // ...
    }
}
```

Controller methods should always accept a `Request` and return something `ResponseEncodable`.

**Note**

[EventLoopFuture](https://docs.vapor.codes/4.0/async/) whose expectation is `ResponseEncodable` (i.e, `EventLoopFuture<String>`) is also `ResponseEncodable`.

Finally you need to register the controller in `routes.swift`:

```swift
try app.register(collection: TodosController())
```

To conform the struct to the protocol, you have to implement a single function:

```swift
func boot(routes: RouteBuilder)throws {}
```

This function is the equivalent of the `routes(_ app: Application) throws` function of the `routes.swift` file. It’s logic, because the `routes` function is our main router, and a collection is like a sub-router, we need so an entry point like a normal router.

Now, because the collection is like a router, you can use the boot function exactly the same way as the routes function of the routes.swift file.

## Middleware

Middleware는 클라이언트와 Vapor의 route handler 사이의 logic chain을 의미

route handler에 가기 전 들어오는 요청과 수행된 응답이 클라이언트에 가기 전에 일정한 연산을 할 수 있게 한다.

### Configuration

Middleware can be registered globally (on every route) in `configure(_:)` using `app.middleware`.

```swift
app.middleware.use(MyMiddleware())
```

You can also add middleware to individual routes using route groups.

```swift
// 이 방식 채택

let group = app.grouped(MyMiddleware())
group.get("foo") { req in
    // This request has passed through MyMiddleware.
}
```

### Order

- 순서가 중요함
- The order in which middleware are added is important. Requests coming into your application will go through the middleware in the order they are added. Responses leaving your application will go back through the middleware in reverse order. Route-specific middleware always runs after application middleware. Take the following example:

```swift
app.middleware.use(MiddlewareA())
app.middleware.use(MiddlewareB())

app.group(MiddlewareC()) {
    $0.get("hello") { req in 
        "Hello, middleware."
    }
}
// 순서는 다음과 같다. 
// Request → A → B → C → Handler → C → B → A → Response
```

Using the example mentioned above, create a middleware to block access to the user if they're not an admin:

```swift
import Vapor

struct EnsureAdminUserMiddleware: Middleware {

   func respond(to request: Request, chainingTo next: Responder) -> EventLoopFuture<Response> {

    guard let user = request.auth.get(User.self), user.role == .admin else {
        return request.eventLoop.future(error: Abort(.unauthorized))
    }

    return next.respond(to: request)
    }

}
```

## Join

Query builder's `join` method allows you to include another model's fields in your result set. More than one model can be joined to your query.

```swift
// Fetches all planets with a star named Sun.
Planet.query(on: database)
    .join(Star.self, on: \\Planet.$star.$id == \\Star.$id)
    .filter(Star.self, \\.$name == "Sun")
    .all()
```

The `on` parameter accepts an equality expression between two fields. One of the fields must already exist in the current result set. The other field must exist on the model being joined. These fields must have the same value type.

Most query builder methods, like `filter` and `sort`, support joined models. If a method supports joined models, it will accept the joined model type as the first parameter.

그러나 키 이름이 다르다면 에러가 난다. 이럴 때는 vapor의 fluent의 relations를 활용해 외래키를 처리해야 한다. 

------

### parent - child ( one to one)

### parent - children ( one to many)

### Siblings (Many-to-many)

`@Parent` annotation : 다른 모델의 id를 가지게 된다.

```swift
final class Planet: Model {
    // Example of a parent relation.
    @Parent(key: "star_id")
    var star: Star
}
```

------

```swift
// Models/Habit.swift
@Parent(key : "user_id")
    var user : User

// ...
init(id: UUID? = nil, habit_name: String, alarm_time: Date, makepublic : Bool, user_id: UUID) {
        self.id = id
        self.habit_name = habit_name
        self.alarm_time = alarm_time
        self.makepublic = makepublic
        self.$user.id = user_id
//user.swift
@Children(for: \\.$user)
        var habits: [Habit]
```

> Join과 Relation의 차이
>
> if we want to do a filter or order on the parent table field then better go with join. We won’t be able to do the filter or order on the relation table using the relation approach, but we can do it with the join:

### Eager Load

Now that the relation is complete, you can use the `with` method on the query builder to automatically fetch and serialize the galaxy-star relation.

```swift
app.get("galaxies") { req in
    Galaxy.query(on: req.db).with(\\.$stars).all()
}
```

### Nested Eager Load

```swift
Planet.query(on: database).with(\\.$star) { star in
    star.with(\\.$galaxy)
}.all().map { planets in
    for planet in planets {
        // `star.galaxy` is accessible synchronously here 
        // since it has been eager loaded.
        print(planet.star.galaxy.name)
    }
}
```

The query builder's `with` method allows you to eager load relations on the model being queried. However, you can also eager load relations on related models.

The `with` method accepts an optional closure as a second parameter. This closure accepts an eager load builder for the chosen relation. There is no limit to how deeply eager loading can be nested.



```swift
func getAllHandler(req: Request) throws -> EventLoopFuture<[User]> {
        return User.query(on: req.db)
            .with(\.$habits) { habit in
                habit.with(\.$checklist).with(\.$donelist)
            }
            .all()
    }
```

