import React, { useState, useEffect } from "react";
import "./style.css";

export default function App() {
    const [tasks, setTasks] = useState([]);
    const [taskInput, setTaskInput] = useState('');

  useEffect(() => {
    const storedTasks = JSON.parse(localStorage.getItem('tasks'));
    if (storedTasks) {
      setTasks(storedTasks);
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('tasks', JSON.stringify(tasks));
  }, [tasks]);

  const addTask = (e) => {
    e.preventDefault();
    if (taskInput.trim() === '') return;

    const newTask = {
      id: Date.now(),
      text: taskInput,
      completed: false,
    };
    setTasks([...tasks, newTask]);
    setTaskInput('');
  };

  const toggleTaskCompletion = (id) => {
    const updatedTasks = tasks.map((task) => 
      task.id === id ? { ...task, completed: !task.completed } : task
    );
    setTasks(updatedTasks);
  };

  const removeTask = (id) => {
    const updatedTasks = tasks.filter((task) => task.id !== id);
    setTasks(updatedTasks);
  };

  return (
    <div className="App">
      <h1>To-Do List</h1>
      <form onSubmit={addTask}>
        <input 
          type="text" 
          value={taskInput} 
          onChange={(e) => setTaskInput(e.target.value)} 
          placeholder="Add a new task" 
        />
        <button type="submit">Add Task</button>
      </form>
      <ul>
        {tasks.map((task) => (
          <li key={task.id} style={{ textDecoration: task.completed ? 'line-through' : 'none' }}>
            <span onClick={() => toggleTaskCompletion(task.id)}>{task.text}</span>
            <button onClick={() => removeTask(task.id)}>Remove</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
