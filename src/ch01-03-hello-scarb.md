# Hello, Scarb!

## Install Scarb

Follow the instructions in the [Scarb documentation](https://docs.swmansion.com/scarb/download)
_Current Scarb version is 0.1.0-rc.2, comes with Cairo v0.1.0-alpha.6_

Verify installation by running

```bash
scarb --version
```

It should output something like

```bash
scarb 0.1.0-rc.2 (8e8d51d80 2023-03-20)
cairo: 1.0.0-alpha.6
```

## Creating a Project with Scarb

Let’s create a new project using Scarb and look at how it differs from our original “Hello, world!” project. Navigate back to your projects directory (or wherever you decided to store your code). Then, on any operating system, run the following:

```bash
scarb init hello-scarb
```

As the result of running scarb new, Scarb has created two files:

- `Scarb.toml` - a configuration file for Scarb
- `src/lib.cairo`

## Building and Running a Scarb Project
