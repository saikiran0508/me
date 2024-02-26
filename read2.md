data new_dataset;
    set old_dataset;

    /* Calculate the difference between the two timestamps */
    time_difference_days = intck('DAY', timestamp1, timestamp2, 'C');
    time_difference_hours = intck('HOUR', timestamp1, timestamp2, 'C');

    /* Optionally, you can convert hours to a fraction of days */
    time_difference_days = time_difference_days + time_difference_hours / 24;

run;
