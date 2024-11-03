# Python learning

Tips:
1. For files and directory locations, note that "/xxxx" is NOT the same as "xxxx". The former denotes we start from the root directory. You might encounter this problem when applying os.path.join()


Q: Cannot detect `lib` as a module!  
A: Several common mistakes

1. Add `__init__.py` in the directory. This allows python to recognize this directory as a module.

2. `import sys`, then `sys.path.append(<PARENT_DIR>)`. Make sure it is the **parent** directory you are adding.  
