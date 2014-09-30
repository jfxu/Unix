
SAS select all variables EXCEPT 

    proc sql;
        select name into :columns separated by ' ' 
        from dictionary.columns
        where libname = 'LIB' and memname = 'TABLE' 
            and name ne 'COLUMN_TO_BE_EXCLUDED';
    quit;

Check duplicate observations in SAS

    %macro dups(table, groupby);
        proc sql noprint;
            select &groupby, count(*) as duplicate_counts
            from &table
            group by &groupby
            having count(*) > 1
            ;
        quit;
    %mend dups;

Adding data to a data set

    proc sql;
        insert into TABLE
            set variable1 = "value1",
                variable2 = "value2"
            set variable1 = "val1"
                variable2 = "val2"
            ;
    quit;

or
 
    proc sql;
        insert into TABLE (variable1, variable2)
            value ("value1", "value2")
            value ("val1", "val2")
            ;
    quit;

or adding data set into table

    proc sql;
        insert into TABLE (variable1, variable2)
            select p_variable1, p_variable2
            from ANOTHER_TABLE
            where ....
        ;
    quit;

SQL: count using different conditions

    select
        count(case when condition1 then 1 end) AS n1,
        count(case when condition2 then 1 end) AS n2,
        count(case when condition3 then 1 end) AS n3
    from data

Select count of rows in another table:
    
    select A.*, (SELECT COUNT(*) FROM B WHERE B.id = A.id) AS TOT FROM A

Check SAS data set:

    %let data_set = libname.data_set_name;

    %let dsid = %sysfunc (open(&data_set));

    %let nobs = %sysfunc(attrn(&dsid,nlobs));

    %let create_date = %sysfunc(attrn(&dsid, crdte));

    %let close_flag = %sysfunc(close(&dsid));

Remove title:
    
    title;
