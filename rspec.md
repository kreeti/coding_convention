## first 'describe' what you are doing then establish 'context'

## DESCRIBING METHODS IN RSPEC

 * use . (or ::) when referring to a class method's name and # when referring to an instance method's name. 

 ```
  # BAD:
    describe 'the authenticate method for User' do
    describe 'if the user is an admin' do

  # GOOD:
    describe '.authenticate' do #CLASS METHOD
    describe '#admin?' do #INSTANCE METHOD

 ```

## USE OF CONTEXTS
  * we should always use two context for one example test, one for positive context and another for negative context
 ```
   context 'for passing in exam' do
   context 'for not passing in exam' do
   end
   end 

 ```
  * When describing a context, start its description with "when" or "with".

## USE SUBJECT 

 * if you are having several tests related to same subject use subject{} to make the code DRY

  ```
  subject { SomeClass.some_method }
    it "should do something" do
      expect(subject.first).to eq(something)
      expect(subject.last).to eq(something_else)
    end

  ```

## USE FACTORIES FOR CREATING NEW DATA

  ```
 # BAD
   user = User.create(
     name: 'xyz',
     birth: '17 september',
     admin: true
    )

 # GOOD
  user = { FactoryGirl.create :user }

  ```

## use 'database_cleaner' gem for cleaning database and configure

  ```
  RSpec.configure do |config|

    config.before(:suite) do
      DatabaseCleaner.strategy = :transaction
    end

    config.around(:each) do |example|
      DatabaseCleaner.clean_with(:truncation)
    end
  end   

  ```

## Keep your description short
 * A spec description should never be longer than 40 characters. If this happens you should split it using a context.

 ```
 #bad
    it 'has 422 status code if an unexpected params will be added' do

 #good
     context 'when not valid' do
       it { is_expected.to respond_with 422 }
     end

 ```

## USE let and let!
  * When you have to assign a variable instead of using a before block to create an instance variable, use let.

  ```
  describe '#type_id' do
    let(:resource) { FactoryGirl.create :device }
    let!(:type)     { Type.find resource.type_id }

    it 'sets the type_id field' do
      expect(resource.type_id).to equal(type.id)
    end
  end

  ```

## expect vs should syntax
  * always use expect synax instead of should syntax

  ```
  #bad
    it 'creates a resource' do
      response.should respond_with_content_type(:json)
    end

  #good
    it 'creates a resource' do
      expect(response).to respond_with_content_type(:json)
    end

   ``` 
## create only data you need
  * only create required data otherwise test suite will become heavy to run

  ```
   #bad
   describe "User" do
     describe ".top" do
       before { FactoryGirl.create_list(:user, 3) }
       it { expect(User.top(2)).to have(2).item }
     end
   end

  ```
