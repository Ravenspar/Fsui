8.Create webpage to using REDUX 
export const FETCH_TASKS_REQUEST = 'FETCH_TASKS_REQUEST';
export const FETCH_TASKS_SUCCESS = 'FETCH_TASKS_SUCCESS';
export const FETCH_TASKS_FAILURE = 'FETCH_TASKS_FAILURE';

export const fetchTasksRequest = () => ({
  type: FETCH_TASKS_REQUEST,
});

export const fetchTasksSuccess = tasks => ({
  type: FETCH_TASKS_SUCCESS,
  payload: tasks,
});

export const fetchTasksFailure = error => ({
  type: FETCH_TASKS_FAILURE,
  payload: error,
});

export const fetchTasks = () => {
  return async dispatch => {
    dispatch(fetchTasksRequest());
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=10');
      const data = await response.json();
      dispatch(fetchTasksSuccess(data));
    } catch (error) 
import { FETCH_TASKS_REQUEST, FETCH_TASKS_SUCCESS, FETCH_TASKS_FAILURE } from './actions';

const initialState = {
  loading: false,
  tasks: [],
  error: '',
};

const taskReducer = (state = initialState, action) => {
  switch (action.type) {
    case FETCH_TASKS_REQUEST:
      return {
        ...state,
        loading: true,
      };
    case FETCH_TASKS_SUCCESS:
      return {
        loading: false,
        tasks: action.payload,
        error: '',
      };
    case FETCH_TASKS_FAILURE:
      return {
        loading: false,
        tasks: [],
        error: action.payload,
      };
    default:
      return state;
  }
};

export default taskReducer; {
      dispatch(fetchTasksFailure(error.message));
    }
  };
};
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import { composeWithDevTools } from 'redux-devtools-extension';
import taskReducer from './reducers';

const store = createStore(taskReducer, composeWithDevTools(applyMiddleware(thunk)));

export default store;
import React, { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchTasks } from './redux/actions';
import './TaskList.css';

const TaskList = () => {
  const dispatch = useDispatch();
  const { loading, tasks, error } = useSelector(state => state);

  useEffect(() => {
    dispatch(fetchTasks());
  }, [dispatch]);

  return (
    <div className="task-list-container">
      <h1 className="title">Task List</h1>
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

export default TaskList;
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

.error {
  color: red;
}

