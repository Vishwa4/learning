### Why ruby on rails

1. `Rapid Development`
   Rails is designed to enable developers to create applications quickly. It emphasizes **convention over configuration**, meaning you spend less time setting up and more time building features.

2. `Full-Stack Framework`
   Rails is a **full-stack framework**, covering both frontend and backend development. It includes tools to handle databases, views, and application logic, streamlining the entire development process.

3. `DRY Principle`
   Rails adheres to the **Don’t Repeat Yourself (DRY)** principle, which reduces code duplication, making applications more maintainable and less prone to errors.

4. `ActiveRecord ORM`
   Rails uses **ActiveRecord**, a powerful object-relational mapping (ORM) tool, to interact with databases. It simplifies database operations, enabling developers to use Ruby code to manage queries without needing raw SQL.

5. `Built-In Testing Tools`
   Rails includes robust testing tools like RSpec and Minitest, which encourage developers to write tests from the beginning, resulting in more reliable applications.

6. `Vibrant Community and Ecosystem`
   Rails has a **large, supportive community** that contributes to its ecosystem. Developers can leverage a wealth of **gems** (pre-built libraries) to add functionality without reinventing the wheel.

7. `Scalability`
   While not as inherently scalable as some alternatives, Rails supports scalability through optimized configurations, caching, and microservices, making it suitable for startups and enterprises alike.

8. `Mature Framework`
   Rails has been around since 2004 and has proven its reliability in powering applications like **GitHub**, **Shopify**, **Airbnb**, and **Basecamp**.

9. `Productivity`
   Developers often cite Ruby on Rails as one of the most **developer-friendly frameworks**. Its intuitive syntax and built-in tools reduce frustration and improve efficiency.

10. `Ideal for Startups`
    Rails is an excellent choice for startups due to its speed of development and the ability to pivot quickly. This is why many tech startups choose Rails for their Minimum Viable Products (MVPs).

### what is the principles of rails


1. Convention over Configuration (CoC)

Rails assumes a set of conventions for structuring your code, which reduces the need for extensive configuration files. By following these conventions, developers can focus on building features rather than spending time on setup.

Example:

    A model named User automatically maps to a database table named users.
    The default directory structure enforces organization, like placing views in the app/views folder.


2. Don’t Repeat Yourself (DRY)

Rails encourages reusability of code to eliminate redundancy. Shared logic can be encapsulated in modules, helpers, or partials, ensuring cleaner and more maintainable code.

Example:

    Shared layouts and partials for HTML templates.
    Reusing methods across controllers using modules.


3. RESTful Design

Rails encourages building applications with RESTful architecture, where routes map to specific controller actions using standard HTTP methods (GET, POST, PUT, DELETE). This leads to clean and predictable URLs.

Example:

    GET /users maps to the index action (list all users).
    POST /users maps to the create action (create a new user).


4. Model-View-Controller (MVC) Architecture

Rails follows the MVC pattern, separating an application into three interconnected layers:

    Model: Manages data and business logic (interacts with the database).
    View: Handles the presentation layer (HTML, CSS, JavaScript).
    Controller: Processes input, handles user requests, and updates the view.

This separation ensures a modular and organized codebase.


5. Active Record Pattern

Rails uses the Active Record design pattern for database interaction. Each model class corresponds to a database table, and instances of the class represent rows in the table. This abstraction simplifies database operations.


6. The Rails Way

Rails emphasizes developer happiness and productivity by promoting conventions and tools that simplify development. Developers can focus on writing meaningful code rather than managing repetitive tasks.

Features:

    Generators to scaffold resources.
    Built-in testing frameworks.

7. Automated Testing

Rails includes built-in support for writing and running tests, encouraging a test-driven development (TDD) approach. Tools like Minitest and external gems like RSpec integrate seamlessly.


8. Security by Default

Rails provides built-in mechanisms to prevent common web vulnerabilities, such as:

    SQL Injection: Through parameterized queries.
    Cross-Site Scripting (XSS): By automatically escaping HTML in views.
    Cross-Site Request Forgery (CSRF): By including authenticity tokens in forms.


9. Scalability and Modularity

Rails supports modularity by allowing developers to use plugins and engines to extend its functionality. Additionally, Rails applications can be scaled using strategies like caching and background job processing.


10. Optimized for Agile Development

Rails promotes quick iterations and adaptability, making it ideal for Agile methodologies. Features like scaffolding and migrations speed up development and allow for continuous changes.

### Difference between include, extend and prepend  
In Ruby, include, extend, and prepend are used with modules to add behavior to classes.
They are also known as Module Mixins. <br>
-> **Include** <br>
`include` adds a module’s methods as instance methods of a class.
That means objects of the class can use those methods. <br>

Example:-
```Ruby
module Greeting
 def say_hello
  puts "Hello"
 end
end

class Person
 include Greeting
end

p = Person.new
p.say_hello
```
-> **Extend** <br>
`extend` adds module methods as class methods. That means the class itself can call the method, not the object. <br>

Example:-
```Ruby
module Greeting
  def say_hello
    puts "Hello"
  end
end

class Person
  extend Greeting
end

Person.say_hello
```
-> **prepend** <br>
`prepend` inserts the module before the class in the method lookup chain.
Means module’s methods as instance methods of a class but module methods will be prioritized <br>

Example :-
```Ruby
module Greeting
  def say_hello
    puts "Hello from module"
  end
end

class Person
  prepend Greeting

  def say_hello
    puts "Hello from class"
  end
end

Person.new.say_hello
```
### Difference between  require and load
In Ruby, require and load are used to import external Ruby files, but they behave differently.

They are generally known as file loading mechanisms or code loading methods in Ruby.

-> **require** <br>
Loads a file only once during program execution. <br>
Ruby keeps track of loaded files in a special array called:
`$LOADED_FEATURES
`
So if the same file is required again, Ruby will not load it again.

-> **load** <br>
Loads the file every time it is called. <br>
Ruby does not check $LOADED_FEATURES.

### Method Lookup Sequence in Ruby
1. Object's singleton class (Eigenclass)
2. Class
3. Included modules (in reverse order)
4. Superclass
5. Modules included in superclass
6. Object
7. Kernel
8. BasicObject
- `super` calls the next method in the lookup chain.
- `ClassName.ancestors` can be used to See the Method Lookup Chain <br>
Example:
```Ruby
class Child < Parent
  include A
end

puts Child.ancestors

Output:

  [Child, A, Parent, Object, Kernel, BasicObject]
```

### Access Modifiers
In Ruby, Access Modifiers control who can access methods of a class. <br>
Ruby has 3 access modifiers:

1. public 
2. private 
3. protected

-> **Public** <br>
Public methods can be called from anywhere.
This is the default access modifier in Ruby.

-> **private** <br>
Private methods can only be called inside the same class.
They cannot be called with an explicit receiver.

-> **Protected** <br>
protected in Ruby is often confusing, so let's break it down very simply.

A protected method:
* Cannot be called from outside the class
* Can be called by another object of the same class

So objects of the same class can access each other's protected methods.

```Ruby
class Person
  def initialize(age)
    @age = age
  end

  def older_than?(other_person)
    age > other_person.age
  end

  protected

  def age
    @age
  end
end

Now create objects:

p1 = Person.new(30)
p2 = Person.new(25)

p1.older_than?(p2)

Output:

true
```
### Struct vs OpenStruct in Ruby
Struct and OpenStruct in Ruby are both used to create objects for storing data, but they differ in flexibility and performance.

-> **Struct**

* Struct defines attributes in advance when the class is created.
* It behaves like a lightweight class with predefined fields.
* It is faster and more memory efficient.

Example:
```Ruby
Person = Struct.new(:name, :age)
person = Person.new("Sai", 28)
person.name # => "Sai"
```
-> **OpenStruct**

* OpenStruct allows attributes to be added dynamically at runtime.
* It internally stores values in a hash and creates methods dynamically.
* Because of this dynamic behavior, it is slower and consumes more memory.

Example:
```Ruby
require 'ostruct'

person = OpenStruct.new
person.name = "Sai"
person.age = 28
person.city = "Bangalore"
```
### difference between symbolize_keys and deep_symbolize_keys:
-> **symbolize_keys**

Scope: Only converts the top-level keys of a hash to symbols.
Does not affect nested hashes.

Example:
```Ruby
hash = {
"name" => "John",
"details" => { "age" => 30, "city" => "Dublin" }
}

symbolized = hash.symbolize_keys

puts symbolized
# => {:name=>"John", "details"=>{"age"=>30, "city"=>"Dublin"}}
```

-> **deep_symbolize_keys**

Scope: Converts all keys — including those inside nested hashes — into symbols.
It’s a recursive version of symbolize_keys.

Example:
```Ruby
hash = {
"name" => "John",
"details" => { "age" => 30, "city" => "Dublin" }
}

deep_symbolized = hash.deep_symbolize_keys

puts deep_symbolized
# => {:name=>"John", :details=>{:age=>30, :city=>"Dublin"}}
```

### difference between find_each and each
→ **each** <br>
Loads all records at once into memory.
Then iterates over them.
Example
```Ruby
User.all.each do |user|
puts user.name
end
🔎 What happens internally?
users = User.all   # Executes SELECT * FROM users
# All records loaded into memory
users.each { ... }
🚨 Problem

If you have:

1,000 records → OK

1,000,000 records → ❌ High memory usage

📌 Use each when:

Dataset is small

You need ordering, includes, or complex queries

```

-> **find_each** <br>

Loads records in batches (default: 1000)
Processes one batch at a time <br>
Very memory efficient

Example

```Ruby
User.find_each do |user|
   puts user.name
end
puts user.name
end
🔎 What happens internally?
SELECT * FROM users WHERE id > 0 ORDER BY id ASC LIMIT 1000;
SELECT * FROM users WHERE id > 1000 ORDER BY id ASC LIMIT 1000;
SELECT * FROM users WHERE id > 2000 ORDER BY id ASC LIMIT 1000;


# customize the batch size for heavy process
User.find_each(batch_size: 500) do |user|
end
```

### preload and includes <br>

In Ruby on Rails (ActiveRecord), both preload and includes are used to solve the N+1 query problem, but they behave differently in how they generate SQL.

- `preload` Always loads associations using separate queries
- `includes` is Smart loading (may use JOIN or separate queries)

### Redirect & render <br>
In Ruby on Rails, redirect and render are two methods used in controllers to handle how the response is sent back to the client, but they serve different purposes and work differently.
1. redirect_to

The redirect_to method is used to send an HTTP redirect response to the client. This instructs the client (usually the browser) to make a new request to a different URL.

2. render

The render method is used to render a view template or return data directly in the HTTP response. It does not involve a new HTTP request.

### Scope vs instance method
→ A scope is a reusable query used to filter records from the database. <br>
→ An instance method works on a single record.
```Ruby
class User < ApplicationRecord
  scope :active, -> { where(active: true) }

  def full_name
     "#{first_name} #{last_name}"
  end
end
```
### class_eval vs instance_eval
In Ruby, class_eval and instance_eval are used for metaprogramming, meaning they allow you to modify classes or objects dynamically at runtime.

**using instance_eval**
```Ruby
person = Person.new
# instance method
person.instance_eval do
  def greet
    "Hello from instance"
  end
end

person.greet

# class method
Person.instance_eval do
   def greet
      "Hello from class method"
   end
end

Person.greet
```
**using class_eval**
```Ruby
class Person
end

# instance methods
Person.class_eval do
  def greet
    "Hello"
  end
end

p = Person.new
p.greet

# class methods
Person.class_eval do
   def self.greet
      "Hello from class method"
   end
end

Person.greet
```

### Callbacks in Rails
Callbacks in Rails are methods that get called at certain points in an object's lifecycle. They allow you to trigger logic before or after certain events, such as creating, updating, or deleting records. <br>
-> **callbacks are basically divided into 3 categories:**
1. `before_*` - called before an action (e.g., before_save, before_create)
2. `after_*` - called after an action (e.g., after_save, after_create)
3. `around_*` - wraps around an action (e.g., around_save)

-> **They can be used along with different events like:** 
- `save` - called when saving a record (both create and update)
- `create` - called only when creating a new record
- `update` - called only when updating an existing record
- `destroy` - called when deleting a record
- `validation` - called during the validation process
- `initialize` - called when a new object is instantiated supports only **after_initialize**
- `commit` - called after a transaction is committed supports only **after_commit**
- `rollback` - called after a transaction is rolled back supports only **after_rollback**
- `find` - called when finding a record supports only **after_find**
- `touch` - called when a record is touched (updated_at is updated) supports only **after_touch**

-> **Order of callbacks:**<br>
**<u>For create:-</u>**  <br>
after_initialize <br>
before_validation <br>
after_validation <br>
before_save <br>
around_save (before yield) <br>
before_create <br>
around_create (before yield) <br>
--- DB INSERT --- <br>
around_create (after yield) <br>
after_create <br>
around_save (after yield) <br>
after_save <br>
after_commit <br>

**<u>For update:-</u>** <br>
before_validation <br>
after_validation <br>
before_save  <br>
around_save (before yield) <br>
before_update <br>
around_update (before yield)  <br>
--- DB UPDATE --- <br>
around_update (after yield) <br>
after_update <br>
around_save (after yield) <br>
after_save <br>
after_commit <br>

**<u>For destroy:-</u>** <br>
before_destroy  <br>
around_destroy (before yield) <br>
--- DB DELETE --- <br>
around_destroy (after yield) <br>
after_destroy <br>
after_commit <br>

