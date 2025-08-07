/* Get today’s date */
%let today = %sysfunc(today());

/* Compute previous week's Monday */
%let start_date = %sysfunc(intnx(week.2, &today, -1, b));

/* Compute previous week's Sunday */
%let end_date = %sysfunc(intnx(week.2, &today, -1, e));

/* Format all values */
%let start1   = %str(%')%sysfunc(putn(&start_date, date7.))%str(%')D;
%let end1     = %str(%')%sysfunc(putn(&end_date, date7.))%str(%')D;
%let end_dt   = %str(%')%sysfunc(putn(&end_date, yymmdd10.))%str(%');
%let filedate = %sysfunc(putn(&end_date, yymmddn8.));
