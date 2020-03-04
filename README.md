# utl-creating_77-additional-variables-do-not-use-a-macro-use-a-datastep-array
Creating 77 additional variables. Do not use a macro use a datastep array.

    Creating 77 additional variables. Do not use a macro use a datastep array.

    github
    https://tinyurl.com/wsmxxa2
    https://github.com/rogerjdeangelis/utl-creating_77-additional-variables-do-not-use-a-macro-use-a-datastep-array

    SAS Forum
    https://tinyurl.com/u6z49m5
    https://communities.sas.com/t5/SAS-Programming/Trying-to-use-SAS-macro-to-create-variable-name/m-p/628485

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
       retain component 'Counts';
       call streaminit(4321);
       do rec=1 to 30;
          Fdevyr = int(100*rand('uniform'));
          Flye = int(100*rand('uniform'));
          Fdevm = int(100*rand('uniform'));
          count=47+int(4*rand('uniform'));
          output;
       end;
    run;quit;


    WORK.HAVE total obs=30

    Obs    COMPONENT    REC    FDEVYR    FLYE    FDEVM    COUNT

      1     Counts        1      79       37       92       47
      2     Counts        2      21       69       45       48
      3     Counts        3      46       37       87       47
      4     Counts        4      74       22       24       49
      5     Counts        5      28       95       10       47
      6     Counts        6      89       67       79       50
     ...

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WORK.WANT total obs=19                                                 77 ADDITIONAL VARIABLES

                                                                   AMOUNT_    AMOUNT_    AMOUNT_  ..  AMOUNT_
    Obs    COMPONENT    REC    FDEVYR    FLYE    FDEVM    COUNT       01         02         03           077

      1     Counts        1      79       37       92       47        49         49         49    ..     49
      2     Counts        2      21       69       45       48        49         49         49           49
      3     Counts        4      74       22       24       49        49         49         49           49
      4     Counts        8      35       98       96       49        49         49         49           49
      5     Counts        9       4       29       17       49        49         49         49           49
      6     Counts       10      83       42       94       47        49         49         49           49
      7     Counts       11      47       76       75       50        49         49         49           49
      8     Counts       13      52       11       29       47        49         49         49           49
      9     Counts       14      43       49       60       47        49         49         49           49
     10     Counts       17      66       16       31       49        49         49         49           49
     11     Counts       19      50       39       24       50        49         49         49           49
     12     Counts       20      68       59       81       49        49         49         49           49
     13     Counts       21      35       11       37       47        49         49         49           49
     14     Counts       22      41       12       26       49        49         49         49           49
     15     Counts       23      62       66       90       47        49         49         49           49
     16     Counts       24      32       73       79       50        49         49         49           49
     17     Counts       25      98       21       86       48        49         49         49           49
     18     Counts       26      35       80       82       48        49         49         49           49
     19     Counts       29      13       78       40       49        49         49         49    ..     49


    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;


    data want(drop=amount_04-amount_077);

      set have;

      array sev[77] amount_01-amount_077  (77*49);

      do i= 1 to 77;

        if i>1 then do;

           if (Fdevyr + Flye) - Fdevm  = (i-1) then
              do;
                 if component = 'Counts' then
                 sev[i] = count;
                 output;
              end;

            end;

        end;

    run;quit;

