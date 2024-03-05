# My Notes

```
>>> file = open("spider.txt")
>>> print(file. readline()) # reading row by row.
The itsy bitsy spider climbed up the waterspout. 
>>> print(file. readline())
Down came the rain

>>> print(file.read())
and washed the spider out.
Out came the sun
and dried up all the rain
and the itsy bitsy spider climbed up the spout again.

file.close() # Closing is important.
```

```
>>> with open("spider.txt") as file:
    print(file.readline())
The itsy bitsy spider climbed up the waterspout.
```

```
>>> with open("spider.txt") as file:
>>>     for line in file:
...         print(line.upper())

THE ITSY BITSY SPIDER CLIMBED UP THE WATERSPOUT.
DOWN CAME THE RAIN
AND WASHED THE SPIDER OUT.
OUT CAME THE SUN
AND DRIED UP ALL THE RAIN
AND THE ITSY BITSY SPIDER CLIMBED UP THE SPOUT AGAIN.
```

```
>>> file = open("spider.txt")
>>> lines = file.readlines()
>>> file.close()
>>> lines.sort()
>>> print(lines)

['Down came the rain\n', 'Out came the sun\n', 'The itsy bitsy spider climbed up the waterspout.\n' , 'and dried up all the rain\n', 'and the itsy bitsy spider climbed up the spout again.\n', 'and wa shed the spider out.\n']

>>> with open("novel.txt", "w") as file:
...     file.write("It was a dark and stormy night")
30
```

![Ekran görüntüsü 2024-01-23 120300](https://github.com/kemda2/Google-Courses/assets/19648132/c2da0f8b-f124-4c3b-a982-d6b999343b1f)

```
>>> import os
>>> os.remove("novel.txt")
>>> os.remove("novel.txt")

Traceback (most recent call last):
File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: 'novel.txt'
```

```
>>> os.rename("first_draft.txt", "finished_masterpiece.txt")
```

```
>>> os.path.exists("finished_masterpiece.txt")
True
```

```
>>> os.path.getsize("spider.txt")
192
```

```
>>> os.path.getmtime("spider.txt")
1578322923.8999994
```


```
>>> import datetime
>>> timestamp = os.path.getmtime("spider.txt")
>>> datetime.datetime.fromtimestamp(timestamp)
datetime.datetime(2020, 1, 6, 7, 2, 3, 899999)

>>> os. path. abspath(" spider . txt" )
'/home/user/spider.txt'

>>> print(os.getcwd())
/home/user

>>> os.mkdir("new_dir") # New folder
>>> os.chdir("new_dir") # Change folder
>>> os.getcwd() # Show current folder
'/home/user/new_dir'

>>> os.mkdir("newer_dir")
>>> os.rmdir("newer_dir") # Remove folder

>>> import os
>>> os.listdir("website")
['images', 'index.html', 'favicon.ico']
```

```
>>> dir = "website"
>>> for name in os.listdir(dir):
...    fullname = os.path.join(dir, name)
...    if os.path.isdir(fullname):
...        print("{} is a directory".format(fullname))
...    else:
...	       print("{} is a file".format(fullname))

website/images is a directory
website/index.html is a file
website/favicon.ico is a file
```

```
$ cat csv_file.txt
Sabrina Green,802-867-5309,System Administrator
Eli Jones,684-3481127,IT specialist
Melody Daniels,846-687- 7436,Prog rammer
Charlie Rivera,698-746-3357,Web Developer
```

```
>>> import csv
>>> f = open("csv_file.txt")
>>> csv_f = csv.reader(f)
>>> for row in csv_f:
...     name, phone, role = row
... print("Name: {}, Phone: {}, Role: {}".format(name, phone, role))

Name: Sabrina Green, Phone: 802-867-5309, Role: System Administrator
Name: Eli Jones, Phone: 684-3481127, Role: IT specialist
Name: Melody Daniels, Phone: 846-687-7436, Role: Programmer
Name: Charlie Rivera, Phone: 698-746-3357, Role: Web Developer

>>> f.close()
```

```
>>> hosts = [["workstation.local", "192.168.25.46"], ["webserver.cloud", "10.2.5.6"]]
>>> with open('hosts.csv', 'w') as hosts_csv:
...	  writer = csv.writer(hosts_csv)
...	  writer.writerows(hosts)

$ cat hosts.csv
workstation.local,192.168.25.46
webserver.cloud,10.2.5.6
```

```
$ cat software.csv 
name,version,status,users 
MailTree,5.34,production,324 
CalDoor,1.25.1,beta,22 
Chatty Chicken,0.34,alpha,4

with open('software.csv') as software:
  reader = csv.DictReader(software) 
  for row in reader:
    print(("{} has {} users").format(row["name"], row["users"]))

MailTree has 324 users
CalDoor has 22 users
Chatty Chicken has 4 users
```

```
>>> users = [ {"name": "Sol Mansi", "username": "solm", "department": "IT infrastructure"},
>>>           {"name": "Lio Nelson", "username": "lion", "department": "User Experience Research },
>>>           {"name": "Charlie Grey", "username": "greyc", "department": "Development }]

keys = ["name", "username", "department"]

>>> with open('by_department.csv', 'w') as by_department:
...   writer = csv.DictWriter(by_department, fieldnames=keys)
...   writer.writeheader()
...   writer.writerows(users)

$ cat by_department.csv

name,username,department
Sol Mansi,solm,IT infrastructure
Lio Nelson,lion,User Experience Research
Charlie Grey,greyc,Development
```
