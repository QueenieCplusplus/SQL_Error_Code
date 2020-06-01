# SQL_Error_Code
{ my experience to DBA }


* Error Code 1370

alter routine command 
denied to user 'account_name'@'IP' 
for routine 'stored_procedure_name'

SQL Statement:
DROP procedure IF EXISTS `stored_procedure_name`

          RROR 1370 (42000): execute command 
          denied to user 'test'@'localhost' for routine 'mydb.myfunc'

* Solution

(1) 授權帳號擁有執行權限

          mysql> grant execute on mydb.* to 'test'@'localhost';
          mysql> flush privileges;
   
(2) 函數調用

          mysql> call myfunc();
          ERROR 1370 (42000): execute command denied to user 'test'@'localhost' for routine 'mydb.myfunc'
      
(3) 函數授權執行需要授權帳號到資料庫外，還需要授權到資料庫的函數

          mysql> grant execute on function mydb.myfunc to 'test'@'localhost';
          mysql> flush privileges;


* Ref Doc

https://www.edoou.com/articles/1575287575563138


* Refresh Stored Procedures and Connection Error Behaviour

https://bugs.mysql.com/bug.php?id=81780
