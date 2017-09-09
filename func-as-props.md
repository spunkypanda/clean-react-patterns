# Function-as-props

I came across a really cool React component composition pattern while reading [Kent C Dodds' article introducing Downshift ](https://medium.com/@kentcdodds/introducing-downshift-for-react-b1de3fca0817 "url"). While this was a new pattern for me, it may not be for others. However for the benefit of anyone who comes across this repo, I shall introduce this nifty pattern. 

In the first code snippet, I shall define a component that can be a parent component that exposes certain props to a stateless child component. This child component shall be a function.

```javascript
class FuncAsProps extends React.Component {
  render() {
    const employee = {
      age: 24,
      name: 'Chinmay Bag',
      twitter: '@JustChinmay',
      github: 'spunkypanda',
      designation: 'Software engineer',
    };

    return (
      <div style={{ fontWeight: 500 }}>
        {
          this.props.children(employee)
        }
      </div>
    );
  }
}
```

The functional component used as a child here destructures the object passed to it by the parent component to take the components its needs in order to correctly render. The parent component exposes the same attributes, irrespective of the child component. In the first snippet, we can build a component that gives a more professional introduction to an employee, displaying a link to their github profile as well.

```javascript
class ProfessionalComponent extends React.Component {
  render() {
    return (
      <div>
        <FuncAsProps>
          {
            ({
              name,
              twitter,
              github,
              company,
            }) => (
              <div>
                <div>`{name}  works at {company}`</div>
                <div>Twitter: <a href={`https://twitter.com/${twitter}`}>{twitter}</a></div>
                <div>Github: <a href={`https://github.com/${github}`}>{github}</a></div>
              </div>
            )
          }
        </FuncAsProps>
      </div>
    );
  }
}
```

In the following snippet, we chose a child component that gives a casual introduction to the employee, just casually mentioning the details and not even providing a link to the mentioned twitter profile.

```javascript
class CasualComponent extends React.Component {
  render() {
    return (
      <div>
        <FuncAsProps>
          {
            ({
              age,
              name,
              twitter,
              company,
            }) => (
              <div>
                <div><b>{name}</b></div>
                <div>Age: {age}</div>
                <div>Twitter: {twitter}</div>
                <div>Company: {company}</div>
              </div>
            )
          }
        </FuncAsProps>
      </div>
    );
  }
}
```
As we have seen, this is a really powerful pattern that allows developers to expose certain props irrespective of the chidl component used. We can go ahead and make changes at later stage or completely replace or conditionally render child components as long as the child component always depends only on the props provided by the Parent Component.


Source:
1. [Introduction to Downshift for React](https://medium.com/@kentcdodds/introducing-downshift-for-react-b1de3fca0817 "url")
2. [Function as Child Components](https://medium.com/merrickchristensen/function-as-child-components-5f3920a9ace9 "url")
