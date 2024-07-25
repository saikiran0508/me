/* Open Excel */
options noxwait noxsync;
x "excel";

/* Wait for Excel to open */
data _null_;
   x=sleep(5); /* Adjust the sleep time as needed */
run;

/* Establish a DDE connection */
filename cmds dde 'excel|system';

/* Open the Excel file */
data _null_;
   file cmds;
   put '[open("C:\path\to\your\file.xlsx")]';
run;

/* Format the first sheet (abc1) */
data _null_;
   file cmds;
   put '[workbook.activate("abc1")]';
   put '[cells.select]';
   put '[selection.Font.Bold = true]'; /* Make header bold */
   put '[columns("A:Z").entirecolumn.autofit]'; /* Auto-fit columns */
   put '[selection.borders(xlEdgeLeft).Weight = 2]';
   put '[selection.borders(xlEdgeRight).Weight = 2]';
   put '[selection.borders(xlEdgeTop).Weight = 2]';
   put '[selection.borders(xlEdgeBottom).Weight = 2]'; /* Apply borders */
   put '[selection.borders(xlInsideVertical).Weight = 1]';
   put '[selection.borders(xlInsideHorizontal).Weight = 1]';
run;

/* Repeat for the other sheets (abc2 and abc3) */
data _null_;
   file cmds;
   put '[workbook.activate("abc2")]';
   put '[cells.select]';
   put '[selection.Font.Bold = true]'; /* Make header bold */
   put '[columns("A:Z").entirecolumn.autofit]'; /* Auto-fit columns */
   put '[selection.borders(xlEdgeLeft).Weight = 2]';
   put '[selection.borders(xlEdgeRight).Weight = 2]';
   put '[selection.borders(xlEdgeTop).Weight = 2]';
   put '[selection.borders(xlEdgeBottom).Weight = 2]'; /* Apply borders */
   put '[selection.borders(xlInsideVertical).Weight = 1]';
   put '[selection.borders(xlInsideHorizontal).Weight = 1]';
run;

data _null_;
   file cmds;
   put '[workbook.activate("abc3")]';
   put '[cells.select]';
   put '[selection.Font.Bold = true]'; /* Make header bold */
   put '[columns("A:Z").entirecolumn.autofit]'; /* Auto-fit columns */
   put '[selection.borders(xlEdgeLeft).Weight = 2]';
   put '[selection.borders(xlEdgeRight).Weight = 2]';
   put '[selection.borders(xlEdgeTop).Weight = 2]';
   put '[selection.borders(xlEdgeBottom).Weight = 2]'; /* Apply borders */
   put '[selection.borders(xlInsideVertical).Weight = 1]';
   put '[selection.borders(xlInsideHorizontal).Weight = 1]';
run;

/* Save and close the Excel file */
data _null_;
   file cmds;
   put '[save]';
   put '[quit]';
run;
