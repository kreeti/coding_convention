#first 'describe' what you are doing then establish 'context'

#DESCRIBING METHODS IN RSPEC
 *use . (or ::) when referring to a class method's name and # when referring to an instance method's name. 
 ```
  BAD:
  describe 'the authenticate method for User' do
  describe 'if the user is an admin' do

  GOOD:
  describe '.authenticate' do #CLASS METHOD
  describe '#admin?' do #INSTANCE METHOD
 ```

#USE OF CONTEXTS
  *we should always use two context for one example test, one for positive context and another for negative context
 ```
   context 'for passing in exam' do
   context 'for not passing in exam' do
   end
   end
 ```

#USE SUBJECT
 *if you are having several tests related to same subject use subject{} to make the code DRY
  ```
  subject { SomeClass.some_method }
    it "should do something" do
      expect(subject.first).to eq(something)
      expect(subject.last).to eq(something_else)
    end
  ```

#USE FACTORIES FOR CREATING NEW DATA
```
 # bad
   user = User.create(
    name: 'xyz',
    birth: '17 september',
    admin: true
    )
 # good
  user = { FactoryGirl.create :user }
```

#use 'database_cleaner' gem for cleaning database

#Keep your description short
 *A spec description should never be longer than 40 characters. If this happens you should split it using a context.