# LV_binary_files

Module to read/write LabVIEW binary files including flattened data and TDMS (based on python3.6+numpy).

## Getting Started

Two classes are defined, one for each type of file:

* LV_fd() works with flattened data. It is a building block for a higher level class that reads/writes this kind of binary file.

* LV_TDMS() works with Technical Data Management Streaming (TDMS).

The former is more advanced in terms of development, although not all types of flattened data are implemented, the latter is highly incomplete and still in an experimental stage.

### Prerequisites

Naturally, the prerequisites for this module are the following:

* Python 3 (3.6 and above)

* Numpy

### Installing

There is not really an install procedure, you just download the module and make it available to `import` in your python scripts somewhere in you folder tree.

The kind of usage intended for LV_fd is the following:

```python
from LVBF import LV_fd

reader = LV_fd(endian='>', encoding='cp1252')

with open('some_file.bin', mode='rb') as reader.fobj:
    value0 = reader.read_numeric(reader.LVint32) # read one LVint32 value
    values = reader.read_numeric(reader.LVfloat64, c=2) # read two LVfloat64 values
    array0 = reader.read_array(reader.read_numeric, reader.LVint32) # read an array of LVint32 values
    array1 = reader.read_array(reader.read_numeric, reader.LVfloat64) # read an array of LVfloat64 values
    string0 = reader.read_string() # read one string
    strings = reader.read_array(reader.read_string) # read an array of strings
    timestamp = reader.read_array(reader.read_timestamp, reader.LVtimestamp) # read an array of LVtimestamp
    eof = reader.EOD() # check for End-Of-Data
    
    if not eof:
        raise EOFError('End-Of-Data not reached!')
```

## Contributing

... TBD

## License

This project is licensed under the BSD 3 clause License - see the [LICENSE.md](LICENSE.md) file for details.
