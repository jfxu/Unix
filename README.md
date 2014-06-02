### Helpful Unix Commands
====

Find the files in the current directory and subdirectory and then delete them

    find . | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh
    gvim doit.sh // check for murphy and his law
    source doit.sh

Specify the file type

    find . -name "*.sas" -o -name "\*.log" | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh

Search two strings in files

    grep "string1.\*string2 | string2 .\* string1" *.sas .

or 

    grep "string1" \*.sas | grep "string2"

Search in VIM with word1 and without word2 

    /word1 \\( .\*word2\\) /i \@!

SAS select all variables EXCEPT 


    proc sql;
        select name into :columns separated by ' ' 
        from dictionary.columns
        where libname = 'LIB' and memname = 'TABLE' 
            and name ne 'COLUMN_TO_BE_EXCLUDED';
    quit;

Remove unix return (    ^M  ) in Vim

    :%s/\r\(\n\)/\1/g

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

    
