# DASHBORD MADE BY ME
#ODI CRICKET DASHBOARD SQl CODE 
create database power_bi;
use power_bi;
create or replace table ODI_match_results(
Result varchar(30),
Margin varchar(30),
BR int,
Toss varchar(30),
Bat varchar(30),
Opposition varchar(30),
Ground varchar(30),
Start_Date varchar(20),
Match_ID varchar(30),
Country varchar(30),
Country_ID int);

select * from ODI_match_results;

create or replace table Bowler(
Overs varchar(30),
Mdns varchar(30),
Runs varchar(30),
Wkts varchar(30),
Econ varchar(30),
Ave varchar(30),
SR varchar(30),
Opposition varchar(30),
Ground varchar(30),
Start_Date date,
Match_ID varchar(30),
Bowler varchar(30),
Player_ID int);

select * from bowler;

create table batsman(
Bat1 varchar(30),
Runs varchar(30),
BF varchar(30),
SR varchar(30),
fours varchar(30),
sixes varchar(30),
Opposition varchar(30),
Ground varchar(30),
Start_Date varchar(20),
Match_ID varchar(30),
Batsman varchar(50),
Player_ID int;

select * from ODI_match_results; truncate table ODI_match_results;
select * from bowler;
select * from batsman;

UPDATE ODI_match_results SET BR = 0 WHERE BR IS NULL;
update ODI_match_results set result = 'N/P'where result = '-';
update ODI_match_results set result = 'N/P' where result = 'aban';
update ODI_match_results set result = 'Not Play' where result = 'N/P';
update ODI_match_results set result = 'Not Play' where result = 'n/r';
update ODI_match_results set result = 'NOT play'  where result ='canc';
update ODI_match_results set margin = 'Not Play' where margin = '-';
update ODI_match_results set margin = '0 wickets' where margin = 'Not Play';
update ODI_match_results set Toss = 'Not Play' where Toss = '-';
update ODI_match_results set bat = 'Not Play' where bat = '-';
UPDATE ODI_match_results
SET Match_id = replace(Match_id,'#',' ');


select * from bowler;
  
Update Bowler set overs = 0 where overs = '-';
Update Bowler Set mdns = 0 where mdns ='-';
update bowler set wkts = 0 where wkts= '-';
update bowler set runs = 0 where runs= '-';
update bowler set Econ = 0 where Econ= '-'; 
update Bowler set ave = 0 where ave = '-';
update Bowler set sr = 0 where sr = '-';
update Bowler set Match_id=replace(match_id,'#',' ');
  
  
select * from batsman;
  
update Batsman set runs = 0 where runs = '-';
update batsman set bf = 0 where bf ='-';
update batsman set sr = 0 where sr = '-';
update batsman set fours = 0 where fours = '-';
update batsman set sixes = 0 where sixes ='-';
update batsman set match_id = replace(match_id,'#',' ');
update BAtsman set bat1 =replace(bat1,'*','');
  
select * from ODI_match_results;
SELECT * FROM BOWlER;
SELECT * FROM batsman;
-----making master table for dirctly connect with power bi
create or replace table ODI_match_details_copy as
select O.*,bt.runs as batsman_run,bt.bf,bt.sr as batsman_sr,bt.fours,bt.sixes,bt.batsman,bt.player_id as batsman_player_id,bl.overs,bl.mdns,bl.runs as bowler_runs,bl.wkts,bl.econ,bl.ave,bl.sr as bowler_sr,bl.bowler,bl.player_id as bowler_player_id from ODI_match_results O
left Outer Join Batsman BT on O.Match_id = BT.Match_id
left outer join Bowler BL on O.Match_id = Bl.match_id;
