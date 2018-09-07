# pytest

install the latest version of pytest

```bash
sudo -H pip3 install -U pytest
```

run pytest with verbose

```bash
pytest -v file_or_dir_name
```

run pytest with printing

```bash
pytest -s file_or_dir_name
```

> test_a.py

```python
import pytest

def setup_module(module):
    #init_something()
    print('init')

def teardown_module(module):
    #teardown_something()
    print('down')

def test_upper():
    assert 'foo'.upper() == 'FOO'

def test_isupper():
    assert 'FOO'.isupper()

def test_failed_upper():
    assert 'foo'.upper() == 'FOo'
```

> test_b.py

```python
import pytest

def setup():
    print("basic setup into module")

def teardown():
    print("basic teardown into module")

def setup_module(module):
    print("module setup")

def teardown_module(module):
    print("module teardown")

def setup_function(function):
    print("function setup")

def teardown_function(function):
    print("function teardown")

def test_numbers_3_4():
    print("test 3*4")
    assert 3*4 == 12

def test_strings_a_3():
    print("test a*3")
    assert 'a'*3 == 'aaa'
```

> ptest_c.py

```python
import pytest

class TestUM:
    def setup(self):
        print ("basic setup into class")

    def teardown(self):
        print ("basic teardown into class")

    def setup_class(cls):
        print ("class setup")

    def teardown_class(cls):
        print ("class teardown")

    def setup_method(self, method):
        print ("method setup")

    def teardown_method(self, method):
        print ("method teardown")

    def test_numbers_5_6(self):
        print("test 5*6")
        assert 5*6 == 30

    def test_strings_b_2(self):
        print("test b*2")
        assert 'b'*2 == 'bb'
```

> test_d.py

```python
import pytest

@pytest.yield_fixture()
def resource_setup():
    print("resource_setup")
    yield
    print("resource_teardown")

def test_1_that_needs_resource(resource_setup):
    print("test_1_that_needs_resource")
```
