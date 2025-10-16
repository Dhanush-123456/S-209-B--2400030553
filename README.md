import React, { useState } from "react";

const employeesData = [
  { name: "DHANUSH", department: "HR", salary: 100000 },
  { name: "SANDHYA", department: "MARKETING", salary: 50000 },
  { name: "VENKY", department: "PR", salary: 18000 },
  { name: "HARINI", department: "PR", salary: 155000 },
];

function SortableTable() {
  const [data, setData] = useState(employeesData);
  const [sortConfig, setSortConfig] = useState({ key: null, direction: "asc" });

  const handleSort = (key) => {
    let direction = "asc";
    if (sortConfig.key === key && sortConfig.direction === "asc") {
      direction = "desc";
    }const sortedData = [...data].sort((a, b) => {
      if (a[key] < b[key]) return direction === "asc" ? -1 : 1;
      if (a[key] > b[key]) return direction === "asc" ? 1 : -1;
      return 0;
    });

    setData(sortedData);
    setSortConfig({ key, direction });
    };
