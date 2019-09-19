# PPAS 兼容性说明 {#concept_hql_wyg_wdb .concept}

本文通过示例让Oracle 用户可以快速了解PPAS数据库中的术语及概念，以便在迁移及开发过程中提高效率。

以下所有操作基于一个基础模型，通过此模型用户可以看到 RDS for PPAS 中最基本的创建数据库、创建数据表、管理用户等操作，基础数据模型如下：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7867/15688581842983_zh-CN.png)

同时，为了模拟 Oracle 上类似的环境，我们会建立一名字为 orcl\_ppas 的数据库（database），在此数据库中建立名为 scott 的用户，并建立与这个用户同名的 schema 用户空间。

## PPAS兼容性手册 {#section_ort_1zg_wdb .section}

关于PPAS兼容性说明的完整内容，请参见[阿里云PPAS兼容性手册](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/26171/cn_zh/1515464223924/%E9%98%BF%E9%87%8C%E4%BA%91PPAS%E5%85%BC%E5%AE%B9%E6%89%8B%E5%86%8C.pdf)。

## 连接数据库 psql {#section_pnh_czg_wdb .section}

``` {#codeblock_lmt_haf_271}
 psql -h ppasaddress.ppas.rds.aliyuncs.com -p 3433 -U myuser -d template1
   用户 myuser 的口令：
   psql.bin (9.4.1.3, 服务器 9.3.5.14)
   输入 "help" 来获取帮助信息.
   template1=>
```

## 创建并连接数据库 CREATE DATABASE {#section_d2b_2zg_wdb .section}

``` {#codeblock_53a_9z4_f2v}
 template1=> CREATE DATABASE orcl_ppas;
   CREATE DATABASE
   template1=> \c orcl_ppas
   psql.bin (9.4.1.3, 服务器 9.3.5.14)
```

## 创建普通用户 CREATE ROLE {#section_spq_fzg_wdb .section}

``` {#codeblock_why_sg6_oao}
  orcl_ppas=> CREATE ROLE scott LOGIN PASSWORD 'scott123';
   CREATE ROLE
```

## 创建用户的私有空间 CREATE SCHEMA {#section_isj_hzg_wdb .section}

``` {#codeblock_jxh_phc_das}
   orcl_ppas=> CREATE SCHEMA scott;
   CREATE SCHEMA
   orcl_ppas=> GRANT scott TO myuser;
   GRANT ROLE
   orcl_ppas=> ALTER SCHEMA scott OWNER TO scott;
   ALTER SCHEMA
   orcl_ppas=> REVOKE scott FROM myuser;
   REVOKE ROLE
```

**说明：** 

-   如果在进行`ALTER SCHEMA scott OWNER TO scott` 之前没有将scott加入到myuser角色，将会出现如下权限问题。`ERROR:must be member of role "scott"`
-   从安全角度出发，在处理完OWNER的授权后，请将scott用户移出myuser角色以提高安全性。

## 连接到 orcl\_ppas 数据库 {#section_f3j_4zg_wdb .section}

**说明：** 此步骤十分重要，以下所有操作都是在scott账号下进行的，否则所建立的数据表及各种数据库对象将不属于scott用户，导致权限问题。

``` {#codeblock_rvj_8i3_s3l}
[root@localhost bin]# ./psql -h ppasaddress.ppas.rds.aliyuncs.com -p 3433 -U scott -d orcl_ppas
用户 scott 的口令：
psql.bin (9.4.1.3, 服务器 9.3.5.14)
输入 "help" 来获取帮助信息.
orcl_ppas=>
```

## 创建数据表 CREATE TABLE {#section_chb_szg_wdb .section}

``` {#codeblock_ygk_z3c_8z9}
CREATE TABLE dept (
   deptno          NUMBER(2) NOT NULL CONSTRAINT dept_pk PRIMARY KEY,
   dname           VARCHAR2(14) CONSTRAINT dept_dname_uq UNIQUE,
   lock            VARCHAR2(13)
);
CREATE TABLE emp (
  empno           NUMBER(4) NOT NULL CONSTRAINT emp_pk PRIMARY KEY,
  ename           VARCHAR2(10),
  job             VARCHAR2(9),
  mgr             NUMBER(4),
  hiredate        DATE,
  sal             NUMBER(7,2) CONSTRAINT emp_sal_ck CHECK (sal > 0),
  comm            NUMBER(7,2),
  deptno          NUMBER(2) CONSTRAINT emp_ref_dept_fk
                  REFERENCES dept(deptno)
);
CREATE TABLE jobhist (
  empno           NUMBER(4) NOT NULL,
  startdate       DATE NOT NULL,
  enddate         DATE,
  job             VARCHAR2(9),
  sal             NUMBER(7,2),
  comm            NUMBER(7,2),
  deptno          NUMBER(2),
  chgdesc         VARCHAR2(80),
  CONSTRAINT jobhist_pk PRIMARY KEY (empno, startdate),
  CONSTRAINT jobhist_ref_emp_fk FOREIGN KEY (empno)
      REFERENCES emp(empno) ON DELETE CASCADE,
  CONSTRAINT jobhist_ref_dept_fk FOREIGN KEY (deptno)
      REFERENCES dept (deptno) ON DELETE SET NULL,
  CONSTRAINT jobhist_date_chk CHECK (startdate <= enddate)
);
```

## 创建视图 CREATE OR REPLACE VIEW {#section_t3v_5zg_wdb .section}

``` {#codeblock_utj_dga_exg}
CREATE OR REPLACE VIEW salesemp AS
   SELECT empno, ename, hiredate, sal, comm FROM emp WHERE job = 'SALESMAN';
```

## 创建序列 CREATE SEQUENCE {#section_vgh_wzg_wdb .section}

``` {#codeblock_x4o_hse_3gp}
CREATE SEQUENCE next_empno START WITH 8000 INCREMENT BY 1;
```

## 插入数据 INSERT INTO {#section_d4x_xzg_wdb .section}

``` {#codeblock_3xj_e94_u7k}
INSERT INTO dept VALUES (10,'ACCOUNTING','NEW YORK');
INSERT INTO dept VALUES (20,'RESEARCH','DALLAS');
INSERT INTO dept VALUES (30,'SALES','CHICAGO');
INSERT INTO dept VALUES (40,'OPERATIONS','BOSTON');
INSERT INTO emp VALUES (7369,'SMITH','CLERK',7902,'17-DEC-80',800,NULL,20);
INSERT INTO emp VALUES (7499,'ALLEN','SALESMAN',7698,'20-FEB-81',1600,300,30);
INSERT INTO emp VALUES (7521,'WARD','SALESMAN',7698,'22-FEB-81',1250,500,30);
INSERT INTO emp VALUES (7566,'JONES','MANAGER',7839,'02-APR-81',2975,NULL,20);
INSERT INTO emp VALUES (7654,'MARTIN','SALESMAN',7698,'28-SEP-81',1250,1400,30);
INSERT INTO emp VALUES (7698,'BLAKE','MANAGER',7839,'01-MAY-81',2850,NULL,30);
INSERT INTO emp VALUES (7782,'CLARK','MANAGER',7839,'09-JUN-81',2450,NULL,10);
INSERT INTO emp VALUES (7788,'SCOTT','ANALYST',7566,'19-APR-87',3000,NULL,20);
INSERT INTO emp VALUES (7839,'KING','PRESIDENT',NULL,'17-NOV-81',5000,NULL,10);
INSERT INTO emp VALUES (7844,'TURNER','SALESMAN',7698,'08-SEP-81',1500,0,30);
INSERT INTO emp VALUES (7876,'ADAMS','CLERK',7788,'23-MAY-87',1100,NULL,20);
INSERT INTO emp VALUES (7900,'JAMES','CLERK',7698,'03-DEC-81',950,NULL,30);
INSERT INTO emp VALUES (7902,'FORD','ANALYST',7566,'03-DEC-81',3000,NULL,20);
INSERT INTO emp VALUES (7934,'MILLER','CLERK',7782,'23-JAN-82',1300,NULL,10);
INSERT INTO jobhist VALUES (7369,'17-DEC-80',NULL,'CLERK',800,NULL,20,'New Hire');
INSERT INTO jobhist VALUES (7499,'20-FEB-81',NULL,'SALESMAN',1600,300,30,'New Hire');
INSERT INTO jobhist VALUES (7521,'22-FEB-81',NULL,'SALESMAN',1250,500,30,'New Hire');
INSERT INTO jobhist VALUES (7566,'02-APR-81',NULL,'MANAGER',2975,NULL,20,'New Hire');
INSERT INTO jobhist VALUES (7654,'28-SEP-81',NULL,'SALESMAN',1250,1400,30,'New Hire');
INSERT INTO jobhist VALUES (7698,'01-MAY-81',NULL,'MANAGER',2850,NULL,30,'New Hire');
INSERT INTO jobhist VALUES (7782,'09-JUN-81',NULL,'MANAGER',2450,NULL,10,'New Hire');
INSERT INTO jobhist VALUES (7788,'19-APR-87','12-APR-88','CLERK',1000,NULL,20,'New Hire');
INSERT INTO jobhist VALUES (7788,'13-APR-88','04-MAY-89','CLERK',1040,NULL,20,'Raise');
INSERT INTO jobhist VALUES (7788,'05-MAY-90',NULL,'ANALYST',3000,NULL,20,'Promoted to Analyst');
INSERT INTO jobhist VALUES (7839,'17-NOV-81',NULL,'PRESIDENT',5000,NULL,10,'New Hire');
INSERT INTO jobhist VALUES (7844,'08-SEP-81',NULL,'SALESMAN',1500,0,30,'New Hire');
INSERT INTO jobhist VALUES (7876,'23-MAY-87',NULL,'CLERK',1100,NULL,20,'New Hire');
INSERT INTO jobhist VALUES (7900,'03-DEC-81','14-JAN-83','CLERK',950,NULL,10,'New Hire');
INSERT INTO jobhist VALUES (7900,'15-JAN-83',NULL,'CLERK',950,NULL,30,'Changed to Dept 30');
INSERT INTO jobhist VALUES (7902,'03-DEC-81',NULL,'ANALYST',3000,NULL,20,'New Hire');
INSERT INTO jobhist VALUES (7934,'23-JAN-82',NULL,'CLERK',1300,NULL,10,'New Hire');
```

## 查询优化器数据分析 ANALYZE {#section_n1f_11h_wdb .section}

``` {#codeblock_h2g_l4o_w41}
ANALYZE dept;
ANALYZE emp;
ANALYZE jobhist;
```

## 建立存储过程 CREATE PROCEDURE {#section_snn_d1h_wdb .section}

``` {#codeblock_joz_z1y_p35}
CREATE OR REPLACE PROCEDURE list_emp
IS
  v_empno         NUMBER(4);
  v_ename         VARCHAR2(10);
  CURSOR emp_cur IS
      SELECT empno, ename FROM emp ORDER BY empno;
BEGIN
  OPEN emp_cur;
  DBMS_OUTPUT.PUT_LINE('EMPNO    ENAME');
  DBMS_OUTPUT.PUT_LINE('-----    -------');
  LOOP
      FETCH emp_cur INTO v_empno, v_ename;
      EXIT WHEN emp_cur%NOTFOUND;
      DBMS_OUTPUT.PUT_LINE(v_empno || '     ' || v_ename);
  END LOOP;
  CLOSE emp_cur;
END;
--
--  Procedure that selects an employee row given the employee
--  number and displays certain columns.
--
CREATE OR REPLACE PROCEDURE select_emp (
  p_empno         IN  NUMBER
)
IS
  v_ename         emp.ename%TYPE;
  v_hiredate      emp.hiredate%TYPE;
  v_sal           emp.sal%TYPE;
  v_comm          emp.comm%TYPE;
  v_dname         dept.dname%TYPE;
  v_disp_date     VARCHAR2(10);
BEGIN
  SELECT ename, hiredate, sal, NVL(comm, 0), dname
      INTO v_ename, v_hiredate, v_sal, v_comm, v_dname
      FROM emp e, dept d
      WHERE empno = p_empno
        AND e.deptno = d.deptno;
  v_disp_date := TO_CHAR(v_hiredate, 'MM/DD/YYYY');
  DBMS_OUTPUT.PUT_LINE('Number    : ' || p_empno);
  DBMS_OUTPUT.PUT_LINE('Name      : ' || v_ename);
  DBMS_OUTPUT.PUT_LINE('Hire Date : ' || v_disp_date);
  DBMS_OUTPUT.PUT_LINE('Salary    : ' || v_sal);
  DBMS_OUTPUT.PUT_LINE('Commission: ' || v_comm);
  DBMS_OUTPUT.PUT_LINE('Department: ' || v_dname);
EXCEPTION
  WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('Employee ' || p_empno || ' not found');
  WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('The following is SQLERRM:');
      DBMS_OUTPUT.PUT_LINE(SQLERRM);
      DBMS_OUTPUT.PUT_LINE('The following is SQLCODE:');
      DBMS_OUTPUT.PUT_LINE(SQLCODE);
END;
--
--  Procedure that queries the 'emp' table based on
--  department number and employee number or name.  Returns
--  employee number and name as IN OUT parameters and job,
--  hire date, and salary as OUT parameters.
--
CREATE OR REPLACE PROCEDURE emp_query (
  p_deptno        IN     NUMBER,
  p_empno         IN OUT NUMBER,
  p_ename         IN OUT VARCHAR2,
  p_job           OUT    VARCHAR2,
  p_hiredate      OUT    DATE
  p_sal           OUT    NUMBER
)
IS
BEGIN
  SELECT empno, ename, job, hiredate, sal
      INTO p_empno, p_ename, p_job, p_hiredate, p_sal
      FROM emp
      WHERE deptno = p_deptno
        AND (empno = p_empno
         OR  ename = UPPER(p_ename));
END;
--
--  Procedure to call 'emp_query_caller' with IN and IN OUT
--  parameters.  Displays the results received from IN OUT and
--  OUT parameters.
--
CREATE OR REPLACE PROCEDURE emp_query_caller
IS
  v_deptno        NUMBER(2);
  v_empno         NUMBER(4);
  v_ename         VARCHAR2(10);
  v_job           VARCHAR2(9);
  v_hiredate      DATE;
  v_sal           NUMBER;
BEGIN
  v_deptno := 30;
  v_empno  := 0;
  v_ename  := 'Martin';
  emp_query(v_deptno, v_empno, v_ename, v_job, v_hiredate, v_sal);
  DBMS_OUTPUT.PUT_LINE('Department : ' || v_deptno);
  DBMS_OUTPUT.PUT_LINE('Employee No: ' || v_empno);
  DBMS_OUTPUT.PUT_LINE('Name       : ' || v_ename);
  DBMS_OUTPUT.PUT_LINE('Job        : ' || v_job);
  DBMS_OUTPUT.PUT_LINE('Hire Date  : ' || v_hiredate);
  DBMS_OUTPUT.PUT_LINE('Salary     : ' || v_sal);
EXCEPTION
  WHEN TOO_MANY_ROWS THEN
      DBMS_OUTPUT.PUT_LINE('More than one employee was selected');
  WHEN NO_DATA_FOUND THEN
      DBMS_OUTPUT.PUT_LINE('No employees were selected');
END;
```

## 建立函数 CREATE FUNCTION {#section_xxl_f1h_wdb .section}

``` {#codeblock_f5d_8o6_4q4}
CREATE OR REPLACE FUNCTION emp_comp (
  p_sal           NUMBER,
  p_comm          NUMBER
) RETURN NUMBER
IS
BEGIN
  RETURN (p_sal + NVL(p_comm, 0)) * 24;
END;
--
--  Function that gets the next number from sequence, 'next_empno',
--  and ensures it is not already in use as an employee number.
--
CREATE OR REPLACE FUNCTION new_empno RETURN NUMBER
IS
  v_cnt           INTEGER := 1;
  v_new_empno     NUMBER;
BEGIN
  WHILE v_cnt > 0 LOOP
      SELECT next_empno.nextval INTO v_new_empno FROM dual;
      SELECT COUNT(*) INTO v_cnt FROM emp WHERE empno = v_new_empno;
  END LOOP;
  RETURN v_new_empno;
END;
--
--  EDB-SPL function that adds a new clerk to table 'emp'.  This function
--  uses package 'emp_admin'.
--
CREATE OR REPLACE FUNCTION hire_clerk (
  p_ename         VARCHAR2,
  p_deptno        NUMBER
) RETURN NUMBER
IS
  v_empno         NUMBER(4);
  v_ename         VARCHAR2(10);
  v_job           VARCHAR2(9);
  v_mgr           NUMBER(4);
  v_hiredate      DATE;
  v_sal           NUMBER(7,2);
  v_comm          NUMBER(7,2);
  v_deptno        NUMBER(2);
BEGIN
  v_empno := new_empno;
  INSERT INTO emp VALUES (v_empno, p_ename, 'CLERK', 7782,
      TRUNC(SYSDATE), 950.00, NULL, p_deptno);
  SELECT empno, ename, job, mgr, hiredate, sal, comm, deptno INTO
      v_empno, v_ename, v_job, v_mgr, v_hiredate, v_sal, v_comm, v_deptno
      FROM emp WHERE empno = v_empno;
  DBMS_OUTPUT.PUT_LINE('Department : ' || v_deptno);
  DBMS_OUTPUT.PUT_LINE('Employee No: ' || v_empno);
  DBMS_OUTPUT.PUT_LINE('Name       : ' || v_ename);
  DBMS_OUTPUT.PUT_LINE('Job        : ' || v_job);
  DBMS_OUTPUT.PUT_LINE('Manager    : ' || v_mgr);
  DBMS_OUTPUT.PUT_LINE('Hire Date  : ' || v_hiredate);
  DBMS_OUTPUT.PUT_LINE('Salary     : ' || v_sal);
  DBMS_OUTPUT.PUT_LINE('Commission : ' || v_comm);
  RETURN v_empno;
EXCEPTION
  WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('The following is SQLERRM:');
      DBMS_OUTPUT.PUT_LINE(SQLERRM);
      DBMS_OUTPUT.PUT_LINE('The following is SQLCODE:');
      DBMS_OUTPUT.PUT_LINE(SQLCODE);
      RETURN -1;
END;
--
--  PostgreSQL PL/pgSQL function that adds a new salesman
--  to table 'emp'.
--
CREATE OR REPLACE FUNCTION hire_salesman (
  p_ename         VARCHAR,
  p_sal           NUMERIC,
  p_comm          NUMERIC
) RETURNS NUMERIC
AS $$
DECLARE
  v_empno         NUMERIC(4);
  v_ename         VARCHAR(10);
  v_job           VARCHAR(9);
  v_mgr           NUMERIC(4);
  v_hiredate      DATE;
  v_sal           NUMERIC(7,2);
  v_comm          NUMERIC(7,2);
  v_deptno        NUMERIC(2);
BEGIN
  v_empno := new_empno();
  INSERT INTO emp VALUES (v_empno, p_ename, 'SALESMAN', 7698,
      CURRENT_DATE, p_sal, p_comm, 30);
  SELECT INTO
      v_empno, v_ename, v_job, v_mgr, v_hiredate, v_sal, v_comm, v_deptno
      empno, ename, job, mgr, hiredate, sal, comm, deptno
      FROM emp WHERE empno = v_empno;
  RAISE INFO 'Department : %', v_deptno;
  RAISE INFO 'Employee No: %', v_empno;
  RAISE INFO 'Name       : %', v_ename;
  RAISE INFO 'Job        : %', v_job;
  RAISE INFO 'Manager    : %', v_mgr;
  RAISE INFO 'Hire Date  : %', v_hiredate;
  RAISE INFO 'Salary     : %', v_sal;
  RAISE INFO 'Commission : %', v_comm;
  RETURN v_empno;
EXCEPTION
  WHEN OTHERS THEN
      RAISE INFO 'The following is SQLERRM:';
      RAISE INFO '%', SQLERRM;
      RAISE INFO 'The following is SQLSTATE:';
      RAISE INFO '%', SQLSTATE;
      RETURN -1;
END;
```

## 建立规则 CREATE RULE {#section_xry_g1h_wdb .section}

``` {#codeblock_9at_4tk_xtk}
CREATE OR REPLACE RULE salesemp_i AS ON INSERT TO salesemp
DO INSTEAD
  INSERT INTO emp VALUES (NEW.empno, NEW.ename, 'SALESMAN', 7698,
      NEW.hiredate, NEW.sal, NEW.comm, 30);
CREATE OR REPLACE RULE salesemp_u AS ON UPDATE TO salesemp
DO INSTEAD
  UPDATE emp SET empno    = NEW.empno,
                 ename    = NEW.ename,
                 hiredate = NEW.hiredate,
                 sal      = NEW.sal,
                 comm     = NEW.comm
      WHERE empno = OLD.empno;
CREATE OR REPLACE RULE salesemp_d AS ON DELETE TO salesemp
DO INSTEAD
DELETE FROM emp WHERE empno = OLD.empno;
```

## 建立触发器 CREATE TRIGGER {#section_tgm_31h_wdb .section}

``` {#codeblock_hm8_zan_2s1}
CREATE OR REPLACE TRIGGER user_audit_trig
  AFTER INSERT OR UPDATE OR DELETE ON emp
DECLARE
  v_action        VARCHAR2(24);
BEGIN
  IF INSERTING THEN
      v_action := ' added employee(s) on ';
  ELSIF UPDATING THEN
      v_action := ' updated employee(s) on ';
  ELSIF DELETING THEN
      v_action := ' deleted employee(s) on ';
  END IF;
  DBMS_OUTPUT.PUT_LINE('User ' || USER || v_action || TO_CHAR(SYSDATE,'YYYY-MM-DD'));
END;
CREATE OR REPLACE TRIGGER emp_sal_trig
  BEFORE DELETE OR INSERT OR UPDATE ON emp
  FOR EACH ROW
DECLARE
  sal_diff       NUMBER;
BEGIN
  IF INSERTING THEN
      DBMS_OUTPUT.PUT_LINE('Inserting employee ' || :NEW.empno);
      DBMS_OUTPUT.PUT_LINE('..New salary: ' || :NEW.sal);
  END IF;
  IF UPDATING THEN
      sal_diff := :NEW.sal - :OLD.sal;
      DBMS_OUTPUT.PUT_LINE('Updating employee ' || :OLD.empno);
      DBMS_OUTPUT.PUT_LINE('..Old salary: ' || :OLD.sal);
      DBMS_OUTPUT.PUT_LINE('..New salary: ' || :NEW.sal);
      DBMS_OUTPUT.PUT_LINE('..Raise     : ' || sal_diff);
  END IF;
  IF DELETING THEN
      DBMS_OUTPUT.PUT_LINE('Deleting employee ' || :OLD.empno);
      DBMS_OUTPUT.PUT_LINE('..Old salary: ' || :OLD.sal);
  END IF;
END;
```

## 建立包 CREATE PACKAGE {#section_ogh_k1h_wdb .section}

``` {#codeblock_ja1_fju_mzh}
CREATE OR REPLACE PACKAGE emp_admin
IS
  FUNCTION get_dept_name (
      p_deptno        NUMBER
  ) RETURN VARCHAR2;
  FUNCTION update_emp_sal (
      p_empno         NUMBER,
      p_raise         NUMBER
  ) RETURN NUMBER;
  PROCEDURE hire_emp (
      p_empno         NUMBER,
      p_ename         VARCHAR2,
      p_job           VARCHAR2,
      p_sal           NUMBER,
      p_hiredate      DATE,
      p_comm          NUMBER,
      p_mgr           NUMBER,
      p_deptno        NUMBER
  );
  PROCEDURE fire_emp (
      p_empno         NUMBER
  );
END emp_admin;
```

## 建立包体 CREATE PACKAGE BODY {#section_ttq_m1h_wdb .section}

``` {#codeblock_34g_7vm_c67}
--
--  Package body for the 'emp_admin' package.
--
CREATE OR REPLACE PACKAGE BODY emp_admin
IS
  --
  --  Function that queries the 'dept' table based on the department
  --  number and returns the corresponding department name.
  --
  FUNCTION get_dept_name (
      p_deptno        IN NUMBER
  ) RETURN VARCHAR2
  IS
      v_dname         VARCHAR2(14);
  BEGIN
      SELECT dname INTO v_dname FROM dept WHERE deptno = p_deptno;
      RETURN v_dname;
  EXCEPTION
      WHEN NO_DATA_FOUND THEN
          DBMS_OUTPUT.PUT_LINE('Invalid department number ' || p_deptno);
          RETURN '';
  END;
  --
  --  Function that updates an employee's salary based on the
  --  employee number and salary increment/decrement passed
  --  as IN parameters.  Upon successful completion the function
  --  returns the new updated salary.
  --
  FUNCTION update_emp_sal (
      p_empno         IN NUMBER,
      p_raise         IN NUMBER
  ) RETURN NUMBER
  IS
      v_sal           NUMBER := 0;
  BEGIN
      SELECT sal INTO v_sal FROM emp WHERE empno = p_empno;
      v_sal := v_sal + p_raise;
      UPDATE emp SET sal = v_sal WHERE empno = p_empno;
      RETURN v_sal;
  EXCEPTION
      WHEN NO_DATA_FOUND THEN
          DBMS_OUTPUT.PUT_LINE('Employee ' || p_empno || ' not found');
          RETURN -1;
      WHEN OTHERS THEN
          DBMS_OUTPUT.PUT_LINE('The following is SQLERRM:');
          DBMS_OUTPUT.PUT_LINE(SQLERRM);
          DBMS_OUTPUT.PUT_LINE('The following is SQLCODE:');
          DBMS_OUTPUT.PUT_LINE(SQLCODE);
          RETURN -1;
  END;
  --
  --  Procedure that inserts a new employee record into the 'emp' table.
  --
  PROCEDURE hire_emp (
      p_empno         NUMBER,
      p_ename         VARCHAR2,
      p_job           VARCHAR2,
      p_sal           NUMBER,
      p_hiredate      DATE,
      p_comm          NUMBER,
      p_mgr           NUMBER,
      p_deptno        NUMBER
  )
  AS
  BEGIN
      INSERT INTO emp(empno, ename, job, sal, hiredate, comm, mgr, deptno)
          VALUES(p_empno, p_ename, p_job, p_sal,
                 p_hiredate, p_comm, p_mgr, p_deptno);
  END;
  --
  --  Procedure that deletes an employee record from the 'emp' table based
  --  on the employee number.
  --
  PROCEDURE fire_emp (
      p_empno         NUMBER
  )
  AS
  BEGIN
      DELETE FROM emp WHERE empno = p_empno;
  END;
END;
```

