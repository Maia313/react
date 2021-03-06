
### React and Redux: Manage State Locally First

First, in the `render()` method, have the component render an input element, button element, and ul element. When the input element changes, it should trigger a `handleChange()` method. Also, the input element should render the value of input that's in the component's state. The button element should trigger a `submitMessage()` method when it's clicked.

Second, write these two methods. The `handleChange()` method should update the input with what the user is typing. The `submitMessage()` method should concatenate the current message (stored in input) to the messages array in local state, and clear the value of the input.

Finally, use the ul to map over the array of messages and render it to the screen as a list of li elements.

```js
class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange=this.handleChange.bind(this);
    this.submitMessage=this.submitMessage.bind(this);

  };
  // add handleChange() and submitMessage() methods here

handleChange(e){
  this.setState({input: e.target.value})
};



submitMessage(){
  let newMessages = [...this.state.messages, this.state.input];
  
this.setState({
     messages: newMessages,
     input: ''
   })
};



  render() {
    
    const items = this.state.messages.map(msg => <li>{msg}</li>)
    
    return (
      <div>
        <h2>Type in a new Message:</h2>
                        
        <input value={this.state.input} onChange={this.handleChange}/>
        <button onClick={this.submitMessage}>Submit Me!</button>
        <ul>{items}</ul>
          
      </div>
    );
  }
};
```

```js
// define ADD, addMessage(), messageReducer(), and store here:
const ADD = 'ADD'; //action type
const defaultState = []; 

//action creator which return the msg in the return action
function addMessage(msg) {
  return {
    type: ADD,
    message: msg
  };
};

//reducer, adds a message to the array of messages held in state, or returns the current state
const messageReducer = (state = defaultState, action) => {
  switch(action.type){
     case ADD: return [...state, action.message]; // This comma should be a semicolon
   break;
     default: return state
  
  };
  
};

//Redux store
const store = Redux.createStore(messageReducer);
```
