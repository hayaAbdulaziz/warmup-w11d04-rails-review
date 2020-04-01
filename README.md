# Rails Review

For each of the following topics, please answer each of the questions. You can use links and images to support your answer. Once done please make a pull request.

## Has many Through

- [Rails Active Record Intro](https://github.com/sei-entropy/lesson-w11d02-rails-active-record#active-record-associations)
-[Hospital App](https://github.com/sei-entropy/hw-w11d02-rails-hospital)

### Questions

1. What is the role of a join table in a many-to-many relationship?

   The role of the join table is to bind two models together using a third mode. Join table will have the primary key and at least two foreign keys that are usually the primary keys of a the other models.

2. What two columns must be present in a join table?
  foreign ids that associate the table to other tables. It's own id that denotes a unique association.


3. Given the example below, edit the code to define a has many :through relationship.

    ```ruby
    class Customer < ActiveRecord::Base
     has_many :purchases
      has_many :products, through: :purchases
      end

    class Product < ActiveRecord::Base
     has_many :purchases
     has_many :customers, through: :purchases
      end

    class Purchase < ActiveRecord::Base
     belongs_to :customer, :product
    end
    ```


4. Based on #3, give an example of associating two instances via the join model.

class UserEventAssociation < ActiveRecord::Migration
  def change
    create_table :attendances do |t|
      t.belongs_to :user
      t.belongs_to :event
    end
    end
    end

## Devise

- [Devise Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-devise)

### Questions

1. What does the `current_user` method that the Devise gem provides?
current_user is a helper is a helper method that is used to return objects that are specific to that user

2. What does the `authenticate_user!` method that the Devise gem provides?
Tauthenticate_user is a helper method that restricts users from specified controller actions i.e. edit or destroyr

3. Write a signout link using the `link_to` rails helper and a devise path.
  <%= link_to('Logout', destroy_user_session_path, method: :delete) %> 

4. How do I generate a devise model in the terminal?
   rails generate devise:install


5. What are the trade offs for using a gem for authentication over a handrolled solution? (no real right answer)
It is allows the use of using code written by coders who are experienced in authentication


## Validations

- [Validations Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-model-validations)

### Questions

1. Which component, of Rails MVC, is responsible for the business logic?
  Controller

2. Assume the user's age is an optional field.  Write the validation to verify that a User's age is between 13 and 125 (inclusive).
    class User < ActiveRecord::Base
    validates :age, numericality: (greater_than_or_equal_to: 13, less_than_or_equal_to: 125)
    end

3. What would `user.errors.messages` return (for the above User), if you assigned `user.age = 12`?

:age=>["must be greater than or equal to 13"] 

4. Assume you visit "/customers/new" and enter some invalid information.  Given this controller code, what url would your browser be on after pressing "Create Customer"?
"/customers/new"
``` ruby
class CustomersController < ApplicationController
  def new
    @customer = Customer.new
  end

  def create
    @customer = Customer.new(customer_params)
    if @customer.save
      redirect_to customer_path(@customer)
    else
      render :new
    end
  end
  ...
  private
  def customer_params
    params.require(:customer).permit(:first_name, :last_name, :age)
  end
end
```


5. Give one reason why we might have the similar validations in the browser, model, and database layer of our application.

We validate the same information, which we input in browser, correspond to our model and will be saved in database.
