# Rails

## Programming

* Write DRY code during development any project.

* Order variables and methods alphabetically when possible.

* Use 2 space indentation.

* Do not make any spelling mistakes or grammar mistakes. Use proper english words.

* put space if needs. like- `<% if current_user %>`(correct) `<%if current_user%>`(wrong).
 Another example: `"hello"` (correct) `" hello "` (wrong)

* Use valid syntax. If you are using rails 5 version, then follow rails 5 syntax.
  Example: don't use `=>` like- `(:presence => true)`, use `(presence: true)`

* Do not repeat same code, write it inside helper. Example: suppose you are styling a button
  with some front-awesome style and this same button needs in more than one places, then write
  it inside a helper method and then call it from view and pass link path.

  ```erb
  # bad
  # index.html.erb
  <%= link_to ('<i class="fa fa-trash" title="Delete Details"></i> Delete').html_safe,
                employee_path(employee),
                method: :delete,
                data: { confirm: "Are you sure?" },
                class: 'btn btn-danger btn-sm' %>

  # show.html.erb
  <%= link_to ('<i class="fa fa-trash" title="Delete Details"></i> Delete').html_safe,
                employee_path(@employee),
                method: :delete,
                data: { confirm: "Are you sure?" },
                class: 'btn btn-danger btn-sm' %>

  # good
  # helper.rb
  def delete_link(path)
    link_to ('<i class="fa fa-trash" title="Delete Details"></i> Delete').html_safe,
              path,
              method: :delete,
              data: { confirm: "Are you sure?" },
              class: 'btn btn-danger btn-sm'
  end

  # index.html.erb
  <%= delete_link(employee_path(employee)) %>

  # show.html.erb
  <%= delete_link(employee_path(@employee)) %>
  ```


* Name of the helper(or variable/funcation/scope) should reflect its purpose.
* Try to avoid comment messages unless the code is too complicated
* Always use lastest syntax.

## Bundler

* Put gems in alphabetical order in the Gemfile.

* Do not use any unnecessary gems in your project.

* Use only established gems in your projects. If you're contemplating on
  including some little-known gem you should do a careful review of its source
  code first.

* If your project needs different gems for different environments, then group it for that specific environment.
  ```ruby
  group :development, :test do
    gem 'mysql2'   #mysql for development
    gem 'pry-rails', "~> 0.3.4"
  end

  group :production do
    gem 'pg'    #postgresql for production
  end
  ```


* Do not remove the `Gemfile.lock` from version control. This is not some
  randomly generated file - it makes sure that all of your team members get the
  same gem versions when they do a `bundle install`.


## Migrations

* Keep the `schema.rb` under version control and arrange it well, so that it clearly understandable.

* Add database level validation as well model level validation

* Enforce foreign-key constraints.

* When writing constructive migrations (adding tables or columns),
  use the `change` method instead of `up` and `down` methods.
  ```Ruby
  # the old way
  class AddNameToPeople < ActiveRecord::Migration
    def up
      add_column :people, :name, :string
    end

    def down
      remove_column :people, :name
    end
  end

  # the new preferred way
  class AddNameToPeople < ActiveRecord::Migration
    def change
      add_column :people, :name, :string
    end
  end
  ```


* If you are writing something within `up` migration, write it in the reverse order within
  `down` migration if needed.

* After migrating a migration use `rollback` command to check whether the database can
  return to its previous state or not.


## Routing

* When you need to add more actions use `member` and `collection` routes.

  ```Ruby
  # bad
  get 'subscriptions/:id/unsubscribe'
  resources :subscriptions

  # good
  resources :subscriptions do
    get 'unsubscribe', on: :member
  end

  # bad
  get 'photos/search'
  resources :photos

  # good
  resources :photos do
    get 'search', on: :collection
  end
  ```


* If you need to define multiple `member/collection` routes use the
  alternative block syntax.

  ```Ruby
  resources :items do
    member do
      get 'allocate'
      put 'reallocate'
      # more routes
    end
  end

  resources :photos do
    collection do
      get 'search'
      # more routes
    end
  end
  ```


* Use nested routes to express better the relationship between ActiveRecord
  models.

  ```Ruby
  class Post < ActiveRecord::Base
    has_many :comments
  end

  class Comments < ActiveRecord::Base
    belongs_to :post
  end

  # routes.rb
  resources :posts do
    resources :comments
  end
  ```


* Left unnecessary routes if those routes are not used. Use `except/only` for the purpose.

  ```ruby
  resources :users, except: [:show]
  resources :employee, except: [:show, :edit, :update]
  ```


## Controllers

* Keep the controllers skinny - they should only retrieve data for the view
  layer and shouldn't contain any business logic (all the business logic
  should naturally reside in the model).

* If more than one action in a controller contains same lines of code, then write
  it into seperate a method and use callback funcation to invoke it on those action.

  ```ruby
  # bad
  # controller.rb
  def edit
    @category = Category.find(params[:id])  
  end

  def show
    @category = Category.find(params[:id])
    @category_items = @category.items.paginate(page: params[:page], per_page: 5)
  end

  #good
  # controller.rb
  before_action :get_category, only: [:edit, :show]
  def show
    @category_items = @category.items.paginate(page: params[:page], per_page: 5)
  end

  def get_category
    @category = Category.find(params[:id])
  end
  ```


* If `current_user` exists in browser, then don't need to hit database every time you need
  `curent_user`.
  ```ruby
  #bad
  def current_user
    @current_user = User.find(session[:user_id]) if session[:user_id]
  end

  #good
  def current_user
    @current_user ||= User.find(session[:user_id]) if session[:user_id]
  end
  ```


* Remove n + 1 query problem from all places in your project.

* Your code should be precise. Like, use flash in single line.
  ```ruby
  #bad
  redirect_to users_path
  flash[:notice] = "User successfully created."

  #good
  redirect_to users_path, flash: { success: "User successfully created." }
  ```

## Model

* Write your model simple and well formated.
  Group same type of method. Follow this coding pattern for model.
  ```ruby
  class Issue < ActiveRecord::Base
    enum priority: [:high, :medium, :low, :as_soon_as_possible]

    belongs_to :item, optional: true
    belongs_to :system, optional: true     

    has_many :resolution, optional: true    

    validates :title, presence: true       
    validate  :item_or_system_presence
    validate  :item_closed_at_limitation
    validate  :system_closed_at_limitation

    scope :order_desending, -> { order('created_at DESC') }
    scope :unclosed,        -> { where(closed_at: nil) }

    def item_or_system_presence
      unless [item, system].any?
        errors.add :base, 'Item / System must be present!'
      end
    end
  end
  ```


* Generate model from terminal. Do not create `model.rb` and migration your own, let
  rails to do it for you.

  ```
  rails generate model Item name:string description:text
  ```


* Choose a proper name for methods, scopes etc.

## Views

* Please do not use inline style.

* Try to avoid html_safe. Instead of using this - link_to("<span>Add</span>".html_safe, new_user_path(@user), class: "btn") ,  we should use link_to block.

  ```erb
  <% link_to(new_user_path(@user), class: "btn") do %>
    <span>Add</span>
  <% end %>
  ```

* Try to use partial instead of writing same code multiple time.
