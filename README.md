# utl_find_the_consecutively_matched_pattern_11_in_11110001101
Find the consecutively matched pattern 11 in 11110001101. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Find the consecutively matched pattern 11 in 11110001101

    see
    https://goo.gl/C8w4E7
    https://github.com/rogerjdeangelis/utl_find_the_consecutively_matched_pattern_11_in_11110001101

      Two Solutions

         WPS/SAS base
         WPS/PROC R

    see
    https://goo.gl/oWhrZC
    https://stackoverflow.com/questions/48239756/find-the-consecutively-matched-pattern-index


    INPUT
    =====
                             | RULES find all non overlapping  11s in 11110001101
        x1 = "11110001101";  |
                             | START    END
                             |
                             |   1       2
                             |   3       4
                             |   8       9


    PROCESS
    =======

       R Working Code

          want<-str_locate_all(pattern = "11", x1);

       WPS/SAS (All the code - cleaner than PRX?)

          data want(keep=beg end);
             x1 = "11110001101";
             do pos=1 to length(x1)-1;
                want= find(x1,'11',pos);
                if want then do;
                   beg=want;
                   end=want+1;
                   put beg= end=;
                   pos=want+1;
                   output;
                end;
             end;
          run;quit;

    OUTPUT
    ======

     R  WORK.WANT total obs=3

        START    END

          1       2
          3       4
          8       9

     WPS/SAS WORK.WANT total obs=3

         BEG     END

          1       2
          3       4
          8       9

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

     data in script

       x1 = "11110001101";

    *                      __
    __      ___ __  ___   / /__  __ _ ___
    \ \ /\ / / '_ \/ __| / / __|/ _` / __|
     \ V  V /| |_) \__ \/ /\__ \ (_| \__ \
      \_/\_/ | .__/|___/_/ |___/\__,_|___/
             |_|
    ;

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    data wrk.want(keep=beg end);
       x1 = "11110001101";
       do pos=1 to length(x1)-1;
          want= find(x1,"11",pos);
          if want then do;
             beg=want;
             end=want+1;
             put beg= end=;
             pos=want+1;
             output;
          end;
       end;
    run;quit;
    ');

    *                      ______
    __      ___ __  ___   / /  _ \
    \ \ /\ / / '_ \/ __| / /| |_) |
     \ V  V /| |_) \__ \/ / |  _ <
      \_/\_/ | .__/|___/_/  |_| \_\
             |_|
    ;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    libname hlp sas7bdat "C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(haven);
    library(stringr);
    have<-read_sas("d:/sd1/have.sas7bdat");
    x1 <- "11110001101";
    want<-as.data.frame(str_locate_all(pattern = "11", x1));
    endsubmit;
    import r=want data=wrk.want;
    run;quit;
    ');

