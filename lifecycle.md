### Use the Lifecycle Method 

React components have several special methods that provide opportunities to perform actions at specific points 
in the lifecycle of a component. These are called `lifecycle methods`, or lifecycle hooks, and allow you to catch components 
at certain points in time. This can be **before they are rendered**, **before they update**, **before they receive props**, **before they unmount**, and so on. Here is a list of some of the main lifecycle methods:

* **`componentWillMount()`**

* **`componentDidMount()`**

* **`componentWillReceiveProps()`**

* **`shouldComponentUpdate()`**

* **`componentWillUpdate()`**

* **`componentDidUpdate()`**

* **`componentWillUnmount()`**


Each Class Component goes through a component life cycle with multiple phases. 

> Mounting Phase Methods

The **`mounting phase`** begins when an instance of a component is created and rendered into the DOM. The following lifecycle methods occur in the order they are listed:

   * constructor(props) - called when the component is first initialized. This method is only called once.
   * componentWillMount() - called when a component is about to mount.
   * render() - called when a component is rendered.
   * componentDidMount() - called when a component has finished mounting. This is where network requests are usually made.

> Updating Phase Methods

The **`updating phase`** begins when a component's properties or state changes. The following lifecycle methods occur in the order they are listed:

   * componentWillReceiveProps(nextProps) - called when a component has updated and is receiving new props.
   * shouldComponentUpdate(nextProps, nextState) - called after receiving props and is about to update. If this method returns false, componentWillUpdate(), render(), and componentDidUpdate() will not execute.
   * componentWillUpdate(nextProps, nextState) - called when a component is about to be updated.
   * render() - called when a component is rerendered.
   * componentDidUpdate(prevProps, prevState) - called when a component has finished updating.

> Unmounting Phase Methods

The **`unmounting phase`** begins when a component is being removed from the DOM. The following life cycle method occurs during the unmounting phase:

   * componentWillUnmount() - called immediately before a component unmounts. This is where any cleanups are made such as cancelling timers or network requests.

