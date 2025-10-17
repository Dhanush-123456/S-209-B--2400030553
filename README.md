import React, { useState, useMemo } from "react";

const employeesData = [
  { name: "DHANUSH", department: "HR", salary: 100000 },
  { name: "SANDHYA", department: "MARKETING", salary: 50000 },
  { name: "VENKY", department: "PR", salary: 18000 },
  { name: "HARINI", department: "PR", salary: 155000 },
];

export default function SortableTable() {
  const [sort, setSort] = useState({ key: null, dir: "asc" });
  const toggle = (k) =>
    setSort((s) => ({ key: k, dir: s.key === k && s.dir === "asc" ? "desc" : "asc" }));

  const data = useMemo(() => {
    if (!sort.key) return employeesData;
    return [...employeesData].sort((a, b) => {
      const A = a[sort.key], B = b[sort.key];
      if (typeof A === "number") return sort.dir === "asc" ? A - B : B - A;
      const cmp = String(A).localeCompare(String(B), undefined, { sensitivity: "base" });
      return sort.dir === "asc" ? cmp : -cmp;
    });
  }, [sort]);

  const ind = (k) => (sort.key === k ? (sort.dir === "asc" ? " ▲" : " ▼") : "");

  return (
    <div>
      <h2>Employees</h2>
      <table>
        <thead>
          <tr>
            <th onClick={() => toggle("name")}>Name{ind("name")}</th>
            <th onClick={() => toggle("department")}>Department{ind("department")}</th>
            <th onClick={() => toggle("salary")}>Salary{ind("salary")}</th>
          </tr>
        </thead>
        <tbody>
          {data.map((e, i) => (
            <tr key={i}>
              <td>{e.name}</td>
              <td>{e.department}</td>
              <td>{e.salary.toLocaleString()}</td>
            </tr>
          ))}
        </tbody>
      </table>
      <button onClick={() => setSort({ key: null, dir: "asc" })}>Reset</button>
    </div>
  );
}
