
to do list 

app

import React from "react";
import TodoFunctional from "./TodoFunctional";
import TodoClass from "./TodoClass";

function App() {
  return (
    <div>
      <TodoFunctional />
      <hr />
      <TodoClass />
    </div>
  );
}

export default App;




class 

import React, { Component } from "react";

class TodoClass extends Component {
  constructor(props) {
    super(props);
    this.state = {
      todos: [
        { id: 1, task: "Learn React" },
        { id: 2, task: "Complete Assignment" }
      ],
      newTask: ""
    };
  }

  // Handle input
  handleChange = (e) => {
    this.setState({ newTask: e.target.value });
  };

  // Add task
  addTask = () => {
    if (this.state.newTask.trim() === "") return;

    this.setState({
      todos: [
        ...this.state.todos,
        { id: Date.now(), task: this.state.newTask }
      ],
      newTask: ""
    });
  };

  // Delete task
  deleteTask = (id) => {
    this.setState({
      todos: this.state.todos.filter(todo => todo.id !== id)
    });
  };

  render() {
    return (
      <div>
        <h2>To-Do List (Class Component)</h2>

        <input
          type="text"
          placeholder="Enter task"
          value={this.state.newTask}
          onChange={this.handleChange}
        />
        <button onClick={this.addTask}>Add</button>

        <ul>
          {this.state.todos.map(todo => (
            <li key={todo.id}>
              {todo.task}
              <button onClick={() => this.deleteTask(todo.id)}>
                Delete
              </button>
            </li>
          ))}
        </ul>
      </div>
    );
  }
}

export default TodoClass;






function 

import React, { useState } from "react";

function TodoFunctional() {
  const [todos, setTodos] = useState([
    { id: 1, task: "Learn React" },
    { id: 2, task: "Complete Assignment" }
  ]);

  const [newTask, setNewTask] = useState("");

  // Add task
  const addTask = () => {
    if (newTask.trim() === "") return;

    setTodos([
      ...todos,
      { id: Date.now(), task: newTask }
    ]);
    setNewTask("");
  };

  // Delete task
  const deleteTask = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };

  return (
    <div>
      <h2>To-Do List (Functional Component)</h2>

      <input
        type="text"
        placeholder="Enter task"
        value={newTask}
        onChange={(e) => setNewTask(e.target.value)}
      />
      <button onClick={addTask}>Add</button>

      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            {todo.task}
            <button onClick={() => deleteTask(todo.id)}>
              Delete
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoFunctional;







products 

app 

import React from "react";

import CounterClass from './CounterClass';
import CounterFunction from './CounterFunction';

// function app and return
function App() {
  return (
    <div>
      <h1>Counter Application</h1>
      <CounterClass/>
      <CounterFunction/>
    </div>
  );
}

export default App;


class

import React from "react";

class CounterClass extends React.Component {
    state = {
        products: [
            { id: 1, name: "Laptop" },
            { id: 2, name: "Mobile" }
        ],
        newProduct: ""
    };

    addProduct = () => {
        const { newProduct, products } = this.state;
        if (newProduct.trim()) {
            this.setState({
                products: [...products, { id: Date.now(), name: newProduct }],
                newProduct: ""
            });
        }
    };

    render() {
        const { products, newProduct } = this.state;
        return (
            <div>
                <h2>Class Component</h2>
                <input
                    type="text"
                    value={newProduct}
                    onChange={e => this.setState({ newProduct: e.target.value })}
                    placeholder="Enter product"
                />
                <button onClick={this.addProduct}>Add</button>
                <ul>
                    {products.map(p => (
                        <li key={p.id}>
                            {p.name}
                            <button onClick={() => this.setState({ products: products.filter(x => x.id !== p.id) })}>Delete</button>
                        </li>
                    ))}
                </ul>
            </div>
        );
    }
}

export default CounterClass;


function 



import React, { useState } from "react";

function CounterFunction() {
    const [products, setProducts] = useState([
        { id: 1, name: "Laptop" },
        { id: 2, name: "Mobile" }
    ]);
    const [newProduct, setNewProduct] = useState("");

    const addProduct = () => {
        newProduct.trim() && setProducts([...products, { id: Date.now(), name: newProduct }]) && setNewProduct("");
    };

    return (
        <div>
            <h2>Functional Component</h2>
            <input
                type="text"
                value={newProduct}
                onChange={(e) => setNewProduct(e.target.value)}
                placeholder="Enter product"
            />
            <button onClick={addProduct}>Add</button>
            <ul>
                {products.map(product => (
                    <li key={product.id}>
                        {product.name}
                        <button onClick={() => setProducts(products.filter(p => p.id !== product.id))}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}

export default CounterFunction;






import React from "react";

import CounterClass from './CounterClass';
import CounterFunction from './CounterFunction';

// function app and return
function App() {
  return (
    <div>
      <h1>Counter Application</h1>
      <CounterClass/>
      <CounterFunction/>
    </div>
  );
}

export default App;




import React, { Component } from "react";

class CounterClass extends Component {
    constructor(props) {
        super(props);
        this.state = {count: null};
    }

    componentDidMount() {
        setTimeout( () => {
            this.setState({ count: 0 });
        }, 2);
    }

    render() {
        const { count } = this.state;
        if(count === null) return <h2>Loading Counter...</h2>;

        return (
            <div>
                <h2>Class Counter : {count}</h2>
                <button onClick={() => this.setState({count: count + 1})}>Increment</button>
                <button onClick={() => this.setState({count: count - 1})}>Decrement</button>
                <button onClick={() => this.setState({count: count * 2})}>Double</button>
                <button onClick={() => this.setState({count: 0})}>Reset</button>
            </div>
        );
    }
}

export default CounterClass;



import React, { useState, useEffect } from "react";

function CounterFunction() {

    // count
    const [count, setCount] = useState(null);

    // useEffect
    useEffect(() => {
        const timer = setTimeout(() => {
            setCount(0);
        }, 2);

        return () => clearTimeout(timer);
    }, []);

    // print loading when null
    if (count === null) return <h2>Loading Counter...</h2>

    // return buttons   
    return (
        <div>
            <h2>Function Counter: {count}</h2>
            <button onClick={() => setCount(count + 1)}>Increment</button>
            <button onClick={() => setCount(count - 1)}>Decrement</button>
            <button onClick={() => setCount(count * 2)}>Double</button>
            <button onClick={() => setCount(0)}>Reset Counter</button>
        </div>
    );
}

export default CounterFunction;

mport express from "express";
import cors from "cors";
import products from "./product.js";
import { ApolloServer } from "@apollo/server";
import { startStandaloneServer } from "@apollo/server/standalone";

//  connections
const app = express();
const PORT = 4000;

//  middleware
app.use(express.json());
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
app.use(cors());

//  rest api
// root
app.get("/", (req, res) => {
    res.send("Hello express");
});

// get products
app.get("/products", (req, res) => {
    res.json(products);
})

// get 1 product
app.get("/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if(!product) return res.status(404).json({error: "not found"});
    res.json(product);
});

// add new product
app.post("/products", (req, res) => {
    const product = {
        id: products.length + 1,
        ...req.body
    };

    products.push(product);
    res.status(201).json(product);
});

// update product
app.put("/products/:id", (req, res) => {
    const product = products.find(p => p.id === parseInt(req.params.id));
    if(!product) return res.status(404).json({error: "not found"});
    Object.assign(product, req.body);
    res.json(product);
});

// delete product
app.delete("/products/:id", (req, res) => {
    const index = products.findIndex(p => p.id === parseInt(req.params.id));
    if(index === -1) return res.status(404).json({error: "not found"});
    const deleted = products.splice(index, 1);
    res.json(deleted[0]);
});

// listen
app.listen(PORT, () => console.log(`REST API running on http://localhost:${PORT}`));


//  graphql
const typeDefs = `#graphql

    type Product {
        id: Int
        name: String
        price: Float
    }

    type Query {
        products: [Product]
        product(id: Int!): Product
    }

    type Mutation {
        addProduct(name: String!, price: Float!): Product
        updateProduct(id: Int!, name: String, price: Float): Product
        deleteProduct(id: Int!): Product
    }
`;

const resolvers = {
    
    Query: {
        products: () => products,
        product: (_, {id}) => products.find(p => p.id === id)
    },

    Mutation: {
        addProduct: (_, {name, price}) => {
            const newProduct = {id: products.length + 1, name, price}
            products.push(newProduct);
            return newProduct;
        },

        updateProduct: (_, {id, name, price}) => {
            const product = products.find(p => p.id === id);
            if(!product) return null;
            if(name) product.name = name;
            if(price) product.price = price;
            return product;
        },

        deleteProduct: (_, {id}) => {
            const index = products.findIndex(p => p.id === id);
            if(index === -1) return null;
            return products.splice(index, 1)[0]; 
        }
    }
};


async function startGQL() {
    const server = new ApolloServer({ typeDefs, resolvers });
    const { url } = await startStandaloneServer(server, {listen: {port: 5000}});
    console.log(`Graphql is running on :${url}`);
}

startGQL();



product.js

let products = [
    {id: 1, name: "Laptop", price: 5000},
    {id: 2, name: "Mobile", price: 7000}
];

export default products;
