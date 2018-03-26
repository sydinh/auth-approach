# react-auth
> An approach for authenticating users

## 1. src/index.js
```Javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'))
```

## 2. src/App.js
```Javascript
import React, { Component } from "react";
import axios from "axios";

class App extends Component {
  state = {
    user: null
  };

  componentDidMount() {
    // When the app loads, try and get the current user
  }

  setUser = user => {
    // Set the current user into state.
  };

  getCurrentUser = () => {
    // 1. Try and retrieve the user's token
    // 2. If they have a token, make a request to /user/current for their user details
    // 3. Pass the token as an Authorization Header
    // 4. If a successful response returns, store the user in state.
  };
  render() {
    // 1. Add React-Router to control what view the user sees
    // 2. If there is an active user in state, send them to the dashboard.
    // 3. If there's no user, send them to the login screen.
    // 4. If a logged in user tries to hit the login screen, redirect them to the dashboard.
    return (
      <div className="App">
        <h1>Authentication App</h1>
      </div>
    );
  }
}

export default App;
```

## 3. src/services/tokenService.js
```Javascript
export const setToken = token => {
  // set an item in local storage called "token" and set it equal to any value we pass to it
};

export const getToken = () => {
  // retrieve our token from local storage
};

export const removeToken = () => {
  // remove our token from local storage
};
```

## 4. src/components/Dashboard.js
```Javascript
import React from "react";
import axios from "axios";
import { getToken } from "../services/tokenService";

class Dashboard extends React.Component {
  state = {
    todo: "",
    todos: []
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  componentDidMount() {
    // 1. When the dashboard loads, get the user's token
    // 2. Send a GET request to /todo and pass the token to grab a list of ONLY this user's todos
    // 3. If we get a successful response, store the todos in state.
  }

  handleSubmit = e => {
    e.preventDefault();
    const { todo } = this.state;

    // 1. Get the user's token
    // 2. Send a POST to /todo with
    //  a - the body containing the TODO we wish to post
    //  b - the Authorization Header Bearer <token>
  };

  render() {
    return (
      <div>
        <h1>Dashboard</h1>
        <form onSubmit={this.handleSubmit}>
          <input name="todo" type="text" onChange={this.handleChange} />
          <button>Add Todo</button>
        </form>
        <ul>
          {this.state.todos.map(todo => {
            return <li>{JSON.stringify(todo, null, 3)}</li>;
          })}
        </ul>
        <button>Logout</button>
      </div>
    );
  }
}

export default Dashboard;
```

## 5. src/components/Login.js
```Javascript
import React, { Component } from "react";
import axios from "axios";
import { setToken } from "../services/tokenService";

class Login extends Component {
  state = {
    email: "",
    password: ""
  };

  handleChange = e => {
    this.setState({ [e.target.name]: e.target.value });
  };

  handleSubmit = e => {
    e.preventDefault();
    const { email, password } = this.state;
    // 1. POST to /auth/login, passing in the email and password in the body
    // 2. If we receive a successful response:
    //  - grab the token from the response
    //  - store it in local storage
    //  - call getCurrentUser
  };
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <div>
          <label htmlFor="login-email">Email: </label>
          <input
            type="email"
            onChange={this.handleChange}
            name="email"
            id="login-email"
            placeholder="email"
          />
        </div>
        <div>
          <label htmlFor="login-password">Password: </label>
          <input
            type="password"
            onChange={this.handleChange}
            name="password"
            id="login-password"
            placeholder="Enter your desired password"
          />
        </div>
        <div>
          <input type="submit" value="Log In" />
        </div>
      </form>
    );
  }
}

export default Login;
```
## 6. src/components/Logout.js
```Javascript
import React from "react";
import { removeToken } from "../services/tokenService";

const Logout = props => {
  const logout = () => {
    // 1. Remove the user's token from local storage.
    // 2. Set the user in state to be equal to null.
  };
  return <button onClick={logout}>Logout</button>;
};

export default Logout;
```
## 7. src/components/Signup.js
```Javascript
import React, { Component } from "react";

class Signup extends Component {
  state = {
    email: "",
    password: ""
  };

  handleChange = e => {
    this.setState({ [e.target.name]: e.target.value });
  };

  handleSubmit = e => {
    e.preventDefault();
    console.log("submitted!");
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <div>
          <label htmlFor="email">Email: </label>
          <input
            type="email"
            onChange={this.handleChange}
            name="email"
            id="email"
            placeholder="email"
          />
        </div>
        <div>
          <label htmlFor="email">Password: </label>
          <input
            type="password"
            onChange={this.handleChange}
            name="password"
            id="password"
            placeholder="Enter your desired password"
          />
        </div>
        <div>
          <input type="submit" value="Signup" />
        </div>
      </form>
    );
  }
}

export default Signup;
```
