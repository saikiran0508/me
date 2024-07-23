ods excel file="C:\path\to\yourfile.xlsx" options(sheet_name="Sheet1" autofilter="all");

proc print data=your_dataset noobs;
run;

ods excel close;


ods excel file="C:\path\to\yourfile.xlsx" options(sheet_name="Sheet1");

/* Define a style with bold headers and borders */
proc template;
    define style styles.myStyle;
        parent=styles.excelxp;
        class header /
            font_weight=bold
            bordercolor=black
            borderwidth=2pt;
        class data /
            bordercolor=black
            borderwidth=1pt;
        class table /
            bordercolor=black
            borderwidth=2pt;
    end;
run;

ods excel options(style=styles.myStyle);

proc print data=your_dataset noobs;
run;

ods excel close;



ods excel file="C:\path\to\yourfile.xlsx" options(sheet_name="Sheet1" autofilter="all" auto_width="on");

proc print data=your_dataset noobs;
run;

ods excel close;




filename myemail email 'recipient@example.com'
                   subject='Your SAS dataset'
                   attach='C:\path\to\yourfile.xlsx';

data _null_;
    file myemail;
    put 'Please find the attached Excel file.';
run;
