---
name: lint-oop
---

Review the code I point you to (or the current branch diff if I don't) for the smells below.

For each finding, give:
- Smell name
- File and line
- Before/after using the real code
- What the change costs (new classes, migrations, callers to update)

Order findings by impact.

## Smells

### 1. Meaning in data structures
```ruby
# before
account_id, sub_id = key.split(":")

# after
AccountKey = Data.define(:account_id, :sub_id) do
  def self.parse(key) = new(*key.split(":"))
end

AccountKey.parse(key).sub_id
```

```ruby
# before
date, reference, amount = row[0], row[1], row[2]

# after
BankFileRow = Data.define(:date, :reference, :amount) do
  def self.from_row(row) = new(*row.first(3))
end

BankFileRow.from_row(row).amount
```

### 2. Hash used as a record
```ruby
# before
payment = { amount: 100, currency: "USD", direction: "credit" }
payment[:amount] * rate

# after
Payment = Data.define(:amount, :currency, :direction)
payment = Payment.new(amount: 100, currency: "USD", direction: "credit")
payment.amount * rate
```

### 3. Values that travel together
```ruby
# before
def convert(amount, currency, rate) = ...
def format(amount, currency) = ...

# after
Money = Data.define(:amount, :currency) do
  def convert(rate) = ...
  def format = ...
end
```

### 4. Locals passed between private helpers
```ruby
# before
def reconcile(payment, file, date)
  match(payment, file, date)
  record(payment, file, date)
end

# after
class Reconciliation
  def initialize(payment:, file:, date:)
    @payment = payment
    @file = file
    @date = date
  end

  def call
    match
    record
  end
end
```

### 5. Branching on a type value
```ruby
# before
class Payment
  def fee = payment_type == "ach" ? 25 : 1500
  def cutoff_time = payment_type == "ach" ? "16:00" : "17:30"
end

# after
class AchPayment < Payment
  def fee = 25
  def cutoff_time = "16:00"
end

class WirePayment < Payment
  def fee = 1500
  def cutoff_time = "17:30"
end
```

### 6. Branching on class
```ruby
# before
case record
when Payment then record.amount
when Refund  then -record.amount
end

# after
class Payment
  def signed_amount = amount
end

class Refund
  def signed_amount = -amount
end

record.signed_amount
```

### 7. Feature envy
```ruby
# before
def fee_for(payment)
  payment.amount * payment.rate + payment.fixed_fee
end

# after
class Payment
  def fee = amount * rate + fixed_fee
end
```

### 8. Tell, Don't Ask
```ruby
# before
if account.balance >= amount && !account.frozen?
  account.balance -= amount
end

# after
class Account
  def withdraw(amount)
    return if frozen? || balance < amount

    self.balance -= amount
  end
end

account.withdraw(amount)
```

### 9. Long call chains
```ruby
# before
payment.counterparty.account.routing_details.first.number

# after
class Counterparty
  def routing_number = account.routing_details.first.number
end

payment.counterparty.routing_number
```

### 10. Scattered `nil` checks
```ruby
# before
name = user ? user.name : "Unknown"
email = user ? user.email : nil

# after
class GuestUser
  def name = "Unknown"
  def email = nil
end

user ||= GuestUser.new
user.name
```
