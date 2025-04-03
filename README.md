# Understanding SQL Joins (SQL ಸೇರಿಸುವಿಕೆಗಳ ಅರಿವು)

## 1. What is JOIN? (JOIN ಎಂದರೇನು?)
A `JOIN` in SQL is used to combine records from two or more tables based on a related column. By default, `JOIN` behaves as an `INNER JOIN` unless specified otherwise. Joins help retrieve meaningful data by establishing relationships between tables.

**SQL ನಲ್ಲಿ, `JOIN` ಅನ್ನು ಎರಡು ಅಥವಾ ಹೆಚ್ಚಿನ ಕೋಷ್ಟಕಗಳ ನಡುವಿನ ಸಂಬಂಧಿತ ಕಾಲಮ್ ಆಧರಿಸಿ ದಾಖಲೆಗಳನ್ನು ಸೇರಿಸಲು ಬಳಸಲಾಗುತ್ತದೆ. ಸಾಮಾನ್ಯವಾಗಿ, `JOIN` ಎಂದರೆ `INNER JOIN`. ಇದು ಕೋಷ್ಟಕಗಳ ನಡುವಿನ ಸಂಬಂಧವನ್ನು ಸ್ಥಾಪಿಸಿ ಉಪಯುಕ್ತ ಮಾಹಿತಿಯನ್ನು ಪಡೆಯಲು ಸಹಾಯ ಮಾಡುತ್ತದೆ.**

---

## 2. INNER JOIN (ಆಂತರಿಕ ಸೇರಿಸುವಿಕೆ)
An **INNER JOIN** returns only the rows where there is a match in both tables. If there is no match, the row is excluded from the result.

**INNER JOIN: ಇದು ಎರಡೂ ಕೋಷ್ಟಕಗಳಲ್ಲಿ ಹೊಂದಾಣಿಕೆಯಿರುವ ಪಂಕ್ತಿಗಳನ್ನು ಮಾತ್ರ ನೀಡುತ್ತದೆ. ಹೊಂದಾಣಿಕೆ ಇಲ್ಲದ ಪಂಕ್ತಿಗಳು ಫಿಲ್ಟರ್ ಆಗಿ ಹೋಗುತ್ತವೆ.**

### Syntax (ಸೂತ್ರ)
```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

### Example Scenario (ಉದಾಹರಣೆ)

#### Customers Table (ಗ್ರಾಹಕರ ಕೋಷ್ಟಕ)
| CustomerID | Name      |
|------------|----------|
| 1          | Alice    |
| 2          | Bob      |
| 3          | Charlie  |

#### Orders Table (ಆರ್ಡರ್ ಕೋಷ್ಟಕ)
| OrderID | CustomerID | Product  |
|---------|-----------|----------|
| 101     | 1         | Laptop   |
| 102     | 2         | Phone    |
| 103     | 1         | Mouse    |
| 104     | 4         | Keyboard |

#### INNER JOIN Query:
```sql
SELECT Customers.Name, Orders.Product 
FROM Customers 
INNER JOIN Orders 
ON Customers.CustomerID = Orders.CustomerID;
```

#### INNER JOIN Result:
| Name   | Product  |
|--------|---------|
| Alice  | Laptop  |
| Bob    | Phone   |
| Alice  | Mouse   |

---

## 3. Other Types of Joins (ಬೇರೆಯ JOIN ಪ್ರಕಾರಗಳು)

### LEFT JOIN (ಎಡ ಸೇರಿಸುವಿಕೆ)
Returns all records from the **left table** and matching records from the **right table**. If no match is found, NULL is returned for right table columns.

**LEFT JOIN: ಎಡದ ಕೋಷ್ಟಕದ ಎಲ್ಲಾ ಪಂಕ್ತಿಗಳು ಮತ್ತು ಹೊಂದಾಣಿಕೆಯಿರುವ ಬಲ ಕೋಷ್ಟಕದ ಪಂಕ್ತಿಗಳನ್ನು ತರುತ್ತದೆ. ಹೊಂದಾಣಿಕೆ ಇಲ್ಲದಿದ್ದರೆ, NULL ನೀಡುತ್ತದೆ.**

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

### RIGHT JOIN (ಬಲ ಸೇರಿಸುವಿಕೆ)
Returns all records from the **right table** and matching records from the **left table**. If no match is found, NULL is returned for left table columns.

**RIGHT JOIN: ಬಲದ ಕೋಷ್ಟಕದ ಎಲ್ಲಾ ಪಂಕ್ತಿಗಳು ಮತ್ತು ಹೊಂದಾಣಿಕೆಯಿರುವ ಎಡದ ಕೋಷ್ಟಕದ ಪಂಕ್ತಿಗಳನ್ನು ತರುತ್ತದೆ. ಹೊಂದಾಣಿಕೆ ಇಲ್ಲದಿದ್ದರೆ, NULL ನೀಡುತ್ತದೆ.**

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

### FULL JOIN (ಪೂರ್ಣ ಸೇರಿಸುವಿಕೆ)
Returns all records from both tables. If there is no match, NULL values are returned for missing matches from either table.

**FULL JOIN: ಎರಡೂ ಕೋಷ್ಟಕಗಳ ಎಲ್ಲಾ ಪಂಕ್ತಿಗಳನ್ನು ತರುತ್ತದೆ. ಹೊಂದಾಣಿಕೆ ಇಲ್ಲದಿದ್ದರೆ, NULL ನೀಡುತ್ತದೆ.**

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
FULL JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

### CROSS JOIN (ಕ್ರಾಸ್ ಸೇರಿಸುವಿಕೆ)
Returns the Cartesian product of both tables, meaning each row from the first table is combined with every row from the second table.

**CROSS JOIN: ಪ್ರತಿ ಪಂಕ್ತಿ ಎರಡೂ ಕೋಷ್ಟಕಗಳ ಎಲ್ಲಾ ಪಂಕ್ತಿಗಳೊಂದಿಗೆ ಸಂಯೋಜನೆ ಹೊಂದುತ್ತದೆ.**

```sql
SELECT Customers.Name, Orders.Product
FROM Customers
CROSS JOIN Orders;
```

---

## 4. Advanced Join Concepts (ಆಧುನಿಕ JOIN ತತ್ವಗಳು)

### SELF JOIN (ಸ್ವಯಂ ಸೇರಿಸುವಿಕೆ)
A `SELF JOIN` is when a table is joined with itself. It is useful when comparing rows within the same table.

**SELF JOIN: ಒಂದು ಕೋಷ್ಟಕವನ್ನು ಅದೇ ಕೋಷ್ಟಕದೊಂದಿಗೆ ಜೋಡಿಸುವುದು. ಒಂದು ಕೋಷ್ಟಕದ ಅಂತರ್ರಜ್‌ಜನೆಯ ಪಂಕ್ತಿಗಳನ್ನು ಹೋಲಿಸಲು ಉಪಯುಕ್ತವಾಗಿದೆ.**

```sql
SELECT A.Name AS Employee, B.Name AS Manager
FROM Employees A
INNER JOIN Employees B
ON A.ManagerID = B.EmployeeID;
```

---

## 5. Summary (ಸಾರಾಂಶ)
| Type of Join  | Includes Unmatched Rows? | Source Table with All Records |
|--------------|-------------------------|-------------------------------|
| INNER JOIN  | No                        | Only Matching Rows            |
| LEFT JOIN   | Yes (Left Table)          | Left Table                    |
| RIGHT JOIN  | Yes (Right Table)         | Right Table                   |
| FULL JOIN   | Yes (Both Tables)         | Both Tables                   |
| CROSS JOIN  | No (All Combinations)     | Both Tables                   |
| SELF JOIN   | No (Used for Self-Matching) | Single Table |

---

## 6. Conclusion (ತೀರ್ಮಾನ)
SQL joins are essential for working with relational databases. Understanding the different types of joins and their use cases helps in efficient query writing and data retrieval.

**SQL ಸೇರಿಸುವಿಕೆಗಳು ಸಂಬಂಧಿತ ಡೇಟಾಬೇಸ್‌ಗಳನ್ನು ನಿರ್ವಹಿಸಲು ಬಹಳ ಅಗತ್ಯ. ವಿವಿಧ JOIN ಪ್ರಕಾರಗಳ ಅರಿವಿನಿಂದ ಉತ್ತಮ ಕಾರ್ಯಕ್ಷಮತೆಗೊಳಿಸಿ ಪ್ರಭಾವೀ ಪ್ರಕ್ರಿಯೆಗಳನ್ನು ಬರೆಯಬಹುದು.**

🚀 *Happy Querying!* (ನಿಮ್ಮ SQL ಪ್ರಶ್ನೆಗಳ ಸಂತೋಷದಯಿ ಬರವಣಿಗೆಗೆ ಶುಭಾಶಯಗಳು!)

[![Video Title](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID/0.jpg)](https://youtu.be/7mz73uXD9DA?t=4207&si=zcukn2py0A9dgA_u)

<iframe width="560" height="315" src="https://www.youtube.com/embed/7mz73uXD9DA?si=zcukn2py0A9dgA_u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


