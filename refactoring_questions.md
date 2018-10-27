# Refactoring Questions

#### What is a code smell?

Code smell is anything that looks structurally wrong in the code, and this makes the code harder to understand/maintain. This includes things like repeated code (belongs in a function), sparse comments and poor variable naming.

#### What are your favourite tools to find code smells and potential bugs?
There are some gems that can be used
- metric_fu: generates easy to read reports on design issues within your code.
- Rails Best Practices: checks code for violations of best practices for good rails code design. It’s command line based.
- Rubycritic: gives a grade (A-F) for churn, complexity, duplication and smells.
- Rubocop: A code analyser that has many checks that can be performed on code. 
- Reek: A smell detector tool.
- Code climate: An online service that checks code for quality, security and test coverage, it links to github account. 

#### Why should you avoid fat controllers?

A fat controller contains overly complex logic and business logic. Under the MVC model the model should contain the business login instead, while the controller is responsible for handling user input. In the case of the fat controller the Model is basically used to just store data in the database and the controller handles the business logic. Fat controllers make an application hard to test and lead to more code repetition. 

#### Why should you avoid fat models?
In large apps the model can grow too fat, making code hard to maintain, also sometimes it is necessary for a method to act on multiple objects, in which case the method should be extracted out of the model and placed into a domain service class. The domain service doesn’t hold any data of its own, rather it interacts with several objects.

#### Explain extract Value, Service, Form, View, Query, and Policy Objects techniques.
All techniques can be found here. https://www.sitepoint.com/7-design-patterns-to-refactor-mvc-components-in-rails/

Each technique extracts code out of the controllers/models and into new classes. 
- Value: small objects representing values that are comparable. Use when you want to move comparison logic out of the model/controller.
- Service: Use when model/controller logic is complex, uses external APIs or uses more than one object.
- Query: Use when need to reuse queries across models.
- Form: Use when needing to reuse data validation/persistence methods across models.
- View: Use to take data/calculations that are only needed to transform the model into a view out of the view model itself. Such as generating an image url, concatenating a first and last name.
- Policy objects: similar to service objects but are used for read operations. Use to extract complex rules (such as who is allowed to create new projects- admin only) from the model/controller.
