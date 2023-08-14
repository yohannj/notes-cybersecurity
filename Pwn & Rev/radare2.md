# Commands
## Help
Add `?` at the end of what we want to do.
`?` can be used alone for general help
`a?` will provide help on analysis commands


## Analyse program
`aa`

## Set assembly syntax to AT&T
`e asm.syntax=att`

## List functions
`afl` Analyze Function List

## Show function content
`pdf @FUNCTION_NAME` Print Disassembled Function (opcodes)
Format: Memory addr | instruction in bytes | instruction human readable

## Breakpoint
`db ADDR` Debug Breakpoint

## Run
`dc` Debug Continue execution
`ood` Launch debugger

## See variable value
`px @VAR_ADDR` Print heXdump.
It will display more than just our value, but our value will start at the beginning of the hexdump.

## See registers
`dr`

## Select a function
`s FUNCTION_NAME`

## Rename variable
`afvn NEW_NAME OLD_NAME`
