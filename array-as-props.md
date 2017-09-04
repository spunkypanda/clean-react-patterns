# Better prop management

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
