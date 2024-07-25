/* Sample dataset */
data sample;
    input Name $ Age Height Weight;
    datalines;
John 23 68 180
Jane 31 65 150
Alice 29 62 120
Bob 34 70 200
;
run;

/* Exporting to Excel and applying formatting */
ods excel file="C:\path\to\your\report.xlsx" 
          options(sheet_name="Sheet1" embedded_titles="yes");

ods excel options(sheet_interval="none");
ods excel options(absolute_column_width="10 10 10 10");

proc report data=sample nowd style(header)=[font_weight=bold borderstyle=solid] 
                                style(column)=[borderstyle=solid];
    columns Name Age Height Weight;
    define Name / "Name" style(column)=[just=center];
    define Age / "Age" style(column)=[just=center];
    define Height / "Height (in)" style(column)=[just=center];
    define Weight / "Weight (lbs)" style(column)=[just=center];
run;

ods excel close;
