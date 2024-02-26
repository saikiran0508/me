data new_dataset;
    set old_dataset;

    /* Calculate the difference between the two timestamps in hours */
    time_difference_hours = intck('HOUR', timestamp1, timestamp2, 'C');

    /* Convert hours to combined format of days and hours */
    days_part = floor(time_difference_hours / 24);
    hours_part = mod(time_difference_hours, 24);
    
    /* Combine days and hours into a single column */
    time_difference = put(days_part, 4.) || ' days ' || put(hours_part, 2.) || ' hours';

    /* Optionally, you can convert days to years if needed */
    /* years_part = floor(days_part / 365.25); */
    /* days_part = mod(days_part, 365.25); */
    
run;
