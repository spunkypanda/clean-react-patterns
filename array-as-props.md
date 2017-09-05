# Better props management with defaultProps

### 1. Array as props

A lot of times, beginners in React start with destructuring out specific attributes out of props passed to the Component instance as shown in the first snippet. But, as soon as a certain prop is not passed to the instance by its parent component, the component starts to break apart. This can happen due to multiple reasons i.e. API calls missing a key in response or the programmer has just forgotten to pass it to our component.

The quickfix solution that most of us come up with is the ``` ||  ``` operator. The first snippet might seem familiar to atleast a few React beginners. 


```javascript
// Earlier implementation

class Posts extends React.Component {
  render() {
    const posts =  this.props.posts || [];
    return (
      <div>
        <ul>
        {
            Array.isArray(posts) && posts.map(item => (<li>{item.text}</li>))
        }
        </ul>
      </div>
    );
  }
}
```
A more elegant way to handle this would be using the defaultProps on the Component to handle these situations, shown as follows.

```javascript
// Cleaner implementation

class Posts extends React.Component {
  render() {
    const { posts } =  this.props;
    return (
      <div>
        <ul>
        {
            posts.map(item => (<li>{item.text}</li>))
        }
        </ul>
      </div>
    );
  }
}

Posts.defaultProps = {
  reportTypes: [],
  reportData: [],
}
```
