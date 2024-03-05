# My notes

```
>>> log = "July 31 07:51:48 mycomputer bad_process[12345]: ERROR Performing package upgrade" »> index = log.index(" [")
>>> print(log[index+l:index+6])
12345
```

```
>>> import re
>>> log = "July 31 07:51:48 mycomputer bad_process[12345]: ERROR Performing package upgrade"
>>> regex = r"\[(\d+)\]"
>>> result = re.search(regex, log)
>>> print(result[l])
12345
```


```
$ grep thon /usr/share/dict/words

Jonathon's
Marathon
Marathon's
Phae Phaethon's
Python
Python's diphthong
diphthong's
diphthongs
marathon
marathon's
marathoner
marathoner's
marathoners
marathons
python
python's
pythons
telethon
telethon's
telethons
thong
thong's
thongs

$ grep -i Python /usr/share/dict/words # -i büyük küçük harf olmadan eşleştirme
Python
Python's
Python
Python's
Pythons
```

```
$ grep l.rts /usr/share/dict/words
alerts
blurts
flirts
```


```
$ grep ^fruit /usr/share/dict/words #fruit ile başlayanlar
fruit
fruit's
fruitcake
fruitcake's
fruitcakes
fruited
fruitful
fruitfully
fruitfulness
fruitfulness's
fruitier
fruitiest
fruiting
fruition
fruition's
fruitless
fruitlessly
fruitlessness	
fruitlessness's
fruits
fruity
```

```
$ grep cat$ /usr/share/dict/words #cat ile bitenler
Muscat
bobcat
copy ducat
lolcat
muscat
polecat
pussycat
scat
tomcat
wildcat
```

```
>>> import re
>>> result = re.search(r"aza", "plaza")
>>> print(result)
<re.Match object; span=(2, 5), match='aza'>

>>> result = re.search(r"aza", "bazaar")
>>> print(result)
<re.Match object; span=(l, 4), match='aza'>

>>> result = re.search(r"aza", "maze")
>>> print(result)
None

>>> print(re.search(r"^x", "xenon"))
<re.Match object; span=(0, 1), match='x'>

>>> print(re.search(r"p.ng", "penguin")) 
<re.Match object; span=(0, 4), match='peng'>

>>> print(re.search(r"p.ng", "clapping"))
<re.Match object; span=(4, 8), match='ping'>

>>> print(re.search(r"p.ng", "sponge"))
<re.Match object; span=(l, 5), match='pong'>

>>> print(re.search(r"p.ng", "Pangaea", re.IGNORECASE))
<re.Match object; span=(0, 4), match='Pang'>
```

```
>>> print(re.search(r"[Pp]ython", "Python"))
<re.Match object; span=(0, 6), match='Python'>

>>> print(re.search(r"[a-z]way", "The end of the highway"))
<re.Match object; span=(18, 22), match='hway'>

>>> print(re.search(r"[a-z]way", "What a way to go"))
None

>>> print(re.search("cloud[a-zA-ZO-9]", "cloudy"))
<re.Match object; span=(0, 6), match='cloudy'>

>>> print(re.search("cloud[a-zA-Z0-9]", "cloud9"))
<re.Match object; span=(0, 6), match='cloud9'>

>>> print(re.search(r"[^a-zA-Z]", "This is a sentence with spaces.")) # not a letter
<re.Match object; span=(4, 5), match=' '>

>>> print(re.search(r"[^a-zA-Z ]", "This is a sentence with spaces.")) # not a letter or space
<re.Match object; span=(30, 31), match='.'>

>>> print(re.search(r "cat|dog", "I like cats."))
<re.Match object; span=(7, 10), match='cat'>

>>> print(re.search(r"cat|dog", "I like dogs."))
<re.Match object; span=(7, 10), match='dog'>

>>> print(re.search(r"cat|dog", "I like both dogs and cats."))
<re.Match object; span=(12, 15), match='dog'>

>>> print(re.findall(r"cat|dog", "I like both dogs and cats."))
['dog', 'cat']
```

```
>>> print(re.search(r"py.*n", "pygmalion"))
<re.Match object; (0,9), match:' Pygmalion'>

>>> print(re.search(r"Py.*n","Python Programming"))
<re.match object; (0,17), match:' Python Programmin'> # Star takes much character as possible

>>> print(re.search(r"py[a-z]n","Python Programming"))
<re.Match object; span=(0,6), match='python'>

>>> print(re.search(r"py[a-z]*n","Pyn"))
<re.Match object; span=(0,3), match='pyn'>

>>> print(re.search(r"o+l+","goldfish"))
<re.Match object; span=(l, 3), match='ol'>

>>> print(re.search(r"o+l+", "woolly"))
<re.Match object; span=(l, 5), match="ooll">

>>> print(re.search(r"0+l+", "boil"))
None

>>> print(re.search(r"p?each","To each thetr own")
<re.Match object; span=(3, 7), match='each'>

>>> print(re.search, "I like peaches")
<re.Match object; span=(7, 12), match='peach'>
```

```
>>> print(re.search(r".com", "welcome" ) ) 
<re.Match object; span=(2, 6), match='lcom'>

>>> print(re.search(r"\.com", "welcome")) 
None

>>> print(re.search(r"\.com", "mydomain.com")) 
<re.Match object; span=(8, 12), match='.com'>

>>> print(re.search(r"\w*", "This is an example")) 
<re.Match object; span=(0, 4), match:'This' >

>>> print(re.search(r"\w*", "And_this_is_another"))
<re.Match object; span=(0, 19), match='And_this_is_another'>
```

```
>>> print(re.search(r"A.*a", "Argentina"))
<re.Match object; span=(0, 9), match='Argentina'>

>>> print(re.search(r"A.*a", "Azerbaijan"))
<re.Match object; span=(0, 9), match='Azerbaija'>

>>> print(re.search(r"^A.*a$", "Azerbaijan"))
None

>>> print(re.search(r"^A.*a$", "Australia"))
<re.Match object; span=(0, 9), match='Australia >

>>> pattern = r"^[a-zA-Z_][a-zA-Z0-9_]*$"
>>> print(re.search(pattern, "_this_is_a_valid_variable_name"))	
<re.Match object; span=(0, 30), match='_this_is_a_valid_variable_name'>

>>> print(re.search(pattern, "this isn't a valid variable"))
None

>>> print(re.search(pattern, "my_variable1"))
<re.Match object; span=(0, 12), match='my_variable1'>

>>> print(re.search(pattern, "2my_variable1"))
None
```

```
>>> result = re.search(r"A(\w*), (\w*)$"> "Lovelace, Ada")
>>> print(result)
<re.Match object; span=(0, 13), match='Lovelace, Ada'>

>>> print(result.groups())
('Lovelace', 'Ada')

>>> print(result[0])
Lovelace, Ada

>>> print(result[l])
Lovelace

>>> print(result[2])
Ada
>>> "{} {}".format(result[2], result[l])
'Ada Lovelace'

>>> def rearrange_name(name) :
... result = re.search(r"A(\w*), (\w*)$", name)
...   if the result is None:
...     return name 
...   return "{} {}".format(result[2], resutt[1])

>>> rearrange_name("Lovelace, Ada")
'Ada Lovelace'

>>> rearrange_name("Ritchie, Dennis")
'Dennis Ritchie'

>>> rearrange_name("Hopper, Grace M.")
"Hopper, Grace M."

>>> def rearrange_name(name):
... result = re.search(r"^([\w .-]*), ([\w .-]*)$", name)
...   if result == None:
...	    return name
...   return "{} {}".format(result[2], result[1])

>>> rearrange_name("Hopper, Grace M.")
'Grace M. Hopper'
```

```
>>> print(re.search(r"[a-zA-Z]{5}", "a ghost"))
<re.Match object; span=(2, 7), match-'ghost'>

>>> print(re.search(r"[a-zA-Z]{5}", "a scary ghost appeared"))
<re.Match object; span=(2, 7), match-'scary'>

>>> print(re.findall(r"[a-zA-Z]{5}", "a scary ghost appeared"))
['scary', 'ghost', 'appea']

>>> print(re.findall(r"\b[a-zA-Z]{5}\b", "A scary ghost appeared"))
['scary', 'ghost']

>>> print(re.findall(r"\w{5,10}", "I really like strawberries"))
['really', 'strawberri']

>>> print(re.findall(r"\w{5,}", "I really like strawberries"))
['really', 'strawberries']

>>> print(re.search(r"s\w{,20}", "I really like strawberries"))
<re.Match object; span=(14, 26), match="strawberries">
```

```
>>> import re
>>> log = "July 31 07:51:48 mycomputer bad_process[12345]: ERROR Performing package upgrade"
>>> regex = r"\[(\d+)\]"
>>> result = re.search(regex, log)
>>> print(result[1])
12345

>>> result = re.search(regex, "A completely different string that also has numbers [34567]")
>>> print(result[1])
34567

>>> print(result[1])
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'NoneType' object is not subscriptable

>>> def extract_pid(log_line):
... regex = r"\[(\d+)\]"
... result = re.search(regex, log_line)
... if result is None:
...   return ""
... return result[1]
>>> print(extract_pid(log))
12345
>>> print(extract_pid("99 elephants in a [cage]"))

```

```
>>> re.split(r"[.?!]", "One sentence. Another one? And the last one!")
['One sentence', ' Another one', ' And the last one', '']

>>> re.split(r"([.?!])", "One sentence. Another one? And the last one!")
['One sentence', '.', ' Another one', '?', ' And the last one', '!', '']

>>> re.sub(r"[\w.%+-]+@[\w.-]+", "[REDACTED]", "Received an email for go_nuts95@my.example.com")
'Received an email for [REDACTED]'

>>> re.sub(r"^([\w .-]*), ([\w .—]*)$", r"\2 \1", "Lovelace, Ada")
'Ada Lovelace'
```

```

```
