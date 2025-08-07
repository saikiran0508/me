/* Today is Monday. Get yesterday (Sunday) as end date */
%let end_date = %sysfunc(intnx(week.2, %sysfunc(today()), -1, 'end'));
%let start_date = %sysfunc(intnx(week.2, %sysfunc(today()), -1, 'begin'));

/* Format required variables */
%let end_dt = %sysfunc(putn(&end_date, yymmdd10.));
%let end1 = %sysfunc(putn(&end_date, date7.));
%let start1 = %sysfunc(putn(&start_date, date7.));
%let filedate = %sysfunc(putn(&end_date, yymmddn8.));
