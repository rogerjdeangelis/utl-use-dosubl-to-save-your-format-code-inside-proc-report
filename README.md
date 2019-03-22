# utl-use-dosubl-to-save-your-format-code-inside-proc-report
Use dosubl to save your format code inside proc report 

    Use dosubl to save your format code inside proc report                                                
                                                                                                          
    github                                                                                                
    https://tinyurl.com/yyqt8ksy                                                                          
    https://github.com/rogerjdeangelis/utl-use-dosubl-to-save-your-format-code-inside-proc-report         
                                                                                                          
    It is frustrating when you misplace your formats.                                                     
                                                                                                          
    It is my belief that 'dosubl' with a shared storage enhancemnet is                                    
    much more usefull than DS2 and FCMP for most problems?                                                
                                                                                                          
    *_                   _                                                                                
    (_)_ __  _ __  _   _| |_                                                                              
    | | '_ \| '_ \| | | | __|                                                                             
    | | | | | |_) | |_| | |_                                                                              
    |_|_| |_| .__/ \__,_|\__|                                                                             
            |_|                                                                                           
    ;                                                                                                     
                                                                                                          
    proc sort data=sashelp.class(keep=name age) out=class;                                                
      by age;                                                                                             
    run;quit;                                                                                             
                                                                                                          
                                                                                                          
    WORK.CLASS total obs=19                                                                               
                                                                                                          
       NAME       AGE                                                                                     
                                                                                                          
       Joyce       11                                                                                     
       Thomas      11                                                                                     
       James       12                                                                                     
       Jane        12                                                                                     
       John        12                                                                                     
       Louise      12                                                                                     
       Robert      12                                                                                     
       Alice       13                                                                                     
       Barbara     13                                                                                     
       Jeffrey     13                                                                                     
       Alfred      14                                                                                     
       Carol       14                                                                                     
       Henry       14                                                                                     
       Judy        14                                                                                     
       Janet       15                                                                                     
       Mary        15                                                                                     
       Ronald      15                                                                                     
       William     15                                                                                     
       Philip      16                                                                                     
                                                                                                          
                                                                                                          
    RULES                                                                                                 
    -----                                                                                                 
                                                                                                          
      NAME       AGE      AGE                                                                             
                                                                                                          
                        +------                                                                           
      Joyce       11    |  11                                                                             
      Thomas      11    |  11                                                                             
      James       12    |  12 background                                                                  
      Jane        12    |  12 clor                                                                        
      John        12    |  12 green                                                                       
      Louise      12    |  12                                                                             
      Robert      12    |  12                                                                             
                        +-------                                                                          
      Alice       13    |  13                                                                             
      Barbara     13    |  13 default                                                                     
      Jeffrey     13    |  13 backgroud                                                                   
      Alfred      14    |  14 color                                                                       
      Carol       14    |  14 white                                                                       
      Henry       14    |  14                                                                             
      Judy        14    |  14                                                                             
                        +------                                                                           
      Janet       15    |  15                                                                             
      Mary        15    |  15 background                                                                  
      Ronald      15    |  15 clor                                                                        
      William     15    |  15 yellow                                                                      
      Philip      16    |  16                                                                             
                        +------                                                                           
    *            _               _                                                                        
      ___  _   _| |_ _ __  _   _| |_                                                                      
     / _ \| | | | __| '_ \| | | | __|                                                                     
    | (_) | |_| | |_| |_) | |_| | |_                                                                      
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                     
                    |_|                                                                                   
    ;                                                                                                     
                                                                                                          
    WORKBOOK d:/xls/class.xlsx                                                                            
                                                                                                          
       d:/xls/class.xlsx                                                                                  
          +---------=---------------+                                                                     
          |     A   |       B       |                                                                     
          +---------+---------------+                                                                     
       1  | NAME    | Age           |                                                                     
          +---------+---------------+                                                                     
       2  | ALFRED  | 11 (green)    |                                                                     
          +---------+---------------+                                                                     
       3  | BARBARA | 11 (green)    |                                                                     
          +---------+---------------+                                                                     
       3  | DAVID   | 11 (green)    |                                                                     
          +---------+---------------+                                                                     
           ...                                                                                            
          +---------+---------------+                                                                     
       20 | WILLIAM | 16 (yellow)   |                                                                     
          +---------+---------------+                                                                     
                                                                                                          
       [CLASS]                                                                                            
                                                                                                          
    *          _       _   _                                                                              
     ___  ___ | |_   _| |_(_) ___  _ __                                                                   
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                  
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                 
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                 
                                                                                                          
    ;                                                                                                     
                                                                                                          
    %utlfkil(d:/xls/traffic.xlsx);                                                                        
                                                                                                          
    proc catalog catalog=work.formats;                                                                    
      delete age.format;                                                                                  
    run;quit;                                                                                             
                                                                                                          
    proc sort data=sashelp.class(keep=name age) out=class;                                                
      by age;                                                                                             
    run;quit;                                                                                             
                                                                                                          
    ods excel file="d:/xls/traffic.xlsx";                                                                 
                                                                                                          
    ods excel options                                                                                     
           (                                                                                              
             sheet_name                 = "Traffic"                                                       
             autofilter                 = "yes"                                                           
             frozen_headers             = "1"                                                             
             frozen_rowheaders          = "1"                                                             
             gridlines                  = "yes"                                                           
            );                                                                                            
    ;run;quit;                                                                                            
                                                                                                          
    proc report data =class(                                                                              
       where=( 0=%sysfunc(dosubl('                                                                        
                   proc format;                                                                           
                     value age                                                                            
                         11,12 = "light green"                                                            
                         13,14 = "white"                                                                  
                         15,16 = "yellow"                                                                 
                   ;run;quit;                                                                             
                   '))));                                                                                 
    cols name age;                                                                                        
    define name / display;                                                                                
    define age  / display style(column)={background=age.};                                                
    run;quit;                                                                                             
                                                                                                          
    ods excel close;                                                                                      
                                                                                                          
                                                                                                          
                                                                                                          
