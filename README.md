Just found out about [Pigweed](https://pigweed.googlesource.com/) and wanted to
experiment with using it. This is that experiment.

Let's start off with just making a simple application that uses sysio and just
sends "Hello World!".

Later:
- Add tests
- Add docs
- Setup flake, etc.

Stretch:
- Support other targets
- Send protos via gRPC


## Design

It's not immediately obvious what the best way is to setup a project that uses
pigweed. I'm going to just setup a submodule in an `external` directory and see
how that works.

## Steps

- Add submodule

### Setup GN

- Copy BUILDCONFIG
- Modify XXX: show commit

Note: When setting up target builds, need to reference in pigweed, eg)

```
gn gen --args='pw_target_config = "//external/pigweed/repo/targets/stm32f429i-disc1/target_config.gni"' out/disco
```

NOT

```
gn gen --args='pw_target_config = "//targets/stm32f429i-disc1/target_config.gni"' out/disco
```
