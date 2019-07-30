### beets
---
https://github.com/beetbox/beets

http://beets.io/

```py
// test/test_parentwork.py
from __future__ import division, absolute_import, print_function

import unittest
from test.helper import TestHelper

from beets.library import Item
from beetsplug import parentwork

class ParentWorkTest(unittest.TestCase, TestHelper):
  def setUp(self):
    """ """
    self.setup_beets()
    self.load_plugins('parentwork')
    
  def tearDown(self):
    self.unload_plugins()
    self.teardown_beets()
    
  def test_normal_case(self):
    item = Item(path='/file',
      mb_workid=u'xxx')
      
      self.run_command('parentwork')
      
      item.load()
      self.assertEqual(item['mb_parentworkid'],
        u'xxx')
        
    def test_force(self):
      self.config['parentwork']['force'] = True
      item = Item(path='/file',
        mb_workid=u'xxx',
        mb_parentworkid=u'XXX')
      item.add(self.lib)
      
      self.run_command('parentwork')
      
      item.load()
      self.assertEqual(item['mb_parentworkid'],
        u'xxx')
        
    def test_no_force(self):
      self.config['parentwork']['force'] = True
      item = Item(path='/file', mb_work=u'xxx-\
        xxx', mb_parentworkid=u'XXX')
      item.add(self.lib)
      
      self.run_command('parentwork')
      
      item.load()
      self.assertEqual(item['mb_parentworkid'], u'XXX')

  def test_direct_parent_work(self):
    mb_workid = u'xxx'
    self.assertEqual(u'xxx',
      parentwork.direct_parent_id(mb_workid)[0])
    self.assertEqual(u'xxx',
      parentwork.work_parent_id(mb_workid)[0])
      
def suite():
  return unittest.TestLoader().loadTestsFromName(__name__)
  
if __name__ == '__main__':
  unittest.main(defaultTest='suite')

```

```sh
beet import ~/music/ladytron
```

```
```


