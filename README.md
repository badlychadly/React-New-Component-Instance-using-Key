# React-New-Component-Instance-using-Key

As React developers every now and then we find ourselves in a situation where we need our component to rerender or be replaced with a new instance if our props change. We are tempted to look at the static lifecycle method `getDerivedStateFromProps()`. I look at the documentation and get hesitant because of all the warnings that say it is for rare cases only. Luckily the documentation covers a few alternatives to using this method one of them being to use the React attribute of `key`.

## Using Key
Keys are mostly used when rendering dynamic lists in React but because key changes in React create a new component instance they are very useful in some Cases. The situation that I found them useful was when using React-Router-Doms `Link` and `Route` components to render the show page of a specific post. I pass props to the compent being rendered by the route but none of them are used for displaying purposes, only for a condition when the component is first  initialized. Because of this the data displayed stays the same even when I click another show page link. In React even though a parent component has prop changes unless the child is displaying the data the component will stay the same. State changes in a component will trigger the needed changes, but in my case my state doesn't need extra clutter. So passing the url params from the routerProps to the key attribute seemed like the easiest solution. Now when I click the links to the posts show page I get a new instance of that component and see the content needed being displayed.
```
///App.js


<Route exact path='/posts/:postId' render={routerProps => <BlogForm key={routerProps.match.params.postId} post={this.props.byId[routerProps.match.params.postId]} readOnly={true} {...routerProps} />}
```
Just a trick to add to your React arsenal!
