# MATLAB with Jupyter 


## 1. [Magic Method for Jupyter Notebook](https://sehyoun.com/blog/20180904_using-matlab-with-jupyter-notebook.html)

```python 

import matlab.engine
import io #python 3
#import StringIO as io#python 2
from IPython.core.magic import register_cell_magic
ip = get_ipython()

out = io.StringIO()
err = io.StringIO()

# Setup matlab cell magic #
@register_cell_magic
def matlab_magic(line,cell):
    out.truncate(0)
    out.seek(0)
    err.truncate(0)
    err.truncate(0)
    raw = '''{line}.eval("""{cell}""", nargout=0, stdout=out, stderr=err)'''
    ip.run_cell(raw.format(line=line, cell=cell))
    print(out.getvalue())
    print(err.getvalue())

```

```python 
eng = matlab.engine.start_matlab()



%%matlab_magic eng
x = 5;
disp(x);
x

```