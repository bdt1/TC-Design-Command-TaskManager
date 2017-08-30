# Command Pattern
* **Purpose** - to demonstrate the [command pattern](https://en.wikipedia.org/wiki/Command_pattern)

## Part 1 - Design Command Interface

### Part 1.1 - Create interface `Command`
* Create an interface named `Command`.
* The class should declare one method of `void` return type named `execute`

### Part 1.2 - Create class `Task`
* Create an abstract class named `Task`.
* `Task` has a field `isUndone` of type `boolean`.
* The class should declare a `void` method `afterExecute`.
* The class should declare a `void` method `afterUndo`.
* The class should define a `final void` method `execute`.
	* This method will call `afterExecute` if the `isUndone` field is false.
* The class should define a `final void` method `redo`.
	* This method will call `afterExecute` if the `isUndone` field is true.
* The class should define a `final void` method `undo`.
	* This method will call `afterUndo` if the `isUndone` field is false.


### Part 1.3 - Create class `TaskManager`
* Create a class `TaskManager`.
* The class should instantiate two `Stack` objects of _parameterized type_ `Task`.
	* `taskStack` - represents the tasks we would like to perform
	* `undoStack` - represents the tasks which have been undone, and have potential to be redone.
* The class should define a `performTasks` method, which iterates through the `taskStack` and invokes `execute` on each `Task` and removes it from the stack.
* The class should define a `pendTask` method, which takes an argument of a `Task` and adds it to the `taskStack` object.
* The class should define an `undo` method which removes the top element from the `taskStack` and adds it to the `undoStack`.
* The class should define a `redo` method which removes the top element from the `undoStack` and adds it to the `taskStack`.













## Part 2 - Design `BankAccount` Interface

### Part 2.1 - Create class `BankAccount`
* Create a class `BankAccount` in the `io.zipcoder.zcw_taskmanager.bankaccount` subpackage
* The class should declare a final field of type `long` named `id`.
* The class should declare a field of type `double` named `balance`.
* The class should define a getter for each of its respective fields.
* The class should define a setter for its `balance` field.
* `BankAccount` has a constructor which takes an argument of a `long` and sets it as its `id` field-value.
* The class should define a an `increaseBalance` method which takes an argument of `double` and increases the `balance` field by the respective amount.
* * The class should define a an `decreaseBalance` method which takes an argument of `double` and decrease the `balance` field by the respective amount.

### Part 2.2 - Create singleton `BankAccountManager`
* Create a class `BankAccountManager` in the `io.zipcoder.zcw_taskmanager.bankaccount` subpackage using [singleton pattern](https://github.com/Zipcoder/TC-Design-Singleton-ObjectCreator).
* The class should instantiate a _static_ field instance of type `BankAccountManager`.
* The class should instantiate a field `bankAccounts` of type `ArrayList` of parameterized type `BankAccount`.
* The class should define a private, empty, nullary constructor.
* The class should define a method `findBankAccount` which uses a `long` parameter to identify and return a `BankAccount` object with a respective `id`.
* The class should define a method `addAccount` which uses a `BankAccount` parameter to add a `BankAccount` to the `bankAccounts`
* The class should define a method `removeAccount` which uses a `BankAccount` to remove a respective `BankAccount` object `bankAccounts
* The class should overload method `removeAccount` with a `long` parameter to identify and remove a `BankAccount` object with a respective `id`.
* The class should define a method `getNumberOfAccounts` which returns the `size` of `bankAccounts`.
* The class should define a _static_ method `getInstance` which returns `instance`.

### Part 2.3 - Modify class `Task`
* The class should define a `getAccountManager` method which returns the singleton `BankAccountManager`












## Part 3 - Create concrete `Task` implementation

### Part 3.1 - Create class `TaskAccountCreate`
* Create a subclass of `Task` named `TaskAccountCreate` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` subpackage.
* The class should declare a final `id` field of type long.
* The constructor should set `id` to the current size of the composite List `bankAccounts` in `BankAccountManager`
* The class should define a method `afterExecute`.
	* Creates a new `BankAccount` with the respective `id` field.
	* Adds the `BankAccount` to the composite `bankAccounts` in `BankAccountManager`.
* The class should define a method `afterUndo` which removes a `BankAccount` from the composite `bankAccounts` in `BankAccountManager` with the respective `id` field.
* The class should define a method `getId` which returns the `id` field.

### Part 3.2 - Create class `TaskAccountDeposit`
* Create a subclass of `Task` named `TaskAccountDeposit` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` subpackage.
* The class should declare a final `dollarAmount` variable of type `double`.
* The class should declare a final `account` variable of type `BankAccount`.
* The constructor should have parameters of type `double` and `long`.
	* The `double` variable should be used to set the `dollarAmount` field.
	* The `long` variable should be used to locate a `BankAccount` with the respective id from the `BankAccountManager` singleton.
* The class should define a method `afterExecute` which increases the respective `account` field by the `dollarAmount` field.
* The class should define a method `afterUndo` which decreases the respective `account` field by the `dollarAmount` field.

### Part 3.3 - Create class `TaskAccountRemove`
* Create a subclass of `Task` named `TaskAccountDeposit` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` subpackage.
* The class should declare a final `bankAccount` variable of type `BankAccount`.
* The constructor should have a parameter of `long` which should be used to locate a `BankAccount` with the respective id from the `BankAccountManager` singleton.
* The class should define a meethod `afterExecute` which removes the `bankAccount` field from the `bankAccounts` list in the `BankAccountManager` singleton.
* The class should define a meethod `afterExecute` which adds the `bankAccount` field to the `bankAccounts` list in the `BankAccountManager` singleton.


### Part 3.4 - Create class `TaskAccountWithdrawal`
* Create a subclass of `TaskAccountDeposit` named `TaskAccountWithdrawal` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` subpackage.
* The constructor should take an argument of `double` and `long` and pass them to its `super` constructor.
* The class should define a method `afterExecute` which decreases its `account` field by the `dollarAmount` field.
* The class should define a method `afterUndo` which increases its `account` field by the `dollarAmount` field.



## Part 4 - Junit Testing

### Part 4.1 - Create class `TestTaskAccount`
* Create an _abstract_ class `TestTaskAccount` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` test-subpackage.
* The class should declare a field `bankAccountManager` of type `BankAccountManager`.
* The class should declare a field `taskManager` of type `TaskManager`.
* The class should define a `setup` method which is annotated with `@Before`
	* The method should assign field `bankAccountManager` to the `BankAccountManager` singleton.
	* The method should assign field `taskManager` to a new `TaskManager` object.

### Part 4.2 - Create class `TestTaskAccountCreate`
* Create a class `TestTaskAccountCreate` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` test-subpackage.
* The class should define a `test` method annotated with `@Test` which will:
	* populate the `taskManager` with `TaskAccountCreate` objects.
	* ensure accounts have not been added
	* perform tasks pending in the `taskManager`
	* ensure accounts have been added.

### Part 4.3 - Create class `TestTaskAccountDeposit`
* Create a class `TestTaskAccountDeposit` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` test-subpackage.
* The class should define a `test` method annotated with `@Test` which should:
	* populate the `taskManager` with a `TaskAccountCreate`.
	* perform tasks pending in the `taskManager`.
	* get reference to the `id` of the newly created `BankAccount`.
	* get reference to the `BankAccount`'s starting balance.
	* populate the `taskManager` with a `TaskAccountDeposit`.
	* perform tasks pending in the `taskManager`.
	* get reference to the `balance` of the `BankAccount`.
	* assert ending balance is the sum of starting balance and deposit amount.

### Part 4.4 - Create class `TestTaskAccountWithdrawal`
* Create a class `TestTaskAccountWithdrawal` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` test-subpackage.
* The class should define a `test` method annotated with `@Test` which should:
	* populate the `taskManager` with a `TaskAccountCreate`.
	* perform tasks pending in the `taskManager`.
	* get reference to the `id` of the newly created `BankAccount`.
	* get reference to the `BankAccount`'s starting balance.
	* populate the `taskManager` with a `TestTaskAccountWithdrawal`.
	* perform tasks pending in the `taskManager`.
	* get reference to the `balance` of the `BankAccount`.
	* assert ending balance is the difference of starting balance and deposit amount.

### Part 4.5 - Create class `TestTaskAccountSuite`
* Create a class `TestTaskAccountSuite` in the `io.zipcoder.zcw_taskmanager.bankaccount.task` test-subpackage.
* The class should be annotated with

```java
RunWith(Suite.class)

@Suite.SuiteClasses({
        TestTaskAccountCreate.class,
        TestTaskAccountRemove.class,
        TestTaskAccountDeposit.class,
        TestTaskAccountWithdrawl.class
})
```

* Run the class as a `junit` test, and ensure all scenarios pass.
