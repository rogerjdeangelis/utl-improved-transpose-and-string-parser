# utl-improved-transpose-and-string-parser
Improved transpose and string parser.
    Improved transpose and string parser

    github
    https://github.com/rogerjdeangelis/utl-improved-transpose-and-string-parser

      1. Parsing pairs into an array
         ELIZIBETH:34|MARY:56|KATE:22|MAGIE:51|MIKE:22

      2. Transpose and parse pairs into an array
         ELIZIBETH:34|MARY:56

      3. Names into an array
         ELIZIBETH MARY KATE MAGIE MIKE

      4. Two sets into two arrays
         ELIZIBETH MARY KATE MAGIE MIKE Y Y N N Y

      5. Name of set then set of values
         NAMES ELIZIBETH MARY KATE MAGIE MIKE
         SEX F F F F M


    ALGORITHMS
    ==========

    1. Parsing pairs ito an array
    =============================

    * parmcards by data_null_;
    filename ft15f001 temp;
    parmcards4;
    ELIZIBETH:34|MARY:56|KATE:22|MAGIE:51|MIKE:22
    ;;;;
    run;quit;

    data want_pairs;
      infile ft15f001 dlm=':|';
      input  (n1 v1 n2 v2 n3 v3 n4 v4 n5 v5)  (: $16.) ;
      put (_all_) (= $ /);
    run;quit;

    N1=ELIZIBETH
    V1=34

    N2=MARY
    V2=56

    N3=KATE
    V3=22

    N4=MAGIE
    V4=51

    N5=MIKE
    V5=22


    2. Transpose and parse pairs into an array
    =============================================
    filename ft15f001 temp;
    parmcards4;
    ELIZIBETH:34|MARY:56
    ;;;;
    run;quit;

    * I do not think you need the output if more thsn one line of input;
    data want_parXpo;
      infile ft15f001 dlm=':|';
      input  name$ age$ @;output;
      input  name$ age$ ;
      output;
    run;quit;

    WORK.WANT_PARXPO total obs=2

     NAME        AGE

     ELIZIBET    34
     MARY        56


    3. Names into an array
    ======================

    filename ft15f001 temp;
    parmcards4;
    ELIZIBETH MARY KATE MAGIE MIKE
    ;;;;
    run;quit;

    data want_parAry;
      infile ft15f001;
      input ( name1 - name5 ) (: $16.);
      output;
    run;quit;


    WORK.WANT_PARARY total obs=1

        NAME1      NAME2    NAME3    NAME4    NAME5

      ELIZIBETH    MARY     KATE     MAGIE    MIKE


    4. Two sets into two arrays
    ===========================

    filename ft15f001 temp;
    parmcards4;
    ELIZIBETH MARY KATE MAGIE MIKE 27 45 34 23 19
    ;;;;
    run;quit;

    data want_twoAry;
      infile ft15f001;
      input ( name1 - name5 ) (: $16.) age1-age5 ;
      output;
    run;quit;

    Middle Observation(1 ) of want_twoAry - Total Obs 1

     -- CHARACTER --
    NAME1  C16      ELIZIBETH
    NAME2  C16      MARY
    NAME3  C16      KATE
    NAME4  C16      MAGIE
    NAME5  C16      MIKE

     -- NUMERIC --
    AGE1   N8       27
    AGE2   N8       45
    AGE3   N8       34
    AGE4   N8       23
    AGE5   N8       19



    5. Name of set then set of values
    =================================

    filename ft15f001 temp;
    parmcards4;
    NAMES ELIZIBETH MARY KATE MAGIE MIKE
    SEX F F F F M
    ;;;;
    run;quit;

    data want_twoAry;
      infile ft15f001;
      input grp$ @;
      input ( namSex1 - namSex5 ) (: $16.);
    run;quit;

    WORK.WANT_TWOARY total obs=2

      GRP     NAMSEX1      NAMSEX2    NAMSEX3    NAMSEX4    NAMSEX5

     NAMES    ELIZIBETH     MARY       KATE       MAGIE      MIKE
     SEX      F             F          F          F          M


