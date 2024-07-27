7. Create API and display API in page on the basis of events.
import React, { useState } from 'react';
import './TaskFetcher.css';

const TaskFetcher = () => {
  const [tasks, setTasks] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchTasks = async () => {
    setLoading(true);
    setError(null);
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=10');
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      const data = await response.json();
      setTasks(data);
    } catch (error) {
      setError(error.message);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="task-fetcher-container">
      <h1 className="title">Task List</h1>
      <button className="fetch-button" onClick={fetchTasks}>
        Fetch Tasks
      </button>
      {loading && <p>Loading...</p>}
      {error && <p className="error">{error}</p>}
      <ul className="task-list">
        {tasks.map(task => (
          <li key={task.id} className="task-item">{task.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default TaskFetcher;

.task-fetcher-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.title {
  font-size: 2em;
  color: #333;
}

.fetch-button {
  padding: 10px 20px;
  margin: 20px 0;
  font-size: 1em;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.fetch-button:hover {
  background-color: #0056b3;
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

.error {
  color: red;
}