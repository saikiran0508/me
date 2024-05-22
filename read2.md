/* Sample input dataset */
data input_dataset;
    input id $ date : date9. numeric_code latest_rank1 earliest_rank2;
    format date date9.;
    datalines;
A 01JAN2021 51 0 1
A 05JAN2021 56 1 0
B 10JAN2021 51 0 1
B 15JAN2021 56 1 0
C 20JAN2021 51 0 1
C 25JAN2021 52 0 0
C 30JAN2021 56 1 0
;
run;

/* Print the input dataset for reference */
proc print data=input_dataset;
    title 'Input Dataset';
run;

/* Create a new dataset with start_date and end_date columns */
data temp_dataset;
    set input_dataset;
    length start_date end_date 8; /* Ensure dates are numeric (SAS dates) */
    format start_date end_date date9.; /* Apply date format */
run;

/* Update the new columns based on the given conditions */
proc sql;
    /* Add start_date based on numeric_code and earliest_rank2 */
    update temp_dataset
    set start_date = date
    where numeric_code = 51 and earliest_rank2 = 1;

    /* Add end_date based on numeric_code and latest_rank1 */
    update temp_dataset
    set end_date = date
    where numeric_code = 56 and latest_rank1 = 1;
quit;

/* Print the final dataset to verify the result */
proc print data=temp_dataset;
    title 'Final Dataset with Start and End Dates';
run;
