Helpful Unix Commands
====

Find the files in the current directory and subdirectory and then delete them

    find . | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh
    gvim doit.sh // check for murphy and his law
    source doit.sh

Specify the file type

    find . -name "\*.sas" -o -name "\*.log" | xargs grep -l "string" | awk '{print "rm "$1}' > doit.sh

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

Remove unix return (^M) in Vim

    :%s/\r\(\n\)/\1/g
