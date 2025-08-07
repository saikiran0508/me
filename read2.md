/* Compute previous week's Monday (beginning of last week) */
%let start_date = %sysfunc(intnx(week.2, %sysfunc(today()), -1, 'b'));

/* Compute previous week's Sunday (end of last week) */
%let end_date = %sysfunc(intnx(week.2, %sysfunc(today()), -1, 'e'));

/* Format as needed */
%let start1 = %str(%')%sysfunc(putn(&start_date, date7.))%str(%')D;
%let end1   = %str(%')%sysfunc(putn(&end_date, date7.))%str(%')D;
%let end_dt = %str(%')%sysfunc(putn(&end_date, yymmdd10.))%str(%');
%let filedate = %sysfunc(putn(&end_date, yymmddn8.));
