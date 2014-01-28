Vagrants: vagrant for multi-directory support.
====
Do you want execute vagrant command for multiple directories at the same time??

This small script `vagrants` is a vagrant wrapper which cascades vagrant commands to sub directories you specified.

Usage
----
```
vagrants [-h] [-v]               -c (vagrant commands to be cascaded)
vagrants [-h] [-v] dir_name      -c (vagrant commands to be cascaded)
vagrants [-h] [-v] /dir_pattern/ -c (vagrant commands to be cascaded)

OPTIONS:
  -h       Print help.
  -v       Verbose mode.
```

Examples
----
Example sudir structure is like blow:

    $ cd examples
    $ ls */Vagrantfile
    teest1/Vagrantfile      test2/Vagrantfile       test3/Vagrantfile

### Example1: The simplest case
```
# below commands cascades 'status' to all subdirs.
$ ../vagrants -c status
[In ./teest1] 
    Current machine states:
    
    master1                   not created (virtualbox)
    master2                   not created (virtualbox)
    master3                   not created (virtualbox)
    
    This environment represents multiple VMs. The VMs are all listed
    above with their current state. For more information about a specific
    VM, run `vagrant status NAME`.

[In ./test2] 
    Current machine states:
    
    slave1                    not created (virtualbox)
    slave2                    not created (virtualbox)
    slave3                    not created (virtualbox)
    
    This environment represents multiple VMs. The VMs are all listed
    above with their current state. For more information about a specific
    VM, run `vagrant status NAME`.

[In ./test3] 
    Current machine states:
    
    default                   not created (virtualbox)
    
    The environment has not yet been created. Run `vagrant up` to
    create the environment. If a machine is not created, only the
    default provider will be shown. So if a provider is not listed,
    then the machine is not created for that environment.
```

### Example2: specifiy subdirectory name
```
$ ../vagrants test2 -c status
[In ./test2] 
  Current machine states:
  
  slave1                    not created (virtualbox)
  slave2                    not created (virtualbox)
  slave3                    not created (virtualbox)
  
  This environment represents multiple VMs. The VMs are all listed
  above with their current state. For more information about a specific
  VM, run `vagrant status NAME`.
```

### Example3: Using regular expression.
To specify subdirectories with regular expressions, you can use `/pattern/` like ruby regex objects (vagrant also support this to specify virtual machines).

```
$ ../vagrants /t*st[12]/ -c status /[ms].*[13]/                                                                       
[In ./teest1] 
  Current machine states:
  
  master1                   not created (virtualbox)
  master3                   not created (virtualbox)
  
  This environment represents multiple VMs. The VMs are all listed
  above with their current state. For more information about a specific
  VM, run `vagrant status NAME`.

[In ./test2] 
  Current machine states:
  
  slave1                    not created (virtualbox)
  slave3                    not created (virtualbox)
  
  This environment represents multiple VMs. The VMs are all listed
  above with their current state. For more information about a specific
  VM, run `vagrant status NAME`.
```

License and Author
----
* Author: Shingo Omura everpeace@gmail.com

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
