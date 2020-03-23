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

NOTE: pre-push hook changed from

```
external/pigweed/repo/pw_presubmit/py/pw_presubmit/pigweed_presubmit.py --base origin/master..HEAD --program quick
```

to

```
external/pigweed/repo/pw_presubmit/py/pw_presubmit/pigweed_presubmit.py --base origin/master..HEAD --program quick --repository external/pigweed/repo
```

I'm assuming this is just completely ignoring my top-level project though, and
we'll want to revisit this later for formatting help, etc.

`pw watch` is getting a file limit issue, just updated `max_user_watches` to
10,000 with `sudo sysctl fs.inotify.max_user_watches=10000`.

Not getting tests of app to run with `pw watch`.
> Had to specify test_group with `_run` appended to get it to run.
