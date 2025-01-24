ods excel file="C:\path\to\your\new_file.xlsx" options(sheet_interval="none" gridlines="off");

    /* For Sheet 1 */
    ods excel options(sheet_name="Sheet1");
    proc print data=your_data_1;
        var your_columns;
        style(header)={font_weight=bold};
        style(data)={bordercolor=black borderwidth=1};
        title "Your Title for Sheet 1";
    run;

    /* For Sheet 2 */
    ods excel options(sheet_name="Sheet2");
    proc print data=your_data_2;
        var your_columns;
        style(header)={font_weight=bold};
        style(data)={bordercolor=black borderwidth=1};
        title "Your Title for Sheet 2";
    run;

    /* For Sheet 3 */
    ods excel options(sheet_name="Sheet3");
    proc print data=your_data_3;
        var your_columns;
        style(header)={font_weight=bold};
        style(data)={bordercolor=black borderwidth=1};
        title "Your Title for Sheet 3";
    run;

ods excel close;
