5. Create  below task in React
a. Create List of  task in react using state
import React, { useState } from 'react';
import './App.css';
const App = () => {
  const [tasks, setTasks] = useState([
    { id: 1, text: 'Learn React' },
    { id: 2, text: 'Build a Todo List' },
    { id: 3, text: 'Style the Todo List' }
  ]);
  return (
    <div className="task-list-container">
      <h1 className="title">Task List</h1>
      <ul className="task-list">
        {tasks.map(task => (
          <li key={task.id} className="task-item">{task.text}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
b. Style the all elements using css
.task-list-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.title {
  font-size: 2em;
  color: #333;
}

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-item {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  padding: 10px 20px;
  margin: 10px 0;
  border-radius: 5px;
  width: 300px;
  text-align: left;
  font-size: 1.2em;
  color: #555;
  transition: background-color 0.3s;
}

.task-item:hover {
  background-color: #eaeaea;
}
