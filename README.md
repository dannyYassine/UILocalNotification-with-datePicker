# UILocalNotification-with-datePicker

User decides the time of the day to be notified from the app.

User choses the time of the reminder from an UIDatePicker somewhere in the app. NSUserDefaults can be used to save this preference.

  -(void) setTimer {
  
          //Where date is from a UIDatePicker chosen by the User
          NSDate *date = [[NSUserDefaults standardUserDefaults] objectForKey:@"dateReminder"];
          
          NSCalendar *calendar = [NSCalendar currentCalendar];
          NSDateComponents *dateComponents = [calendar components:(NSCalendarUnitHour | NSCalendarUnitMinute) fromDate:date];
          
          NSInteger hour = [dateComponents hour];
          NSInteger minute = [dateComponents minute];
          
          [dateComponents setHour:hour];
          [dateComponents setMinute:minute];
          
          UILocalNotification *reminderNote = [[UILocalNotification alloc]init];
          reminderNote.fireDate = [calendar dateFromComponents:dateComponents];
          reminderNote.repeatInterval = NSCalendarUnitDay;
          reminderNote.alertBody = @"Hey! Open the App!";
          reminderNote.timeZone = [NSTimeZone defaultTimeZone]
          reminderNote.alertAction = @"View";
          reminderNote.soundName = UILocalNotificationDefaultSoundName;
          [[UIApplication sharedApplication] scheduleLocalNotification:reminderNote];
        
      
  }
