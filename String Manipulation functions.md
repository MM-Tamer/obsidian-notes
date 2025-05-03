
| Function                                                                                                               | Usage                                                                                                                                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| LOWER(column_name)                                                                                                     | converts the string to lowercase.                                                                                                                                                                                                                                                    |
| UPPER(column_name)                                                                                                     | converts the string to uppercase.                                                                                                                                                                                                                                                    |
| INITCAP(column_name)                                                                                                   | capitalizes the first letter in the string.                                                                                                                                                                                                                                          |
| SUBSTR(column, i, n)                                                                                                   | returns the substring of the field starting from index i and spanning n characters afterwards. If n is excluded, all the remaining characters will be included.                                                                                                                      |
| CONCAT(str1, str2)                                                                                                     | concatenates two strings only.                                                                                                                                                                                                                                                       |
| INSTR(string, substring, starting_index, n_th_occurence)                                                               | returns the first index of the matching substring or 0 if no match is found. The starting index could be negative to denote searching backwards.                                                                                                                                     |
| TRIM(str)                                                                                                              | The default behavior is deleting both leading and trailing whitespaces. you can use BOTH, LEADING or TRAILING. You can also specify the the character to be trimmed. It is possible to trim multiple characters however, this is only possible with the LEADING or TRAILING options. |
| LTRIM / RTRIM('my name is adammmm', 'm');                                                                              | Same as TRIM function.                                                                                                                                                                                                                                                               |
| REPLACE(string, substring, replacement).<br>`select replace('undertaker','und') rpl from dual;` will return 'ertaker'. | Replaces the substring with the replacement. If the replacement is not provided, the default behavior is delete.                                                                                                                                                                     |
| LPAD / RPAD(string, total_length, padding_char)<br>`select LPAD('undertaker', 15, '*') rpl from dual;`                 | Adds padding either to the left or the right respectively, the number of padding characters = string_length - total_length. The default padding character is whitespace. CAUTION: if the total_ length is less than the string length, characters will be omitted from the end.      |

>[!info]- TRIM function
>```sql
>SELECT TRIM ('     My Name is Adam   ') trm from dual;
>
SELECT TRIM (' ' FROM '     My Name is Adam   ') trm from dual;
>
>SELECT TRIM (BOTH ' ' FROM '     My Name is Adam   ') trm from dual;
>
SELECT TRIM (LEADING ' ' FROM '     My Name is Adam   ') trm from dual;
>
SELECT TRIM (TRAILING ' ' FROM '     My Name is Adam   ') trm from dual;
>
>SELECT TRIM (TRAILING 'm' FROM '     my Name is Adam   ') trm from dual;
>
>SELECT TRIM (TRAILING 'm' FROM 'my Name is Adam') trm from dual;
>
SELECT TRIM (TRAILING 'm' FROM 'my Name is Adammmmm') trm from dual;
>
SELECT TRIM (LEADING 'm' FROM 'my Name is Adam') trm from dual;
>
SELECT TRIM (BOTH 'm' FROM 'my Name is Adam') trm from dual;
>
SELECT TRIM ('m' FROM 'my Name is Adam') trm from dual;
>
SELECT TRIM ('m' FROM 'my Name is Ada') trm from dual;
>
SELECT TRIM (TRAILING 'm' FROM 'my Name is Ada') trm from dual;
>
>SELECT TRIM (TRAILING 'my' FROM 'my Name is Ada') trm from dual;
>```
************
>[!info]- to_char function
>```sql
SELECT first_name, hire_date FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'YYYY') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'YY') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'RR') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'YEAR') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'MM') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'MM-YYYY') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'MON-YYYY') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'MON-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'mon-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Mon-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'MONTH-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Month-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'DD-Month-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'DY-Month-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Dy-Month-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Day-Month-yyyy') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Dy-Month-yyyy HH12') "Formatted Date" FROM employees;
>
>SELECT first_name, hire_date, to_char(hire_date,'Dy-Month-yyyy HH24') "Formatted Date" FROM employees;
