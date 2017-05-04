# React

# Naming

* Always use JSX syntax.

* Use .jsx extension for React components.

* Use PascalCase for filenames. E.g., FoodMenus.jsx.

# Syntax

* Do not use React.createElement unless you're initializing the app from a file that is not JSX.

  # bad
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

  # good
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }

* Use PascalCase for React components and camelCase for their instances. 

  # bad
  import foodMenus from './FoodMenus';

  # good
  import FoodMenus from './FoodMenus';

  # bad
  const FoodMenus = <FoodMenus />;

  # good
  const foodMenus = <FoodMenus />;

* Use the filename as the component name. For example, FoodMenus.jsx should have a reference name of FoodMenus.

* Do not use displayName for naming components. Instead, name the component by reference.

  # bad
  export default React.createClass({
    displayName: 'ReservationCard',
    // ...
  });

  # good
 class ReservationCard extends React.Component {
   // ...
 }

* Follow these alignment styles for JSX syntax.

  # bad
  <Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

  # good
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  />

* Use double quotes (") for JSX attributes & single quotes (') for all other JS. 

  # bad
    <Foo bar='bar' />

  # good
    <Foo bar="bar" />

  # bad
    <Foo style={{ left: "20px" }} />

  # good
    <Foo style={{ left: '20px' }} />

* Always include a single space in your self-closing tag.

  # bad
  <Foo/>

  # good
  <Foo />

* Use camelCase for prop names.

  # bad
  <Foo UserName="john" />

  # good
  <Foo userName="john" />

* Omit the value of the prop when it is explicitly true.
  # bad
  <Foo hidden={true} />

  # good
  <Foo hidden />

* Avoid using an array index as key prop, prefer a unique ID.

  # bad
  {todos.map((todo, index) =>
    <Todo
      {...todo}
      key={index}
    />
  )}

  # good
  {todos.map(todo => (
    <Todo
      {...todo}
      key={todo.id}
   />
  ))}

* Wrap JSX tags in parentheses when they span more than one line.

  # bad
  render() {
    return <MyComponent className="long body" foo="bar">
             <MyChild />
           </MyComponent>;
  }

  # good
  render() {
    return (
      <MyComponent className="long body" foo="bar">
        <MyChild />
      </MyComponent>
    );
  }

