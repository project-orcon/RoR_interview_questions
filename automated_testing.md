# Automated Testing

#### What is unit testing (in classical terms)?

From stack overflow
A unit test is a test written by the programmer to verify that a relatively small piece of code is doing what it is intended to do. They are narrow in scope, they should be easy to write and execute, and their effectiveness depends on what the programmer considers to be useful. 

Part of being a unit test is the implication that things outside the code under test are mocked or stubbed out. Unit tests shouldn't have dependencies on outside systems. 

An integration test is done to demonstrate that different pieces of the system work together. Integration tests cover whole applications, and they require much more effort to put together.


#### What is the primary technique for writing a test?

The primary technique for writing tests involves using Assert statements to test if the actual result matches the expected result.

#### What are your favorite tools for writing unit tests?

For writing unit tests, either using Minitest or Rspec. Rspec is more like written english and is more verbose than Minitest and requires setup and configuration (unlike Minitest). Minitest is my preferred testing suite. FactoryGirl is useful for mocking up databases for unit testing and is preferred to fixtures, as it shows the data being used in the test, making it easier to understand what is going on. 

Unit tests are performed on the models and controllers. Model Testing checks things like model validation, associations, scopes and custom methods/attribute writers. 

Controller testing is also known as functional testing. Since controllers should be skinny in rails, controller testing can be omitted in favour of thorough integration tests instead. However if your controller is very complicated, it might be necessary to unit test. 

#### What are your favorite tools for writing feature tests?
Feature tests involve testing the application by interacting with it just like a real user, they are also known as integration/system tests. My favourite tool for feature testing is capybara. 

for more information on using minutest and capybara
https://semaphoreci.com/community/tutorials/integration-testing-ruby-on-rails-with-minitest-and-capybara


