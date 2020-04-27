### Dependency Injection

Dependency injection is a technique for helping you test classes in isolation. 

It allows a class to use either its real dependency, or a double.

### Refactoring

  * Improve the design of your code
  * Learn more about the whole program you're designing
  * Define the patterns and names that make your code extensible.

### Unit vs Integration tests

If you create real objects (not doubles) in your unit tests other than that which is the subject, then you are using the Chicago style of unit testing (also called integration testing). 

London style with doubles effectively isolates the class being tested in a unit test.

```
# London Style
describe Order do
  let(:menu) { double :menu, price: '£1.00', contains?: true }
  subject(:order) { described_class.new(menu) }

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
# Chicago Style 
describe Order do
  subject(:order) { described_class.new(Menu.new) } # note real Menu class

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
```

### Law of Demeter

The Law of Demeter suggests that:

* Each object should have only limited knowledge about other units: only units "closely" related to the current unit.
* Each object should only talk to its friends; don't talk to strangers.
* Only talk to your immediate friends.
