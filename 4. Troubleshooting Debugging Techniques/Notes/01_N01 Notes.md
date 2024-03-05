# Introduction to Debugging

<br>
<br>

## Silently Crashing Application

```
$ cd ~/purplebox/


purplebox$ ./purplebox.py


purplebox$ strace ./purplebox.py
-lots of output


purplebox$ strace -o failure.strace .purplebox.py
-lots of output


purplebox$ less failure.strace
...
openat(AT_FDCND, "/home/user/.config/purplebox", O_RDONLY|O_NONBLOCK|O_CLOEXEC|0_DIRECTORY) = -1 ENOENT (No such file or directory) # Eksik dosya yada klasör hatası 


purplebox$ mkdir ~/.config/purplebox


purplebox$ ./purplebox.py # program çalıştı.
```

<br>
<br>

# Understanding the Problem

<br>
<br>

## Intermittently Failing Script

```
$ cd meeting_reminder


meeting_reminder$ ./meeting_reminder.sh
```

![Ekran görüntüsü 2024-02-02 151548](https://github.com/kemda2/Google-Courses/assets/19648132/43c468bd-3d6e-44fc-ac08-ee0d71ed2add)

```
meeting_reminder$ atom meeting_reminder.sh
meeting_info=$(zenity --forms \
    --title 'Meeting' --text 'Reminder information' \
    --add-calendar 'Date' --add-entry 'Title' \
    --add-entry 'Emails' \
    2>/dev/null)

echo $meeting_info

if [[ -n "$meeting_info" 1]]; then
    python3 send_reminders.py "$meeting_info"
fi


meeting_reminder$ ./meeting_reminder.sh
01/13/2020|Test|amanda
Failure to send email


meeting_reminder$ atom send_reminders.py
#!/usr/bin/env python3

# To trigger the error, LANG=en_US.UTF-8

import datetime
import email
import smtplib
import sys

def usage():
    print("send_reminders: Send meeting reminders")
    print()
    print("invocation:")
    print(" send_reminders 'date|Meeting Title|Emails' ")
    return 1

def dow(date):
    dateobj = datetime.datetime.strptime(date, r"%d/%m/%Y")
    return dateobj.strftime("%A")

def message_template(date, title):
    message = email.message.EmailMessage()
    weekday = dow(date)
    message['Subject'] = f'Meeting reminder: "{title}"'
    message.set_content(f'''

Hi all!

This is a quick mail to remind you all that we have a meeting about:
"{title}"
the {weekday} {date}.
See you there.
''')
    return message

def send_message(message, emails):
    smtp = smtplib.SMTP('localhost')
    message['From'] = 'noreply@example.com'
    for email in emails.split(','):
        del message['To']
        message['To'] = email
        smtp.send_message(message)
    smtp.quit()
    pass

def main():

    if len(sys.argv) < 2:
        return usage()

    try:
        date, title, emails = sys.argv[1].split('|')
        message = message_template(date, title)
        send_message(message, emails)
        print("Successfully sent reminders to:", emails)

    except Exception as e:
        print("Failure to send email", file=sys.stderr)

if __name__ == "__main__":
    sys.exit(main())


meeting_reminder$ ./meeting_reminder.sh
01/13/2020|Test|amanda
Failure to send email with: time_data '01/13/2020' does not match format '%d/%m/%Y'


meeting_reminder$ atom meeting_reminder.sh
meeting_info=$(zenity --forms \
    --title 'Meeting' --text 'Reminder information' \
    --add-calendar 'Date' --add-entry 'Title' \ I
    --add-entry 'Emails' \
    + --forms-date-format='%Y-%m-%d' \
    2>/dev/null)

echo $meeting_info

if [[ -n "$meeting_info" ]]; then
    python3 send_reminders.py "$meeting_info"
fi


meeting_reminder$ atom send_reminders.py
#!/usr/bin/env python3

# To trigger the error, LANG=en_US.UTF-8

import datetime
import email
import smtplib
import sys

def usage():
    print("send_reminders: Send meeting reminders")
    print()
    print("invocation:")
    print(" send_reminders 'date|Meeting Title|Emails' ")
    return 1

def dow(date):
    - dateobj = datetime.datetime.strptime(date, r"%d/%m/%Y") -
    + dateobj = datetime.datetime.strptime(date, r"%Y-%m-%d") +
    return dateobj.strftime("%A")

def message_template(date, title):
    message = email.message.EmailMessage()
    weekday = dow(date)
    message['Subject'] = f'Meeting reminder: "{title}"'
    message.set_content(f'''

Hi all!

This is a quick mail to remind you all that we have a meeting about:
"{title}"
the {weekday} {date}.
See you there.
''')
    return message

def send_message(message, emails):
    smtp = smtplib.SMTP('localhost')
    message['From'] = 'noreply@example.com'
    for email in emails.split(','):
        del message['To']
        message['To'] = email
        smtp.send_message(message)
    smtp.quit()
    pass

def main():

    if len(sys.argv) < 2:
        return usage()

    try:
        date, title, emails = sys.argv[1].split('|')
        message = message_template(date, title)
        send_message(message, emails)
        print("Successfully sent reminders to:", emails)

    except Exception as e:
        print("Failure to send email", file=sys.stderr)

if __name__ == "__main__":
    sys.exit(main())


meeting_reminder$ ./meeting_reminder.sh
2020-01-13|Test|amanda
Successfully sent reminders to: amanda
```

# Binary Searching 3 Problem
<br>
<br>

## Finding Invalid Data

```
$ cd import_data


import_data$ cat contacts.csv | ./import.py -—server test # üretim server'ı etkilenmesin diye test serverını kullanıyoruz.
Import error 


import_data$ wc -l contacts.csv
100 contacts.csv


import_data$ head -15 contacts.csv
Lynn Y. Lane,"P.O. Box 806, S784 Adipiscing Road",Panama,(496) 438-3936,863811-8896
Craig A. Marks,1683 Primis Av.,"Palestine, State of",(267) 181-1525,185098-9664
Venus K. Wooten,478-3002 Neque. Street,Togo,(492) 616-1465,835568-8980
Ifeoma Q. Alford,574-9507 Integer St.,French Guiana,(728) 524-7469,589242-0851
Xaviera Q. Keller,"P.0. Box 796, 6845 At St.",Romania,(972) 587-0317,113246-7109
Teagan X. Barlow,7802 Urna. St.,Italy,(407) 825-4265,892826-386S
Anastasia I. Gregory,"P.O. Box 907, 7803 Eleifend. St.",Kenya,(647) 244-8309,304519-2550
Hunter w. Soto,Ap #911-8124 Eget Ave,Sierra Leone,(967) S74-1705,488147-6610
Ahmed M. Baker,"Ap #252-5421 At, Rd.",0man,(SS7) 46S-1997,525926-0049
September Y. Carter,5659 Dui. St.,"Virgin Islands, United States",(724) S78-8290,607064-8131
Ahmed w. Ramsey,4278 Nec Av.,Sierra Leone,(950) 433-933S,763513-4476
Tate V. Shepherd,Ap #748-6362 Ullamcorper Street,Suriname,(776) 820-4067,607412-3362
Tatiana F. Duncan,"195-2365 Eu, Street",Mayotte,(936) Sis-9001,974615-9681
Isadora H. Munoz,7029 Morbi Rd.,Turks and Caicos Islands,(919) 732-4098,138089-7833
Preston X. Montoya,9941 Aliquam Ave,Timor-Leste,(193) 109-3193,922318-6710


import_data$ tail -20 contacts.csv
Myra Q. Torres,"P.O. Box 942, 5132 Odio Ave",Brazil,(418) 833-9405,786858-4215
Rashad L. Mcdonald,Ap #391-7931 Vestibulum Av.,Madagascar,(259) 570-5417,784060-5963
Leila D. Hyde,799-6623 Varius Rd.,Moldova,(479) 460-9168,285900-3945
Brennan X. Blake,246-8319 Ut Rd.,Cook Islands,(375) 484-2615,254033-7488
Briar Z. Peters,625 Quis Road,Zambia,(951) 421-2090,?65844-6955
Ruth A. Fuentes,408-4658 Sed St.,Benin,(801) 437-0854,866958-1459
Leila L. Gonzalez,"P.O. Box 834, 7009 Ante Rd.",Turkey,(164) 731-3343,375014-9183
Raymond G. Martin,Ap #482-1746 Auctor Ave,Marshall Islands,(716) 897-6947,544193-0301
Nehru E. Mathews,"P.O. Box 987, 8698 Lacus. Rd.",Equatorial Guinea,(436) 785-4709,188590-0769
Drake S. Nilliamson,"P.O. Box 136, 9468 Pede. Road",Slovenia,(109) 907-7668,892024-6397
Bradley 0. Sexton,"P.O. Box 197, 3474 Auctor St.",French Southern Territories,(448) 179-5607,579541-9018
Amal w. Benton,"P.O. Box 138, 7423 Nostra, St.",Syria,(688) 526-6632,978123-0918
Blaine P. Atkinson,"P.O. Box 795, 5709 Suspendisse St.",Holy See (Vatican City State),(116) 265-5850,5294
98-5964
Aaron 3. Reese,"P.0. Box 845, 9401 Duis Road",Ethiopia,(715) 711-6301,314217-0699
Claire Z. England,317-1945 Tortor. Ave,Antigua and Barbuda,(680) 481-7212,403078-7289
Ria Y. Hatfield,Ap #853-3952 Ac St.,Norfolk Island,(177) 838-2059,183263-6680
Austin V. Henry,Ap #418-5546 Sed St.,American Samoa,(793) 4Z6-1591,168172-2011
Kessie U. Rodriquez,"P.O. Box 605, 5348 Sed Ave",Micronesia,(495) 728-4534,425211-8262
Hade X. Morgan,Ap #348-6095 Risus Rd.,Bouvet Island,(158) 459-6441,403105-6023
Nynter T. Nashington,Ap #313-5371 Iaculis Rd.,Yemen,(661) 489-1590,908970-4390


import_data$ head -50 contacts.csv | ./import.py --server test
Import error 


import_data$ head -50 contacts.csv | head -25| ./import.py --server test
Import successful


import_data$ head -50 contacts.csv | tail -25| ./import.py --server test
Import error


import_data$ head -50 contacts.csv | tail -25 | head -13| ./import.py --server test
Import successful


import_data$ head -50 contacts.csv | tail -25 | tail -12 | head -6 | ./import.py --server test
Import error


import_data$ head -50 contacts.csv | tail -25 | tail -12 | head -6 | head -3 | ./import.py --server test
Import error


import_data$ head -50 contacts.csv | tail -25 | tail -12 | head -6 | head -3 |
Mechelle S. Fischer,"P.0. Box 548, 5515 In Avenue",Bulgaria,(766) 353-8154,836079-3486
Harding V. Berry,Ap #818-800 Elit. Avenue,Liberia,(182) 889-8702,735723-1674
Rhona K, England,Ap #193-1392 Sit Road,"Virgin Islands, United States",(151) 405-5437,439017-6784 # Rhona K'den sonra . olmalı


import_data$ atom contacts.csv
# Rhona K, England,Ap #193-1392 Sit Road,"Virgin Islands, United States",(151) 405-5437,439017-6784
Rhona K. England,Ap #193-1392 Sit Road,"Virgin Islands, United States",(151) 405-5437,439017-6784


import_data$ cat contacts.csv | ./import.py --server test
Import successful
```