# SQL Part 2. Join Tables

### 1. Join data from EMP and DEPT using WHERE clause
```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, D.DNAME, D.LOC
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO;
```

### 2. Join data from EMP and DEPT using INNER JOIN
```sql
SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, D.DNAME, D.LOC
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### 3. Select employee name and department name for all employees in alphabetical order
```sql
SELECT E.ENAME, D.DNAME
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO
ORDER BY E.ENAME ASC;
```

### 4. Find all employees with their numbers and names of departments they work in
```sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### 5. Select employee name, job and department name for all employees who earn more than 1500
```sql
SELECT E.ENAME, E.JOB, D.DNAME
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL > 1500;
```

### 6. Get a list of employees with name, job, salary and earning class (table SALGRADE)
```sql
SELECT E.ENAME, E.JOB, E.SAL, S.GRADE
FROM EMP E
INNER JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL;
```

### 7. Select all information for employees in 3rd earning class
```sql
SELECT E.*
FROM EMP E
INNER JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE S.GRADE = 3;
```

### 8. Find employees who work in Dallas
```sql
SELECT E.ENAME
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE D.LOC = 'DALLAS';
```

### 9. For each employee select his name, department name and earning class
```sql
SELECT E.ENAME, D.DNAME, S.GRADE
FROM EMP E
INNER JOIN DEPT D ON E.DEPTNO = D.DEPTNO
INNER JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL;
```

### 10. Find all employees with their numbers and names of departments they work in. Include departments without any employees
```sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM DEPT D
LEFT JOIN EMP E ON D.DEPTNO = E.DEPTNO;
```

### 11. Find all employees with their numbers and names of departments they work in. Include employees without departments
```sql
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMP E
LEFT JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### 12. Find employees (name, department number) from departments 20 and 30
```sql
SELECT E.ENAME, E.DEPTNO
FROM EMP E
WHERE E.DEPTNO IN (20, 30);
```

### 13. List jobs appearing in departments 10 and 30
```sql
SELECT DISTINCT E.JOB
FROM EMP E
WHERE E.DEPTNO IN (10, 30);
```

### 14. List jobs appearing in department 10 or 30 (or both)
```sql
SELECT DISTINCT E.JOB
FROM EMP E
WHERE E.DEPTNO = 10
   OR E.DEPTNO = 30;
```

### 15. List jobs appearing in department 10 but not in department 30
```sql
SELECT DISTINCT E.JOB
FROM EMP E
WHERE E.DEPTNO = 10
  AND E.JOB NOT IN (SELECT DISTINCT JOB FROM EMP WHERE DEPTNO = 30);
```

### 16. Find employees who earn less than their managers
```sql
SELECT E.ENAME AS Employee, M.ENAME AS Manager, E.SAL AS Employee_Salary, M.SAL AS Manager_Salary
FROM EMP E
JOIN EMP M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL;
```

### 17. For each employee show his name and name of the manager. Sort results by managers name
```sql
SELECT E.ENAME AS Employee, M.ENAME AS Manager
FROM EMP E
LEFT JOIN EMP M ON E.MGR = M.EMPNO
ORDER BY M.ENAME;
```
