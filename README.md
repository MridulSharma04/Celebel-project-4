#import React, { useState } from "react";
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";
import {
  LineChart, Line, XAxis, YAxis, Tooltip, CartesianGrid, ResponsiveContainer
} from "recharts";

const data = [
  { name: 'Jan', uv: 400 },
  { name: 'Feb', uv: 300 },
  { name: 'Mar', uv: 200 },
  { name: 'Apr', uv: 278 },
  { name: 'May', uv: 189 }
];

const Table = () => (
  <div className="p-4">
    <h2 className="text-xl font-semibold mb-4">User Table</h2>
    <table className="min-w-full border text-sm">
      <thead className="bg-gray-100">
        <tr>
          <th className="py-2 px-4 border">ID</th>
          <th className="py-2 px-4 border">Name</th>
          <th className="py-2 px-4 border">Email</th>
        </tr>
      </thead>
      <tbody>
        {[1, 2, 3].map(id => (
          <tr key={id}>
            <td className="py-2 px-4 border">{id}</td>
            <td className="py-2 px-4 border">User {id}</td>
            <td className="py-2 px-4 border">user{id}@example.com</td>
          </tr>
        ))}
      </tbody>
    </table>
  </div>
);

const Chart = () => (
  <div className="p-4">
    <h2 className="text-xl font-semibold mb-4">Sales Chart</h2>
    <ResponsiveContainer width="100%" height={300}>
      <LineChart data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis dataKey="name" />
        <YAxis />
        <Tooltip />
        <Line type="monotone" dataKey="uv" stroke="#6366f1" strokeWidth={2} />
      </LineChart>
    </ResponsiveContainer>
  </div>
);

const Calendar = () => (
  <div className="p-4">
    <h2 className="text-xl font-semibold mb-4">Calendar</h2>
    <p className="text-gray-600">Integrate with a calendar library like <code>react-calendar</code> or <code>fullcalendar</code>.</p>
  </div>
);

const Kanban = () => (
  <div className="p-4">
    <h2 className="text-xl font-semibold mb-4">Kanban Board</h2>
    <div className="grid grid-cols-3 gap-4">
      {['To Do', 'In Progress', 'Done'].map(stage => (
        <div key={stage} className="bg-gray-100 p-3 rounded shadow-sm">
          <h3 className="font-medium mb-2">{stage}</h3>
          <div className="bg-white p-2 rounded shadow">Example Task</div>
        </div>
      ))}
    </div>
  </div>
);

const ThemeToggle = ({ theme, onToggle }) => (
  <button
    onClick={onToggle}
    className="fixed top-4 right-4 px-4 py-2 bg-indigo-600 text-white rounded shadow"
  >
    {theme === 'light' ? 'Switch to Dark' : 'Switch to Light'}
  </button>
);

const Layout = ({ children, theme, onToggle }) => (
  <div className={`${theme === 'dark' ? 'bg-gray-900 text-white' : 'bg-white text-gray-900'} min-h-screen transition-colors`}>
    <nav className="p-4 border-b flex gap-4 text-sm">
      <Link to="/">Home</Link>
      <Link to="/table">Table</Link>
      <Link to="/chart">Chart</Link>
      <Link to="/calendar">Calendar</Link>
      <Link to="/kanban">Kanban</Link>
    </nav>
    <ThemeToggle theme={theme} onToggle={onToggle} />
    <main className="p-4">{children}</main>
  </div>
);

const DashboardApp = () => {
  const [theme, setTheme] = useState("light");
  const toggleTheme = () => setTheme(prev => (prev === "light" ? "dark" : "light"));

  return (
    <Router>
      <Layout theme={theme} onToggle={toggleTheme}>
        <Routes>
          <Route path="/" element={<h2 className="text-xl font-semibold">Welcome to the Admin Dashboard</h2>} />
          <Route path="/table" element={<Table />} />
          <Route path="/chart" element={<Chart />} />
          <Route path="/calendar" element={<Calendar />} />
          <Route path="/kanban" element={<Kanban />} />
        </Routes>
      </Layout>
    </Router>
  );
};

export default DashboardApp;
