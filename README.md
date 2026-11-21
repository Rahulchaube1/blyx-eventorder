<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin lifting an out-of-order clock tile from a row of log entries.">

# EventOrder

Locate time-order anomalies in a log stream in receipt order. This Blyx library is part of the audit, identity and reliability collection.

Sorting an export by timestamp can conceal a clock rollback. Audit receipt order and sequence continuity as separate signals. [OpenTelemetry, logs data model](https://opentelemetry.io/docs/specs/otel/logs/data-model/)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-eventorder.git
cd blyx-eventorder
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-eventorder) · [Package page](https://www.blyx-lang.space/packages/eventorder) · [Handbook](https://doc.blyx-lang.space/guide/barnowl)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-eventorder.git vendor/eventorder
```

```blyx
use vendor::eventorder::eventorder;

fn main() {
    let times = [10, 13, 11, 11];
    let result = eventorder_scan(times);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
2
2
```

## API

`eventorder_scan(times)`

Returns [adjacent clock reversals, largest backward step, first reversal index]. Equal timestamps preserve order. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| times | Vector of values, each a exact signed integer |

## In use

[Barnowl](https://github.com/Rahulchaube1/blyx-barnowl) uses this module to inspect a supplied audit export for sequence gaps, replays and clock reversals.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-eventorder/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
