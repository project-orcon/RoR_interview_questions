# Active Record


#### Explain the Active Record pattern.

In Active Record, objects carry both persistent data and behaviour which operates on that data.

from PoEAA book.
> An object that wraps a row in a database table or view, encapsulates the database access, and adds domain logic on that data.


#### What is Object-Relational Mapping?

 From rails guide.
> Commonly referred to as its abbreviation ORM, is a technique that connects the rich objects of an application to tables in a relational database management system. Using ORM, the properties and relationships of the objects in an application can be easily stored and retrieved from a database without writing SQL statements directly and with less overall database access code.

ORM is a layer between the database and application. 


#### Describe Active Record conventions.

Taken from rails guide.
In order to prevent having to write a lot of configuration code, rails has several conventions that are used instead.

- Naming conventions: ActiveRecord using naming conventions to find out how the mapping between models and database tables should be created. It pluralises class names to find the respective database table. Rails has very powerful pluralisation mechanisms (eg. Mouse will be pluralised to Mice). When a class name contains more than one word, the model class name should use CamelCase form while the table contains the words separated by underscores.

- Schema conventions: ActiveRecord uses naming conventions for the columns in database tables, depending on their purpose.
  - Foreign keys: These are the fields looked for when associations are created on the model. And follow the pattern className_id (e.g. item_id).
  - Primary keys: By default active record creates an integer column named id as the tables primary key. 
  - Additional columns: These add additional features to activeRecord instances, these include created_at (sets dateTime when record is created), updated_at, lock_version, type and more. Be sure not to use type as a column name, as it is a reserved keyword.
 

#### Explain the Migrations mechanism.
Taken from rails guide.

Migrations provide a way to alter your database schema over time. They use a Ruby DSL so no SQL needs to be written by hand, allowing the schema and changes to be data independent. Each migration can be considered to be a new version of the database. Each Migration modifies the schema to add/remove tables, columns or entries. Migrations can be reversed too by rolling them back. 

to create a migration use
```
rails g migration addcompletefield
```

#### Describe types of associations in Active Record.

Most of the following was taken from the rails guide. https://guides.rubyonrails.org/association_basics.html. Associations represent connections between models. 

There are six types of associations in rails.
- belongs_to
- has_one
- has_many
- has_many :through
- has_one :through
- has_and_belongs_to_many

##### belongs_to
sets up a one to one connection with another model, declaring that one object belongs to another instance of another.

Book Model *belongs_to* Author model. In the database a foreign_key :author_id is added to the book model. 

##### has_one
Sets up a one to one connection with another model. Declares that each instance of a model contains or possesses one instance of another.
For example the Supplier model h*as_one* account model.



##### has_many
Sets up a one to many connection with another model. Each instance of the model has zero or more instances of another model. The other model name is pluralised when it’s declared.

```
class Author < ApplicationRecord
  has_many :books
end
```

##### has_many :through
Sets up a many-to-many connection with another model. This declares that a model can be matched with zero or more instances of another model by proceeding through a third model.

For example consider the three models. Doctor, Appointment and Patient.

Here a doctor can have many patients and a patient can have many doctors, and this occurs through the appointments model.

The Doctor has_many appointments. The doctor has many patients through the appointments model. The Patient has_many appointments, the Patient has_many Doctors through the appointments model. 

```
class Physician < ApplicationRecord
  has_many :appointments
  has_many :patients, through: :appointments
end
```

##### has_one :through
Sets up a one to one association with another model. Declares that a model can be matched with one instance of another model, through a third model. Consider three models, Supplier, Account and AccountHistory. The Supplier has one Account and each Account is associated with one AccountHistory. 

```
class Supplier < ApplicationRecord
  has_one :account
  has_one :account_history, through: :account
end
 
class Account < ApplicationRecord
  belongs_to :supplier
  has_one :account_history
end
 
class AccountHistory < ApplicationRecord
  belongs_to :account
end
```

##### has_and_belongs_to_many

Similar to the has_many :through model in that it creates a many to many connection however it does so without a third model. For example consider two models, Part and Assembly. Each assembly can have many parts and each part can belong to many assemblies.

A has_and_belongs_to_many works with a table in the database named :assemblies_parts (the model names are ordered alphabetically), which contains both the assembly_id and the part_id. 

```
class Assembly < ApplicationRecord
  has_and_belongs_to_many :parts
end
 
class Part < ApplicationRecord
  has_and_belongs_to_many :assemblies
end
```

#### What is Scopes? How should you use it?

A scope is a subset of a collection. They return ActiveRecord:Relation objects which means that they can be chained together.  Scopes are defined in the model class. They allow you to specify commonly used/complex queries. 

Taken from stack overflow
```
class Zombie
  scope :rotting, -> { where(rotting: true) }
  scope :fresh, -> { where('age < ?', 25) }
  scope :recent, -> { order(:created_at, :desc) }
end
```

can be used as 
```
Zombie.rotting.fresh.recent.limit(3)
```


#### Explain the difference between optimistic and pessimistic locking.

Locking is necessary to prevent two concurrent processes from updating the same object at the same time. 

Optimistic Locking assumes that a database transaction conflict only happens rarely. It raises an error when other user tries to update the record while it is locked. To use optimistic locking you create a lock_version column in the model you want to place the lock. Every time the object is updated lock_version will be increased. 


Pessimistic locking assumes that a database transaction conflict is very likely to happen. It locks the record until the transaction is done. If the record is currently locked and another user makes a transaction, that second transaction will wait until the lock in first transaction is released.

```
user = User.lock.find(1) #locks the record
user.name = ‘kim’
user.save! #release the lock
```





