#use . (or ::) when referring to a class method's name and # when referring to an instance method's name. 

BAD:
describe 'the authenticate method for User' do
describe 'if the user is an admin' do

GOOD:
describe '.authenticate' do
describe '#admin?' do

