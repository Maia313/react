
#### Controlled Components

**Handling forms**
```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
**Controlled form**

```js
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
   // 
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    // 
    event.preventDefault();
    this.setState({
      submit: this.state.input
    })
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          { /* change code below this line */ }
          <input value={this.state.input} onChange={this.handleChange} />
          { /* change code above this line */ }
          <button type='submit'>Submit!</button>
        </form>
      
        <h1>{this.state.submit}</h1>
      </div>
    );
  }
};
```


##### Controlling input fields
```js
class ControlledInput extends React.Component{

    constructor(props){
        super(props)
        this.state = {value: ''}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){
        this.setState({value: event.target.value})
    }
    render(){
        return (
            <input type = "text" value = {this.state.value} onChange = {this.handleChange}/>
        )
    }
}
```
##### Controlling Checkboxes
```js
class ControlledInput extends React.Component{

    constructor(props){
        super(props)
        this.state = {checked: false}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){
        this.setState({checked: event.target.checked})
    }
    render(){
        return (
            <input type = "checkbox" checked = {this.state.checked} onChange = {this.handleChange}/>
        )
    }
}
```
##### Controlling TextArea fields

```js
class ControlledTextArea extends React.Component{

    constructor(props){
        super(props)
        this.state = {value: ''}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){
        this.setState({value: event.target.value})
    }
    render(){
        return (
            <textarea type = "text" value = {this.state.value} onChange = {this.handleChange}/>
        )
    }
}
```
##### Controlling select tags
```js
class ControlledSelect extends React.Component{

    constructor(props){
        super(props)
        this.state = {value: 'apple'}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){
        this.setState({value: event.target.value})
    }
    render(){
        return (
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="apple">apple</option>
            <option value="banana">banana</option>
            <option value="carrot">carrot</option>
            <option value="donuts">donuts</option>
          </select>
        )
    }
}
```
Select Components can also have their options dynamically generated using the map() method.
```js
class ControlledSelect extends React.Component{

    constructor(props){
        super(props)
        this.state = {value: 'apple'}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){
        this.setState({value: event.target.value})
    }
    render(){
        var array = ["apple","banana","carrot","donuts"]
        var options = array.map( (item) =>
            <option value = {item}>{item}</option>
        )
        return (
          <select value={this.state.value} onChange={this.handleChange}>
            {options}
          </select>
        )
    }
}
```

##### Handling Multiple Inputs

```js
class ControlledMultiple extends React.Component{

    constructor(props){
        super(props)
        this.state = {value: 'apple'}
        this.handleChange = this.handleChange.bind(this)
    }
    handleChange(event){


        this.setState({[event.target.name]: event.target.value})
    }
    render(){
        var array = ["apple","banana","carrot","donuts"]
        var options = array.map( (item) =>
            <option value = {item}>{item}</option>
        )
        return (
            <form>
                <input name="inputName" type = "input" value = {this.state.inputName} onChange = {this.handleChange}/>
                <textarea name="textAreaName" type = "text" value = {this.state.textAreaName} onChange = {this.handleChange}/>

                <select name = "selectName" value={this.state.selectName} onChange={this.handleChange}>
                    {options}
                </select>
            </form>
        )
    }
}
```
