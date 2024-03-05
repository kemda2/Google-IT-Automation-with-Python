# Notes

```
$ cat rearrange.py
#!/usr/bin/env python3

import re

def rearrange_name(name):
  result = re.search(r""([\w .]*), ([\w .]*)$", name)
  return "{} {}".format(result[2], result[1])

$ python3
Python 3.7.3 (default, Apr 3 2019, 05:39:12)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from rearrange import rearrange_name
>>> rearrange_name("Lovelace, Ada")
'Ada Lovelace'

$ cat rearrange_test.py
from rearrange import rearrange_name
import unittest

class TestRearrange(unittest.TestCase):
  def test_basic(self):
    testcase = "Lovelace, Ada"
    expected = "Ada Lovelace"
    self.assertEqual(rearrange_name(testcase), expected)

unittest.main()

$ chmod +x rearrange_test.py
$ ./rearrange_test.py
.
-------
Ran 1 test in 0.000s

OK

$ cat rearrange_test.py
from rearrange import rearrange_name
import unittest
class TestRearrange(unittest.TestCase):
  def test_basic(self):
    testcase = "Lovelace, Ada"
    expected = "Ada Lovelace"
    self.assertEqual(rearrange_name(testcase), expected)
  # Test empty eklendi.
  def test_empty(self):
    testcase = ""
    expected = ""
    self.assertEqual(rearrange_name(testcase), expected)
unittest.main()

$ ./rearrange_test.py
.E
---
ERROR: test_empty (__main__.TestRearrange)
---
Traceback (most recent call last):
  File "./rearrange_test.py", line 15, in test_empty
    self.assertEqual(rearrange_name(testcase), expected)
  File "/home/user/rearrange.py", line 7, in rearrange_name
    return "{} {}".format(result[2], result[1])
TypeError: 'NoneType' object is not subscriptable
---
Ran 2 tests in 0.001s
FAILED (errors=1)

import re
def rearrange_name(name):
  result = re.search(r""([\w .]*). ([\w .]*)$", name)
  # if eklendi
  if result is None:
    return ""
  return "{} {}".format(result[2], result[1])

$ ./rearrange_test.py
Ran 2 tests in 0.000s
OK
```

```
$ cat rearrange_test.py
from rearrange import rearrange_name
import unittest

class TestRearrange(unittest.TestCase):
  def test_basic(self):
  testcase = "Lovelace, Ada"
  expected = "Ada Lovelace"
  self.assertEqual(rearrange_name(testcase), expected)

  def test_empty(self):
  testcase = ""
  expected = ""
  5elf.a55ertEqual(rearrange_name(testcase), expected)

  # + test_double_name
  def test_double_name(self):
  testcése = "Hopper, Grace M."
  expected = "Grace M. Hopper"
  self.assertEqual(rearrange_name(testcase), expected)

unittest.main()

$ ./rearrange_test.py
Ran 3 tests in 0.000s
OK

$ cat rearrange_test.py
from rearrange import rearrange_name
import unittest

class TestRearrange(unittest.TestCase):
  def test_basic(self):
  testcase = "Lovelace, Ada"
  expected = "Ada Lovelace"
  self.assertEqual(rearrange_name(testcase), expected)

  def test_empty(self):
  testcase = ""
  expected = ""
  5elf.a55ertEqual(rearrange_name(testcase), expected)

  # + test_double_name
  def test_double_name(self):
  testcése = "Hopper, Grace M."
  expected = "Grace M. Hopper"
  self.assertEqual(rearrange_name(testcase), expected)

  # + test_one_name
  def test_one_name(self):
    testcase = "Voltaire"
    expected = "Voltaire"
    self.assertEqual(rearrange_name(testcase), expected)

unittest.main()

$ ./rearrange_test.py
...F
FAIL: test_one_name (__main__.TestRearrange)
Traceback (most recent call last):
  File "./rearrange_test.py", line 25, in test_one_name
    self.assertEqual(rearrange_name(testcase), expected)
AssertionError: " l: 'Voltaire'
+ Voltaire

Ran 4 tests in 0.001s

FAILED (failures=1)

$ cat rearrange_test.py
import re
def rearrange_name(name):
result = re.search(r""([\w .]*), ([\w .]*)$", name)
if result is None:
  return name # "" yerine name yazıldı
return "{} {}".format(result[2], result[1])

$ ./rearrange_test.py
Ran 4 tests in 0.000s
OK
```

```
$ cat charfreq.py
def character_frequency(filename):
  """Counts the frequency of each character in the given file."""
  # First try to open the filo
  try:
    f = open(filename)
  except OSError:
    return None
  # Now process the file
  characters = {}
  for line in f:
    for char in line:
      characters[char] = character5.get(char, 0) + 1
  f.close()
  return characters
```

```
$ cat validations.py
def validate_user(username, minlen):
  if len(username) < minlen:
    return False
  if not username.isalnum():
    return False
  return True

def validate_user(username, minlen):
  # if eklendi
  if minlen < 1:
    raise ValueError("minlen must be at least 1")
  if len(username) < minlen:
    return False
  if not username.isalnum():
    return False
  return True

$ python3
Python 3.7.3 (default, Apr 3 2019, 05:39:12)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from validations import validate_user
>>> validate_user("", -1)
Traceback (most recent call last):
  File "<5tdin>", line 1, in <module>
  File "/home/u5er/validations.py", line 5, in validate_user
    raise ValueError("minlen must be at least 1")
ValueError: minlen must be at least 1
>>> validate_user("", 1)
False
>>> validate_user("myuser", 1)
True
>>> validate_user(88, 1)
Traceback (most recent call last):
  File "<5tdin>", line 1, in <module>
  File "/home/user/validations.py", line 6, in validate_user
    if len(username) < minlen:
TypeError: object of type 'int' has no len()
>>> validate_user([], 1)
False
>>> validate_user(["name"], 1)
Traceback (most recent call last):
  File "<5tdin>", line 1, in <module>
  File "/home/user/validations.py", line 8, in validate_user
    if not username.isalnum():
AttributeError: 'list' object has no attribute 'isalnum'

$ cat validations.py
def validate_user(username, minlen): 
  assert type(username) == str, "username must be a string" # Assert eklendi.
  if minlen < 1:
    raise ValueError("minlen must be at least 1")
  if len(username) < minlen:
    return False
  if not username.isalnum():
    return False
  return True

$ python3
Python 3.7.3 (default, Apr 3 2019, 05:39:12)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from validations import validate_user
>>> validate_user([3], 1)
Traceback (most recent call last):
File "<5tdin>", line 1, in <module>
File "/home/u5er/validations.py", line 4, in validate_user
assert type(username) == str, "username must be a string"
AssertionError: username must be a string
```

```
$ cat validations.py
import unittest
from validations import validate_user
class TestValidateUser(unittest.TestCase):
  def test_valid(self):
    self.assertEqual(validate_user("validuser", 3), True)
  def test_too_short(5elf):
    self.assertEqual(validate_user("inv", 5), False)
  def test_invalid_characters(self):
    self.assertEqual(validate_user("invalid_user", 1), False)
  def test_invalid_minlen(self):
    self.assertRaises(ValueError, validate_user, "user", -1)
# Run the tests
unittest.main()

$ ./validations_test.py

Ran 4 tests in 0.000s
OK 
```
