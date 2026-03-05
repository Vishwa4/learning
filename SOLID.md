# SOLID
SOLID principles are object-oriented design principles that help you write clean, maintainable, scalable code
especially important when controllers, models, and services start growing.

S — Single Responsibility Principle (SRP) <br>
O — Open/Closed Principle (OCP) <br>
L — Liskov Substitution Principle (LSP) <br>
I — Interface Segregation Principle (ISP) <br>
D — Dependency Inversion Principle (DIP) <br>

## S — Single Responsibility Principle (SRP)
A class should have only ONE reason to change.

## O — Open/Closed Principle (OCP)
Open for extension, closed for modification. <br>
You should extend behavior without modifying existing code. <br>
In Rails, OCP is achieved using polymorphism, STI, modules, and duck typing.

Bad code:
```Ruby
class PaymentProcessor
  def process(payment)
    if payment.type == "credit_card"
      # logic
    elsif payment.type == "paypal"
      # logic
    end
  end
end
```

Good code:
```Ruby
class PaymentProcessor
 def process(payment_method)
  payment_method.pay
 end
end

class CreditCardPayment
 def pay
  # credit card logic
 end
end

class PaypalPayment
 def pay
  # paypal logic
 end
end

Now adding ApplePay makes it easy as below:

class ApplePayPayment
 def pay
  # apple pay logic
 end
end
```


## L — Liskov Substitution Principle (LSP)
- Subclasses should be replaceable with their parent class without breaking behavior. <br>
- LSP means a subclass should be able to replace its parent class without breaking the program. The child class should follow the same behavior contract as the parent. <br>

Bad Code: 
```Ruby
class Bird
 def fly
  "Flying"
 end
end

class Penguin < Bird
 def fly
  raise "Penguins can't fly"
 end
end
```
Penguin breaks parent behavior. <br>

Good Code: 
```Ruby
class Bird
end

class FlyingBird < Bird
 def fly
  "Flying"
 end
end

class Penguin < Bird
end
```
Now no broken behavior.

## I — Interface Segregation Principle (ISP)
- Clients should not depend on methods they don't use.
- ISP states that a class should not be forced to depend on methods it does not use. In Rails, we achieve this by creating small, focused modules instead of large, multi-purpose concerns.

Bad code: 
```Ruby
module Worker
  def work; end
  def eat; end
end

class Robot
  include Worker

  def work; end
  def eat
    raise "Robots don't eat"
  end
end
```
Good code: 
```Ruby
module Workable
  def work; end
end

module Eatable
  def eat; end
end

class Human
  include Workable
  include Eatable
end

class Robot
  include Workable
end
```

## D — Dependency Inversion Principle (DIP)
- High-level modules should not depend on low-level modules. Both should depend on abstractions. <BR>

Think of it like:
 You plug a charger into a wall socket.
 - You depend on the socket interface
 - You don’t care if electricity comes from:
   - Solar
   - Nuclear
   - Coal
   - Generator

You depend on abstraction (socket), not power plant.

That’s DIP.

Bad code:
```Ruby
class OrderService
  def initialize
    @gateway = StripeGateway.new
  end

  def process
    @gateway.charge
  end
end
```
Good code:

```Ruby
class OrderService
  def initialize(gateway)
    @gateway = gateway
  end

  def process
    @gateway.charge
  end
end

# Usage: 
OrderService.new(StripeGateway.new).process

# Now easily testable:
fake_gateway = double(charge: true)
OrderService.new(fake_gateway).process
```


# Interview Questions
### How do you apply SOLID in Rails?
* I keep models skinny by extracting business logic into service objects (SRP).
* I use polymorphism instead of conditionals (OCP).
* I ensure subclasses respect parent contracts (LSP).
* I split large concerns into smaller modules (ISP).
* I inject dependencies instead of tightly coupling classes (DIP).

### What is Duck Typing?

Duck typing means Ruby doesn’t check the object’s type. It only checks if the object responds to the required method. If it behaves correctly, it works. <br>
**Example**:-
```Ruby
class Dog
  def speak
    "Woof"
  end
end

class Cat
  def speak
    "Meow"
  end
end

def make_sound(animal)
  animal.speak
end

puts make_sound(Dog.new)
puts make_sound(Cat.new)
```