### What is code coverage?

In technical terms, code is, what you, the dev has written. Coverage is, what percentage of this code is **traversed** by your testing suite. In simple terms, code coverage is the portion of your code which has been dry run, intentionally or accidentally, at least once by you (via a testing suite).

For a software with lots of code, coverage is calculated as average of its code base.

---

### What is a test case?

To test an implementation code, we write a test case. A test case is a piece of code which executes(dry runs) the implementation code so we can validate and verify its intended functioning. 

---

### Why do we need to write it?

One can argue that, when we have dedicated resources for manual and automated testing in a project, why are devs required to write test cases? Isn't it redundant? It consumes time and effort for the devs, translating into increased cost and delivery time. 

The argument is not incorrect. It does incur time and effort. It is redundant. But it is as necessary as the implementation itself, maybe even more.
#### Abstract motivation

**Some build up**
So I heard this quote from some seasoned engineer and while it wasn't particularly related to testing. 

It goes like this: 
	`Your code should be boring. Boring is good. Boring is` **predictable**.

The foundation of computation stands on **unambiguity**. An ambiguous code is like a gossip. It can be right, it can be wrong, it can make sense or be non-sensical in different lights. While we may be able to deduce a gossip at times, a computer won't. It needs **definitive** instructions.

![[https://github.com/P01SHUBHAMP/discovery_onboarding_roadmap/blob/main/Gutenberg%20Project/images/image_0.png| 300]]

When you are sitting on a table and someone says, *`Kripya panni badhaiye`*. You pass the water container towards the person. If you translate this statement into english word-by-word, it becomes non-sensical, i.e; *`Please increase water`*. While you would effortlessly understand the statement, a computer sitting behind layers of translators simply would not.

What my point is, in a project of thousands of lines of code, we need a degree of unambiguity and definitive-ness to show proof of our(developers') translation capability, from business requirement to software. And what better way to prove it than by showcasing that every **unit** of this product is put through test by the creators themselves.

**To sum up the notion, we should write test cases to**:
- Reinforce unambiguous translation of requirement into code.
- Proof of definitive-ness
- Prideful ownership of your creation
#### Apparent motivation

So, the fundamental idea is to **definitively** traverse every possible decision path a **unit** of code can take and validate its behavior or outcome.

Following are some apparent benefits of writing test cases:
1. **Living and interact-able documentation of the code base.**
	   While comments and self explanatory naming conventions can greatly assist in understanding what a function or class does, they are generally meant for the consumers of the code. For example, a package is rated based on how descriptive or well documented it is. But that still doesn't explain how the package works. It's still a blackbox with labels and manual of use. To understand the mechanics of a package for "inspirational", auditing or security purposes, you have to read its source code, which can be very time consuming. And a better way to dissect the task is to look at the test cases. 
	   Why?
	   Because a test case describes each logical chunk in isolation, which can help you understand how the implementation is done in an overview, what all general, edge or super rare cases it can handle, where all it will fail and so on.
2. **Announces assumption and boundaries of the code base.**
	   A test case not only provides verification of a code working well. It also helps in defining the assumptions which were agreed upon while ideation and technical reviews. It acts as proof of proper understanding and implementation within the purview of agreed boundaries.
3. **Self enforces development to be testable.**
	   Writing test cases is cumbersome. Writing test cases for a complex code is nightmare. We've all been in the situation where we frustratingly thought, "rewriting the whole implementation would be quicker than writing test cases for this piece of biscuit". This notion bars us from writing overly complex code. In turn directing us towards adopting smaller and maintainable principles of coding. Something in a SOLID state ;-)
4. **Maintainability**
	   A software is a delicate organism. If the behaviour of a code block is altered, intentionally or by mistake, it might fall apart. The test case works as a safeguard, whose description when read by the dev making changes, provides him/her information of the scope and boundary of this code block, so he/she can take informed decision before pushing unsafe changes. Do note, that there will always be scenarios where test case might not sound alarms.
5.  **Debugging**
	   A test case can be used to debug an implementation and understand the control flow with the provide context/arrangement. It can enable you to visualize cases which you might have missed while implementing the logic keeping the scope localized to the code block subject to the testing.  

#### Compliance and Governance

When we have so much motivation of having code coverage in the development process, why do we still need hard threshold to comply with?

We forget. Sometimes we need guardrails. Crossing the coverage threshold feels good. Acing it feels even better.

---

### Thought process & Scope of coverage

Now that we know the "**why**" of writing test cases, lets discuss the "**what**", or rather the "**what all**" should we aim to cover.

Reiterating the notion:
	The fundamental idea is to **definitively** traverse every possible decision path a **unit** of code can take and validate its behavior or outcome.

Let's break it down with following example:

```dart
class Foo {
  const Foo(this.service);

  final Some3rdPartyService service;

  String getValue() {
    try {
      final valueOrNull = service.getValue(); // return type: String?
      if(valueOrNull != null) {
        if(value.isNotEmpty) return value;
        return "fallbackValue";
      }
      return "fallbackValue";
    }
    catch (error) {
      throw FooException(
        message: "failed to get value", 
        error: error as String,
      );
    }
  }
}

void main() {
  final service = Some3rdPartyService();
  final foo = Foo(service);

  final result = foo.getValue();
  print("my value: $result");
}

```
- We have a class declaration `Foo` with a default `constructor` and a method `getValue`.
- When **foo.getValue()** is called, following are the scenarios which can occur:
	- **Scenario1**:`service.getValue()` returns a string `"value"`, which is returned for `foo.getValue()`.
	- **Scenario2**:`service.getValue()` returns an empty string `""`, then `foo.getValue()` returns `"fallbackValue"`.
	- **Scenario3**:`service.getValue()` returns `null`, then `foo.getValue()` again returns `"fallbackValue"`.
	- **Scenario4**:`service.getValue()` fails, then `foo.getValue()` throws a `FooException` object.

The thought process for a class method like one above should be, to **distinctively** and **exhaustively** cover all **"apparent"** scenarios which can pan out, i.e; we should have test cases for `Scenario1`, `Scenario2`, `Scenario3`, and `Scenario4`.

The emphasis on "**apparent**" is intentional as there might arise certain scenarios which one might not be able to identify upfront. For example, what if the 3rd party service which in negative scenario, was supposed to throw an error of type `String`, throws error of some different type. This scenario can break our code. (Note that this too can be handled, but we may not have control over external code).

This scenario should bring our attention to **Scope of coverage**.

We'll always be building upon one or many external (intra/inter-team or 3rd party) packages(any codebase). And the accountability of such packages working fine lies with their respective owners. But most likely these are non-binding contracts. Your code can break apart because of such dependencies.  So the thing we should keep ourselves aware of is, "in how many ways, concerned external code can behave", so that we can handle such behaviour in our usecase and not have surprises. Our responsibility should be to cover for our codebase with all apparent scenarios only.

Remember surprises in a codebase is bad. But they are unfortunate reality at times.

---

### Fundamentals of writing a test case

#### Structure
Your test cases should be structured exactly like your source code structure so that its no-brainer to create, find, and manage test cases as your source code grows.

![[https://github.com/P01SHUBHAMP/discovery_onboarding_roadmap/blob/main/Gutenberg%20Project/images/image_1.1.png | 300]]
*`Image 1.1: source code structure`*

![[https://github.com/P01SHUBHAMP/discovery_onboarding_roadmap/blob/main/Gutenberg%20Project/images/image_1.2.png | 300]]
*`Image 1.2: test code structure`*

#### Before writing a test case

**Filename**: 
For a source file with name `text_resolver_extension.dart` (*Image 1.1*), your corresponding test file must always be named as `text_resolver_extension_test.dart` (*Image 1.2*), i.e;  use same name as source file for the test file with an added **\_test** suffix.

**Required boilerplate**:
Following is the minimum required code you should always have in a new test file. `main` is your entry point of your test case, which your testing suite(the tool which runs your testcases) looks for. Having this prevents any interference with the testing suite. 
```dart
void main() {
  //TODO: your test case goes here
}
```
Don't keep your test file with no content.
