# utl-add-a-column-to-the-table-if-the-column-does-not-exist
Add a column to the table if the column does not exist
    Add a column to the table if the column does not exist

    github
    https://tinyurl.com/t37w528
    https://github.com/rogerjdeangelis/utl-add-a-column-to-the-table-if-the-column-does-not-exist

    SAS Forum
    https://tinyurl.com/tsm27ux
    https://communities.sas.com/t5/SAS-Programming/check-if-a-field-exist-and-if-not-to-create-a-field-with-missing/m-p/612999

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
      set sashelp.gas(obs=5);
    run;quit;

    WORK.HAVE total obs=171

       FUEL      CPRATIO    EQRATIO     NOX

      Ethanol      12.0      0.907     3.741
      Ethanol      12.0      0.761     2.295
      Ethanol      12.0      1.108     1.498
      Ethanol      12.0      1.016     2.881
      Ethanol      12.0      1.189     0.760
    ...

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WANT total obs=5
                                                              | RULE
       WORKSTATION     FUEL      CPRATIO    EQRATIO     NOX   |
                                                              |
          BEAST       Ethanol       12       0.907     3.741  | Variable 'BEAST' added
          BEAST       Ethanol       12       0.761     2.295  | because it did not exist
          BEAST       Ethanol       12       1.108     1.498  |
          BEAST       Ethanol       12       1.016     2.881  |
          BEAST       Ethanol       12       1.189     0.760  |

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    data _null_;

      rc=open('sashelp.gas');
      pos=varnum(rc,'workstation');

      if pos=0 then do;
         rc=dosubl('

         data want;
           retain workstation "BEAST";
           set have;
         run;quit;

        ');
      end;

    run;quit;

