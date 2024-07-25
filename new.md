/* Prepare the datasets */
data work.dataset1;
    set sashelp.class; /* Example dataset */
    /* Make any necessary changes here */
run;

data work.dataset2;
    set sashelp.cars; /* Example dataset */
    /* Make any necessary changes here */
run;

data work.dataset3;
    set sashelp.iris; /* Example dataset */
    /* Make any necessary changes here */
run;

/* Advanced formatting using ODS EXCEL */
ods excel file="/path/to/your/output_file.xlsx" options(sheet_interval='none' sheet_name='Sheet1');

proc report data=work.dataset1 nowd;
    columns _all_;
    define _all_ / style(header)=[foreground=black font_weight=bold] 
                   style(column)=[borderstyle=solid bordercolor=black];
    compute before _page_;
        call define(_page_, 'style', 'style=[bordertopwidth=2 bordertopcolor=black borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
    compute after _page_;
        call define(_page_, 'style', 'style=[borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
run;

ods excel options(sheet_name='Sheet2');

proc report data=work.dataset2 nowd;
    columns _all_;
    define _all_ / style(header)=[foreground=black font_weight=bold] 
                   style(column)=[borderstyle=solid bordercolor=black];
    compute before _page_;
        call define(_page_, 'style', 'style=[bordertopwidth=2 bordertopcolor=black borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
    compute after _page_;
        call define(_page_, 'style', 'style=[borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
run;

ods excel options(sheet_name='Sheet3');

proc report data=work.dataset3 nowd;
    columns _all_;
    define _all_ / style(header)=[foreground=black font_weight=bold] 
                   style(column)=[borderstyle=solid bordercolor=black];
    compute before _page_;
        call define(_page_, 'style', 'style=[bordertopwidth=2 bordertopcolor=black borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
    compute after _page_;
        call define(_page_, 'style', 'style=[borderbottomwidth=2 borderbottomcolor=black]');
    endcomp;
run;

ods excel close;
