---
layout: post
title: "Generating test doubles in Go"
categories: note
---

- What are [test doubles](https://en.wikipedia.org/wiki/Test_double)?
- Using interfaces to inject test doubles in Go

```golang
type logger interface {
	Info(msg string)
}

func Do(logger logger) {
	logger.Info("running do function")
}
```

- Benefits of generating test doubles for interfaces
  - No need to hand-rolling each test double
  - Enables consistency in a project
  - Thread-safe test doubles
- Special-case test doubles like [`code.cloudfoundry.org/clock`](https://code.cloudfoundry.org/clock)
- My experience with [Counterfeiter](#counterfeiter)

Options:
- [Hand-rolled](#hand-rolled)
- [Counterfeiter](#counterfeiter)
- [Charlatan](#charlatan)
- [Pegomock](#pegomock)
- [minimock](#minimock)

## Roundup

### <a id="hand-rolled"></a> Hand-rolled
Write your own test doubles by hand

For example, [`fakes.HostKey`](https://github.com/cloudfoundry/socks5-proxy/blob/3659db090cb23a57807b53e2f8580b2427dc2659/fakes/host_key.go) implements the [`proxy.hostKey`](https://github.com/cloudfoundry/socks5-proxy/blob/3659db090cb23a57807b53e2f8580b2427dc2659/socks5_proxy.go#L20-L22) interface in the `github.com/cloudfoundry/socks5-proxy` package.

### <a id="counterfeiter"></a> Counterfeiter
> A tool for generating self-contained, type-safe test doubles in go
>
> [github.com/maxbrunsfeld/counterfeiter](https://github.com/maxbrunsfeld/counterfeiter)

### <a id="charlatan"></a> Charlatan
> Go Interface Mocking Tool
>
> [github.com/percolate/charlatan](https://github.com/percolate/charlatan)

### <a id="pegomock"></a> Pegomock
> Pegomock is a powerful, yet simple mocking framework for the Go programming language
>
> [github.com/petergtz/pegomock](https://github.com/petergtz/pegomock)

### <a id="minimock"></a> minimock
> Powerful mock generation tool for Go programming language
>
> [github.com/gojuno/minimock](https://github.com/gojuno/minimock)

## Conclusions
- Any preferences?
- Pros and cons?
- Anything else to consider?
