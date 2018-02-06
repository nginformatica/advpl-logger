# AdvPL Logger

> Keep track of what happens! Awesome logs for AdvPL

![AdvPL Logger](https://i.imgur.com/MQw7hER.png)

Keeping track of your AdvPL application, either desktop or webservice, may be a complex task. Inserting `ConOut`s everywhere
and exploring the `console.log` file is definitely **not** the way to go, so we created AdvPL Logger!

AdvPL Logger is a library with support for ANSI VT100 formatted strings that allows you to output your logs to both your
AppServer console and to the file system (with auto resource management).

## Examples

You create a logger passing a **context** to `:New()`, that is, a name to say what is being tracked.

- Simple
```xbase
Local oLogger := Logger():New( 'CAPYBARAS_MANAGEMENT' )
oLogger:Info( 'Capybara server started!' )
```

- Simulating a REST server
```xbase
User Function TestLogger
    Local nCounter
    Local nRandom
    Local aMethods
    Local aRoutes
    Local cMessage
    Local oLogger := Logger():New( 'REST_ADVPL' )
    oLogger:Log( 'Starting logger service' )
    oLogger:Info( 'Rest started on port {1}', { 8080 } )
    oLogger:Error( '500 internal server error {1} - {2} {1} {45}', { 'EITA', 'PREULA', 'FOO' } )
    oLogger:Warn( 'GET on /login is deprecated' )
    oLogger:Success( 'Loved all capybaras!' )

    aMethods := { 'GET', 'POST', 'PUT', 'PATCH', 'DELETE' }
    aRoutes := { '/login', '/users', '/user/10', '/capybaras', '/version', '/help' }
    For nCounter := 1 To 100
        cMessage := { aMethods[ Randomize( 1, 5 ) ], aRoutes[ Randomize( 1, 6 ) ] }
        nRandom := Randomize( 1, 15 )
        If nRandom == 6
            oLogger:Error( '{1} {2}', cMessage )
        ElseIf nRandom == 5 .Or. nRandom == 9
            oLogger:Warn( '{1} {2}', cMessage )
        Else
            oLogger:Info( '{1} {2}', cMessage )
        EndIf
        Sleep( Randomize( 150, 450 ) )
    Next
    Return
```

The log file can be found in your dictionary folder under `logs/`.

## Methods

- `:Log` (gray)
- `:Info` (cyan)
- `:Error` (red)
- `:Warn` (yellow)
- `:Success` (green)

## Formatting

This library supports string formatting with placeholders. You can do such things like:

```xbase
oLogger:Success( 'Server started at {1}:{2}', { '127.0.0.1', 8080 } )
```

All the methods support this format. Keep calm, with support all kind of data inside the formatting array and the
placeholders are positional.

## License

This work is licensed under MIT. All rights reserved.
