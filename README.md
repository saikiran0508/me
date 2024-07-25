/* Connect to Excel to format headers */
proc sql;
    connect to excel (path="path-to-your-excel-file.xlsx");

    /* Format headers in Sheet1 */
    execute(
        update [Sheet1$A1:Z1]
        set font.color='000000', font.bold=true, wrap_text=true
    ) by excel;

    /* Format headers in Sheet2 */
    execute(
        update [Sheet2$A1:Z1]
        set font.color='000000', font.bold=true, wrap_text=true
    ) by excel;

    /* Format headers in Sheet3 */
    execute(
        update [Sheet3$A1:Z1]
        set font.color='000000', font.bold=true, wrap_text=true
    ) by excel;

    disconnect from excel;
quit;

/* Clear the library */
libname myexcel clear;
