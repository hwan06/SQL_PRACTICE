# SQL 연습 문제

### 1. 연봉이 12000 이상되는 직원들의 last_name 및 연봉을 조회한다.   
select last_name, salary    
from employees    
where salary >= 12000;   
    
---    
    
### 2. 사원번호가 176인 사람의 last_name 과 부서 번호를 조회한다.   
select last_name, department_id    
from employees     
where employee_id = 176;   
    
---    
    
### 3. 연봉이 5000에서 12000의 범위 이외인 사람들의 last_name 및 연봉을 조회한다.   
select last_name, salary    
from employees    
where salary < 5000 or salary > 12000;     
where not salary between 5000 and 12000;     
    
---    
    
### 4. 2002/02/20 일부터 2008/05/01 사이에 고용된 사원들의 last_name, 사번, 고용일자를 조회한다.       
-- 		고용일자 순으로 정렬한다.    
select last_name, employee_id, hire_date    
from employees    
where hire_date between '2002/02/20' and '2008/05/01'       
where hire_date >= '2002/02/20' and hire_date <= '2008/05/01'       
order by hire_date asc;      
    
---    
    
### 5. 20 번 및 50번 부서에서 근무하는 모든 사원들의 last_name 및 부서 번호를 조회한다.       
--		last_name의 알파벳순으로 정렬     
select last_name, department_id     
from employees     
where department_id in(20,50)     
order by last_name;     
      
---    
    
### 6. 20번 및 50번 부서에 근무하며, 연봉이 5000 ~ 12,000 사이인 사원들의 last_name 및 연봉을 조회한다.    
select last_name, salary    
from employees    
where department_id in(20,50) and salary >= 5000 and salary <= 12000;    
    
---    
    
### 7. 2004년도에 고용된 모든 사람들의 last_name 및 고용일을 조회한다.    
select last_name, hire_date      
from employees     
where hire_date like '04%';     
where hire_date between '2004/01/01' and '2004/12/31';    
    
---    
    
### 8-1. 매니저가 없는 사람들의 LAST_NEME 및 JOB_ID를 조회한다    
SELECT LAST_NAME, JOB_ID    
FROM EMPLOYEES    
WHERE MANAGER_ID IS NULL;    
WHERE MANAGER_ID = '';    
    
---    
    
### 8-2. 매니저가 있는 사람들의 LAST_NEME 및 JOB_ID를 조회한다    
SELECT LAST_NAME, JOB_ID    
FROM EMPLOYEES    
WHERE MANAGER_ID IS NOT NULL;    
WHERE MANAGER_ID != '';        
    
---    
    
### 9. 커미션을 버는 모든 사원들의 LAST_NAME, 연봉 및 커미션을 조회한다.    
#### 연봉 역순, 커미션 역순차로 정렬한다.    
SELECT LAST_NAME, SALARY, COMMISSION_PCT    
FROM EMPLOYEES    
WHERE COMMISSION_PCT IS NOT NULL    
ORDER BY SALARY DESC , COMMISSION_PCT DESC;    
    
---      
    
### 10. LAST_NAME 의 네번째 글자가 a 인 사람들의 LAST_NAME를 조회한다.
SELECT LAST_NAME
FROM EMPLOYEES
WHERE LAST_NAME LIKE '___a%';

---    

### 11. LAST_NAME에 a및(OR), e 글자가 있는 사람들의 LAST_NAME을 조회한다.    
SELECT LAST_NAME    
FROM EMPLOYEES    
WHERE LAST_NAME LIKE '%a%' OR LAST_NAME LIKE '%e%';    
    
---    
    
### 12. 연봉이 2500, 3500, 7000이 아니며 직업이 SA_REP이나 ST_CLERK인 사람들을 조회한다.      
SELECT LAST_NAME, SALARY, JOB_ID     
FROM EMPLOYEES     
WHERE SALARY NOT IN(2500, 3500, 7000) AND JOB_ID = 'SA_PEP' OR JOB_ID = 'ST_CLERK';     
     
---    
     
### 13. 직업이 AD_PRES인 사람은 A등급, ST_MAN인 사람은 B등급, IT_PROG 인 사람은 C등급, SA_REP 인사람은 D등급을, ST_CLERK인 사람은 E등급 나머진 0      
SELECT JOB_ID, DECODE(JOB_ID, 'AD_PRES','A','ST_MAN','B','IT_PROG','C','SA_REP','D','ST_CLERK','E','0')      
FROM EMPLOYEES;     
      
---    
     
### 14. 모든 사원들의 LAST_NAME, 부서 이름 및 부서 번호를 조회한다.      
SELECT E.LAST_NAME, D.DEPARTMENT_NAME, D.DEPARTMENT_ID      
FROM EMPLOYEES E, DEPARTMENTS D     
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID;     
     
---    
     
### 15. 부서번호 30내의 모든 직업들을 유일한 포맷(중복제거)으로 조회한다. (90 부서 또한 포함한다.)    
#### JOB_ID, DEPARTMENT_ID, DEPARTMENT_NAME를 출력하고 JOB_ID 오름차순으로 정렬하시오       
SELECT DISTINCT E.JOB_ID, D.DEPARTMENT_ID, D.DEPARTMENT_NAME    
FROM EMPLOYEES E, DEPARTMENTS D     
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND D.DEPARTMENT_ID IN (30, 90)      
ORDER BY E.JOB_ID;     
    
---    
    
### 16-1. 커미션을 버는 모든 사람들의 last_name, 부서 명, 지역 id 및 도시명을 검색한다.    
SELECT E.LAST_NAME, D.DEPARTMENT_NAME, L.LOCATION_ID, L.CITY    
FROM EMPLOYEES E, DEPARTMENTS D, LOCATIONS L     
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND D.LOCATION_ID = L.LOCATION_ID    
AND COMMISSION_PCT IN NOT NULL;    
     
---    
     
### 16-2. 옥스포드에 사는 사람 중 커미션을 버는 모든 사람들의 last_name, 부서명, 지역 id 및 도시명을 검색한다.     
SELECT E.LAST_NAME, D.DEPARTMENT_NAME, L.LOCATION_ID, L.CITY    
FROM EMPLOYEES E, DEPARTMENTS D, LOCATIONS L     
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND D.LOCATION_ID = L.LOCATION_ID       
AND CITY = 'Oxford' AND COMMISSION_PCT IS NOT NULL;     

---

### 16-2(서브쿼리)
SELECT E.LAST_NAME, D.DEPARTMENT_NAME, L.LOCATION_ID, L.CITY   
FROM EMPLOYEES E, DEPARTMENTS D, LOCATIONS L     
WHERE E.DEPARTMENT_ID = D.DEPARTMENT_ID AND D.LOCATION_ID = L.LOCATION_ID    
AND COMMISSION_PCT IS NOT NULL     
AND D.LOCATION_ID = (SELECT LOCATION_ID      
			FROM LOCATIONS    
			WHERE CITY = 'Oxford');


---

### 17. LAST_NAME 이 Davies 인 사람보다 후에 고용된 사원들의 LAST_NAME 및 HIRE_DATE를 조회한다.					
SELECT LAST_NAME, HIRE_DATE   
FROM EMPLOYEES    
WHERE (SELECT HIRE_DATE     
		FROM EMPLOYEES     
		WHERE LAST_NAME = 'Davies') < HIRE_DATE;
