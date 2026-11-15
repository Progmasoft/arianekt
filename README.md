<!-- SPDX-FileCopyrightText: 2026 Progmasoft <support@progmasoft.com> -->
<!-- SPDX-License-Identifier: MIT -->

# ArianeKt

ArianeKt brings the diagnostics of [Ariane](https://github.com/Progmasoft/ariane) to Kotlin: reports drawn over the
source code they are about, with labels, notes and helps, by the Rust library Ariadne behind Ariane's C API.

It is for Kotlin/JVM 25 and later only. It reaches Ariane's C API through the Foreign Function and Memory API of
the JVM. Its builds are published to the Maven repository of Progmasoft:

```kotlin
repositories {
    maven("https://maven.progmasoft.com/wrapper")
}

dependencies {
    implementation("com.progmasoft.arianekt:arianekt-ffm:$arianektVersion")
}
```

No code is written yet; the first version of ArianeKt follows the first release of Ariane.

## Why not JAriane?

[JAriane](https://github.com/Progmasoft/jariane) works from Kotlin too, but it is written for Java: for every JVM
language that calls Java, from Java 21 on. ArianeKt is written for Kotlin alone, and uses what only Kotlin has:

- **A DSL for reports.** A report is written as a block, such as `report(Kind.ERROR, span) { message = "..." }`,
  with Kotlin's receivers and `@DslMarker`, in place of builders and setters.
- **Kotlin types for the API.** Optional values are nullable types, kinds and colors are sealed and value classes,
  and a failure is a sealed result read with `when`, in place of status codes and exceptions.
- **Extension functions and named arguments**, so a source or a span is made the way Kotlin code reads, with
  defaults in place of overloads.
- **Kotlin's way to release native memory.** Sources and reports are `AutoCloseable`, taken with `use { }`.
- **No JNI glue.** On JVM 25, the Foreign Function and Memory API calls the C API directly: ArianeKt ships no native
  code of its own, where JAriane, which has to run on Java 21, needs JNI.

## The Ariane family

| Repository | For |
| --- | --- |
| [Progmasoft/ariane](https://github.com/Progmasoft/ariane), Ariane | C, through its C API |
| [Progmasoft/arianex](https://github.com/Progmasoft/arianex), Arianex | C++17 |
| [Progmasoft/jariane](https://github.com/Progmasoft/jariane), JAriane | Java 21+ and the JVM 21+ languages with Java interop |
| [Progmasoft/arianekt](https://github.com/Progmasoft/arianekt), ArianeKt | Kotlin/JVM 25+ |
| [Progmasoft/ariane.net](https://github.com/Progmasoft/ariane.net), Ariane.NET | the .NET 8+ languages |

## License

[MIT](LICENSE.txt). Progmasoft's own code is also covered by the [Progmasoft Patent Grant 1.1](PATENTS.md).
Participation follows the [Code of Conduct](CODE_OF_CONDUCT.md).
