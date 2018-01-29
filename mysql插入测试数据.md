``` sql
DROP PROCEDURE IF EXISTS `proc_while`;
DELIMITER ;;
CREATE DEFINER=`root`@`localhost` PROCEDURE `proc_while`(IN n int)
BEGIN

    DECLARE i int;
    SET i = 5;

    SET autocommit=0;
    WHILE i < n DO
        insert into dev_gateway
(sn,tenant_id,grp_id,type,name,ip,mac,description,crt_time,crt_name) 
		values(i,'469bd06ab1ee4e129bcfbcff2c15e1d4',4,800,'i','127.0.0.1','1234567','datatest',sysdate(),'datatest');


	set i=i+1;	
    END WHILE;
    select i;
COMMIT;
    
END
;;
DELIMITER ;
call proc_while(1200000);
set @loop=1200000;
call proc_while(@loop);
