# Process memory
-- Higher memory addresses
User Stack (↓)     -- Info required to run the program (counters, registers, ...)
...
Shared library regions
...
Run time heap(↑)
R/W Data
RO code/data       -- Store executable + initialised variables.
-- 0 aka bottom

# Frame (function call) memory
ESP = Stack Pointer (where we start to write)
EBP = Base Pointer (beginning of our function)

ESP:    buf        -- let's start to write stuff (overflow write below, new stuff to write goes above)
        var2       -- variable created inside the method
        var1       -- variable created inside the method
EBP:    EBP(old)   -- Caller stack frame
        ret        -- return adress once we have finished using this function
        arg1       -- argument used to call the function
        arg2       -- argument used to call the function