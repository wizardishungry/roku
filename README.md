# roku

[![Documentation](https://godoc.org/jonwillia.ms/roku?status.svg)](http://godoc.org/jonwillia.ms/roku)

Roku ECP library written in Go

Inspired by https://github.com/ncmiller/roku-cli

The project started out aiming to essentially be a GoLang fork of roku-cli, adding in the options of VolumeUp and VolumeDown buttons.

It is now turning into a Roku [ECP](https://developer.roku.com/docs/developer-program/debugging/external-control-api.md) library, with accompanying CLI Roku Remote

## Library

### Installation

```bash
go get -u jonwillia.ms/roku
```
or use `go mod`

### Example

```go
package main

import (
  "jonwillia.ms/roku"
)

func main() {
  devices, err := roku.FindRokuDevices()
  if err != nil {
    panic(err)
  }
  r, err := roku.NewRemote(devices[0].Addr)
  if err != nil {
    panic(err)
  }
  err = r.VolumeUp()
  if err != nil {
    panic(err)
  }
  if r.Device.PowerMode == "PowerOn" {
    // ignoring errors for brevity
    r.PowerOff()
    r.Refresh()
  }
}

```

## CLI

### Installation

```bash
go get -u jonwillia.ms/roku
```

### Usage

```bash
roku -ip 192.168.1.51
```

You can also simply run
```bash
roku
```
and it will search for Roku devices on the network (takes an extra 3 seconds).
