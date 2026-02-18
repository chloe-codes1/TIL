# ENTRYPOINT vs CMD

The biggest difference is whether a default is specified for the execution command when the container starts.

### ENTRYPOINT

> Defines the base command that is always executed
>
- Used when there is a command that must always be executed first when the container starts
- Even if arguments are passed via the `docker run` command, the existing command is still executed

### CMD

> Defines default parameters for the ENTRYPOINT command / can be overwritten at docker run
>
- A command that is executed when the container starts, but used when it needs to be changeable
- If arguments are passed via the `docker run` command, the command and arguments specified in `CMD` are ignored
