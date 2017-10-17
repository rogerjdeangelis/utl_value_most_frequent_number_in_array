# utl_value_most_frequent_number_in_array
Given an array of numbers with duplication, select the number with the max frequency. Big data analytics. Data management.

    ```  Identify the most frequent number in an array                                                                                                                ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```         array buc[99] _temporary_ (99*0);  * only 99 slots possible if 1 to 2 digits;                                                                         ```
    ```         array cs c:;                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```         do i=1 to dim(cs);                                                                                                                                    ```
    ```           buc[cs[i]]=sum(buc[cs[i]],1);    * fill in frequencies;                                                                                             ```
    ```         end;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```         maxFrq=whichn(max (of buc[*]),of buc[*]); * this tricky because the bucket index                                                                      ```
    ```                                                     is also the bucket number;                                                                                ```
    ```                                                                                                                                                               ```
    ```    10 million  200 bytes per record is only  2gb I can load 32 of them into ram on my $600                                                                    ```
    ```    dell T7400 workstation?                                                                                                                                    ```
    ```    even with 8 bytes per variable it is only 8gb. 1Tb costs about $25, 2gb costs about 5 cents.                                                               ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/programming-help/m-p/403056                                                                              ```
    ```                                                                                                                                                               ```
    ```  see gamotte profile                                                                                                                                          ```
    ```  https://communities.sas.com/t5/user/viewprofilepage/user-id/30622                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  WORK.HAVE total obs=4               |          RULES                                                                                                         ```
    ```                                      |         maxFreq                                                                                                        ```
    ```  Obs    C1    C2    C3    C4    C5   |                                                                                                                        ```
    ```                                      |     15   because it occurs the most often                                                                              ```
    ```   1     10    12    15    55    15   |     15   because it occurs the most often                                                                              ```
    ```   2     10    10    15    10    12   |                                                                                                                        ```
    ```   3     10    10    10    10    10   |                                                                                                                        ```
    ```   4     10    10    12    12    15   |                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                      |                                                                                                                        ```
    ```  WANT                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  WORK.WANT total obs=4                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  Obs    C1    C2    C3    C4    C5    MAXFRQ                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```   1     10    12    15    55    15      15                                                                                                                    ```
    ```   2     10    10    15    10    12      10                                                                                                                    ```
    ```   3     10    10    10    10    10      10                                                                                                                    ```
    ```   4     10    10    12    12    15      10                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```  input C1 C2 C3 C4 C5;                                                                                                                                        ```
    ```  cards4;                                                                                                                                                      ```
    ```  10 12 15 55 15                                                                                                                                               ```
    ```  10 10 15 10 12                                                                                                                                               ```
    ```  10 10 10 10 10                                                                                                                                               ```
    ```  10 10 12 12 15                                                                                                                                               ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data want(drop=i);                                                                                                                                           ```
    ```    array buc[99] _temporary_ (99*0);                                                                                                                          ```
    ```    set have;                                                                                                                                                  ```
    ```    array cs c:;                                                                                                                                               ```
    ```    do i=1 to dim(cs);                                                                                                                                         ```
    ```      buc[cs[i]]=sum(buc[cs[i]],1);                                                                                                                            ```
    ```    end;                                                                                                                                                       ```
    ```    maxFrq=whichn(max (of buc[*]),of buc[*]);                                                                                                                  ```
    ```    output;                                                                                                                                                    ```
    ```    call missing(of c:);                                                                                                                                       ```
    ```  run;quit;                                                                                                                                                    ```

