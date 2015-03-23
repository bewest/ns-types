


## how big are medical records?

`HBG` is code for `LD`'s son.  He's kept immaculate records of all data.

How big is it?


## total?

```bash
$ du -h -s ../../HBG/*
119M    ../../HBG/All_Hayden_Data_R2
45M     ../../HBG/All Hayden's Data R2.zip
4.0K    ../../HBG/emailFromLane
4.0K    ../../HBG/hbg1.R
4.0K    ../../HBG/hbg2.R
4.0K    ../../HBG/hbg3.R
4.0K    ../../HBG/hbgRawDataProcessing.py
4.0K    ../../HBG/HBG.Rproj
4.0K    ../../HBG/tr_function.R
bewest@paragon:~/src/tidepool/blip-repo-data$ 

```

## just the data?

```bash
$ du -h -s ../../HBG/*/*
83M     ../../HBG/All_Hayden_Data_R2/All_Hayden_Data_R2.csv
37M     ../../HBG/All_Hayden_Data_R2/All Hayden's Data R2.xlsx

```

## how much data?

```bash
$ head -n 15 ../../HBG/All_Hayden_Data_R2/All_Hayden_Data_R2.csv | tail -n 6
DEVICE DATA (422463 records),,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
Data Range,8/29/2009 9:27,to,7/30/2012 20:28,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
Index,Date,Time,Timestamp,New Device Time,BG Reading (mg/dL),Linked BG Meter ID,Temp Basal Amount (U/h),Temp Basal Type,Temp Basal Duration (hh:mm:ss),Bolus Type,Bolus Volume Selected (U),Bolus Volume Delivered (U),Programmed Bolus Duration (hh:mm:ss),Prime Type,Prime Volume Delivered (U),Suspend,Rewind,BWZ Estimate (U),BWZ Target High BG (mg/dL),BWZ Target Low BG (mg/dL),BWZ Carb Ratio (grams),BWZ Insulin Sensitivity (mg/dL),BWZ Carb Input (grams),BWZ BG Input (mg/dL),BWZ Correction Estimate (U),BWZ Food Estimate (U),BWZ Active Insulin (U),Alarm,Sensor Calibration BG (mg/dL),Sensor Glucose (mg/dL),ISIG Value,Daily Insulin Total (U),Raw-Type,Raw-Values,Raw-ID,Raw-Upload ID,Raw-Seq Num,Raw-Device Type
1,8/29/2009,9:27:00,8/29/2009 9:27,,43,,,,,,,,,,,,,,,,,,,,,,,,,,,,BGTherasense,"AMOUNT=43, TEMPERATURE_STATUS=false, CAL_CODE=0",2356523215,2828008,37,FreeStyle
2,8/29/2009,11:41:00,8/29/2009 11:41,,204,,,,,,,,,,,,,,,,,,,,,,,,,,,,BGTherasense,"AMOUNT=204, TEMPERATURE_STATUS=false, CAL_CODE=0",2356523214,2828008,36,FreeStyle
3,8/30/2009,16:51:00,8/30/2009 16:51,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,CheckTherasenseControlSolution,"TEMPERATURE_STATUS=false, CAL_CODE=0, AMOUNT=106",2356523213,2828008,0,FreeStyle

```

```bash

tail -n 2 ../../HBG/All_Hayden_Data_R2/All_Hayden_Data_R2.csv
422462,7/30/2012,20:28:16,7/30/2012 20:28,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,CurrentVariableBolusEnable,ENABLE=true,8876487822,51543163,2,Paradigm Revel - 723
422463,7/30/2012,20:28:17,7/30/2012 20:28,,,,,,,,,,,,,Suspended,,,,,,,,,,,,,,,,,ChangeSuspendEnable,"ENABLE=user_suspend, ACTION_REQUESTOR=rf_diagnostic, PRE_ENABLE=null",8876487907,51543163,86,Paradigm Revel - 723


```