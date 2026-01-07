## SALAM ALAKUM

## 1. employees → departments JOIN edərək işçi və department adını göstər
```sql
SELECT e.first_name, e.last_name, d.department_name
FROM hr.employees e
JOIN hr.departments d
ON e.department_id = d.department_id;
## 2. Hər bir işçinin job_title-nı göstər
```sql
SELECT e.first_name, e.last_name, j.job_title
FROM hr.employees e
JOIN hr.jobs j
ON e.job_id = j.job_id;
## 3.Adı 6 simvoldan uzun olan işçiləri seç və maaşlarını 12% artır
```sql
SELECT first_name, last_name, salary,
       salary * 1.12 AS increased_salary
FROM hr.employees
WHERE LENGTH(first_name) > 6;
## 4.job_id və salary sütunlarını birlikdə sırala**
```sql
SELECT job_id, salary
FROM hr.employees
ORDER BY job_id, salary;
## 5.Maaşı azdan çoxa, hire_date-i çoxdan aza sırala
```sql
SELECT *
FROM hr.employees
ORDER BY salary ASC, hire_date DESC;
## 6.Bütün department adlarını və işçi sayını göstər
```sql
SELECT d.department_name, COUNT(e.employee_id) AS employee_count
FROM hr.departments d
LEFT JOIN hr.employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
## 7. department_id-si 10 olan departmentin adını tap
```sql
SELECT department_name
FROM hr.departments
WHERE department_id = 10;
## 8.departments → locations JOIN edərək department və şəhər adını göstər
```sql
SELECT d.department_name, l.city
FROM hr.departments d
JOIN hr.locations l
ON d.location_id = l.location_id;
## 9. İşçilərin ad-soyadı və department adını göstər
```sql
SELECT e.first_name, e.last_name, d.department_name
FROM hr.employees e
JOIN hr.departments d
ON e.department_id = d.department_id;
## 10. job_id üzrə orta maaşı hesabla və artan sırala
```sql
SELECT job_id, AVG(salary) AS avg_salary
FROM hr.employees
GROUP BY job_id
ORDER BY avg_salary;
## 11.Department orta maaşından çox qazanan işçiləri tap
```sql
SELECT e.*
FROM hr.employees e
JOIN (
    SELECT department_id, AVG(salary) avg_sal
    FROM hr.employees
    GROUP BY department_id
) a
ON e.department_id = a.department_id
WHERE e.salary > a.avg_sal;
## 12.job_title üzrə minimum və maksimum maaş
```sql
SELECT j.job_title,
       MIN(e.salary) AS min_salary,
       MAX(e.salary) AS max_salary
FROM hr.employees e
JOIN hr.jobs j
ON e.job_id = j.job_id
GROUP BY j.job_title;
## 13.Ən yüksək maaş alan 5 işçi
```sql
SELECT *
FROM hr.employees
ORDER BY salary DESC
FETCH FIRST 5 ROWS ONLY;
## 14.Meneceri olan və olmayan işçilər
```sql
-- Meneceri olanlar
SELECT * FROM hr.employees WHERE manager_id IS NOT NULL;

-- Meneceri olmayanlar
SELECT * FROM hr.employees WHERE manager_id IS NULL;
## 15.Şəhər üzrə ümumi maaş xərci
```sql
SELECT l.city, SUM(e.salary) AS total_salary
FROM hr.employees e
JOIN hr.departments d ON e.department_id = d.department_id
JOIN hr.locations l ON d.location_id = l.location_id
GROUP BY l.city;
## 16.salary > 8000 olan işçilərin job_title və department_name
```sql
SELECT j.job_title, d.department_name
FROM hr.employees e
JOIN hr.jobs j ON e.job_id = j.job_id
JOIN hr.departments d ON e.department_id = d.department_id
WHERE e.salary > 8000;
## 17.Hər manager üçün ümumi maaş xərci
```sql
SELECT manager_id, SUM(salary) AS total_salary
FROM hr.employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id;
## 18. Adı 5 hərfdən uzun olan işçilərin job_title və departmenti
```sql
SELECT e.first_name, j.job_title, d.department_name
FROM hr.employees e
JOIN hr.jobs j ON e.job_id = j.job_id
JOIN hr.departments d ON e.department_id = d.department_id
WHERE LENGTH(e.first_name) > 5;
## 19.hire_date 2003–2006 arası olan işçilərin department adları
```sql
SELECT DISTINCT d.department_name
FROM hr.employees e
JOIN hr.departments d ON e.department_id = d.department_id
WHERE e.hire_date BETWEEN
      TO_DATE('2003-01-01','YYYY-MM-DD')
  AND TO_DATE('2006-12-31','YYYY-MM-DD');
## 20.Eyni maaşa sahib işçiləri qrupla və sayını tap
```sql
SELECT salary, COUNT(*) AS employee_count
FROM hr.employees
GROUP BY salary;
## 21.job_title içində 'Manager' olanların sayı
```sql
SELECT COUNT(*) AS manager_count
FROM hr.jobs
WHERE job_title LIKE '%Manager%';
## 22.Ölkə–şəhər–department–işçi siyahısı
```sql
SELECT c.country_name, l.city,
       d.department_name,
       e.first_name, e.last_name
FROM hr.employees e
JOIN hr.departments d ON e.department_id = d.department_id
JOIN hr.locations l ON d.location_id = l.location_id
JOIN hr.countries c ON l.country_id = c.country_id;
## 23.Hər department üçün ən erkən hire_date
```sql
SELECT department_id, MIN(hire_date) AS earliest_hire
FROM hr.employees
GROUP BY department_id;




## 24. job_id üzrə commission alan işçilərin sayı
```sql
SELECT job_id, COUNT(*) AS commission_count
FROM hr.employees
WHERE commission_pct IS NOT NULL
GROUP BY job_id;


## 25. Hər departmentdə neçə menecer var
```sql
SELECT department_id, COUNT(DISTINCT manager_id) AS manager_count
FROM hr.employees
WHERE manager_id IS NOT NULL
GROUP BY department_id;
## 26. Maaş artımı: salary + 8% + 300 bonus
```sql
SELECT first_name, last_name,
       salary,
       salary * 1.08 + 300 AS new_salary
FROM hr.employees;
## 27. employees → jobs JOIN edərək job_title-ları göstər
```sql
SELECT e.first_name, e.last_name, j.job_title
FROM hr.employees e
JOIN hr.jobs j
ON e.job_id = j.job_id;
## 28. 10% bonusdan sonra maaşı > 12000 olanlar
```sql
SELECT first_name, last_name,
       salary * 1.10 AS new_salary
FROM hr.employees
WHERE salary * 1.10 > 12000;






















