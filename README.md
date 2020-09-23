<div align="center">

## PhP IP Client Logger


</div>

### Description

Detect Client IP, save it to file(include first time,last time hit) and count client hit.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Kevin Leonardi](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kevin-leonardi.md)
**Level**          |Intermediate
**User Rating**    |4.3 (78 globes from 18 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__8-9.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kevin-leonardi-php-ip-client-logger__8-539/archive/master.zip)

### API Declarations

please vote me ! if you like this code.


### Source Code

```
<!--
/*************************************************************************/
/* Script Name : IP Logger 												 */
/* Description : Detect Client IP, save it to file, and count client hit */
/* Author   : Kevin Leonardi                     */
/* Email    : fotx@yahoo.com                     */
/*                										 */
/* Please Vote Me if you like my script! :)								 */
/*************************************************************************/
//-->
<?php
 $found = "false";
 $filename = "count.inc";
 if (file_exists ($filename))
   {$fp = fopen($filename,"r+");}
 else{$fp = fopen($filename,"w");}
 $offset = 0;
 $cnt = 1;
 while ($row = fgets($fp,4096)) {
  $cols = explode(";",$row);
  if ($cols[0] == $HTTP_SERVER_VARS["REMOTE_ADDR"]){
   $cols[1]++; // increase counter;
   $cnt = $cols[1];
   $cols[3] = date("M/d/Y_H:i:s"); //save hour minute seconds _ month date year
   fseek($fp,$offset);
   fputs($fp,implode(";",$cols));
   $found = "true";
  }
  $offset = ftell($fp);
 }
 if ($found=="false"){
  $cols = array($HTTP_SERVER_VARS["REMOTE_ADDR"],1,date("M/d/Y_H:i:s"),date("M/d/Y_H:i:s"),"\n");
  fputs($fp,implode(";",$cols));
 }
 fclose($fp);
?>
<!--
/**************************************************************************/
/*
/* If you'd like this below messages disappear, just remark them with "//"
/* at the every beginning of the line.
/*************************************************************************/
//-->
<HTML>
<HEAD><TITLE>IP Logger</TITLE></HEAD>
<BODY BGCOLOR="#000000">
<font face="Courier,Verdana,Arial" size=3 Color="#FFFFFF">
<b>YOUR IP ADDRESS : <font color="red"><?php echo $HTTP_SERVER_VARS["REMOTE_ADDR"]."<br>"; ?></b></font>
You've been hit this site <font color="red"><b><?php echo $cnt;?></b></font> times
since <font color="cyan"><b><?php echo eregi_replace("_"," at ",$cols[2]);?>.<br></b></font>
Last time I saw you : <font color="Yellow"><b><?php echo eregi_replace("_"," at ",$cols[3]);?></b></font>.
<br><br>
<font color="lime"><b>Vote Me! if you like this code.</b></font>
<font>
</BODY>
</HTML>
```

