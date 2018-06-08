
So far, if any component receives **new state** or **new props**, it re-renders itself and all its children. 
This is usually okay. 
But React provides a `lifecycle method` you can call when child components receive new state or props, 
and declare specifically if the components should update or not. The method is `shouldComponentUpdate()`, and it 
takes `nextProps` and `nextState` as parameters.

This method is a useful way to optimize performance. For example, the default behavior is that your component re-renders 
when it receives new props, even if the props haven't changed. You can use `shouldComponentUpdate()` to prevent this 
by comparing the props. The method must return a boolean value that tells React whether or not to update the component. 
You can compare the `current props (this.props)` to the `next props (nextProps)` to determine if you need to update or not, 
and return true or false accordingly.
